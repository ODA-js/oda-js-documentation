# Configuring security of API schema

## Resolving user information

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

