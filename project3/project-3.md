## STEP 1 – BACKEND CONFIGURATION

Update ubuntu

`sudo apt update`

![1-sudo-apt-update](https://user-images.githubusercontent.com/85305109/180265629-62cab46d-f400-4c94-9347-85a11ef39143.jpg)


Upgrade ubuntu

`sudo apt upgrade`

![2-sudo-apt-upgrade](https://user-images.githubusercontent.com/85305109/180265928-bf232843-950e-4c42-8c90-21ccd95d894a.jpg)


Locating the Node.js software from Ubuntu repositories

`curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

![3-locating-nodejs-repo](https://user-images.githubusercontent.com/85305109/180265999-6b203b13-17d1-4809-9196-6acc57c231dd.jpg)


Install Node.js on the server

`sudo apt-get install -y nodejs`

![4-sudo-apt-install-nodejs](https://user-images.githubusercontent.com/85305109/180266162-ba5a3a09-ceb9-49bc-a3a2-17a15af60256.jpg)



Verify the node installation

`node -v`

Verify the npm installation

`npm -v` 

![5-version](https://user-images.githubusercontent.com/85305109/180266422-c8f7de8a-454e-4224-be03-dffc592b520d.jpg)


Application Code Setup

`mkdir Todo`

`cd Todo`

`npm init`



Install ExpressJS

`npm install express`

![A-install-express](https://user-images.githubusercontent.com/85305109/180272619-6a7fd32b-b7f4-40d4-b3b1-e8f7abbde436.jpg)



Create a file index.js 

`touch index.js`



Install the dotenv module

`npm install dotenv`

![B-Install-dotenv](https://user-images.githubusercontent.com/85305109/180272692-5a216bcc-70a6-45bd-a16c-ecf69e3c6e2f.jpg)



Open the index.js file 

`vim index.js`


![C-Running-port-5000](https://user-images.githubusercontent.com/85305109/180273339-a7ef92d0-e22c-4a4a-a245-5538e799091d.jpg)


![7-welcome-express](https://user-images.githubusercontent.com/85305109/180278766-fe2cfcc0-03be-44fe-b982-3ef82aeebc13.jpg)


 Create a folder routes

`mkdir routes`

`touch api.js`


![image](https://user-images.githubusercontent.com/85305109/180279933-cdb18fd0-f503-4572-a957-029d6d37c85f.png)


MODELS


install mongoose in the Todo directory

`npm install mongoose`

![E-Install-mongoose](https://user-images.githubusercontent.com/85305109/180286108-c2f1e6de-bc10-4ba3-910b-177d7c277c3f.jpg)


`mkdir models`

