# Project Folder Structure

The project is managed as [monorepo](https://www.npmjs.com/package/multipack#what-does-such-a-monorepo-look-like). it is means that all developed services must be rely on the same project folder. it allow us to reuse same libraries and packages between different services without creating duplicates in the project.

```
charidy-server/
    api/
    auth/
    beAdmin/
    config/
    data/
    lib/
    static/
    ...
```
## Folder 

* api - root folder for api
* auth - root folder for authentication service
* beAdmin - root for current admin project
* config - root folder for configuration files
* data - schema store for Relay data layer
* lib - root folder for common functions for every projects.
* statics - root for common static files. it is used by `webpack-dev-server` indevelopment and stores compiled client scripts.



