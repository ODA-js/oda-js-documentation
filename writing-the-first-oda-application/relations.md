  ## Relations

Let' s look at example of relation field. 

**Note: Source relation - it's mean source relation model. Target relation - it's mean slave relation model.**<br>


```
  ...
      profile: {
        indexed: true,
        relation: {
          hasOne: 'StudentProfile#',
        },
      },
  ...

```
<br>

**Note: field with relation section should contain flag "indexed: true".**<br>

Relation section can contain:
* **relation type** - it can be "source" (**hasOne** or **hasMany**)  or "target" relation (**belongsTo** or **belongsToMany**);<br>
* **oposite** - **to be used only with relation of "target" type**. It contains field name in "source" relation, where this relation can be found.<br>
* **using** - use only for **many-to-many** relations.It contains:<br>
`using: 'NameTableBundle#idFieldName`<br>
  * **"NameTableBundle"** - name of bundle table.This entity can be created manually or ODA can create it automatically.<br>
  * **idFieldName** - can be empty or contain name of the key that will be used for bind. **By default, idFieldName   is "id"**.<br><br>
  
### Type of relations:
ODA system use following types of relations:<br>
* "one-to-one" (1:1). [Full description of this relation can be found here](http://docs.sequelizejs.com/manual/tutorial/associations.html#one-to-one-associations).<br>
* "one-to-many" (1:n). [Full description of this relation can be found here.](http://docs.sequelizejs.com/manual/tutorial/associations.html#one-to-many-associations)
<li>"many-to-many" (m : n). [Full description of this relation can be found here.](http://docs.sequelizejs.com/manual/tutorial/associations.html#scopes)


