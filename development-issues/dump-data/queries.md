# Initial Load

The Queries for the loaderConfig are placed in the `api4/data/queries` folder. Every entity has it's own folder named by the name of the entity.  
For example, there's **Organization** entity \(`api4/data/initialLoad/Organization`\).

Every imported entity needs queries:

* **create.graphql**

  ```javascript
  mutation createOrganization($organization:createOrganizationInput!) {
    createOrganization(input:$organization) {
      organization {
        node {
          ...ViewOrganization
        }
      }
    }
  }
  ```

  **Note: **You can replace _organization_ by the name of any entity. The same works for other queries too.

* **findByName.graphql**

  ```javascript
  query findOrganizationByName($name: String){
    organization(name:$name) {
      ...ViewOrganization
    }
  }
  ```

* **update.graphql**

  ```javascript
  mutation updateOrganization($organization:updateOrganizationInput!) {
    updateOrganization(input:$organization) {
      organization {
        ...ViewOrganization
      }
    }
  }
  ```

* **view.graphql**

  ```javascript
  fragment ViewOrganization on Organization {
    id
    name
  }
  ```

If the entity has relations, it also will need relating query. In our example it is

* **assignToProfileType.graphql**

```javascript
mutation assignOrganizationToProfileType($connection:addToOrganizationBelongsToManyProfileTypesInput!){
  addToOrganizationBelongsToManyProfileTypes(input:$connection){
    organization{
      ...ViewOrganization
    }
  }
}
```

All queries and mutations from this section are described in [Documentation Explorer](/working-with-graphiql/documentation-explorer.md) and can be checked in [GraphQL](/working-with-graphiql.md).

