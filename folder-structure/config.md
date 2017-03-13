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
    "site": {
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
    "security": {
      "host": "localhost",
      "port": 3002,
      "dev": {
        "port": 3002
      }
    }
  },
  "db": {
    "api": {
      "url": "mongodb://localhost/testGen"
    },
    "session": {
      "url": "mongodb://localhost/charidy"
    }
  },
  "passport": {
    "salt2": "002bb4cd957c5e35586dd710b2eb485d83fd5641",
    "secret": "THE VERY secret ONE",
    "expiresIn": "1h"
  }
}
```



