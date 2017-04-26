# Development Environment

* `node.js` is the platform for development,
* [nvm install](https://github.com/creationix/nvm#install-script) to node js instalaltion
* `nvm install v7; nvm use v7` to install node.js

## Project initialization

Project repository is [oda-boilerplates](http://gitlab.pfrus.com/vedmalex/oda-boilerplates.git).

## Developer environment setup

We prefer to use [Visual Studio Code \(VSCode\)](https://code.visualstudio.com/). The project contains all settings to the editor. It make the code environmet feel and look the same between different developers.

## Install project dependency
copy api-sample package to other directory(ubuntu example):

```
mkdir new-api-name
cp -rp oda-boilerplates/packages/api-sample/* new-api-name/

```

run in root directory of project

```bash
npm i
npm run compile
npm start
```

## Start working with code

open terminal in root project and type

```bash
code .
```



