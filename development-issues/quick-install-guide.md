# Development Environment

For working with Oda system, on user’s PC should be installed:
**Nodejs** - version 7 or above;
**NVM** (Node Version Manager);
**MongoDB**
**NPM** (Node Package Manager).
**ODA API**
**VS Code** (Visual Studio Code).

# Install Nodejs.

Check if **Nodejs** version 7 or above is installed on your PC. 

In terminal window run command:
```bash
 node --version
```
If you get message that `nodejs is not installed`, you should install it:

In terminal window run command:
```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
```
**Note:** If you get nvm:
`command not found`
after running the install script, your system may not have a [.bash_profile file] where the command is set up.
Simply create one with touch `~/.bash_profile` and run the install script again. 
More detailed information about nodejs can be found [here](https://github.com/creationix/nvm#install-script
) 

Now install **Nodejs**, run in terminal:
```bash
nvm install v7; 
nvm use v7
```

# Install MongoDB.
Check if **MongoDB** is installed on your PC.
In terminal window, run command: 

```bash
mongo --version
```

If you get the message that `mongodb is not installed`, you should install it in terminal:

```bash
https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/
```

Now run **MongoDB** in terminal:
```bash
sudo mongod
```
**Note:** If you get an error “shutting down with code 100”, open your root folder - cd / - and then create required folder - sudo mkdir data/db
**Note:** For **OSX**, **MongoDB** should be running every time. On **Linux**, **MongoDB** is running automatically, after system reboot.

# Install developer environment
* **VSCode** (Visual Studio Code).

For comfortable work with code, we recommend to install  **Visual Studio Code (VSCode)**.

The project contains all settings to the editor. It make the code environment feel and look the same between different developers. 

**Note:** that installing of **VSCode** is highly recommended, but is not necessary. You can also use any text editor like **Sublime**, **Atom**, **Notepad++**, etc.
