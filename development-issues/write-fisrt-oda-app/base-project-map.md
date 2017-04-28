# File generators

Some part of project generate from **src** files.
The main files is:

```bash
  bin/
    www
  config/
    default.json
    production.json
  src/
    schema/
      entities/
      mutations/
      packages/
  package.json
```

`package.json` - main project config file
`bin/www` - init start file
`config/` - development config files
`src/schema/` - contain project schema
`src/schema/entities/` - put your model here
`src/schema/mutations/`- put your custom mutations here
`src/schema/packages/` - contain GenUML configuration
