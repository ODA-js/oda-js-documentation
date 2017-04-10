# Data import/export

This project provides opportunity to import/export data to/from the database. You can configure every entity or their combination for loading/unloading.

Open the `/api4/package.json` file. It contains strings:

```json
"restoreData": "node dist/seeds/restore.js data/dump.json",
"dumpData": "node dist/seeds/dumpDirect.js data/dump1.json",
```

It asks that

* the command to restore \(import to the database\) data is:
  `npm run restoreData` 
* the command to dump \(export from the database\) data is: 
  `npm run dumpData`

**Note**: run the commands from the api4 folder.

**api4/src/seeds** folder contains the `dumpDirect.ts` and `restore.ts` files that implement the import/export operations.

`loaderConfig.ts` file is placed in the same folder. It is the main config file that defines what you want to import/export. \(Learn more about [LoaderConfig](/dump-data/loaderconfig.md)\)

`api4/data/queries` folder contains queries for import/export and used by loaderConfig. \(Learn more about [Queries for LoaderConfig](./queries.md)\)

* See the result of the data export in the `api4/data/dump1.json` file. 
* Place the imported data in the `api4/data/dump.json` file. 

Or you can change the filenames in the forementioned `package.json` file.

**Note:** If you change the loaderConfig.ts or some of its query\(queries\), you must recompile api4 by running command 

`npm run compile` from api4.

