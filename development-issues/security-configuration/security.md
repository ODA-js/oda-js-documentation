# Configuring security of API schema

## Resolving different user information

There is two kinds of user information that security middleware is need. First is how to get user from the system schema. Second how to determine what information it can access.

Look to `api4/src/app.ts`

```javascript
[...]
 passport.init(app, passportLib, resolveUser);
[...]
 app.use(middleware.ownerDiscovery(resolveOwner));
[...]
```

The two library methods `resolveUser` and `resolveOwner` is responsible for getting those two kind of information from the system.

### Resolving user information

For resolving user we make next steps:

* request user from the system using system-schema for the application.
  * if user has `admin` role in main organization then we decide that this is `system` user.
  * if user has `admin` role in currently connected organization then we decide that this is `admin` user for that specific organization
  * if user has any profile in selected organization then we decide that is is `owner` user.
  * otherwise user is `pulbic` and we restrict the access to him
* return this information to the system

The source of `api4/src/model/resolvers/user.ts`

    import { SystemGraphQL } from '../runQuery';

    export const getUser = (id: string) => {
      return SystemGraphQL.query({
        query: `
          query getUser($userId: ID) {
            user(id: $userId) {
              id
              userName
              enabled
              isAdmin
              isSystem
              owner
              userSetting {
                selectorId
              }
              userProfiles:userOrganizationProfiles{
                edges{
                  node{
                    orgProfile:organizationProfile {
                      organization {
                        id
                      }
                      profileType{
                        key
                      }
                    }
                  }
                }
              }
            }
          }
        `,
        variables: {
          userId: id,
        },
      }).then(
        (res) => {
          if (res.data && res.data.user) {
            let user = res.data.user;
            let selectorId = user.userSetting ? user.userSetting.selectorId : null;
            let result = {
              id: user.id,
              userName: user.userName,
              enabled: user.enabled,
              isAdmin: user.isAdmin,
              isSystem: user.isSystem,
              owner: user.owner,
              userSetting: user.userSetting,
              profileName: user.profileName,
            };

            if (!result.isAdmin && selectorId) {
              result.isAdmin = user.userProfiles.edges
                .filter(edge => edge.node.orgProfile.organization.id === selectorId)
                .some(edge => edge.node.orgProfile.profileType.key === 'admin');
            }
            if (result.isAdmin) {
              result.profileName = 'admin';
            }
            if (!result.isSystem) {
              result.isSystem = user.userProfiles.edges
                .filter(edge => edge.node.orgProfile.organization.id === 'T3JnYW5pemF0aW9uOmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZg==')
                .some(edge => edge.node.orgProfile.profileType.key === 'admin');
            }
            if (result.isSystem) {
              result.profileName = 'system';
            }
            if (!result.profileName) {
              let selected = selectorId ? user.userProfiles.edges
                .filter(edge => edge.node.orgProfile.organization.id === selectorId)[0]
                : null;

              if (selected) {
                result.profileName = selected.node.orgProfile.profileType.key;
              } else {
                result.profileName = 'public';
              }
            }
            return result;
          }
        }).catch(e => {
          throw e;
        });
    };



### Resolving owner information

For resolving owner information we make same steps as for dicovering user information with some specific additions.

To make security check we need know the label of security for specific user.

**Label of Security **is the global id of somthing that owns the data in the system.

In our case it is user.id and organization.id. So to make security check successfull we need to 
- Detemrime the user status: `system`, `admin`, `owner` of `public` user
 
- return as result list of global object id for each of the next arifacts:
 - user
 - user.owner
 - id for each organization where the user has profile of any kind.
 - if user isAdmin we need to retur also list of ids of user of selected organization.

The source of `api4/src/model/resolvers/owner.ts`

