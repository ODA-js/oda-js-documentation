# Relation


Example **relation** field.
Next at text *Source* entity - it mean **Master** model
*Target* entity - it mean **Slave** model

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
It should contain flag **indexed: true**.
Relation section can contain:

  * **hasOne** or **belongsTo** or **hasMany** or **belongsToMany** - type of relation
  * **oposite** - use only with **belongsTo** or **belongsToMany** type. It conain name of field at *Source* entity where ODA can find current(*Target*) entity


Type of relations:

* **1 : 1**

Description points of relation.

| Entity 1 | Entity 2 |
| --- | --- |
| hasOne | belongsTo |
| nameEntity1\#indexed field | nameEntity2\#identity field |

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

Consider examples of relations:  
**1\)  1 : 1**  
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



