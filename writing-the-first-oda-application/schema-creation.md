## Schema creation
Data Model of your application describe in folder: `src/schema/entities`
'/schema' folder structure:<br>
1. Entities - data structure is described in this folder.<br>
2. Mutations - Customer Mutations is described in this folder.<br>
3. Packages - folder with UML diagram generation structure.<br><br>
### Entity creation
Before create entities your need to build Data Model. Each object of your Data Model is an entity.<br>
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
4. Save all changes in the file.
5. Open terminal window with npm running and stop server. To do this push "Ctrl+C" on your keyboard.
6. Need to compile project, by running comand: ` npm run compile`.
7. Run server: `npm start`

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
<li> `field_name`- field name,required. Type:string. The name must not contain spaces, special characters, and must begin with a small letter</li>
<li>'type' - field type. Types: string, boolean, number, Date. By default type is 'string' </li>
<li>'description' - field description. Type: string.</li>
<li>'required' - indicates this field is required or not. Type: boolean. The default value is set to false.
<li>'indexed' - whether the field is indexable and whether it can be searched.Type: boolean. The default value is set to false.</li>
<li>'identity' - indicates whether the field is an identifier. Type: boolean. The default value is set to false. </li>
<li>'relation' - describes the relationship between an object and another data model object. More detail about relations [here](/writing-the-first-oda-application/relations.md)</li>
When entity is described need to add it to index file. To do his open `src/schema/entities/index.ts` and add described entity to index file. Need to add described entity to 'import' (1) and 'export'(2).


```
import User from './User';
import Student from './Student'; //(1) 

import StudentProfile from './StudentProfile';
import StudentsGroup from './StudentsGroup';
import Teacher from './Teacher';
import Subject from './Subject';

export default [
  User,
  Student, //(2)
  StudentsGroup,
  StudentProfile,
  Teacher,
  Subject,
];
```