```javascript
import { SystemGraphQL } from '../runQuery';

export const getOwner = (id: string) => {
  return SystemGraphQL.query({
    query: `
      query getUserOwner($userId: ID) {
        user(id: $userId) {
          id
          userName
          enabled
          isAdmin
          isSystem
          owner
          userSetting{
            selectorId
          }
          userProfiles:userOrganizationProfiles{
            edges{
              node{
                orgProfile:organizationProfile {
                  organization {
                    id
                  }
                  profileType{
                    key
                  }
                }
              }
            }
          }
          profiles:userOrganizationProfiles{
            edges{
              node{
                profile:organizationProfile{
                  organization{
                    id
                    profiles:organizationProfiles{
                      edges {
                        node {
                          users:userOrganizationProfiles{
                            edges{
                              node{
                                user{
                                  id
                                }
                              }
                            }
                          }
                        }
                      }
                    }
                  }
                  profileType{
                    key
                  }
                }
              }
            }
          }
        }
      }
    `,
    variables: {
      userId: id,
    },
  }).then(
    (res) => {
      if (res.data && res.data.user) {
        let user = res.data.user;
        let result = {
          id: user.id,
          userName: user.userName,
          enabled: user.enabled,
          isAdmin: user.isAdmin,
          isSystem: user.isSystem,
          owner: user.owner,
          userSetting: user.userSetting,
          ownerIds: {},
        };

        let selectorId = user.userSetting ? user.userSetting.selectorId : null;
        if (!result.isAdmin && selectorId) {
          result.isAdmin = user.userProfiles.edges
            .filter(edge => edge.node.orgProfile.organization.id === selectorId)
            .some(edge => edge.node.orgProfile.profileType.key === 'admin');
        }
        if (!result.isSystem) {
          result.isSystem = user.userProfiles.edges
            .filter(edge => edge.node.orgProfile.organization.id === 'T3JnYW5pemF0aW9uOmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZg==')
            .some(edge => edge.node.orgProfile.profileType.key === 'admin');
        }

        if (!result.isSystem) {
          result.ownerIds[user.id] = 1;
          result.ownerIds[user.owner] = 1;

          if (user.profiles && user.profiles.edges.length > 0) {
            user.profiles.edges.forEach(edge => {
              if (edge.node && edge.node.profile
                && edge.node.profile.organization) {
                result.ownerIds[edge.node.profile.organization.id] = 1;
                if (edge.node.profile.profileType.key === 'admin') {
                  edge.node.profile.organization.profiles.edges.forEach(pedge => {
                    pedge.node.users.edges.filter(e => e.node.user.id !== 'VXNlcjpmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmY=').
                      forEach(e => {
                        result.ownerIds[e.node.user.id] = 1;
                      });
                  });
                }
              }
            });
          }
        }
        return result;
      }
    }).catch(e => {
      throw e;
    });
};
```

## Setup security checks

The file `api4/src/model/hooks.ts` is responsible for security setup.

The model infrastructure has hooks-api to make generation-time modifications.

when we genearates the schema we use it like mentioned in `api4/src/generate.ts` and `api4/src/genUml.ts`.

the source of `generate.ts`-flie

```javascript
import * as  path from 'path';
import { generator } from '@charidy/graphql-backend-gen';
import schema from './schema';
import * as modelHooks from './model/hooks';

generator({
  // role: 'admin', // public, admin, system
  hooks: [
    // entities
    modelHooks.adapter,
    modelHooks.userCollectionName,
    // fields
    // fix default visibility
    modelHooks.accessFixEntities,

    modelHooks.defaultVisibility,
    modelHooks.dictionariesVisibility,

    // secure fields without default
    modelHooks.securityFields,
    modelHooks.ownerFields,
    // metadata
    modelHooks.securityAcl,
    modelHooks.ownerAcl,

    // mutations
    modelHooks.accessFixMutations,
    modelHooks.defaultMutationAccess,
    // id is visible by default to all
    modelHooks.defaultIdVisibility,
    // user
    modelHooks.userIsAdmin,
    modelHooks.userIsSystem,
  ] as any,
  pack: schema,
  rootDir: path.join(__dirname, '../src', 'graphql-gen'),
  config: {
    graphql: false,
    packages: true,
  },
});

```

### hooks

The hook tell the system wiich entities and how must be changed.

for example this hook updates all entities fields `createdBy`,`updateBy`,`createdAt`, `updatedAt` with metadata inoformation about acl, that is it only read for `admin`-user profile.


```javascript
export let securityAcl = {
  name: 'security',
  'entities.*.fields.[createdBy,updateBy,createdAt, updatedAt].metadata.acl.read': 'admin',
};
```

**selectors** 

`*` -  all listed subitems

`[...]` - only listed items

`^[...]` - all except listed items
 
**NOTE!!!**

hooks is just json files that can be packed in one line

for example this record `entities.User.fields.name.metatdata.acl.read:'owner'` will be transformed to 
```
{
  entities: {
    User:{
      fields:{
        name:{
          metadata:{
            acl:{
              read:'owner'
            }
          }
        }
      }
    }
  }
}
```

**Using this hooks developer can shape model to any structure of model he need.
**
