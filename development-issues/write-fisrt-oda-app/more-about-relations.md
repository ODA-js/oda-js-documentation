# Relation


Example **relation** field.
**Note**:
* *Source* relation - it mean relation **Master** model
* *Target* relation - it mean relation **Slave** model

```js
    ...
      profile: {
        indexed: true,
        relation: {
          hasOne: 'StudentProfile#',
        },
      },
    ...
```
**Noote**: field with relation section should contain flag `indexed: true`.

Relation section can contain:

  * **hasOne** or **hasMany**(*Source* relation) or **belongsTo** or **belongsToMany**(*Target* relation) - type of relation
  * **oposite** - use only with *Target* relation. It conain name of field in *Source* relation's entity where it relation can be find.
  * **using** - use only for many-to-many relations. It contain: 

    ```js
      using: 'NameTableBundle#idFieldName'
    ```

 1) `<NameTableBundle>` - name of table bundle. It entity can be create manualy or ODA create it automaticaly
 2) `<idFieldName>` - name of id that use for bind or empty.
**Note**: By default `<idfieldName>` is `'id'`. Leave the field empty:

     ```js
       using: 'NameTableBundle#'
     ```
  
# Type of relations:

ODA use **one-to-one**(1 : 1), **one-to-many**(1 : n) and **many-to-many**(m : n) relations

# Relation one-to-one(1 : 1)

Description points of relation.

| Entity 1 | Entity 2 |
| --- | --- |
| `hasOne: <NameEntity2>#<idFieldEntity2>`| `belongsTo: <NameEntity1>#<idFieldEntity1>` |
|  | `oposite: <indexedFieldEntity1>` |

***Example***: 
Student relations with StudentProfile.  
File _Student.ts_:

```js
    ...
    profile: {
      indexed: true,
      relation: {
        hasOne: 'StudentProfile#',
      },
    },
    ...
```

File _StudentProfile.ts_:

```js
    ...
    student: {
      indexed: true,
      relation: {
        belongsTo: 'Student#',
        opposite: 'profile',
      },
    },
    ...
```


All descriptions you can find by link [One-To-One Associations](http://docs.sequelizejs.com/en/v3/docs/associations/#one-to-one-associations)

# Relation one-to-many(1 : n)

| Entity 1 | Entity 2 |
| --- | --- |
| `hasMany: <NameEntity2>#<idFieldEntity2>` | `belongsTo: <NameEntity1>#<idFieldEntity1>` |
|  | `oposite: <indexedFieldEntity1>` |

StudentsGroup has many Students. Student belongs to one StudentsGroup.  
File _StudentsGroup.ts_:

```js
    ...
    students: {
      indexed: true,
      relation: {
        hasMany: 'Student#',
      },
    },
    ...
```

File _Student.ts_:

```js
    ...
    group: {
      indexed: true,
      relation: {
        belongsTo: 'StudentsGroup#',
        opposite: 'students',
      },
    },
    ...
```

All descriptions you can find by link [One-To-Many Associations](http://docs.sequelizejs.com/en/v3/docs/associations/#1m)


# Relation one-to-many(m : n)

| Entity 1 | Entity 2 |
| --- | --- |
| `hasMany: <NameEntity2>#<idFieldEntity2>` | `belongsToMany: <NameEntity1>#<idFieldEntity1>` |
| `using: <NameTableBundle>#<idFieldEntity1>` | `using: <NameTableBundle>#<idFieldEntity2>` |
|  | `oposite: <indexedFieldEntity1>` |

StudentsGroup relations with Subjects.  
File _StudentsGroup.ts_:

```js
    ...
    subjects: {
      indexed: true,
      relation: {
        belongsToMany: 'Subject#',
        using: 'StudentsGroupSubject#',
        opposite: 'groups',
      },
    },
    ...
```

File _Subject.ts_:

```js
    ...
    groups: {
      indexed: true,
      relation: {
        belongsToMany: 'StudentsGroup#',
        using: 'StudentsGroupSubject#',
      },
    },
    ...
```

All descriptions you can find by link [Many-To-Many Associations](http://docs.sequelizejs.com/en/v3/docs/associations/#nm)


