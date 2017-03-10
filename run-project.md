# Run project

If not yarn or typescript is not installed:
```
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
$ sudo apt-get update && sudo apt-get install yarn
$ sudo npm i -g typescript
```
For the install dependence and run project:

```bash
npm run fullbuild
npm run dev
# in other terminal
npm run dev-api
# in other terminal
cd graphiql
npm start
```



