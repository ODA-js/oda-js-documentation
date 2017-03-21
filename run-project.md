# Run project

If neither yarn nor typescript is installed:

```
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
$ sudo apt-get update && sudo apt-get install yarn
$ sudo npm i -g typescript
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



