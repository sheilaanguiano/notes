# Node
-----

Author: Sheila Anguiano

-----
1. [Node.js](#node)
2. [npm Basics](#npm)
3. [Express Basics](#express)
4. [Asynchronous Code in Express](#async-express)
5. [SQL ORMs with Node.js](#sql-orm-with-node)
5. [Sequelize ORM with Express.js](#sequelize-express)
6. [REST APIs with Express](#api-express)
7. [Data Relationshipts with SQL and Sequelize](#sequelize-data-relationships)
8. [REST API Validation with Express](#rest-api-validation-with-express)
9. [Sequelize Model Validation](#sequelize-model-validation)


## Node.js <a name="node"></a>
### Introduction to Node.js
#### What is Node.js
A **runtime environment** is where code is executed. Runtime environments like Node provide access to features of the JavaScript language like data types, objects and functions, plus they have a built in engine that compiles code, translating your code into something that computers can use and understand. We often run JS code in a web browser. Browsers like Chrome are common examples of a run time environment, also called **front-end runtimes**.

Node is used for backend or server-side JavaScript. Dynamic web applications can be though of as restaurants. While web applications have a browser client for users to interpret and interact with, restaurants have a menu for guests to understand their offerings and make orders. Servers, and I mean restaurant servers, tja the guest order, pass it to the kitchen, and return with the food. We can think of a server in this example as an application programming interface, or a way for programs to communicate.
The kitchen in this example, is the back end of the applications. They take the request from a client and return the requested resources or food. Backend JavaScript is often used to manage data or interact with other applications. Node can be used to make front end applications dynamic, and it can be used on its own. Before Node developers had to use other languages like Python to manage data, authenticate users, and deliver personalized experiences.

All JavaScript runtime environments use the standard built in objects that are part of the JavaScript programming language, these are called **native objects** and are often referred as global objects. Different runtime environments have unique objects that allow javascript code to execute in that specific environment, these are called **host objects** and they're supplied to JavaScript by the environment., for example the browser offers the window object for accessing the DOM. Node.js for example provides a different set of host objects like *protocols* for requesting data, reading files.

-   **Native Objects**: Objects provided by the JS programming language, like string, array, date, math, etc. You can use these in any environment
- **Host Objects**: Objects provided by the environment. In the case of the browser, it’s like Window, document, history, XMLHttpRequest and many more.

Node is based on Google Chrome's V8 open source JavaScript engine and it comes equipped with its own tools. The V8 engines is what compiles JavaScript and handles memory. A main benefit of Node is its non blocking asynchronous execution of JavaScript code. Because of Node's non blocking capabilities, Node apps can easily scale or be built to serve more people.
- Netflix uses node to stream videos to millions of users
- Paypal and Capital one speed up their transactions when they went from Java to Node
- LinkeIn is built on node

[Netflix case study](https://openjsf.org/blog/2020/09/24/from-streaming-to-studio-the-evolution-of-node-js-at-netflix/)
[Case Study Node.js & NASA](https://openjsf.org/wp-content/uploads/sites/84/2020/02/Case_Study-Node.js-NASA.pdf)
[A Brief Explanation of the JavaScript Engine and Runtime](https://dev.to/sanderdebr/a-brief-explanation-of-the-javascript-engine-and-runtime-2idg)

#### Hello World
You can use the REPL (an interactive programming environment) to read, evaluate, prit out feedback and loop over this process. Node can function as a REPL with a single command in the terminal. You can exit with ctrl + D once or ctrl + C twice**
```
node
```
We can also crea a script file, name it app.js an create our first node program
```javascript
console.log("Hello World");
```
Now, we can run it from the terminal typing `node app.js`

### Building a Command Line Application
#### Planning our Project
Project: In our command line application we'll search for user information from Treehouse profiles and print out the requested information to the console.
- We should be able to enter a user name when we execute the program for example: `node project.js janedoe` and should be able to return the number of points and badges a user has

Threehosue has a REST API endpoint to a student profile information https://teamtreehouse.com/profiles/sheilaanguiano.json which is easier to understand with Chrome's extension JSONview

Steps:
- Connect to api
- Get data from api
- Format the data
- Print the data

#### Requesting Data with http
In javaScrit we can handle events using callback functions. There are 2 types of events that occur:
- User events : triggered by user input
- System events: triggerded by machine
	- Data events
	- Completion events
	- Error events

When we make request in Node, different types of system events occur through the cycle of the request, these include: 
- data events (when data is received)
- completion events (when a request is finished)
- error events

To connect to Treehouse's API we need to read the documentation on the `https` module, so we go to node.js > Documentation > API > https > GET method

In order to use a module like `https` we need to indicate that our code requires it. The `require` function in JavaScript allos to include modules that exist in separate files

Node comes with a `console.dir` method that is similar to `console.log`. When `console.dir` is given an object as an argument, it displays that object's properties in a list
```javascript
const https = require("https");
function getProfile(){
    const request = https.get(
        'https://teamtreehouse.com/profiles/sheilaanguiano.json',
        (response) => {
            console.dir(response.statusCode); //Returns 200
        });
}
//We call our function
getProfile();
```

Run the program on the console my writing
```bash
node namefile.js
```

#### Getting the Response Body
We need more than just status code to complete our goal, to get more information from the body of the response. Looking at the Node docs, the response object as a data event that gets emitted when a piece of data like student data from an API comes in. We can add a handler for the data event and give it a `consele.dir` statement to print out the response.

In Node whe handle events using the `on` method. We pass the ON method two arguments, an event ot watch for and a callback function to run when that event occurs, similar to `addEventListener`. In this case the event to watch is the data event.

The data event occurs when data is received by our program. Passing around large amounts od data is best done with certain type od data. **Buffers**. All data types like strings are useful for humans, machines use binary data. Large amounts of dinary data are called **streams* and can be stored using buffers
```javascript
//...
function getProfile(){
    const request = https.get(
        'https://teamtreehouse.com/profiles/sheilaanguiano.json',
        (response) => {
			let body = '';
            response.on('data', data =>{
                console.dir(data); //
				//Concatenate the string and tranform it to a string
				body += data.toString(); 
            })
			response.on('end', ()=>{
				//this will print our body
				console.dir(body);
			})
        });
}
//..
``` 
Beecause the data comes in piece by piece, we can define a variable to store the response and concatenate data to it until the stream is complete. Inside this event handler, intead of prinitng out the reponse. let's add the data and transform it to a String.

Along with the data event, there's also an `end event` that's emitted when there is no more data to be consumed from the stream. This tells when all the data has been sent, and we can handle this event just like other events in our callback

Since we'll get a long string, we'll use the `JSON.parse()` method to convert this into an object and it's much more readable.

#### The Process Object
So far or getProfile function is inflexible, it only searches for the username hardcoded into the URL, so will allow this function to take the username as an argument.
```javascript
const https = require("https");


//Function to print message
function printMessage(username, badgeCount, points) {
    const message = `${username} has ${badgeCount} total badge(s) and ${points} points in JavaScript`;
    console.log(message);
}


function getProfile(username){
    const request = https.get(
        `https://teamtreehouse.com/profiles/${username}.json`,
        (response) => {
			let body = '';
            response.on('data', data =>{
				//Concatenate the string and tranform it to a string
				body += data.toString(); 
            })
			response.on('end', ()=>{
				//this will print our body string
                let profile = JSON.parse(body);
                printMessage(username, profile.badges.length, profile.points.JavaScript);
			})
        });
}
//We call our function
getProfile('sheilaanguiano');
```
In the browser, we have a global window object that stores information about a given window. Node has its own global object, it's called the **process**. The process contains information about the location of Node on your computer, as well as the file being executed and any arguments we enter at execution.

One importan property is **argv**, which give us the node binary file, our app.js and it normally contains an array of arguments we enter into the command line

In our program, we can access *argv* and store arguments entered
```javascript
const https = require("https");


//Function to print message
function printMessage(username, badgeCount, points) {
    const message = `${username} has ${badgeCount} total badge(s) and ${points} points in JavaScript`;
    console.log(message);
}


function getProfile(username){
    const request = https.get(
        `https://teamtreehouse.com/profiles/${username}.json`,
        (response) => {
			let body = '';
            response.on('data', data =>{
				//Concatenate the string and tranform it to a string
				body += data.toString(); 
            })
			response.on('end', ()=>{
				//this will print our body string
                let profile = JSON.parse(body);
                printMessage(username, profile.badges.length, profile.points.JavaScript);
			})
        });
}
//We call our function
console.dir(process);
const users = process.argv.slice(2);
users.forEach(getProfile);
```
Now we can type to studen names and get information
```bash
 node app.js sheilaanguiano csalgado
```
[JSON Documentation on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)
[process.argv](https://nodejs.org/api/process.html#processargv)

### Handling Errors in Node
#### The error event in Node
With the error object we can get feedback from errors occur and this help us correct them, there are different types of errors:
- Standard JS errors
- System Errors
- User-specified errors
- Assertion
We're able to dund out more about a given error, including its type by examining its properties
- error.stack - error location
- error.code - kind of error
- error.message - string description

The `try-catch` block is an error handle technique used to execute a block of code and throw and erro message if something goes wrong that works mostly for *synchronous code*

```javascript
function getProfile(username){
	const request = https.get(
		//we remove a dot from the adress to cause a error to test or request.on(error)
		`https://teamtreehousecom/profiles/${username}.json`,
		(response) => {
			let body = '';
			response.on('data', data =>{
				//Concatenate the string and tranform it to a string
				body += data.toString(); 
			})
			response.on('end', ()=>{
				//this will print our body string
				let profile = JSON.parse(body);
				printMessage(username, profile.badges.length, profile.points.JavaScript);
			})
		});
		request.on('error', error =>{
			console.error('The request address was not found');
		})

}
```
Now sometimes, your program won't even get to make an asynchronous call, and in this case is a good idea to add a try-catch block
```jaavscript
function getProfile(username){
    try{ 
        const request = https.get(
			//By removing the protocal `https` our program won't even get to make an asynchrounous call
            `://teamtreehouse.com/profiles/${username}.json`,
            (response) => {
                let body = '';
                response.on('data', data =>{
                    //Concatenate the string and tranform it to a string
                    body += data.toString(); 
                })
                response.on('end', ()=>{
                    //this will print our body string
                    let profile = JSON.parse(body);
                    printMessage(username, profile.badges.length, profile.points.JavaScript);
                })
            });
            request.on('error', error =>{
                console.error('The request address was not found');
            })
    } catch (error) {
        console.log(error);
    }

}
```
#### Capture Synchronous Errors with Try Catch
When we look for a profile that doesn't exist, the message 'Not Found' is returned, so we'll run our code dealing with parsing in a try-catch block
```javascript
response.on('end', ()=> {
	try{
		//this will print our body string
		let profile = JSON.parse(body);
		printMessage(username, profile.badges.length, profile.points.JavaScript);
	} catch(error){
		console.error(error.message);
	}
})
```
[try..catch Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)

#### Handle Status Code Errors
Finally, we're just going to add a small function to make our code DRY
```javascript
function printError(error) { 
    printError(error);
}
```

### Building a Dictionary App




## npm Basics <a name="npm"></a>
### Introduction to npm
#### What's NPM
When building JavaScript applications, one might often find oneself wondering, thats someone might have already done this or don't know how to do something.
The good news is that developers and companies release open source software all the time to help with common problems. Also, as applications grow, this will include multiple open source libraries and it could start getting tricky maintaining each version.

**npm** is a package manager for JavaScript and it's most commonly used for installing packages for Node.js. Instead or arbitrarily searching the internet for other people's code, manually downloading, and including them, the package manager lets you install, update and uninstall packages through a standardized way. It helps you keep track of the current versions of each package.
- npm packages for Node.js projects are called **modules**
- You can check if you have Node using `node -v`

#### How to Find and Choose Packages
One of the main reasons you'd want to install a package is to use pre existing code. There is no need to reinvent the wheel or do a lot of difficult time consuming programming when you can install a module and utilize in in your node application. 

1. First look into the npm website and determine what package to use based on:
	 * Popularity on npm  – the number of downloads
	*  Release Date  – the more recent the better
	* Number of Releases  – the more frequent the better
	* Passing Tests  - if there's tests passing
	* Number of Open Issues  – the less the better
	* Popularity on GitHub  – The more Stars, Forks and Watches the better
	* Number of Contributors on GitHub  – more eyes on the code the better

2. Search on the internet to corroborate

#### Semantinc Versioning
You may beging to noce that NPM packages are often referred by a combination of the name of the package followed by a version number

A lot of software uses this style of versioning where you have 3 numbers separated by dots, this is known as **semantic versioning** or **SemVer** for short. The first number is a major release, meaning if you move from version one to two, the code that you use from version one will NOT work with version two. The second digit is a minor release meaning if you move from version 1.1 to 1.2, the code that you work should still work. It should be backwardly compatible, but that's not 100% guaranteed. Minor releases add new functionality in, hopefully, in a non-destructive way. The third release is for patch releases. These are bug fixes that don't necessarily break backward compatibility. It's always good idea to make sure that you have the latest patch version, since newer patches fix bugs that might affect your project.

**Semantic Versioning**

-   `MAJOR.MINOR.PATCH`
-   `^`  before a version number means install up to the latest  `MINOR`  release.
    -   e.g.  `^1.1`  can install  `1.3`  if available but not  `2.0`
-   `~`  before a version number means install up to the latest  `PATCH`  release.
    -   e.g.  `~2.0.1`  can install  `2.0.9`  if available but not  `2.1.0`

[semver](https://semver.org/)

### Managing Packages with NPM
#### Installing Packages
Npm packages can be installed locally or globally:
**Locally**
Npm create a special folder called node modules, in here you'll find all the modules that you install with npm.
All the packages dependencies are put in the top level node modules folder. You rarely might need to do something in these folders. You may want to look at some of the source code if something is really plaguing your project, but mostly you'll leave this alone and let npm handle the contents of this folder.
**Globally**
For example, the *http-server package* makes it easy to start a simple web server on your computer, so it makes sense to install it so it's always available, we call these kinds f always available packages, **global packages** 
*To install a package globally* we use `npm <package name> -g`

Get help for a command
`npm <command> -h`
e.g. `npm install -h`

Installing a global package
npm install <package_name> -g
e.g. npm install http-server -g

Installing a local package
npm install <package_name>
e.g. npm install express
Documentation
http-server
Fixing npm Permission Issues

#### Managing Dependencies
npm provides files that allow us to both track and manage packages in a project. It also provides us with a way of avoiding uploading the node modules folder
`npm init` creates a file named `package.json`
`npm init -y` creates a page with default information

The `package.json` file will contain other important information including a list of all the packages you've installed. The modules installed are listed as a **dependancy** a dependancy is a packafe that a project requires to run.

Now `package.json` doesn't always get updated when packages are updated. To track the exact version of the packages you install, npm uses the `package-lock.son`. Is similar to package.json but includes more information including the exact version number of installed packages

#### Igone Files and Directories with gitignore
Use a .gitignore file to instruct your version control system to ignore or avoid tracking specified files or directories when you make a commit.

In your project, create a file named .gitignore in the root directory. Inside this file, you list the name of files and directories that you don’t want to include in your GitHub repo. In this case, it’s node_modules/.

All project files should be present when you commit and push your latest code to GitHub except for the node_modules directory and files.

Remember: the .gitignore file must be created and list any files or folders you want to ignore before pushing to GitHub.

In the following video, you’ll practice updating, uninstalling, and executing packages.

[gitignore](https://git-scm.com/docs/gitignore)
[Github Ignoring Files](https://docs.github.com/en/get-started/getting-started-with-git/ignoring-files)
[Collection of gitignore templates](https://github.com/github/gitignore)

#### Updating, Uninstalling and Executing Packages
Over time, newer version of packages are release, or we may find new, better packages to replace existing packages in a project
- npm unistall
- npm update
- npm outdated : tells you which packages are out dated without updating them

- npx is a package runner and is used to simplify your workflow by executing packages in one command
[npm Doc](https://docs.npmjs.com/)
[Updating packages from registry](https://docs.npmjs.com/updating-packages-downloaded-from-the-registry)
[npx](https://nodejs.dev/learn/the-npx-nodejs-package-runner)
[npm uninstall](https://docs.npmjs.com/uninstalling-packages-and-dependencies)



## Express Basics <a name="express"></a>
### Getting Started with Express
Build your first Express App from scratch
#### What is Express?
>Express is a routing and middleware web framework that has minimal functionality of its own: An Express application is essentially a series of middleware function calls.

Express is a web application framework for Node.js that allows you to rapidly build dynamic web applications. 

Web applications have a lot of commonalities between them. Commonalities in software are called **patterns** (solutions for common problems in software). A web framework provides lots of solutions for making web applications. The solutions can differ from framework to framework, but the most common include

- templating for dynamic layouts
- URL mapping / routing
- User Input Processing

**Benefits of Web Framework**
- Write applications faster
- Focus on business logic
- Understand other codebases
- Collaborate with other developers

The principles you'll learn here are transferable to other languages and frameworks such as
- Express/Node.js
- Flask/Python
- Spark/Java
- Sinatra/Ruby

What you'll learn:
- Installing and Setting Up Express
- Pug Templating
- Routing in Express
- Serving Static Assets
- Middleware

#### Installing Express
1. We start by creating a new folder with the terminal
`mkdir express-flashcards`
2. Initilize a Node application with the default options using `-y` flag
`npm init -y`
3. We can now install express with the save flaq to save it into our package.json file
`npm install express@4.15.2 --save`
4. Open a new file with the name of *app.js* from the terminal using:
* atom						`atom app.js`
* visual studio code	`code app.js`

#### Creating a Server in Express
Express sets up its server, a server is a program that runs on a remote computer. Its job is to wait for HTTP request from clients. Request is a technical term for whats happening when you type in a URL into a browser. Your browser is making a request to a server at the URL address you type in. When a browser, or client, makes  an HTTP request to the server, the service brings into action putting together a response. The development process requires you, the developer, to test and build a web application. It's usually much easier to run an application server on your local machine. This means you'll have both a server and a client on your computer. You'll use a browser to test the server in one window for example, and then see the server respond in another. Later, when you're ready to make your application available to the public. You'll need to deploy it to a remote server, where other people can visit it.

To create an Express application we can just call express `express();` the express function returns an express application. Let's assign the express application to a new variable called `app` . This apps is the central part of our application, we'll extend it throughout this course by adding routes, middleware and other settings.
`const app = express();`
 The first thing we'r going to do is setup the development server using the *listen method*, which can receive one parameter, which is the port number.
 running this and going to *[http://localhost:3000/](http://localhost:3000/)* will show an error message from express
```javascript
const express = require('express');

const app = express();

app.listenerCount(3000);
```



[Deploy a Node Application to Heroku](https://teamtreehouse.com/library/deploy-a-node-application-to-heroku)


####  Creating a Route with Express
Express handles request through routes that we can setup in the app. It's called a route, because it's the path a user takes to access data on a server. From an application perspective a route also called an end point, is a command to run a specific function, which in turn send a response back to the client

When you type an URL into your browser and hit return, the browser sends what's called a GET REQUEST to the server. This means, you're asking to view or get a web page. GET is known as an HTTP verb, because it represents what the client wants the server to do. In this case of GET the client is simply asking the server to return something, but what? This is where the URL comes in, which is more like a noun or *resource* as its called. The URL tells the server what to get for the client. GET requesta re the most common request made by browsers, and a server response to a GET request by sending information off in a web page. But a browser also can send information to the server.

To create a route, we'll use the get method on the app object. The get method is used to handle the get request to a certain URL. In this example, we're going to create a route for the root route for our app.

We use the '/' (slash) as the first parameter, or sometimes called the location parameter, the second parameter of the get method is an anonymous callback function, that takes to parameters:

```JavaScript
app.get('/',(request, response => {
}));
```
 This callback will run, when the client request this route. The `response.send()` method sends a string to the client.

We'll install *nodemon* package as a global dependency to avoid starting and stoping the server manually.

`npm install -g nodemon`

To use it, make sure that package.json has the property main and it points to the right entry file for tour app.
 
[HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
[HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

#### Adding Multiple Routes to the App
Express Applications will have several (and often many) routes. Let's set another route up and see how it allows us to serve different content, depending on which route a user visits.

We had made our app with one route so far, but it doesn't actually serve HTML yet. You can drop HTML right into the send method as a string. We can also add a `console.log()` That will popup every time nodemon re-starts the server.

```JavaScript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
	res.send('<h1>Hello World via Express</h1>');
});
app.listen(3000, () => {
	console.log('The application is running on localhost:3000!')
});
```

Now we would add another route:
```JavaScript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
	res.send('<h1>Hello World via Express</h1>');
});

app.get('/hello', (req, res) => {
	res.send('<h1>Hello JavaScript Developer!</h1>');
});

app.listen(3000, () => {
	console.log('The application is running on localhost:3000!')
});
```

You could make a pretty nice site with what you know so far, serving HTML from different routes with the `re.send()` method. But there's better way to server HTML from Express in templates.

[res.send](https://expressjs.com/en/4x/api.html#res.send)

### Using Templates with Express
#### What is Template Rendering
The majority of the HTML you surf from an app, will never change. If a user is viewing a gallery for example, the photos change but the rest of the page stays the same. Most web application framework handle this situations using what are called **templates**. 

A template provides the basic HTML for your app and serves it to the users. Templates also lets you vary the output to provide customized responses. 

When a request comes in toa given route,  the server decides how to handle the request. A server can send back response containing HTML derived from a template. Templates are a special type of file that have their own syntax and language. They live on the server, and act as some kind of form letter for your HTML. So its like an HTML page with holes or blanks in it. You can fill in those blanks with custom content by adding variables to the template. The result is a full HTML page send to the client. The process is called **rendering the template** . Because rendering a template results in what the viewer sees on their screens, templates are often called **views**. Most templating languages resemble HTML, the most popular templating languages in JavaScript are:
 
- Handlebars
- EJS
- Pug (formerly Jade)

You can use basically any templating engine with Express, but Pug is by far the most popular. Pug syntax has a slightly steeper learning curve than some of the other templating languages

[Pug.js](https://pugjs.org/api/getting-started.html)
[Handelbars.js](http://handlebarsjs.com/)

#### What is Pug?
Pug is one of the most popular templating engines for Node. It is also commonly used with Express.
Pug is a language that compiles or translates to HTML

**PUG**
```Pug
html (lang="eng")
	head
	body
	div.wrapper
		p#mainContent Hi!
		h1 love Treehouse!
		ul
			li Red
			li Yellow
```
**HTML**
```html
<html lang="eng">
<head></head>>
	<body>
	<div class="wrapper>
	<p id="mainContent">Hi!</p>
	<h1>I love Treehouse!</h1>
```

#### Using Pug in your Express App
To use Pug in our app, we'll follow these steps:
1. Download Pug with npm
2. Update code in app to use Pug
3. Create templates
4. Render templates with response.render()

`npm install pug --save`
Now we can use pug in our App using the set method:
`app.set('view engine', 'pug')`. The `app.set()` method defines different settings in express. By default, Express will look in a folder called **views** in the root of your project, if you want to name your folder something else, or nest it into another folder you need to define the view setting point and point Express to the right place.

We'll create our pug file and change our response from `res.send()` to `res.render()` in our index route.

```JavaScript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
	res.render('index');
});

app.get('/hello', (req, res) => {
	res.send('<h1>Hello JavaScript Developer!</h1>');
});

app.listen(3000, () => {
	console.log('The application is running on localhost:3000!')
});
```

[Using template engines with Express](https://expressjs.com/en/guide/using-template-engines.html)

#### Express's Response.render() Method
The real power of templates comes into play when you use variables to inject customized content, such as a user's name, a list of shopping cart items, or text of a blog post.

In this section, we'll create a flash card template by using variables, which are injected into the template as it's rendered.

**Static Text**
```Pug
h1 static Text
```
**Variable**
```Pug
h1= variable
```
The `response.render()` takes two optional parameters. The second parameter is called *locals*. Placing an object here will define the locals for the view. Locals is the name for the variables we want the view to have access to when it's being rendered. The properties of the object we pass in as the second argument will define the locals in the template.

```Pug
app.get('/cards', (req, res) => {
	res.render('card', { prompt: "Who is buried in Grant's tomb?"});
});
```

Another way to do it, by adding properties to the res.locals. The name of the property will define the local variable name:
```Pug
app.get('/cards', (req, res) => {
	res.locals.prompt = "Who is buried in Grant's tomb?"
	res.render('card');
});
```
If we wanted to use some other static text plus a variable inside we can use interpolations, similar to the way we use template literals in JavaScript. To interpolate we do the following:

```Pug
//Pug
h1 My name is #{name}
```
This will render de following in HTML
```html
<!-- html -->
<h1> My name is Andrew</h1>
```
Note that interpolation doesn't work for attributes though. You'll need to concatenate strings with any values you want to put intro attributes, or use template literals.

```Pug
//Pug
h1(title='My name is ' + name) #{name}
```
```html
<!-- html -->
<h1 title="My name is Andrew">Andrew</h1>
```
[res.render()](https://expressjs.com/en/4x/api.html#res.render)

#### Using Logic in Pug
Pug templates can contain logic you can use to make them more versatile. You can show or hide parts of the page conditionally, or iterate over arrays of data to express tables or lists more concisely.

**Using conditionals in Pug**
```Pug
<!--card.pug -->
	section#content
		h2= prompt
		if hint
			p
				i Hint: #{hint}
			else
				p (There is no hint.) 
				
	footer
		p An app to help you study
```

```JavaScript
//app.js
app.get('/cards', (req, res) => {
	res.render('card', { prompt: "Who is buried in Grant's tomb?"});
});
```
**Looping through and array of values**
```JavaScript
//app.js

const colors = [
 'red', 
 'orange', 
 'yellow', 
 'green', 
 'blue', 
 'purple' 
 ];
```
```Pug
<!--card.pug -->
	section#content
		ul
			each color in colors
				li= color
```
Challege: Create a sandbox template to create a two column table with a first name and a last name, and render a table.

#### Breaking your Project's Templates into Partials
Let's make your templating more modular and reusable.

If we include the same elements in all of our HTML templates, we'll run into a problem when w need to update our HTML, like changing the content of the footer across all o the pages on our site. 

Pug lets you include a template into another template. The child, or the included template is extended, or nested within the layout.

Let's create a template called `layout.pug`.  The layout should include everything that our templates have in common, like header and footer. Finally we add the block content keywords:
```Pug
<!--layout.pug -->
doctype html
html(lang="en")
	head
		title Flash Cards
	body
		header
			h1 Flash Cards
		
		block content
				
		footer
			p An app to help you study
```
This `block content` let's Pug know that any template extending the layout can inject its HTML there. Now, we can slice and dice the content that's duplicated in the index.pug file and tell it to extend or inherit from the layout file

```Pug
<!--index.pug -->
extends layout

block content
	section#content
		h2 Welcome, student!
```

In a small and simple page like this, it might not seem important to break the header and footer, but for real world applications, headers and footers can get really complicated, or the application can often grow. Having it broken up ahead of time can help keep it organized and make maintaining it easier.

[Template Inheritance](https://pugjs.org/language/inheritance.html)
[Includes](https://pugjs.org/language/includes.html)

### Deeper into Routing with Express
Routing is how users can access different parts of your application. Let's examine how to offer users more from our app.
#### POST Request.
When a client sends data to the server it's called a POST request. We'll do this by creating a Pug Form, that request a name and creating an alternative route that will handle the submission of the form.

[app.post.method](https://expressjs.com/en/4x/api.html#app.post.method)

#### The Request Object.
We've been using the response object to return a response to the client. But we haven't been using the request object yet, apart from declaring it. There are quite a few properties that you can access on the request. The one we're most interested in is the body property, this is where our form response will end up. Notice though that by default it is undefined, and is populated when you use body-parsing middleware such as body-parser and multer.

Middleware is basically some code that fits in the middle of a request or a response. Middleware does something to the incoming data and hands the result of to the rest of your application.

```JavaScript
app.post('/hello', (req, res) => {
	console.dir(req);
	res.render('hello');
});
```
Looking at the request object in the console, we can see that it includes a lot of information, which can give us an idea of the amount of work express does to simplify our job as developers. Most of the time, we don't need many of these properties. When we examine the property body, we get *undefined* just as the documents promised
```JavaScript
app.post('/hello', (req, res) => {
	console.dir(req.body);
	res.render('hello');
});
```
Let's install the middleware, called by the docs. It's called body parser and it will process the incoming form submission data into a format that's easier for our program to read.
`npm install body-parser --save` and we can require it in our app.js file.

Body-parser contains several parses, the different way the clients send data. HTML forms normally encode the data they send the way URLs do.So we'll need to use the Url encode parser. We'll pass in an object, turning off the parser's extended option

`app.use(bodyParser.urlencoded({ extended: false}));`

Now when we submit the form, the  name, has a username property and is no longer undefined. Our app is able to understand the information it's getting from our form.

[Sending Form Data](https://developer.mozilla.org/en-US/docs/Learn/Forms/Sending_and_retrieving_form_data)
[Web Forms](https://developer.mozilla.org/en-US/docs/Learn/Forms)
[Express Request Object](https://expressjs.com/en/4x/api.html#req)
[body-parser](https://github.com/expressjs/body-parser)

What is body-parser doing? In case you're curious, here's a little code that reads the body of an incoming request and logs it to the console. This is just a flavor of how using body-parser is making your life easier!
```JavaScript
 let bodyString = '' 
 req.on('data', chunk => bodyString += chunk.toString()); 
 req.on('end', () => { 
	 console.log(bodyString); 
 });
```
#### The Response Object
While the request object allows the applications to look at the request that the client has made, the response object offers ways to shape the response back to the client.

In this section, we'll use the name received from the form and send it back in a message that greets the user.

We have been using several response methods like `res.send()` and `res.render()`.  There's also another method that's commonly used to send back data to the client JSON. Sometimes clients don't want all the presentation of HTML and CSS, they just want the data, that's what JSON is good for. Serving data is the primary use for Express for many developers. Now, when we submit the username we'll get a json file.

```JavaScript
app.post('/hello', (req, res) => {
	res.json(req.body);
});
```
Now, we want to serve the same template when the user post the form. remember Pug  you add some basic programming logic to your templates. So you can use the same template to show different HTML content.

You MIGHT notice that if you refreshing the browser after submitting the form, you'll see the welcome message. That's because the name has been already entered earlier. This happens because the browser refreshes the last post request from the form, including the date for the request. To make sure that you're getting a get request, hit enter on the URL. 

With this, we've completed the request response cycle using the data we collected from the user. The basics you've learned are like a scaffold you can build our from here.

[Response](https://expressjs.com/en/4x/api.html#res)
[https://teamtreehouse.com/library/build-a-rest-api-with-express](https://teamtreehouse.com/library/build-a-rest-api-with-express)


#### Statelessness, Setting and Reading Cookies
HTTP is a stateless protocol. Learn more about what that means, and how to save state.

In the next sections, we'll add another page to our app. We'll add a welcome page, that our form will move to after a user submits the name.

HTTP is a stateless protocol or in other words the server doesn't track the relationship between one request and another. Each transaction with a server is independent and unrelated from the server's perspective. A server retains no memory of the client after sending a response, now matter how recently or often they interact. Tracking state often takes a lot of architecture and memory, so by avoiding it altogether, the web has been able to grow to a massive scale, but sometimes applications need to remember previous interactions, in other words we need to save the state of a request and remember it later. 

One of the earliest and still most common methods for saving states on the web is a **cookie**. A cookie is a piece of data that the service stores on the client, for example in your web browser. After receiving the cookie information from the server, when the client makes another request of the server, the client sends the cookie information too. It will even send other cookies that have been previously set perhaps by other web pages on that site. This way, the client can remind the server of any information it should hand back in its response.

Cookies are stored in your browser by domain, this means that one domain cannot access another domain's cookies. Let's see how to use cookies to remember or app's current user. We can use the cookie method on Express's response object.

The `res.cookie` method takes a name and a value. You can also pass in an *options object* as a third parameter.

In our app.js file let's set the cookie when the user submits the form to the post route.  The `res.cookie('username', req.body.username` will send a cookie to the browser after we submit the form

We can check this using DevTools and looking at the  Application Panel > Cookies

Now the browser will automatically send this cookie with every request it makes. At this point though, our app isn't reading the cookie it's getting back

```JavaScript
app.post('/hello', (req, res) => {
	res.cookie('username', req.body.username);
	res.render('hello', {name: req.body.username});
});
```
Let's read the cookie and share the user's name when the user makes a get request to this route. To read the cookie from the request, we need the cookie's property on the request object. Looking at the documentation, we'll need another piece of middleware that reads the cookies, called **cookie-parser**. After we connect the cookie-parses middleware, we can read cookies much the same way as we did with the request body parameter earlier to read the form data.
We download the *cookie-parser* module with npm, add to our app using `app.use` just like the *body-parser* and add it or app.

Now down in the get hello route, we can provide it to the template as a variable. Now our app is reading the cookie correctly.
```JavaScript
app.get('/hello', (req, res) => {
	res.render('hello', {name: req.cookies.username});
});

app.post('/hello', (req, res) => {
	res.cookie('username', req.body.username);	
	res.render('hello', {name: req.body.username});
});
```
Cookies are just one way to save states and it's one of the simple ways that are available to developers. Databases and other different browser storage called **session storage** are examples of other commonly used ways to save state.

*It's best not to store sensitive data in COOKIES because they're plain text, so don't save passwords or credit card information*

[https://github.com/expressjs/cookie-parser](https://github.com/expressjs/cookie-parser)
[https://expressjs.com/en/4x/api.html#res.cookie](https://expressjs.com/en/4x/api.html#res.cookie)
[https://expressjs.com/en/4x/api.html#req.cookies](https://expressjs.com/en/4x/api.html#req.cookies)
[https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)

#### Redirects
Learn about HTTP redirects and how they can be used in a web application.

When you submit  a form like this in a website, that website generally redirects to another page, like a welcome page.  Redirecting after a for submission prevents duplicate submissions if a user refreshes the page. Likewise, when you try and visit a protected page on a website, it will often redirect you to a login screen. Then when you've login, it will redirect you back to the page you wanted to visit.

In HTTP, redirecting represents a series of specific events. When a client request a resource from a server that is protected or perhaps is being moved, the server will often respond with the response call that redirect which contains a URL. The client receiving this response will usually make a second instant request to the new URL, but this happens you quickly that you'll not even notice its happening. For this reason redirects are often used to make the same work page available from several URLs. Apps will often use redirects to manage authentication by sending users to a log in page before they are permitted to view certain pages or redirect users to those pages when they log in successfully.

In our project, after users enter their name, let's redirect them to our app's main welcome page. We just call the redirect method instead of the render method to complete the response, and then the browser will get the URL that we enter as an argument
```JavaScript
app.post('/hello', (req, res) => {
	res.cookie('username', req.body.username);
	res.redirect('/');
});
```
Now, in the hello template, we can remove the conditional altogether as no one will ever land on this page unless the app doesn't know their name. It can simply display the form to collect the information before the user is redirected to the welcome page. Now, we can update index.pug  and replace the generic greeting with our personalized one.
```Pug
extends layout.pug

block content
	section#content
		h2 Welcome, #{name}!
```
Now I need to make sure that the template has access to the cookies name value, so we take the cookie and make it a variable.
```JavaScript
app.get('/', (req, res) => {
	const name = req.cookies.username;
	res.render('index', {name: name});
});
```
We can also use the ES6 object shorthand ro remove the usage of the color and the extra name
```JavaScript
app.get('/', (req, res) => {
	const name = req.cookies.username;
	res.render('index', {name});
});
```

[Redirections in HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Redirections)
[Objects shorthand](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer)
[Destructuring_assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

### Middleware
Two essential components of Express are routing and middleware. Now that we have a handle on routing, let's see what middleware is all about!
#### What is Express Middleware?
Middleware so integral in express that just about everything you write in Express is Middleware. Consider when someone asks you a question, you hear the question, think about it for a moment, and then answer the question. If we relate this to the request response cycle, the middle step, the thinking is analogous to what Middleware does.

An Express application receives requests and sends responses, you can sort of think of Express' request response cycle like a conveyor belt. The request comes in at the beginning and the responses leaves at the end. All along the conveyor belt Middleware acts upon the requests, packaging the response to send back t the end user. There can be as many pieces of Middleware as you want to have before sending a response.

The basic structure of Middleware code is very simple. It's a function with three parameters. Inside the function, Middleware can read, modify the request and response objects. For example, the cookie parser modified the response object, placing the cookie's contents onto it.
`(req, res, next) => {};`
Next is a function that must be called, when the work is done. This triggers the Middleware function after the current one to execute. To run Middleware in response to requests, pass it into app.use. This will run the Middleware function for every request. 
`app.use((req, res, next) => {});`
To only run it for a specific route, pass the router argument in before the Middleware function
`app.use('/users', (req, res, next) => {});`
You can also limit the Middleware to only use get requests.
`app.get('/users', (req, res, next) => {});`


[Using Middleware](https://expressjs.com/en/guide/using-middleware.html)
[Writing middleware for use in Express apps](https://expressjs.com/en/guide/writing-middleware.html)

#### Middleware Sequence and Routing
You'll often pass Middleware in an anonymous function into the app.use method. We write this in the middle of our applications and this middleware runs every time a request comes into the app.

```JavaScript
app.use((req, res, next)=> {
	console.log('One');
	next();
})
```
It's important to know that you can depend on the sequence. Earlier middleware functions, runs before the later ones. You can pass several functions into the same app.use method code and they will rin in the order they're passed in.
```JavaScript
app.use((req, res, next)=> {
	console.log('One');
	next();
},
	(req, res, next)=> {
		console.log('One and a half');
		next();
});

app.use((req, res, next)=> {
	console.log('Two');
	next();
});

//Terminal will display
//[nodemon] starting `node app.js`
//The application is running on localhost:3000!
//One
//One and a half
//Two
```
You can call the app.use as many times as you'd like, passing in a function to each call. You can also pass in as many functions as you want into a single `app.use` call. Express will always run functions in the order they appear. Let's trigger the middleware base on the URL or route that a user visits. We can do ties by placing the URL as the first argument to the app.use method 

You can also pass information between functions. Let's use the request object to pass the data from the first middleware function to the next middleware one.
```JavaScript
app.use((req, res, next)=> {
	req.message = "This message made it!";
	next();
});

app.use((req, res, next)=> {
	console.log(req.message);
	next();
});

//Terminal will display
//[nodemon] starting `node app.js`
//The application is running on localhost:3000!
//This message made it!
```
We just modified the request object for the first time. That's what gives middleware its power. Allowing us to gather and compute data and send it back to the client.

#### The 'next' function and a closer look at middleware
The `next` function is an important part of middleware. Learn why and when to use it.

**Next()** signals the end of middleware functions
```JavaScript
app.use((req, res, next)=> {
	console.log("Hello");
});

app.use((req, res, next)=> {
	console.log("World");
	next();
});

//Terminal will display
//[nodemon] starting `node app.js`
//The application is running on localhost:3000!
//Hello
```
In this case, the app hangs when middleware is not closed out with a next(). The app is waiting indefinitely for next to be called. Express relies on the next function to know when to move forward, but `next()` isn't the only way to end a middleware function. Looking at our route handlers, we're sending a response to client, which is middleware too, but we're ending the function by sending a response to the client. We've talked about several ways to send a response, you can use send, render or json methods for example. The main thing to remember is that you can end middleware by either calling next or sending a response.

Understanding Express' execution flow is really helpful in building and troubleshooting apps.
An outer function that returns an inner function is a common occurrence in JavaScript, and it's also known as a closure

[Understanding closures in JavaScript](https://teamtreehouse.com/library/understanding-closures-in-javascript)
[Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)

#### Handling Errors in an Express App
Handling errors is an important (and easy to overlook) topic any program should address. Learn how to handle them in Express. Errors are an important tool for your users as they learn how to interact with your app. They offer information about the limits of how your app can be used. Errors also guide developers in fixing bugs in an application.

In Express, you can use the `next()` function to signal an error in your app. By passing an objects as a parameter to next, Express knows there is an error to handle. Express will then immediately terminate and handle the error.

```JavaScript
app.use((req, resp, next)  =>  {
	console.log("Hello");
	const  err  =  new  Error("Oh noes!");
	next(err);
});
//Browser:
// Error: Oh noes!  
//   at /Users/shei/Data/projects/treehouse/express-flashcards/app.js:14:17
//
```
The error is thrown at the top, the next line tells us that the error was thrown at line 14, the second number is the column, or how many spaces from the first position on line 14. Pinpointing where an error is in an app can really speed up the process of fixing bugs. All of the lines after this indicate deeper layers on the Express framework.

This output is coming from Express' built in error handler

#### Error Handling Middleware
Build a custom error middleware function into the app.

Now that we know hot to tell Express when an error has occurred in our App, let's tell Express how to handle it. While Express middleware has three parameters, error middleware has four

**Middleware**
`(req, res, next) => {}`
**Error Middleware**
`(err, req, res, next) => {}`

So far, Express invokes its own native handler inside its code base. We can overwrite that behavior by putting it in our own error handler, which will serve a custom template back to the client. The template is where we can format the error to be more readable than the text we currently see
```JavaScript
app.use((err, req, res, next)  =>  {
	res.locals.error  =  err;
	res.render('error');
});
```
The error object has properties that hold the data about the error, so we can pass that into the second argument to the render function. This will give the template the access to the error data.
Now, we create the error.pug file

In our error handler, we can set the status of the response using the status method on the response object. Normally, if there's an error in the code on the server it will throw a status 500, this is a general error, that just means the server couldn't fulfill the request because something was unexpected.

[Error Handling in Express](https://expressjs.com/en/guide/error-handling.html)
[HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

#### Handling 404 Errors
Now that we have a custom error handler, let's add a middleware function to handle 404 errors, and send them to the error handler.

When an app gets a request, it will go form one `app.use()` call to the next looking for a match. If it gets to the end and there are no errors, express' native handler will send a 404 back to the client with some plain text. If we catch the request before it get's to the end of the line, we can send users a better page.

For our app,  we want to access the request at the end of our app and before the error handler.
```JavaScript
// ------------ ERROR HANDLERs --------
app.use((req, res, next)  =>  {
	const  err  =  new  Error('Not Found');
	err.status  =  404;
	next(err);
});

app.use((err, req, res, next)  =>  {
	res.locals.error  =  err;
	res.status(err.status);
	res.render('error');
});
```
[Error MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)

### Parameters, Query Strings, and Modularizing Routes
Now that we have a solid grasp on the basics, let's apply that knowledge to developing the Flashcard application.
#### Modular Routes
Make the app more maintainable by moving the routes into their own file.
Knowing how to modularize your app will keep your code well organized and easy to maintain over time. This is how most professionals structure their code. So you'll often see routes in a separate file in Production Express apps.

We'll create a new folder named *routes* and inside a file named *index.js*  remember when requiring a file in Node.js we can just refer to the folder name and if there's a file named *index* that will be loaded by default. Relying on this convention will make make code a little simpler and easier to read.

A router is kind of like a mini app in Express, you can add middleware and routes to it, and declare them with the router instead of the app. Note that apps will often have more than one routes file. You can add a path as a first argument to mount those routes to. In fact, we'll create another routes file now we'll use for the flash card routes.

card.js file
```JavaScript
const express =  require('express');
const router = express.Router();  

router.get('/',  (req, res)  =>  {
	res.render('card',  { prompt:  "Who is buried in Grant's tomb?"});
});

module.exports  = router;
```
index.js file
```JavaScript
const express =  require('express');
const router = express.Router();

router.get('/',  (req, res)  =>  {
	const  name  =  req.cookies.username;
	if(name){
		res.render('index',  {name});
		}  else  {
		res.redirect('/hello');
		}
});
// --------- HELLO ROUTE -----------
router.get('/hello',  (req, res)  =>  {
	const  name  =  req.cookies.username;
	if(name){
		res.redirect('/');
	}  else  {
		res.render('hello');
	}
});

router.post('/hello',  (req, res)  =>  {
	res.cookie('username',  req.body.username);
	res.redirect('/hello');
});

// --------- GOODBYE ROUTE -----------
router.post('/goodbye',  (req, res)  =>  {
	res.clearCookie('username');
	res.redirect('/hello');
});
module.exports  = router;
```
And finally this is how the app.js file will look like
```JavaScript
const express =  require('express');
const bodyParser=  require('body-parser');
const cookieParser=  require('cookie-parser')  

const app =  express();

app.use(bodyParser.urlencoded({  extended:  false}));
app.use(cookieParser());

app.set('view engine',  'pug');

const mainRoutes =  require('./routes');
const cardRoutes =  require('./routes/cards');

app.use(mainRoutes);
app.use('/cards', cardRoutes);

// ------------ ERROR HANDLERs --------

app.use((req, res, next)  =>  {
	const  err  =  new  Error('Not Found');
	err.status  =  404;
	next(err);
});

app.use((err, req, res, next)  =>  {
	res.locals.error  =  err;
	res.status(err.status);
	res.render('error');
});

// --------- SANDBOX -----------
app.get('/sandbox',  (req, res)  =>  {
	res.render('sandbox');
});

app.listen(3000,  ()  =>  {
	console.log('The application is running on localhost:3000!')
});
```
Now that we've got a well-organized directory structure, we're in a great position to start building out the app.Let's starts by developing the card template and bringing some data into our app.

#### Using data Data and Route Parameters
Using and maintaining data is normally handled by connecting the app to a database. For the sake of this course, we will add our card flash data in what's sometimes called a **flat data file**
The file contains a JSON objects with the data property. The data property refers to an object with one property called cards. Cards is an array of objets that contain each flashcard's data.

Let's pull this data into our card's route file. We'll stre the JSON data property into a constant named *data*.

```JavaScript
//card.js file
const express =  require('express');
const router = express.Router();

const  { data }  =  require('../data/flashcardData.json');
// Which can also be written const data = requiere('../data/flashcardData.json').data
const  { cards }  = data;
// const cards = data.cards`

  
router.get('/',  (req, res)  =>  {
res.render('card',  { prompt:  "Who is buried in Grant's tomb?"});
});
 
module.exports  = router;
```
We'll separate the cards from the data because the cards will be the main data we want to use. Also notice the ES6 Syntax: `const  { data }  =  require('../data/flashcardData.json');` which is the same as saying `cards = data.cards`

You can also include JSON directly in Node. It reads the text file and then parses the text and converts it int JSON object so you don't have to call json.parse

Now, we'll connect the template to the first question just to be sure its working:
```JavaScript
router.get('/',  (req, res)  =>  {
	res.render('card',  {
		prompt:  cards[0].question,
		hint:  cards[0].hint
	});
});
```
But, how will we pull up any card that we want in the browser? We'll use a route parameter for that. A **route parameter** is a variable that a user can put right into the URL to point to a particular resource. For our current URL, we want to place a number at the end indicating which card to display, and we can do this with a *:* to tell express it can treat that portion of the URL a a variable or route parameter named id( or any other name). The value for the route parameter from the URL will be stored in the request object params property.
```JavaAcript
router.get('/:id',  (req, res)  =>  {
	res.render('card',  {
		prompt:  cards[req.params.id].question,
		hint:  cards[req.params.id].hint
	});
});
```

Using URL parameters is a powerful way to access different resources. In the next step, e'll take a look at another way to use a URL to pull specific data from a resource called the *query string*

#### Card Template
We can see different questions now by specifying an ID in the URL:

/cards/4
/cards/5

But how can we view answers to those questions. We could add another URL parameter after the id that would look for a string, for example question or answer:

 cards/4/question
 cards/4/answer

Or we can use a query string. A *query string* goes at the end of a URL and it starts with a question marks. After the questions mark you can pass the server a keyvlue pair separated by an equal sign

cards/4/question?key=value&key2=value2

Checking for a query string is very similar to checking for a route parameter or a cookie
```JavaScript
router.get('/:id',  (req, res)  =>  {
	const  {  side  }  =  req.query;
	const  {  id  }  =  req.params;
	const  text  =  cards[id][side];
	const  {  hint  }  =  cards[id];
	const  templateData  =  {  text,  hint  };
	
	res.render('card',  templateData);

});
```
Now how do we make sure that the **hint** only appears on the question side

```JavaScript
router.get('/:id',  (req, res)  =>  {
	const  {  side  }  =  req.query;
	const  {  id  }  =  req.params;
	const  text  =  cards[id][side];
	const  {  hint  }  =  cards[id];
	
	const  templateData  =  {  text  };

	if( side  ===  'question'){
		templateData.hint  =  hint;
	}
	
	res.render('card',  templateData);
});
```

#### Adding Links
Challenge: Make it easier for the user to flip the card from one side to the other. Keep in mind that you can use JS template literals in Pug templates

**card.pug**
```JavaScript
extends layout.pug

block content
	section#content
		h2= text
			if hint
				p
					i Hint: #{hint}
					
		a(href=`/cards/${id}?side=${sideToShow}`)= sideToShowDisplay
```
**cards.js**
```JavaScript
router.get('/:id',  (req, res)  =>  {
	const  {  side  }  =  req.query;
	const  {  id  }  =  req.params;
	const  text  =  cards[id][side];
	const  {  hint  }  =  cards[id];
	const  templateData  =  {  id,  text  };

	if( side  ===  'question'){
		templateData.hint  =  hint;
		templateData.sideToShow  =  'answer';
		templateData.sideToShowDisplay=  'Answer';
	}  else  if (side  ===  'answer'){
		templateData.sideToShow  =  'question';
	templateData.sideToShowDisplay  =  'Question';
	}
	res.render('card',  templateData);
});
```

#### Randomize Cards
Randomizing the cards the user sees will help them learn the material better. In this video you'll be challenged to implement that feature!

Solution: Create a new route in the cards.js file
```JavaScript
router.get('/',  (req, res)  =>  {
	const  numCards  =  cards.length;
	const  flashcardId  =  Math.floor(Math.random() *  numCards);
	res.redirect(`/cards/${flashcardId}?side=question`);
});
```
Remember, because we're inside a router that is mounted in the cards route in the app.js file, we don't need to start any of our URLs with *cards*

#### Linking Around the Application
Here, we'll re-arrange several parts of our app:
- Move the welcome information an log in information to the layout.pug
- Connect hello to the random cards route
- Connect the cookie information to the cards information
- Make the "Hello, !" messages when the cookies are cleared

[JS Unit Testing Class](https://teamtreehouse.com/library/javascript-unit-testing)

### Serving Static Files in Express
Web pages need CSS and other assets to look good. Express can supply those with what's called a static server. Let's set one up; it's easy!
#### What are Static Assets?
At this point our application generates **dynamic** content using templates, variables and cookies, but sometimes a server doesn't need to do anything more complex than sending the files directly to the user.
Static files like images, and stylesheets don't need to be processed by the application. They jus t need to be delivered to the browser.

When a browser makes a get request to the index route of our application, it receives HTML, but as we've seen there is no file called index.html in any of the folders in our application. When the app receives the request it has to assemble and render the HTML from templates and data. This allows the application to server customize web pages to different clients. As you know, browsers use HTML, CSS and JS to display a web page. The CSS and client-side JavaScript files will be the same no matter who requests them, or what the application state is. Express doesn't need to build them, like it does the HTML in our application. For this reason, there files are called static assets.

We've writing our Express application in JavaScript. This is different from the client-side JavaScript our web page might use. Our Express app and our browser app are two different environments and play different roles in what the end-user sees. In Fact the static JavaScipt files don't even look like JavaScript to Express. These files are just handed straight over to the browser without even being attempted to be interpreted by Express. The browser know what to do with these files and turns them into all kinds of magical user interaction.

For these assets, Express uses something called a Static Server. Because these files are prebuilt and won't change on the server, passing them through all of Express's routing and template rendering would be a waste of time. The Static Server just send them to the client saving EXpress time and effort.

#### Adding Static Assets to the App
Our job in this stage is to tie the HTML into our App logic. The work we'll do is mostly in the templates. Let's first take a look in how to serve static assets in Express using the static methods:
`express.static(root, [options]`

We'll add the statics assets and name the folder *public*. The name **Public** is commonly used for the folder containing static assets. I've got a couple of CSS files that I want to serve, so we go to app.js we add the static middleware
`app.use(express.static('public'));` with this we'll make the public folder content available from the root of the app.
  
Note: If you think folders or file names, in the public folder will conflict with other routes in your app, you can route the static server to specific location:
`app.use('/static', express.static('public'));`

Next, we need to link the HTML app produces to this file. Since we want to make all the styles available to the pages in our application, the best place to link the style sheets will be in the template layout, since is the one that holds the head element.
```Pug
head
	title Flash Cards
	link(rel='stylesheet', href='/static/stylesheets/style.css')
```
When express renders this template it send the HTML to the browser, the browser sees the link tag and make a request the static/stylesheets/style.css Because we set up a static server, the public folder's content is at /static. Any path in the folder will automatically be available to static

#### Merging the Design Files

##### Server-Side vs Client-Side

This course has been about writing JavaScript to assemble and serve webpages to browsers. But, as you know, you can run JavaScript in the browser too, to add interactivity to the pages an Express app serves. These two environments, the server-side and the client-side, are worth knowing about and understanding. You have probably written client-side JavaScript already, in previous treehouse courses, for example. That's the JavaScript that is loaded into HTML and manipulates the DOM, among other things.

[HTML to Jade Converter](http://html2jade.org/)
[HTML to Jade Converter](http://html2jade.aaron-powell.com/)





## Asynchronous Code in Express <a name="async-express"></a>
### Asynchronous Code in Express
Asynchronous programming in JavaScript has evolved rapidly in recent years. Due to this change, handling asynchronous tasks in Express, such as getting information from a database, can be achieved in a variety of ways. 
#### Asynchronous Programming with Express
Writing asynchronous code in Express often involves action upon data whenever you happen to receive it. For example, say you want to retrieve a list of movies from a database and render that movie data into a template. Because of the asynchronous nature of working with the database, there's no guarantee I'll get that movie information back before Express renders the template. thus the result would be an empty HTML template sent to the browser.

Traditionally, Express uses call backs to deal with asynchronous tasks. You'll call a function that retrieves a list of movies, and that function would take a call back tat runs when and only when the list of movies has returned, or an error ha occurred.  This is fine if the actions you are performing are simple. It's when you have several asynchronous task to perform before you send something to the browser that things can get messy. For example, if you needed to retrieve a certain subset of movies from a database then the ratings for those movies, then a list of the actors who starred in those movies. You'd end yo with a call back, nested in a call back, nested in a call back. This is a reason that approaches to asynchronous programming in JavaScript have evolved and changed a lot over the years. Making the async landscape sometimes difficult and overwhelming to navigate. Recently, new approaches have become available natively in JavaScript : Promises and async/await. These approaches are used by popular libraries like Mongoose and Sequelize that help you interact with databases.
You should understand:
* Understand building  server side application with Express
* Asynch programming
	* Callbacks
	* Promises

[https://www.freecodecamp.org/news/javascript-from-callbacks-to-async-await-1cc090ddad99/](https://www.freecodecamp.org/news/javascript-from-callbacks-to-async-await-1cc090ddad99/)
[https://javascript.info/async](https://javascript.info/async)

#### Using Callbacks
We'll be using a very simple Express application that retrieves information about users from a JSON file and renders it into a main index template, or if there's an error, and error template

In our example the function `getUsers` retrieves data from the data.json file for us. The function takes a callback. Once getUser have retrieve the data from the file, it returns a call to this callback function and passes to that callback the data it's retrieved from the file. We're storing the data in a variable called `users` which we're then passing to the callback. So we're saying data.users, once you're done retrieving the users from the file, call whatever function we pass to you, and pass the list of users into that function. This means that when we call to getUsers function we can pass in an anonymous function that will access to our user data and we'll be able to work with that user data inside that function. 

Async methods in node that accepts callbacks follow a patter of passing an error as the first argument when an error occurs. So'll pass an anonymous function to our getUsers function nested in our Express home route. If there's an error we'll render the error template, else if everything goes as expected we'll render the index page, and we'll give the template a title. Last, we'll need to provide the template our user data.

This example might not look so bad, but it can become pretty messy following this approach. Say we want to find a user's followers perhaps for a social media app, as you can see we're performing two actions: (getting the User and then his or her followers) and things are getting pretty messy with nested in functions and repetitive error handling (The pyramid of doom / callback hell)

```JavaScript
app.get('/:id', (req, res) => { 
	getUser(req.params.id, (err, user)=>{ 
		if(err){ 
			res.render('error', {error: err}); 
		} else { 
			getFollowers(user, (err, followers) =>{ 
				if(err){ 
					res.render('error', {error: err}); 
				} else { res.render('profile', {title: "Profile Page", user: user, followers: followers});
				 } 
				}); 
			} 
		});
	});
```
#### Refactor Using Promises
Promises allow us to clearly outline the order in which things need to done, by chaining functions together in the order we wish them to execute, rather than nesting them one inside of another.
```JavaScript
app.get('/:id', (req, res) => { 
	getUser(req.params.id)
	 .then((user)=>{ 
		 return getFollowers(user);
	 }) 
	.then((user, followers)=>{ 
		res.render('profile', {title: "Profile Page", users: user, followers: followers});
	}) 
	.catch((err) => { 
		res.render('error', {error: err});
	}); 
});
```

#### Refactor Using Async / Await
Async await is basically a way to work with promises using a generally less verbose syntax, that looks a lot like using synchronous functions. Using async and await, we can write express routes that are even more straight forward to follow. Another benefit of async away syntax is that it's easier to debug. When an error occurs in a massive chain of `.then()`s, it can be difficult to pinpoint exactly where the error occurred, with async await, it's much easier to tell on which line an error was throw, because the syntax structure of your code is a lot like using standard synchronous functions.

The beauty of async await is that I can now perform as many asynchronous actions as I want, and I can write them just like synchronous functions.



```JavaScript
app.get('/:id', async (req, res) => {
 try { 
	 const user = await getUser(req.params.id); 						   			   			
	const followers = await getFollowers(user);    
	res.render('profile', {title: "Profile Page", user: user, followers: followers}); 
	} catch(err){ 
	res.render('error', {error: err}); 
	} 
});
```
Now because of the necessity of the try catch block for error handling, we might get a little verbose again. The good news is, that there are ways to abstract the try catch block, either manually or by using a library

#### Reduce Error Handling Code when using Async/Await
If our application were one that had many routes, using a try-catch block each time would make our code pretty long and unwieldy after a while. To get around this, we can use a piece of middleware to wrap each or our routes automatically in a try-catch block, that way we won't have to explicitly write it over and over again. Let's write that middleware at the top of our file naming it `asyncHandler` and it'll take a callback
```javascript
function asyncHandler(callback){
  return async(req, res, next)=>{
	try{
		await callback(req, res, next);
		} catch(err){
			res.render('error', {error:err});
		}	
	}
}

app.get('/', asyncHandler(async (req,res)=>{
	const users = await getUsers();
	res.render('index', {title:"Users", users: users.users});
	}
));

```




## Using SQL ORMs with Node.js <a name="sql-orm-with-node"></a>
### Getting Started with Sequelize
Most node applications need to talk to a database at some point to query data or create and update specific data.

#### What is ORM(Object-Relational Mapping)
ORM tools let you interact with a database using your language of choice. An ORM handles the movement of data between your application and the database. An ORM executes all the same SQL queries using your preferred language, while abstracting away some of the complexities of connecting with databases.

Another advantage is using writing your applications using one language (JS) instead of two (SQL and JS).

Sequelize is a popular and well maintained ORM library that provides built-in queries and key functionality to help you maintain and interact with databases including:
* Table creation
* CRUD operations
* Validations

For our database, we'll use SQLite a simple, easy to use relational database that doesn't require you to install or configure anything on your system in order to make use of it. This makes it an ideal database for learning projects.


[https://sequelize.org/](https://sequelize.org/)
[https://github.com/sequelize/cli](https://github.com/sequelize/cli)
**Note:**  
For production-ready applications, you'll want to rely upon a database server platform like [PostgreSQL](https://www.postgresql.org/), [Oracle](https://www.oracle.com/database/), [SQL Server](https://www.microsoft.com/en-us/sql-server/default.aspx), or one of the cloud-based solutions from Amazon, Microsoft, or Google.

#### Install and Configure Sequelize and SQLite
1. Create a new project 
2. run `npm init -y` to create the package.json file with defaults
3. Create `app.js`
4. Configure `package.json` (main and scripts)
5. Install sequelize
6. Install SQL Lite
7. Configure Sequelize and connect to the Database creating the movies.bd
8. Test the connection with a `try..catch` block

You’ve installed the Sequelize ORM, implemented a database with the SQLite database software, and opened a connection to a database! Next you'll learn to leverage the power of SQL and manage the data for your simple Node app using Sequelize.
[Distinctive Features Of SQLite](https://www.sqlite.org/different.html)
[IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)

### Define a Model
Sequelize is all about models. As you learned earlier, when using an ORM library like Sequelize, developers interact with a set of models to do database operations. Instead of interacting directly with the database, Sequelize acts as a mediator that oversees the movement of data from the database to the models and back.

A model in Sequelize represents a  _table_  in the database. A model also predefines how data should be stored, and determines whether or not a database entry is valid (for example, if the entry should be a number, string, etc.).
##### Define a Model
Models are often defined as JavaScript classes. Each model (or class) represents a thing that your application will be working with – all of the _nouns_. A model contains a collection of attributes (or class properties) that are used to describe each model instance. For example, a "Person" model might include "name" and "age" attributes to represent the name and age of a specific person.

1. **Define a  `Movie`  model.** In `app.js`, create a class named `Movie` that `extends` the `Sequelize.Model` base class:

```JavaScript
// Movie Model
class  Movie  extends  Sequelize.Model  {}
```
In JavaScript classes, the `extends` keyword is used to create a subclass, or a child of another class. In this case we're extending from `Sequelize.Model`, which is part of Sequelize's API for model definition.

2. **Initialize a model.** Call the static class `init()` method on the model name (`Movie`) to initialize and configure the model:
```JavaScript
const Sequelize = require('sequelize');   
const sequelize = new Sequelize({...});   
// Movie model 
class Movie extends Sequelize.Model {} 
Movie.init();

(async () => {
     ... 
})(); 
```    
`Movie.init()`  defines a new table in the database with the name 'Movies'. Sequelize will look for information in the  `Movies`  table.

An important distinction is that the model name is singular and the table name is plural. Sequelize uses a library called  [inflection](https://www.npmjs.com/package/inflection)  under the hood to automatically pluralize the table name (for example, from  `Movie`  to  `Movies`).

#### Set Model Attributes and Options

The  `init()`  method takes two arguments. The first argument is an object literal that defines the model's attributes -- each attribute is a  _column_  of the table. The second argument is an object literal that sets the model options.

Now that we have a 'Movies' table, let's create a column for movie titles.

1.  **Set the model attributes.**  Define a column named 'title' by passing  `init()`  an object with a  `title`  property. Each column must have a data type. The  `title`  should be a string data type, so set the value of  `title`  to  `Sequelize.STRING`:

```JavaScript  
const Sequelize = require('sequelize');   
const sequelize = new Sequelize({...});   
// Movie model 
class Movie extends Sequelize.Model {} 
Movie.init({
     title: Sequelize.STRING 
});   

(async () => {
... })(); 
``` 
Sequelize's data types allow attributes (or column names) to be assigned only certain types of data. For example,  `Sequelize.STRING`  indicates that the value of  `title`  should be a variable length string with a default length of 255 (for example, 'Spider-Man: Into the Spider-Verse').
    
2.  **Set the model options.**  You can set a number of options in your model definition; for example, a custom name for your model and a timestamp. The only  **required**  option is a  `sequelize`  property that defines the sequelize instance to attach to the model.
    
3.  Pass  `init()`  an object as a second argument. Inside the object, attach the Sequelize instance by setting the  `sequelize`  property to the variable  `sequelize`:

```JavaScript    
const Sequelize = require('sequelize');   
const sequelize = new Sequelize({...});
// Movie model 
class Movie extends Sequelize.Model {} 
Movie.init({
     title: Sequelize.STRING 
}, { sequelize }); // same as { sequelize: sequelize }   
(async () => {
     ... 
})(); 
``` 

**Note:**  Sequelize will throw an error if you don't provide a  `sequelize`  property.
    
This code initializes a model representing a 'Movies' table in the database, with one column: 'title'.

#### Synchronize Models with the Database
The final step to set up Sequelize is to synchronize your models with the database. Sequelize provides the  `sync()`  method, which automatically creates or updates your database tables (according to your model definition). In other words, we want to create the actual 'Movies' table. We’ve only defined the model in JavaScript. We need to sync those changes.

You can synchronize individual tables by calling  `.sync()`  on a table.

1.  Inside the  _async_  function,  `await`  a Promise returned by calling  `Movie.sync()`:
```JavaScript       
...   
// Movie model 
class Movie extends Sequelize.Model {} 
Movie.init({
     title: Sequelize.STRING, 
}, { sequelize });   
(async () => {
     // Sync 'Movies' table 
     await Movie.sync();   
     try {   
     } catch (error) { 
     console.error('Error connecting to the database: ', error); 
     } 
})(); 
```    
Now that you're successfully connecting to the database, feel free to comment out (or remove) the code inside the  `try`  block, which was used to test the connection.
    
As you create more models, you may want a way to sync all your models at once. Calling the  `sync()`  method on the  `sequelize`  instance lets you do just that, automatically create and update all the tables in the database.
    
2.  **Replace  `Movie.sync()`  with  `sequelize.sync()`:**
    
```JavaScript       
...   
// Movie model 
class Movie extends Sequelize.Model {} 
Movie.init({
     title: Sequelize.STRING, 
}, { sequelize });   
(async () => {
     // Sync 'Movies' table 
     await sequelize.sync();   
     try {   
     } catch (error) { 
     console.error('Error connecting to the database: ', error); 
     } 
})(); 
``` 
Calling  `sync()`  issues a  `CREATE TABLE IF NOT EXISTS`  statement, which will sync all models and create tables that do not exist in the database. In development (or testing), you may want to refresh your database tables each time you start your app. For this, the  `sync()`  method accepts an object with a  `force`  parameter that lets you control the database synchronization.
    
3.  **Force sync all models.**  Pass  `{ force: true }`  to the  `sync()`  method:
    
```JavaScript       
...   
// Movie model 
class Movie extends Sequelize.Model {} 
Movie.init({
     title: Sequelize.STRING, 
}, { sequelize });   
(async () => {
     // Sync 'Movies' table 
     await sequelize.sync({ force: true });   
     try {   
     } catch (error) { 
     console.error('Error connecting to the database: ', error); 
     } 
})(); 
``` 
    

Calling  `sync({ force: true })`  issues a  `DROP TABLE IF EXISTS`  statement, which completely deletes the table, before issuing the  `CREATE TABLE IF NOT EXISTS`  statement. In other words, it will drop a table that exists, each time you start your app, and recreate it from the model definition.

#### Create a Record

Finally, let's create one test record (or a  _row_  in the database table) that stores a movie title. To create a record, you use the  `Model.create()`  method.

1.  **Insert data into the  `Movies`  table.**  Inside the  `try`  block, initialize a  `movie`  variable to a new  `Movie`  instance with  `await Movie.create()`:
    
    class Movie extends Sequelize.Model {} Movie.init({ ... });   (async () => {
     await sequelize.sync({ force: true });   try { // Instance of the Movie class represents a database row const movie = await Movie.create();   } catch (error) { console.error('Error connecting to the database: ', error); } })(); 
    
    `Movie.create()`  builds a new model instance, which represents a database row, and automatically stores the instance's data. It returns a  `Promise`  object, which resolves or rejects based on the successful or failed interaction with your database.
    
    `create()`  requires an object with properties that map to the model attributes (the ones defined in  `Movie.init()`, for example). Our  `Movie`  model currently has one attribute,  `title`, so let's create a new row with a movie title.
    
2.  Pass  `Movie.create()`  an object with a  `title`  property. Set the value to your favorite movie title as a string:
    
```JavaScript       
...   
// Movie model 
class Movie extends Sequelize.Model {} 
Movie.init({
     title: Sequelize.STRING, 
}, { sequelize });   
(async () => {
     // Sync 'Movies' table 
     await sequelize.sync({ force: true });   
     try {
	   const movie = await Movie.create({
	     title: 'Silent Hill',
	  });   
     } catch (error) { 
     console.error('Error connecting to the database: ', error); 
     } 
})(); 
``` 

#### Test Your Record

We'll revisit creating records later in the course. For now, let's quickly log the  `movie`  variable (`Movie`  instance) to the console to see our newly created record.

1.  **Log the data returned by  `movie.toJSON()`:**
    
```JavaScript       
...   
// Movie model 
class Movie extends Sequelize.Model {} 
Movie.init({
     title: Sequelize.STRING, 
}, { sequelize });   
(async () => {
     // Sync 'Movies' table 
     await sequelize.sync({ force: true });   
     try {
	   const movie = await Movie.create({
	     title: 'Silent Hill',
	  });
	  console.log(movie.toJSON());   
     } catch (error) { 
     console.error('Error connecting to the database: ', error); 
     } 
})(); 
``` 
Calling  `movie.toJSON()`  converts the instance to JSON – in other words, it returns a JSON representation of the data.

If you log just the instance, you will notice that there is a lot of additional output. In order to hide and reduce the output to just the JSON data, use  `toJSON()`.
    
2.  In your Terminal, run the app and create the record with  `npm start`. You should see a similar JSON object in your console output:

``` 
{ id: 1, 
title: 'Toy Story', 
updatedAt: 2019-07-10T14:16:48.886Z, 
createdAt: 2019-07-10T14:16:48.886Z } 
``` 
Don't worry about all the statements displayed above the JSON for now. Those are the SQL statements that Sequelize generated and executed to store the record in the table.

Sequelize also added an  `id`  property and timestamps, with the  `createdAt`  and  `updatedAt`  properties. We'll review these in the next step, and test that the app and database are set up and working as expected.

[Model](https://sequelize.org/master/class/lib/model.js~Model.html)
[Model Definition](https://sequelize.org/master/manual/models-definition.html)
[Model Instances](https://sequelize.org/master/manual/model-instances.html)
[Sequelize Data Typesl](https://sequelize.org/master/manual/data-types.html)
[Model Basics](https://sequelize.org/master/manual/model-basics.html)

### Test the Database
After defining and initializing the  `Movie`  model in the previous step, you learned that models are both the objects that you interact with in your application and the tables created and managed in your database. And the ORM (Sequelize) acts as the  _translator_  between objects in your code and data stored in a relational database.

In this step, you will test that the 'movies' database was created with the expected table, columns and entries.

#### DB Browser Lite
Test that your database was configured correctly by following the steps below.

1.  **Launch the DB Browser for SQLite app on your computer.**
2.  **Click the "Open Database" button in the top-left corner.**  Or select File > "Open Database".
3.  **Select the 'movies' database file in your project folder (`movies.db`), and click "open".**
4.  **Click the "Browse Data" button near the top-left side of the app.**  This should display the 'Movies' table, which has a 'title' column with the entry created in the previous step.

#### Default Attributes
By default, Sequelize automatically adds the attributes  `createdAt`  and  `updatedAt`  to your model. That way you'll know when the database entry went into the database and when it was last updated. Your 'Movies' table should also display the columns 'createdAt' and 'updatedAt', each with a timestamp value.

Sequelize also adds an auto-incrementing  `id`  attribute to your model, which creates a unique ID for each entry (or row). The table should display an 'id' column. We've created just one entry, so the ID should be  `1`. The next entry you insert into the table will have an ID of  `2`, then  `3`, and so on -- that way all IDs are unique.

#### Sequelize Logging

At this point, you know that Sequelize handles the creation of tables and inserts entries for you, so you don’t have to write or deal with any raw SQL. When you run your app (with  `npm start`), you'll notice that Sequelize prints the SQL statements being executed to the console by default.

You can disable SQL logging by passing the  `logging`  parameter to the  `Sequelize()`  constructor and setting it to  `false`:

```JavaScript
const Sequelize = require('sequelize');   
const sequelize = new Sequelize({
 dialect: 'sqlite', 
 storage: 'movies.db', 
 logging: false // disable logging 
});   ... 
```
This will prevent Sequelize from outputting SQL to the console.

#### Wrap UP
Now that you've verified that your database was created with the expected table, and that you're able to insert data into the table, try adding a new record to the 'Movies' table. For example:

```JavaScript         
(async () => {
     // Sync 'Movies' table 
     await sequelize.sync({ force: true });   
     try {
	   const movie = await Movie.create({
	     title: 'Silent Hill'
	  });
	  console.log(movie.toJSON());
	  
	  //New entry
	  const movie2 = await Movie.create({
	     title: 'Old boy'
	  });
	  console.log(movie2.toJSON());

   
     } catch (error) { 
     console.error('Error connecting to the database: ', error); 
     } 
})(); 
``` 
**Note:** You can create a record in your project without declaring a variable. We declared `movie` and `movie2` only to view the JSON data in the console. You're still able to insert an entry by simply awaiting `Model.create()`. For example:

```JavaScript         
(async () => {
     // Sync 'Movies' table 
     await sequelize.sync({ force: true });   
     try {
	   await Movie.create({
	     title: 'Silent Hill'
	  });
		 await Movie.create({
	     title: 'Old boy'
	  });   
     } catch (error) { 
     console.error('Error connecting to the database: ', error); 
     } 
})(); 
```
You can also create multiple records using the `Promise.all()` method, which waits until all promises returned by the model `.create()` method are fulfilled:

### Improve the Project Layout
You started the project by writing all of your code in the `app.js` file. Now you're going to improve your project by moving all the database and model related code into their respective files and folders. This will help keep your Sequelize code organized and easier to maintain.

#### Database and Model Files
1.  In your main project folder, create a new folder named  `db`.
2.  Inside the  `db`  folder, create a folder named  `models`.
3.  In the  `models`  folder, create a new file named  `movie.js`. This file should  `require`  the  `'sequelize'`  module and export the initialized  `Movie`  model as shown below:
```
const Sequelize = require('sequelize');   
module.exports = (sequelize) => {
	 class Movie extends Sequelize.Model {} 
	 Movie.init({ 
	  title: Sequelize.STRING, 
	}, { sequelize });   
	return Movie; 
};
```
4. **Add an  `index.js`  file inside the  `db`  folder.** This file should contain the code to configure the `Sequelize` instance and `require` (or load) the `Movie` model defined in the `models/movie.js` file:
```JavaScript
const Sequelize = require('sequelize');   
const sequelize = new Sequelize({
 dialect: 'sqlite', 
 storage: 'movies.db', 
 logging: false 
 });   
 const db = {
 sequelize, 
 Sequelize, 
 models: {}, 
 };   
 db.models.Movie = require('./models/movie.js')(sequelize);   
 module.exports = db;
```
The file `exports` the `db` object, which holds the Sequelize and database configurations, as well as the models. Exposing the Sequelize package wherever you import models into your code means that you'll have all of Sequelize's methods and functionality to use.

5. **Update the  `app.js`  file.** The entry file imports the database and destructures the 'Movie' model imported from `db.models`. The `app.js` file should now contain only code related to syncing models, querying data and CRUD operations:
```JavaScript
const db = require('./db'); 
const { Movie } = db.models;   

(async () => {
 await db.sequelize.sync({ force: true });   
	 try { 
		 const movie = await Movie.create({ 
		 title: 'Toy Story' 
		 }); 
		 console.log(movie.toJSON());   
		 const movie2 = await Movie.create({ 
		 title: 'The Incredibles' 
		 }); 
		 console.log(movie2.toJSON());   
	  } catch (error) { 
		console.error('Error connecting to the database: ', error); 
	} 
})();
```
#### Test and Wrap Up

Check that everything still works as expected by running the app with  `npm start`. You should see the two JSON objects in the console containing the movie title entries.

Nice work so far! In this stage, you learned what an ORM (object-relational mapper) is, and the benefits of using an ORM library like Sequelize in a Node.js application. You installed and configured Sequelize with a SQLite database, even defined a model and added an entry into the database, all from your Node project.

In the next stage, you will use options to improve how you define a model, explore common Sequelize data types, add validations to a model, and more.

[Destructuring_assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

### Defining Models
Learn how to further define your model structures with data types, validations, default values, options, and more.
### Go Further with Models
A relational database like SQL (and database system like SQLite) consists of a table of rows and columns. In the previous stage, you learned that models in Sequelize represent a table in the database.

When setting up a model, you specify a set of instructions for Sequelize that define (or shape) how data should be stored. The model lets Sequelize create, retrieve, update or delete rows of data following those instructions. This is all done via plain JavaScript objects, for example:
```JavaScript
Movie.init({
 title: Sequelize.STRING,
  }, { sequelize });   
  ... 
 await Movie.create({
   title: 'Toy Story', 
 });
```
Models  _map_  JavaScript objects to relational database tables – thus the name "Object-Relational Mapper". In this step, you will learn how to further define the structure of your database table with data types, default values, constraints, and more.

#### Common Sequelize Data Types
Data types are used when defining a new model. For instance, in the previous stage, you set the  `title`  attribute of the  `Movie`  model to accept a string data type with  `Sequelize.STRING`. Sequelize supports  [other common data types](http://docs.sequelizejs.com/manual/data-types.html)  like integers, booleans, dates, and floats.

Let's add three new columns to the 'Movies' table to store a movie's runtime, release date, and whether or not it's available on  [VHS](https://en.wikipedia.org/wiki/VHS)  (because awesome VHS collections). Each new column will be a different data type.

1. **Open the file** `db/models/movie.js` Add the properties  `runtime`, `releaseDate` and `isAvailableOnVHS` to the Model attributes object,  and set each to an object:
```JavaScript
const Sequelize = require('sequelize');   
module.exports = (sequelize) => {
 class Movie extends Sequelize.Model {} 
 Movie.init({ 
 title: Sequelize.STRING,
 runtime: { }, 
 releaseDate: { }, 
 isAvailableOnVHS: { },
}, { sequelize });   

return Movie; };
```
Inside the object, we can specify configuration options for an attribute to further define how data should be stored. The `type` property, for example, sets a data type.

2. **Specify data types**. Set the `type` property of each attribute using Sequelize's supported data types as shown below (change the `title` attribute as well)
**Note:**  
The default length of  `Sequelize.STRING`  is 255 (or  `varchar(255)`), but you can specify a different length after the type. For example,  `Sequelize.STRING(500)`.

An important distinction is that the  `DATE`  data type accepts a date value provided in  `yyyy-mm-dd hh:mm:ss`  format, while  `DATEONLY`  accepts a date value in  `yyyy-mm-dd`  format (`DATE`  without time).

#### Specify a Primary Key that's Auto Incremented
Sequelize adds an  `id`  attribute to your model, which generates an 'id' column in your table that assigns each row a unique ID. The ID acts as a 'primary key', or a unique indexable reference for each entry.

Instead of the default generated  `id`  column, you can set a custom column name for primary keys in your table, using  `primaryKey: true`.

1.  **Add an  `id`  property to the Model attributes object.**  Set  `id`  to an object with  `type`,  `primaryKey`  and  `autoIncrement`  properties set to `true`.
Specifying  `primaryKey: true`  intructs Sequelize to generate the primary key column using the property name defined in the model (in this case it's  `id`, but it could be anything, like  `identifier`). The ID should be a number, so its data type is  `INTEGER`, and  `autoIncrement: true`  automatically generates an ID that increments by 1 for each new entry.

#### Allow or Disallow nulls
The  `NULL`  value in SQL indicates that data does not exist for a field in a column. For example, if you create a record without providing a title, the database will display  `NULL`  as the title value.
Fields set to `NULL` can produce unexpected results in queries, so it's often a good idea to set certain fields of a model to not allow `null`, using `allowNull: false`.
With  `allowNull: false`  in place, if a field is  `null`  (for example, no  `title`  data exists), Sequelize will throw a validation error. For example:  `SequelizeValidationError: notNull Violation: Movie.title cannot be null`.

**Note:**  
`allowNull: true`  would mean that data does not have to exist for a particular field when inserting or updating a record.

#### Specify Default Values
Use `defaultValue` to set default values on properties.

[Sequelize Model](https://sequelize.org/master/class/lib/model.js~Model.html)
[Models Definition](https://sequelize.org/master/manual/models-definition.html)

### Add Validations to a Model
An ORM like Sequelize can automatically validate models, or a  _column's_  value.

Currently, you can successfully create a record by passing the  `Movie`  model instance an empty string for 'title', a negative 'runtime' integer, or even a release date that dates back to the pre-cinema era. 
This is less than ideal, so let's add validators to prevent inaccurate (and wasteful) records from being created as shown above.

#### Add a Validator

You specify a validator on a model attribute using a  `validate`  object. Within the  `validate`  object you can use the built-in validators supported by Sequelize (implemented by the library  [validator.js](https://github.com/validatorjs/validator.js)), or define your own custom validators.

1.  Add a  `validate`  property within the  `title`,  `runtime`, and  `releaseDate`  model attributes. Set  `validate`  to an object.
To prevent a value from being set to an empty string, use the `notEmpty` validator. In the `title` attribute's `validate` object, set `notEmpty` to `true`
**Customize the Error Message**
You can set a custom message when validation fails. To specify a custom error message, set the validator property to an object containing a  `msg`  property set to your custom message.
**Customize Validators - min / max**
Sequelize also supports custom validators that check if a value is within an expected range (like a date or number), part of a specified substring, or if it contains certain characters (like only letters or no letters, for example). It even provides regular expression validators, and [many more](http://docs.sequelizejs.com/manual/models-definition.html#validations).
You can think of a validator as a function that takes an argument: the value to validate. That argument is checked by the validator which determines if it's valid or invalid.
**Validate Dates**
View code example

Be sure to view the list of all the validators supported by Sequelize in [this link](http://docs.sequelizejs.com/manual/models-definition.html#validations). The next step will teach you how to catch `SequelizeValidationError` error types when calling the `create()` method, and how to transform errors to a simpler format.

[Model Basics](https://sequelize.org/master/manual/model-basics.html)

### Handle Validation Errors
When validation fails, Sequelize throws a `SequelizeValidationError` showing the message. For example:
`SequelizeValidationError: Validation error: Please provide a value for "title"`

We're currently catching and logging all errors to the console with a  `catch`  block and  `console.error()`. The format of the error is complex, which makes it difficult to track down the actual validation error message. In this step, we'll transform errors to a simpler format by  _catching_  `SequelizeValidationError`  error types when creating or updating records.

1. Replace the nody of te catch block with if..else blocks. The error thrown by Sequelize contains an `errors` property, which is an array with 1 or more `ValidationErrorItems`, each represents a failed validation. Before displaying the error, we want to check the type of error.
2. _If_ the error is `SequelizeValidationError`, map over the error item(s) and return an array holding any error messages. In this case, we're outputting them to the console.
3. n the _else_ block, use a `throw` statement to rethrow other types of errors caught by `catch` (for example, general errors, a record is missing, or any other unforeseen errors):

[array.prototype.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

### Use Options to Adjust Models
*Sequelize* provides options to set on each model to control table and column names, timestamps and more.

To further configure a model using options, pass  [option properties](http://docs.sequelizejs.com/manual/models-definition.html#defining-as-part-of-the-model-options)  to the model instance's "options" object –- the second argument of  `model.init()`. You can control:
* Timestamps
* Prevent Pluralization of Tables with `freezeTableName`
* Modify Model Names
* Custom Tables Names with `TableName`
* Global Options: Some model options can be set globally by passing the `define` options object to the Sequelize constructor.
```JavaScript
const sequelize = new Sequelize({
 dialect: 'sqlite', 
 storage: 'movies.db', 
 // global options 
 define: { 
	 freezeTableName: true, 
	 timestamps: false, 
	 }, 
 });
```
You set the properties for all tables in one place rather than having to set them separately.

Model options are just that: options available to you to influence the way Sequelize handles the movement of data to and from your database. How you use these options is up to you and your project needs.

### Performing CRUD Operations
#### Create a Record
In this step, we'll explore two common methods for creating records (or building model instances):  `build()`  and  `create()`.

#### `build()`
The  `build()`  method builds a non-persistent model instance. It returns an unsaved object, which you explicitly have to save to the database. Creating a record with  `build()`  is a two-step process: you  _build_  an instance, then  _save_  it.

1. Call  `build()`  on the model. Notice that if you run `npm start` the `id` value for this record would be `null`, and wont appear on the DB Browser for SQLite 
2. Store the record in the database.** Call the `save()` method
```JavaScript
 // New instance 
 const movie3 = await Movie.build({ 
 title: 'Toy Story 3', 
 runtime: 103, 
 releaseDate: '2010-06-18', 
 isAvailableOnVHS: false, 
 }); 
 await movie3.save(); // save the record 
 console.log(movie3.toJSON());
```
#### create( )
While `build()` requires that you call `save()` to persist and store your instance's data, `create()` both builds and automatically saves a model instance, all in one step.

The `build()` method stores data in memory only; data is not saved to the database until calling `.save()`. Because of this, `build()` gives you the ability to modify an instance after it's instantiated, but before any data is stored in the database.
```JavaScript
 const movie3 = await Movie.build({ 
 title: 'Toy Story 3', 
 runtime: 103, 
 releaseDate: '2010-06-18', 
 isAvailableOnVHS: false, 
 }); 
 movie3.title = 'Updated Title';
 await movie3.save(); // save the record 
 //title: 'Updated Title' is stored in the database
```
`build()` is useful when you need to manipulate instances in any way before storing them. `build()` would also be useful when you need a model instance to bind to a template (for example, a "New Record" form or page). You can create then save a database object from the data bound to the template.

`create()` is convenient when you just need to create and save a new record at once (within an Express POST route handler, for example).
[Model Instances](https://sequelize.org/master/manual/model-instances.html)
[build( )](https://sequelize.org/master/class/lib/model.js~Model.html#static-method-build)
[create( )](https://sequelize.org/master/class/lib/model.js~Model.html#static-method-create)

### Retrive Records
In this step, you will learn how to perform  _read_  operations on your database tables using Sequelize's data retrieval methods, which query data from the database.

We'll start with finder methods that search for one specific element in the database. At this point, feel free to add more 'Movie' and 'People' records to your database.

* `findByPk()` The method `findByPk()` (or 'find by primary key') retrieves a single instance by its primary key (or id) value.
* `findOne()`  retrieves **one** specific element in a table. The  `where`  object is used to filter a query using the property / value pairs passed to it. As you'll soon learn, the property values can be primitives for equality matches or objects for creating more complex comparisons, using  [Sequelize's operators](http://docs.sequelizejs.com/manual/querying.html#operators). 
Since `findOne()` always returns only the first matching record, there may be times when the method returns the wrong record (or not the one you want). `findByPk()` is a more precise and efficient way to find a record.
* `findAll()` retrieves a collection of  **all**  records, instead of a single record. The `findAll()` method also take an options object where you can add any number of criteria to filter the results. You can also use `where` for more complex _AND_ conditions by nesting two or more properties

[Sequelize Querying](https://sequelize.org/master/manual/querying.html)
[Data Retrieval](https://sequelize.org/master/manual/models-usage.html#data-retrieval---finders)
[findByPk( )](https://sequelize.org/master/class/lib/model.js~Model.html#static-method-findByPk)
[findAll( )](https://sequelize.org/master/class/lib/model.js~Model.html#static-method-findAll)
[Model Querying](https://sequelize.org/master/manual/model-querying-basics.html)

### Attributes , Operators and Ordering
Currently, when you retrieve data using a retrieval method, all attributes (or columns) of an entry are returned. For instance:
```JavaScript
{ id: 2,
 title: 'The Incredibles', 
 runtime: 115, 
 releaseDate: '2004-04-14', 
 isAvailableOnVHS: true, 
 createdAt: 2019-07-19T15:36:05.066Z, 
 updatedAt: 2019-07-19T15:36:05.066Z } 
```
Sequelize lets you pass an  _attributes_  option to a finder method to specify exactly which attributes to return.
```JavaScript
 const movies = await Movie.findAll({ 
 attributes: ['id', 'title'], // return only id and title 
 where: { 
 isAvailableOnVHS: true, 
 }, 
 }); console.log( movies.map(movie => movie.toJSON()) );
```
**Operators**
You'll often want to create more complex comparisons and filtering of data. For example, return all movies released after  `1-01-2004`, or movies with a runtime greater than 95 minutes.

Sequelizes provides special properties called operators to let you do just that. You can specify comparisons like "greater than", "less than", "endsWith" and  [much more](http://docs.sequelizejs.com/manual/querying.html#operators)  within your  `where`  clauses.

The  `db/index.js`  file exposes the Sequelize package whenever you import  `./db`  into your application code. This means that wherever you use  `require('./db')`, you have access to all of Sequelize's methods and functionality. Let's begin using operators by first destructuring the  `Op`  (Operators) property from Sequelize.
```JavaScript
const { Op} = db.Sequelize;
```
You use an operator by calling the operator property (`Op`) followed by the operator you want to use inside brackets.

**Ordering**
Within the `findAll()` method's options object, you can also specify the order of the returned results
```JavaScript
const movies = await Movie.findAll({
 attributes: ['id', 'title'], 
 where: { title: { 
 [Op.endsWith]: 'story' 
 },
}, 
order: [['id', 'DESC']] // IDs in descending order }); 
console.log( movies.map(movie => movie.toJSON()) );
```
[https://sequelize.org/master/manual/querying.html#operators](https://sequelize.org/master/manual/querying.html#operators)

### Update a Record
Once you've found the record, there are two ways you might update it:

-   Update the property using dot notation (`instance.property = new value`) and persist the changes with  `save()`.
```JavaScript
...
const toyStory3 = await Movie.findByPk(3);
toyStory3.isAvailableOnVHS = true; 
await toyStory3.save();   

console.log( toyStory3.get({ plain: true }) );
...
```
The  `save()`  method needs to be called on the model instance to save the update to the database.

**Note:** When converting an instance or collection of instances to JSON, calling  `get({ plain: true})`  returns the same as calling  `.toJSON()`  – a  _plain_  object with just the model attributes and values.

-   Use the Sequelize  `update()`  method.
```JavaScript
...
const toyStory3 = await Movie.findByPk(3);
await toyStory3.update({
	isAvailableOnVHS: true,
}); 

console.log( toyStory3.get({ plain: true }) );
...
```
Both approaches you learned effectively update a record and persist the changes to the database. Once you update a record, its `updatedAt` value automatically updates to the time at which the update occurred

**Define Which Attributes to Save**
Sequelize gives you the ability to specify exactly which attributes should be saved when using either the `save()` or `update()` method, with the `fields` property.
```JavaScript
const toyStory3 = await Movie.findByPk(3); 
await toyStory3.update({ 
	title: 'Trinket Tale 3', // this will be ignored 
	isAvailableOnVHS: true, 
	}, { fields: ['isAvailableOnVHS'] });   

console.log( toyStory3.get({ plain: true }) );
```
Being able to allow/disallow (or _whitelist_) columns to update is useful when you want to ensure that users cannot pass objects with columns that should not be updated via a form, for example).

[Model Instances](https://sequelize.org/master/manual/model-instances.html)
[update( )](https://sequelize.org/master/class/lib/model.js~Model.html#static-method-update)

### Delete a Record
In this step, you will learn how to delete records with Sequelize. Once you've created an instance and have a reference to it, you can delete a record from your database using the Sequelize `destroy()` method.
1. Find the record in order to delete it.
2. Call destroy() method to destroy it
```JavaScript
(async () => {
  await db.sequelize.sync({ force: true });   
  try { 
  // All model instances...   
  // Find a record 
  const toyStory = await Movie.findByPk(1);   
  // Delete a record await toyStory.destroy();   	

  // Find and log all movies 
  const movies = await Movie.findAll(); 
  console.log( movies.map(movie => movie.toJSON()) );   
  } catch(error) { 
  ... 
  } 
})();
```
**Note:** Since `delete` is a reserved keyword in JavaScript, Sequelize uses `destroy()`.

**Logical / "Soft" Deletes vs. Physical Deletes**
Sequelize provides a "paranoid" setting for "soft" deletes. This gives you the ability to mark a record as deleted instead of physically removing it from the database.
1. **Open the file  `db/models/movie.js`.** Pass the `paranoid` property to your `Movie` model's options object and set it to `true`:
```JavaScript
module.exports = (sequelize) => {
 class Movie extends Sequelize.Model {} 
 Movie.init({ 
   id: {...}, 
   title: {...}, 
   runtime: {...}, 
   releaseDate: {...}, 
   isAvailableOnVHS: {...},
 }, { 
   paranoid: true, // enable "soft" deletes 
   sequelize 
 });   
 return Movie; 
};
```
Setting the `paranoid` option to `true` means that a destroyed record will not be physically deleted from the database, but it will also not be returned in future queries.
Not permanently deleting a record with `destroy()` could have its advantages. It allows you to keep a history for database auditing. It also makes it easier to restore "deleted" data, and there is less risk of data loss if something goes wrong.
However, soft-deleted records also take up space in your database. They could add complexity to your queries and you may have to consider the performance implications of keeping all the data down the road.

[bulkCreate( )](https://sequelize.org/master/class/lib/model.js~Model.html#static-method-bulkCreate)

### Next Steps
This course was an introduction to ORMs and Sequelize. It did not cover topics like defining data relationships, managing multiple environments (local, test, and production), using the Sequelize CLI, or CRUD operations using Sequelize and Express routes

**Associations (Data Relationships)**

The data in your models can be described using the  _nouns_  that you've identified for your application – in this case,  `Movie`  and  `Person`.

There are also relationships between your models (or tables). For example, a Movie might be associated with a Person as a director, and might also be associated with one or more "People" (the plural of Person) as its actors. These associations between Movie and Person are known as "data relationships".

A follow-on instruction step will teach how to  [define data relationships using SQL and Sequelize](https://teamtreehouse.com/library/data-relationships-with-sql-and-sequelize). You can also refer to the Sequelize docs to  [learn more about the various association types in Sequelize](http://docs.sequelizejs.com/manual/associations.html).

###  Data Relationships with SQL and Sequelize
This lesson will explore how to define data relationships using SQL and [Sequelize](https://sequelize.org/master/), a Node.js ORM (object-relational mapping) library for SQL databases.

[https://teamtreehouse.com/library/reporting-with-sql](https://teamtreehouse.com/library/reporting-with-sql)
[https://teamtreehouse.com/library/querying-relational-databases](https://teamtreehouse.com/library/querying-relational-databases)

**Understand Data Relationships**
When designing an application database, it's a common practice to start by listing all the things that the application will be working with—all of the "nouns".
The data for your application can be described using the nouns that you've identified for your application (Movie and Person in the case of the course exercise) There are also relationships between your nouns.

**Database Normalization** 
Database designers often refer to related or duplicated data contained within a single table as "unnormalized" data and the process of splitting that data into separate tables as "normalization".

**Data Relationship Types**
The data relationship between a person who has directed a movie and the movie itself is known as a one-to-many relationship. The "one" in this relationship is a person—the director—and the "many" are the movies that the person has directed.
One-to-many data relationships are the most common data relationship type. Other data relationship types include many-to-many and one-to-one. In this lesson, we'll be focusing on one-to-many data relationships.

**Define Data Relationship in Sequelize Models**
Earlier we saw an example of defining a one-to-many data relationship between two tables by adding a foreign key column to a table. When interacting with the database directly, developers write and execute SQL statements to make changes to the database.
When using an ORM like Sequelize, you don't interact with the database directly. Instead, you define models and model relationships to configure how Sequelize creates the database.

In theory, using an ORM makes your life as a developer "easier". When you're used to interacting with the database directly, there's actually a learning curve to familiarize yourself with how Sequelize (or any ORM) handles data relationships. But once you're comfortable with the ORM's terminology and API, it's generally a time saver when writing queries.

** Data Relationships in Sequelize** 
Sequelize refers to data relationships as **"associations"**. Just as there are data relationship types, there are a variety of association types. The type of association you use is determined by the data relationship type between two models—the "source" model and the "target" model.

Earlier, we looked at a one-to-many data relationship between the People and Movies database tables. In that one-to-many relationship, the "one" is a person—the director—and the "many" are the movies that the person has directed.

Let's start with examining the association from the Person model's point of view (the source model) to the Movie model (the target model). A single (or "one") person can be associated with one or more (or "many") movies as its director. So the Sequelize association type between the Person and Movie models is a one-to-many association.

Now let's flip it around and examine the association from the Movie model's point of view (making it the "source" model) to the Person model (making it the "target" model). A single (or "one") movie can be associated with a single (or "one") person as its director. So the association type between the Movie and Person models is a one-to-one association.

While it's technically possible to define a data relationship using only a single association within a single model, defining the relationship using an association within each model gives us flexibility when retrieving data from the database.

**Define a One-to-Many Relationship using Sequelize Associations**
Associate both The movie and person files.
**Refine Sequelize Associations**
Sequelize provides a variety of association options that we can use to fix these shortcomings.
**Customize the Foreign Key Name**
To customize the foreign key name—both in the model and the associated database table—we can pass an options object as a second argument into the `belongsTo()` and `hasMany()` methods.

**models/movie.js:**
```JavaScript
Movie.associate = (models) => {
 Movie.belongsTo(models.Person, { foreignKey: 'directorPersonId' }); }; 
```
**models/person.js:**
```JavaScript
Person.associate = (models) => {
 Person.hasMany(models.Movie, { foreignKey: 'directorPersonId' }); };
```
**Note:** Notice that we're updating both sides of the relationship with the same options. The foreign key configuration must be kept in sync across the Movie and Person models or Sequelize will not be able to understand that the associations are describing the same data relationship! Not keeping the options in sync will (typically) result in a duplicate foreign key column being added.

**Configure the Nullability of the Foreign Key Column**
We'll update both side of the relationship with the same options to ensure that Sequelize will understand that the association are describing the same data relationship.
**Create Related Data Using Sequelize Models**
To set a director on a Movie record, we first need to create the Person records. This is necessary because each Person model instance  `id`  value must be available before attempting to set the Movie model  `directorPersonId`  foreign key property.

The  `app.js`  file is the entry point into the application. Within this file, the Sequelize models are used to create and retrieve data from the database. Let's review this file to understand the overall behavior of the application.

**Open and Review the  `app.js`  File**
At the very top of the file, we declare the  `sequelize`  and  `models`  variables and initialize them to the  `sequelize`  and  `models`  objects imported from the  `./db`  module:

```JavaScript
const { sequelize, models } = require('./db'); 
```

In the above code, we're using  [JavaScript destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)  to get references to the  `sequelize`  and  `models`  objects. Without destructuring, the code looks like:

```JavaScript
const dbModule = require('./db'); 
const sequelize = dbModule.sequelize; 
const models = dbModule.models; 
```
Then we declare the  `Person`  and  `Movie`  variables and initialize them to the individual Person and Movie models available on the  `models`  object:
```JavaScript
const { Person, Movie } = models; 
```
Before interacting with the database, we declare a collection of variables for the Person and Movie records that we're creating as seed data:
```JavaScript
let bradBird; 
let vinDiesel; 
let eliMarienthal; 
let craigTNelson; 
let hollyHunter; 
let theIronGiant; 
let theIncredibles;
```
**Note:** Declaring a variable for each record is impractical when seeding the database with a large number of records. A more robust solution would use a query to retrieve records from the database before creating any related records.

Every interaction with the database using Sequelize is an asynchronous operation represented by a JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

In this lesson, we'll use the [ES2017 async/await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) syntax for all asynchronous calls made with Sequelize. We'll keep things really simple by executing all Sequelize queries and instance methods in `app.js` within an _async_ immediately invoked function expression ([IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)). Inside the IIFE, a `try/catch` statement runs the code that needs to be executed and catches any exceptions that are thrown.

1. To start, call the Sequelize `authenticate()` method to test the connection to the database.
2. Sync the models with the database by calling the Sequelize `sync()` method. This causes the model's associated tables in the database to be dropped (i.e. deleted) and created every time the application is started, which makes it easy to make a change, run the app, and test the change.
**Note:** The `{force: true}` parameter completely drops a table and re-creates it afterwards each time you start your app (it's a destructive operation). While useful for testing purposes, it might not be safe to use in a project (or production database) where you'd want your data to persist.
--------------------
**Population the Database with Seed Data**
1. Create a person record
2. Use the `Promiseall()` method to wait until all five promised have been fullfilled. Store the aggregate promise in the variable `peopleInstances`
3. Use a combination of the `console.log()` and `JSON.stringify()` methods to log the data stored in `movieInstances` to the console as a JSON string
```JavaScript
console.log(JSON.stringify(peopleInstances, null, 2));
```
**Note:** The [JSON stringify() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) defines two optional parameters after the first `value` parameter. We're passing a numeric value of `2` for the second optional parameter—the `space` parameter—in order to indicate how many space characters should be used for whitespace.

4.  Use [Array destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) to _pluck_ the individual Person model instances from the `peopleInstances` variable (which is an array of values returned from the Promise `all()` method call):
```JavaScript
[bradBird, vinDiesel, eliMarienthal, craigTNelson, hollyHunter] = peopleInstances;
```
5. We create the movie instances just like Persons
6. Finally, use Sequelize's `findAll()` method to retrieve the movie and person data from the database, then map over the results and output them to the console as JSON objects.

When converting an instance or collection of instances to JSON, calling `.get({ plain: true})` returns the same as calling `.toJSON()` – a _plain_ object with just the model attributes and values.

**Set a Movie's Director**
* Set a movie's director by adding a `directorPersonId` property within the object passed to `Movie.create()`.
* Test
```JavaScript
[
 { 	"id": 1, 
	"title": "The Iron Giant", 
	"releaseYear": 1999, 
	"directorPersonId": 1 
}, 
{ 
	"id": 2, 
	"title": "The Incredibles", 
	"releaseYear": 2004, 
	"directorPersonId": 1 
	} 
]
```
On its own, this isn't very useful information to have. We could use the primary key value to retrieve the director's row from the People table, but that'd require another database operation. Luckily, Sequelize gives us a way to retrieve related data via a single query method call.

**Use the Sequelize _include_ Query Option**
When calling the Movie `findAll()` method, we can pass an options object literal to configure the query. One of the available options—specified using the `include` property—allows us to indicate that we want any related Person model data.
```JavaScript
const  movies  =  await  Movie.findAll({
	include: [
		{
			model:  Person,
		},
	],
});
console.log(movies.map(movie  =>  movie.get({  plain:  true})));
```
With this, the data returned from the database looks like this:
```JavaScript
[
 { 	"id": 1, 
	"title": "The Iron Giant", 
	"releaseYear": 1999, 
	"directorPersonId": 1,
	 "Person": { 
		 "id": 1, 
		 "firstName": "Brad", 
		 "lastName": "Bird" 
		 } 
	}, 
	{ 
	"id": 2, 
	"title": "The Incredibles", 
	"releaseYear": 2004, 
	"directorPersonId": 1,
	"Person": { 
		 "id": 1, 
		 "firstName": "Brad", 
		 "lastName": "Bird" 
		 }
	} 
]
```
**Customize the Associated Model Property Name**
The `Person` property in the retrieved movie data doesn’t convey anything about the relationship of a person to a movie. This makes it difficult to understand that the person is the movie's director. The `Person` property also doesn't match the property naming convention of the other model properties (i.e. `id`, `title`, `releaseYear`, `directorPersonId`). This increases the chance that clients will introduce capitalization related bugs into their code.

To address these shortcomings we’ll provide an alias for the model association and include that alias in our query method options.

1. **`models/movie.js`  file.** Create an alias for the model association by adding an `as` property to the `belongsTo()` method options object literal. The value of the `as` property is the alias that we want to use for this association. Let's also keep the Person model association in sync with the Movie model association.
2. **Open the  `db/models/person.js`  file.** Add an `as` property to the `hasMany()` method options object literal and set its value to `'director'`
3. Back in the `app.js` file, update the `Movie.findAll()` method `include` option with the same `as` alias property

**Take Full Advantage of Your Model Associations**
Earlier, it was mentioned that defining a data relationship from both models' point of view gives you flexibility with how you can retrieve data from the database. Let's see that in action by updating our Person `findAll()` method call to include any related Movie model data.

#### Sequelize CLI
When you're building large applications, setting up Sequelize and writing all the model configurations by hand (including importing & exporting files) can get tiresome, and you could make a mistake.

The  [Sequelize CLI](https://github.com/sequelize/cli)  is a tool that initializes all the configuration code, folders and helpers you need for your application. It also sets up and  [configures Sequelize](http://docs.sequelizejs.com/manual/migrations.html#the-cli)  to generate and export your models

#### Manage Multiple Environments
et up database configurations for the three main environments you need in an application:

-   **Development:**  environment for when you're programming your app.
-   **Testing:**  environment for running automated tests to make sure your code interacts correctly with the database.
-   **Production:**  environment for the live site using the "real data" your application needs.

The Sequelize CLI helps  [handle the database configurations](http://docs.sequelizejs.com/manual/migrations.html#configuration)  for each of the three environments

#### Express Routes and CRUD Operations
You'll often wire [Express routes](https://expressjs.com/en/guide/routing.html) to your SQL-based database via Sequelize ORM. The following demonstrates how you might use Sequelize within an Express application to perform CRUD operations:

```JavaScript
const { Router } = require('express'); 
const { Movie } = require('../models');   

const router = new Router();   

/* POST create movie */ 
router.post('/', async (req, res, next) => {
 const movie = await Movie.create(req.body); 
 res.redirect('/movies/' + movie.id); });   
 
/* GET / retrieve movie to update */ 
router.get('/:id/edit', async (req, res, next) => {
 const movie = await Movie.findByPk(req.params.id); res.render('movies/edit', { movie, title: 'Edit Movie' }); 
 });   

/* PUT update movie */ 
router.put('/:id', async (req, res, next) => {
 const movie = await Movie.findByPk(req.params.id); 
 await movie.update(req.body); 
 res.redirect('/movies/' + movie.id);
  });
 
 /* Delete movie */ 
 router.post('/movies/:id/delete', async (req, res) => {
 const movieToDelete = await Movie.findByPk(req.params.id); 
 await movieToDelete.destroy(); 
 res.redirect('/movies'); 
 });

```





## Sequelize ORM with Express <a name="sequelize-express"></a>
### Introducing the Project
In previous lessons, you learned how to use the Sequelize ORM to interface with sql based databases within a Node JS application. You also learned how to work with the Express Web Application framework for Node to build dynamic web applications. 

In this workshop you'll bring together much of what you've learned about Sequelize and Express to build a simple CRUD application that is connected to a Sequel database. You'll use the method Sequelize provides to perform CRUD operations withing Express routes using HTTP methods like GET and POST to manage the data and the database.

In addition, you'll work with the sequelize/cli a helpful command line interface for sequelize to initialize all the configuration code, folders and helpers  needed for the application.

[Express Tutorial Part 2: Creating a skeleton website](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/skeleton_website)
[Express application generator](https://expressjs.com/en/starter/generator.html)
[Sequelize CLI / Installed](https://github.com/sequelize/cli)


### Install and Use Sequelize CLI
Many development tools have what's called a CLI, or command-line interface, which is a special piece of software that's used to aid in the development process. Sequelize is no different, it has a useful command-line interface for initializing and bootstrapping your database project, creating models, database configuration files and more. The CLI operates with many relational databases like PostgreSQL, MySQL, MSSQL, and Sqlite.

`npx sequelize --help` Sequelize help command
`npx sequelize init` Initializes all the configuration code, folders and helpers needed for the applications, it sets up four directories: *config*, *migrations*, *models*, and *seeders*

**Note:** The `seeders` folder usually contains "seed files", which hold data you can use to populate your database tables with sample or test data. You will not create or use seed files in this workshop, so feel free to delete the `seeders` folder.
_________
#### Configuration
This file holds the database configurations for the three main environments you need in an application:
-   **Development:**  For when you're programming your app
-   **Testing:**  For running automated tests to make sure your code interacts correctly with the database
-   **Production:**  For the live site using the "actual data" your application needs

By default, `config.json` is configured with boilerplate credentials for a MySQL database. But the project might use other relational databases -- in this case, SQLite.

You can specify the options shown in the examples in your `config.json` file for each of the three environments. Ideally, in development, you use the same database you use in production. But it's not uncommon to use different databases. For instance, you might use SQLite in development and testing so that you don’t need to install and run a large database on your computer, and use [PostgreSQL](https://www.postgresql.org/) for a more powerful Linux server in production.

1. We'll update the config.json a
2. Create a Model
Another important folder generated by the Sequelize CLI is `models`, which holds all your models – the code that maps JavaScript objects to database tables. The `index.js` file inside the `models` folder is the entry point file for models. It imports and syncs up all the models you define, and it exposes the Sequelize package whenever you import models into your application code.
3. Add the Article attributes inside the object literal that defines model attributes.

#### Synchronize Models with the Database
Finally, let's set up Sequelize to synchronize models with the database. You've learned that the `sync()` method automatically creates or updates your database tables according to your model definition. We can automatically sync models with the database by calling `sync()` every time the server starts. An ideal place to sync models is in the executable file that starts the app, `bin/www`. The Express application generator creates this file to start the server (on port `3000` by default) and set up basic error handling.

1. Open the file `bin/www`
2. Synchronize all models by calling `sequelize.sync()` first.
3. Since the file now references `sequelize`, be sure to require sequelize from the models index file at the top of the `www` file:
Saving the latest changes (or running `npm start`) should generate a `development.db` file in the root of the application folder.

With the database code set up, you can now focus on the important parts of the application. There's currently no data in the database, so in the next video, you'll begin to work on the routes for data creation.

[https://sequelize.org/master/manual/migrations.html#the-cli](https://sequelize.org/master/manual/migrations.html#the-cli)
[https://github.com/sequelize/cli](https://github.com/sequelize/cli)
[https://blog.npmjs.org/post/162869356040/introducing-npx-an-npm-package-runner](https://blog.npmjs.org/post/162869356040/introducing-npx-an-npm-package-runner)
[https://sequelize.org/master/manual/models-definition.html#database-synchronization](https://sequelize.org/master/manual/models-definition.html#database-synchronization)
[https://sequelize.org/master/manual/migrations.html#creating-first-seed](https://sequelize.org/master/manual/migrations.html#creating-first-seed)

### Create Entries
We've configured sequelized, initialized a connection to the SQLite database, and synced the article model with the database. Now, well work on the routes for data creation.

- Include the article model at the top of the articles.js routes file `const  Article  =  require('../models').Article;` now we're able to use all the associated ORM methods you've worked with before.
- Now, w're ready to work on getting data into the database
```JavaScript
/* POST create article. */

router.post('/',  asyncHandler(async  (req,  res)  =>  {
	console.log(req.body);
	res.redirect("/articles/");
}));
``` 
You'e learned that the sequelize `create()` method builds a new model instance, which represents a database row and automatically stores its data in the database

The request's  `body`  property returns an object containing the key/value pairs of data submitted in the request body. The following  `app.use()`  methods, written in  `app.js`, provide access to the request body.
```JavaScript
// view engine setup
... 
app.use(express.json()); 
app.use(express.urlencoded({ extended: false }));
```

[VSCode extension to explore and query SQLite databases](https://marketplace.visualstudio.com/items?itemName=alexcvzz.vscode-sqlite)

### Find Entries
1. Find th GET route for the individual article
2. Create a constant and use the Sequelize `findByPk()` method

Next, we'll work on retrieving all the articles and rendering them in the root route or main articles page.

### Instance Methods
Sequelize allows you to extend models with additional functionality. Since Sequelize models are ES6 classes, you can easily add custom instance level methods that encapsulate the functionality. In this video, you'll create helper methods to format an article's publish date and short description.

We'll create a "published at" helper method which formats the publish or created at date, and a short description method that generates a short description for an article when displayed in the main article listing view. These methods will be available to ALL model instances created or invoked in the context of each model hence the name _instance methods._

1. Go to the model that will have the date helper method
2. Require the moment library
3. Update the model, with the format that you'd like to use
4. And update the view to display the methods

[moment.js](https://momentjs.com/)
[String.prototype.substring()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring)


### Update and Delete Entries
Updating and deleting entries is a two  step process, first you retrieve the entry to update or delete from the database, then once you found the entry, perform a sequelize update or destroy operation on it.
**To Update**:
- Edit the article form
-  Update article in the POST route

[Model Instances](https://sequelize.org/master/manual/model-instances.html)

### Validating and Handling Errors
So far, the `catch` block in the `asyncHandler` function is the only part of the code that's handling rejected Promises returned from the database calls. It catches a rejected promise when an error occurs and sends a `500` status code (or Internal Server Error) to the user

* Return a 404 status when someone looks for an inexistent article in all CRUD operations, except create and read.
* Add Validation
	* to the Article Model

REVIEW FUNNY BEHAVIOR IN THE UPDATE FORM THAT LETS YOU UPDATE ONCE THE ERROR HAS BEEN THROWN AND WHEN SUBMITTING SENDS A 404.
[Nesting_try...catch_statements](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#Nesting_try...catch_statements)
[Model Instancesl](https://sequelize.org/master/manual/model-instances.html)

### Next Steps
You can extend this project:
- Add a comments to the articles
- User Authentication
- Filter by Author using WHERE
- Add pagination
[Sequelize](https://sequelize.org/master/manual/getting-started.html)
[Express APIl](https://expressjs.com/en/4x/api.html)

## REST APIs with Express <a name="api-express"></a>
### Getting to Know REST APIs
#### Intro to REST APIs
 To define a REST API, we first need to talk about a traditional web application. This applications handle both server side and client side concerns. Say you build a web application to keep a record of your favorite recipes. To view a certain recipe, you'd click on that recipe's URL, and your browser would request that recipe from a server. A traditional server side application would respond to that request by finding the recipe data in a database, assembling that data into HTML templates and sending that HTML back to the browser to be displayed. But what if you wanted to use that same recipe information to build a mobile app, or an entirely different application, that's where REST API comes in, when you request specific recipe in a RESTful application, the application respond only with the recipe data, typically in the form of JSON, sending JSON data rather that HTML means that the back end only has to be built once, while any number of front end applications can consume and display the data.

When designing an application this way, you can manipulate the same data in endless ways. If a have a REST API for recipes, for example, I could create a recipe website, but I could also use the same data to create a meal planning app, a calorie tracking app, a virtual cookbook, and on, an on.

REST APIs can provide data and content for rich web applications, mobile apps, and other server side applications, even those other applications written in other programming languages. Basically, a REST API let's you retrieve data and present thatd ata in any way you want, providing amazing flexibility.

In this course, we'll use Node and Express to build out a simple API that provides data about famous quotes. When we're finished, users will be able to request famous quotes from our API, as well as add new quotes, edit and delete existing quotes, and request a random quote.

[JavaScript Async/await callbacks](https://www.freecodecamp.org/news/javascript-from-callbacks-to-async-await-1cc090ddad99/)

#### What is a REST API
To get a better sense of what a REST API is, let's first talk about how information is transferred on the web. First a client (an applications often JavaScript running in a web browser) request information from a server using a URL.

The REST in REST API stand for **Representational State Transfer**, and it's essentially a set of ideas about how the server should respond to a request from a client. A traditional application server side application responds with HTML, a REST API simply responds with data. It's then up to another application, a front-end application build with a framework like React or Vue, or a mobile device, or even a command line tool to format and display the data from the API.

* http://api.github.com/users/:username
* http://api.github.com/users/sheilaanguiano

Notice that in API speak, this is known as *requesting a resource*, the GitHub data in this case being the resource. The URL from which I request the resource is called an endpoint. By entering this URL into the browser, I'm making a GET request, and in response GitHub's REST API is sending me back the information I requested. In order to do anything useful with this information, I need a way to make a GET request programmatically with jQuery, the Fetch API or a library like Axios

[Axios](https://github.com/axios/axios)
[Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
[https://randomuser.me/](https://randomuser.me/)
[https://developer.github.com/v3/](https://developer.github.com/v3/)

#### HTTP Methods and CRUD Operations
We use web applications for a huge variety of things, but at their simples, many follow a common patter, CREATE, READ, UPDATE and DELETE. Take a blog or a popular social media site. You can usually make a new post, view other posts, edit a post or delete a post. This pattern is commonly known by the acronym **CRUD**. REST APIs allow a client to manipulate data using actions that map closely to the idea of CRUD. These actions are GET, POST, PUT and DELETE, which are known as HTTP verbs or HTTP methods. There are actually many more HTTP methods.

Information in a REST API is typically organized using nouns that describe what the data represents, nouns like users, posts, movies or recipes. Using HTTP methods and API nouns, a client can tell a REST API what information it wants and what it wants to do with that information.When we write an API, we're essentially programming responses to various HTTP requests for resources. 

#### A Simple API
A simple route that responds to a GET request with JSON.

1- Download the project files and install the needed packages running `npm install`
2- Create an Express GET route handler. Recall that the Express functions adds a bunch of methods to Node's HTTP server to make it easier for us to receive and respond to requests. These express methods include GET, POST, pUT and DELETE
3- Inside the callback function , we wanna send back JSON, so to do that, we can use the JSON method available.
```javascript
const express = require('express');
const app = express();
 
 /* 
 The GET method takes 2 arguments:
 1.Route that we wanna handle
 2.The callback functionwe want to run when this request comes in, how we want to respond 
 The callback takes at least 2 arguments, one representing the incoming request from the client, and one representing the ongoing response from the server shortened into: req & res
 */
app.get('/greetings', (req, res) => {
  res.json({greeting: "Hello World"})
});

```

By visiting `localhost:3000/greetings` we're sending a GET request to the greetings rote, which we've programmed in our Express application to send back a JSON object containing a greeting. So, we wrote code that respond with JSON when a client makes a request to an endpoint. This is a very simple API

#### Planning Out a REST API
We can plan a RESTful application by describing what we want it to do in plain english by using the most common HTTP request methods: get, post, put, and delete, and mapping them to CRUD operations, create, read, update, and delete.
```JavaScript
//Send a GET request to READ a list of quotes
//Send a GET request to READ(view) a quote
//Send a POST request to CREATE a new quote
//Send a PUT request to UPDATE(edit) a quote
//Send a DELETE request to DELETE a quote
//Send a GET request to READ (view) a random quote
```
This is a good plan, but let's not forget the nouns we discussed earlier. We use nouns to describe the resources or data representations, that the client can request from the API. A resource can be any number of things: users, customers, books, etc. in our case is quotes. So we want the client to be able to send GET request to `/quotes` to READ a list of quotes, and to view a single quote, the client will send a request to `/quotes/:id` the `:` indicates that `:id` is a representation,  or a parameter or the actual endpoint

```JavaScript
//Send a GET request to /quotes to READ a list of quotes
//Send a GET request to /quotes/:id to READ(view) a quote
//Send a POST request to /quotes to CREATE a new quote
//Send a PUT request to /quotes/:id to UPDATE(edit) a quote
//Send a DELETE request to/quotes/:id to DELETE a quote
//Send a GET request to /quotes/quote/random READ (view) a random quote
```
Notice that many of these endpoints are the same, that's because each endpoint can have multiple HTTP methods

#### GET a Quote, GET all the Quotes
```javascript
const express = require('express');
const app = express();

//Send a GET request to /quotes to READ a list of quotes
app.get('/quotes', (req, res) => {
	res.json(data);
});

//Send a GET request to /quotes/:id
app.get('/quotes/:id', (req, res) => {
	const quote = data.quotes.find(quote => quote.id == req.params.id);
	res.json(quote);
});


const data = {
	quotes: [
		{
			id: 8721,
			quote: 'Hello World',
			author: 'Someone'
		}
	]
}
```

### Managing Data and Asynchronous Code
#### Managing REST API Data
To keep things simple and focused, we’re going to store the data for our REST API in this JSON file called data.json. Think of the data.json file as a mock database-- a datastore where we can save and persist information for our API.

Typically, when you're building an application, you store application data in a database such as PostgressSQL or MongoDB. Depending on which database you choose, you'd likely use some kind of library, know as an ORM or **object-relational mapping**, to facilitate the communication between your express app and your database. Some example of ORM's include Mongoose for MongoDB and SQLize for SQL based databases . Learning to use an ORM can get complex, which is why or application won't use one, instead we've provided a module containing a few key function for building out our app.

The `recors.js` will serve as a very basic ORM, where there's a method to get quotes from our data store, a method to get one quote and so on. The purpose of this module is to allow us to work with some data for our API without a lot of the overhead.

Tool for Documention Code JSDoc
[https://jsdoc.app/about-getting-started.html](https://jsdoc.app/about-getting-started.html)

#### Refactor the GET all quotes route
The client will send us a requests containing the unique ID number of the requested quote. We'll use that number to find the correct quote in our data store, and then we' send that quote back to the client.

First, we'll need to know the ID of the quote the client is requesting, by using `req.params.id` and store the results in a variable called `quote`, and we send it back the response in json

### Create, Read, Update, Delete
#### Using Postman to Test Routes
By default, browsers send GET request, which makes them easy to test. Just hop into a browser and send a request to an endpoint. If you get back the information you were expecting, you know the route is working as intended. 
Sending other types of request from the browser like POST or DELETE, can be a little trickier.
**Postman** is an application that will allow us to send a variety of request to our API so that we can write endpoints to create, update and delete quotes, and then make sure our application us functioning as we expected. 

- Make sure the server is running.

#### Create a New Quote
To be able to access values on `req.body` we need to put a line of code (middleware)`app.use(express.json())` when a request comes in it'll be sent through this function before it hits one of our rout handlers. This middleware tells Express that we're expecting requests to come in as JSON, that way, Express can take the JSON we're sent, via the request body, and make it available to us on the request object on the property called body.

On Postman
* Select Post > route
* On the Body Tab > Select JSON and then write an object:
{
	"quote":"There is no place like home",
	"author": "Dorothy"
}
*hit SEND

#### Using Try/Catch with Async/ Await
Not much to add

#### HTTP Status Code
Sending proper status codes is a crucial part of building a useful and usable restful API.

#### Edit a Quote
A put request indicates to our application that a change is going to be made to an existing resource.
We'll expect the client to send us an object containing the author and the quote text to replace the current values. The client will send a request containing the new object, from the endpoint of the quote they wish to change.

For a put request, it is convention to send status code 204, which means no content. This generally means that everything went okay, but there's nothing to send back. Up until now, we've responded tp request with JSON, but for put request, it's convention not to respond with anything, but we need another way to end the request or the server will just hand indefinitely. We can end the request with the Express end method, which simply tells Express that we're done.

In a more real-world situation, you'd also wanna validate the information the client has sent to you. For example, has the client sent data for all the required properties? Is the data in the form your API is expecting, like a string or a number. When you're using an ORM you'll most likely create data models to do exactly that. You define the shape of your data in one place, which properties are required, which data type each property expect, and so on.

#### Delete a Quote
The delete route is going to be a lot like the update quote route, only it will completely remove the specified quote form the data store.

### Refactoring and Modularizing a REST API
#### Writing a Global Error Handler
A lot can go wrong in an application, and a big part of a developer’s job is to account for and gracefully deal with a variety of errors. We'll write a global error handler to send error messages to the client as JSON.
We're already doing a decent job of that, but there are some things we can do that will cut down on some of our repeating code.

There are two basic types of errors we're dealing with, stuff that went wrong with the request, and stuff that went wrong with the server. For our API, we're going to need to create our own custom error handler so that we can send the error message as a JSON object. We'll do that first by writing some middleware that creates an error, we'll then pass that error to an express error handling function, and that function will send error message as JSON. Express middleware are functions that run after a request comes in from the client and before a response is sent.

Middleware will run each time a request comes in unless you specify otherwise.

Express will call middleware functions in the order they've been added, so we'll want to place this middleware function below all of our other routes. This way if a request comes in, that doesn't match any of these routes, the request will fall into this piece of middleware.

#### Refactor with Express middleware
Using try/catch blocks to handler errors for each route can get messy after a while. We can write a middleware function that can abstract away the try/catch block to DRY up our code.

#### Structuring your REST API
If you've accessed information from an API in the past, you may have noticed that often, you request information from a `/api` route, like the randomuser API or the star wars API.

We can set up our API the same way within an express router, which is created using a method called express.router. Doing this way will be beneficial in two ways:
* We can map each of our routes to an endpoint that starts with `/api` without having to repeat /api for each and every route.
* Will keep our express files more modular, by moving all our routes out of app.ks and into their own file

`app.use('/api', routes);` Here we're saying when a request starts with the path `/api` use the routes inside of the `routes.js` file 

Back in `routes.js` we'll set up a new router. The router method allows us to route everything to `/api`without having to specify it on every single route

So we've created a new module named routes and moved all our quote routes into it. We're using the express router method which allow us to map these routes to a specified path. We're assigning express router to a variable called router, and using it to handle our various types of request. Finally, at the bottom of the file, we're exporting router along with all the routes we've defined in our file

#### Get a Random Quote

#### Going Further
When you're bulding your own API there are a number of things to consider
**Using a Database anr ORM**
* CORS
* User Authentication
* User Authorization

Now that you've had an introduction to building REST APIs with xPress, a natural next step would be to build an API using a database and an ORM. A database will help you maintain and persist larger and more complex datasets, while an ORM will help you interact with the database more easily. CORS, or cross-origin resource sharing is a mechanism that allows one web domain to communicate with another. If you tried to build a front-end for the REST API we just created, you could run into problems due to CORS.

Most applications involve some sort of login system, which is where user authentication and authorization come into play. Both involve building a login system for your application so that only authenticated users can use the API.



[https://www.html5rocks.com/en/tutorials/cors/](https://www.html5rocks.com/en/tutorials/cors/)
[https://expressjs.com/en/resources/middleware/cors.html](https://expressjs.com/en/resources/middleware/cors.html)
[https://serverfault.com/questions/57077/what-is-the-difference-between-authentication-and-authorization](https://serverfault.com/questions/57077/what-is-the-difference-between-authentication-and-authorization)
[https://teamtreehouse.com/library/oauth-authentication-with-passport](https://teamtreehouse.com/library/oauth-authentication-with-passport)

## Data Relationships with SQL and Sequelize <a name="sequelize-data-relationships"></a>
### Understand Data Relationships
#### Data Relationships
A SQL database is a relational database
- Organize data into tables
- Store, access, and connect data in relation to other data
- Think about and use data as related sets

For example, when designing an applications database, it's a common practice to start by listing all of the things that the application will be working with or all of the *nouns* and you reprent these nouns in multiple tables.

There are also relationships between these nouns or tables, these are called *data relationships*

#### Explore Data Relationship in a SQL Database
Data relationships are useful to  save storage space, let's imagine that we have a movie database with:
* id
* title
* releaseYear
* directorFirstName
* directorLastName

In the case of Steven Spilberg we'd have to repeat his name 37 times, without much reason. By creating a separate table named People we can connect this information using a single **foreign key**

**People Table**
id			Integer, primary key
firstName	varchar(255)
lastName	varchar(255)

**Movies**
id					Integer, primary Key
title				varchar(255)
releaseYear			Integer
direcrorPersonId	Integer, Foreign Key

With one number we have replaced the first name, last name and any other related information

#### Database Normalization
Database designers often refer to related or duplicated data within a single table as "unnormalized" data and splitting that data into separate tables as "normalization".

During the normalization process, database designers think about how to best fit relevant data into tables while looking for data that could potentially repeat, as well as values that depend on one another, and anything that could be grouped logically. That way, as you learned earlier, they avoid having to make changes to their data across multiple places (perhaps even millions of rows!).

After determining the tables you need, the next step in data normalization is to understand relationships and how they apply to the data you're working with.

[Ridiculously Unnormalized Database Schemas – Part One](https://michaeljswart.com/2011/01/ridiculously-unnormalized-database-schemas-part-one/)

#### Data Relationship Types
There are three types of relationships between tables. Developers describe these types by how many rows can relate to each other on either side of the relationship.  
*  "One to One"
* "One to Many"
* "Many to Many"

### Data Relationships in Sequelize
#### Database and Sequelize Configuration
The project uses SQLite, a simple, easy-to-use, relational database that doesn't require you to install anything on your system to make use of it. This makes it an ideal database for learning projects. For production-ready applications, you'll want to rely upon a database server platform like PostreSQL, Oracle, SQL Server, or one of the cloud-based solutions from Amazon, Microsoft, or Google.

One benefit of using an ORM like Sequelize is that it'll create the database for your application based upon your models. Sequelize generates and executes the following SQL statements to create the model's associated tables:

```sql
CREATE TABLE IF NOT EXISTS `People` (
    `id` INTEGER PRIMARY KEY AUTOINCREMENT,
    `firstName` VARCHAR(255) NOT NULL,
    `lastName` VARCHAR(255) NOT NULL
);
```
```sql
CREATE TABLE IF NOT EXISTS `Movies` (
    `id` INTEGER PRIMARY KEY AUTOINCREMENT,
    `title` VARCHAR(255) NOT NULL,
    `releaseYear` INTEGER NOT NULL
);
```
In the db/index.js file, Sequelize is configured as follows:

The dialect parameter specifies the specific version of SQL you're using (the SQL dialect of the database), which in this case it's sqlite.
The storage key sets the file path or the storage engine for SQLite. The value 'movies.db' creates a database file in your project named 'movies.db'.
Timestamps are disabled by setting the timestamps option to false. This removes the createdAt and updatedAt columns from the tables that Sequelize generates from our models.
```javascript
const options = {
  dialect: 'sqlite',
  storage: 'movies.db',
  define: {
    timestamps: false,
  },
};
```
#### Connect to Database
The app.js file is the entry point into the application. Within this file, we will use the Sequelize models to create and retrieve data from the database. Let's review this file to understand the overall behavior of the application.

At the very top of the file, we declare the sequelize and models variables and initialize them to the sequelize and models objects imported from the ./db module:
```javascript
const { sequelize, models } = require('./db');
```
In the above code, we're using JavaScript destructuring to get references to the sequelize and models objects. Without destructuring, the code looks like:
```javascript
const dbModule = require('./db');
const sequelize = dbModule.sequelize;
const models = dbModule.models;
```
**Async/await**
Every interaction with the database using Sequelize is an asynchronous operation represented by a JavaScript Promise.

In this course, we'll use the ES2017 async/await syntax for all asynchronous calls made with Sequelize. We'll keep things simple by executing all Sequelize queries, and instance methods in `app.js` within an *async* immediately invoked function expression (IIFE). Inside the IIFE, a try/catch statement runs the code that needs to be executed and catches any exceptions that are thrown.
```javascript
(async () => {
  try {
    // all asynchronous calls made with Sequelize

  } catch(error) {
    // catch and display Sequelize validation errors
  }
})();

```
To test the connection we'll call the sequelize `authenticate()` method and sync the models by calling `sync()`
```javascript
console.log('Testing the connection to the database...');

(async () => {
  try {
    // Test the connection to the database
    await sequelize.authenticate();
    console.log('Connection to the database successful!');

    // Sync the models
    console.log('Synchronizing the models with the database...');
    await sequelize.sync({ force: true });

             ...
  } catch(error) {
    ...
  }
})();
```
**Note**: The {force: true} parameter completely drops a table and re-creates it afterwards each time you start your app (it's a destructive operation). While useful for testing purposes, it might not be safe to use in a project (or production database) where you'd want your data to persist.

[Testing the connection](https://sequelize.org/docs/v6/getting-started/#testing-the-connection)
[Immediately invoked function expression (IIFE)](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)

#### Define Data Relationships in Seuqelize
When interacting with the database directly, developers write and execute SQL statements to make changes to the database.

When using an ORM like Sequelize, you don't interact with the database directly. Instead, you define models and model relationships to configure how Sequelize creates the database.

Sequelize refers to data relationships as **"associations"**. Just as there are data relationship types, there are a variety of association types. You determine the type of association to use by the data relationship type between two models—the "source" model and the "target" model.

Let's start by examining the association from the Person model's point of view (the source model) to the Movie model (the target model). A single (or "one") person can be associated with one or more (or "many") movies as its director. So the Sequelize association type between the Person and Movie models is a one-to-many association.

Now let's flip it around and examine the association from the Movie model's point of view (making it the "source" model) to the Person model (making it the "target" model). A single (or "one") movie can be associated with a single (or "one") person as its director. So the association type between the Movie and Person models is a one-to-one association.

**Note**: In real life, a movie can have more than one director. For our purposes, we're taking a simplified approach and allowing a movie to only have a single director.

While it's technically possible to define a data relationship using only a single association within a single model, defining the relationship using an association within each model gives us flexibility when retrieving data from the database. You'll learn how this works in a later step.
[Associations](https://sequelize.org/docs/v6/core-concepts/assocs/)
[Defining the Sequelize Associations](https://sequelize.org/docs/v6/core-concepts/assocs/#defining-the-sequelize-associations)

#### Define a One-to-Many Relationship Using Sequelize Associations
Currently our person file looks like this: 
```javascript
'use strict';
const Sequelize = require('sequelize');

module.exports = (sequelize) => {
  class Person extends Sequelize.Model {}
  Person.init({
    id: {
      type: Sequelize.INTEGER,
      primaryKey: true,
      autoIncrement: true,
    },
    firstName: {
      type: Sequelize.STRING,
      allowNull: false,
    },
    lastName: {
      type: Sequelize.STRING,
      allowNull: false,
    },
  }, { sequelize });

  Person.associate = (models) => {
    // TODO Add associations.
  };

  return Person;
};
```
We the add the association
```javascript
  Person.associate = (models) => {
    // one-to-many associations between Person and Movie model
    Person.hasMany(models.Movie);
  };
```
This tells Sequelize that a person can be associated with one or more (or "many") movies.
If we run the command npm start, we'll see that Sequelize generates and executes the following SQL statements to create the models' associated tables:
```sql
CREATE TABLE IF NOT EXISTS `People` (
    `id` INTEGER PRIMARY KEY AUTOINCREMENT,
    `firstName` VARCHAR(255) NOT NULL,
    `lastName` VARCHAR(255) NOT NULL
);
```
```sql
CREATE TABLE IF NOT EXISTS `Movies` (
    `id` INTEGER PRIMARY KEY AUTOINCREMENT,
    `title` VARCHAR(255) NOT NULL,
    `releaseYear` INTEGER NOT NULL,
    `PersonId` INTEGER REFERENCES `People` (`id`) ON DELETE SET NULL ON UPDATE CASCADE
);
```
The SQL for the People database table is unchanged from what it was before, but the SQL for the Movies database table now contains a PersonId foreign key column definition:

**Defining a One-to-One Association**
Now let's define the relationship from the "one" side, by adding a one-to-one association to the Movie model.
```javascript
 Movie.associate = (models) => {
    // one-to-one association
    Movie.belongsTo(models.Person);
  };
```
#### Refine Sequelize Associations
We've defined our first data relationship using Sequelize associations. Great! Unfortunately, our current approach has the following issues:

* The Movie table PersonId foreign key column name doesn't match the column naming convention of the other table columns (i.e., id, title, releaseYear) nor does it convey anything about the relationship of a person to a movie.
* The PersonId foreign key column currently allows null values, so a movie isn't required to have a director set.

Sequelize provides various association options that we can use to fix these shortcomings.

**Customize the foreign key name**
```javascript
 Movie.associate = (models) => {
    // one-to-one association
    Movie.belongsTo(models.Person, { foreignKey: 'directorPersonId'});
  };

```
```javascript
  Person.associate = (models) => {
    // one-to-many associations between Person and Movie model
    Person.hasMany(models.Movie, { foreignKey: 'directorPersonId' });
  };

```
Notice that we're updating both sides of the relationship with the same options. You must keep the foreign key configuration in sync across the Movie and Person models, or Sequelize will not be able to understand that the associations describe the same data relationship! Not keeping the options in sync will (typically) result in a duplicate foreign key column being added.

**Configure the Nullability of the Foreign Key Column**
To configure the nullability of the foreign key column (i.e., whether or not you can set the column to null), we can use the foreignKey property on the options object that's passed to the belongsTo() and hasMany() method calls.
```javascript
  Movie.associate = (models) => {
    // one-to-one association
    Movie.belongsTo(models.Person, { 
      foreignKey: {
        fieldName: 'directorPersonId',
        allowNull: false,
      }, 
    });
  };
```

### Create Related Data Using Sequelize Models
#### Create Reladted Movie and Person Data
Now it's time to start creating related data using our Movie and Person models.

To set a director on a Movie record, we first need to create the Person records. This is necessary because each Person model instance id value must be available before attempting to set the Movie model directorPersonId foreign key property.

At the top of the app.js file, we declare the Person and Movie variables and initialize them to the individual Person and Movie models available on the models object:
```javascript
'use strict';

const { sequelize, models } = require('./db');

// Get references to our models.
const { Person, Movie } = models;
```
**Notice**: Declaring a variable for each record is impractical when seeding the database with a large number of records. A more robust solution would use a query to retrieve records from the database before creating any related records. We're using this example only for this course.

#### Populate the Database with Seed Data
We'll start with populating the People database table with five records.
1. Create a person record. Call the Person model create() method, passing in an object literal with the desired property values. 
The create() method returns a promise that when fulfilled, gives us access to the Person model instance for Brad Bird. There are five records to create, so we call the create() method a total of five times.
2. Use the Promise all() method to wait until all five promises have been fulfilled. Store the aggregate promise in the variable peopleInstances:
```JavaScript
const peopleInstances = await Promise.all([
      Person.create({
        firstName: 'Brad',
        lastName: 'Bird',
      }),
      Person.create({
        firstName: 'Vin',
        lastName: 'Diesel',
      }),

```
await Promise.all() returns a resolved promise containing all of the Person model instances we just created (in an array), which is stored in the peopleInstances variable.
3. Use a combination of the console.log() and JSON.stringify() methods to log the data stored in peopleInstances to the console as a JSON string:

**Note**: The JSON stringify() method defines two optional parameters after the first value parameter. We're passing a numeric value of 2 for the second optional parameter—the space parameter—in order to indicate how many space characters should be used for whitespace.

4. Use Array destructuring to pluck the individual Person model instances from the peopleInstances variable (which is an array of values returned from the Promise all() method call):
```javascript
 console.log(JSON.stringify(peopleInstances, null, 2));
  
    // Update the global variables for the people instances
    [bradBird, vinDiesel, eliMarienthal, craigTNelson, hollyHunter] = peopleInstances;
```
[Database Seeding](https://en.wikipedia.org/wiki/Database_seeding#:%7E:text=Seeding%20a%20database%20is%20a,initial%20setup%20of%20an%20application.)
[Creating an Instance](https://sequelize.org/docs/v6/core-concepts/model-instances/#creating-an-instance)

#### Create a Movie Record
```javascript
try {
  // Code removed for brevity's sake...

  // Add Movies to the Database
  console.log('Adding movies to the database...');
  const movieInstances = await Promise.all([ 
    // Movie instances
  ]);
  console.log(JSON.stringify(movieInstances, null, 2));

  // Retrieve movies
  const movies = await Movie.findAll();
  console.log(movies.map(movie => movie.get({ plain: true })));

  // Retrieve people
  const people = await Person.findAll();
  console.log(people.map(person => person.get({ plain: true })));

  process.exit();

} catch(error) {
  ...
}
```
When converting an instance or collection of instances to JSON, calling .get({ plain: true}) returns the same as calling .toJSON() – a plain object with just the model attributes and values.

**Set a Movie's Director**
In our models, we used the foreignKey property to specify the foreign key name directorPersonId.

1. Set a movie's director by adding a directorPersonId property within the object passed to Movie.create(). The directorPersonId value needs to be set to a Person model instance id property value. For example, Brad Bird is the director for The Iron Giant, so set the directorPersonId property to the bradBird.id property value:
```javascript
console.log('Adding movies to the database...');
const movieInstances = await Promise.all([ 
  Movie.create({
    title: 'The Iron Giant',
    releaseYear: 1999,
    directorPersonId: bradBird.id,
  }),
  ...
]);
```
You might recall that the Movie model defines only three properties or attributes—id, title, and releaseYear:
If we're defining only those three properties, how does Sequelize add the directorPersonId property to the Movie model? Sequelize adds it to the model because of the association that's defined between the Movie and Person models:
[Logging Instances](https://sequelize.org/docs/v6/core-concepts/model-instances/#note--logging-instances)
[Shirtcut to Create Method](https://sequelize.org/docs/v6/core-concepts/model-instances/#a-very-useful-shortcut--the--code-create--code--method)

### Retrieve Related Data in Sequelize Queries
#### Retrieve Data with findAll()
Towards the end of the try block in the app.js file, we use the Movie findAll() method to retrieve the movie and person data from the database:
```javascript
try {
  // Code removed for brevity's sake...

  // Retrieve movies
  const movies = await Movie.findAll();
  console.log(movies.map(movie => movie.get({ plain: true })));

  // Retrieve people
  ...

  process.exit();

} catch(error) {
  ...
}
```
The `process.exit()` method instructs Node.js to terminate the process (or program) immediately.
When we call the Movie findAll() method, Sequelize generates and executes the following SQL SELECT statement:
```sql
SELECT `id`, `title`, `releaseYear`, `directorPersonId` FROM `Movies` AS `Movie`;
```
The data returned from the database looks like this:
```javascript
[
  {
    "id": 1,
    "title": "The Iron Giant",
    "releaseYear": 1999,
    "directorPersonId": 1
  },
  {
    "id": 2,
    "title": "The Incredibles",
    "releaseYear": 2004,
    "directorPersonId": 1
  }
]
```
As you can see from the above SQL statement and retrieved data, the Movie findAll() method is targeting the Movies table only. Because of this, the only information that we have about a movie's director is its directorPersonId value—the primary key value for the director's row in the People table.

On its own, this isn't very useful information to have. We could use the primary key value to retrieve the director's row from the People table, but that'd require another database operation. Luckily, Sequelize gives us a way to retrieve related data via a single query method call.

**Use the Sequelize `include` Query Option**
When calling the Movie findAll() method, we can pass an options object literal to configure the query. One of the available options—specified using the include property—allows us to indicate that we want any related Person model data.
1. Within the options object literal, add an include property and set it to an array of objects – one object literal for each related model that we want to include:
```javascript
...
// Retrieve movies
const movies = await Movie.findAll({
  include: [
    {
      model: Person,
    },
  ],
});
console.log(movies.map(movie => movie.get({ plain: true }
```
There's currently only one model associated with the Movie model—the Person model—so the array only has one object.
2. Run the app with the npm start. Now when we call the Movie findAll() method with the include option, Sequelize generates and executes the following SQL SELECT statement:
```sql
SELECT `Movie`.`id`, `Movie`.`title`, `Movie`.`releaseYear`, `Movie`.`directorPersonId`, `Person`.`id` AS `Person.id`, `Person`.`firstName` AS `Person.firstName`, `Person`.`lastName` AS `Person.lastName`
FROM `Movies` AS `Movie`
  LEFT OUTER JOIN `People` AS `Person`
  ON `Movie`.`directorPersonId` = `Person`.`id`;

```
```javascript
[
  {
    "id": 1,
    "title": "The Iron Giant",
    "releaseYear": 1999,
    "directorPersonId": 1,
    "Person": {
      "id": 1,
      "firstName": "Brad",
      "lastName": "Bird"
    }
  },
  ...
```
[Model Querying Basics](https://sequelize.org/docs/v6/core-concepts/model-querying-basics/)
[Fetching al Associated Elements](https://sequelize.org/docs/v6/advanced-association-concepts/eager-loading/#fetching-all-associated-elements)

#### Customized the Associated Model Property Name
The Person property in the retrieved movie data doesn’t convey anything about the relationship of a person to a movie:

This makes it difficult to understand that the person is the movie's director. The Person property also doesn't match the property naming convention of the other model properties (i.e. id, title, releaseYear, directorPersonId). This increases the chance that clients will introduce capitalization related bugs into their code.

To address these shortcomings, we’ll provide an alias for the model association and include that alias in our query method options.
1. Open the db/models/movie.js file. Create an alias for the model association by adding an as property to the belongsTo() method options object literal:
```javascript
Movie.associate = (models) => {
  Movie.belongsTo(models.Person, {
    as: 'director', // alias
    foreignKey: {
      fieldName: 'directorPersonId',
      allowNull: false,
    },
  });
};
```
The value of the as property is the alias that we want to use for this association. Let's also keep the Person model association in sync with the Movie model association.
2. Open the db/models/person.js file. Add an as property to the hasMany() method options object literal and set its value to 'director':
```javascript
Person.associate = (models) => {
  Person.hasMany(models.Movie, {
    as: 'director', // alias
    foreignKey: {
      fieldName: 'directorPersonId',
      allowNull: false,
    },
  });
};
```
3. Back in the app.js file, update the Movie.findAll() method include option with the same as alias property:
```javascript
const movies = await Movie.findAll({
  include: [
    {
      model: Person,
      as: 'director',
    },
  ],
});
console.log(movies.map(movie => movie.get({ plain: true }
```

#### Take Full Advantage of Your Model Associations
Earlier, you learned that defining a data relationship from both models' point of view gives you flexibility in retrieving data from the database. Let's see that in action by updating our Person findAll() method call to include any related Movie model data.

1. In the app.js file, update the Person findAll() method call by passing in an options object literal with an include property to indicate that we want any related Movie model data:
```javascript
// Retrieve people
const people = await Person.findAll({
  include: [
    {
      model: Movie,
      as: 'director',
    },
  ],
});
console.log(JSON.stringify(people, null, 2));
```

## REST API Validation with Express <a name="rest-api-validation-with-express"></a>
### The Importance of Data Validation
#### What is Data Validation
When we develop REST APIs that allow users to create or update data, we're establishing a relationship with our users.

Regardless of how well we know or trust our users, users often want to do the right thing when creating and updating data. Sometimes though, knowing what the "right" thing is can be challenging to determine. And in rare circumstances, users might try to do something that's unexpected or unwanted—or even worse, harmful.

As developers, we should strive to create applications that ensure that data created and updated by our users is useful.

We want our application's data to be useful—or said another way, to be "high quality" data. To do that, we need to validate the data that users submit to our REST APIs.

When developing full stack web applications, we can validate data in the following places:

**Client**: For web applications, client-side validation typically means writing JavaScript that'll run in the browser to validate form data before submitting it to the server.

**Server**: Implementing server-side validation means writing code to validate data sent to a server via an HTTP request. You can do this using your chosen language and platform, such as Python and Django, or Ruby on Rails. Our application is built using Node.js and the Express web application framework, so we'll use JavaScript (again) to implement our server-side validation.

**Database**: Most databases provide ways to validate data as it's inserted or updated, but that will depend on which database platform you're using (i.e., MySQL, Postgres, SQL Server, etc.).

Also, it's not an either/or choice—it's best to validate data on the client, on the server, and (if possible) within the database. Validating data on the client ensures that users have the best possible experience by providing immediate feedback as they update form fields. Validating data on the server ensures that savvy users can't submit bad data by bypassing client-side validation. Validating data within the database ensures that another application (or a user who has the ability to access the database directly) can't persist bad data into the database.

#### Review the Routes
Our REST API contains two routes (formatted in the following way: HTTP METHOD Route Response HTTP Status Code):

* GET /api/users 200 - Returns a list of user accounts.
* POST /api/users 201 - Creates a new user account.

Open the app.js file. The router is imported from the routes module into the app.js file and added to the main application using the Express Application use() method:

```javascript
// Add routes.
app.use('/api', routes);

```
Notice that a path is passed to the use() method before passing in the router, so routes defined in the router will only be considered if the requested route starts with the /api path. This means that the complete path for the GET and POST user routes is /api/users.

**Review the Get Users Route**
Open the routes.js file. The GET `/api retrieves a list of user accounts and returns it as JSON:
```javascript
router.get('/users', (req, res) => {
  res.json(users);
});

```
The app will store users in the JavaScript Array declared near the top of the routes module. Using an array instead of a database keeps things as simple as possible for this course:

**Review the Create User Route**
The POST /api/users route (also defined in the routes.js file) creates a new user account:
```javascript
router.post('/users', (req, res) => {
  // Get the user from the request body.
  const user = req.body;

  // Add the user to the `users` array.
  users.push(user);

  // Set the status to 201 Created and end the response.
  res.status(201).end();
});
```
The Express Router post() method call registers a route handler to handle POST requests to the "/users" path. We retrieve new user data from the Express Request body property and push it into the users array in the route handler.
```javascript
// Get the user from the request body.
const user = req.body;

// Add the user to the `users` array.
users.push(user);
```
Lastly, we use the status() method to set the status to 201 Created, followed by a call to the end() method to end the response:
```javascript
// Set the status to 201 Created and end the response.
return res.status(201).end();
```
#### Test the Create User Route
To test creating a new user account using the POST /api/users route, start the application by running npm start from the command line, open Postman, and complete the following steps:

1. Select the "POST" HTTP method in the drop-down list to the left of the URL field.
2. Change the URL to "http://localhost:5000/api/users".
3. Switch to the "Body" tab, and select "raw" and "JSON (application/json) for the body format.
4. Provide body content similar to the following:

#### Further Testing the New User Account Route
Currently, if we supply name, we'll notice that currently we avoid supply any information and still get a 201 code, so now we can add the validation.

### Validating Data
#### Define Data Validation Requirements
In a software development project, a set of written requirements typically guides the development of the application.

The written requirements often describe the data that the application will use. If the app allows users to create data, the requirements will also describe how data should be validated to determine if that data meets the expectations for "high quality" data.

**Validate Data in a Request Handler**
We need name and email values to create a new user account per our requirements. The name and email values are known as "required values". To ensure that new users have those values, we'll implement "required" value (or field) validation rules.

**Write Our First Required Validation Rule**
We create new users by sending an HTTP request to the POST /api/users route, so we'll implement our required validation rules by adding code to the route's request handler.

We'll add our validation rules just after the user variable declaration and initialization. That'll give us access to the request body (via the user variable) within our validation rule code. Also, if there's a problem with the request data, we'll prevent adding the user to the users array and return any validation errors to the client.

2. Before writing our first validation rule, let's declare and initialize a variable for an array of error messages.
3. Write the first validation rule by adding a conditional statement that checks if the user.name property has a value by checking the following:
- The name property exists on the user object
- The name property isn't set to undefined, null, or an empty string ('')

If the name property doesn't exist on the user object, then attempting to access that property will return undefined
undefined, null, and an empty string are all "falsy" in JavaScript
The logical NOT operator (!) flips a "falsy" value to "truthy" so that the code in the if statement's code block will execute
If the if statement's condition is met, push an error message into the errors array
```javascript
router.post('/users', (req, res) => {
  // Get the user from the request body.
  const user = req.body;

  const errors = [];

  // Validate that we have a `name` value.
  if (!user.name) {
    errors.push('Please provide a value for "name"');
  }

  // Add the user to the `users` array.
  users.push(user);

  // Set the status to 201 Created and end the response.
  res.status(201).end();
});
```

#### Return Validation Error Messages
If the errors array contains any elements (indicating that one of our validation rules failed) let's return a response with a 400 Bad Request HTTP status code along with the errors.
1. In route.js, add the if statement shown below to the POST /api/users route handler:
```javascript
// Validate that we have a `name` value.
if (!user.name) { ... }

// Validate that we have an `email` value.
if (!user.email) { ... }

// If there are any errors...
if (errors.length > 0) {
  // Return the validation errors to the client.
  res.status(400).json({ errors });
} 
```
**Note**: The object literal that's passed to the Express Response object `json()` method is using the [ES2015 object initializer shorthand syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#property_definitions). You can use this syntax as long as the property and variable names are the same.

2. Next, move the code that pushes the user into the users array and returns a 201 Created HTTP status code into an else clause. This code will execute only if there are no validation errors:
```javascript
if (errors.length > 0) {
  // Return the validation errors to the client.
  res.status(400).json({ errors });
} else {
  // Add the user to the `users` array.
  users.push(user);

  // Set the status to 201 Created and end the response.
  res.status(201).end();
}
```
#### Test Validation Rules in Postman
Let's test our POST /api/users route validation rules! Start the application by running npm start from the command line, open Postman, and complete the following steps:
Select the "POST" HTTP method in the drop-down list to the left of the URL field.
Change the URL to "http://localhost:5000/api/users".
Switch to the "Body" tab, and select "raw" and "JSON (application/json) for the body format.
Provide the following body content:
```javascript
{}
```
5. Click the "send" button

If you set up the validation rules correctly, you'll receive a 400 Bad Request HTTP status code back from the server, meaning that it did not create the user. The response body will also contain a JSON formatted list of validation errors

#### Format Validation Error Messages
There's no standard format for REST API validation errors, so you're free to choose a format that suits your application's needs. Whatever format you use, it's important to be consistent so that clients can reliably parse and display validation errors returned by your REST API.

**Consider your Audience**
It's also worth considering your audience: are your validation error messages meant to be read by a developer (who's using your REST API) or by an end-user (who uses an application that's using your REST API)? If it's a developer, it's generally okay to display technically worded messages. If it's an end-user, you'll want to make your messages friendlier and avoid anything that only a developer would understand.

In some situations, it might be both developers and end-users who need to read your messages! If that's the case, you can provide separate messages as shown below:
```javascript
{
  "errors": {
    "name": [
      {
        "message": "The request body must contain a \"name\" field set to the user's name",
        "userMessage": "Please provide a value for \"name\""
      }
    ],
    "email": [
      {
        "message": "The request body must contain a \"email\" field set to the user's email address",
        "userMessage": "Please provide a value for \"email\""
      }
    ]
  }
}
```
Again, the possibilities are endless. Research, experiment, and choose a format, but remember to be consistent.

#### Explore Data Validation Types
Required value validation rules only scratch the surface of what's possible with data validation. Other common validation types include:

* Data type validation
* Range and constraint validation
* Consistency check validation

**Data Type Validation**
Sometimes string values need to be converted to another data type. For example, numbers or dates that are sent to the server via the request body as strings. Data type validation rules ensure that you can successfully convert string values to the expected data type before attempting the conversion.

**Range and Constraint Validation**
Range validation rules ensure that values fall within an expected range. For example, does a password contain at least eight characters but no more than 20 characters? Does the user's age fall between 16 and 120 years?

Constraint validation rules check that values match an expected pattern. For example, does a provided value match the expected pattern for an email address, phone number, credit card number, or URL? Developers often use regular expressions to implement constraint validation rules.

**Consistency Check Validation**
Consistency check validation rules validate that values are logically consistent when compared with other values. For example, does the start date for a course come before the end date? Does a user's password match their password confirmation?

**Other Validation Types**
Validation rules sometimes need to perform operations that involve systems or APIs outside of your application to determine if a value is valid. For example, while a constraint validation rule can validate that a string value matches the expected pattern for an email address, it can't determine if you can successfully deliver an email to that address. Other examples include using external or third party APIs to validate credit card numbers or physical location addresses.

#### Next Steps: Expamd Data Validation Requirements
Now that you've learned about some additional validation types let's expand the data validation requirements for creating new user accounts by requiring a password.
1. In your POST /api/users route request handler, add an if statement that checks for a missing password value
2. Restart your application by running ctrl-C then npm start. Test your changes in Postman by selecting the "POST" HTTP method and providing body content similar to the following:
```javascript
{
  "name": "Anwar Montasir",
  "email": "anwar@testing.com",
  "password": "abc123"
}

```
**Hash User Passwords**
To protect our users' security, we shouldn't store user passwords in "plain" text—text that's not hashed or encrypted. Anyone with access to the data store (typically the application's underlying database) could write a query to retrieve a list of users and access each user's password.

You'll learn more about protecting user passwords before storing them in a database with a technique called "hashing" in a later course (and comparing an unhashed password to a hashed password). To wrap up this course, we'll use the bcrypt npm package to hash user passwords before saving them to the users array.

1. The bcrypt package is already included in your project. Start by importing the bcrypt module at the top of routes.js
```javascript
const bcrypt = require('bcrypt');
```
2. In your /api/users post route handler, add an else clause to the password validation. Use bcrypt's hashSync() method to hash the user's password before adding the user to the users array, as shown below:
```javascript
  // Validate that we have a `password` value.
  if (!user.password) {
    errors.push('Please provide a value for "password"');
  } else {
    user.password = bcrypt.hashSync(user.password, 10);
  }
```
3. Restart your application by running ctrl-C then npm start. Test that the password hashing worked by creating a new user.

A hash is a fixed-length value generated from a value of any length using a hashing function—an algorithm that mathematically transforms a value into a jumble of characters. For example, a hash of the password "abc123" might look like:
```
$2b$10$GXkppqnLNvFwTWr9nuN2Kui2.37nCGiEMaX1QVg6NbEHCdpThTC7e
```
The second value passed to bcrypt.hashSync() is the number of "salt rounds" used to hash the password – in this case, 10 rounds. You can learn more about salt rounds in the "Resources" section of this page.

**Using a Data Validation Library**
When possible, we should avoid writing code that we don't need to write. Using a library can help make applications quicker to develop, more reliable, and easier to maintain. [Review this (optional) instruction step](https://teamtreehouse.com/library/using-a-data-validation-library) to learn how to use the express-validator library to validate input and report any errors before creating a user.

**Validating Data Using an Object-Relational Mapping Library**
If you're using an ORM library like Sequelize, you can take advantage of its built-in data validation capabilities instead of using a validation library like express-validator.
[A note about rounds](https://www.npmjs.com/package/bcrypt#a-note-on-rounds)
[What are Salt rounds](https://stackoverflow.com/questions/46693430/what-are-salt-rounds-and-how-are-salts-stored-in-bcrypt)

## Sequelize Model Validation <a name="sequelize-model-validation"></a>
#### Introducing the Project
Sequelize can run validation on a model to require specific values and define constrains to prevent incorrect, unexpected or potentially harmful data from being recorded into the database.
We'll continue to use Sequelize to wirte robust server side data validation for a REST API developed with Express.

#### Set Validations for a Model
Let's begin setting up validations and constrains for the user model to prevent invalid data from being entered into the database

User Model
```javascript
module.exports = (sequelize) => {
  class User extends Model {}
  User.init({
    name: {
      type: DataTypes.STRING,
      allowNull: false
    },
    email: {
      type: DataTypes.STRING,
      allowNull: false    
    },
```
Also since the Sequelize Validator returns a lot of information we're going to tailor it to provide more user friendly messages, inside our route handler
```javascript
// Route that creates a new user.
router.post('/users', asyncHandler(async (req, res) => {
  try {
    await User.create(req.body);
    res.status(201).json({ "message": "Account successfully created!" });
  } catch (error) {
    console.log('ERROR: ', error.name);

    if (error.name === 'SequelizeValidationError' || error.name === 'SequelizeUniqueConstraintError') {
      const errors = error.errors.map(err => err.message);
      res.status(400).json({ errors });   
    } else {
      throw error;
    }
  }
}));
```

#### Validators and Customr Error Messages
Sequelize offers several built-in validators that allow you to specify validations for each attribute of the model as well as custom error messages. To being using them add the `validation` object
*Not NUll doesn't cover for empty or blank string
```javascript
module.exports = (sequelize) => {
  class User extends Model {}
  User.init({
    name: {
      type: DataTypes.STRING,
      allowNull: false,
      validate: {
        notNull: {
          msg: 'A name is required'
        },
        notEmpty: {
          msg: 'Please provide a name'
        }
      }
    },
    email: {
      type: DataTypes.STRING,
      allowNull: false,
      validate: {
        notNull: {
          msg: 'An email is required'
        },
        isEmail: { //isEmail is a special Sequelize validator for email
          msg: 'Please provide a valid email address'
        }
      }    
    },
    birthday: {
      type: DataTypes.DATEONLY,
      allowNull: false,
      validate: {
        notNull: {
          msg: 'A birthday is required'
        },
        notEmpty: {
          msg: 'Please provide a birthday'
        }
      }
    },
    password: {
      type: DataTypes.STRING,
      allowNull: false,
      validate: {
        notNull: {
          msg: 'A password is required'
        },
        notEmpty: {
          msg: 'Please provide a password'
        }
      }
    }
  }, { sequelize });

  return User;
};
```
#### Set Unique Constrains
Let's continue by adding a constrain to our user model. By constrains, I mean rules for more in-depth checks perfomed at the SQL level versus at the sequelize level.

For example when a email is used a query is done to check that is a unique email in the database, and we can add custom errors
```javascript
email: {
      type: DataTypes.STRING,
      allowNull: false,
      unique: true,
      validate: {
        notNull: {
          msg: 'An email is required'
        },
        isEmail: { //isEmail is a special Sequelize validator for email
          msg: 'Please provide a valid email address'
        }
      }    
    },
```
Or with a tailored message
```javascript
email: {
      type: DataTypes.STRING,
      allowNull: false,
      unique: {
        msg: 'The email you enter already exists'
      },
      validate: {
        notNull: {
          msg: 'An email is required'
        },
        isEmail: { //isEmail is a special Sequelize validator for email
          msg: 'Please provide a valid email address'
        }
      }    
    },
```

#### Date and Lenght Validators 
Now, we're going to use the `isDate` validator to check for validate strings for the birthday field and use the `len` or length validator to allow a password value only if it falls within a specific length or an expected range of characters
```javascript
 birthday: {
      type: DataTypes.DATEONLY,
      allowNull: false,
      validate: {
        notNull: {
          msg: 'A birthday is required'
        },
        isDate: {
          msg: 'Your birthday must be a valid date'
        }
      }
    },

```
When you set a validator to an object, you can pass values or arguments to it
via an `args` property, in this case, we'll use it to pass an array to define a range of characters for the password
```javascript
 password: {
      type: DataTypes.STRING,
      allowNull: false,
      validate: {
        notNull: {
          msg: 'A password is required'
        },
        notEmpty: {
          msg: 'Please provide a password'
        },
        len: {
          args: [8, 20],
          msg: 'The password shold be between 8 and 20 characters in length'
        }
      }
    }
```
#### Password Confirmation and Hashing
The User model validation is almost complete. In this step, we'll write the validation for the user password confirmation. This will be a required attribute (or field) that checks if its value matches the password field's value.

If the values match, we'll protect the password by hashing it with the bcrypt library before creating the database's new user record. If the values do not match, we'll display a validation error message.

**Add the Model Attribute**
1. In the file `user.js`, add a new attribute named `confirmedPassword` inside the `User.init({ })` object.
2. Set the `confirmedPassword` data type to `STRING` and disallow `null` values with `allowNull: false`.
```javascript
class User extends Model {}
User.init({ 
  name: { ... },
  email: { ... },
  birthday: { ... },
  password: { ... },
  confirmedPassword: { // new attribute
    type: DataTypes.STRING,
    allowNull: false,
  }
}, { sequelize });
```
**Compare passwords values**
Next, we'll compare passwords, hash the confirmed password if they match, and set the value to store in the database. Sequelize lets you define custom setters for model attributes with the set() function.

1. Add the set() function inside the confirmedPassword object. set() receives the value to set via a parameter. Name that parameter val:
```javascript
confirmedPassword: {
  type: DataTypes.STRING,
  allowNull: false,
  set(val) {

  }
}
```
`val` represents the value being set for confirmedPassword.
2. Inside the setter, check if the confirmedPassword value matches the value of password:
```javascript
confirmedPassword: {
  type: DataTypes.STRING,
  allowNull: false,
  set(val) {
    if ( val === this.password ) {

    }
  }
}
```
If the values match, we'll hash (or protect) the confirmed password's value using bcrypt, a popular library that makes it simple to hash passwords. You can learn more about bcrypt and hashing in the instruction step resources.

3. The bcrypt package is already included in the project. Import the bcrypt module at the top of user.js:
4. In the setter function, if the values are the same, we will hash the confirmed password and assign it to the variable hashedPassword.
One way to hash a password with bcrypt is calling `bcrypt.hashSync()`.
5. `hashSync()` accepts two arguments: the value to hash and the number of "salt rounds" used to hash the password. Let's hash the value assigned to val using 10 salt rounds:

```javascript
set(val) {
  if (val === this.password) {
    const hashedPassword = bcrypt.hashSync(val, 10);
  }
}
```
n short, it will help encrypt the password mathematically by transforming the value into a jumble of characters.

**Set the password value to Store**
Now let's set the value of confirmedPassword to the hashed password.
1. Inside the if statement, call the setDataValue Sequelize method, which is used inside setters to update the underlying data value:
`setDataValue` accepts two arguments. The first argument is the key (or property) to set for the User model instance (or the record stored in the database). The second is the value to set for the given property.
2. Set the `confirmedPassword` value to the hashed password assigned to `hashedPassword`
Sequelize calls the setter automatically and hashes the confirmed password before sending data to the database. That way the database stores the hashed value only.
```javascript
set(val) {
  if (val === this.password) {
    const hashedPassword = bcrypt.hashSync(val, 10);
    this.setDataValue('confirmedPassword', hashedPassword);
  }
}
```
**Disallow a `null` value for `confirmedPassword`**
We've defined our setter function to set the value for `confirmedPassword`. However, if the passwords do not match, then the setDataValue method does not run and the SQL query will attempt to set the confirmedPassword value to null. In that case, the allowNull check throws a validation error.
Below the `set()` function, add a `validate` object and define a custom error message for `null` values, using the `notNull` validator:
```javascript
...
confirmedPassword: {
      type: DataTypes.STRING,
      allowNull: false,
      set(val) {
        if( val === this.password) {
          const hashedPassword = bcrypt.hashSync(val, 10);
          this.setDataValue('confirmedPassword', hashedPassword);
        }
      },
      validate: {
        notNull: {
          msg: 'Both passwords must match'
        }
      }
    }
  }, { sequelize });
```
**Virtual Fields**
If both passwords match, we'll only store the confirmed password in the database because that's the hashed password. We also don't want to store two password values for each user – we want to avoid any irrelevant or duplicate data.

Sequelize provides a VIRTUAL data type for defining "virtual fields". These are attributes of a Model that only Sequelize populates but don't actually exist or get inserted as a column into the SQL database table.

Set the password attribute's data type to VIRTUAL:
```javascript
class User extends Model {}
  User.init({
    ...
    password: {
      type: DataTypes.VIRTUAL, // set a virtual field
      allowNull: false,
      validate: {
        ...
      }
    },
    confirmedPassword: { ... }
  }, { sequelize });
```
That's it for password validation! You'll test all your latest updates using Postman
