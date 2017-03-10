# Queries 

The Queries for the loaderConfig are placed in the `api4/data/queries` folder. Every entity has it's own folder named by the name of the entity.
For example, get **InviteMatcher** entity (`api4/data/queries/InviteMatcher`).

Every imported/exported entity needs queries:
* **create.graphql**
```javascript
mutation createInviteMatcher($inviteMatcher:createInviteMatcherInput!){
  createInviteMatcher(input:$inviteMatcher){
    inviteMatcher{
      node {
        ...ViewInviteMatcher
      }
    }
  }
}
```
**Note: **You can replace _InviteMatcher_ by the name of any entity. The same works also for other queries.
 
* **findById.graphql**
```javascript
query findInviteMatcherById($id:ID){
  inviteMatcher(id: $id){
    ...ViewInviteMatcher
  }
}
```
* **list.graphql**
```javascript
query InviteMatchers {
  viewer{
    inviteMatchers{
      edges{
        node{
          ...ViewInviteMatcher
        }
      }
    }
  }
}
```
* **update.graphql**
```javascript
mutation updateInviteMatcher($inviteMatcher:updateInviteMatcherInput!){
  updateInviteMatcher(input:$inviteMatcher){
    inviteMatcher{
      ...ViewInviteMatcher
    }
  }
}
```

* **view.graphql**
```javascript
fragment ViewInviteMatcher on InviteMatcher {
  type
  displayName
  id
}
```

* **export.graphql**
```javascript
query ExportInviteMatchers {
  viewer{
    inviteMatchers{
      edges{
        node{
          ...ExportInviteMatcher
        }
      }
    }
  }
}
```

* **exportFragment.graphql**
```javascript
fragment ExportInviteMatcher on InviteMatcher {
  ...ViewInviteMatcher
  invitedMatcher {
    edges {
      node {
        ...ViewInvitedMatcher
      }
    }
  }
}
```


If the entity has relations, it also will need relating query. In our example it is
* **assignToInvitedMatcher.graphql**

```javascript
mutation assignInviteMatcherToInvitedMatcher($connection: addToInviteMatcherHasManyInvitedMatchersInput!){
  addToInviteMatcherHasManyInvitedMatchers (input:$connection){
    inviteMatcher{
      ...ViewInviteMatcher
    }
  }
}
```
All queries and mutations from this section is described in [Documentation Explorer](/working-with-graphiql/documentation-explorer.md) and can be checked in [GraphQL](/working-with-graphiql.md).