# MEAN STACK
# updating in ubuntu machine
sudo apt update
![image](https://user-images.githubusercontent.com/53397202/191009540-4cbb6710-0710-4133-9b6a-a11b35a3c39c.png)
# Upgrade the server
sudo apt upgrade
# Add certificate
sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates
![image](https://user-images.githubusercontent.com/53397202/191010890-ce66e7b0-fbe1-43ea-a677-ce935ee13922.png)
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash 
![image](https://user-images.githubusercontent.com/53397202/191011161-1c3450f7-987e-4701-97b4-1a92403106f3.png)

# Install node.js
sudo apt install -y nodejs
![image](https://user-images.githubusercontent.com/53397202/191011697-1ed27314-ede3-4793-ab77-88553faf120b.png)
# Install MongoDB
MongoDB stores data in flexible, JSON-like documents. Fields in a database can vary from document to document and data structure can be changed over time. For our example application, we are adding book records to MongoDB that contain book name, isbn number, author, and number of pages.
mages/WebConsole.gif
*sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6*
![image](https://user-images.githubusercontent.com/53397202/191012105-c65a696d-50aa-458d-9bad-a3f916405e80.png)
*echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list*
![image](https://user-images.githubusercontent.com/53397202/191012348-4fe87326-1b9d-4d59-b5cb-65f8f331a81d.png)
# Install MongoDB
sudo apt install -y mongodb
![image](https://user-images.githubusercontent.com/53397202/191042498-9556360c-4856-4adb-bc03-83f5691132c5.png)
# Start The server
 sudo service mongodb start
 ![image](https://user-images.githubusercontent.com/53397202/191042964-1cbbc135-8454-4c8e-9730-9df35c3c813a.png)
# Verify that the service is up and running
sudo systemctl status mongodb
![image](https://user-images.githubusercontent.com/53397202/191043324-35420920-d21f-431c-9581-3695c3f476fe.png)
# Install npm – Node package manager.
First install aptitude on the machine: sudo apt-get install aptitude
Use aptitude to install npm: sudo aptutide install -y npm 
sudo aptutide install -y npm
# Install body-parser package
sudo npm install body-parser
![image](https://user-images.githubusercontent.com/53397202/191045589-655f5d24-ac85-43e6-b1d7-85f45a76a3ba.png)
# Create a folder named ‘Books’
mkdir Books && cd Books
![image](https://user-images.githubusercontent.com/53397202/191046060-1a48642e-6740-4f15-a32a-f94f99e4e2f8.png)
# Initialize npm project in Book
![image](https://user-images.githubusercontent.com/53397202/191046380-dd7d5e55-9fd1-4b04-a615-f20cf2ded468.png)
# Add a file to it named server.js
vi server.js
Paste the code below;
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
# Install Express and set up routes to the server

Express is a minimal and flexible Node.js web application framework that provides features for web and mobile applications. We will use Express in to pass book information to and from our MongoDB database.

We also will use Mongoose package which provides a straight-forward, schema-based solution to model your application data. We will use Mongoose to establish a schema for the database to store data of our book register.

sudo npm install express mongoose

![image](https://user-images.githubusercontent.com/53397202/191047861-ef4bff0d-fd93-4690-9e53-e5166ed3f306.png)
# In ‘Books’ folder, create a folder named apps
mkdir apps && cd apps

![image](https://user-images.githubusercontent.com/53397202/191048302-7fdf597d-41b5-47aa-802c-4339bd60b5d0.png)

# Create a file named routes.js
vi routes.js
Paste the code below:
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

# In the ‘apps’ folder, create a folder named models
mkdir models && cd models
# Create a file named book.js
vi book.js
Copy and paste to the file:
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
# Access the routes with AngularJS
AngularJS provides a web framework for creating dynamic views in your web applications. In this tutorial, we use AngularJS to connect our web page with Express and perform actions on our book register.
Change the directory back to ‘Books’
# Create a folder named public
mkdir public && cd public
![image](https://user-images.githubusercontent.com/53397202/191050925-75e1a37d-a54f-4a3f-804b-413059b3ff78.png)

# Add a file named script.js
vi script.js
Copy and paste the the code below into the file
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
# In public folder, create a file named index.html;
vi index.html
copy and paste the code below into the file
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

![image](https://user-images.githubusercontent.com/53397202/191052012-c6f31b44-38f5-454d-810b-1a54d26dc5c6.png)

# Change the directory back up to Books and start node server.js
node server.js
![image](https://user-images.githubusercontent.com/53397202/191054461-0584518f-6010-480a-a1dc-101699451b1e.png)

![image](https://user-images.githubusercontent.com/53397202/191283955-ed3065d4-c7c8-41c6-818b-d4b7ce107d47.png)

