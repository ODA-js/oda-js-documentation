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
* **oposite** - to be used only with Target relation. It contains field name in Source relation, where this relation can be found.<br>
<li>using - use only for many-to-many relations.It contains:  `using: 'NameTableBundle#idFieldName`<ol>`NameTableBundle` - name of bundle table.This entity can be created manually or ODA can create it automatically.<br>`idFieldName` - can be empty or contain name of the key that will be used for bind. By default, 'idFieldName`   is 'id'.</ol></li>
### Type of relations:
ODA system use following type of relations:
<li>one-to-one(1:1). Full description about this relation you can find by the link [One-To-One Associations](http://docs.sequelizejs.com/en/v3/docs/associations/#one-to-one-associations)
<li>one-to-many(1:n). Full description about this relation you can find by the link [One-To-Many Associations](http://docs.sequelizejs.com/en/v3/docs/associations/#1m)
<li>many-to-many(m : n). Full description about this relation you can find by the link [Many-To-Many Associations](http://docs.sequelizejs.com/en/v3/docs/associations/#nm)


