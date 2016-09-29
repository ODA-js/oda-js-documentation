# Project Layout

Each service type have its own predictable folder structure.

the common parts of each project is the following:

```
/src
    index.js
/public
    /<serviceName>
.env
start.js
package.json
```

* `src` is the folder for source files.
* `src/index.js` is the main file for the current service
* `/public/<service name>` - static files folder, it can be configured through `.env`-file.
* `.env` is the config for environment variables that is be used in the project

```bash
NODE_CONFIG_DIR=../config
STATIC_ROOT=./public
```

* `start.js` starter file for the service

```javascript
require('dotenv').config({ silent: true });
require('../common/babel/server.babel');
require('./src');

```

* `package.json` npm project file that contains `<service name>` definition, description and external project dependency, as far as development dependency.

```javascript
{ 
 "version": "0.1.0",
 "name": "api",
 "description": "graffity GraphQL Server",
 "private": true,
 "scripts": { 
    "start": "node start.js" 
 }
}

```

