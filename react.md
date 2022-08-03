# React
-----

Author: Sheila Anguiano

-----

# Table of Contents
1. [React Basics](#react)
2. [React Components](#components)
3. [Using Create React App](#create-react)
4. [Data Fetching in React](#fetch-react)
5. [React Router 4](#react-router)
6. [Deploy React App](#deploy-react-app)
7. [React Context API](#react-context-api)
8. [React Hooks](#hooks)
9. [React Authentication](#react-auth)

## React Basics <a name="react"></a>
### First Steps in React
#### Introducing React
React is a JavaScript library for building user interfaces.It introduces  a more efficent and flexible way of building organizing and mantaining your user interface code (UI) code.

One of the main venefits of working with React, is that it lets you build your application's UI by breaking it up into small reusable pieces of code called **components**

The other big benefit is that React leeps your application's data or state and UI in-sync and can efficiently update your UI when data changes.

#### Add React to a Project
There is two common ways to install and get set up with React:
* Create React App
* CDN

Create React App was built by developers at Facebook to help save you from the time consuming setup amd configuration that building a react application normally requires.There acan be a lot of moving parts, from third party libraries, to loats of configurations and built tools

When building web applicatios in React, you use two libraries:
* React
* React-dom

#### Create a React Element
At it's core, React is on;ly a library for creating and updating HTML elements in your UI, 

At its simplest, React is a library for creating and updating HTML elements. So to better understand how React creates UI, we're going to begin using the React API to create React elements, which are the smallest building blocks

`.createElement()` accepts three arguments that define the element you want to create:
1. The type of element you want to create (string)
2. An object containing any attribute and value you want to give the element
3. Contents or children of the element you're creating
```javascript
const title = React.createElement(
	'h1',
	//If you're not passing anything, you can write an empty object {} or write 'null'
	{ id: 'main-title', title: 'This is a title'},
	'My first react element'
)
```
Now, one of the first important details of React is that React DOES NOT create actual DOM nodes, is actually and OBJECT that describes a DOM node. It's an object representation of a DOM node

#### Render an Element
The React DOM library provides DOM specific methods, such as `ReactDOM.render()` to render React elements to the DOM. This is the function that actially does the creating and updating of the DOM, is what connect React to the DOM. It accepts two arguments:
1. The react element or JavaScript object that describes the element you'd like to render and the actual HTML element you want to update or render to
2. The container element where our code will be rendered by React

```javascript
const title = React.createElement(
	'h1',
	{ id: 'main-title', title: 'This is a title'},
	'My first react element'
);

ReactDOM.render(
	title,
	document.getElementById('root')
);

```
This `root` element (which can be named anuthing) is where we'll be mounting our react application.
Any existing DOM elements inside the root will be replaced when render is called. Now we can **compose**

```javascript
const title = React.createElement(
	'h1',
	{ id: 'main-title', title: 'This is a title'},
	'My first react element'
);

const desc = React.createElement(
	'p',
	null,
	'I just learned to create a React node and render it'
);

const header = React.createElement(
	'header',
	null,
	title,
	desc
);


ReactDOM.render(
	header,
	document.getElementById('root')
);
```

#### Understanding JSX
**JSX** is a syntax extension to JavaScript that uses mark-up like syntax to describe elements in the UI
```javascript
const title = <h1>My First React Element!</h1>	
const desc = <p>I just learned to create a React node and render it</p>

const header = React.createElement(
	'header',
	null,
	title,
	desc
);

ReactDOM.render(
	header,
	document.getElementById('root')
);
```
Now if you want to see this in the browser, you'll get an error, because this needs to be transpiled into `React.createElement` calls. This is were we
re going to use the babel compiler by adding an html tag. This is going to allow us to use JSX without a built step.
We also need to add the `type` attribute to the `app.js` script tag for it to work. This signal to the babel script that the JavaScript at app.js should be compiled before being executed. 

Just remember that in production your code would probably be already be precompiled using babel using a tool like webpack before serving it to the browser.
 
```html
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
<script type="text/babel" src="./app.js"></script>
```

#### Embed JavaScript expressions in JSX
JSX tags can contain children, or nested elements. *While isn't required is a good code style practice to surround with parentheses JSX that is more two lines of code.
```javascript
const header = (
	<header>
		<h1>My first react Element!</h1>
		 <p>I just learned to create a React node and render it</p>
	</header>
);

ReactDOM.render(
	header,
	document.getElementById('root')
);

```
Now since JSX is an extension of the JavaScript language, you can use curly brances to write JavaScript expression, making JSX more dynamic. When you use curly braces in JSX, it's called a **JSX expression** and it can be placed between JSX tags or as value of an attribute in the JSX tag
```javascript
const title = 'My First React Element!';	
const desc = 'I just learned to create a React node and render it';
const myTitleID = 'main-title';

const header = (
	<header>
		<h1 id={ myTitleID }>{ title }</h1>
		 <p>{ desc }</p>
	</header>
);

ReactDOM.render(
	header,
	document.getElementById('root')
);

```
Now there are some rules or conventions to remember about JSX and React:
* Attribute names: React uses a camel case property naming convention
*Comments in JSX are different from comments in JavaScript, you need to put them inside curly brances `{/*This is a JSX comment */}`


### Thinking in Components
#### What's a Component
A component is a piece of UI that you can reuse. Being able to split your UI code into independent reusable pieces and think about each puece in isolation is one of the most embraced features of React.
#### Create a Component
Create a React component is a 2 step process
1. Define the component as a function or a class
2. Display the component with a JSX tag

The easies way to define a component is to write a Javascript function
React components are required to beging with an upper case letter as it helps to know a functions is defining a component

```javaScript
{/* The react component Header is going to @return react elments describing what should appear on the screen using JSX

*/}
function Header(){
	return(
		<header>
			<h1>Scoreboard</h1>
			<span className="stats">Players : 1</span>
		</header>
	);
}
```
[Functional and Class Components](https://reactjs.org/docs/components-and-props.html#functional-and-class-components)
[Why use parenthesis on JavaScript return statements?](https://jamesknelson.com/javascript-return-parenthesis/)


#### Use a component with JSX
JSX let's you definr your own tags. A JSX tag cannot only represent an HTML element like an `h1` or `div`, it can also represent a user defined component. For example we can use the `Header` component as a `header` tag whenever we need it, that why upper case letter are important, to differentiate from normal html tags from react components.

You can use self closing tags if you don't have any more children tags to nest inside the component, like the example below.

A component JSX tah is also a function call to `React.createElement` under the hood.

```javaScript
function Header(){
	return(
		<header>
			<h1>Scoreboard</h1>
			<span className="stats">Players : 1</span>
		</header>
	);
}

ReactDOM.render(
	<Header />
	document.getElementById('root')
);

```
#### Components as Arrow Functions
You'll often see component defined as arrow functions. We'll convert our Header function declaration to an arrow function

```javaScript
{/*   Function Declaration  */}
function Header(){
	return(
		<header>
			<h1>Scoreboard</h1>
			<span className="stats">Players : 1</span>
		</header>
	);
}

```
```javaScript
{/*   Arrow Function Expression */}
const Header = () => {
	return(
		<header>
			<h1>Scoreboard</h1>
			<span className="stats">Players : 1</span>
		</header>
	);
}
```
If you're writing a simple function that just returns JSX, you can use an implicit return, and delete the curly braces
```javaScript
{/*   Arrow Function Expression with implicit return */}
const Header = () => (
		<header>
			<h1>Scoreboard</h1>
			<span className="stats">Players : 1</span>
		</header>
	);
```
Or you can even find them without even the parentheses, but that is up to you

```JavaScript
{/*   Arrow Function Expression with implicit return without parentheses */}
const Header = () => 
		<header>
			<h1>Scoreboard</h1>
			<span className="stats">Players : 1</span>
		</header>;
```
[Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

#### Create the Player Component
```javascript
const Player = () => {
	return(
		<div className="player">
			<span className="player-name">
				Sheila
			</span>

			<div className="counter">
				<button className="conter-action decrement"> - </button>
				<span className="counter-score">35</span>
				<button className="conter-action increment"> + </button>
			</div>
		</div>
	);
}

ReactDOM.render(
	<Player />
	document.getElementById('root')
);

```
#### Composing Components
Extract the counter component from the player one, to have 2 separate components. Now when a component has another component inside this is called **composition**
```javascript
const Player = () => {
	return(
		<div className="player">
			<span className="player-name">
				Sheila
			</span>

			<Counter />
		</div>
	);
}

const Counter = () => {
	return (
		<div className="counter">
			<button className="conter-action decrement"> - </button>
			<span className="counter-score">35</span>
			<button className="conter-action increment"> + </button>
		</div>

	);
}

const App = () => {
	return (
		<div className="scoreboard">
			<Header />
			{/* Player List */}
				<Player />

		</div>


	);
}

ReactDOM.render(
	<App />
	document.getElementById('root')
);

```
Typically, react applications have a single top level component that wraps the entire application and composes all the main components together. 

[Composing Components](https://reactjs.org/docs/components-and-props.html#composing-components)
[Extracting Components](https://reactjs.org/docs/components-and-props.html#extracting-components)
[How do you know what should be its own component?](https://reactjs.org/docs/thinking-in-react.html#step-1-break-the-ui-into-a-component-hierarchy)

#### React Developer Tools
[React Dev Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)


### Introducing Props
#### Setting and Using Props
**Props** A list of properties used to pass data to a component. Components are customized and made reusable with props.
- You pass props to a component via the component's JSX tag at the place where it's used
```JavaScript
{/* The header tag is used in the App component, so */}
const  App  =  ()  => {
  return (
	<div  className="scoreboard">
	  <Header  title="Scoreboard McScoreboard"  totalPlayers={1}  />
	  <Player  />
	</div>
  );
}
``` 
- It's a good practice to use camel case for prop names consisting of two or more words
- values other than a string should be placed between curly braces
- When you define a component using a function, the function gets one default argument from React, a props objects containing a list of props given to the component, you can use any name you want. but `props` is the most used.

**Using Props**
- Define the props in a component's JSX tag
- Enable the use of props in a component

[Components and Props](https://reactjs.org/docs/components-and-props.html)

### Components and Props
An important detail to remember about props is that they are "read only" (or immutable), which means that a component can only read the props given to it, never change them. The (parent) component higher in the tree owns and controls the property values.

That way you avoid unintended behavior (or side effects) in your components. Further, React components are similar to "pure" functions in JavaScript. They do not attempt to change their inputs, and always return the same result for the same inputs.

**Prop Tips**
- When a component has more than one prop, you'll often see them written on separate lines and indented
- You can omit the value of a prop when it's explicitly true
- Use double quotes (") when writing props. HTML attributes commonly use double quotes instead of single, so props mirror this convention

### Use Props to Create Reusable Components
You can think of props as what react components use to talk to each other and share information. Props pass data from a parent component down to a child component.

We'll set up the Player component to receive props and pass props down to the Counter component. This will make the Player component dynamic and reusable.
```JavaScript
const  Header  =  (props)  => {
	return (
		<header>
			<h1>{  props.title }</h1>
			<span  className="stats">Player: {  props.totalPlayers }			</span>
		</header>
	);
}

const  Player  =  (props)  => {
	return (
		<div  className="player">
			<span  className="player-name">
				{  props.name }
			</span>
			<Counter  score={props.score} /></div>
	);
}

const  Counter  =  (props)  => {
	return (
		<div  className="counter">
			<button  className="counter-action decrement"> - </button>
			<span  className="counter-score">{  props.score }</span>
			<button  className="counter-action increment"> + </button>
		</div>
	);
}

  
const  App  =  ()  => {
	return (
		<div  className="scoreboard">
			<Header
				title="Scoreboard"
				totalPlayers={1}
			/>
			
			{/* Players list */}
			<Player  name="Brisa"  score={100}/>
			<Player  name="Momo"  score={89}/>
			<Player  name="Nieve"  score={60}/>
		</div>
	)
}

ReactDOM.render(
	<App  />,
	document.getElementById('root')
	);
```
So this is where the concept of independent, self-contained, and reusable components begins to manifest itself. Components facilitate what's known as separation of concerns. That's the idea that each component in your UI should be responsible for one thing only, and shouldn't contain extra code that handles other things.

* Project Note: While there is not much information in the _Header_ componet, it allows our app component to be easier to read, reduces code complexity and improves maintainability.

### Iterating and Rendering with map()
  We currently have 4 hard coded players in our app. We'll built a loop to iterate over data to produce a list of elements.
  1) We'll convert or player list, into a Players array
  2) We'll pass this array as a prop in the `ReactDOM.render` method (as is the parent) and map through the array using curly brackets inside the component
```javascript
const  App  =  (props)  => {
	return (
		<div  className="scoreboard">
			<Header
				title="Scoreboard McScoreboard"
				totalPlayers={props.initialPlayers.length}
			/>
			
			{ props.initialPlayers.map( player =>
				<Player
					name=  {player.name}
					score=  {player.score}
				/>
				)
			}
		</div>
	);
}


```


[array.prototype.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 
[Rendering multiple components](https://reactjs.org/docs/lists-and-keys.html#rendering-multiple-components)
[JS array iteration methods](https://teamtreehouse.com/library/transform-array-items-with-map)

### Use Keys to keep track of elements.
React manages what gets rendered to the DOM. In order for this process to be fast and efficient, React needs a way to quickly know which items were changed, added, or removed. For this, React gives elements a special built-in prop named `key`. A **KEY** is a unique identifier that gives React a way to quickly and reliably identify an element in a list.

```JavaScript
const players = [
	{
		name:  "Guil",
		score:  50,
		id:  1
	},
	{
		name:  "Treasure",
		score:  85,
		id:  2
	},
	{
		name:  "Ashley",
		score:  95,
		id:  3
	},
	{
		name:  "James",
		score:  80,
		id:  4
	}
]

...
const  App  =  (props)  => {
	return (
		<div  className="scoreboard">
			<Header
				title="Scoreboard"
				totalPlayers={props.initialPlayers.length }
			/>
			{/* Players list */}
			{ props.initialPlayers.map ( player =>
			<Player
				name={ player.name }
				score={ player.score }
				key={ player.id.toString() }

			/>
			)}
		</div>
	)	
}
``` 
- React Docs recommend that we use a string as the key value
- If data come from an API there usually will be a unique ID for each item, that you could use for key values.- React Docs recommend that we use a string as the key value
- Not all react elements need a key prop. Pass a key prop anytime you're creating elements by iterating over an array of items that will be rearranged added or deleted in your UI. The key will help React identify which items were changed, added or removed from the DOM

React does not recommend using index for unique keys, because the index might not always uniquely identify elements. It's usually best to use a unique id.

According to React docs:
>We don’t recommend using indexes for keys if the order of items may change. This can negatively impact performance and may cause issues with component state. Check out Robin Pokorny’s article for an [in-depth explanation on the negative impacts of using an index as a key](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318). If you choose not to assign an explicit key to list items then React will default to using indexes as keys.

[Keys - React Docs](https://reactjs.org/docs/lists-and-keys.html#keys)

### Understanding State
In React, state stores information about a component that can change over time. State determines how a component renders and behaves, and is what makes components interactive, allowing them to update and react to changes by updating DOM elements.
#### What is State?
In React, "state" is the data you want to track in your app. State is what allows you to create components that are dynamic and interactive, and it's the only data that changes over time.

There are two ways data gets handle in react:
- props
- state

So far we built our applications using functions that take props and return react elements, but props are read-only or immutable. A component can only read the props given to it, never change them. For any data that's going to change, we have to use **_state_**

In react, state is the data you want to track in your app, state is what allows you to create components that are dynamic and interactive, and it's the only data that changes over time.

State is a regular JavaScript object with properties that define the pieces of data that change. State is what keeps your UI in sync with your data. As the data changes, different components of the app will update what they show to the user. Normally, in a regular javaScript application, the more data you have and the more spread out it is, the more complex the applications becomes to maintain and debug. So react provides a more convenient way to store and maintain your data with state, now this doesn't mean that you won't need props. Props still play a major role in your application, because data from state is distributed through props. Props are still how you get data into a component.

State is only available to components that are class components

[Adding Local State to a Class - React Docs](https://reactjs.org/docs/state-and-lifecycle.html#adding-local-state-to-a-class)
[Component State](https://reactjs.org/docs/faq-state.html)
[props vs state](https://github.com/uberVU/react-guide/blob/master/props-vs-state.md)

#### Create a Component as a Class
There are two ways to create a component in React:
- function
- class

So far, we defined our components with  functions in a style called **stateless functional components**. These components are only receiving input through props and rendering UI.

Class components offer a more powerful way to build components, because they're the only type of components that let you use state. 

Based on what we want `Counter` to do, we'll create a `class Counter` using the ES2015 class syntax that `extends React.Component` In JavaScript classes, the `extends` keyword is used to create a subclass, or child of another class, in this case, we're extending from React.Component which is part of React's API for component class definition. 

The only method you need to define in a class component is called `render()`

```JSX
class  Counter  extends  React.Component  {
	render(){
		return (
			<div  className="counter">
			<button  className="counter-action decrement"> - </button>
			<span  className="counter-score">{ props.score }</span>
			<button  className="counter-action increment"> + </button>
			</div>
		);
	}
}
```
You use a class component just like a functional component by including its JSX tag wherever you want to display it. However, there is one important change we need to make in the JSX expression. Instead of accessing props with `props.propname`, for example,  classes need to access props with `this.props.propsname`

Class components are not accessed though arguments like they are in functional components. Props are a property of the component itself. So `this` refers to the component instance.

 So when do you use a class versus a function. If the component is only receiving input through props and rendering UI, it's best to use a function or a stateless functional component. Now, when you want to add state, that's when you use a class component. However, you can also create stateless components as classes. One benefit of that approach is that if you ever need to convert the component from stateless to stateful, you'll already have a class define for it.


[React.Component](https://reactjs.org/docs/react-component.html)
[Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
[extends](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/extends)
[converting-a-function-to-a-class](https://reactjs.org/docs/state-and-lifecycle.html#converting-a-function-to-a-class)

#### Create a Stateful Component
Now, we'll create a stateful component by first defining an initial state inside the Counter class.

Since state is an object, you create an initialized state within a class inside the constructor method. Inside the constructor we'll call `super()` in order  to call the constructor of the component class we're extending, and this needs to be done before we can use the `this` keyword. Then to initialize our component state, we set off an object.
You must name this object **state**, otherwise this will not work.

```JSX
class  Counter  extends  React.Component  {
	constructor() {
		super()
		this.state = {
			score:  0
			}
		}
....
```
Next, let's remove the `score.prop`  to the Counter and Player components.

```JSX
const  Player  =  (props)  => {
	return (
		<div  className="player">
			<span  className="player-name">
			{ props.name }
			</span>
			<Counter  />
		</div>
		);
	}
```
```JSX
const  App  =  (props)  => {
	return (
		<div  className="scoreboard">
			<Header
				title="Scoreboard" totalPlayers={props.initialPlayers.length }
			/>
			{/* Players list */}
			{ props.initialPlayers.map ( player =>
				<Player
					name={ player.name }
					key={ player.id.toString() }
				/>
			)}
		</div>
	)
}
```
You access state in the similar way you access props. You can think of the render method in a class component as being a function of not just props, but props and state. In other words, if either props or state changes, React executes the render method to update what gets displayed to the user.

You can also initialize state inside a React component using the class property syntax:
```JSX
class  Counter  extends  React.Component  {
	state = {
		score:  0
	};
...
}	
```
This class property syntax is a feature of JavaScript that's currently not supported in all Browsers, but since we're using the Babel transpiller, we don't have to worry about browser support.



[constructor – MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor)
[super – MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super)
[Adding Local State to a Class](https://reactjs.org/docs/state-and-lifecycle.html#adding-local-state-to-a-class)
[Babel’s Transform Class Properties Plugin: How it Works and What it Means for your React Apps](https://medium.com/@jacobworrel/babels-transform-class-properties-plugin-how-it-works-and-what-it-means-for-your-react-apps-6983539ffc22)
[Is it better to define state in constructor or using property initializers?](https://stackoverflow.com/questions/37788342/is-it-better-to-define-state-in-constructor-or-using-property-initializers/37788410#37788410)

### Handling Events
In React, you UI changes from one state to another. And state is local to a component, meaning a component can maintain its own state, unlike props, which are read-only.

React events are similar to JavaScript events except that they're written inline and named using camelCase.
1. We'll create the function or event handler that updates our state using React's built-in set state method.
2. We'll give our buttons an `onClick`  React event that calls the event handler when clicked. You pass React events a JSX expression, using curly braces and the event handler that will get called when the specified event happens. Notice that we pass a reference to the method (without the parenthesis) otherwise the method will be called when the component mounts.

```JSX
class  Counter  extends  React.Component  {
	state = {
		score:  0
	};
  
	incrementScore() {
		console.log('Hi, from inside incrementScore!');
	}

	render(){
		return (
			<div  className="counter">
				<button  className="counter-action decrement"> - </button>
				<span  className="counter-score">{  this.state.score }</span>
				<button  className="counter-action increment"  onClick={this.incrementScore}  > + 
				</button>
			</div>
		);
	}
}
```

[Handling Events – React docs](https://reactjs.org/docs/handling-events.html)
[Passing Arguments to Event Handlers](https://reactjs.org/docs/handling-events.html#passing-arguments-to-event-handlers)
[Supported Events in React](https://reactjs.org/docs/events.html#supported-events)

#### Updating State
State is never modified directly. The only way React allows you to update a component state is by using its built-in set state method. React needs to be told when state changes and that it should re-render and make changes to the component, based on the change in state.

You pass `setState` an object that contains the part of the state you want to update.

```JavaScript
class Counter extends React.Component {
	state = {
		score:  0
	};
	
	incrementScore() {
		this.setState({
			score:  this.state.score +1
			});
		}
	}

render(){ ..
```
So to recap, `setSate` is going to do 2 things:
1. Update the value of the score state
2. It'll tell React that this component needs to be re-rendered to make sure that everything is up to date in the UI
3. If we run it like this, we'll notice that we lose the binding


[`setState()`](https://reactjs.org/docs/react-component.html#setstate)
[Using State Correctly](https://reactjs.org/docs/state-and-lifecycle.html#using-state-correctly)
[Understanding React  `setState`](https://css-tricks.com/understanding-react-setstate/)

### Bind Event Handlers to Components
In objects or classes, `this` usually refers to the parent that owns the method. When you create a class component that extends from `React.Component`, any custom methods you create are not bound to the component by default. You need to bind your custom methods, so that `this` refers to the component instance.

There are several ways to bind the thisContext in React. A common way is to call bind in the render method. In our example, each counter component that gets mounted into the DOM is an instance of the *Counter* class
```JSX
class  Counter  extends  React.Component  {
	state = {
		score:  0
	};
  
	incrementScore() {
		this.setState({
			score:  this.state.score +  1
		});
	}

	render(){
		return (
			<div  className="counter">
				<button  className="counter-action decrement"> - 					</button>
				<span  className="counter-score">{  this.state.score }</span>
				<button  className="counter-action increment"  onClick={this.incrementScore.bind(this)}  > + 
				</button>
			</div>
		);
	}
}
```
The other common way to bind event handlers is with an arrow function, where we don't even need to `.bind(this)`, because arrow functions use what's called a lexical `this` binding which means that automatically bind them to the scope in which they are defined.

```JSX
	...
				<button  className="counter-action increment"  onClick={() => this.incrementScore()}  > + 
				</button>
			</div>
		);
	}
}
```
We know that inside the render method,  `this`  refers to the counter component instance, the arrow function is enclosed inside the render method, so it takes on that same context and the `this` value inside it will properly point to the counter component instance

But the most common way to define an event handler in React is with an arrow function. We learned that arrow functions are automatically bound to the scope in which they're defined, so if we rewrite the `incrementScore` method as an arrow function, the function gets bound to the component instance, and we don't need to worry about binding it in the `onClick` event

```JSX
class  Counter  extends  React.Component  {
	state = {
		score:  0
	};
  
	incrementScore = () => {
		this.setState({
			score:  this.state.score +  1
		});
	}

	render(){
		return (
			<div  className="counter">
				<button  className="counter-action decrement"> - 					</button>
				<span  className="counter-score">{  this.state.score }</span>
				<button  className="counter-action increment"  onClick={this.incrementScore}  > + 
				</button>
			</div>
		);
	}
}
```
Another way is
```JSX
constructor() {
	 super(); this.state = { score: 0 }; this.incrementScore = 		this.incrementScore.bind(this); }

..
<button onClick={ this.incrementScore }> + </button>
```

[Handling Events – React docs](https://reactjs.org/docs/handling-events.html)
[Passing Functions to Components](https://reactjs.org/docs/faq-functions.html)
[This is why we need to bind event handlers in Class Components in React](https://medium.freecodecamp.org/this-is-why-we-need-to-bind-event-handlers-in-class-components-in-react-f7ea1a6f93eb)
[React — to Bind or Not to Bind](https://medium.com/shoutem/react-to-bind-or-not-to-bind-7bf58327e22a)

### Update State Based on Previous State
Whenever you need to update state based on previous state, you shouldn't rely on `this.state` to calculate the next state. State updates may be asynchronous, so it may not always lead to the component re-rendering with new data, and could cause state inconsistency. `setState()` accepts a callback function that produces state based on the previous state in a more reliable way.

```JSX
incrementScore  =  ()  => {
	this.setState( prevState => {
		return {
			score: prevState.score +  1
		};
	});
}

decrementScore  =  ()  => {
	this.setState({
		score:  this.state.score -  1
	});
}
```
Our program will work the same, but now we have a more reliable way to set state based on previous State, because the callback function is guaranteed to fire after the update is applied and rendered out to the DOM.
You can also make the callback more concise:
```JSX
incrementScore  =  ()  => {
	this.setState( prevState => ({
	score: prevState.score +  1
	}));
}
```
So, whenever you're updating to a new state based on a previous state, it's actively recommended that you use this approach.

[`setState()`](https://reactjs.org/docs/react-component.html#setstate)
[State Updates May Be Asynchronous](https://reactjs.org/docs/state-and-lifecycle.html#state-updates-may-be-asynchronous)
[State Updates are Merged](https://reactjs.org/docs/state-and-lifecycle.html#state-updates-are-merged)
[Why doesn’t React update this.state synchronously?](https://reactjs.org/docs/faq-state.html#why-doesnt-react-update-thisstate-synchronously)

### Creating the Application State
We'e going to learn how to remove items from state. We'll initialize a player state in the app component, then create and wire up and even handler that removes a player on click.

Since the app component is responsible for rendering the player component, it's going to own and maintain the player state. The state will then be passed down and available to the player component as well as all children of App via props.

1. Make App a class component
2. Initialize State with the player list, without Scores, because they're already initialized on the Counter component
3. Change or map function to iterate trough the players array that now is located in state.

```javascript
class  App  extends  React.Component  {
  state = {
    players: [
		{
			name:  "Guil",
			id:  1
		},
		{
			name:  "Treasure",
			id:  2
		}
	]
};
  render() {
	return (
		<div  className="scoreboard">
		<Header
			title="Scoreboard McScoreboard"
			totalPlayers={this.state.players.length}
		/>
		{  this.state.players.map( player =>
			<Player
				name=  {player.name}
				key=  {player.id.toString()}
			/>
			)
		}
		</div>
		);
	}
}

ReactDOM.render(
	<App  />,
	document.getElementById('root')
);
```

One important concept to understand is the different types of state. There are two main types when designing a React App.
* Application State: Data that is available to the entire application, in our example, application state lives in the app component 
* Component State: State that is specific to a component and not shared outside of the component, this is usually referred as local component state

### Remove Items from State
We could use `.filter()`, but we want to avoid updating the state directly, therefore:
1. We'll create the remove player handler function as part of the Application state and add the props that we'll need for the child Player component.

```JavaScript
class  App  extends  React.Component  {
...
handleRemovePlayer  =  (id)  => {
	this.setState( prevState => {
		return {
			players: prevState.players.filter( p => p.id !== id )
		};
	});
}
...
render() {
	return (
		<div  className="scoreboard">
		<Header
			title="Scoreboard McScoreboard"
			totalPlayers={this.state.players.length}
		/>
		{  this.state.players.map( player =>
			<Player
				name=  {player.name}
				id={player.id}
				key=  {player.id.toString()}
				removePlayer={this.handleRemovePlayer}
			/>
		)
	}
</div>
);

}

```

2. Inside the Player component we add the `x` button, along with its functionality
```JavaScript
const  Player  =  ( props )  => {
	return (
		<div  className="player">
			<span  className  ="player-name">
				<button  className="remove-player"  onClick={  ()  => 	props.removePlayer(props.id)}>✖</button>
				{ props.name }
			</span>
			<Counter  />
		</div>
	)
}
```


[Constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor)
## React Components  <a name="components"></a>

### Build Modular Interfaces with Components
Developers normally use Create React App for developing react applications because it lets you quickly create and run React Apps with no configuration. It sets your development environment with tools like Babel to compile JSX to JavaScript and Webpack to process and bundle your JavaScript files and project assets. 

Create React App is well-suited for projects of any size and often used for developing production ready apps. 

With Create React App you run one command to set up the tools and files you need to start your React Project

`npx create-react-app nameOfProjectFolder`

`npx` is a tool that's included with **npm** as a version 5.2, that makes it easy to install and run packages, especially command-line tools like create-react-app. If you need to use a global package that's not installed on your computer, running `npx` will download and execute the package you specify all in one command.

Since we're using provided started files, we'll only run `npm install` followed by `npm start`

#### Using Create React App
Developers use compiling as part of a build process to avoid the overhead of downloading Babel and multiple JavaScript files to the client.  [Create React App](https://teamtreehouse.com/library/what-is-create-react-app)  sets up a modern build system for your React apps in little time, no need to install or configure tools like  [Webpack](https://webpack.js.org/)  or  [Babel](https://babeljs.io/). The tools are already pre-configured in each new project, that way you can focus on building your app.

To get started, install Create React App and create a new app, at all once, with  [npx](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b). For example:

```
npx create-react-app scoreboard 
cd scoreboard 
npm start
```

**What's in package.json?**  
When you create a project with Create React App, it installs the latest version of React and React-DOM, as well as the latest version of react-scripts, a development dependency that manages all other dev dependencies that run, test and build your app.

**Progressive Web App Features**  
Create React App sets up a fully functional, offline-first  [Progressive Web App](https://developers.google.com/web/progressive-web-apps/)  by default. However, we removed the  [PWA related files](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#making-a-progressive-web-app)  just for this project to focus on the React components only.

#### Separating Function Components into Modules
ES modules is a feature in JavaScript that lets you break up your code into individual JavaScript files. Modules provide a better way to organize and maintain your code, as well as provide scope for your variables, functions and classes.

The module system allows you to import and export entire modules or just parts of a module. Over time you'll find that putting all of your components and logic into one monolithic file can become difficult to manage.

In React, it's common to think of each component as an independent module. The first thing you'll usually do when creating a React component as a module is import React, since each module has its own scope

#### Separating Class Components Into Modules
When working with class components you'll often see the React import statement written like this: 
`import React, { Component } from 'react';`

This is called a **named import**, and with this named import statement, you can create a class without extending from `React.Component`, so you can re-write your classes:

* From: 	`class App extends React.Component` 

* To:  	`class App extends Component`

* [Import multiple exports from module – MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#Import_a_single_export_from_a_module)

* [ES modules: A cartoon deep-dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)

* [ES6 Modules in Depth](https://ponyfoo.com/articles/es6-modules-in-depth)

**Another way to export a class**
```
export default class Counter extends Component {
 render() { ... } } 
```
**Another way to export a function**
```
export const Counter = () => {
 return ( ... ); } 
```
Then import the function:
```
import { Counter } from './Counter';
```

### Managing State and Data Flow
It’s important to think carefully about where state resides in your application. In this stage, you will restructure state and data flow to be more unidirectional.
#### Unidirectional Data Flow
In React, data naturally flows down the component tree, from the app's top-level component down to the child components, via props. This is called "unidirectional data flow".

It's important to think carefully about where state resides in your application. For instance, if you have dozens of component, each maintaining their own state, building and maintaining your application can become really cumbersome. 

[The Data Flows Down – React docs](https://reactjs.org/docs/state-and-lifecycle.html#the-data-flows-down)

#### Lifting State Up
When two or more components need access to the same state, we move the state into their common parent. This is called "lifting state up".

In our scoreboard exercise the score state is gonna be managed as high up in the application as possible. 

Exercise explanation: 
1. We'll remove state from the `counter` module as well as the click events, reverting it to a stateless component that takes data from props
2. In the player component we'll pass the score to the counter with the prop `prop.score`
3. And in the App component we'll pass the score to player and initialize the score state in the players array and set it to 0 by default.


[Lifting State Up – React docs](https://reactjs.org/docs/lifting-state-up.html)

#### Communicating Between Components
Instead of  passing state to a child component, the parent can pass down a callback function. The callback will allow you to communicate events and changes in your data upwards, while data continues to flow downwards.

In order to design how data flows upward through our component tree, we need to think about each component and its responsibilities

>delta is the variation of a function in this case, the number the score should be changed by

```JavaScript
{/*Score handlers refactoring inside the App component*/}
handleScorechange =(delta)=> {
	}
/*And we'll give the player component a new prop. This callback is going to run at a later time through some interaction with a child component */
<Player 
..
changeScore = {this.handleScoreChange}
/>  
```
We'll pass the `handleScoreChange` function to the counter component with props, by first passing it to the player component, then supply to the counter component. A function will then be called inside the counter using an `onClick` event
```JSX
/*Player.js*/
const Player = (props) => {
  return (
    <div className="player">
    ...
    <Counter 
	    score={props.score
	    /*Adding the below props to the component,the function is ready to be invoked inside the counter component*/
	    changeScore={props.changeScore}	
	 />
  );
}
```
Finally we add the `onClick` event inside the Counter component
```JSX
const Counter =(props) => {
  return (
	<div clasName="counter">
		<button ClassName="counter-action decrement" onClick={() => props.changeScore(-1)}> - </button>
		<span className="counter-score">{props.score)}</span>
		<button ClassName="counter-action increment" onClick={() => props.changeScore(1)}> + </button>	
	</div>	
  );
}
```
[Callback functions in React](https://medium.com/@thejasonfile/callback-functions-in-react-e822ebede766)


#### Update State Based on a Player's Index
**Note** : While updating the `score` state of a player, you may have noticed that `prevState` references the same object as `this.state`

In the video, we used  `prevState`  in  `this.setState()`  to update a player's score based on the previous score. It turns out that  `prevState`  is in fact still a reference to the previous state object, and it should not be directly mutated.

A better way to update a specific player's score might be as follows:
```JSX
 handleScoreChange = (index, delta) => { 
	 this.setState( prevState => { 
		 // New 'players' array – a copy of the previous `players` state 		
		 const updatedPlayers = [ ...prevState.players ]; 
		 // A copy of the player object we're targeting 
		 const updatedPlayer = { ...updatedPlayers[index] };   

		// Update the target player's score 
		updatedPlayer.score += delta; 
		// Update the 'players' array with the target player's latest score 		
		updatedPlayers[index] = updatedPlayer;   
		// Update the `players` state without mutating the original state 
		return { players: updatedPlayers 
		}; 
	}); 
} 
```
This will build a new object based on the data from  `prevState`, which update a player's  `score`  state without mutating  `this.state`

This seems like the safest approach, especially when managing state across larger applications.

#### Building the Statistics Component
Now that our state has been lifted all the way up in our App, we can use it in any other component such as the following stateless functional component

```JSX
import React from ''react;

const Stats = (props) => {
  return (
    <table className="stats">
      <tbody> 
        <tr> 
          <td>Players:</td> <td>0</td> 
        </tr> 
        <tr> 
          <td>Total Points:</td> 
          <td>0</td> 
        </tr> 
      </tbody> 
    </table>
  );
}
```
Now we'll add the **Stats** into its parent component **Header** and delete the `span` element that was displaying that information, so in the **App** component we'll need to pass the player's state, so it can be use in Header

```JSX
class App extends Component {
...
....
  render() {
    return(
    <Header 
	  title="Scoreboard"
	  players={this.state.players}
	/>
    ):
  
  }
}

```
Now we need to pass the players to the stats component  
```JSX
const Header = (props) => {
  return (
	<header>
	  <Stats players={props.players} />
	</header>
  );
}
```
So now in the **Stats** component we can calculate the stats using plain JavaScript
```JSX
import React from ''react;

const Stats = (props) => {
  
  const totalPlayers = props.players.length;
  const totalPoints =props.players.reduce((total, player) => {
    return total + player.score;
    }, 0);
  
  return (
    <table className="stats">
      <tbody> 
        <tr> 
          <td>Players:</td> 
          <td>{ totalPlayers }</td> 
        </tr> 
        <tr> 
          <td>Total Points:</td> 
          <td>{ totalPoints }</td> 
        </tr> 
      </tbody> 
    </table>
  );
}
```


#### Controlled Components
In React, form elements work differently from other elements because form elements naturally keep some internal state. Input fields in html for example are typically considered stateful. When you type into a text field, you're changing it's state. The values update based on user input. In react, we need to handle a form element state explicitly.
```JSX
import React, { Component } from 'react';

class AddPlayerForm extends Component {
  render() {
    return(
      <form>
        <input
          type="text"
          placeholder="Enter a player's name"
        />
        <input
          type="submit"
          value="Add Player"
        />

      </form>
    
    );
  }
}

export default AddPlayerForm;
```
To manage our input field state, we'll need to build what's called a controlled component. A controlled component renders a form that controls what happens in that form on subsequence user input. In other words it's a form element whose value is controlled by react with state.

**Creating a Controlled Component for Input Element**
* Initialized state for the value of the input
* Listen for changes on the input to detect when value is updated
* Create an event handler that updates the value state

Setting the inputs value property to the state, ensures that the content in the text field is always in sync with the state, so 
1. We'll create the component state
2. We'll provide our input with React's built in `onChange` event. This event gets triggered immediately after each change, here we'll pass our event handler


```JSX
import React, { Component } from 'react';

class AddPlayerForm extends Component {
  
  state={
  value: ''
  };
  
  handleValueChange = (e) => {
    this.setState({ value: e.target.value });
 }

  render() {
    return(
    ...
  }
}

export default AddPlayerForm;
```

React uses a cross-browser wrapper around browser's native event called `syntheticEvent` so that the cross-browser differences of DOM events won't get in our way.

[Controlled Components](https://reactjs.org/docs/forms.html#controlled-components)
[Controlled vs. Uncontrolled Components](https://reactjs.org/docs/glossary.html#controlled-vs-uncontrolled-components)
[SyntheticEvent](https://reactjs.org/docs/events.html) 

#### Adding Items to State
Now, to let the user add players to the scoreboard using the form that we created. 

Currently, the AddPlayerForm component has no access to the player state maintained in the app component, and the AddPlayerForm component state is local state, meaning it's just state that's needed for the component to do its job and no other component has access to it.

First, we're going to create an event handler to allow users to submit the form, and then a function that will add the new player to state and display it on the board.

For this part, we'll create the `handleSubmit` arrow function which is going to be bind to an  `onSubmit` event inside the `<form>` tag. This event will execute the `handleSubmit` function as soon as the form is submitted by either clicking the submit button or pressing the enter or return key.

```JSX
import React, { Component } from 'react';

class AddPlayerForm extends Component {
  
  state={
  value: ''
  };
  
  handleValueChange = (e) => {
    this.setState({ value: e.target.value });
 }
 
 handleSubmit = (e) => {
   e.preventDefault(); // To prevent the browser deletes the submited info
   this.props.addPlayer(this.state.value);
 
}

  render() {
    return(
      <form onSubmit={this.handleSubmit}>
        <input
          type="text"
          placeholder="Enter a player's name"
        />
        <input
          type="submit"
          value="Add Player"
        />

      </form>
    
    );
  }
}

export default AddPlayerForm;
```
So in App.js we'll give the prop `addPlayer` to the AddPlayerForm component and pass it a function named `handleAddPlayer`

For the Id counter we'll initialize the `prevPlayerId` property and set to the id following the last one in our array. There are other ways we could create the id, for example creating a function that generates a unique id or declaring a `counter` variable outside of the class instead of a property on the class
```jsx
//player id counter property
prevPlayerId = 4;

handleAddPlayer = (name) => {
this.setState({
  players: [
    {
      name, // We can use this, instead of name: name using ES2015 shorthand
      score: 0,
      id:this.prevPlayerId +=1
    }
  ]
})
}
 
render() {
   return (
 ...
     <AddPlayerForm addPlayer={this.handleAddPlayer} 
```
Now, we need to bring in all the existing player objects in state and combine them with the new player object being added to state.We'll use the spread operator to bring in a copy of all the existing player objects.
```jsx
handleAddPlayer = (name) => {
this.setState({
  players: [
     ...this.state.players,
    {
      name, // We can use this, instead of name: name using ES2015 shorthand
      score: 0,
      id:this.prevPlayerId +=1
    }
```
Finally, we need the text field to clear once a user submits a name, so we'll return to the `handleSubmit` function
```jsx
handleSubmit  =  (e)  =>  { 
  e.preventDefault();
  this.propr.addPlayer(this.state.value);
  this.setState({value: ''});
 }
```

[Form Events](https://reactjs.org/docs/events.html#form-events)
[Spread syntax – MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
[Rest Parameters and Spread Operator](https://teamtreehouse.com/library/rest-parameters-and-spread-operator)

#### Update the Players State based on previous state
To reiterate, is usually a good idea to update to a new state based on the previous state, that way we can be sure that this.state always holds the correct updated state

```jsx
handleAddPlayer = (name) => {
this.setState(prevState => {
  return {
    players: [
     ...prevState.players,
      {
        name, // We can use this, instead of name: name using ES2015 shorthand
        score: 0,
        id:this.prevPlayerId +=1
	  }
    }
```
Another way is the `concat()` method, which is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.
```jsx
handleAddPlayer = (name) => {
 let newPlayer = { 
	name, 
	score: 0, 
	id: this.prevPlayerId += 1 
	}; 
	
	this.setState( prevState => ({ 
		players: prevState.players.concat(newPlayer) 
		})
	); 
}
```

* [`setState()`](https://reactjs.org/docs/react-component.html#setstate)
* [State Updates May Be Asynchronous](https://reactjs.org/docs/state-and-lifecycle.html#state-updates-may-be-asynchronous)
* [State Updates are Merged](https://reactjs.org/docs/state-and-lifecycle.html#state-updates-are-merged)
* [Why doesn’t React update this.state synchronously?](https://reactjs.org/docs/faq-state.html#why-doesnt-react-update-thisstate-synchronously)

### Stateful Components and Lifecycle Methods
#### Designing the Stopwatch
This stopwatch will be a stateful component that counts seconds, and allows user to start, stop and reset the time. We'll crate:
1. A button to stop and start the timer. If the time is stopped and started again, it'll continue from where it left off.
2. A reset button that will return the timer to 0

We'll start by building the stop watch component and its elements, then we'll use State to make the stopwatch timer run. and write function to let users start, stop and reset the stopwatch

Our stopwatch will require three pieces of state. A running state, an elapsed time state, and a previous time state to let us calculate how much time has passed. So we have to determine if this should be application state or components state. A case could be made for either, but in our app we have no need to the stopwatch state outside the stopwatch component, so this will be a component state., which mean thsi will be a stateful component 

```javascript
import React, from { Component }  from 'react";

class Stopwatch extends Component {
  render(){
    return (
      <div className="stopwatch">
        <h2>Stopwatch</h2> 
        <span className="stopwatch-time">0</span> 
        <button>Start</button> 
        <button>Reset</button> 
      </div>
    );
  }
}
export default Stopwatch;
```

#### Stopwatch State
The stopwatch will have two main states visible to the user. It will be either in a running state, or a stopped state. The buttons on the interface should change based on the running state. We'll start by initializing state in the `Stopwatch` component.

```javascript
import React, from {Component}  from 'react";

class Stopwatch extends Component {
  state= {
    isRunning: false 
  };
  handleStopwatch = () => {
    this.setState({
     isRunning: !this.state.isRunning
    });
  }
  
  render(){
    return (
      <div className="stopwatch">
        <h2>Stopwatch</h2> 
        <span className="stopwatch-time">0</span> 
        <button onClick={this.handleStopwatch}>
          { this.state.isRunning ? 'Stop' : 'Start' }
        </button> 
        <button>Reset</button> 
      </div>
    );
  }
}
export default Stopwatch;
```


* [Conditional (ternary) Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)
* [Conditional Rendering – React docs](https://reactjs.org/docs/conditional-rendering.html)
* [Inline If-Else with Conditional Operator](https://reactjs.org/docs/conditional-rendering.html#inline-if-else-with-conditional-operator)
* [Ternary Operator – Treehouse workshop](https://teamtreehouse.com/library/ternary-operator)

**Conditional rendering with  `if...else`:**
```JSX
render() {
	let button; 
	if (this.state.isRunning) { 
		 button = <button>Stop</button>; 
	} else { 
		button = <button>Start</button>; 
	}   

	return ( 
		<div className="stopwatch"> 
			<h2>Stopwatch</h2> 
			<span className="stopwatch-time">...</span> 
			{ button } 
			<button onClick={this.handleReset}>Reset</button> 
		</div> 
	); 
}
```

#### Update the Stopwatch State with componentDidMount()
Now, we'll create the tick function which is going to be the most essential piece of our stopwatch, wince the code that involves making the timer tick second after second.


##### Component Lifecycle
In React, every component instance follows a cycle: its mounted onto the DOM, it's updated with changes in data, and it's unmounted from the DOM. This is referred as the components lifecycle. 
##### React Lifecycle Methods
* Built-in lifecycle methods that get called at each point in the life cycle. 
* The lifecycle methods act as hooks you can run code at key times in your component's lifecycle
*  Gives you the ability to control what happens when a component mounts, updates and unmounts. 

The lifecycle method you'll likely use the most is called `componentDidMount()`. Usually, any custom method or function you write need to be called somewhere, like with an event or from inside another function for example. The `componentDidMount()` method gets called by React as soon as the component is inserted or mounted into the DOM, and because of this, is a convenient hook for setting up timers, fetching data, or anything else you might need to do when your component is mounted into the page. Lifecycle methods like this one are also referred as lifecycle hooks, because they let you hook into, or provide hooks to certain parts of a components lifecycle. 

Because `componentDidMount()` is immediately called after a component mounts it'a a convenient hook for setting up timers, fetching data, or anything else you might need to do when your component is mounted into the page.

We'll set up the timer with JS `setInterval()` method. This method repeatedly calls a function or executes some code with a fixed time delay between each call, it returns an internal ID which uniquely identifies the interval. A stopwatch usually consist of a counter that's always counting up, we're going to store that data in state with a property  called `elapsedTime`, this will represent the amount of time thats; passed by we'll initialize to 0.

In order to increase the count each time `tick` is called , we'll need to calculate the amount of time since the last tick and add it to the `elapsedTime`. Ideally, the interval should always be 100 milliseconds from tick to tick, but it's not always guaranteed, so instead, we should get the exact time at wihch the previous tick happened, and subtract the current time from that, which will give us a more accurate interval, and then we take that value and add it to elapsed time.

So first we'll initialize `previousTime` to 0. The `handleStopwatch` functions starts the timer which not only will update `isRunning` to true, but also update the `previousTime` state using JS date.now method

```jsx
class Stopwatch extends Component {
  state= {
    isRunning: false,
    elapsedTime: 0,
    previousTime: 0   
  };
  componentDidMount(){
    this.intervalID = setInterval(() => this.tick(), 100 );
  }
  tick =() => {
  if(this.state.isRunning){
    const now = Date.now();
    this.setState( prevState => ({
      previousTime: now,
      elapsedTime: prevState.elapseTime + (now - this.state.previousTime)
    }));
  }
    
  }
  
  handleStopwatch = () => {
    this.setState( prevState=> ({
     isRunning: !this.state.isRunning
    }));
    if(!this.state.isRunning){
     this.setState({previousTime: Date.now() });
    }
  }
  
  render(){
  ..
  } 
}

```
* [Adding Lifecycle Methods to a Class](https://reactjs.org/docs/state-and-lifecycle.html#adding-lifecycle-methods-to-a-class)
* [`componentDidMount()`  – React docs](https://reactjs.org/docs/react-component.html#componentdidmount)
* [`setInterval()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval)
* [`Date.now()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now)
* [Reasons for delays longer than specified](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout#Reasons_for_delays_longer_than_specified)

#### Resetting the Stopwatch
In order to display the stopwatch in Seconds, we need to convert `elapsedTime` from milliseconds to seconds.

```jsx
class Stopwatch extends Component {
...
  render(){
    return ( 
		<div className="stopwatch"> 
			<h2>Stopwatch</h2> 
			<span className="stopwatch-time">
            	{ Math.floor(this.state.elapsedTime /1000)}
            </span> 
			
			<button  onClick={  this.handleStopwatch }>
				{  this.state.isRunning ?  'Stop'  :  'Start'  }
			</button>
			
			<button onClick={this.handleReset}>Reset</button> 
		</div> 
	);
  } 
}
```
But to make the code more organized by storing the function and calculation in a variable. In the render method, any intermediary variables should be written outside the return statement.

```jsx
  render(){
  	const seconds = Math.floor(this.state.elapsedTime /1000)
    
	return ( 
		<div className="stopwatch"> 
		...
			<span className="stopwatch-time">
            	{ seconds }
            </span> 
		...
		</div> 
	);
  } 
}
```
Finally, we'll create a function to handle the reset and connect it to our Reset button via a OnClick event.

```jsx
handleReset  =  ()  => {
	this.setState({ elapsedTime:  0 });
}
```

#### Prevent Memory Leaks with componentWillUnmount()
Since components do not always stay in the DOM, React also provides the `componentWillUnmount` lifecycle method to help you handle unmounting of components. This can help prevent memory leaks in your application.

 So any time, you use the `componentDidMount()` method, you should also be thinking about what might happen when the component unmounts. Since `componentWillUnmount()` is an unmounting method, it's where you should perform any clean-ups thats should be done like
 - clearing timers
 - cancelling active network request
 - tearing down any DOM elements or event listeners created in `componentDidMount`

```jsx
componentWillUnmount(){
  clearInterval(this.intervalID);
}
```

* [Adding Lifecycle Methods to a Class](https://reactjs.org/docs/state-and-lifecycle.html#adding-lifecycle-methods-to-a-class)
* [`componentWillUnmount()`  – React docs](https://reactjs.org/docs/react-component.html#componentwillunmount)
* [`clearInterval()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/clearInterval)
* [Beyond Memory Leaks in JavaScript](https://medium.com/outsystems-experts/beyond-memory-leaks-in-javascript-d27fd48ae67e)
* [Fetching Data with the Fetch API](https://teamtreehouse.com/library/fetching-data-with-the-fetch-api)

### React Component Patterns
#### Optimize Performance with PureComponent
Usually when a component detects a change in its props, React will update the parts of UI that need to change as a result of the change in props, this is called **Wasted Render**. When a component re-renders every data in the component, when only a small part changed. This can be solve using `PureComponent`. This is more performant version of a component, and is another way you might see classes written in React.

```JSX
import React, { PureComponent } from  'react';
import Counter from  './Counter';

class  Player  extends  PureComponent  {
	render() {
		console.log(this.props.name +  ' rendered');
		return (
			<div  className="player">
				<span  className="player-name">
				<button  className="remove-player"  onClick={()  =>  this.props.removePlayer(this.props.id)}>✖</button>
{  this.props.name }
				</span>
				<Counter
					score={  this.props.score }
					index={  this.props.index }
					changeScore={  this.props.changeScore}			
				/>
			</div>
		);
	}
}
export  default Player;
```

`PureComponent` implements a lifecycle methods behind the scenes called `shouldComponentUpdate` that runs a shallow comparison of props and state. The lifecycle method automatically checks whether a render is required for the component and calls render only if it detects changes in state or props.

Use PureComponent when you have performance issues and have determined that a specific component is re-rendering too often.

[React.PureComponent](https://reactjs.org/docs/react-api.html#reactpurecomponent)
[Using  `<PureComponent/>`  in React](https://medium.com/front-end-hacking/using-a-purecomponent-in-reacts-262972f9f1e0)
[`shouldComponentUpdate()`](https://reactjs.org/docs/react-component.html#shouldcomponentupdate)

A PureComponent should only contain child components that are also PureComponents.

Converting Player to a class and a PureComponent in Player.js


#### Destructuring Props
ES2015 introduced **destructuring assignment**, which is a special kind of syntax you can use to "unpack" (or extract) values from arrays, or properties from objects, into distinct variables. Developers often use destructuring in React to make their components cleaner and easier to understand. It provides a more concise way to write your props.

In our example, wherever we're using props we need to repeat `props.propname` or `this.props.propsname` over and over again. Since props is an object, we can destructure a component's props into individual variables

There are two ways you can destructure props in a stateless functional component:
- variable assignment
- function parameters

**Header. js**
```JSX
import React from  'react';
import Stats from  './Stats';
import Stopwatch from  './Stopwatch';

const  Header  =  (props)  => {
	return (
		<header>
			<Stats  players={ props.players }  />
			<h1>{ props.title }</h1>
			<Stopwatch  />
		</header>
	);
}

export  default Header;
```
**Header. js** after using variable assignment
```JSX
import React from  'react';
import Stats from  './Stats';
import Stopwatch from  './Stopwatch';

const  Header  =  (props)  => {
	const {players, title} = props;
	return (
		<header>
			<Stats  players={ players }  />
			<h1>{ title }</h1>
			<Stopwatch  />
		</header>
	);
}

export  default Header;
```
**Header. js** using function parameters
```JSX
import React from  'react';
import Stats from  './Stats';
import Stopwatch from  './Stopwatch';

const  Header  =  ({ players, title })  => {
	return (
		<header>
			<Stats  players={ players }  />
			<h1>{ title }</h1>
			<Stopwatch  />
		</header>
	);
}

export  default Header;
```
In classes props are not accessed through a props parameter, like they're in functions. To destructure from `this.props` you use a variable assignment

[Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
[Learn the basics of destructuring props in React](https://medium.freecodecamp.org/the-basics-of-destructuring-props-in-react-a196696f5477)

#### Refs and the DOM
In React you typically do not target elements directly, and modify them like you would when working with JavaScript and the DOM. To modify what a React component or element display on the screen, you use state and props. You trigger a state change and a re-render the component with new props, and if it's a component with local state or a controlled component, you'll re-render it with each update in state. There may be times when you need to target and modify an element outside of that typical data flow so React provides an espace hatch with **refs**. Refs let you access and interact with the DOM nodes or React elements created in the render method. They make it possible to let you do the more traditional DOM manipulation, and they're commonly used to access form elements and get their values.

Earlier, we learned how to update the value of an input field using state, by creating a controlled component. We created a value's state, wrote a function to update the value of state and wired the input field to the function using an onChange event. For only one input field , writing this code is not a big deal and this is still the recommended React way to control form elements, especially if you need to validate user input in real time, or filter results with every keystroke. However, if you're building a form that does not require internal state, you can use ref attribute instead of writing an even handler for every state update. So we'll a ref that will access the player text field.

You create a ref using the `React.createRef()` method, and the you attach the ref to a react element via the ref attribute.

Addplayer.js
```JSX
import React, { Component } from  'react';

class  AddPlayerForm  extends  Component  {
	state = {
		value:  ''
	};
	
	handleValueChange  =  (e)  => {
		this.setState({ value: e.target.value });
	}
	
	handleSubmit  =  (e)  => {
		e.preventDefault();
		this.props.addPlayer(this.state.value);
		this.setState({ value:  ''});
	}
	
	render(){
		return (
			<form  onSubmit={ this.handleSubmit }>
				<input
					type="text"
					value={  this.state.value }
					onChange={ this.handleValueChange }
					placeholder="Enter a player's name"
				/>
				<input
					type="submit"
					value="Add Player"
				/>
			</form>
		);
	}
}
export  default AddPlayerForm;
```

Refs can provide an easier and quicker way to get the value of an input field. Now, when building forms, when should you use a controlled component instead of creating refs, and vide versa?. Controlled components have internal state and require functions to update state. They make it easier to modify or validate user input or filter results based on user input in real time. Controlled components with state render on every stroke, whereas in refs, render is only called once.

```JSX
import React, { Component } from  'react';

class  AddPlayerForm  extends  Component  {
	
	playerInput = React. createRef();

	handleSubmit  =  (e)  => {
		e.preventDefault();
		this.props.addPlayer(this.playerInput.current.value);
		//Reset the Submit field after adding a Player
		e.currentTarget.reset();
	}
	
	render(){
		return (
			<form  onSubmit={ this.handleSubmit }>
				<input
					type="text"
					ref={ this.handleSubmit }
					placeholder="Enter a player's name"
				/>
				<input
					type="submit"
					value="Add Player"
				/>
			</form>
		);
	}
}
export  default AddPlayerForm;
```
Finally, refs are not limited to class components. You can create and use refs inside a functional component. 
```JSX
const AddPlayerForm = ({ addPlayer }) => {   
	let playerInput = React.createRef(); 
	let handleSubmit = (e) => { 
		e.preventDefault(); 
		addPlayer(playerInput.current.value); 		
		e.currentTarget.reset(); 
	}   
	return ( 
		<form onSubmit={handleSubmit}> 
		<input 
			type="text" 
			ref={playerInput} 
			placeholder="Enter a player's name" 
		/>   
		<input 
			type="submit" 
			value="Add Player" 
		/>
	</form> 
	); 
}
```
[Refs](https://reactjs.org/docs/glossary.html#refs)
[Refs and the DOM](https://reactjs.org/docs/refs-and-the-dom.html)
[Refs and Functional Components](https://reactjs.org/docs/refs-and-the-dom.html#refs-and-functional-components)
[`currentTarget`](https://developer.mozilla.org/en-US/docs/Web/API/Event/currentTarget)

#### Validate Props with PropTypes
Props play a huge role in React, since in the dypical dataflow, props are the only way that components can interact with other components
As your app grows, it's a good practice to "type check" or validate the data a component receives from props. There are three popular ways to handle type checking in React:
- Prop Types
- TypeScript
- Flow

We'll learn how to validate props with the PropTypes library. PropTypes used to be built into React, it was moved into a separate package, because type checking is optional, and to give developers the option ob using other tools and approaches, therefore they need to be installed and imported
```console
npm install --save prop-types
```
To run type checking on the props for a component, you assign it the PropTypes property. The propTypes object contains the props being passed to the component as its keys.

PropTypes comes with a range of validators you can use to make sure that the data coming in from props is valid. It provides helpful warnings at runtime.
```jsx
import PropTypes from 'prop-types';

....
Stats.propTypes ={
//We can be very specific by even checking the properties of the object
 players: PropTypes.arrayOf(PropTypes.shape({
    score:PropTypes.number
  }))
}:
```
PropTypes not only help you catch and avoid bugs, they also serve as a documentation for components. Other developers working on the same project will know exactly which props your components take, and what types they should be.

This is not required, but this makes for much easier debugging, and for _perfomance reasons, PropTypes is only checked in development mode_.

[Static Type Checking](https://reactjs.org/docs/static-type-checking.html)
[TypeScript](https://www.typescriptlang.org/)
[Flow: A static type checker for JavaScript](https://flow.org/)
[Typechecking With PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)
[PropType validators](https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes)
[prop-types](https://www.npmjs.com/package/prop-types)

#### Static PropTypes and Default Props
In class components, it's common to define `propTypes` inside the class, usually at the top and outside of the render method with the `static` keyword. Static just provides another way to define prop types on the class. The main difference between the other method and `static`, is that with `static` you don't need to instantiate the class to access PropTypes, you call prop types straight from the class.

One advantage of defining propTypes with `static`, is that it makes your prop validation immediately visible to everyone right at the top of the class.

```jsx
...
class  Player  extends  PureComponent  {
	static propTypes = {
		changeScore:  PropTypes.func,
		removePlayer:  PropTypes.func,
		name:  PropTypes.string.isRequired,
		score:  PropTypes.number,
		id:  PropTypes.number,
		index:  this.propTypes.number
	};
	render() { ...
```
You can even make a prop required. This can be extremely helpful; if you omit a prop  altogether, just chain `isRequired`

```jsx
...
class  Player  extends  PureComponent  {
	static propTypes = {
		changeScore:  PropTypes.func,
		removePlayer:  PropTypes.func,
		name:  PropTypes.string.isRequired,
		score:  PropTypes.number.isRequired,
		....
	};
```
Finally, you can also set a default value for your props, with a `defaultProps` object.

Header.js
```jsx
Header.defaultProps = {
	title:  'Scoreboard'

}
```
[Default Prop Values](https://reactjs.org/docs/typechecking-with-proptypes.html#default-prop-values)
[`static`  – MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static)

TO DO
- Add propTypes for the other components
HIghest Score Feature
- Add a crown icon next to the player name inside the player component
- When a player on the scoreboard has the highest score the icon changes from light grey to gold and displays a short scaling animation
- There is no highest score when the page reloads, so all icons should be light grey
- When the player with the highest score is removed, the next one should get the crown
- There is css for the SVG as well as a class `is-high-score`
- Player state
## Using Create React App <a name="create-react"></a>
### What is Create React App?
Setting the front ends tools to develop a React Application can be intimidating and time consuming. 
- Setting up babel to transpile JSX into browser ready code
- Configuring webpack to bundle your project Assets
- Creating your project structure and production build.

Create-React-App is a tool built by developers at Facebook to help you build React applications. This tool provides amazing features like scripts to develop your project locally and deploy to production.

Projects are built as progressive web apps by default, so this mean that in production your apps will be faster and more reliable than traditional web apps and provide engaging mobile experiences.

Creat React App also ships with **jest**, a JavaScript testing framework for testing React components, and it provides helpful run time errors right in the browser and more.

The following command will install create-react-app globally
`npm install -g create-react-app`


* [Create Apps with No Configuration](https://facebook.github.io/react/blog/2016/07/22/create-apps-with-no-configuration.html)
* [What's New in Create React App](https://facebook.github.io/react/blog/2017/05/18/whats-new-in-create-react-app.html)

### Installing and Using Create React App
You create a new project using your console
`create-react-app project-name`
Running the command installs the dependencies needed to build your project. It also generates the initial project structure. After a couple of minutes, you'll get a message saying 'Success!, saying that inside the directory you can run several commands:
- npm start: Starts the development server, and auto reloads the page anytime you make an edit
- npm run build: Bundles the app into static files for production.
- npm test:
- num run eject: Takes your app out of the create-react-app setup, which lets you customize your project configuration.

Starting the server automatically launches your app in the browser on localhost port 3000. In addition, the console output displays a LAN address so that you can access the app from a mobile device on the same network.

In the browser you can see the template create-react-app provides to help you get started. Most of the files we're going to be working with are located in the `src` folder.

Index.js is the entry file for the app, it imports `index.css` the app's base stylesheet, and imports and renders the App component into the DOM via the root div located in the `index.html` file inside the public folder

Create React App sets a fully functional offline first progressive web app by default. Progressive web apps or **PWAs** are web applications that use a collection of modern web technologies to provide native app-like experiences on all types of devices. This web apps rely on special scrips called **service workers** to give users that app-like experience.
 
- `manifest.json` is a file containing metadata associated with your app.  By default sets the app to display in standalone mode when launched from the home screen, this will make the application look and feel like a standalone native app. The main purpose of the manifest is to install the app to the home screen of a device, providing your user with quicker access and a richer experience
- The Jest testing framework is already configured

Use the  `npx`  command to install Create React App and create a new app, all at once. For example:

```
npx create-react-app my-app
```

npx is a tool that's included with npm, as a version 5.2, that makes it easy to install and run packages, especially command-line tools like Create React App.

Learn more about  `npx`  [here](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b), or see  `npx`  in action in  [this Treehouse video](https://teamtreehouse.com/library/setting-up-with-create-react-app-2).

* [Create React App – repo](https://github.com/facebookincubator/create-react-app)
* [Jest testing framework](https://facebook.github.io/jest/)
* [Progressive Web Apps](https://developers.google.com/web/progressive-web-apps/)
* [Making a Progressive Web App](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#making-a-progressive-web-app)
* [Service Workers: an Introduction](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers)
* [Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest)

#### Related Videos
[Introducing Progressive Web Apps – workshop](https://teamtreehouse.com/library/introducing-progressive-web-apps)


### Customizing your Project
You usually delete most of the code inside the App.js starter file and add your own code. 

Mini Project: Search-app

* [react-bootstrap](https://react-bootstrap.github.io/)
* [Updating to New Releases](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#updating-to-new-releases)

### Next Steps with Create React App
Jest is used for writing unit tests
- If you name your files `.spec.js` or `.test.hs`, or place your test files inside a special test folder, Jest will find those files and run tests

`npm run build`
Create React App will generate a build folder inside your project containing all the static files that can be used on a production web server. Build transpiles your react code into code the browser understands using Babel, and it optimizes your files for best performance. It bundles all your JavaScript files into one minified file, and minifies resources like HTML template and CSS to help reduce download times

`npm run eject`
Lets you modify the configuration files, but be careful because once ejected you cannot go back. After the script runs, you'll see a config directory added to your project containing files like `webpack.config`

>The only case in which you need to eject is when the dependency demands that you also chance the build toolchain. For example, if a dependency enforces use of CSS Modules or can't work without a Babel plugin. In that case you would need to Eject
>> Dan Abramov
>Create React App co-autor

* [New Features in React 16](http://blog.teamtreehouse.com/new-features-react-16?_ga=2.260031946.1722474909.1608526474-1889591538.1550124630)
* [Testing React Apps](https://facebook.github.io/jest/docs/tutorial-react.html)
* [`npm run build`](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#npm-run-build)
* [`npm run eject`](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#npm-run-eject)[What's New in Create React App](https://facebook.github.io/react/blog/2017/05/18/whats-new-in-create-react-app.html)
## Data Fetching in React <a name="fetch-react"></a>
Ways to fetch external data with React by creating a GIF searching app by using the Giphy API

1. Once we download the project files we'll install the project dependencies running `npm install` followed by `npm start` to run the project
2. So we'll define an initial state inside the App class that will represent the collection of objects that will change and be updated by components
3. Next, we're going to set up all our data fetching inside React's `componentDidMount()` lifecycle method. This method is called immediately after a component is added to the DOM, which makes it a good place to create the request

```javascript
export  default  class  App  extends  Component  {
	constructor() {
		super();
		this.state = {
			gifs: []
		};
	}
  
	componentDidMount(){
		fetch(`https://api.giphy.com/v1/gifs/trending?api_key=${key}&limit=25&rating=G`)
			.then(response => response.json())
			.then(responseData => {
				this.setState({ gifs: responseData.data });
			})
			.catch(error => {
				console.log('Error fectching and parsing data', error);
		});
	}
	render() {
		console.log(this.state.gifs);
		return (
			<div>
				<div  className="main-header">
					<div  className="inner">
						<h1  className="main-title">GifSearch</h1>
						<SearchForm  />
					</div>
				</div>
				<div  className="main-content">
					<GifList  />
				</div>
			</div>
		);
	}
}
```
Note: I create an external file to include the API key
```javascript
const key =  'this!sMyKEYZZZzz';
export  default key
```

The fetch method and JavaScript promises are available in the latest generation of most browsers, but to make sure that the data fetching also works in older browsers we can install the fetch polyfill developed by GitHub
https://github.com/github/fetch

### Fetching Data with Axios
Like the Fetch API, Axios isn't specific to React so you can use it to fetch data in other JS frameworks, libraries or any Node.js app. In addition to having stronger browser support than Fetch, Axios has  useful built in features:
- supports the Promise API
- Intercept request and responses and alter them before they're handle by `.then()` or `.catch()` 
- automatically converts data to JSON
- you can also use axios to post data to a server 
- protect your app againts XSRF or CSRF attacks and vulnerabilities, so it could prevent malicious request and actions from being executed on your app

So, we'll start by installing it as a project dependency `npm install --save axios`  and them importing it in our file, then we'll copy an example of a GET request from the axios docs and tailor it to our example
```javascript
import axios from  'axios';

componentDidMount(){
	axios.get(`https://api.giphy.com/v1/gifs/trending?api_key=${key}&limit=25&rating=G`)
		.then(response => {
			this.setState({
				gifs: response.data.data
			});
		})
		.catch(error => {
			console.log('Error fetching and parsing data', error);
		});
}
```

-   [Axios documentation](https://github.com/mzabriskie/axios)
-   [Giphy API documentation](https://developers.giphy.com/docs/sdk)
-   [Trending GIFs Endpoint](https://developers.giphy.com/docs/api/endpoint#trending)
-   [What advantage does axios give us over fetch?](https://github.com/mzabriskie/axios/issues/314)

### Displaying the Data
Now we'll display the gifs in our App. 
In our App, the app component is the container responsible for rendering the markup of the app as well as child components. In react is a best practice to include your data fetching logic within a container component like app, you see presentational components should not handle their own data fetching because it tightly couples the data to the view, the two should stay separate. 
1. In the App.js file we'll pass props to the `<GifList />` component
```javascript
render() {
	console.log(this.state.gifs);
	return (
		<div>
			<div  className="main-header">
				<div  className="inner">
					<h1  className="main-title">GifSearch</h1>
					<SearchForm  />
				</div>
			</div>
			<div  className="main-content">
				<GifList  data={this.state.gifs}  />
			</div>
		</div>
	);
}
```
2. Inside the `<GiftList/>` we'll map the data that will go into each `<Gif component />` using a variable
```javascript
const  GifList  = props => {  
	const results = props.data;
	let gifs = results.map(gif =>
		<Gif  url={gif.images.fixed_height.url}  key={gif.id}  />
	);
return(
	<ul  className="gif-list">
		{gifs}
	</ul>
	);
}
```
3. Inside the `<Gif />` component we'll pass the url using props
```javaScript
import React from  'react';
	const  Gif  = props => (
		<li  className="gif-wrap">
			<img  src={props.url}  alt=""/>
		</li>
);

export  default Gif;
```
4. Finally we'll get back to `<GifList />` to render each gif using the variable and a JSX expression

### Building a Search Feature
1. We'll create a function `performSearch` that fetches the data and updates the GIF state when called
2. We'll update the URL to an endpoint that return a search query and change several parameters along with one that will change according to the user input
```javascript
performSearch  =  (query)  => {
	axios.get(`http://api.giphy.com/v1/gifs/search?q=${query}&limit=24&api_key=dc6zaTOxFJmzC`)
		.then(response => {
			this.setState({
				gifs: response.data.data
			});
		})
		.catch(error => {
			console.log('Error fetching and parsing data', error);
		});
}
```
3. We'll wire up this function the component via props
```javascript
render() {
	console.log(this.state.gifs);
	return (
		<div>
			<div  className="main-header">
				<div  className="inner">
					<h1  className="main-title">GifSearch</h1>
					<SearchForm  onSearch={this.performSearch}  />
				</div>
			</div>
			<div  className="main-content">
				<GifList  data={this.state.gifs}  />
			</div>
		</div>
	);
}
```
Now, inside the SearchForm component there's a  `Search Text` state that's specific to the component and gets updated with the `onSearchChange` function with the text users type into the input field, followed by a `handleSubmit` function when the form is submitted, which is where we're going to invoke the `perform Search` function that fetches our data
```javascript
import React, { Component } from  'react';

export  default  class  SearchForm  extends  Component  {
	state = {
		searchText:  ''
	}
	onSearchChange  = e => {
		this.setState({ searchText: e.target.value });
}
	handleSubmit  = e => {
		e.preventDefault();
		this.props.onSearch(this.state.searchText);
		e.currentTarget.reset();
}
	render() {
		return (
			<form  className="search-form"  onSubmit={this.handleSubmit}  >
				<label  className="is-hidden"  htmlFor="search">Search</label>
				<input  type="search"
					onChange={this.onSearchChange}
					name="search"
					placeholder="Search..."  />
				<button  type="submit"  id="submit"  className="search-button"><i  className="material-icons icn-search">search</i></button>
			</form>
		);
	}
}
```
### Displaying the Results
In this app, the `searchText` state is local to the search-form component. The type of value of the input isn't really part of the application state, it's just state that's needed for the component to work. So it's acceptable to use the `searchText` state to update the gif state here on Submit. Now if you're building a large app where `searchText` may be used in other parts of the app or you simple don't want a state that's dependent on another state, you can also use a `ref` to access the value of the input field.

In React, `ref`s allow you to reference or get direct access to a DOM element. When used on an HTML element, the `ref` attribute takes a callback function that receives the underlaying DOM element as its argument, so in this case is a un input
```javascript
ref={(input)  =>  this.query = input}
```
What this does is it puts a reference to the input on the search form class. So now this callback is executed immediately after the component is mounted to the DOM, when the input is rendered onto the page it returns a reference to this input which you can access with `this.query`. Now we can reference the input inside our `handleSubmit` function
```javascript
handleSubmit  = e => {
	e.preventDefault();
	this.props.onSearch(this.query.value);
	e.currentTarget.reset();
 }
```
Now, to make the app more appealing, we need to load some gifs by default, so in our App component, we'll set a default value
```javascript
performSearch  =  (query = 'funny')  => {
	axios.get(`http://api.giphy.com/v1/gifs/search?q=${query}&limit=24&api_key=dc6zaTOxFJmzC`)
		.then(response => {
			this.setState({
				gifs: response.data.data
			});
		})
		.catch(error => {
			console.log('Error fetching and parsing data', error);
		});
}
```
And then updating the `componentDidMount()` method to load the component with the default query
```javascript
componentDidMount(){
	this.performSearch();
}
```
Finally, we have to include a NO GIF component in case someone search for something that's not available, we'll do this with conditional rendering inside the GifList component
```javascript
const  GifList  = props => {  
	const results = props.data;
	let gifs;
	
	if(results.length >0){
		gifs = results.map(gif => <Gif  url={gif.images.fixed_height.url}  key={gif.id} />);
	} else {
		gifs =  <NoGifs />
	} 
return(
	<ul  className="gif-list">
		{gifs}
	</ul>
	);
}
```
Finally, these is a slight second we're you can see the `<NoGifs />` when the component mounts and fetch the data, to make it even more professional, we can add a Loading state in the App component
```javascript
// 1. We add the loading in the state object, initializing it as TRUE
constructor() {
	super();
	this.state = {
		gifs: [],
		loading:  true
};

//2. We change it to false after fetching the data
performSearch  =  (query =  'funny')  => {
	axios.get(`http://api.giphy.com/v1/gifs/search?q=${query}&limit=24&api_key=dc6zaTOxFJmzC`)
	.then(response => {
		this.setState({
			gifs: response.data.data,
			loading:  false
		});
	})

//3. Finally we use conditional rendering with a ternary operator to switching between states

<div  className="main-content">
	{
		(this.state.loading)
			?  <p>Loading...</p>
			:  <GifList  data={this.state.gifs}  />
	}
</div>
```
## React Router 4 Basics <a name="react-router"></a>

### Getting Started with React Router
React Router is a popular React library that manage navigation and rendering of components in Apps.

In web development, **routing** is the process of matching a URL to a view, or the set of components being rendered. In single page apps, routing dynamically loads components and changes what's displayed in the browser as users navigate the app, all without reloading the page. React itself doesn't have built in routing features, thus many developers rely on React Router

[React](https://facebook.github.io/react/)
[React Router](https://reacttraining.com/react-router/web/guides/quick-start)

#### What is Routing?
In this course, we're going to create a **single-page app** or **SPAs** using React and the React Router library. 

SPAs are web applications that display on a single web page, the app's HTML, JavaScript and CSS are loaded only once by the browser, and the content changes dynamically as the user interacts with the app. The app itself never reloads unless the user manually refreshes it. This provides a smoother browsing experience for users. In SPAs routing is responsible for loading and unloading content, while matching the URL with the set of components being rendered.

* A good dependable routing solution should also keep track of the browser's history, to keep the UI in sync with the URL, that way the users can navigate the app using the browser's back and forward buttons.
* Routing should seamlessly link users to specific sections of your app

In other words, routing in SPAs sound work in a way that's consistent with the navigation experience of regular multi-page sites an apps.

JavaScript frameworks like Angular and Ember, come with built-in routing features, but React is not a framework, is a library concerned with rendering your UI 

#### Installing React Router and Declaring Routes
React router is an external library that you install with npm or yarn, since we're working on a react WEB app that uses the DOM and runs in a browser we'll need to install react router DOM, so we'll install it as a dependency of our project

`npm install --save react-router-dom`

React router extends what you already know about react, and the library itself is just a small set of react components, so you write your routes using JSX. React Router DOM provides two components to get you started:
- BrowserRouter: the root routing component that keeps you UI in sync with URL and
- Route: which is responsible for rendering a component in your app, when the URL matches its path.

You begin declaring routes with react router by rendering a router that wraps all your app components, so we'll wrap the BrowserRouter component around our app
```jsx
import React from  'react';
import {
	BrowserRouter,
	Route
} from  'react-router-dom';

const  App  =  ()  => (
	<BrowserRouter>
		<div  className="container">
		</div>
	</BrowserRouter>
);
export  default App;
```
This renders the root router that listens to URL changes, and provides other react router components about the current URL. Normally in react, you render nested or child components with its tag, and is similar with the route component, and the quickest way to create a route us by specifying a path, and the component you want to render for that path by using the path and component properties.
```jsx
<BrowserRouter>
	<div  className="container">
		<Header  />
		<Route  exact  path="/">
			<Home  />
		</Route>
```
#### Inline Rendering with Route
There are other ways you can render a component with **Route** besides the component, for example the **render** prop lets you do inline component rendering, so instead of passing a name of the component to render
```jsx
<Route path="/about" component={About}>
```
you pass it a function that returns the component, so now whenever the URL matches the _path_ the functions gets called and renders that component. 
```jsx
<Route path="/about" render={()=>} <About /> />
```
Now one of the main reasons you'd want to use the render prop over the component one is when you need to pass props to the component you're rendering. Remember that in React, we pass data to components via attributes called props.

### Navigating, Nesting and Redirecting Routes
#### Navigating Between Routes
No SPA is complete without navigation that links users to the different sections of your app. Users need to move though the app by clicking the links in the main menu.

Usually you'll use anchor elements to link different portion of the website with

```html
<ul>
  <li><a href="#">Home</a></li>
   <li><a href="#">About</a></li>
</ul>
```
With React router you use the `link` component, so we imported it into our component and start using it

```jsx
import { Link } from  'react-router-dom';

<header>
	<span  className="icn-logo"><i  className="material-icons">code</i></span>
	<ul  className="main-nav">
		<li><Link  to="/">Home</Link></li>
		<li><Link  to="/about">About</Link></li>
...
```
[`<Link>`  - React Router docs](https://reacttraining.com/react-router/web/api/Link)

#### Styling Active Links
A good intuitive navigation gives users visual feedback about which page they're visiting. React Router provides a simple way to change the appearance of a link when it's active or when the path matches the URL. The `NavLink` component is a special version of the `Link` component that can recognize when it matches the current URL

The NavLink component also lets you assign customs class name to an active link and you can also write active styles directly
```jsx
<ul  className="main-nav">
	<li><NavLink  exact  to="/" activeStyle={{ background: 'tomato'}}>Home</NavLink></li>
	<li><NavLink  to="/about" activeClassName=""actyMcActiveFace">About</NavLink></li>
	<li><NavLink  to="/teachers">Teachers</NavLink></li>
```


* [`<NavLink>`](https://reacttraining.com/react-router/web/api/NavLink)
* [`activeClassName`](https://reacttraining.com/react-router/web/api/NavLink/activeClassName-string)
* [`activeStyle`](https://reacttraining.com/react-router/web/api/NavLink/activeStyle-object)
* [`exact`](https://reacttraining.com/react-router/web/api/NavLink/exact-bool)

#### Redirecting a Route
Instead of hardcoding a path to a submenu, you can use Redirect. It requires a `to` prop and the value should be the URL to redirect to.

```jsx
import { NavLink, Route, Redirect } from  'react-router-dom';
...

<Redirect  to="/courses/html"  />
```
The only problem with this solution is that you refresh in another page, you get automatically redirected, so a better solution is to override the existing courses route and render a redirect component that will navigate to the new location.

```jsx
import { NavLink, Route, Redirect } from  'react-router-dom';
...
<Route  exact  path='/courses'  render={  ()  =>
	<Redirect  to="/courses/html"  />
}>
</Route>
<Route  path='/courses/html'>
	<HTML  />
</Route>
<Route  path='/courses/CSS'>
	<CSS  />
</Route>
...
```


* [`<Redirect>`](https://reacttraining.com/react-router/web/api/Redirect)
* [`<Route>`](https://reacttraining.com/react-router/web/api/Route)

#### Using the Match Object
When you render a component with a `<Route>` react router passes the component additional information about the current path name and the path and URL the route is matching

If we inspect the component in State we can find the `match` object that contains information about how a route is matching the URL. We can access this data from inside components being rendered by `<Route>`. We'll use `match` to dynamically match `<Route>` and `<NavLink>` to the current URL and path.

The path and url properties are useful when building nested routes and links

### Going Further with Routing
#### Displaying 404 Error Routes using Switch

```jsx
import {
BrowserRouter,
Route,
Switch
} from  'react-router-dom';

//After importing component, envelope all Routes in Switch and Add component
<Switch>
....
	<Route  path="/courses">
		<Courses  />
	</Route>
	<Route>
		<NotFound  />
	</Route>
</Switch>
```
## Deploying a React App <a name="deploy-react-app"></a>
### Create a Production Build
Before you can deploy your React application, you'll first need to create a **production-ready built** of your app. This means that you'll create a separate configuration of your app that optimizes your code to run in browsers and make it download as fast as possible.

Using **create-react-app**: 
1. Run `npm run build` This will generate a build folder inside your project containing all the static files that can be used on a production web server. The build command transpiles, optimizes all JavaScript into one minified file and minifies resources like the HTML template and CSS to help reduce download times. It's also going to provide a service worker file to help run the app offline and this will be the folder that you deploy to the server. Now, to view the production build, you'll still need to run it on a server, a quick way to do that  as suggested in the Create React App docs is to use a tool called **serve**, which serves static sites and single page applications 

- In the console run `npm install -g serve` 
- Then `serve -s build` This will serve and let you view the production view of your app on localhosto port 5000
- now, any time you make a change to your app and want to preview it at this URL, you'll need to rebuild the app

### Deploy to Github Pages
1. Have your react app in a repo on GitHub
2. Add the homepage field to the package.json file
3. Installe the Github pages package via npm and add a couple of deploy scripts to package.json, so in the console write `npm install --save gh-pages` This is going to let you publicsh to a btranch on GitHub called gh-pages, anything you push to that branch, like your build is going to appeat on the github.io domain
4. Next in the same package.json file go to the scripts object add two properties
```json
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build",
```
Deploy will publish everything from your build folder to your gh-pages branch. Make sure to write predeploy first, that way predeploy will run begore deploy runs, which means that it will automatically create the production-ready build of your app. It will even generate the build folder for you, if you haven'd donde that yet.

Now, you can publish your build to a gh-page branch on the github repo by running `npm run deploy`. This begins creating an optimized production build


**Set a Base URL**
When using React Router, if your app is served from a sub-directory, pass the 'basename' prop to the router to set the base URL for all locations. For example:

<BrowserRouter basename="/course-directory">

## React Context API <a name="react-context-api"></a>
### What is the Context API
In the typical React data flow, components communicate with each other via props. A parent passes props down to child components. Sometimes the intermediary components get props passed to them with the sole purpose of passing that data down one (or several) more levels deep. This cascade of props is often referred to as **prop drilling**.  While prop drilling is not completely discourage or considered a bad practice, but it can become tedious, difficult to manage and error prone.

To get around prop drilling and help prevent state management issues developers often turn to third party libraries like **MobX or Redux. Both help maintain and manage application state in a more scalable and predictable way. Now, in some cases using a library like Redux just to avoid prop drilling might be overkill, so React offers a built in way to do this without having to reach for a state management tool

The **React Context API** provides a way to pass data to components without having to pass props manually at every single level.

Context was an experimental feature in older versions of React, and it officially became a stable feature in React 16.3. In fact, libraries like redux and React Router use **context** behind the scenes as a way to communicate between components 

[Context – React docs](https://reactjs.org/docs/context.html)
[Prop Drilling](https://blog.kentcdodds.com/prop-drilling-bb62e02cb691)

### How Context Works
Context is mainly used when some data needs to be accessible by many components at different nesting levels
The context API has three essential parts:
- `createContext()`
- Provider
- Consumer

First, you have to create the context, so `React.createContext()` sets up a context and returns an object with a provider and a consumer, the two main components of the Context API.

A single **provider** component is used as highest possible in the tree, it allows consumer components to subscribe to context changes. **Consumers** access the provider to get any data they need, thus avoiding prop drilling. The provider and consumers are constantly communicating, it's the communication between the two that makes Context work.

### Create Context
We'll create a new folder named `Context` and  create a new file named `index.js` (This folder and naming structure naming isn't required) where we're going to define our context, provider and consumer:

```jsx
import React from  'react';

const ScoreboardContext =  React.createContext();
  
export  const Provider =  ScoreboardContext.Provider;
export  const Consumer =  ScoreboardContext.Consumer;
```
We'll make use of the `Provider` in the parent `App.js` component.

You don't need to include `index.js` in the import path when resolving the import path to the context directory, node will look for an `index.js` file and load it. So `./Context` is really a path to `'./Context/index.js'`

To provide the context to all children of app, we'll wrap all the JSX in the return statement with a `<Provider>` tag

```jsx
import React, { Component} from 'react';
import { Provider } from  './Context';
...

render() {
	return (
		<Provider value={ this.}>
			<div  className="scoreboard">
				<Header
					title="Scoreboard"
					players={  this.state.players }
				/>
				{/* Players list */}
				{this.state.players.map( (player, index)  =>
				<Player
				...
				 <AddPlayerForm  addPlayer={this.handleAddPlayer}  />
			</div>
		</Provider>

		);
	}
}
```

[`React.createContext()`](https://reactjs.org/docs/context.html#reactcreatecontext)
[Provider](https://reactjs.org/docs/context.html#provider)

### Provide and Consume State
The provider usually lives at the top level of your app. In requires a value prop to share data. This value can be anything, but it's usually the application state and any actions or event handlers shared between components. 
```jsx
...
	<Provider value={this.state.players}>
```
A single provider, can be connected to many consumers, no matter how far down they are on the component tree.

So now, we'll add context to the `Stats.js` component from this:
```jsx
import React from  'react';
import PropTypes from  'prop-types';

const  Stats  =  ({ players })  => {
  const totalPlayers = players.length;
	const totalPoints = players.reduce((total, player)  => {
		return total + player.score;
		}, 0);
	return (
	<table  className="stats">
		<tbody>
			<tr>
				<td>Players:</td>
				<td>{ totalPlayers }</td>
			</tr>
			<tr>
				<td>Total Points:</td>
				<td>{ totalPoints }</td>
			</tr>
		</tbody>
	</table>
	);
}

Stats.propTypes = {
	players:  PropTypes.arrayOf(PropTypes.shape({
		score:  PropTypes.number
		}))
	};
export  default Stats;
```
To this

```jsx
import React from  'react';
import { Consumer} from  './Context';

const  Stats  =  ()  => {
	return(
		<Consumer>
			{ context => {
				const totalPlayers = context.length;
				const totalPoints = context.reduce((total, player)  => {
					return total + player.score;
				}, 0);
				
				return (
				<table  className="stats">
					<tbody>
						<tr>
							<td>Players:</td>
							<td>{ totalPlayers }</td>
						</tr>
						<tr>
							<td>Total Points:</td>
							<td>{ totalPoints }</td>
						</tr>
					</tbody>
				</table>
				);
			}
		}
		</Consumer>
	);
}
export  default Stats;
```



To render anything inside the consumer, you use a pattern in React called **Render Prop**, this refers to a method for sharing code between React components using a prop whose value is a function. A component is provided a prop which takes a function that returns a React element. This pattern is also called **function as a child**, because instead of passing a prop, you're also able to write a function inside the opening and closing Consumer tags. The function returns the part of the UI you want to render. So, we'll use a function that returns the stats UI (from the exercise) inside the consumer, this function is required and needs to be placed inside a JSX expression.

The function takes the current context value as a parameter, and returns JSX. This parameter is commonly named value or context. The context parameter passed to the function will be equal to the value prop of the provider, in other words, the data we pass into the provider's value prop. So the consumer is now subscribed to any context changes

```jsx
<Component render={ data => (
	<h1>Hello, {data.user}!</h1>
)} />
```

And now, we can clean `Header.js`
Before using context
```jsx
import React from  'react';
import PropTypes from  'prop-types';
import Stats from  './Stats';
import Stopwatch from  './Stopwatch';

const  Header  =  ({ players, title })  => {
	return (
		<header>
		<Stats  players={ players }  />
		<h1>{ title }</h1>
		<Stopwatch  />
		</header>
	);
}

Header.propTypes = {
	title:  PropTypes.string,
	players:  PropTypes.arrayOf(PropTypes.object)
}

Header.defaultProps = {
	title:  'Scoreboard'
}  

export  default Header;
```
After Context
```jsx
import React from  'react';
import Stats from  './Stats';
import Stopwatch from  './Stopwatch';

const  Header  =  ({ title })  => {
	return (
		<header>
		<Stats />
		<h1>{ title }</h1>
		<Stopwatch  />
		</header>
	);
}
export  default Header;
```
`React.Fragment` lets you group a list of sibling elements or components without having to add an unnecessary wrapper element. It doesn't render anything out to the DOM.


[Consumer](https://reactjs.org/docs/context.html#consumer)
[Using Props Other Than render](https://reactjs.org/docs/render-props.html#using-props-other-than-render)
[Fragments](https://reactjs.org/docs/fragments.html)
[Render props](https://reactjs.org/docs/render-props.html)

#### Provide and Consume Actions
We've learned how to read from the state provided by context. But we can also pass functions that modify that state, that way consumers can respond to user interactions with state updates.

It's common to pass the provider's value prop an object to store multiple properties in state, as well as any event handlers or actions you want to perform on the data.

For instance, the `handleScoreChange` function defined in the App component, is passed to the Counter componet by a way on the PlayerLists and Player Component
App.js
```jsx
//App.js

import React, { Component } from 'react';
/* 2. You don't need to include /index.js
in the import path, when resolving the import path to the context directory node will look for an index file and load it
*/
import { Provider } from './Context';
import Header from './Header';
import PlayerList from './PlayerList';
import AddPlayerForm from './AddPlayerForm';

class App extends Component {
  state = {
    players: [
      {
        name: "Guil",
        score: 0,
        id: 1
      },
      {
        name: "Treasure",
        score: 0,
        id: 2
      },
      {
        name: "Ashley",
        score: 0,
        id: 3
      },
      {
        name: "James",
        score: 0,
        id: 4
      }
    ]
  };

  // player id counter
  prevPlayerId = 4;

  handleScoreChange = (index, delta) => {
    this.setState( prevState => ({
      score: prevState.players[index].score += delta
    }));
  }

  handleAddPlayer = (name) => {
    this.setState( prevState => {
      return {
        players: [
          ...prevState.players,
          {
            name,
            score: 0,
            id: this.prevPlayerId += 1
          }
        ]
      };
    });
  }

  handleRemovePlayer = (id) => {
    this.setState( prevState => {
      return {
        players: prevState.players.filter(p => p.id !== id)
      };
    });
  }

  render() {
    return (
    /*
    * 3. Wrap everything after the return statement inside the Provider tag
    4. We'll passed the value state > Stats.js
    */ 
      <Provider value={this.state.players}>
        <div className="scoreboard">
          <Header />

          <PlayerList 
       
            changeScore={this.handleScoreChange}
            removePlayer={this.handleRemovePlayer}   
          />
          
          <AddPlayerForm addPlayer={this.handleAddPlayer} />
        </div>
      </Provider>
    );
  }
}

export default App;
```

```jsx
//PlayerList Component
import React from 'react';
import { Consumer } from './Context';
import PropTypes from 'prop-types';
import Player from './Player';

const PlayerList = (props) => {
  return (
    <Consumer>
      { context => {

        return(
          <React.Fragment>
            {context.map( (player, index) =>
            <Player 
            /* We using this spread operator to pass the name, score 
            and ID we're getting from each player object via map all 
            at once as props, that way you don't have to explicitly list each prop name and value */ 
              {...player}
              key={player.id.toString()} 
              index={index}
              changeScore={props.changeScore}
              removePlayer={props.removePlayer}           
            />
            )}
          </React.Fragment>


        );
      }}

    </Consumer>
  );
}

PlayerList.propTypes = {
  changeScore: PropTypes.func.isRequired,
  removePlayer: PropTypes.func.isRequired,
};

export default PlayerList;
```
```jsx
//Player component

import React, { PureComponent } from 'react';
import PropTypes from 'prop-types';
import Counter from './Counter';

class Player extends PureComponent {

  static propTypes = {
    changeScore: PropTypes.func.isRequired,
    removePlayer: PropTypes.func.isRequired,
    name: PropTypes.string.isRequired,
    score: PropTypes.number.isRequired,
    id: PropTypes.number.isRequired,
    index: PropTypes.number.isRequired
  };

  render() {
    
    const { 
      name,
      id,
      score,
      index,
      removePlayer,
      changeScore
    } = this.props;

    return (
      <div className="player">
        <span className="player-name">
          <button className="remove-player" onClick={() => removePlayer(id)}>✖</button>
          { name }
        </span>
  
        <Counter 
          score={score}
          index={index}
          changeScore={changeScore} 
        />
      </div>
    );
  }
}

export default Player;
```
Before making it's way into the Counte. The prop passed to each component acts as a callback function, that's called at a later time to change a piece of state

```jsx
import React from 'react';
import PropTypes from 'prop-types';

const Counter = ({ index, score, changeScore }) => {
  return (
    <div className="counter">
      <button className="counter-action decrement" onClick={() => changeScore(index, -1)}> - </button>
      <span className="counter-score">{ score }</span>
      <button className="counter-action increment" onClick={() => changeScore(index, 1)}> + </button>
    </div>
  );
}

Counter.propTypes = {
  index: PropTypes.number,
  score: PropTypes.number,
  changeScore: PropTypes.func  
};

export default Counter;
```
Se, we'll start by providing the `handleScoreChange` function, along with the players state directly to a consumer.


Finally, we can move the `<Provider>` along with the state and actions into a separate (higher order) component. As a result, the `App` component will have less code and responsibilities, making it easier to think about and maintain.

[Higher-Order Components](https://reactjs.org/docs/higher-order-components.html)

#### Provide Remaining Actions to Child Components
The consumer doesn't always have to wrap everything in the return statement, in the example below the consumer only wraps the part of the UI that needs to consume the `removePlayer` action.
```jsx
import React, { PureComponent } from 'react';
import PropTypes from 'prop-types';
import { Consumer } from './Context';
import Counter from './Counter';

class Player extends PureComponent {

  static propTypes = {
    name: PropTypes.string.isRequired,
    score: PropTypes.number.isRequired,
    id: PropTypes.number.isRequired,
    index: PropTypes.number.isRequired
  };
 
  render() {
    
    const { 
      name,
      id,
      score,
      index
    } = this.props;

    return (
      <div className="player">
        <Consumer>
          { context => (
            <span className="player-name">
              <button className="remove-player" onClick={() => context.actions.removePlayer(id)}>✖</button>
              { name }
            </span>

          )
          }
        </Consumer>
        
  
        <Counter 
          score={score}
          index={index}
      
        />
      </div>
    );
  }
}

export default Player;
```

#### Refactor the Provider
Now, we can move the provider along with state and actions into a separate high order component as a result our main app component will have less coding responsabilities making it that much easier to think about and maintain.

In JavaScript a higher-order function is a function that accepts another function as an argument, in a similar way a **Higher-Order Component(HOC)** access a wrapper takes an existing component and returns a new component. Higher-order component lets you share functionality accross multiple components.

```jsx
//index.js
export class Provider extends Component { 
    state = {
        players: [
          {
            name: "Guil",
            score: 0,
            id: 1
          },
          {
            name: "Treasure",
            score: 0,
            id: 2
          },
          {
            name: "Ashley",
            score: 0,
            id: 3
          },
          {
            name: "James",
            score: 0,
            id: 4
          }
        ]
      };

      // player id counter
  prevPlayerId = 4;

  handleScoreChange = (index, delta) => {
    this.setState( prevState => ({
      score: prevState.players[index].score += delta
    }));
  }

  handleAddPlayer = (name) => {
    this.setState( prevState => {
      return {
        players: [
          ...prevState.players,
          {
            name,
            score: 0,
            id: this.prevPlayerId += 1
          }
        ]
      };
    });
  }

  handleRemovePlayer = (id) => {
    this.setState( prevState => {
      return {
        players: prevState.players.filter(p => p.id !== id)
      };
    });
  }

    render() {
        return (
            <ScoreboardContext.Provider value={{
                //Inside this object, we'll pass in our data with a set of properties
                players: this.state.players,
                actions: {
                  changeScore: this.handleScoreChange,
                  removePlayer: this.handleRemovePlayer,
                  addPlayer: this.handleAddPlayer 
                }
              }}>
              { this.props.children }
            </ScoreboardContext.Provider>   
         );
    }

} ScoreboardContext.Provider;

```
**children** is a special prop in React that lets you pass components as data to other components. Whenevever we use the Provider component by defining a set of provider tags, any elements placed between the tags is considered to be children of the component. So `props.children` is going to pass anything we include between the opening and closing tags into the Provider component and render it to the UI.

For example, the provider should live as close to the top as possible. So in the App entry file

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from './components/Context';

import App from './components/App';
import './index.css';

ReactDOM.render(
  <Provider>
    <App />
  </Provider>, 
  document.getElementById('root')
);

```
`props.children` is what allows the App component, along with all of the app's children to be passed into the provider and rendered.

So now App is a simple staleess component. so we can simplify it even further by converting it to a function.
```jsx
//App.js

import React from 'react';
import Header from './Header';
import PlayerList from './PlayerList';
import AddPlayerForm from './AddPlayerForm';

const App = () => {
  return (    
    <div className="scoreboard">
      <Header />

      <PlayerList />
      
      <AddPlayerForm />
    </div>
  );
}
  
  

export default App;

```

#### Refactor Consumers
Just like we've done with props, we can use ES2015 destructuring to extract the state and actions from the value object receipt from the provider

In PlayerList we can unpack the players property by passing the consumers function and object with the variable players, then replace 	`contest.players` with just players

We've successfully offloaded state management and the distribution of events handlers on to the provider. The provider component is now the App's single source of truth for the data and actions

Notice that we didn't use a consumer in the Stopwatch component, the stopwatch consist of local component state, and actions not shared with other components in the app.

*You might not always know how many components will be between the parent and the nested children you want to get that data to, so context provides an incredible handy way for components at any nesting level to directly access the data they need.

*Pending to destructure the actions and players in the STATS and AddPlayerForm components*

##  React Hooks <a name="hooks"></a>

The React library has traditionally allowed developers to create and manage state, as well as run certain code based on the lifecycle of a component. 
Class components provide one way to declare and manage state, and call lifecycle methods like `componentDidMount` and `componentWillUnmount` but they with some drawbacks like:
- Optimizing classes can be slower to process for machines, making it more dificult to minify files
- Can also interfere with React tools and features like hot reloading

Until recently, developers referred to function components which are regular JavaScript functions, as stateless components, because you weren't able to access features like state and lifecycle methods, but that's where React Hooks come in.

React hooks are special built-in functions that allow you to hook into the power of class components, with a cleaner and more straightforward syntax. Hooks solve common tasks like 
- Handling state and rendering UI when state changes.
- Provide easier access to your React app's context
- Update components with an alternative to lifecycle methods.

### useState Hook
Usually, to create a stateful class component, you add a constructor that assigns the initial `this.state`:
```javascript
class App extends React.Component {
 constructor(props) { 
	 super(props); 
	 this.state = { 
		 score: 0 
	 }; 
  }   
render() {...} 
}
```
You use Hooks inside functions only (Hooks don't work inside classes), so  `this`  is not available inside a function component. Instead, you use the  `useState`  Hook for state management. As you'll learn,  `useState()`  is the equivalent of both  `this.state`  and  `this.setState`  for function components.

Once you import  `useState`  from React, the next step is to declare a state variable by calling  `useState()`. The following declares a state variable named  `score`

`useState()`  accepts one optional argument – the initial value of the state variable. In the example above, the initial value of the  `score`  state is  `0`. Calling  `useState()`  with the initial state returns an array with two values:

The first array element is a variable with the current state value (`0`  in this case). It's similar to  `this.state`. The second element is a function to update that value, and it's similar to  `this.setState()`.

When working with React Hooks, you use  [destructuring assignment syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)  to assign each returned value to a distinct variable.

In class components, the state always has to be an object. With  `useState()`  state can be an object, array, or another JavaScript primitive like a string or integer.
```javascript
import React, { useState } from  'react';
import  './App.css';

function  App() {
	const [ score, setScore ] =  useState(0);  // [0, f]
  
  return (
	<div  className="App">
		<header  className="App-header">
			<h1>  { score }</h1>
		</header>
	</div>
  );
}
export  default App;
```

### Update State
The first time you call  `useState()`, it sets the initial component state, and on all following calls, you're able to access or update what's in state.

In a class component, you call  `this.setState()`  to update what's in state, for example:
```javascript
class App extends React.Component {
 ...   
 render() {
	return ( 
		<div className="App"> 
			<header className="App-header"> 
				<h1>{ this.state.score }</h1> 
				<button onClick={() => this.setState({ score: this.state.score + 1 })}> Increase score 
				</button> 
			</header> 
		</div> 
	); 
  } 
}
```
but with Hooks
```javascript
  return (
	<div  className="App">
		<header  className="App-header">
			<h1>  { score }</h1>
			<button  onClick={()  =>  setScore(score +  1)}> // update the score state
			</button>
		</header>
	</div>
  );
}
```
With Hooks, you can easily set and update the state without worrying about using  `this`  as the state is already within the scope of the component!

### Declare Multiple States
`useState()` lets you declare one state variable at a time, but you aren’t limited to just one `useState()` call inside a component. You can call `useState()` numerous times to declare multiple state variables
```javascript
function  App() {
	const [ score, setScore ] =  useState(0);  // [0, f]
	const [ message, setMessage ] =  useState('Welcome');
  
  return (
	<div  className="App">
		<header  className="App-header">
			<h1>  { message }</h1>
			<h2>{ score }</h2>
			<button  onClick={()  =>  setScore(score +  1)}>  {/* Update score */}
			Increase Score
			</button>
		</header>
	</div>
  );
}
export  default App;
```
### Update State Based on Previous State
If you need to update state using the previous state value, you can pass a function to the method updating state. The function receives the previous state value and uses it to return the updated value.
```javascript
<button  onClick={()  =>  setScore(prevScore => prevScore +  1)}>  {/* Update score */}
Increase Score
</button>
```

### Perform Side Effects with useEffect
You've learned that there are different phases in a React component's lifecycle: mounting, updating, and unmounting. React provides lifecycle methods to run code at these specific moments. They are used to re-render a component, update the DOM when data changes, fetch data from an API or perform any necessary cleanup when removing a component. Developers refer to these types of actions as "side effects" because you cannot perform them during rendering (additional code runs after React updates the DOM).

Common lifecycle methods React uses to handle side effects in class components are `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`. Forgetting to include one of these methods when needed, can leave us with stale data or [memory leaks](https://teamtreehouse.com/library/prevent-memory-leaks-with-componentwillunmount).

>If you’re familiar with React class lifecycle methods, you can think of useEffect Hook as componentDidMount, componentDidUpdate, and componentWillUnmount combined. -- [React Docs](https://reactjs.org/docs/hooks-effect.html)

```javascript
import React, { useState, useEffect } from 'react';   

function App() {
 const [score, setScore] = useState(0); 
 const [message] = useState('Welcome!');   
	
  // The effect happens after render 
  useEffect(() => { 
	  console.log('useEffect called!'); 
  });   

  return (...); 
}
```
The  `useEffect`  Hook instructs React to do  _something_  after render, so it's called when the component first renders and after each subsequent re-render or update. If you run the code above, notice how "useEffect called!" immediately displays in the console. The message displays, again and again, each time the  `score`  state updates.

### Prevent `useEffect` from Causing Unnecessary Renders
Since  `useEffect`  gets called after every render, applying it after each render might create a performance problem. The  `useEffect`  Hook takes an optional array as a second argument that instructs React to skip applying an effect (and re-rendering) if specific values haven’t changed between re-renders.

In the array, you list any dependencies for the effect. In other words, any state variables that are used or updated inside  `useEffect`. The array instructs the  `useEffect`  Hook to run  **only**  if one of its dependencies changes.

```javascript	
  // The effect happens after render 
  useEffect(() => { 
	  console.log('useEffect called!'); 
  }, []); // pass an empty array to useEffect once   
```
### Access State inside `useEffect`
You're able to access a state variable (even update state) from inside `useEffect`. A common example is updating the document's title when state changes. Manually changing the DOM in React components, as shown below, is one example of a side effect:
```javascript
useEffect(()  => {
	document.title =`${message}. Your score is ${score}`
	}, [message, score]);
```
React runs `useEffect` to compare `score` from the previous render to `score` from the next render. Each time the value of `score` changes (increments/decrements), React re-applies the effect and updates the page's title:

### Data Fetching with `useEffect`
You'll most likely use the `useEffect` Hook to fetch data from an API, similar to how you'd use the `componentDidMount` method in a class. Consider the following example, which fetches data (a random dog image) from the [Dog API](https://dog.ceo/dog-api/):
```javascript
function App() {
 const [data, setData] = useState('');   

  useEffect(() => { 
	  console.log('useEffect called!'); 
	  fetch('https://dog.ceo/api/breeds/image/random') 		
	  .then(res => res.json()) 
	  .then(data => setData(data.message)) 
	  .catch(err => console.log('Oh noes!', err)) 
	  }, []);   
	
 return ( 
	 <div className="App"> 
	 <img src={data} alt="A random dog breed" /> 
	 </div> 
  ); 
}
```
Again, passing `useEffect` an empty array as the second argument ensures that it runs only once after the component's initial render. In some cases, omitting the second array argument causes `useEffect()` to execute in an infinite loop, endlessly fetching data. This happens because you're modifying the component's state inside `useEffect()`, which triggers the effect again and again.

-   [`useEffect`  - React docs](https://reactjs.org/docs/hooks-reference.html#useeffect)
-   [Using the Effect Hook - React docs](https://reactjs.org/docs/hooks-effect.html)
-   [Tip: Use Multiple Effects to Separate Concerns](https://reactjs.org/docs/hooks-effect.html#tip-use-multiple-effects-to-separate-concerns)

#### "Clean Up"  `useEffect`

Some side effects in React require "cleanup," or running additional code when a component unmounts (to prevent a memory leak, for example). With classes, you'd use the  `componentWillUnmount()`  lifecycle method to perform any necessary cleanup.

With Hooks, you don't need a separate function to perform cleanup. Returning a function from your effect takes care of the cleanup, running the function when the component unmounts. Review the  [Hooks documentation](https://reactjs.org/docs/hooks-effect.html#effects-with-cleanup)  to learn more about effects with cleanup.

### Create a GIF Search App with React Hooks
1. First, we'll declare the GIF data State by using `useState` hook, passing it an empty array. the `data` state will hold the array of GIF objects returned from the Giphy API. In the `App` component's `return` statement, render the `<GifList>` component and pass it the `data` state via a prop named `data` 
```javascript
import React, { useState } from 'react';
...
function App(){
  const [data, setData] = useState([]);
}
```
2. We'll use **axios** to fetch the GIF data. Since you use `useEffect` hook when you need to do something after your component renders (perform a side effect) thus we'll use to make the fetch request with axios.

In the `then()` method, we'll use the `setData()` function to update the `data` state with the data returned from the API.

Then we'll declare the state variable to hold the GIF search query. This state will be updated with the value the user types into the search field

```javascript
import React, { useState, useEffect } from  'react'
import  '../App.css';
import key from  '../key.js';
import axios from  'axios';

import SearchForm from  './SearchForm';
import GifList from  './GifList';

function  App() {
	const [data, setData] =  useState([]);
	const [query, setQuery] =  useState('cats');
  
	useEffect(()=> {
		axios(`http://api.giphy.com/v1/gifs/search?q=${query}&limit=24&api_key=${key}`)
		.then(response =>  setData(response.data.data))
		.catch(error =>  console.log('Error fetching and parsing data', error))
		}, []);
		
	return (
		<>
			<div  className="main-header">
				<div  className="inner">
					<h1  className="main-title">GifSearch</h1>
					
					<SearchForm  />
				</div>
			</div>
			<div  className="main-content">
				<GifList  data={ data }  /> //pass down the data state
			</div>
		</>
	);
}
export  default App
```
The  `query`  state is now a dependency of the  `useEffect`  Hook (we're using it in the search query parameter), so we need to include it in the dependency array -- that's the second argument passed to  `useEffect()`:

```javascript    
 useEffect(() => {
     axios(`http://api.giphy.com/v1/gifs/search?q=${query}&limit=24&api_key=YOUR_API_KEY`) .then(response => setData(response.data.data)) .catch(error => console.log('Error fetching and parsing data', error)) }, [query]); // add the query dependency 
    
```
Adding the  `query`  dependency instructs React to call  `useEffect()`  each time the  `query`  state updates.

To update the `query` state, we'll create a function called  `performSearch` that updates the query state
```javascript
function App() {
 const [data, setData] = useState([]); 
 const [query, setQuery] = useState('cats');   
 // update the query state 
 const performSearch = (value) => setQuery(value);   

  useEffect(() => { 
	  ... 
  }, [query]);
```
Now we need to wire the function up to the `SearchForm` component. In the `App` component's `return` statement, give the `SearchForm` component the prop `onSearch`, passing it a reference to the `performSearch` function
```javascript
return (
  ...
  <SearchForm  onSearch={ performSearch }  />
  ...
);
```
Then we need to declare the `SearchForm` component State, in here we'll declare the state that updates the search query on form submit
1. We'll import `useState` and declare the variables that will handle state: `searchText` and `setSearchText` setting the initial state to an empty string.
2. In the `onSearchChange` function, we'll call `setSearch` to update the `searchText` state with the value on the search field. 
```javascript
function SearchForm(props) {
 const [searchText, setSearchText] = useState('');   
 
 const onSearchChange = (e) => setSearchText(e.target.value);
 ...
```
The `performSearch` function in `App.js` accepts one argument -- the search query. In the `handleSubmit` function, pass the `searchText` state up to the `App` component via the `onSearch` function callback. On form submit, the search  `query`  state gets updated, which triggers the  `useEffect()`  Hook to fetch new data.
```javascript
 const handleSubmit = (e) => { e.preventDefault(); 
 // pass the search text back to the App component   
 props.onSearch(searchText); 
 e.currentTarget.reset();
```
Finally, we'll add the loading indicator
```javascript
function  App() {
  ...
  const [isLoading, setIsLoading] =  useState(true);

useEffect(()=> {
	axios(`http://api.giphy.com/v1/gifs/search?q=${query}&limit=24&api_key=${key}`)

	.then(response =>  setData(response.data.data))
	.catch(error =>  console.log('Error fetching and parsing data', error))
	.finally(()  =>  setIsLoading(false));
  }, [query]);

return (
<>

<div  className="main-header">
	<div  className="main-content">
		{
			isLoading
				?  <p> Loading... </p>
				:  <GifList  data={ data }  />  //pass down the data state
		}
	</div>
  </>
);
}
```

## React Authentication <a name="react-auth"></a>
### Introducing the Project
Authentication provides password protection to hide content from unauthorized users. It lets you serve content specifically to a user, as well as customize their settings and experience.

When the client wants to authenticate itself with a server (for example, log in a user), it can do so by including an Authorization request header with the user credentials. Basic Auth transmits the credentials as user ID/password pairs, which are encoded using an encoding scheme called base64 – more on this later.

**What you're gonna build**
In this text-based course, you will learn how to implement Basic Authentication within a React client application, using the Express REST API you built.

You will make requests to the Express API routes from the React client app, implement user registration and login, and configure React Router to protect specific routes (i.e. require that the user be authenticated in order to view a private route). We will be working with the Express app only – no database, just in-memory data. Users will be stored in a JavaScript Array, in order to keep things as simple as possible.

*While this approach works fine for our example, for most situations it'd be less than ideal, as all of the data will be lost between application restarts.*

### Project Preview
This project consist of 4 main routes or views:

- Default root route that's public and visible to every user
- Sign Up route that's also public with Validation errors for inclomplete submission
- Sign In route also with validation
- Authenticated route which is accessible to authenticated or logged user only

THe app also preserves the user's authenticated stated across page refreshes or even if the user closes the browser tab by mistake.

For this app, we'll focus only on the client authentication features of this app (not build it from scratch), which means that you will write all the code for this course within the files inside the client folder.

The client/src folder contains the files you will be working with in this course. Let's quickly review the main files and folders.

* index.js - The entry point into the application which renders the main <App> component.

* App.js - Renders the router that wraps the components of the app.
Context.js - A higher-order component (HOC) that shares functionality across the components of the app. This will let you reuse component logic and state. Remember - "Context" is used in React when data needs to be accessible by many components at different nesting levels.

* Data.js - Contains a class of Data with the API authentication utility methods you will use to create, sign up and authenticate a user. The file is mostly pre-written, making GET and POST requests to the REST API, for example. For this course, we're only going to focus on the authentication parts.

The components folder holds all the individual components of the app. For example, components that render the "Public" and "Authenticated" views, and the sign in and sign up forms.
The styles folder contains the CSS for the application. We will not be working with the CSS as we go through the project, but feel free to change it as you please.

#### Run the Express Server
**REST API Routes and Endpoints**

In the REST API Authentication with Express instruction step, you implemented `/users` routes to create and login a new user, as well as return the current authenticated user, which you tested using an API testing tool like Postman.

In this course, all POST and GET requests from the React client will be made to the /users endpoint using the helper methods for creating and getting users located in the file client/src/Data.js. Be sure to review this file before the next step.

### Implementing Basic Authentication
#### Set up User Registration
```jsx
import config from './config';

/*
helper class that provides utility methods to allow the React client to talk to the Express server
*/

export default class Data {

  api(path, method = 'GET', body = null) {

    /*
    * The url constant configures the request path using the
    * base URL defined in config.js, which gets passed to the
    * returned fetch() method.
    */
    const url = config.apiBaseUrl + path;
  
    const options = {
      method,
      headers: {
        'Content-Type': 'application/json; charset=utf-8',
      },
    };

    if (body !== null) {
      options.body = JSON.stringify(body);
    }

    return fetch(url, options);
  }

  async getUser() {
    const response = await this.api(`/users`, 'GET', null);
    if (response.status === 200) {
      return response.json().then(data => data);
    }
    else if (response.status === 401) {
      return null;
    }
    else {
      throw new Error();
    }
  }
  
  async createUser(user) {
    const response = await this.api('/users', 'POST', user);
    if (response.status === 201) {
      return [];
    }
    else if (response.status === 400) {
      return response.json().then(data => {
        return data.errors;
      });
    }
    else {
      throw new Error();
    }
  }
}

```
`fetch()` accepts an optional second parameter: a configuration object that lets you control a number of different settings you can apply to the request.

The `options` object, for example, sends a request with the HTTP method, as well as the request headers and a stringified body (if body is provided).

The `getUser()` and `createUser()` methods perform the async operations that create and get an authenticated user of our app, using the api() method.

`getUser()` makes a `GET` request to the `/users` endpoint, and returns a JSON object containing user credentials. And `createUser()` makes a `POST` request, sending new user data to the `/users` endpoint.

**Context Review**
Context is primarily used when some data needs to be accessible by many components at different nesting levels. Context lets you pass data through the component tree without having to pass props down manually at every level.

**Use Context Through the App**
1. Pass context to the Provider. In the return() statement pass <Context.Provider> a value prop and, within curly braces, pass it value:
```jsx
return (
  <Context.Provider value={value}>
    {this.props.children}
  </Context.Provider>  
);

```

`value` represents an object containing the context to be shared throughout the component tree.
2. Create a value object to provide the utility methods of the class Data. In the render() method (above the return statement), initialize a variable named value to an object containing a data property set to this.data:
```jsx
const value = {
  data: this.data,
};

return (
  <Context.Provider value={value}>
    {this.props.children}
  </Context.Provider>  
);
```
At the bottom of Context.js is a higher-order function named withContext that wraps a provided component in a <Context.Consumer> component. In other words, withContext automatically subscribes (or connects) the component passed to it to all actions and context changes:
```jsx
export default function withContext(Component) {
  return function ContextComponent(props) {
    return (
      <Context.Consumer>
        {context => <Component {...props} context={context} />}
      </Context.Consumer>
    );
  }
}
```
This will come in handy soon when we need to share user authentication data and actions throughout the app.

**Connect the UserSignUp Component to Context**
Next, we're going to set up the initial user signup logic in the UserSignUp component. Let's connect the component to context first.
1. In App.js, import the withContext function from Context.js:
2. Initialize a variable named UserSignUpWithContext. Set the value to call withContext(UserSignUp):
```jsx
import withContext from './Context';

const UserSignUpWithContext = withContext(UserSignUp);
```
3. Render UserSignUpWithContext. In the signup route, change the component to render when the URL path matches /signup from UserSignUp to UserSignUpWithContext:
```jsx
<Switch>
  ...
  <Route path="/signup" component={UserSignUpWithContext} />
  ...
  <Route component={NotFound} />
</Switch>
```
When React renders a component that subscribes to context, it will read the context value passed to it from its Provider.

#### Implement the Sign up Form
*Getting the Know `UserSignUp.js`**
The file contains a `UserSignUp` class that employs the ["render prop"](https://reactjs.org/docs/render-props.html) technique in React to render a form. Notice how the component <Form> uses an elements prop whose value is a function which returns the input fields to be used in each of the forms:
```jsx
export default class UserSignUp extends Component {
  ...
  render() {
    ...
    return (
      ...
        <Form 
          ...
          elements={() => ( // render prop
            <React.Fragment>
              <input ... placeholder="Name" />
              <input ... placeholder="User Name" />
              <input ... placeholder="Password" />
            </React.Fragment>
          )} /> 
    )
  }
  ...
}
```
**Review Form.js**
The file components/Form.js exports a function that renders any validation errors sent from the API, via the <ErrorsDisplay> function component. It also renders the "Submit" and "Cancel" buttons of a form, as well as handle their functionality, via the functions handleSubmit and handleCancel. Props are passed to this component – from a parent component like UserSignUp – to provide it the data it needs.
```jsx

export default (props) => {
  const {...} = props;

  function handleSubmit(event) {
    event.preventDefault();
    submit();
  }

  function handleCancel(event) {
    event.preventDefault();
    cancel();
  }

  return (
    <div>
      <ErrorsDisplay errors={errors} />
      <form onSubmit={handleSubmit}>
        { elements() }
        <div className="pad-bottom">
          <button className="button" type="submit">{submitButtonText}</button>
          <button className="button button-secondary" onClick={handleCancel}>Cancel</button>
        </div>
      </form>
    </div>
  );
}
```
**Write the Submit Functionality**
Let's write the submit function that creates a new user and sends their credentials to the Express server. A new user will be created using the state initialized in the UserSignUp class and the createUser() method defined in Data.js. Remember, the UserSignUp component is now a component "with context", meaning it's subscribed to the application context – in fact the data is passed to the component via a prop named context.
1. Open the file UserSignUp.js.
2. Destructure props and state. In the body of the submit function (line 74), use destructuring assignment to extract the context prop from this.props, and unpack the name, username and password properties from the state object (this.state) into distinct variables
3. Initialize a variable named user to an object whose properties are name, username and password:
```jsx
  submit = () => {
    const { context } = this.props;
    const {
      name,
      username,
      password,
    } = this.state; 

    // New user payload
    const user = {
      name,
      username,
      password,
    };
  }
```
This user object is the new user payload that will be passed to the createUser() method. It uses the ES2015 object shorthand syntax to include the just the key names because the values have the same name as the keys.

**Create User**
To create a new user, call the createUser() method, which you can access via the destructured context variable. Context itself is an object which currently has only one property, data. Earlier, in Context.js, you passed Context.Provider a value prop whose value was an object with a data property. The authentication API utilities provided to app are available via the context.data property.
1. Call the createUser() method with context.data.createUser(). createUser() accepts one argument, which is the new user payload
2. Pass the method the user object as the argument:
createUser() is an asynchronous operation that returns a promise. The resolved value of the promise is either an array of errors (sent from the API if the response is 400), or an empty array (if the response is 201).
3. Get the value out of the returned promise. Chain a then() method to createUser():
In the then() method, we'll check if the returned PromiseValue is an array of errors. If it is, we will set the errors state of the UserSignUp class to the returned errors.
4. Pass then() an arrow function that takes the fulfillment value as a parameter named errors:
If, for instance, a user submits an empty sign up form, the API returns a response status of 400 as well as an array of validation error messages.

In the body of the function, we'll check **if** there are items in the array returned by the Promise, using `errors.length.` If there are items in the array, it means that there are errors to display to the user.
5. In the if block, use setState() to update the errors state to the returned errors:
```jsx
 submit = () => {
    ...
    context.data.createUser(user)
     .then( errors => {
       if (errors.length) {
         this.setState({ errors });
       }
     })
   }
```
If the response returns no errors (or an empty array) it means that a new user was successfully created and sent to the server.

6. Add an else statement that logs a 'success' message to the console for now, displaying the username created:

Sheila Anguiano
 React Authentication
Instruction
#### Implement the Sign up Form
In this step, we'll begin implementing the sign up form that connects to the Express server and creates an authenticated user.

##### Getting to Know 'UserSignUp.js'
The file contains a UserSignUp class that employs the "render prop" technique in React to render a form. Notice how the component <Form> uses an elements prop whose value is a function which returns the input fields to be used in each of the forms:
```jsx
export default class UserSignUp extends Component {
  ...
  render() {
    ...
    return (
      ...
        <Form 
          ...
          elements={() => ( // render prop
            <React.Fragment>
              <input ... placeholder="Name" />
              <input ... placeholder="User Name" />
              <input ... placeholder="Password" />
            </React.Fragment>
          )} /> 
    )
  }
  ...
}
```
In this case, there is an input field for name, username and password.

##### Review `Form.js`
The file components/Form.js exports a function that renders any validation errors sent from the API, via the <ErrorsDisplay> function component. It also renders the "Submit" and "Cancel" buttons of a form, as well as handle their functionality, via the functions handleSubmit and handleCancel. Props are passed to this component – from a parent component like UserSignUp – to provide it the data it needs.
```jsx
export default (props) => {
  const {...} = props;

  function handleSubmit(event) {
    event.preventDefault();
    submit();
  }

  function handleCancel(event) {
    event.preventDefault();
    cancel();
  }

  return (
    <div>
      <ErrorsDisplay errors={errors} />
      <form onSubmit={handleSubmit}>
        { elements() }
        <div className="pad-bottom">
          <button className="button" type="submit">{submitButtonText}</button>
          <button className="button button-secondary" onClick={handleCancel}>Cancel</button>
        </div>
      </form>
    </div>
  );
}
```
Write the Submit Functionality
Let's write the submit function that creates a new user and sends their credentials to the Express server. A new user will be created using the state initialized in the UserSignUp class and the createUser() method defined in Data.js. Remember, the UserSignUp component is now a component "with context", meaning it's subscribed to the application context – in fact the data is passed to the component via a prop named context.

##### Open the file UserSignUp.js.
Destructure props and state. In the body of the submit function (line 74), use destructuring assignment to extract the context prop from this.props, and unpack the name, username and password properties from the state object (this.state) into distinct variables:
```jsx
submit = () => {
  const { context } = this.props;

  const {
    name,
    username,
    password,
  } = this.state; 
}
```
This will make the submit handler cleaner and easier to understand.

Initialize a variable named user to an object whose properties are name, username and password:
```jsx
  submit = () => {
    const { context } = this.props;
    const {
      name,
      username,
      password,
    } = this.state; 

    // New user payload
    const user = {
      name,
      username,
      password,
    };
  }
```
This user object is the new user payload that will be passed to the createUser() method. It uses the ES2015 object shorthand syntax to include the just the key names because the values have the same name as the keys.

Create a User
To create a new user, call the createUser() method, which you can access via the destructured context variable. Context itself is an object which currently has only one property, data. Earlier, in Context.js, you passed Context.Provider a value prop whose value was an object with a data property. The authentication API utilities provided to app are available via the context.data property.

Call the createUser() method with context.data.createUser(). createUser() accepts one argument, which is the new user payload.
Pass the method the user object as the argument:
```jsx
  submit = () => {
    const { context } = this.props;
    const { .. } = this.state; 
    const user = { ... };

    context.data.createUser(user)
 }
```
createUser() is an asynchronous operation that returns a promise. The resolved value of the promise is either an array of errors (sent from the API if the response is 400), or an empty array (if the response is 201).

Be sure to have another look at the `createUser()` method in `Data.js` to review its inner-workings.
Get the value out of the returned promise. Chain a then() method to createUser():
```jsx
 submit = () => {
   ...
   context.data.createUser(user)
    .then()
 }
```
In the `then()` method, we'll check if the returned PromiseValue is an array of errors. If it is, we will set the errors state of the UserSignUp class to the returned errors.

Pass then() an arrow function that takes the fulfillment value as a parameter named errors:
```jsx
  submit = () => {
    ...
    context.data.createUser(user)
     .then( errors => {

     })
  }
```
If, for instance, a user submits an empty sign up form, the API returns a response status of 400 as well as an array of validation error messages.

In the body of the function, we'll check if there are items in the array returned by the Promise, using errors.length. If there are items in the array, it means that there are errors to display to the user.

In the if block, use setState() to update the errors state to the returned errors:
```jsx
  submit = () => {
    ...
    context.data.createUser(user)
     .then( errors => {
       if (errors.length) {
         this.setState({ errors });
       }
     })
   }
```
If the response returns no errors (or an empty array) it means that a new user was successfully created and sent to the server.

Add an else statement that logs a 'success' message to the console for now, displaying the username created:
```jsx
  submit = () => {
    ...
    context.data.createUser(user)
     .then( errors => {
       if (errors.length) {
         this.setState({ errors });
       } else {
         console.log(`${username} is successfully signed up and authenticated!`);
       }
     })  
  }
```
**Handle Errors with catch()**
A catch() method chained to the promise sequence handles a rejected promise returned by createUser(). For example, if there's an issue with the /users endpoint, the API is down, or there's a network connectivity issue, the function passed to catch() will get called.

1. Chain the `catch()` method to `then()`.
2. Pass `catch() `an arrow function that takes the parameter `err` (the rejection reason) and logs it to the console, that way we can immediately see the reason why the promise was rejected:
```jsx
context.data.createUser(user)
 .then( errors => {
   if (errors.length) {
     console.log(errors);
   } else {
     console.log(`${username} is successfully signed up and authenticated!`);
   }
 })
 .catch( err => { // handle rejected promises
   console.log(err);
 });  


```
In the event of an error, we will change the current URL from /signup to /error. In other words, redirect the user to another route. Navigating to the /error route will display a "Not Found" message in the browser, providing a user-friendly way to let users know that something went wrong.

**Render and 'Error" Route**
As you learned in the React Router course, a component rendered by <Route> gets passed a history object (via props) that listens for changes to the current URL, keeps track of browser history and the number of entries in the history stack. The history object can also be used to programmatically change the current URL.

You access `history` inside the `UserSignUp` class with this.props.history
1. In the `catch()` method, push a new entry onto the history stack using the `push()` method, which you can access with `this.props.history.push()`.
2. Pass the push() method '/error' as the redirect route:
```jsx
context.data.createUser(user)
 .then( errors => {
   ...
 })
 .catch( err => { 
   console.log(err);
   this.props.history.push('/error'); // push to history stack
 });  

```
React Router lets you create a 404-like error route that displays when a URL's path does not match any of the paths defined in your routes. /error does not match any URL path defined inside the <Switch> component of App.js. Because of this, when the URL path changes to /error, the router is going to render the NotFound component written in components/NotFound.js.

**Write the `cancel` Function**
Now we'll wire up the "Cancel" button to the cancel function defined in UserSignUp.js. This should be straightforward. If a user decides to cancel registration, we will redirect them back to the home route upon clicking "Cancel".

To accomplish the redirect, we'll once again use history. In the body of the cancel function push the root path ('/') onto the history stack:
```jsx
 cancel = () => {
    this.props.history.push('/');
  }
```
Nice work so far, you've come a long way in this stage! You reviewed the fundamentals of basic authentication and how to connect your React client application to an Express REST API. You also created a user registration component that successfully creates a new authenticated user, as well as display validation errors when necessary.

#### Set Up Basic Auhentication
In this step, we will implement an Authorization request header and the Basic authentication scheme to authenticate a registered user. That way the user can use their credentials to sign into the app.

**Require Authentication and Credentials**
1. Open the file `Data.js`. The api() helper method will take two additional arguments that indicate if the request requires authentication and the credentials of the user.
2. After the body parameter, add a parameter named requiresAuth, giving it a default value of false
3. Include a credentials parameter with a default value of null.
We initialize the parameters with default values in case no values or undefined gets passed for either. In the api() method's body, we'll check if an endpoint (or route) requires user authentication
```jsx
api(path, method = 'GET', body = null, requiresAuth = false, credentials = null) {
  ...
}
```
4. Above the return statement, write an if conditional statement that checks if requiresAuth is truthy (or considered true):
```jsx
api(....) {
  ...

  if (body !== null) {...}

  // Check if auth is required
  if (requiresAuth) {    

  }

  return fetch(url, options);
}
```
If we're making a request to a protected route on the server, authentication is required (the `requiresAuth` is true). In that case, we'll encode the user credentials and set the HTTP `Authorization` request header to the Basic Authentication type, followed by the encoded user credentials.

**Encode User Credentials**
In the Basic auth scheme, a server requests authentication information (a user ID and password) from a client. The client passes the authentication information to the server in an Authorization header using base-64 encoding.

1. Initialize a constant named encodedCredentials and set the value to the [`btoa()` method](https://developer.mozilla.org/en-US/docs/Web/API/btoa)

The btoa() method creates a base-64 encoded ASCII string from a "string" of data. We'll use btoa() to encode the username and password credentials passed to the api() method. The credentials will be passed as an object containing username and password properties.

2. Pass `btoa()` a template literal that interpolates the `username` and `password` values of the `credentials` object to produce an encoded string. Be sure to separate each property with a colon (`:`) as shown below:
```jsx
  ...
  if (body !== null) {...}

  if (requiresAuth) {    
    const encodedCredentials = btoa(`${credentials.username}:${credentials.password}`);
  }

  return fetch(url, options);
```
**Implement Authorization**
We'll set an Authorization header on each request that requires authentication by adding an Authorization property to the headers object. You add new properties to existing JavaScript objects the same way you modify them.
1. Add an Authorization property to options.headers as shown below
The `Authorization` request header should hold the credentials to authenticate the client with the server.
2. Using a template literal, set the `Authorization` type to `Basic`, followed by the encoded credentials, stored in the variable `encodedCredentials`
```jsx
  ...
  if (body !== null) {...}

  if (requiresAuth) {    
    const encodedCredentials = btoa(`${credentials.username}:${credentials.password}`);

    options.headers['Authorization'] = `Basic ${encodedCredentials}`;
  }

  return fetch(url, options);
```
Below is an example of what an Authorization header sent to the server might look like using Basic auth and encoded credentials:
```
Authorization: Basic am9lQHNtaXRoLmNvbTpqb2U=
```

**Set Required Auth and Credential Arguments**
The only server request that requires authentication is the `GET` request made to `/users`, which logs in an authenticated user. The `getUser()` method of the Data class calls the `api()` method to return an authenticated user. Let's pass the `api()` method inside `getUser()` values for the `requiresAuth` and `credentials` arguments.
1. Set requiresAuth to true and credentials should be an object containing the username and password information passed to getUser:
2. The getUser() method needs to accept arguments for username and password now that it's passing that data to api():
```jsx
  async getUser(username, password) { // add new parameters
    const response = await this.api(`/users`, 'GET', null, true, { username, password });
    ...
  }
```
Basic auth is all set up on the client side, but there's more work left to do in our React app. Submitting the sign up form does not authenticate the request to `/users `just yet. In the next step, we'll create the `signIn()` function that gets a registered user's credentials from the server, and write the form submit logic in `UserSignIn.js`.

[Authorization](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization)

#### Impement Sign In
In this step, we'll write the signIn() function that retrieves a registered user's credentials from the server, then write a function to log in an authenticated user upon submitting the "Sign In" form.

**Create the Sign in Function**
1. Open the file Context.js. Scroll down to the signIn function, just below the render() method
The `signIn` function is an asynchronous function that takes a `username` and `password` as arguments. `signIn` uses those credentials to call the getUser() method in `Data.js`, which makes a `GET` request to the protected /users route on the server and returns the user data.
2. Start by specifying the parameters username and password in the signIn function definition
3. In the body of the function, initialize a variable named user and set the value to await a promise returned by this.data.getUser():
```jsx
 
  signIn = async (username, password) => {
    const user = await this.data.getUser();

  }
```
The returned `PromiseValue` will be an object holding the authenticated user's `name` and `username` values. For example:
```jsx
{name: "Guil", username: "guil@guil.com"}
```
4. Pass the getUser() method the user credentials with the arguments username and password
5. Set `signIn()` to return the user object stored in the variable `user`
That's all the signIn behavior we need for now. We'll revisit this function in a later step to set and store the user data in a cookie, and update state to the authenticated user. This will maintain the user's authenticated state across multiple requests and page refreshes.

**Pass the `singIn` Function to the Provider**
It's common to pass the Provider's value prop an actions object to store any event handlers or actions you want to perform on data that's passed down through context. Next, we'll need to pass the signIn function to <Context.Provider>, that way we can call it within any component that's connected to context changes.

Above the return() statement is the value object containing the context to be shared throughout the component tree.
1. Add a new property named actions, and set it to an object
2. Store the signIn function in a property named signIn; the value should be a reference to the function: this.signIn:
```jsx
const value = {
  data: this.data,
  actions: { // Add the 'actions' property and object
    signIn: this.signIn
  }
};

return (
  <Context.Provider value={value}>
    {this.props.children}
  </Context.Provider>  
);
```
**Subscribe the `UserSignIn` Component to Context**
As we did earlier with the UserSignUp component, we'll subscribe (or connect) the UserSignIn component to context – in other words, the data and actions to be shared throughout the component tree.
1. Open the file `App.js`. Below the `UserSignUpWithContext` variable, initialize a variable named `UserSignInWithContext` whose value calls `withContext(UserSignIn)`:
2. Render `UserSignInWithContext`. In the sign in route, change the component to render when the URL path matches /signin from UserSignIn to UserSignInWithContext:
```jsx
import withContext from './Context';

const UserSignUpWithContext = withContext(UserSignUp);
//conect UserSignIn to context
const UserSignInWithContext = withContext(UserSignIn);

export default () => (
  <Router>
    <div>
      <Header />

      <Switch>
        <Route exact path="/" component={Public} />
        <Route path="/authenticated" component={Authenticated} />
        <Route path="/signin" component={UserSignInWithContext} />

```
The UserSignIn component now has access to the signIn function, as well as any data or actions passed to <Context.Provider value={value}>.

##### Create the Submit Function
The `submit()` function will log in an authenticated user upon submitting the "Sign In" form. Most of the logic for this function will resemble what we wrote for the "Sign Up" form.
1. Open the file `components/UserSignIn.js`. The UserSignIn component is also a component "with context", meaning it's subscribed to the application context – the data is passed to the component via a context prop.
2. In the body of the submit function, let's again use destructuring assignment to extract the context prop from this.props
3. To make the function cleaner, unpack the username and password properties from the state object (this.state) into distinct variables – these are the properties needed to sign in a user
4. Call the `signIn()` function, which you can access via the destructured `context` variable. In `Context.js`, you passed `Context.Provider` a value prop whose value was an object with an actions property. The `signIn()` function provided to the `UserSignIn` component is available via context.actions.signIn
5. The `signIn` function accepts two arguments, username and password, to log in a registered user
`signIn()` is an asynchronous operation that calls the `getUser` API method (written in Data.js) and returns a promise. The resolved value of the promise is either an object holding the authenticated user's name and username values (sent from the API if the response is 201), or null (if the response is a 401 Unauthorized HTTP status code). Be sure to have another look at the getUser() method in Data.js to review its inner-workings.
6. Get the value out of the returned promise by chaining a then() method to signIn
7. Pass then() an arrow function that takes the fulfillment value as a parameter named user
8. Inside then(), check if the returned PromiseValue is strictly equal to null (or a response of 400)
9. If the returned promise value is null, set the errors state of the UserSignIn class to an array which holds the string 'Sign-in was unsuccessful' (this will be the validation message displayed to the user):
If the response returns the user object (response status is 200), use history and the push() method to navigate the user from the /signin route to the /authenticated route, which will render the "Authenticated" view to let them know sign-in was successful.
10. Inside an else block, call this.props.history.push(), passing it '/authenticated' as the redirect route
11. To view the authenticated username (and know that registration worked), log a "Success" message to the console that displays the username

```jsx
submit = () => { 
    const { context } = this.props;
    const { username, password } = this.state;
    context.actions.signIn(username, password)
      .then( user => {
        if(user === null){
          return {errors: ['Sign-in was unsucccessful']};
        } else {
          this.props.history.push('/authenticated');
          console.log(`SUCCESS! ${username} is now signed in!`);
        }
      })
  }

```
##### Catch Errors
Like we did earlier in the UserSignUp component, we'll chain the catch() method to the promise sequence to handle a rejected promise returned by signIn().
1. Chain the `catch()` method to `then()`
2. Pass `catch()` an arrow function that takes the parameter `err` (the rejection reason) and logs it to the console.
3. In the event of an error, again use history and the push() method to navigate the user from /signin to /error, providing a user-friendly way to let them know that something went wrong:
```jsx
.catch( err => {
        console.log(err);
        this.props.history.push('/error');
      })
```
##### Write the "Cancel" Function
Let's wire up the "Cancel" button to the cancel function defined in UserSignIn.js. This function will be the same as the cancel function defined in UserSignUp.js. Feel free to copy that code and paste it inside the cancel function of the UserSignIn class.

If a user decides to cancel sign-in, we will redirect them back to the home route upon clicking "Cancel". To accomplish the redirect, push the root path ('/') onto the history stack:
```jsx
 cancel = () => {
    this.props.history.push('/');
  }

```
#### Display Authenticated User in the Header
Currently, when a registered user logs in (via the "Sign In" form), there are no visual changes in the user interface to let them know that they are authenticated (or logged in). Now that we have a way to authenticate and identify users, we can associate data with specific users.

When an authenticated user logs into the app, we'll display a "Welcome" message in the header using their name. We'll also replace the "Sign In" link with a "Sign Out" link.

##### Connect the Header to Context
The `Header` component needs to be subscribed to the context changes provided by `Context.js`. The data passed to `Header` will determine whether it renders the "Welcome" message displaying the user's name, or the "Sign In" and "Sign Up" links displayed by default.

1. In App.js, initialize a variable named HeaderWithContext and set the value to withContext(Header)
Like other components "with context," we've provided the `Header` component access to the data and actions passed to <Context.Provider value={value}>
```jsx
...
import withContext from './Context';

// Connect the Header component to context
const HeaderWithContext = withContext(Header);
const UserSignUpWithContext = withContext(UserSignUp);
const UserSignInWithContext = withContext(UserSignIn);
```
2. Inside <Router>, change the <Header /> JSX tag to <HeaderWithContext />:
```jsx
export default () => (
  <Router>
    <div>
      <HeaderWithContext />

      <Switch>...</Switch>
    </div>
  </Router>
);
```
##### Authenticated User State
You've learned that in React, "state" is the data you want to track in your app. State allows you to create components that are dynamic and interactive, and it's the only data that changes over time. Next, we're going to initialize an `authenticatedUser` state to determine what content gets presented to the user.

If `authenticatedUser` is `null` (there is no authenticated user), we'll display the default header. Otherwise, we'll display the user name in the header in a "Welcome" message alongside a "Sign Out" link.

1. In `Context.js`, initialize an `authenticatedUser` state in the `Provider` class. Set the default state to `null`:
```jsx
export class Provider extends Component {

  state = {
    authenticatedUser: null
  };

  ...
}
```
2. In the render() method, use destructuring assignment to extract authenticatedUser from this.state
3. Pass state to <Context.Provider> by adding the `authenticatedUser` variable to the value object
```jsx
  render() {
    const { authenticatedUser } = this.state;

    const value = {
      authenticatedUser,
      data: this.data,
      actions: {
        signIn: this.signIn
      },
    };
    ...
  }

```
##### Conditionally Render the Header Nav
The `Header` class in `Header.js` now receives the `authenticatedUser` state via context and props, `with this.props.context.authenticatedUser`. We will use this data to determine what to display to the user.

1. In the render() method of the Header class, extract context from this.props to make the data easier to manage
2. Store the authenticatedUser data in a variable named authUser
The value of `authUser` is either an object holding the authenticated user's `name` and `username` values, or `null`. In the return statement we'll conditionally render the header nav content based on the value of `authUser` (the `authenticatedUser` state).

```jsx
export default class Header extends React.PureComponent {
  render() {
    const { context } = this.props;
    const authUser = context.authenticatedUser;
    ...
  }
  ...
}
```
3. Between the <nav> tags, open a JSX expression using curly braces ({ })
4. Inside the curly braces, use a conditional (ternary) operator to render content representing the current state, using the value of authUser as the condition.
5. If `authUse`r evaluates to a truthy value (there is an authenticated user in state), the `Header` class renders a <span> element containing a "Welcome" message that displays the user name. Render the user's name with {`authUser.name`}
When a user is logged in, we should provide them a way to log out.
6. Below the span tag, add a <Link> component that navigates the user to the path /signout. The link should display the text "Sign Out"
7. If authUser is falsy (the authenticatedUser state is null, for example), the Header class renders the default navigation, displaying the "Sign Up" and "Sign In" links

```jsx
<nav>
  {authUser ?
    <React.Fragment>
      <span>Welcome, {authUser.name}!</span>
      <Link className="signout" to="/signout">Sign Out</Link>
    </React.Fragment>
  :    
    <React.Fragment>
      <Link className="signup" to="/signup">Sign Up</Link>
      <Link className="signin" to="/signin">Sign In</Link>
    </React.Fragment>
  }
</nav>

```
That's all the code we need to include in Header.js. Next, when a registered user logs into the app, we will update the authenticatedUser state. The value in state will be a user object holding the authenticated user's name and username.

##### Update State on Sign in
In the Context.js file, the `signIn` function of the `Provider` class currently returns `null` or the authenticated user via the `getUser()` method. The data is stored in the variable `user` which, as you learned earlier, is either null or an object holding the authenticated user's name and username values. For example:
```jxs
{name: "Guil", username: "guil@guil.com"}
```

1. Update the `authenticatedUser` state upon sign in with a conditional statement that checks if the value of user is not equal to null
2. The value of user is not null, update the authenticatedUser state to the value of user
```jsx
  signIn = async (username, password) => {
    const user = await this.data.getUser(username, password);
    if (user !== null) {
      this.setState(() => {
        return {
          authenticatedUser: user,
        };
      });
    }
    return user;
  }
```
### React Router Authentication
#### Protect Routes that Require Authentication
You'll often need to protect certain routes in your application from unauthorized users. For instance, the `/authenticated` route would likely display private information that we don't want unauthorized (or logged-out) users to view.

Currently, the '/authenticated' route is accessible to any user, whether they are authenticated or not. This is likely not what you or your users would expect; the route should be private to authenticated users only.

In this step, you will use React Router to control what users can and cannot view in your application based on their identity. You will create a routing feature that allows only logged-in users to view the /authenticated page. Users who are not authenticated will be redirected to the /signin page.

##### Set up the Private Route
1. In `App.js`, import the PrivateRoute component (located in the src folder)
2. Within the <Switch> tags, change the <Route> tag that renders the Authenticated component to <PrivateRoute>
```jsx
  <Switch>
    <Route exact path="/" component={Public} />
    <PrivateRoute path="/authenticated" component={Authenticated} />
    ...
  </Switch>

```
##### Review PrivateRoute.js
The `PrivateRoute` component will serve as a high-order component for any routes that you want to protect and make accessible to authenticated users only. The component will either allow the user to continue to the specified private component, or redirect them to the sign in page if they are not logged in.
<PrivateRoute> will work similar to how <Route> works. It will render the private component passed to its component prop when the URL matches the specified path. Let's go over the code for this function component.
1. Open the file `src/PrivateRoute.js`. The function first destructures and renames the component prop in its parameters. It also collects any props that get passed to it in a ...rest variable:

```jsx
import React from 'react';
import { Route, Redirect } from 'react-router-dom';
import { Consumer } from './Context';

export default ({ component: Component, ...rest }) => {
  return (
    <Consumer>
      { context => (
        <Route
          {...rest}
          render={}
        />
      )}
    </Consumer>
  );
};
```
2.  Inside `return()`, the <Consumer> component subscribes PrivateRoute to all the actions and data provided by Context.js
In this case, a <Route> component is rendered inside the consumer and any specified props (like path) are passed to it via ...rest.

##### Redirect the User
The <Route> component utilizes a "render prop" to render either the protected component or a redirect.
Anything rendered within <Consumer> is connected to context changes, which means that <Route> has access to the `authenticatedUser` state (via context.authenticatedUser). The value of `context.authenticatedUser` is either an object holding the authenticated user's name and username, or null.
1. In the render prop, check whether or not the user is authenticated (there is an authenticated user in state)
If the user is authenticated, the component specified in <PrivateRoute>'s component prop gets rendered.
```jsx
...
    <Consumer>
      {context => (
        <Route
          {...rest}
          render={props => context.authenticatedUser ? (
              <Component {...props} />
            )
          }
        />
    )}
    </Consumer>
  );
```
2. If the user not authenticated, redirect to /signin:
The <Redirect> component instructs the router to redirect from one route to another. The value passed to its to prop specifies the URL to redirect to – in this case /signin.
```jsx
export default ({ component: Component, ...rest }) => {
  return (
    <Consumer>
      { context => (
        <Route
          {...rest}
          render={ props => context.authenticatedUser ? (
            <Component {...props} />
          ) : (
            <Redirect to='/signin'/>
          )
          }
        />
      )}
    </Consumer>
  );
};
```
##### Connect the `Authenticated` Component to Context
The `Authenticated` component is currently not subscribed to context, which means that it does not have access to the authenticatedUser state and is not able to display custom content to the user. Header, for example, uses context to render a "Welcome" message displaying the authenticated user's name.

To display custom content in the private Authenticated component (like a user's name and username), we'll need to subscribe the component to context.

1. In `App.js`, initialize a variable named AuthWithContext with a value of withContext(Authenticated)
2. In the <PrivateRoute> JSX tag, change the value of the `component` prop from `Authenticated` to `AuthWithContext`:
```jsx
<Switch>
    <Route exact path="/" component={Public} />
    <PrivateRoute path="/authenticated" component={AuthWithContext} />
    ...
  </Switch>
```
3. Open the file `components/Authenticated.js`. The value of the authenticatedUser state is now available to this function via props.context.authenticatedUser.
4. To make things cleaner, extract the context property from props in the function's parameters
5. Store the authenticatedUser data in a variable named authUser.
6. In the return statement, display the authenticated user's name in the heading, and the username in a paragraph, using the name and username properties provided by context:
```jsx
import React from 'react';

export default ({ context }) => {
  const authUser = context.authenticatedUser;

  return (
  <div className="bounds">
    <div className="grid-100">
      <h1>{ authUser.name } is authenticated!</h1>
      <p>Your username is {authUser.username}.</p>
    </div>
  </div>
  );
}
```
#### Impement User Sign Out
User authentication would not be complete without a sign out feature that provides a way to let users log out of your app.

In this step, we'll write a signOut function that sets the authenticatedUser state back to null when invoked. We'll also implement a /signout route and a UserSignOut component that redirects the user to the main public page upon logging out.

##### Write the Sign Out Function
1. Open the file Context.js. At the bottom of the Provider class is an empty function named signOut (below the signIn function):
2. Inside the body of the signOut function, use this.setState() to update the authenticatedUser state to null:
This removes the name and username properties from state – the user is no longer authenticated and cannot view the private components.
Like the `signIn` function, we will need to pass the `signOut` function as an action to <Context.Provider> to make it available to all components connected to context changes.
```jsx
 signOut = () => {
    this.setState({authenticatedUser: null });
  }
```
3. In the `value.actions` object, store the `signOut` functions in a property name `signOut` and set the value to reference the function, with this.signOut:
```jsx
  const value = {
      authenticatedUser,
      data: this.data,
      actions: {
        signIn: this.signIn,
        signOut: this.signOut
      },
    }
```
##### Connect the `UserSignOut` Component to Conext
The "Sign Out" link in the Header component navigates the user to the `/signout` URL path, so let's now declare the `/signout` route in `App.js`.

1. Initialize a variable named UserSignOutWithContext to withContext(UserSignOut)
This subscribes the UserSignOut component to context changes, that way we'll be able to reference the `signOut` action (which calls the signOut function) from within the component
2. Update the sign out <Route> to render `UserSignOutWithContext` when the URL path is /signout:

```jsx
import React from 'react';
import {
  BrowserRouter as Router,
  Route,
  Switch
} from 'react-router-dom';

import Header from './components/Header';
import Public from './components/Public';
import NotFound from './components/NotFound';
import UserSignUp from './components/UserSignUp';
import UserSignIn from './components/UserSignIn';
import UserSignOut from './components/UserSignOut';
import Authenticated from './components/Authenticated';

import withContext from './Context';
import PrivateRoute from './PrivateRoute';

const HeaderWithContext = withContext(Header);
const AuthWithContext = withContext(Authenticated);

const UserSignUpWithContext = withContext(UserSignUp);
const UserSignInWithContext = withContext(UserSignIn);
const UserSignOutWithContext = withContext(UserSignOut);

export default () => (
  <Router>
    <div>
      <HeaderWithContext />

      <Switch>
        <Route exact path="/" component={Public} />
        <PrivateRoute path="/authenticated" component={AuthWithContext} />
        <Route path="/authenticated" component={Authenticated} />
        <Route path="/signin" component={UserSignInWithContext} />
        <Route path="/signup" component={UserSignUpWithContext} />
        <Route path="/signout" component={UserSignOutWithContext} />
        <Route component={NotFound} />
      </Switch>
    </div>
  </Router>
);

```
##### Redirect the User to the Root Route on Sign-out
The file `UserSignOut.js` contains a function component we'll use to call the `signOut()` action and redirect the user to the root path ('/').
1. Open the file components/UserSignOut.js
2. Extract the `context` property from `props` in the function's parameters
3. In the body of the function, call the signOut() action passed down through context
4. Return a <Redirect> component that redirects the user to the root path ('/')
```jsx
import React from 'react';
import { Redirect } from 'react-router-dom';

export default ({ context }) => {
  context.actions.signOut();
  return (
    <Redirect to="/" />
  );
}

```
##### Now you can test User Sign-Out
The router should navigate to the /signout path and render the UserSignOut component, which immediately redirects to the main public page.

##### Important Update
In the latest version of React, the following warning will appear in your browser's JavaScript console when signing out of the application:
```
index.js:1 Warning: Cannot update during an existing state transition (such as within `render`). Render methods should be a pure function of props and state.

```
Why the warning: 
While rendering, the UserSignOut component calls the signout() action to update the application's authenticatedUser state.

Developers refer to these types of actions as "side effects" and React now warns that you shouldn't perform them during rendering.

This state update should happen after the UserSignOut component renders. React now provides a straightforward way to do that with the useEffect Hook.

Update the code in UserSignOut.js as shown below:
```jsx
import React, { useEffect } from 'react';
import { Redirect } from 'react-router-dom';
export default ({context}) => {
  // component calls signOut and updates state after render
  useEffect(() =>  context.actions.signOut());

  return (
    <Redirect to="/" />
  );
}

```
After the component renders, the signOut action gets called to logout the user. Learn more about useEffect in our React Hooks workshop.

#### Refine and Complete Authentication
The authentication feature of the React app is effectively complete. We're successfully registering users, and providing ways for them to log in and out.

Currently, when a user submits the registration form on the "Sign Up" page, the app in no way indicates whether they registered successfully. Also, they need to click the "Sign In" link then submit the form to log into the app.

In this step, we'll further refine the registration and sign in experience by automatically signing in the user upon successful registration.

##### Updating the `submit` Function
The submit() function we wrote earlier only logs a 'success' message to the console if the createUser() method returns no errors. After creating the user, we're also going to sign in the user to retrieve the user data from the API and maintain the user's authenticated state. We'll accomplish this using the signIn() function provided by context.
1. Open the file UserSignUp.js
2. In the else block, call signIn(), with context.actions.signIn(). The signIn function accepts two arguments, username and password, to log in a registered user
```jsx
submit = () => {
  ...
    context.data.createUser(user)
      .then( errors => {
        if (errors.length) {
          this.setState({ errors });
        } else {
          context.actions.signIn(username, password)
        }
      })
      .catch((err) => {...});
}
```
As you learned earlier, signIn() is an asynchronous operation that returns a promise. Once the promise is fulfilled (the user was authenticated), we'll navigate the user to the /authenticated URL path.
3. Chain a then() method to signIn(username, password)
Once the authenticated user is in state, we'll push a new entry onto the history stack to navigate the user to the `/authenticated` route.
4. Pass then() a function that calls this.props.history.push('/authenticated')`:
This renders the `Authenticated` component which displays that registration was a success.
5. Test the Sign Up Redirect: Clicking the "Sign Up" button should navigate you to the /authenticated route and display the private Authenticated component.

##### Smarter Redirect for Unauthenticated Users
There's one more improvement we can make to the sign in experience. Currently, a logged-out (or unauthenticated) user who tries to visit /authenticated gets redirected to /signin via the <PrivateRoute> component. Once they sign in, they can access /authenticated.

Our simple app currently has only one private route ( /authenticated), but it's likely that a larger app will have many routes that are private to unauthenticated users. In that case, we'd need to provide a smarter, more efficient login redirect for users.

For example, let's say that our app also has the private route /settings. A user who isn’t authenticated tries to access /settings and is redirected to the "Sign In" page. The user submits the sign in form, and instead of redirecting to /settings (the page they want to access) they redirect to /authenticated. A better experience would be to redirect the user back to the page they were trying to access once they're authenticated. React Router's <Redirect> component provides a simple way to achieve this!

##### Update the <Redirect> Component
1. Open the file PrivateRoute.js.
2. In the <Redirect />component, change the to prop from a string to an object
The object contains information about the path to redirect to (if not authenticated), and the route the user was trying to access before being redirected.
3. To redirect an unauthenticated user to the "Sign In" page, pass the object a pathname property and set the value to '/signin'
4. Pass a state property whose value is the current location of the route the user tried to access
The `state` property holds information about the user's current location (i.e., the current browser URL). That way, if authentication is successful, the router can redirect the user back to the original location (from: props.location).

Since pathname: '/signin' renders the UserSignIn component on redirect, you can access from via this.props.location.state.from within the UserSignIn component

##### Update the UserSignIn Component
In the UserSignIn component, we'll need to update the submit() function. If the user is redirected to `/signin` from a previous route, `submit()` should navigate them back to the original route once they authenticate.
Update the submit() function as shown below:
```jsx
submit = () => {
  const { context } = this.props;
  const { from } = this.props.location.state || { from: { pathname: '/authenticated' } };
  const { username, password } = this.state;

  context.actions.signIn(username, password)
   .then( user => {
     if (user === null) {
       ...
     } else {
       this.props.history.push(from);
     }
   })
   .catch((error) => {...});
}
```
The `from` variable passed to `history.push(from)` contains information about the pathname an unauthenticated user redirected from (via `this.props.location.state`). For example, if a user redirects to the sign up page from `/settings`, `from` will be equal to pathname: "/settings".

If a user submits the sign in form without previously visiting a protected route, they will navigate to `/authenticated` by default. You can learn more about the pathname, state and from properties in the resources below.

##### Test Redirect
1. Declare a new <PrivateRoute /> in App.js. For example, /settings
2. Click the "Sign Out" link in the header to make sure that you are logged out.
3. Try to access /settings. This should redirect you to /signin.
4. Submit the sign in form. You should redirect back to /settings.

#### Preserve the User State with Cookies
