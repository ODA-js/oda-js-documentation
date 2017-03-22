# Configuring security of API schema



##


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

### Restricting the mutation executation

This is the way to resctict execution of specific mutations for any groups of users.

```javascript
export let runtimeMutationAcl = {
  system: {
    '*': true,
  },
  admin: {
    createOrganization: false,
    deleteOrganization: false,
    createOrganizationCustom: false,
    '*': true,
  },
  user: {
    createOrganization: false,
    deleteOrganization: false,
    createOrganizationCustom: false,
    createUserAddOrganizationProfile: false,
    '^addTo': false,
    '^removeFrom': false,
    '*': true,
  },
  frs: {
    'updateUserSetting': true,
    '*': false,
  },
  public: {
    loginUser: true,
    '*': false,
  },
};
```

**Note!!!**

`*` means all not listed items within specified for each king of user schema.

For example:
the member of `public`-group can execute **ONLY** loginUser mutation.
the member of  `frs`-group can execute **ONLY** updateUserSetting mutation.
the member of  `user`-group can execute everything except:
  `createOrganization`, `deleteOrganization`, `createOrganizationCustom`, `createUserAddOrganizationProfile` and any mutations that starts with `addTo` or `removeFrom`.
  

