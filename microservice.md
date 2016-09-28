# Microservice architecture

We have next types of services:

* UI-rich
* API-rich
* Combined

**UI-rich** can be any react application with `react-router` driven routing. It isprovide UI routes for application. The example is Admin-UI itself.

**API-rich** is module that provide some api-calls. Data-layer that is build withGraphQL is a API-rich. As UI-rich application API-rich module can be any node.jsapplication or other platform that provide specific url-routes for its API.

**Combined** service can provide both API and UI for system. Auth-UI exposelogin-system functionality for the application.

Each application can be deployed to different location to providehorizontal scalabillity.

we've prepared configuration files for building javascript projects andstarter seed-projects to start building.


