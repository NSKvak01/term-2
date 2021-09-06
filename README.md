## Easier way to code if statement if there are only two conditions - ternary statement
```
if (n === undefined){
  return array[0]
} else {
  return array.slice(0, n)
}
```

is the same as 

`return n === undefined ? array[0] : array.slice(0, n)`

if there is one condition we use &&

`return n===undefined && array[0]`


## How to use slice with Math.max

```
let newArr = []
  if(n<array.length){
    for(let i=array.length-n; i<array.length;i++){
      newArr.push(array[i])
    }
  } else if(n>=array.length) {
    for(let i=0; i<array.length;i++){
      newArr.push(array[i])
    }
  } else if(n===0){
    newArr=[]
  } else if(n===undefined){
    newArr=array[array.length-1]
  }
  return newArr
  ```
  is the same as

  ```
  if(n !== undefined){
    return array.slice(Math.max(0,array.length-n))
  } else {
    return array[array.length-1]
  }
  ```


## instanceof 

`if (collection instanceof Array)`

## typeof
```
console.log(typeof 42);
// expected output: "number"

console.log(typeof 'blubber');
// expected output: "string"

console.log(typeof true);
// expected output: "boolean"

console.log(typeof undeclaredVariable);
// expected output: "undefined"
```


.map - loops only through array
_.map - loops through array and objects



## node

