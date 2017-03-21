# Run project

## Development
If neither yarn nor typescript is installed:

```
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
$ sudo apt-get update && sudo apt-get install yarn
$ sudo npm i -g typescript
$ sudo npm i -g @2fd/graphdoc

```

### install forever + tmux

* **forever**

  \[sudo if you not using nvm\]

  ```
  [sudo] npm install -g forever
  ```

* **tmux**

  ```
  sudo apt-get install tmux
  ```

### For the install dependence and run project:

```bash
$ ./run-dev-api4.sh
```
##Production

To run production environment we need:
- install project for development,
- build static files
- change `config/production.json` file according to working environment.
- setup `NODE_ENV=production` to `config`-module took right configuration file.
- run shell command: `NODE_ENV=production forever production.json`




