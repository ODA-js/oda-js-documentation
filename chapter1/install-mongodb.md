## MongoDB installation

1. Check if MongoDB installed on your PC.<br>
a) Open terminal window;<br>
b) Run command:<br> 
`mongo --version`<br>
c) If you see output that contains this string **"MongoDB shell version v3.4.4-rc0"** in terminal, this means that MongoDB with fresh enough version is installed in your system. You can skip step 2.<br>
d) If you see output **"The program 'mongo' is currently not installed. You can install it by typing: sudo apt install mongodb-clients"** in terminal, this means that MongoDB is not installed in your system. Please, proceed with installation.<br> 

2. Install MongoDB, using this [tutorial](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/). 

3. Run MongoDB using command:<br>`sudo mongod &` <br>
`Note:` If you get error message "shutting down with code 100", open your root folder and create required folder (`sudo mkdir data/db`).
`Note:` For OSX, MongoDB should be running every time. If you have rebooted the system, you should run MongoDB again.



    




