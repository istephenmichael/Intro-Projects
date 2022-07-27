



### Step 1: Install NodeJs

Update ubuntu

`sudo apt update`


Upgrade ubuntu

`sudo apt upgrade`


Add certificates

`sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates`

`curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`


Install NodeJS

`sudo apt install -y nodejs`



### Step 2: Install MongoDB

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list


Install MongoDB

`sudo apt install -y mongodb`


Start The server

`sudo service mongodb start`


Verify that the service is up and running

`sudo systemctl status mongodb`


Install npm – Node package manager.

`sudo apt install -y npm`


Install body-parser package

`sudo npm install body-parser`


Create a folder named ‘Books’

`mkdir Books && cd Books`


In the Books directory, Initialize npm project

`npm init`


Add a file to it named server.js

`vi server.js`




### Step 3: Install Express and set up routes to the server




### Step 4: Access the routes with AngularJS
