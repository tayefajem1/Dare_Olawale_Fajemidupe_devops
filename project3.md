# Project MERN
# update ubuntu
sudo apt update
![image](https://user-images.githubusercontent.com/53397202/190870228-8182d9e8-8250-4fcc-856d-0fd46afbf399.png)

# To upgrade
sudo apt upgrade
![image](https://user-images.githubusercontent.com/53397202/190870456-c404a852-4e66-4a1f-87db-08ecbb14648d.png)
# To get the location of Node.js software from Ubuntu repositories.
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
![image](https://user-images.githubusercontent.com/53397202/190870507-d01ca6f0-6f30-4914-9d36-4a6273e4a8b3.png)
# Install nodejs server
sudo apt-get install -y nodejs
# Verify version of nodejs installed
node -v
npm -v 
![image](https://user-images.githubusercontent.com/53397202/190870885-7d446ad9-3916-4345-b02a-7d766a2483d7.png)

# Create a new directory for your To-Do project:
mkdir Todo
![image](https://user-images.githubusercontent.com/53397202/190871007-0c6591aa-e0e6-4f74-81b2-43362f7c07d1.png)
# To see if TODO is created
ls
ls -lih 
ls --help
# Change directory to TODO
cd Todouse the command npm init to initialise your project, so that a new file named package.json will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press Enter several times to accept default values, then accept to write out the package.json file by typing yes.
# To initialize, use the command npm init to initialise your project, so that a new file named package.json will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press Enter several times to accept default values, then accept to write out the package.json file by typing yes.
npm init
Continue to press enter from the keybord
![image](https://user-images.githubusercontent.com/53397202/190871351-26d8b9bc-fed6-4ee7-b453-928396b8060f.png)
run ls (To confirm you have the package.json
![image](https://user-images.githubusercontent.com/53397202/190871416-c0e13c3e-4661-48e4-820a-ec08ec507515.png)
# To install EXPRESSJS
npm install express
# Create a file called index.js
touch ndex.js
![image](https://user-images.githubusercontent.com/53397202/190871619-a77f69cf-91a4-4778-bd3c-5c83ea4c7073.png)
# Install the dotenv module
![image](https://user-images.githubusercontent.com/53397202/190871687-6bc7c808-2c47-42d4-8fad-b54c233cd34b.png)
# Open the index.js file with the command below
vim index.js
Paste the below:
const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
# To very if server is running
node index.js
Server running on port 5000
![image](https://user-images.githubusercontent.com/53397202/190871963-560e036e-7795-4499-931d-5bf3daaa22ee.png)
# set your instance port 5000
Browse http://3.133.148.207:5000
# To get you IP address and dns run the command below
 Run curl -s http://169.254.169.254/latest/meta-data/public-ipv4 for Public IP address or curl -s http://169.254.169.254/latest/meta-data/public-hostname for Public DNS name.
 # 3 ways to Route
 Routes
There are three actions that our To-Do application needs to be able to do:

Create a new task
Display list of all tasks
Delete a completed task
Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes
# Create directory route
mkdir routes
# change to route folder
cd routes
# Create file api.js inside routes
touch api.js
# Open api.js and paste
vim api.js
paste
const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;

![image](https://user-images.githubusercontent.com/53397202/190872309-18ac9e2d-ac5c-4323-8410-5f33b01f2217.png)

# MODEL
Now comes the interesting part, since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model.

A model is at the heart of JavaScript based applications, and it is what makes it interactive.

We will also use models to define the database schema . This is important so that we will be able to define the fields stored in each Mongodb document. (Seems like a lot of information, but not to worry, everything will become clear to you over time. I promise!!!)

In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties

To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier.

Change directory back Todo folder with cd .. and install Mongoose
# Intall Mongoose
npm install mongoose
![image](https://user-images.githubusercontent.com/53397202/190872994-778ec154-3375-4234-835d-c0182417de02.png)
# Create model
mkdir models
# Change to model
cd model
# create todo.js file inside models
touch todo.js
# you can define all the command at once
mkdir models && cd models && touch todo.js
# Open todo and paste (some ....)
paste:
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
# Now we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model. In Routes directory, open api.js with vim api.js, delete the code inside with :%d command and paste there code below into it then save and exit
Paste:
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
# Sign up to MongoDb and configure
create a file in Todo foldetr
touch .env
# Open the file
vi .env
# Add the connection string to access the database in it, just as below:
DB = 'mongodb+srv://<username>:<password>@<network-address>/<dbname>?retryWrites=true&w=majority'
# Delete contect in node.js
  const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

//connect to the database
mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
.then(() => console.log(`Database connected successfully`))
.catch(err => console.log(err));

//since mongoose promise is depreciated, we overide it with node's promise
mongoose.Promise = global.Promise;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use(bodyParser.json());

app.use('/api', routes);

app.use((err, req, res, next) => {
console.log(err);
next();
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
# Start node.js
  node index.js
 ![image](https://user-images.githubusercontent.com/53397202/190877154-6fcd0faa-3427-469d-8add-e67642063c93.png)
 



