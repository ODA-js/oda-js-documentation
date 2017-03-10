# Loader config

Lets look on the simple example of the import/export configuration. 
**api4/src/seeds/loaderConfig.ts**
```javascript
export default {
  uri: 'http://localhost:3003/graphql',
  import: {
    queries: {
      InvitedMatcher: {
        filter: `{
          firstName
          lastName
          fullName
          id
          amount
          email
        }`,
        uploader: {
          findQuery: 'InvitedMatcher/findById.graphql',
          createQuery: 'InvitedMatcher/create.graphql',
          updateQuery: 'InvitedMatcher/update.graphql',
          dataPropName: 'invitedMatcher',
          findVars: (f) => ({ id: f.id }),
        },
      },
      InviteMatcher: {
        filter: `{
          type
          displayName
          id
        }`,
        uploader: {
          findQuery: 'InviteMatcher/findById.graphql',
          createQuery: 'InviteMatcher/create.graphql',
          updateQuery: 'InviteMatcher/update.graphql',
          dataPropName: 'inviteMatcher',
          findVars: (f) => ({ id: f.id }),
        }
      }
    },
    relations: {
      InviteMatcher: {
        invitedMatcher: {
          type: 'InvitedMatcher',
          filter: `{
            id
            invitedMatcher {
              id
            }
          }`,
          relate: 'InviteMatcher/assignToInvitedMatcher.graphql',
        }
      }
    },
  },
  export: {
    queries: {
      InvitedMatcher: {
        query: `InvitedMatcher/export.graphql`,
        process: (f) => ({
          InvitedMatcher: f.viewer.invitedMatchers ? f.viewer.invitedMatchers.edges.map(e => ({
            ...e.node,
          })) : [],
        }),
      },
      InviteMatcher: {
        query: `InviteMatcher/export.graphql`,
        process: (f) => ({
          InviteMatcher: f.viewer.inviteMatchers ? f.viewer.inviteMatchers.edges.map(e => ({
            ...e.node,
            invitedMatcher: e.node.invitedMatcher ? e.node.invitedMatcher.edges.map(d => d.node) : [],
          })) : [],
        }),
      },
    },
  },
};
```
This configuration describes: 
* **inviteMatcher** entity with id, type, displayName fields
* **invitedMatcher** entity with firstName, lastName, fullName, id, amount, email fields.
* **Relation** of these entities (InviteMatcher has many InvitedMatchers). (Learn more about [Relations](/update-schema.md))

The config contains 3 sections.
##### 1. Import, queries section
It describes a structure of the entities what you want to import. It uses the queries of _uploader_ section in the import process.
**FindQuery** finds an entity in a database by id or other unique field. If the entity doesn't exist, **createQuery** creates it. Else **updateQuery** updates the finded entity by the data from the dump. **findVars** returns the unique value of field which is used in findQuery.

The queries is placed in `api4/data/queries` folder. Every entity has it's own folder with it's own data fragments. 
**Note**: Learn more about Queries from the [Queries](/dump-data/queries.md) section.

##### 2. Import, relations section
It contains the relations between entities and has the next structure: 
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

##### 3. Export