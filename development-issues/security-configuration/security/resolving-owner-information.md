# Resolving owner information

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

