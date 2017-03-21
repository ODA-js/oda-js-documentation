# Network architectiure

## Overall stricture

The overall network architecture cosists of next parts:

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
- authenication service
- file-upload service
- graphql service

### File-upload service

it is built using plane node.js on-top of express.js.
Right now it is not using any service.

### Authentifiction service

It is built using react.js, and uses isomorfic javascript code.

it uses:
- graphql-backend service

### GraphQL-backend service

it is build using [apollodata](http://www.apollodata.com) for server.

it is uses:
- mongodb database serice.

## Security 

We use token based authorization and authetification. see [jwt.io](https://jwt.io) for more information.

### Authentication
Once user is autheticated authorization layer is generates auth token with specified lifetime. in developer configuration token lives 1h. After it expired user need to login once more to recreate token.

Services didn't uses any session store to avoid storing cookies on client.
Authetication mechanizm check if user is enable once per each request.

### Authorization

The system has 4 main group of user, each of wich uses different data schema, to avoid api-hacking by third parties.

Athorization groups^
- System,
- Admin,
- Owner,
- Public.

#### System

It is users that belongs to main organization and has admin profile. the have uresticted access to any data in teh system. This rights can be granted or direct or indirectly.

#### Admin

It is admin users of customer company, it have unrestricted acces within its company.

#### Owner

It is users of the customet company just as viewers, fundrising profile manages and etc. Its access it restricted accorrding to specified rules for specified type of users.


#### Public

It is any unathentificated user. Public users can see only public dictionaries and make login operation.

