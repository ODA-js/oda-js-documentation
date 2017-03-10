#Data import/export

This project provides to import/export data to/from the database. You can to config every entity or their combination for loading/unloading. 

Open the `/api4/package.json` file. It contains the next strings: 
```json
"restoreData": "node dist/seeds/restore.js data/dump.json",
"dumpData": "node dist/seeds/dumpDirect.js data/dump1.json",
```

It asks that 
* the command to restore (import to the database) data is:
  `npm run restoreData` 
* the command to dump (export from the database) data is: 
  `npm run dumpData`

**Note**: run the commands from the api4 folder.

api4/src/seeds folder contains dump and restore files and loaderConfig.ts file. it is the main file of dump that describes what you want to i/e.

api4/data/queries folder contains the queries for i/e and used by loaderConfig. 

If you change loaderConfig or Query, you must to recompile api4 by running command
npm run compile

See the result of dump in the data/dump1.json file.
Place the data what you want to import to the database in the data/dump.json file. 