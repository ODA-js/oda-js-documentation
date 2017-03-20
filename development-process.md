# Development Environment

* `node.js` is the platform for development,
* `javascript ES2016 +` is the main language for the project
* `Relay` is the data-layer
* `React` is the viewing engine
* `babel.js` is teh transpiler for the javascript

##  Project initialization

Project repository is [charidy-server](http://gitlab.pfrus.com/vedmalex/charidy-server).

## Developer environment setup

We prefer to use [Visual Studio Code (VSCode)](https://code.visualstudio.com/). The project contains all settings to the editor. It make the code environmet feel and look the same between different developers.

to use VSCode you need to install next plugins:

* [Babel ES6/ESt7](https://marketplace.visualstudio.com/items?itemName=dzannotti.vscode-babel-coloring)
* [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

### ESLint

To use ESlint plugin you need to install it globally:

```
npm i -g eslint
```

## install project dependency

run in root directory of project

```
npm run fullbuild
```

## Start working with code

open terminal in root project and type

```bash 
code .
```




