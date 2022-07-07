# React

# Table of Contents
1. [React Basics](#react)
2. [React Components](#components)
3. [React Router 4](#react-router)



## React Basics <a name="react"></a>
### First Steps in React
#### Introducing React
React is a JavaScript library for building user interfaces.It introduces  a more efficent and flexible way of building organizing and mantaining your user interface code (UI) code.

One of the main venefits of working with React, is that it lets you build your application's UI by breaking it up into small reusable pieces of code called **components**

The other big benefit is that React leeps your application's data or state and UI in-sync and can efficiently update your UI when data changes.





At its simplest, React is a library for creating and updating HTML elements.
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
