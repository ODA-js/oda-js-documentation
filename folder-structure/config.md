# Configuring appilcation

## Tooling

Node.js module [config](https://www.npmjs.com/package/config) is intended to store and use different configurations for the appilcation. It use json format to store specific parameters for applciation.

## file structure in common

all configudation for file layout is relative to root fol

```json
{
  "AppName": "@charidy/new",
  // path to static folder
  // !!! NOTE: the last '/' is required
  "statics": "/public/", // path to url last / is required!!!
  "hosts": {
    "api": {
      "host": "localhost",
      "port": 3003
    },
    "api-images": {
      "host": "localhost",
      "port": 3004
    },
    "auth": {
      "host": "localhost",
      "port": 2999,
      "dev": {
        "port": 3012
      }
    },
    "admin": {
      "host": "localhost",
      "port": 3000
    },
    "app": {
      "host": "localhost",
      "port": 3001,
      "dev": {
        "port": 3011
      }
    },
  },
  "db": {
    "api": {
      "url": "mongodb://localhost/testGen"
    }
  },
  "passport": {
    "salt2": "002bb4cd957c5e35586dd710b2eb485d83fd5641",
    "secret": "THE VERY secret ONE",
    "expiresIn": "1h"
  }
}
```

## sections of configuration

* AppName -- application name
* statics -- configuration of static files path for web servers.
* hosts -- configuration of mictoservices, is user by app loader
* db --  database configuration
* passport -- security schema

### `hosts` section

it contains root cofnguration for specific services.

In the sample we have several roots. the structure is not strict, but we have to configure micoservicec in the same way:

- host
- port
- dev -- development configuration. it is user for UI-Rich sevices

the key of json-object is the configured name of the project? than mentioned in `package.json` of the project.

```json
{
  "name": "api", //!!!<<<<
```
the name means that it will take configuration from the section `api`.

### `db` section

Here we configure db connection strings

### usage specfics

as far as we use single file configuration, we need to provide `config` with information about location. So we user node.js library `env`.

to use it we need to:

1. create `.env`-file in the specific service root folder
2. edit it with the environment variables values? just like this

```
NODE_CONFIG_DIR=../config
STATIC_ROOT=./public
```
`NODE_CONFIG_DIR` it is the path for configuration file.

### file namings and multiple configurations


