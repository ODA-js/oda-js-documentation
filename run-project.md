# Run project

if not yarn or typescript is not installed:
```
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
$ sudo apt-get update && sudo apt-get install yarn
$ sudo npm i -g typescript
```

for the install dependence and run project:

```
$ npm run fullinstall
// in other terminals
$ npm run dev
// in other terminals
$ npm run dev-api
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



