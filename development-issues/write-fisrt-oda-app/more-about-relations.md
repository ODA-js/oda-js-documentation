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
      using: 'TableBundleName#fieldName'
    ```

 1) `'TableBundleName'` - name of table bundle. It entity can be create manualy or ODA create it automaticaly
 2) `'fieldName'` - name of field that use for bind. By default `'id'` for example:

     ```js
       using: 'TableBundleName#'
     ```
  
# Type of relations:

ODA use **one-to-one**(1 : 1), **one-to-many**(1 : n) and **many-to-many**(m : n) relations

* **Relation one-to-one(1 : 1)**

Description points of relation.

| Entity 1 | Entity 2 |
| --- | --- |
| `hasOne: 'nameEntity2'#'indexedFieldEntity2'`| `belongsTo: 'nameEntity1'#indexedFieldEntity1` |
|  | `oposite: 'indexedFieldEntity1'` |

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

* **1 : n**

| Entity 1 | Entity 2 |
| --- | --- |
| hasMany | belongsTo |
| nameEntity1\#indexed field | nameEntity2\#identity field |

All descriptions you can find by link [One-To-Many Associations](http://docs.sequelizejs.com/en/v3/docs/associations/#1m)

* **m : n**

| Entity 1 | Entity 2 |
| --- | --- |
| belongsToMany | belongsToMany |
| nameEntity1\#identity field | nameEntity2\#identity field |

All descriptions you can find by link [Many-To-Many Associations](http://docs.sequelizejs.com/en/v3/docs/associations/#nm)


**2\)  1 : n**  
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

**3\)  m : n**  
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



