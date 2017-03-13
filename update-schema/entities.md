# Entities

Before create **entities** your need to build **Data Model**. Each object of your Data Model is it **entity**.  
Entity describes fields of object and relations object with another object of model.

**For example: **describe object City and relation City with Country.

1. Go to folder `api4/src/schema`;
2. Create a new file with  extension _.ts_  - `City.ts`;

**Note:** File must be named by next rules:

* not contain spaces or other special characters;
* start with a capital letter. 

3.Describes fields and relations of object;

    export default {
      name: 'City',
      title: 'City',
      description: `
        # Dictionary.
        # Value list of available City. Each Country has your list of cities.
      `,
      fields: [
        {
          name: 'value',
          required: true,
        },
        {
          name: 'key',
          identity: true,
        },
        {
          name: 'country',
          indexed: true,
          description: 'relation with Country',
          relation: {
            belongsTo: 'Country#key',
          },
        },
      ],
    };



