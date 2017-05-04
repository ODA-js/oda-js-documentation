## Schema creation
Data Model of your application describe in folder: `src/schema/entities`
'/schema' folder structure:<br>1. Entities - data structure is described in this folder. <br>2. Mutations - Customer Mutations is described in this folder.<br>3. Packages - folder with UML diagram generation structure.
### Entity creation
Before create entities your need to build Data Model. Each object of your Data Model is an entity.
Entity describes fields of object and relations between object and another object of model.
1. Run Visual Studio Code
2. Click on "Open Folder" button and in file manager window choose main folder on your project.
3. Go to folder `src/schema/entities.` In this folder you can create a new file with extention _.ts_ where you can descibe entities. For example, let's look at the existing file _Student.ts_. The file describes the object 'Student' and its relations with Student Profile and Students Group.
`Note:` The filename must not contain spaces, special characters, and must begin with a capital letter


```
export default {
      name: 'Student',
      fields: {
        firstName: {
          indexed: true,
        },
        middleName: {},
        lastName: {
          identity: true,
        },
        uin: {
          identity: true,
        },
        dateOfBirth: {
          type: 'Date',
        },
        profile: {
          indexed: true,
          relation: {
            hasOne: 'StudentProfile#',
          },
        },
        group: {
          indexed: true,
          relation: {
            belongsTo: 'StudentsGroup#',
            opposite: 'students',
          },
        },
      },
    };

```
### Entity fields
The entity has the following fields:
 

```
 fields: {
    ...
    field_name: {
      type: 'field_type',
      description: 'description put here',
      required: true,
      indexed: true,
      identity: true,
      relation: <Relation description...>,
    },
    ...
  }
```
<ul>
<li> `field_name`- field name,required. Type:string. The name must not contain spaces, special characters, and must begin with a capital letter</li>
<li>'type' - field type. Types: string, boolean, number, date. By default type is 'string' </li>
<li></li>
