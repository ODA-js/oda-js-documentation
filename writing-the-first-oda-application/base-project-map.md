## Base project map

Base project files described below:<br> 

```
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
    ...
  package.json
  ...
```

* **bin/www** -  init start file;<br>
* **config/** - development configuration files;<br>
* **src/schema/** - contain project schema;<br>
* **src/schema/entities/** - folder where your [entities](/writing-the-first-oda-application/schema-creation.md) are stored;<br>
* **src/schema/mutations/** - folder where your custom [mutations](/writing-the-first-oda-application/queries-and-mutations.md) are stored;<br>
* **src/schema/packages/** - contain GenUML (Generator of UML diagrams for current schema) configuration.
