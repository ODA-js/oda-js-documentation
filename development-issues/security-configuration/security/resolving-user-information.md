# Resolving user information

For resolving user we make next steps:

* request user from the system using system-schema for the application.
  * if user has `admin` role in main organization then we decide that this is `system` user.
  * if user has `admin` role in currently connected organization then we decide that this is `admin` user for that specific organization
  * if user has any profile in selected organization then we decide that is is `owner` user.
  * otherwise user is `pulbic` and we restrict the access to him
* return this information to the system

The source of `api4/src/model/resolvers/user.ts`

```javascript

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

```

