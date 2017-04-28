# Create project.

Open another terminal window.

Install **typescript** (variation of javascript, needed for working with typescript files):

```bash
npm install -g typescript
```

Install Yeoman and generator-oda-api-simple using npm: 

```bash
sudo npm install -g yo
sudo npm install -g generator-oda-api-simple
```

Generate your new project 
```bash
yo oda-api-simple
```

Go to project folder (instead of `<your-project-name>` use the name of your project):

```bash
cd <your-project-name> 
```

Run project:

```bash
npm start
```

Open web browser. 
Go to **localhost:3003/graphiql** to check that everything is working.