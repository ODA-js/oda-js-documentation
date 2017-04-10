# Network architecture

## Overall stricture

The overall network architecture consists of next parts:

- Main Web-server;
- Admin UI-Rich service;
- Authentication UI-Rich service;
- File-upload api-rich service;
- GraphQl-backend api-rich service;
- mongodb database service.

![](/assets/Diagrams for Charidy.png)

## Network service dependencies

### Main Web-server
In current state it is just a concept, that will aggregate different services, that will provide for users specific features for the  system.  

### Admin
It is built on-top of react.js, and uses isomorfic javascript code.
Admin panel is the separate UI-rich service, which uses:
- authentication service
- file-upload service
- graphql service

### File-upload service

It is built using plane node.js on-top of express.js.
Right now it is not using any service.

### Authentication service

It is built using react.js, and uses isomorfic javascript code.

It uses:
- graphql-backend service

### GraphQL-backend service

It is build using [apollodata](http://www.apollodata.com) for server.

It is uses:
- mongodb database serice.

## Security 

We use token based authorization and authentication. see [jwt.io](https://jwt.io) for more information.

### Authentication
Once user is authenticated authorization layer is generates auth token with specified lifetime. in developer configuration token lives 1h. After it expired user need to login once more to recreate token.

Services didn't uses any session store to avoid storing cookies on client.
Authentication mechanism check if user is enable once per each request.

### Authorization

The system has 4 main group of user, each of which uses different data schema, to avoid api-hacking by third parties.

Athorization groups^
- System,
- Admin,
- Owner,
- Public.

#### System

It is users that belongs to main organization and has admin profile. The have unrestricted access to any data in the system. This rights can be granted or direct or indirectly.

#### Admin

It is admin users of customer company, it have unrestricted access within its company.

#### Owner

It is users of the customer company just as viewers, fundraising profile, manages and etc. Its access it restricted according to specified rules for specified type of users.


#### Public

It is any unauthenticated user. Public users can see only public dictionaries and make login operation.

