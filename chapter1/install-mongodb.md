## MongoDB installation

1. Check if MongoDB installed on your PC.<br>
a) Open terminal window;<br>
b) Run command:<br> 
`mongo --version`<br>
c) If you see output that contains this string **"MongoDB shell version v3.4.4-rc0"** in terminal, this means that NodeJS with fresh enough version is installed in your system. You can skip steps 2 and 3 and go next to [installation of Visual Studio Code application](/chapter1/install-visual-studio-code-vscode.md).

2. If you have MongoDB on your PC, then run MongoDB using command:<br>`sudo mongod     `

3. If you get a message that MongoDB is not installed, you should install it, using this [tutorial](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/). After installation run MongoDB using command:<br>`sudo mongod` <br>
`Note:` If you get error message "shutting down with code 100", open your root folder and create required folder (`sudo mkdir data/db`).
`Note:` For OSX, MongoDB should be running every time. If you have rebooted the system, you should run MongoDB again.



    




