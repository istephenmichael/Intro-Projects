# PROJECT 3 - MERN STACK IMPLEMENTATION

## SIMPLE TO-DO APPLICATION ON MERN WEB STACK

### STEP 1 – BACKEND CONFIGURATION

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

![6-app-discpi](https://user-images.githubusercontent.com/85305109/180627463-11ecbd19-c0fe-4ad7-b6db-b1223614a822.jpg)


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

`node index.js`


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

`cd models`

Create file in ***models*** folder
`touch todo.js`

`vim todo.js`

```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;

```

Update api.js in ‘routes’ directory with code below

```
const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;

```
Create a MongoDB database and collection 

Create a file in your Todo directory called ***.env***

`touch .env`
`vi .env`

Add the connection string to access the database

Update the index.js to reflect the use of .env so that Node.js can connect to the database

Start your server using the command:

`node index.js` 

![F-DB-connected-successfully](https://user-images.githubusercontent.com/85305109/180627694-0773c6e5-3f25-45fd-b87c-20c367c9a830.jpg)


use Postman to test our API

![POST](https://user-images.githubusercontent.com/85305109/180627589-7596fee1-6cd1-489a-b587-53c39bf04119.jpg)

![GET](https://user-images.githubusercontent.com/85305109/180627592-e740097f-9b76-4600-96ae-f6c35ac86507.jpg)

---

## STEP 2 – FRONTEND CREATION

`npx create-react-app client`

![10-npx-create-react-app-client](https://user-images.githubusercontent.com/85305109/180625057-2c480f2a-c7dd-4cc8-ac69-e9fe4db8cbd8.jpg)


Running a React App

Install concurrently

`npm install concurrently --save-dev`

![11-Install-concurrently](https://user-images.githubusercontent.com/85305109/180625082-a67450cc-6ef4-462a-a630-9ee67a21a01f.jpg)



Install nodemon

`npm install nodemon --save-dev`

![12-nodemon](https://user-images.githubusercontent.com/85305109/180625101-701f2ff8-f0ab-4bb3-8b58-6ff31c5be31c.jpg)



Configure Proxy in package.json

`cd client`

`vi package.json`

`npm run dev`

![13-Port-3000](https://user-images.githubusercontent.com/85305109/180627275-2d8419ad-1a97-4bf9-aefb-799d5d6f1e80.jpg)


![14-REACT-3000](https://user-images.githubusercontent.com/85305109/180627256-db38ce49-4cef-4768-af61-6daa6595bf3a.jpg)


Creating your React Components

`cd client`

move to the src directory

`cd src`
Inside your src folder create another folder called components

`mkdir components`
Move into the components directory with

`cd components`
Inside ‘components’ directory create three files Input.js, ListTodo.js and Todo.js.

`touch Input.js ListTodo.js Todo.js`

Open Input.js file

`vi Input.js`

Copy and paste the following code

```
import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {

state = {
action: ""
}

addTodo = () => {
const task = {action: this.state.action}

    if(task.action && task.action.length > 0){
      axios.post('/api/todos', task)
        .then(res => {
          if(res.data){
            this.props.getTodos();
            this.setState({action: ""})
          }
        })
        .catch(err => console.log(err))
    }else {
      console.log('input field required')
    }

}

handleChange = (e) => {
this.setState({
action: e.target.value
})
}

render() {
let { action } = this.state;
return (
<div>
<input type="text" onChange={this.handleChange} value={action} />
<button onClick={this.addTodo}>add todo</button>
</div>
)
}
}

export default Input
```


Install Axios

`npm install axios`

![15-axios](https://user-images.githubusercontent.com/85305109/180626257-b1498552-0fbb-4cf6-a934-8768f0470e65.jpg)






![END-TO-DO-LIS](https://user-images.githubusercontent.com/85305109/180625716-848dae8e-de23-4b1c-ba4b-fb31c925088a.jpg)
