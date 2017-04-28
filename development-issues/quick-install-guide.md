# Development Environment

For working with Oda system, on user’s PC should be installed:
**Nodejs** - version 7 or above;
**NVM** (Node Version Manager);
**MongoDB**
**NPM** (Node Package Manager).
**ODA API**
VS Code (Visual Studio Code).

# Install Nodejs.

Check if **Nodejs** version 7 or above is installed on your PC. 

In terminal run command:
```bash
 node --version
```
If you get message that nodejs is not installed, you should install it:
 In terminal window run command:
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
Note: If you get nvm: command not found after running the install script, your system may not have a [.bash_profile file] where the command is set up. Simply create one with touch ~/.bash_profile and run the install script again.
More detailed information about nodejs can be found here: https://github.com/creationix/nvm#install-script
Установите nodejs, выполнив эти команды в командной строке:
nvm install v7; 
nvm use v7

Install MongoDB.
Check if MongoDB is installed on your PC.
In terminal window, run command: mongo --version
If you get the message that mongodb is not installed, you should install it:
https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/
Run mongodb: sudo mongod
Note: If you get an error “shutting down with code 100”, open your root folder - cd / - and then create required folder - sudo mkdir data/db
Note: For OSX, MongoDB should be running every time. On Linux, MongoDB is running automatically, after system reboot.
