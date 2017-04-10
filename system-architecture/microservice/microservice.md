# Microservice architecture

We have next types of services:

* UI-rich
* API-rich
* Combined

**UI-rich** can be any react application with `react-router` driven routing. It is provide UI routes for application. The example is Admin-UI itself.

**API-rich** is module that provide some api-calls. Data-layer that is build with GraphQL is a API-rich. As UI-rich application API-rich module can be any node.js application or other platform that provide specific url-routes for its API.

**Combined** service can provide both API and UI for system. Auth-UI expose login-system functionality for the application.
Each application can be deployed to different location to provide horizontal scalability.
We've prepared configuration files for building javascript projects and starter seed-projects to start building.
