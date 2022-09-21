# Project MERN
### Update ubuntu
sudo apt update
![image](https://user-images.githubusercontent.com/53397202/190870228-8182d9e8-8250-4fcc-856d-0fd46afbf399.png)

### To upgrade
sudo apt upgrade
![image](https://user-images.githubusercontent.com/53397202/190870456-c404a852-4e66-4a1f-87db-08ecbb14648d.png)
### To get the location of Node.js software from Ubuntu repositories.
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
![image](https://user-images.githubusercontent.com/53397202/190870507-d01ca6f0-6f30-4914-9d36-4a6273e4a8b3.png)
### Install nodejs server
sudo apt-get install -y nodejs
### Verify version of nodejs installed
node -v
npm -v 
![image](https://user-images.githubusercontent.com/53397202/190870885-7d446ad9-3916-4345-b02a-7d766a2483d7.png)

### Create a new directory for your To-Do project:
mkdir Todo
![image](https://user-images.githubusercontent.com/53397202/190871007-0c6591aa-e0e6-4f74-81b2-43362f7c07d1.png)
### To see if TODO is created
ls
ls -lih 
ls --help
### Change directory to TODO
cd Todouse the command npm init to initialise your project, so that a new file named package.json will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press Enter several times to accept default values, then accept to write out the package.json file by typing yes.
### To initialize, use the command npm init to initialise your project, so that a new file named package.json will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press Enter several times to accept default values, then accept to write out the package.json file by typing yes.
npm init
Continue to press enter from the keybord
![image](https://user-images.githubusercontent.com/53397202/190871351-26d8b9bc-fed6-4ee7-b453-928396b8060f.png)
run ls (To confirm you have the package.json
![image](https://user-images.githubusercontent.com/53397202/190871416-c0e13c3e-4661-48e4-820a-ec08ec507515.png)
### To install EXPRESSJS
npm install express
### Create a file called index.js
touch ndex.js
![image](https://user-images.githubusercontent.com/53397202/190871619-a77f69cf-91a4-4778-bd3c-5c83ea4c7073.png)
### Install the dotenv module
![image](https://user-images.githubusercontent.com/53397202/190871687-6bc7c808-2c47-42d4-8fad-b54c233cd34b.png)
### Open the index.js file with the command below
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
### To very if server is running
node index.js
Server running on port 5000
![image](https://user-images.githubusercontent.com/53397202/190871963-560e036e-7795-4499-931d-5bf3daaa22ee.png)
### set your instance port 5000
Browse http://3.133.148.207:5000
### To get you IP address and dns run the command below
 Run curl -s http://169.254.169.254/latest/meta-data/public-ipv4 for Public IP address or curl -s http://169.254.169.254/latest/meta-data/public-hostname for Public DNS name.
 ### 3 ways to Route
 Routes
There are three actions that our To-Do application needs to be able to do:

Create a new task
Display list of all tasks
Delete a completed task
Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes
### Create directory route
mkdir routes
### change to route folder
cd routes
### Create file api.js inside routes
touch api.js
### Open api.js and paste
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

### MODEL
Now comes the interesting part, since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model.

A model is at the heart of JavaScript based applications, and it is what makes it interactive.

We will also use models to define the database schema . This is important so that we will be able to define the fields stored in each Mongodb document. (Seems like a lot of information, but not to worry, everything will become clear to you over time. I promise!!!)

In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties

To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier.

Change directory back Todo folder with cd .. and install Mongoose
### Intall Mongoose
npm install mongoose
![image](https://user-images.githubusercontent.com/53397202/190872994-778ec154-3375-4234-835d-c0182417de02.png)
### Create model
mkdir models
### Change to model
cd model
### create todo.js file inside models
touch todo.js
### you can define all the command at once
mkdir models && cd models && touch todo.js
### Open todo and paste (some ....)
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
### Now we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model. In Routes directory, open api.js with vim api.js, delete the code inside with :%d command and paste there code below into it then save and exit
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
### Sign up to MongoDb and configure
create a file in Todo foldetr
touch .env
### Open the file
vi .env
### Add the connection string to access the database in it, just as below:
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
### Start node.js
  node index.js
 ![image](https://user-images.githubusercontent.com/53397202/190877154-6fcd0faa-3427-469d-8add-e67642063c93.png)
 
You shall see a message ‘Database connected successfully’, if so – we have our backend configured. Now we are going to test it.

Testing Backend Code without Frontend using RESTful API
So far we have written backend part of our To-Do application, and configured a database, but we do not have a frontend UI yet. We need ReactJS code to achieve that. But during development, we will need a way to test our code using RESTfulL API. Therefore, we will need to make use of some API development client to test our code.

In this project, we will use Postman to test our API.
Click Install Postman to download and install postman on your machine.

Click HERE to learn how perform CRUD operartions on Postman

You should test all the API endpoints and make sure they are working. For the endpoints that require body, you should send JSON back with the necessary fields since it’s what we setup in our code.

Now open your Postman, create a POST request to the API http://<PublicIP-or-PublicDNS>:5000/api/todos. This request sends a new task to our To-Do list so the application could store it in the database.
 
### Post in postman
 ![image](https://user-images.githubusercontent.com/53397202/190901808-f0ba0d64-fdea-43e0-b158-f3dc270561c9.png)
### for Get in Postman
 ![image](https://user-images.githubusercontent.com/53397202/190901872-1cd2ea2c-a8c6-4789-b65c-ccfae1fbc427.png)
### Delete
 ![image](https://user-images.githubusercontent.com/53397202/190902019-6d104bbb-ea49-4442-ac69-4eceaf6654f0.png)
### Frontend creation
 it is time to create a user interface for a Web client (browser) to interact with the application via API. To start out with the frontend of the To-do app, we will use the create-react-app command to scaffold our app.
 * npx create-react-app client*
![image](https://user-images.githubusercontent.com/53397202/190902235-5dd0f64f-facf-46ae-9648-4daa69eb63b6.png)
 
# Running a React App
Before testing the react app, there are some dependencies that need to be installed.
 
1. Install concurrently. It is used to run more than one command simultaneously from the same terminal window.
 *npm install concurrently --save-dev*
 ![image](https://user-images.githubusercontent.com/53397202/190902348-e22e5103-99a1-4680-9a8e-cc276a13aba8.png)

2. Install nodemon. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.
 *npm install nodemon --save-dev*
 ![image](https://user-images.githubusercontent.com/53397202/190902384-df9057dd-f19c-4157-9553-8b5bf739f9ec.png)
 
 3. In Todo folder open the package.json file. Change the highlighted part of the below screenshot and replace with the code below.
 
### Configure Proxy in package.json
Change directory to ‘client’
*cd client*
Open the package.json file
*vi package.json*
Add the key value pair in the package.json file "proxy": "http://localhost:5000".
The whole purpose of adding the proxy configuration in number 3 above is to make it possible to access the application directly from the browser by simply calling the server url like http://localhost:5000 rather than always including the entire path like http://localhost:5000/api/todos
 Now, ensure you are inside the Todo directory, and simply do:
 *npm run dev*
 ![image](https://user-images.githubusercontent.com/53397202/190904403-73e380ab-c318-461e-a630-d3786eed7a97.png)
 
Important note: In order to be able to access the application from the Internet you have to open TCP port 3000 on EC2 by adding a new Security Group rule. You already know how to do it.
Creating your React Components
One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. For our Todo app, there will be two stateful components and one stateless component.
From your Todo directory run
### Change to client
 cd client
 cd src
 Inside your src folder create another folder called components
 mkdir components
 Inside ‘components’ directory create three files Input.js, ListTodo.js and Todo.js.
Open Input.js file and Copy and paste the following
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
 To make use of Axios, which is a Promise based HTTP client for the browser and node.js, you need to cd into your client from your terminal and run yarn add axios or npm install axios.

Move to the src folder
 cd .. (2x)
### Install Axios
 ![image](https://user-images.githubusercontent.com/53397202/190908252-f420be32-65e1-4b0e-8956-60d023745d7a.png)
### change to src and components
 cd src/components
### After that open your ListTodo.js
 vi ListTodo.js
import React from 'react';

const ListTodo = ({ todos, deleteTodo }) => {

return (
<ul>
{
todos &&
todos.length > 0 ?
(
todos.map(todo => {
return (
<li key={todo._id} onClick={() => deleteTodo(todo._id)}>{todo.action}</li>
)
})
)
:
(
<li>No todo(s) left</li>
)
}
</ul>
)
}

export default ListTodo
### Open Todo.js file you write the following code
 import React, {Component} from 'react';
import axios from 'axios';

import Input from './Input';
import ListTodo from './ListTodo';

class Todo extends Component {

state = {
todos: []
}

componentDidMount(){
this.getTodos();
}

getTodos = () => {
axios.get('/api/todos')
.then(res => {
if(res.data){
this.setState({
todos: res.data
})
}
})
.catch(err => console.log(err))
}

deleteTodo = (id) => {

    axios.delete(`/api/todos/${id}`)
      .then(res => {
        if(res.data){
          this.getTodos()
        }
      })
      .catch(err => console.log(err))

}

render() {
let { todos } = this.state;

    return(
      <div>
        <h1>My Todo(s)</h1>
        <Input getTodos={this.getTodos}/>
        <ListTodo todos={todos} deleteTodo={this.deleteTodo}/>
      </div>
    )

}
}

export default Todo;
### We need to make little adjustment to our react code. Delete the logo and adjust our App.js to look like this.
Move to the src folder 
### In src folder run open
 vi App.js
delete the initial import logo and paste the following:
 import React from 'react';

import Todo from './components/Todo';
import './App.css';

const App = () => {
return (
<div className="App">
<Todo />
</div>
);
}
 

export default App;
 
 
 # Open App.css
 vi App.css
 copy and paste
 .App {
text-align: center;
font-size: calc(10px + 2vmin);
width: 60%;
margin-left: auto;
margin-right: auto;
}

input {
height: 40px;
width: 50%;
border: none;
border-bottom: 2px #101113 solid;
background: none;
font-size: 1.5rem;
color: #787a80;
}

input:focus {
outline: none;
}

button {
width: 25%;
height: 45px;
border: none;
margin-left: 10px;
font-size: 25px;
background: #101113;
border-radius: 5px;
color: #787a80;
cursor: pointer;
}

button:focus {
outline: none;
}

ul {
list-style: none;
text-align: left;
padding: 15px;
background: #171a1f;
border-radius: 5px;
}

li {
padding: 15px;
font-size: 1.5rem;
margin-bottom: 15px;
background: #282c34;
border-radius: 5px;
overflow-wrap: break-word;
cursor: pointer;
}

@media only screen and (min-width: 300px) {
.App {
width: 80%;
}

input {
width: 100%
}

button {
width: 100%;
margin-top: 15px;
margin-left: 0;
}
}

@media only screen and (min-width: 640px) {
.App {
width: 60%;
}

input {
width: 50%;
}

button {
width: 30%;
margin-left: 10px;
margin-top: 0;
}
}
 
 # Open index.css
 vim index.css
 copy and paste
 body {
margin: 0;
padding: 0;
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
"Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
sans-serif;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
box-sizing: border-box;
background-color: #282c34;
color: #787a80;
}

code {
font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
monospace;
}
 ![image](https://user-images.githubusercontent.com/53397202/190911189-7f676ae2-8cdb-4c79-b5dd-6223da067d9e.png)
 
 ### Run the code below when change to Todo folder
 npm run dev
 ![image](https://user-images.githubusercontent.com/53397202/190911393-cbde8291-ce8d-42c6-b928-0b9fa52453b4.png)



