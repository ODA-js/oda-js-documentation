# Schema

Data Model of your application describes in folder `src/schema`.   
Structure of folder **schema**:

* **entities** - folder where structure of data is described.
* **mutations** - folder where [Custome Mutations](./customer-mutation.md) are described.
* **packages** - folder where structure for [Generate UML Diagrams](./generation-of-uml-diagrams.md) is described.

# Entities

Before create **entities** your need to build **Data Model**. Each object of your Data Model is an **entity**.  
Entity describes fields of object and relations between object and another object of model.

**For example: **describe object City and relation City with Country.

1. Go to folder `src/schema`;
2. Create a new file with  extension _.ts_  - `Stutent.ts`;

**Note:** File must be named by next rules:

* no spaces or other special characters;
* start with a capital letter. 

3.Describe fields and relations of entity object:

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
  


# Fields of Entity

Field have next atributes:

* **name** - string, **required** attribute. Doesn't contain spaces or other special characters and start with a lowercase letter.
It contain name of entity.
* **description** - string, it contain description of entity;
* **fields** - object, It contaian:

        fields: {
          ...
          <name>: {
            type: 'Date',
            description: 'description put here',
            required: true,
            indexed: true,
            identity: true,
            relation: <Relation description...>,
          },
          ...
        }
            
     1) <**name**> - string, **required** attribute. Doesn't contain spaces or other special characters and start with a lowercase letter.
     2) **description** - string, any text;
     3) **type** - string, default value is _string_. Types supported by project:

        string  
        boolean
        number
        Date
  
    4) **required** - boolean, default value _false_;
    4) **indexed** - boolean, default value _false_;
    5) **identity** - boolean, default value _false_;
    6) **relation** - object. Atribute which describes relation by object with another object of data model. \(See [Relation](./relation.md)\)
  







