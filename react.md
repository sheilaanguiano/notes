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