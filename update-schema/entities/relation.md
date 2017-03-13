# Relation

Type of relations:
- **1 : 1**

Description points of relation.


| Entity 1 | Entity 2 |
| --------------| ---- |
|hasOne | belongsTo |
|nameEntity1#indexed field | nameEntity2#identity field |

All description you find by link [One-To-One Associations](http://docs.sequelizejs.com/en/v3/docs/associations/#one-to-one-associations)
- **1 : n**

| Entity 1 | Entity 2 |
| --------------| ---- |
|hasMany | belongsTo |
|nameEntity1#indexed field | nameEntity2#identity field |


All description you find by link [One-To-Many Associations](http://docs.sequelizejs.com/en/v3/docs/associations/#1m)

- **m : n**

| Entity 1 | Entity 2 |
| --------------| ---- |
| belongsToMany| belongsToMany |
|nameEntity1#identity field | nameEntity2#identity field |


All description you find by link [Many-To-Many Associations](http://docs.sequelizejs.com/en/v3/docs/associations/#nm)

Consider examples of relations:
**1)  1 : 1**
Contact relations with Phone.
File _Contact.ts_:
```
    {
      'name': 'phone',
      'description': 'relation with Phone',
      'relation': {
        'hasOne': 'Phone#contact',
        'opposite': 'contact' // no required atribute.
      },
    }
```
File _Phone.ts_:
```
    {
      'name': 'contact',
      'indexed': true,
      'description': 'relation with Contact',
      'relation':{
        'belongsTo': 'Contact#id',
      },
    }
```
**2)  1 : n**
Organization has many Campaigns. Campaign belongs to one Organization.
File _Organization.ts_:
```
    {
      'name': 'campaigns',
      'relation': {
        'hasMany': 'Campaign#organization',
        'opposite': 'organization',
      },
    },
```
File _Campaign.ts_:
```
    {
      'name': 'organization',
      'indexed': true,
      'relation': {
        'belongsTo': 'Organization#id',
      }
    },
```
**3)  m : n**
Organization relations with object Profile Type.
File _Organization.ts_:
```
    {
      'name': 'profileTypes',
      'relation': {
        'belongsToMany': 'ProfileType#key',
        'using': 'OrganizationProfile#organization',
        'opposite': 'organizations',
      },
    },
```
File _ProfileType.ts_:
```
    {
      'name': 'organizations',
      'relation': {
        'belongsToMany': 'Organization#id',
        'using': 'key@OrganizationProfile#profileType',
      },
    },
```