* Create folder
* npm init
* main - server.js (it's gonna look for this file later)
* enter
* inside the folder: touch server.js
* touch index.js
* npm install -d
* package-lock.js makes sure that all people are working on the same version of node
* inside the server.js type

```
const fs = require('fs')
const http = require('http')

http
    .createServer(function(req, res){
        if (req.url ==='/'){
            fs.readFile("index.html", function (err, data){
                if(err){
                    res.end(err)
                } else {
                    res.writeHead(200, {"content-Type":"text/html"})
                    res.write(data)
                    return res.end()
                }
            })
        }
    })
    .listen(3000, function(){
        console.log("Server started")
    })
```


* sudo npm install nodemon -g
* then run: nodemon server.js (or any other file)

* ctrl+c - exits from node


## Postman
* get - retrieve
* post - create
* put - update
* delete - delete 

CRUD - create, retrieve, update, delete

```
const fs = require('fs')
const http = require('http')

http
    .createServer(function(req, res){
        if (req.url ==='/'){
            fs.readFile("text.txt", function (err, data){
                if(err){
                    res.end(err)
                } else {
                    res.writeHead(200, {"content-Type":"text/html"})
                    res.write(data)
                    return res.end()
                }
            })
        }
        console.log(req.url)
        console.log(req.method)
        if(req.url === "/create-a-file" && req.method === "POST"){
          res.end("OK!")  
        }
    })
    .listen(3000, function(){
        console.log("Server started")
    })
    
```

endpoint = url

## Create a file
```
const fs = require('fs')
const http = require('http')

http
    .createServer(function(req, res){
        if (req.url ==='/'){
            fs.readFile("text.txt", function (err, data){
                if(err){
                    res.end(err)
                } else {
                    res.writeHead(200, {"content-Type":"text/html"})
                    res.write(data)
                    return res.end()
                }
            })
        }
        console.log(req.url)
        console.log(req.method)
        if(req.url === "/create-a-file" && req.method === "POST"){
            fs.writeFile("text.txt", 'w', function(err){
                if(err){
                    res.end(err)
                } else {
                    res.end('file created')
                }
            })  
        }
    })
    .listen(3000, function(){
        console.log("Server started")
    })
```

Dynamic version of this code:
```
const fs = require('fs')
const http = require('http')

http
    .createServer(function(req, res){
        if (req.url ==='/'){
            fs.readFile("text.txt", function (err, data){
                if(err){
                    res.end(err)
                } else {
                    res.writeHead(200, {"content-Type":"text/html"})
                    res.write(data)
                    return res.end()
                }
            })
        }
        console.log(req.url)
        console.log(req.method)
        if(req.url === "/create-a-file" && req.method === "POST"){
            let body = ""
            req.on("data", function(data){
                body += data.toString()
            })

            req.on("end", function (){
                let parsedBody = JSON.parse(body)
                fs.writeFile(parsedBody.fileName, parsedBody.message, function(err){
                    if(err){
                        res.end(err)
                    } else {
                        res.end('file created')
                    }
                })
            })  
        }
    })
    .listen(3000, function(){
        console.log("Server started")
    })
```

* fs.unlink - to delete file
* fs.appendFile - to update the file


## Express

### Set express in terminal
* Create a folder
* npm init
* for entry point type app.js
* touch app.js
* npm i express

### Set express in js
```
const express =ruquire.express()
const app - express()

app.listener(3000, function(){
  console.log(`Server is running on PORT: $(3000)`)
  res.json({
    name:"hamster", 
    friends:["tomy", "ego", "john"].
    food:{
      food1:"candies", 
      food2:"burgers"
    }, 
    boolean1:true,
    boolean2:false,
    number:123
  })
```

To make url dynamic use `req.params.product`
###### Example:
```
  app.get("/:product", function (req, res){
    res.json({
      price:100, 
      type:req.params.product
    })
  })
})
```
With the list of pages it can look like this
###### Example:
```
let teams = [
  {team: "celtics"}, 
  {team: "bulls}, 
  {team:"lakers"}
]
app.get('/:teams', function(req, res){
  let foundTeam = teams.map((item)=> {
    if (request.params.teams ===item.team){
      return team
    }

  res.json(
    foundTeam
  )
}) 
```

* app.get
###### Example:
```
app.get('/', function (req, res){
  app.send('Hello')
})
```

* res.send - prints something on the page
* res.json
* app.set - shows the folder using "views" and the type of the file using "view engine"
#####  Path
  * __dirname - is the path to the current file
  * `path.join(__dirname, "views")` - joins the previous path to another folder
```
const path = require("path")

app.set("views", path.join(__dirname, "views"));
app.set("view engine", "ejs");
```

* res.render - connects it to the html file from js side
```
app.get("/", function (req, res){
  res.render("index")
}
```
`const teamRouter = require("./routes/team)` - if there is a dot in the path, it means that we are creating the folder


`app.use("/api/team), teamRouter)` - means that we are gonna use teamRouter when in api/team url. It says use this before and after application.

### Router
``` 
const router = express.Router()
module.exports = router
```

When we type url?name=lakers we use req.query
```
router.get('/), function(req, res){
  console.log(req.query)
  let foundTeam
  if(req.query{
    team.name ===req.query.name){
      foundTeam = team
    }
  })
}
```
## Morgan
Morgan - shows requests we are making and what path we are on - it calls middleware (or abilities)
* in terminal type npm i morgan
* in js:
```
const logger = require("morgan")
app.use(logger("dev"))
app.use(express.json())
```

`app.use(express.json())` - ability to parse json

## MVC
* Model - database
* View - client - show on screen
* Controller - handle the logic

## Javascript template engines
* EJS
* Mustache
* pug

`npm i ejs` - to use ejs template


## EJS syntax

```
 <% if (user) { %>
    <div>
      Welcome back <%- user -%>
    </div>
    <% } else { %>
      <div>Please login</div>
      <% } %>
        <hr />
        <ul>
          <% teams.forEach(function(item) { %>
            <li>
              <%- item.team -%>
            </li>
            <% }); %>
        </ul>

```

in js
```
response.render ("index", {
  user:null,
  teams:[{team:"lakers"}, {team:"knicks"}, {team:"magic"}]
})
```
## Router
1. `const router = express.Router()`
2. `module.exports = router` - don't forget to export the file 
3. `const teamRouter = require("./routes/teamRouter")` - import route file in app.js
4. `app.use("/api/team", teamRouter)` - use this file


## Query
`req.query` - takes what's inside url and put it in json
###### Example
`localhost:3000/api/team?name=Nastya&age=26`
it will look like 
```
{
  "name":"Nastya",
  "age":26
}
```

### If need to loop through array
```
router.get("/", function (req, res){
  if(req.query){
    let foundTeam
    teamArray.forEach((item)=>{
      if (item.name === req.query.name){
        foundTeam = item
      }
    })
    return res.json({foundteam:foundTeam})
  } else{
  return res.json({ data:teamArray})
  }
})
```

## Changing json using post

uuid library for id
`const uuidv4 = require('uuid').v4`

router.put - to update json
```
router.put("/update-team/:name", function(req, res){
    res.json({name:req.params.name = "LAKERS"})
})
```
### indexOf VS findIndex

```
let isFound = teamArray.findIndex(function(element){
    return element.name === "bulls"
})
```

is the same as 
```
let isFound = teamArray.map(e=>e.maps).indexOf("bulls")
```
### Retrieving syntax
```
const {id, name, type} = req.params
```
is the same as

```
const id = req.params.id
const name = req.params.name
const type = req.params.type
```

### To change status when showing an error
`res.status(404).json({message:"not found"})`


### Express generator
It will create all folders and files
* `npm install -g express-generator`
* `sudo npm install -g express-generator`
* `express express-generator-demo --view=ejs`
* `npm i`
---
`npm uninstall ejs` - to delete ejs

## Mongoose
* `npm i mongoose` - to install mongoose 


* Create users folders inside that folder create controller folder with userController.js file inside and model folder with User.js file and usersRouter.js file inside users folder.
* Inside User.js file 
```
const mongoose = require('mongoose')

const userSchema = new mongoose.Schema({
  firstName:{
        type:String,
    },
    lastName:{
        type:String
    },
    email:{
        type:String
    }, 
    password:{
        type:String
    }, 
    username:{
        type:String
    }
})

module.exports = mongoose.model("user", userSchema)
```
* in app.js add this code
```
const mongoose = require("mongoose")
mongoose  
  .connect("mongodb://localhost:27017/express-mongodb-intro", {
    useNewUrlParser: true,
    useUnifiedTopology: true
  })
  .then(()=>{
    console.log("MongoDB connected")
  })
  .catch(function(e){
    console.log(e)
  })
```


## New keyword creates a mongodb object

Usercontroller.js
```
const User = require ('../model/User')

module.exports = {
    getAllUsers: function(callback) {
        User.findOneAndUpdate({}, function (err, payload){
            if(err){
                callback(err, null)
            } else {
                callback(null, payload)
            }
        })
    }
}
```

for get request we use User.find
for post request we use User.save
for put request we use User.findByIdAndUpdate
for delete request we use User.findByIdAndDelete

## MVC
Model -> Controller -> usersRouter

### Model
In model, we create schema/template for data and assign type of data.

```
const mongoose = require('mongoose')

const recipeSchema = new mongoose.Schema({
    recipeName:String
})

module.exports = mongoose.model("recipe", recipeSchema)
```

### Controller
In controller, we bring model and create functions that will check errs and manipulater databases

```
const Recipe = require('../model/Recipe')

module.exports = {
    getAllRecipe:function(callback){
        Recipe.find({}, function (err, payload){
            if(err){
                callback(err, null)
            } else {
                callback(null, payload)
            }
        })
    },
    createRecipe: function(body,callback){
        let createdRecipe = new Recipe ({
            recipeName:body.recipeName
        })
        createdRecipe.save(function(err, payload){
            if (err){
                callback(err, null)
            }else {
                callback(null, payload)
            }
        })
    },
    updateUserByID: function(id, body, callback){}
}
```

In router, we use express and do CRUD methods with functions from controller

* ### GET
```
router.get('/get-all-users', function(req, res){
  userController.getAllUsers(function (some, pay){
    if(some) {
      res.status(500).json({message:"Error", error:some})
    } else {
      res.json({message:"Success", data:pay})
    }
  })
})
```
in controller
```
 getAllUsers: function(callback) {
        User.find({}, function (err, payload){
            if(err){
                callback(err, null)
            } else {
                callback(null, payload)
            }
        })
    },
```
* ### POST
```
router.post('/create-user', function (req, res){
  userController.createUser(req.body, function(err, payload){
    
    if(err){
      res.status(500).json({message:"Error", error:err })
    } else {
      res.json({message:"Success", data: payload})
    }
  })
})
```
in controller
```
 createUser: function(body, callback){
        let createdUser = new User({
            firstName:body.firstName,
            lastName:body.lastName,
            password: body.password,
            email:body.email,
            username:body.username
        })

        createdUser.save(function(err, payload){
            if(err){
                callback(err, null)
            } else{
                callback(null, payload)
            }
        })
    }
```
* ### PUT
```
router.put('/update-user-by-id/:id', function (req, res){
  userController.updateUserByID(
    req.params.id,
    req.body,
    function(err, updatedPayload){
      if (err){
        res.status(500).json({message:"Error", error:err})
      }else {
        res.json({message:"Success", data:updatedPayload})
      }
    }
  )
})
```
in controller
```
updateUserByID: function(id, body, callback){
        User.findByIdAndUpdate(
            {_id:id}, 
            body,
            {new: true},
            function (err, updatePayload){
                if(err){
                    callback(err, null)
                } else {
                    callback(null, updatedPayload)
                }
            }
        )
    }

```

### DELETE
```
router.delete('/delete-user-by-id/:id', function(req,res){
  userController.deleteUserByID(
    req.params.id, 
    function(err, deletedPayload){
    if (err){
      res.status(500).json({
        message:"Error", error:err
      })
    } else{
      res.json({message:"Success", data:deletedPayload})
    }
  })
})
```
in controller
```
deleteUserByID:function(id, callback){
        User.findByIdAndDelete(
            {_id:id},
            function(err, deletedPayload){
                if(err){
                    callback(err, null)
                }else {
                    callback(null, deletedPayload)
                }
            }

        )
    }
```

## Callback hell

#### Hash and bcrypt
* `npm i bcryptjs`
* in controller type `var bcrypt = require('bcryptjs')`
* then use bcrypt to hash passwords
```
 createUser: function (body, callback){
        bcrypt.genSalt(10, function(err, salt){
            if (err) {
                callback(err, null)
            } else {
                bcrypt.hash(body.password, salt, function(err,hash){
                    if(err){
                        callback(err, null)
                    } else{
                        let savedUser = new User({
                            firstName:body.firstName,
                            lastName:body.lastName,
                            password: hash,
                            email:body.email,
                            username:body.username
                        })
                        savedUser.save(function(err, payload){
                            if(err){
                                callback(err,null)
                            } else {
                                callback(null, payload)
                            }
                        })
                    }
                })
            }
        })
    },
```

∆ this pyramid is called callback hell.


# Promises
* ### Get
In controller
```
getAllUsers: function() {
        return new Promise ((resolve, reject)=>{
            User.find({})
                .then((payload)=>{
                    resolve(payload)
                })
                .catch((error)=>{
                    reject(error)
                })
        })
    },
```
In router
```
var {getAllUsers} = require('./controller/userController')

router.get('/get-all-users', function(req, res){
  getAllUsers() 
      .then((payload)=>{
        res.json({message:"Success", payload})
      })
      .catch((error)=>{
        res.status(500).json({message:"Error", error})
      })
})
```
* ### post
In controller
```
createUser: function (body){
        return new Promise ((resolve, reject)=>{
            bcrypt
                .genSalt(10)
                .then((salt)=>{
                    return bcrypt.hash(body.password, salt)
                })
                .then((hashedPassword)=>{
                    let savedUser = new User({
                        firstName:body.firstName,
                        lastName:body.lastName,
                        password: hashedPassword,
                        email:body.email,
                        username:body.username
                    })
                    return savedUser.save()
                })
                .then((savedUser)=>{
                    resolve(savedUser)
                })
                .catch((error)=>{
                    reject(error)
                })
        })
    }
```
In router
```
router.post('/create-user', function (req, res){
  createUser(req.body)
    .then((payload)=>{
      res.json({message:"Success", payload})
    })
    .catch((error)=>{
      res.status(500).json({message:"Error", error})
    })
})
```

# Async/await
### Get
In controller
```
router.get('/get-all-users', async function(req, res){
  try{
    let foundAllUsers = await getAllUsers()
    res.json({message:"Success", foundAllUsers})
  } catch(error){
    res.status(500).json({message:"error", error:error.message})
  }
})
```
in router
```
async function getAllUsers(){
    try{
        let foundAllUsers = await User.find({})
        return foundAllUsers
    } catch(error){
        return error
    }
}

module.exports = {
    getAllUsers
    }
```

In try, we need to store function from controller into variable (it's gonna be our pauload), then do res.json
and in catch do res.json for error


If mongoDB doesn't work, use this code in terminal `brew services start mongodb-community@4.4`

## Package VS library
Package follows JS, are basically like shortcuts to get certain features like bcrypt or validator

Libraries are more complicated and set new rules of syntax. React is a library

### Validator.JS
Helps to validate passwords, emails, usernames and so on. 
* npm i validator
* ```
let {isEmail, isStrongPassword, isAlpha} = require("validator")


### res.locals
to save variable across the app in the first file we should put 
`res.locals.example = example`
and to extract it
`const {example} = res.locals`

## dotenv and jsonwebtoken

`npm i dotenv jsonwebtoken`

jwt - to set expiration of logged in status
* in controller in login in sucess part type
```
let jwtToken = jwt.sign({email:foundUser.email, username:foundUser.username}, 
  "cheeseburger007greatday",
  {
  expiresIn:"1d"
  }
)
```

* in .gitignore 
```
/node_modules
.env
```
* create env globally
and inside env file type
```
MONGO_DB = "mongodb://localhost:27017/backend-api"

PRIVATE_JWT_KEY = "somekey"
```

* in controller instead of actual key type 
```
 let jwtToken = jwt.sign({email:foundUser.email, username:foundUser.username}, 
  process.env.PRIVATE_JWT_KEY,
  {
  expiresIn:"1d"
  }
)
```
* in server.js, bring dotenv 
`require("dotenv").config()`
* in mongoose connect part, instead of actual path to port type 
`process.env.MONGO_DB`

## Closure
When returning funciton inside the funciton
```
function outerFunc(num1){
  return function innerFunc(num2){
    return num1 + num2
  }
}

let closure = outerFunc(5)

closure(5)
```

### this - is a keyword that looks for the closest object
```
let johny = {
  name:"Johny Bravo",
  sayName: function (){
    console.log(this)
  }
}

johny.sayName()
```
we can change it to
```
let sayNameFunc = function(obj){
  obj.sayName = function(){
    console.log(`Hi, my name is ${this.name}`)
  }
  return obj
}

let john = sayNameFunc({name:"Johny bravo"})
john.sayName()
```
* ### Call
Calls objects right into function but one by one
```
let sayName = function(food1, food2, food3, food4){
  console.log(`hi, my name is ${this.name} and my favorite food is ${food1}, ${food2}, ${food3}, and ${food4}`)
}

let john = {
  name:"john",
  hobby:"basket"
}

let favoriteFood = ["bacon", "juice", "steak", "veggies"]

sayName.call(john, favoriteFood[0], favoriteFood[1], favoriteFood[2], favoriteFood[3])
```
there is the way to call ecerything from the list using one variable
```
sayName.call(john, ... favoriteFood)
```

* ### Apply
Apply the whole array
```
let sayName = function(food1, food2, food3, food4){
  console.log(`hi, my name is ${this.name} and my favorite food is ${food1}, ${food2}, ${food3}, and ${food4}`)
}

let john = {
  name:"john",
  hobby:"basket"
}

let favoriteFood = ["bacon", "juice", "steak", "veggies"]

sayName.apply(john, favoriteFood)
```

* ### Merging two arrays using three dots
```
let array = [1,2,3]

let newArray = [4,5,6...array]
```
or 
```
sayName.call(john, ... favoriteFood)
```
* ### bind
Saves a function into a variable that can be used later (apply and call can't store it)
```
let sayName = function(food1, food2, food3, food4){
  console.log(`hi, my name is ${this.name} and my favorite food is ${food1}, ${food2}, ${food3}, and ${food4}`)
}

let john = {
  name:"john",
  hobby:"basket"
}

let favoriteFood = ["bacon", "juice", "steak", "veggies"]

let newFunc = sayName.bind(john, ... favoriteFood)

newFunc()
```

* ### new
New create "this" keyword. If we are using "this" in a function we need "new" before function otherwise there is no object to refer to
```
function Robot(name, type, color){
  this.name = name
  this.type = type
  this.color = color

  this.sayName = function () {
    console.log(this)
    console.log(`I am ${this.name}. A ${this.type} robot and my color is ${this.color}`)
  }
}

let battleRobot = new Robot('Optimus prime', "Destroyer", "red and blue")
let medicRobot = new Robot('Bumbee', "Medic", "yellow")

// battleRobot.sayName()
medicRobot.sayName()
```

## Global 
There is no parameter in function, it will grab global one, but new parameter will overwrite it, it there is this.name inside the function, it will overwrite everything
```
window.name = "johny bravo"
  // or global.name if working in node.js

let sayName = function(){
  // this.name = "Lucy"
  console.log(`my name is ${this.name}`)
}

let person1 = {
  name:"dexter"
}
sayName.call(person1)
sayName.apply(person1)

sayName()
```
## Class
```
class Robot {
  constructor(name, color, battery){
    this.name = name
    this.color = color
    this.battery = battery
  }
  greeting() {
    console.log(`My name is ${this.name}`)
    this.battery -= 1
  }
  sayColor(){
    console.log(`My color is ${this.color}`)
    this.battery -=1
  }
  checkBatteryHealth(){
    console.log(`My battery is at ${this.battery}%`)
  }
  chargeBattery(energy){
    this.battery +=energy
    console.log(`Battery charged. Battery level is at ${this.battery}%`)
  }
}

let prime = new Robot("optimus prime", "black", 1000)
prime.greeting()
prime.sayColor()
prime.chargeBattery(2)
prime.checkBatteryHealth()
```

if you need to use the funciton inside the class that was deifned inside the class we first should bind it and create in a model and then call it later
```
class Robot {
  constructor(name, color, battery){
    this.name = name
    this.color = color
    this.battery = battery

    this.checkBatteryHealth = this.checkBatteryHealth.bind(this)
  }
  checkBatteryHealth(){
    console.log(`My battery is at ${this.battery}%`)
  }
  chargeBattery(energy){
    this.battery +=energy
    console.log(`Battery charged. Battery level is at ${this.battery}%`)
    this.checkBatteryHealth()
  }
}

let prime = new Robot("optimus prime", "black", 1000)
prime.greeting()
prime.sayColor()
prime.chargeBattery(2)

```
or you can use arrow functions because it automatically bind to the closest scope
```
class Robot {
  constructor(name, color, battery){
    this.name = name
    this.color = color
    this.battery = battery

  }
  checkBatteryHealth = () => {
    console.log(`My battery is at ${this.battery}%`)
  }
  chargeBattery = (energy) => {
    this.battery +=energy
    console.log(`Battery charged. Battery level is at ${this.battery}%`)
    this.checkBatteryHealth()
  }
}

let prime = new Robot("optimus prime", "black", 1000)
prime.greeting()
prime.sayColor()
prime.chargeBattery(2)
```

### to create a new class using existing one
new class with extends always have an access to previous functions
```
class Defender extends Robot{
constructor(name, color, battery, shield){
  super(name, color, battery)
  this.shield = shield
}
}
```

# React
To start react:
* `npx create-react-app name-of-the-project`
* `cd name-of-the-project`
* `npm run start` - to get localhost opened
If react doesn't work on M1 chip try this code:
* `brew upgrade node`


* `import` is the same as `const variable = require('/)`
* in App.js type `rce` and the template will show up

* first it brings the react and component 
* then creates a class extending component class
* inside the class it grabs jsx and 
* define functions (use either bind or arrow functions)
* then render jsx and use these functions
* to use style we need double brakets 
* for js we need single curly brakets
* if we want to use 50px, we can just type 50 , but "50%"
* to update the number on screen use `this.setState`

```
import React, { Component } from 'react'

export class App extends Component {
  constructor(props){
    super(props)

    this.state = {
      count: 0
    }
  }
  addCount = () => {
    this.setState({
      count:this.state.count+1
    })
  }
  minusCount = () => {
    this.setState({
      count:this.state.count - 1
    })
  }
  render() {
    return (
      <div style = {{textAlign:"center", marginTop:50}}>
        <div>Count:{this.state.count}</div>
        <button onClick={this.minusCount}>-</button>
        <button onClick={this.addCount}>+</button>
      </div>
    )
  }
}

export default App

```

## className VS style
We bring style from down there or from inline style
className is from separate css file

### Tree ways of doing style:
* use styles
```
<div style={styles.divStyle}></div>

<!-- outside of the class create styles -->

const styles = {
  divStyle:{
    height: "350px",
    backgroundColor:"yellow"
  }
}
```
* inline style
```
<div
        style  = {{textAlign:"center", marginTop:50}}>
</div>
```
* bring css file
```
<div className = {`toggle-me-original toggle-me-div`}></div>
```
In className we can use logic 
```
<div className = {`toggle-me-div ${
this.state.toggleMe
?"toggle-me-original" 
: "toggle-me-not-original"}`}>
<button onClick={this.toggleMeColor}>Toggle me</button>
</div>
```

### Prev state
it rememebers the whole state
```
this.setState((prevState) => {
  return{
    toggleMe:true
  }
})
}
```
without prev state it looks like this

```
toggleMeColor = () => {
    this.setState({
      toggleMe: !this.state.toggleMe
    })
  }
```
## Child
* To create any child.js we need to create components folder and put the file there
* We need to import child to app.js
* We can just render `<Child />`
#### If not binding anything,just using arrow functions, we don't need to use constructor

In app.js we can type
```
<Child1 name="Joe" age={10}/>
<br />
<Child1 name="Cathy" age={5}/>
<br />
<Child1 name="Mike" age={15} />
```

and in child.js
```
<div>
Hi, my name is {this.props.name} age {this.props.age}</div>
```
name that was defined in app.js will be part of props and can be used in child.js 

* When setting timeout for child and manipulating child in app.js, it probably will manipulate before child will appear, that's why we need `componentWillUnmount`
```
class Child1 extends Component {
  state = {
    pokemon:"pikachu"
  }


  componentDidMount (){
    this.timer = window.setTimeout(()=>{
    this.setState({
      pokemon:"Mew 2"
    })
    }, 2000)
  }

  componentWillUnmount(){
    clearTimeout(this.timer)
  }
  render(){
    return 
    <div>
      Child Component: {this.state.pokemon}
    </div>
  }
}
```

## Without constructor
```
import React, { Component } from 'react'

export class App extends Component {
  state={
    
  }
  render() {
    return (
      <div>
        
      </div>
    )
  }
}

export default App
```

* ## componentDidMount
It runs only once and overwrites the initial state.

* ## componentDidUpdate
Whenever state is trigurred it's gonna run componentDidUpdate. It remebers only previous state.

* ## shouldComponentUpdate
Takes nextProps and nextState
to prevent from updating
```
shouldComponentUpdate(nextProps, nextState){
  if(nextState.username ==="goku"){
    return false
  } else{
    return true
  }
}
```


### The order of execution:
1. constructor
2. render
3. componentDidMount
4. shouldComponentUpdate -> either true or false
5. componentDidUpdate

#### When we set timeout we need to clear it before doing anything else (when loading the page but clicked on another page, we need to stop loading the previous page):
```
componentWillAmount(){
  clearTimeout(this.timer)
}
```
## Can you tell us about REACT?
* REACT has life-cycle methods
* It starts with a constructor
* Then render
* then component did mount
* If there will be any updates, should component update will get called (returning true or false)
* If returning true, component did update will run

## Update TODO list
```
import React, { Component } from 'react'
import {v4 as uuidv4} from "uuid"
import "./Todo.css"
export class Todo extends Component {
    state={
        todoList:[
            {
                id:uuidv4(),
                todo:"a"
            },
            {
                id:uuidv4(),
                todo:"b"
            },
            {
                id:uuidv4(),
                todo:"c"
            },

            ]   
    }

    handleTodoOnChange = (e)=>{
        this.setState({
            todoInput:e.target.value
        })
    }

    handleOnSubmit = (e)=>{
        e.preventDefault()
        let newArray = [...this.state.todoList, {
            id:uuidv4(),
            todo:this.state.todoInput
        }]
        this.setState({
            todoList:newArray
        })
    }
    render() {
        return (
            <div className="todo-div">
                <form onSubmit={this.handleOnSubmit}>
                    <input name="todoInput" type="text" onChange={this.handleTodoOnChange} />
                </form>
                <div className="todo-div">
                    <ul >
                    {this.state.todoList.map((item, index)=>{
                        return <li key={index}>{item.todo}</li>
                    })}
                    </ul>
                </div>
            </div>
        )
    }
}

export default Todo
```
* Don't forget to preventDefault so the whole page is not refreshed
* Don't push into array use ...
```
handleOnSubmit = (e)=>{
  e.preventDefault()
  let newArray = [...this.state.todoList, {
      id:uuidv4(),
      todo:this.state.todoInput
  }]
  this.setState({
      todoList:newArray
  })
}
```


* Delete todo
```
handleDeleteByID = (id)=>{
  let filteredArray = this.state.todoList.filter((item)=> item.id !== id)
  this.setState({
      todoList: filteredArray
  })
}
```

### 
* `npm install --save prop-types`
* `import PropTypes from "prop-types"`
* type in the end before export:
```
TodoList.propTypes = {
  item:PropTypes.object.isRequired,
}
```

## axios
we use it in componentDidiMount to handle HTTP request in browser without postman
```
async componentDidMount() {
        try {
            let allTodos = await axios.get(
                "http://localhost:3001/api/todo/get-all-todos"
            );
            console.log(allTodos);
            } catch (e) {
            console.log(e);
        }
    }    
```

We need to type this thing when want to post somethins before set state

### GET 
```
async componentDidMount() {
        try {
            let allTodos = await axios.get(
                "http://localhost:3001/api/todo/get-all-todos"
            );
            this.setState({
                todoList:allTodos.data.payload
            })
            console.log(this.state.todoList);
        } catch (e) {
            console.log(e);
        }
    }    
```

### POST

```
try {
    let createTodo = await axios.post(
        "http://localhost:3001/api/todo/create-todo",
        {
            todo:this.state.todoInput
        }
    )
    console.log(createTodo)
} catch (error) {
    console.log(error)
}
```

### DELETE
```
 handleDeleteByID = async (_id)=>{
    try {
      let deleteTodos = await axios.delete(
        `http://localhost:3001/api/todo/delete-todo/${_id}`,
        );
        let filteredArray = this.state.todoList.filter((item)=> item._id !== deleteTodos.data.payload._id)
        this.setState({
          todoList:filteredArray
        })
      console.log(deleteTodos)
  } catch (e) {
      console.log(e);
  }
}
```

### Sorting
* descending: descending, desc, -1, "-1"
We need to sort in back-end
```
async function getAllTodos(req,res){
    try {
        if(Object.keys(req.query).length === 0){
            let foundTodos = await Todo.find({})
            res.json({message:"success", payload:foundTodos})
        } else {
            let sortedTodo = await  Todo.find({}).sort({date: req.query.sort});
            res.json({message:"success", payload:sortedTodo})
        }
    } catch (error) {
        res.status(500).json({message:"error", error:error.message})
    }
}
```

and then in front-end
```
sortByDate = async (sort)=>{
        try {
            let sorted = await axios.get(`http://localhost:3001/api/todo/get-all-todos?sort=${sort}`)
            this.setState({
                todoList:sorted.data.payload
            })
            console.log(sorted)
            
        } catch (error) {
            console.log(error)
        }
    }
