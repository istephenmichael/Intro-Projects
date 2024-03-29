# PROJECT 4 - MEAN STACK DEPLOYMENT TO UBUNTU IN AWS



### Step 1: Install NodeJs



Update ubuntu

`sudo apt update`

![1](https://user-images.githubusercontent.com/85305109/182267660-dd7f9d44-e8dc-4520-8ec4-3c374330b2ba.jpg)



Upgrade ubuntu

`sudo apt upgrade`

![2](https://user-images.githubusercontent.com/85305109/182267709-cac5f549-5099-4196-9dce-dd93bad35d0b.jpg)



Add certificates

`sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates`

![3](https://user-images.githubusercontent.com/85305109/181521909-ad5b17f0-0795-4cb0-9471-379204e6adbf.jpg)


`curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`

![4](https://user-images.githubusercontent.com/85305109/181522024-64084e3f-27f1-4ae5-8ffc-99e095b9022a.jpg)



Install NodeJS

`sudo apt install -y nodejs`

![5](https://user-images.githubusercontent.com/85305109/181522196-14deec1d-efff-41de-a1e0-ddd2ad7562cc.jpg)

--- 




### Step 2: Install MongoDB



`sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6`

`echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list`

![step2-1](https://user-images.githubusercontent.com/85305109/182268129-381a04ed-61de-48a8-baad-696d319ba831.jpg)


Install MongoDB

`sudo apt install -y mongodb`

![step2-2](https://user-images.githubusercontent.com/85305109/182270179-f2dde214-24cc-4aad-a4c6-94155802da1b.jpg)


Start The server

`sudo service mongodb start`

![step2-3](https://user-images.githubusercontent.com/85305109/182270112-d507b9f5-52c7-427a-8d79-c27655da4b42.jpg)


Verify that the service is up and running

`sudo systemctl status mongodb`


Install npm – Node package manager.

`sudo apt install -y npm`


Install body-parser package

`sudo npm install body-parser`

![step2-4](https://user-images.githubusercontent.com/85305109/182270288-5d154b39-0359-4aec-a764-53d59036aa66.jpg)


Create a folder named ‘Books’

`mkdir Books && cd Books`


Initialize npm project in the ***Books*** directory, 

`npm init`

![step2-5](https://user-images.githubusercontent.com/85305109/182270393-36c37c8c-2dd7-4365-a5fc-7fd0fee694eb.jpg)


Add a file to it named ***server.js***

`vi server.js`

Copy and paste the web server code below into the ***server.js*** file.

```
var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(express.static(__dirname + '/public'));
app.use(bodyParser.json());
require('./apps/routes')(app);
app.set('port', 3300);
app.listen(app.get('port'), function() {
    console.log('Server up: http://localhost:' + app.get('port'));
});

```
---




### Step 3: Install Express and set up ***'routes'*** to the server



`sudo npm install express mongoose`



In ***‘Books’*** folder, create a folder named ***apps***

`mkdir apps && cd apps`



Create a file named ***'routes.js'***

`vi routes.js`



Copy and paste the code below into routes.js

```
var Book = require('./models/book');
module.exports = function(app) {
  app.get('/book', function(req, res) {
    Book.find({}, function(err, result) {
      if ( err ) throw err;
      res.json(result);
    });
  }); 
  app.post('/book', function(req, res) {
    var book = new Book( {
      name:req.body.name,
      isbn:req.body.isbn,
      author:req.body.author,
      pages:req.body.pages
    });
    book.save(function(err, result) {
      if ( err ) throw err;
      res.json( {
        message:"Successfully added book",
        book:result
      });
    });
  });
  app.delete("/book/:isbn", function(req, res) {
    Book.findOneAndRemove(req.query, function(err, result) {
      if ( err ) throw err;
      res.json( {
        message: "Successfully deleted the book",
        book: result
      });
    });
  });
  var path = require('path');
  app.get('*', function(req, res) {
    res.sendfile(path.join(__dirname + '/public', 'index.html'));
  });
};

```


In the ‘apps’ folder, create a folder named ***'models'***

`mkdir models && cd models`



Create a file named ***'book.js'***

`vi book.js`



Copy and paste the code below into ***‘book.js’***

```
var mongoose = require('mongoose');
var dbHost = 'mongodb://localhost:27017/test';
mongoose.connect(dbHost);
mongoose.connection;
mongoose.set('debug', true);
var bookSchema = mongoose.Schema( {
  name: String,
  isbn: {type: String, index: true},
  author: String,
  pages: Number
});
var Book = mongoose.model('Book', bookSchema);
module.exports = mongoose.model('Book', bookSchema);

```
---





### Step 4: Access the routes with AngularJS



Change the directory back to ***‘Books’***

`cd ../..`


Create a folder named ***'public'***

`mkdir public && cd public`



Add a file named ***'script.js'***

`vi script.js`


Copy and paste the Code below (controller configuration defined) into the script.js file.

```
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
  $http( {
    method: 'GET',
    url: '/book'
  }).then(function successCallback(response) {
    $scope.books = response.data;
  }, function errorCallback(response) {
    console.log('Error: ' + response);
  });
  $scope.del_book = function(book) {
    $http( {
      method: 'DELETE',
      url: '/book/:isbn',
      params: {'isbn': book.isbn}
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
  $scope.add_book = function() {
    var body = '{ "name": "' + $scope.Name + 
    '", "isbn": "' + $scope.Isbn +
    '", "author": "' + $scope.Author + 
    '", "pages": "' + $scope.Pages + '" }';
    $http({
      method: 'POST',
      url: '/book',
      data: body
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
});

```

In public folder, create a file named ***'index.html'***

`vi index.html`



Cpoy and paste the code below into ***'index.html'*** file.

```
<!doctype html>
<html ng-app="myApp" ng-controller="myCtrl">
  <head>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
    <script src="script.js"></script>
  </head>
  <body>
    <div>
      <table>
        <tr>
          <td>Name:</td>
          <td><input type="text" ng-model="Name"></td>
        </tr>
        <tr>
          <td>Isbn:</td>
          <td><input type="text" ng-model="Isbn"></td>
        </tr>
        <tr>
          <td>Author:</td>
          <td><input type="text" ng-model="Author"></td>
        </tr>
        <tr>
          <td>Pages:</td>
          <td><input type="number" ng-model="Pages"></td>
        </tr>
      </table>
      <button ng-click="add_book()">Add</button>
    </div>
    <hr>
    <div>
      <table>
        <tr>
          <th>Name</th>
          <th>Isbn</th>
          <th>Author</th>
          <th>Pages</th>

        </tr>
        <tr ng-repeat="book in books">
          <td>{{book.name}}</td>
          <td>{{book.isbn}}</td>
          <td>{{book.author}}</td>
          <td>{{book.pages}}</td>

          <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
        </tr>
      </table>
    </div>
  </body>
</html>
```

Change the directory back up to ***'Books'***

`cd ..`


Start the server by running this command:

`node server.js`


Connect to server via port 3300. 

`curl -s http://localhost:3300`

![webpage-port-3300](https://user-images.githubusercontent.com/85305109/182270660-c056098b-d770-4a34-8037-0b38f9440d1b.jpg)



