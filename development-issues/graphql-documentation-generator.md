#Graphql documentation generator

To generate documentation from graphql endpoint we use [graphdoc](https://github.com/2fd/graphdoc)

## install 

`npm install -g @2fd/graphdoc`

## use 

`graphdoc -s ./schema.json -o ./doc/schema`

## update project's package.json

```
    {
        "name": "project",
        "graphdoc": {
            "endpoint": "http://localhost:8080/graphql",
            "output": "./doc/schema",
        }
    }
```