# Run project

if not yarn or typescript is not installed:
```
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
$ sudo apt-get update && sudo apt-get install yarn
$ sudo npm i -g typescript
```

for the install dependence and run project:

```bash

npm run fullinstall
npm run dev
# in other terminals
npm run dev-api
```



