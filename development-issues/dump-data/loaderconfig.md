# Initial

Lets look at the simple example of the import configuration.  
**api4/src/seeds/initial.ts**

```javascript
export default {
  uri: 'http://localhost:3003/graphql',
  import: {
    queries: {
      User: {
        filter: `{
          id
          firstName
          enabled
          userName
          password
          isSystem
          owner
        }`,
        uploader: {
          findQuery: 'User/findByName.graphql',
          createQuery: 'User/create.graphql',
          updateQuery: 'User/update.graphql',
          dataPropName: 'user',
          findVars: (f) => ({ userName: f.userName }),
        },
      },
      Organization: {
        filter: `{
          id
          name
          owner
        }`,
        uploader: {
          findQuery: 'Organization/findByName.graphql',
          createQuery: 'Organization/create.graphql',
          updateQuery: 'Organization/update.graphql',
          dataPropName: 'organization',
          findVars: (f) => ({ name: f.name }),
        },
      }
    },
    relations: {
      User: {
        userSetting: {
          type: 'UserSetting',
          filter: `{
            userName
            userSetting {
              id
            }
          }`,
          relate: 'User/assignToUserSetting.graphql',
        },
      },
      Organization: {
        profileTypes: {
          singular: 'profileType',
          type: 'ProfileType',
          filter: `{
            id
            name
            profileTypes {
              key
            }
          }`,
          relate: 'Organization/assignToProfileType.graphql',
        },
      }
    },
  },
```

This configuration describes:

* **user** entity with id, firstName, enabled, userName, password, onwer fields
* **organization** entity with name, id,  owner fields.
* **Relations** entities. \(Learn more about [Relations](/update-schema.md)\)

The config contains 3 sections.

##### 1. Import, queries section

It describes a structure of the entities that you want to import. It uses the queries of _uploader_ section in the import process.  
**FindQuery** finds an entity in a database by id or other unique field. If the entity doesn't exist, **createQuery** creates it, else **updateQuery** updates the found entity by the data from the dump. **findVars** returns the unique value of field which is used in findQuery.

The queries are placed in `api4/data/queries` folder. Every entity has it's own folder with it's own data fragments.  
**Note**: Learn more about Queries from the [Queries](/dump-data/queries.md) section.

##### 2. Import, relations section

It contains the relations between entities and has structure like this:

```javascript
ParentEntity: {
  childEntityFieldName: {
  type: 'ChildEntity',
  filter: `{
    uniqueKeyOfParent
    childEntityFieldName {
      uniqueKeyOfChild
    }
  }`,
  relate: 'ParentEntity/assignToChildEntity.graphql',
  }
}
```

_Relate_ contains the path to the relating query.

