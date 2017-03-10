# Project Folder Structure

The project is managed as [monorepo](https://www.npmjs.com/package/multipack#what-does-such-a-monorepo-look-like). It means that all developed services must be rely on the same project folder. It allows us to reuse same libraries and packages between the different services without creating duplicates in the project.

```
charidy-server/
    api4/
    api-images/
    auth/
    beAdmin/
    config/
    common/
    lib/
    static/
    site/
    uploads/
    ...
```
## Folder 

* api4 - root folder for api
* api-images - root folder for the service of image uploading
* auth - root folder for authentication service
* beAdmin - root for current admin project
* config - root folder for configuration files
* common - root folder for common functions for every project.
* lib - root folder for the universal libraries for every project.
* statics - root for common static files. It is used by `webpack-dev-server` indevelopment and it stores compiled client scripts.
* site - root for Charidy site project
* graphiql - root folder for custom GraphQL service (see [Using GraphQL](/working-with-graphiql.md))
* uploads - directory for the uploaded files