```

For true or false we can use -1 to show false value first and 1 to show true values first


### In class we can only have one outer div, but we can use `<></>` or `<React.Fragment></Reac.Fragment>`

Use `RFE` to have a template without class 
```
import React from 'react'

export default function Button() {
    return (
        <div>
            
        </div>
    )
}
```

### Focus on todoInput
```
componentDidUpdate(){
  let input = document.getElementById(this.props.ID)
  if(input){
      input.focus()
  }
}
```

### reset CSS
create _base.css file and import ion index.js in front end
```
html,
body,
div,
span,
applet,
object,
iframe,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
pre,
a,
abbr,
acronym,
address,
big,
cite,
code,
del,
dfn,
em,
img,
ins,
kbd,
q,
s,
samp,
small,
strike,
strong,
sub,
sup,
tt,
var,
b,
u,
i,
center,
dl,
dt,
dd,
ol,
ul,
li,
fieldset,
form,
label,
legend,
table,
caption,
tbody,
tfoot,
thead,
tr,
th,
td,
article,
aside,
canvas,
details,
embed,
figure,
figcaption,
footer,
header,
hgroup,
menu,
nav,
output,
ruby,
section,
summary,
time,
mark,
audio,
video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  display: block;
}
body {
  line-height: 1;
}
ol,
ul {
  list-style: none;
}
blockquote,
q {
  quotes: none;
}
blockquote:before,
blockquote:after,
q:before,
q:after {
  content: "";
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
img,
iframe {
  vertical-align: bottom;
  max-width: 100%;
}
input,
textarea,
select {
  font: inherit;
}
* {
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
}
```

### Emmet - built-in html shortcut
`div.` - to add class
`div#` - to add id 
`div.text{Sign up}`- then go to the end of the line and hit tab. Curly brackets mean the content
`div.*5` - will create 5 identical lines
`div.parent>div.child*5` - create 5 childs

### Dynamic handleOnChange
```
handleOnChange = (event) => {
  this.setState({
    [event.target.name] : event.target.value
  })
}
```

* ### setState function are asynchronous, if we need to check something, we should do it inside setState.
```
handleOnChange = (event) => {
  this.setState({
    [event.target.name] : event.target.value
  }, ()=>{
    if(this.state.firstName.length===0){
      console.log("firstName cannot be empty")
    }
  })
}
```

* onFocus - when you click on input
* OnBlur - when you click outside of the input

### React-router-dom
* npm i react-router-deom
* npm audit fix --force
* in App.js bring `import{BrowserRouter as Router, Route} from "react-router-dom"`

```
import{BrowserRouter as Router, Route} from "react-router-dom"
import Signup from './components/Signup/Signup'
import Home from "./components/Home/Home"
// import Login from "./components/"
import "./App.css"
import React from "react"


export class App extends Router {
  render() {
    return (
      <Router>
        <React.Fragment>
        <Route path="/sign-up" component={Signup} />
        <Route path="/" component={Home} />
        </React.Fragment>
      </Router>
    )
  }
}

export default App
```

### In react <a> equals <Link>. <Link> doesn't refresh the whole page lika <a>.
```
import {Link} from "react-router-dom"
<Link to="/">Movie with friends!</Link>
```

### Use <NavLink> to show user what page they are on
```
 <ul>
      <li>
          <NavLink activeClassName="selected" to="/sign-up">Sign up</NavLink>
      </li>
      <li>
          <NavLink activeStyle={{borderBottom:"1px solid white"}} to="/login">Login</NavLink></li>
  </ul>
```

### Axios

* create Axios.js in utils folder and paste this code
```
import axios from "axios"

const Axios = axios.create({
    baseURL: process.env.NODE_ENV === "development"
    ? "http://localhost:8080"
    :"DEPLOY CLOUD ADDRESS",
    timeout:50000
})

export default Axios
```
###### if there is no response in 5 econds, call will be cancelled

* in App.js put logger in if statement so it runs only in development
```
if (process.env.NODE_ENV === "development"){
    app.use(logger("dev"))
}
```

* in package.json under "scripts" add:
```
"start": "NODE_ENV=development nodemon server.js",
"build:prod":"NODE_ENV=production nodemon server.js"
```
If we type npm run start it will run development, if we type npm run build:prod it will be in production

Produciton is way faster than development

### Error handling
* In App.js bring errorController and ErrorMessageHandlerClass
```
const ErrorMessageHandlerClass = require ("./routes/utils/ErrorMessageHandlerClass")
const errorController = require("./routes/utils/errorController")
```
* in App.js put this code at the bottom before export
```
app.all("*", function (req,res, next){
    next(new ErrorMessageHandlerClass(
        `Cannot find ${res.originalUrl} on this server! Check your URL`, 404
    ))
})
app.use(errorController)

```
* in userController.js in post request catch (error) section type`next(error)` - it will trigger app.use(errorController) in App.js that will trigger errorController.
* in utils folder create errorController.js, where we create err.statusCode to be equal either the original or 500, we spread the operator to show object without huge message, and save it into the new error object and add err.message. Then, we check if there is a duplicate MongoDB error code, if yes, we create a new errorMessageHandlerClass. 
```
const ErrorMessageHandlerClass = require("./ErrorMessageHandlerClass");

function dispatchErrorDevelopment (error,req,res){
    if(req.originalUrl.startsWith('/api')){
        return res.status(error.statusCode).json({
            status:error.status,
            error:error,
            message:error.message,
            stack:error.stack
        })
    }
}
function dispatchErrorProduction (error,req,res){}

function handleMongoDBDuplicate(err){
    return new ErrorMessageHandlerClass(err,400)
}

module.exports = (err, req, res, next) =>{
    err.statusCode= err.statusCode || 500;
    err.status = err.status || "error"

    let error  = {...err}
    error.message = err.message

    if (error.code === 11000 || error.code === 11001){
        error = handleMongoDBDuplicate(error)
    }
    if(process.env.NODE_ENV === "development"){
        dispatchErrorDevelopment(error, req, res)
    } else{
        dispatchErrorProduction(error, req, res)
    }
}
```
* In utils create ErrorMessageHandlerClass.js file and put the following code
```
class ErrorMessageHandlerClass extends Error {
    constructor(message, statusCode){
        super(message, statusCode)
        this.statusCode = statusCode
        this.status = `${statusCode}`.startsWith("4") ?"fail":"error"
        this.isOperational = true
    }
}

module.exports  = ErrorMessageHandlerClass
```


### form
When using form to handle submit button we need to type `onSubmit` inside <form> not `onClick` inside <button>


### express-rate-limit
* use to limit the number of times user can try incorrect password
* npm i express-rate-limit
* const rateLimit = require("express-rate-limit");
```
const limiter = rateLimit({
    windows: 60 * 60 * 1000, // 15 minutes
    max: 5,
    message:"Too many requests"
});

app.use("/api/", limiter);
```
* in front end use status code to show toastify messages
```
...
catch (error) {
if(error.response.status === 429){
    toast.error('Too many failure requests', {
        position: "top-center",
        autoClose: 5000,
        hideProgressBar: false,
        closeOnClick: true,
        pauseOnHover: true,
        draggable: true,
        progress: undefined,
    })
}
```


* We need jwtToken generated in the backend to have access to other features that only logged-in users have, in `handleSubmitButton` under axios call type
```
let jwtToken = process.data.payload;
  window.localStorage.setItem("jwtToken", jwtToken)
```

## MainRouter
We need to toggle our nav bar depending on user state.
We create MainRouter that has all the components
```
import React, { Component } from 'react'
import{BrowserRouter as Router, Route} from "react-router-dom"
import Signup from './components/Signup/Signup'
import Login from "./components/Login/Login"
import Home from "./components/Home/Home"
import Nav from "./components/Nav/Nav"

const MainRouter = (props)=>{
    return (
        <Router>
        <Nav user={props.user}/>
            <React.Fragment>
                <Route exact path="/sign-up" component={Signup} />
                <Route exact path="/login"
                render={()=> <Login handleUserLogin={props.handleUserLogin}/>}/>
                <Route exact path="/" component={Home} />
            </React.Fragment>
        </Router>
        )
    }

export default MainRouter

```

## Nav.js
in Nav.js we toggle nav state
```
// 
import React, { Component } from "react";
// we bring link to link signup and sign in pages because <a> doesn't work in react
import { Link, NavLink } from "react-router-dom";
// bring nav css file
import "./Nav.css";
export class Nav extends Component {
  state = {
  }
  render() {
    return (
      <nav className="Navbar">
        <div className="h1-logo">
          <h1>
            {/* this h1 redirects to home page */}
            <Link to="/">Movie with friends!</Link>
          </h1>
        </div>
        <div className="right-side-nav">
          <ul>
            <li>
              {this.props.user ? 
              (<NavLink activeClassName="selected" to="/profile">
                Profile 
              </NavLink>
              ):(
                <NavLink activeClassName="selected" to="/sign-up">
                Sign up
                </NavLink>
              )}
            </li>
            <li>
              {this.state.user?
              (<NavLink
                activeStyle={{ borderBottom: "1px solid white" }}
                to="/profile"
              >
                Profile
              </NavLink>):
              (
                <NavLink
                activeStyle={{ borderBottom: "1px solid white" }}
                to="/login"
              >
                Login
              </NavLink>
              

              )}
            </li>
          </ul>
        </div>
      </nav>
    );
  }
}
// exports nav to use it in App.js
export default Nav;

```

### render

In main router get 
```
 <Route
    exact
    path="/login"
    render={({ history, location, match, staticContext }) => (
      <Login
        history={history}
        location={location}
        match={match}
        staticContext={staticContext}
        handleUserLogin={props.handleUserLogin}
      />
    )}
  />
  ```

is the same as

```
<Route exact path="/login"
  render={(routerProps)=> <Login {...routerProps} handleUserLogin={props.handleUserLogin}/>}/>
```

### Push
after we get routerProps in Login.js, in handleOnSubmit we need to use push to direct to another page

```
 this.props.history.push("/movie")
```

## Not allow to show login or signup pages to logged-in users

We cannot show these pages so in Login.js and Signup.js we use componentDidMount to check if there is jwt key, if yes, we push it to movie page.
```
componentDidMount(){
    let getJwtToken = window.localStorage.getItem("jwtToken")
    
    if(getJwtToken){
        const currentTime = Date.now() /1000
        let decodedJwtToken = jwtDecode (getJwtToken)
        if(decodedJwtToken.exp>currentTime){
            this.props.history.push("/movie")
        } else {
            
        }
    }
}
```

### PrivateRoute and Redirect
* Sometimes we need to redirect pages to login if user not logged-in. In this case we need to create PrivateRoute.js component and type the following code inside
```
import React from 'react'
import { Route, Redirect } from 'react-router-dom'
import checkUser from '../utils/checkUser'

const PrivateRoute = ({component:Component, ...rest})=>{
    return (
    <Route {...rest}
    render = {(routerProps)=>
        checkUser() ? <Component {...routerProps}/>
    : <Redirect to="/login" />}
        />
    )
}
    
export default PrivateRoute
```
* in MainRouter.js use Private route
```
<PrivateRoute exact path="/movie-detail/:movieTitle" component={MovieDetail} />
<PrivateRoute exact path="/movie" component={Movie} />
```

## Twilio
Use twilio for sending messages
* first we need hookup twilio to backend
* create a new twilioRouter.js file

```
const express = require("express");
const router = express.Router();
const jwtMiddleware = require("../utils/jwtMiddleWare")

const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
const client = require("twilio")(accountSid, authToken);
console.log(accountSid, authToken)
router.post("/send", jwtMiddleware,  (req, res) {
    client.messages
        .create({
            body: req.body.message,
            from: "+16514725167",
            to: "+16469456249",
        })
        .then((message) => res.json(message))
        .catch((error) => {
        console.log(error.message);
        res.status(error.status).json({ message: error.message, error });
    });
});
module.exports = router;
```
* in app.js bring twilioRouter and do `app.use('/api/sms', twilioRouter)`
* if there is "requre username" error check `require("dotenv").config()` in sever.js - it should be in the first line of the code, otherwise our hiddenapi keys in .env will be undefined

### jwtMiddleware
* create jwtMiddleware.js in utils folder
* type the following code
```
const jwt = require("jsonwebtoken")

const { modelName } = require("../user/model/User")

async function checkJwtToken (req,res, next){
    try {
        let decodedJwt = jwt.verify(jwtToken, process.env.PRIVATE_JWT_TOKEN)

        if(req.headers && req.headers.authorization){
            let jwtToken = req.headers.authorization.slice(7)
            next()
        } else{
            throw {message:"You don't have permission", statusCode:500}
        }
        console.log(req.headers)
    } catch (e) {
        return next(e)
        res.status(500).json({message:e.message, error:e})
    }
}

modelName.exports = checkJwtToken
```

* `throw` in else sttement goes directly to catch block and passes message and statusCode to catch block
* we also need to return `next()` in catch block and type `next()` in true part of if statement


# Parent-Child in hooks

We used to use selfClosing component tags,but if we use a closing tag everything in between becomes a Child

```
function App() {
  return (
    <div className="App">
      <Parent>
        <h1>Good morning class</h1>
      </Parent>
      <Parent>
        <Child />
        <Child2 />
        <Child3 />
      </Parent>
    </div>
  )
}

export default App
```

Son, in parent we can use props or extract shildren from the props

```
import React from 'react'

function Parent({children}) {
    return (
        <div>
            {children}
        </div>
    )
}

export default Parent
```

# Reducer

### App.js
In App.js we bring Counter and CounterContext (counterContextWrapper), and wrap Counter in CounterWrapper
```
import React from 'react'
import Counter from './components/Counter/Counter'
import CountContextWrapper from './components/context/CountContext'

function App() {

  return (
    <div className="App">
      <CountContextWrapper>
        <Counter />
      </CountContextWrapper>
    </div>
  )
}

export default App
```

### CounterContext.js
* Here we create counter context and bring reducer.
* Then we export CountContext 
* Create initial state
* In reducer,  we create cases. each case is a type that defines the action
* In count wrapper, we bring state and dispatch. Dispatch works like a callback.
* Render provider with value and child inside it.

```
import React, {useReducer} from "react"

export const CountContext = React.createContext({})
const initialState = {
    count:0
}

function reducer(state, action){
    switch(action.type){
        case "INCREMENT":
            return{
                count:state.count+1
            }
        case "DECREMENT":
            return{
                count:state.count-1
            }
        case "DIVIDE":
            return{
                count:state.count/2
            }
        case "MULTIPLY":
            return{
                count:state.count*3
            }
            case "RESET":
                return{
                    count:0
                }
            default:
                return state
        }
    }
function CountContextWrapper({children}){
    const [state, dispatch] = useReducer(reducer, initialState)
    return(
        <CountContext.Provider value={{ state, dispatch}}>
            {children}
        </CountContext.Provider>
    )
}

export default CountContextWrapper
```

### Counter.js
* The child we rendered will become Counter according to App.js
* Bring context
*  bring state, and dispatch using useContext. We can extract count from state
* for onClick function we just use `{()=>dispatch({type:"SOMETHING"})}`

```
import React,  {useContext} from 'react'
import { CountContext } from '../context/CountContext'
function Counter() {

    const {
        state:{count}, 
        dispatch} = useContext(CountContext)
    return (
        <div>
            <h1>Count: {count}</h1>
            <button onClick = {()=>dispatch({type:"INCREMENT"})}>+</button>
            <button onClick = {()=>dispatch({type:"DECREMENT"})}>-</button>
            <button onClick = {()=>dispatch({type:"DIVIDE"})}>/2</button>
            <button onClick = {()=>dispatch({type:"MULTIPLY"})}>*3</button>
            <button onClick = {()=>dispatch({type:"RESET"})}>Reset</button>
        </div>
    )
}

export default Counter
```
### Spinner
To show the spinner when loading the page
* App.js
use `React.Suspense fallback={<Spinner />}`
```
function App() {
  return (
    <React.Suspense fallback={<Spinner />}>
    <Router>
      <MainRouter />
    </Router>
    </React.Suspense>
  )
}
```
* MainRouter.js

We need to use React.lazy instead of actual import component

Lazy loading only imports the on component at the time that we need to use,that way we don't have to load all the components every time. 

###### Because we use Navbar everywhere, we don't need to fdo lazy loading for navbar.

```
const Home = React.lazy(()=>import ("./components/Home/Home"))
const Auth = React.lazy(()=>import ('./components/Auth/Auth'))
const NotFound = React.lazy(()=> import ('./components/NotFound/NotFound'))
```

### Toggle Signup and Login
We need to check the path using isLoginRoute and assign Login or signup to the button using buttonTitle and isLoginRoute variable
```
function Auth(props) {
    const classes = useStyles()
    let isLoginRoute = props.match.path==="/login"
    let buttonTitle = isLoginRoute ?"Login":"Sign up"
    return (
        <Grid container spacing spacing={0} justifyContent="center">
            <form className={classes.root}>
                <Grid item m={6}>
                <TextField fullWidth label="Email" name="email" />
                </Grid>
                {
                    !isLoginRoute && (
                        <Grid item m={6}>
                            <TextField fullWidth label="Username" name="username" />
                        </Grid>
                    )
                }
                <Grid item m={6}>
                <TextField fullWidth label="Password" name="password" />
                </Grid>
                <Grid style={{textAlign:"center"}}>
                    <Button type="submit" variant="contained" color="primary"
                    style={{marginTop:10}}>{buttonTitle}</Button>
                </Grid>
            </form>
        </Grid>
    )
}
```

# hooks
Hooks are functions that we use in multiple places.

We can define hooks using general parameteres that we return in the end as an array and then define these parameters in other files so functions can be dynamic.

Example that checks input for login and registration:
```
import {useState} from "react"
import {isAlpha, isAlphanumeric, isEmail, isStrongPassword} from "validator"

function useChangeInputConfig(inputType){
    const [value, setValue] = useState("")
    const [isError, setIsError] = useState(false)
    const [errorMessage, setErrorMessage] = useState("")
    const [isDisabled, setIsDisabled] = useState(true)

    function onChange(e){
        let value = e.target.value
        setValue(value)
        checkInput(value)
    }

    function clearInput(){
        setValue("")
    }

    function checkInput(value){
        if(value.length===0){
            setIsError(true)
            setErrorMessage(`${inputType} is required`)
            setIsDisabled(true)
        } else {
            setIsError(false)
            setErrorMessage("")
            setIsDisabled(false)
        }

        if(inputType==="First name" || inputType==="Last name"){
            if(!isAlpha(value)){
                setIsError(true)
                setErrorMessage(`${inputType} can only contain letters`)
            }
        }
        if(inputType==="Username"){
            if(!isAlphanumeric(value)){
                setIsError(true)
                setErrorMessage(`${inputType} can only contain letters and numbers`)
            }
        }

        if(inputType==="Email"){
            if(!isEmail(value)){
                setIsError(true)
                setErrorMessage(`Please type email format`)
            }
        }

        if(inputType==="Password"){
            if(!isStrongPassword(value)){
                setIsError(true)
                setErrorMessage(`Password must include 1 lowercase, 1 uppercase, 1 special character, 1 number, and a length of 8`)
            }
        }
    }
    return [value, onChange, isError, setIsError, errorMessage, setErrorMessage, isDisabled, clearInput]
}

export default useChangeInputConfig 
```

and then bring this hooks to Auth.js
```
import useChangeInputConfig from '../hooks/useInput'
function Auth(props) {
   const [email, handleEmailChange, isEmailError, ,emailErrorMessage, ,isEmailDisabled, clearEmailInput] = useChangeInputConfig("Email")
    const [emailUsername, handleEmailUsernameChange, isEmailUsernameError, ,emailUsernameErrorMessage, ,isEmailUsernameDisabled, clearEmailUsernameInput] = useChangeInputConfig("Email/Username")
    const [password, handlePasswordChange, isPasswordError, ,passwordErrorMessage, ,isPasswordDisabled, clearPasswordInput] = useChangeInputConfig("Password")
    const [passwordLogin, handlePasswordLoginChange, isPasswordLoginError, ,passwordLoginErrorMessage, ,isPasswordLoginDisabled, clearPasswordLoginInput] = useChangeInputConfig("Password ")
    const [username, handleUsernameChange, isUsernameError, ,usernameErrorMessage, ,isUsernameDisabled, clearUsernameInput] = useChangeInputConfig("Username")
    const [firstName, handleFirstNameChange, isFirstNameError, ,firstNameErrorMessage, ,isFirstNameDisabled, clearFirstNameInput] = useChangeInputConfig("First name")
    const [lastName, handleLastNameChange, isLastNameError, ,lastNameErrorMessage, ,isLastNameDisabled, clearLastNameInput] = useChangeInputConfig("Last name")
    const [confirmPassword, handleConfirmPasswordChange, isConfirmPasswordError, setIsConfirmPasswordError, confirmPasswordErrorMessage, setConfirmPasswordErrorMessage,isConfirmPasswordDisabled, clearConfirmPasswordInput] = useChangeInputConfig("Confirm password")
}
```

Another hooks that checks if cookie exists and retFurns functions as an object
```
import React, {useContext} from 'react'
import Cookie from "js-cookie"
import jwtDecode from "jwt-decode"
import { AuthContext } from '../../context/AuthContext'



function CheckAuthCookie() {
    const {dispatch} = useContext(AuthContext)

    function checkIfCookieExists(){
        const cookie = Cookie.get("jwt-cookie")
        if(cookie){
            return true
    } else{
        return false
    }
}


    function logUserIn(){
        let checkFCookieExists = checkIfCookieExists()
        
        if(checkCookieExists){
            const cookie = Cookie.get("jwt-cookie")
            let jwtDecodedToken = jwtDecode(cookie)
            dispatch({
                type:"LOGIN",
                user:{
                    username:jwtDecodedToken.username,
                    email:jwtDecodedToken.email,
                }
            })
        }
    }

    return {
        checkIfCookieExists,
        logUserIn
    }
}

export default CheckAuthCookie
```
We bring checkIfCookieExists function to Auth.js
```
const {checkIfCookieExists} = checkAuthCookie()
```

# useEffect
useEffect works as componentDidMount ot componentDidUpdate. It runs the code inside if something is triggered, we put triggers inside array brackets.
```
useEffect(() => {
       handleUserInfo()
    }, [])
```

# useReducer
useReducer works as useState,
we define cases and use callbacks to call dispatch types.
```
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```
# useRef
Ususally when we type in input the DOM gets updated right away, with useRef, DOM is not mutated.

We use useRef to sometimes hide information so it's not visible for users or hackers. 
```
import React, {useState, useEffect, useRef} from 'react'
function App() {
  const [value, setValue]  = useState("")
  const inputRef = useRef(null)
  
  useEffect (()=>{
    console.log(value)
  },[value])

function submit(){
  console.log(inputRef.current.value)
}

  return (
  <div className="App">
    <input type="text" onChange={(e)=>setValue(e.target.value)}/>
    <button>Submit</button>
    {value}
    <input type="text" ref={inputRef}/>
    <button onClick={submit}>Submit</button>
    {inputRef?.current?.value}
  </div>
  )
}

export default App
```
to grab the info from ref, we use inputRef.current.value in this example. Usually, use reference+.current+defined value

# Dynamic axios call
* Create hooks called useFetchAPI.js
```
import { useState, useEffect, useContext } from "react";
import axios from "axios"
import { AuthContext } from "../../context/AuthContext";
function useFetchAPI(url){
    const baseURL = process.env.NODE_ENV==="development"
    ? "http://localhost:3000/api"
    :"DEPLOYED LOCATION"
    
    const [isLoading, setIsLoading] = useState(false)
    const [response, setResponse] = useState(null)
    const [error, setError] = useState(null)
    const [options, setOptions] = useState({})
    const [isMessageOpen, setIsMessageOpen] = useState(false)
    const [successMessageValue, setSuccessMessage] = useState(null)

    const {dispatch} = useContext(AuthContext)

    function handleMessageOpen(){
        setIsMessageOpen(true)
    }

        function handleMessageClose(){
            setError(null)
            setResponse(null)
            setIsMessageOpen(false)
            setSuccessMessage(null)
        }

        function handleAPICallButtonSubmit(options={}){
            setOptions(options)
            setIsLoading(true)
        }

        async function handleAPIFetchCall(props){
            const requestOptionObj = {
                ...options,
                withCredentials:true,
                credentials:"include",
                ...{
                    headers:{
                        authorization:null
                    }
                }
            }
            try {
                let response = await axios(baseURL+url, requestOptionObj)
                if(response.data.message === "Success - user created"){
                    setIsLoading(false)
                    handleMessageOpen()
                    setResponse(response.data.message)
                    setSuccessMessage(response.data.message)
                } else if (response.data.message==="Success login"){
                    setIsLoading(false)
                    handleMessageOpen()
                    setResponse(response.data.message)
                    setSuccessMessage(response.data.message)

                    dispatch({
                        type:"LOGIN",
                        user:{
                            username:response.data.user.username
                        }
                    })
                }

            } catch (e) {
                console.log(e)
                setError(e.response.data.message)
                setIsLoading(false)
                handleMessageOpen()
            }
        }

        useEffect(()=>{
            if(!isLoading){
                return
            }
            handleAPIFetchCall()
        }, [isLoading, url, options, baseURL])

        return[
            {isLoading, response, error, setError, setResponse},
            handleAPICallButtonSubmit,
            isMessageOpen,
            handleMessageClose, 
            handleMessageOpen,
            successMessageValue
        ]
}

export default useFetchAPI
```
in Auth.js 
```
 async function handleOnSubmit(e){
        e.preventDefault()
        const user = isLoginRoute ? {emailUsername, passwordLogin}:{firstName, lastName, username, email, password}

        handleAPICallButtonSubmit({
            method:"post",
            data:{
                ...user
            }
        })
    }
```



