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

**Note**: start the commands from the api4 folder.

