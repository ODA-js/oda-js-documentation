## Queries and Mutation

1. Open your browser and go by link: [Localhost:3003/graphiq](/Localhost:3003/graphiq)
2. GraphiQL editor will be opened. You can create graphql-queries using this editor. You can read more about GraphQL [here](http://graphql.org/learn/)
![](/assets/356.png)
3. Put graphql-queries in left block of editor.
4. Click 'Run query' button and choose one of available queris.
5. The result of the query will be displayed in the right block.
6. Click 'Docs' button if you want to see the documentation about mutations and queries.

### Mutations
'Mutation' - list of all actions, that you can do with your models(create, delete, update, assign, reassign). For example: let's add add mutation 'createStudent':


```
mutation createStudent{
  createStudent(input:{
    firstName: "StudentName",
    lastName: "StudentLasname",
    uin: "jiherig-4fj98734-c8h78-erfr"
  }) {
    student {
      node {
        id
        firstName
        lastName
      }
    }
  }
}
```

