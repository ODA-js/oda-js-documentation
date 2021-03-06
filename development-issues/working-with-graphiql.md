# How to use GraphQL

In this section we will describe using of GraphQL.

You can access API viewer here: http://localhost:3003/graphiql

It looks like this:

![](/assets/graphiQl.png)

To view data, you must first insert API sample in left part, and then click on ![](/assets/image1_1.png) button, and API will be executed.

For example, you can try this API request to create an organization:

```
mutation createOrganization {
  createOrganization(input: {
  name: "TestOrganization", 
  about: "Test Organization For Test Purposes", 
  analyticId: "analyticId"}) {
    organization {
      node {
        id
        name
        about
        analyticId
      }
    }
  }
}
```

Replace "**OrganizationName**", "**Organization description**" and "**analyticId**" with desired organization name, description and Analytics ID, and push execute button. Result will look like this: 

![](/assets/image2.png)

As you can see, created organization will instantly get ID, and the rest data \(name, description and AnalyticID\) will be as was set in request.

