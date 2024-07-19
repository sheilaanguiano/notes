# Redux

**Redux** is a state management library for JavaScript apps. It can be used with React, Angular, Vue and Vanilla JS because Redux is a state management

When an application UI needs to keep track of cosntantly changing data that flows through different components, this data could act in umpredictable ways or even enter infinite loops. Facebook encountered this problem and 
came up with an architectural pattern called *flux*. Redux is inspired by Flux but it has grown more popular due to its simplicity and elegance

**State Management Solutions**
- Flux
- Redux
- MobX

With Redux instead of scaterring application state in varios parts of the UI, we store all of the application State inside a central repository, that is a single JavaScript object called the **Store** that is the single source of Truth, you can think of it as a database for the front end, so with this architecture the different pieces of the UI will no longer maintain their own state, instead they get what they need for the store. If we need to update the data there is a single place we have to update, so this immediately solves the problem of synchronizing the data accross different parts of the UI, but Redux architecture also makes it easier to understand how the data changes in our applications if something goes wrong, we can see exactly how the data changed. How, why, when and where it came from

**Redux in a Nutshell** 
* Centralized application's state
* Makes data flow transparent and predictable

*Redux Dev Tools Chrome Extension*
We're going to work on a restaurant app. Imagine that you start adding items and suddenly you delete one, with *Time Travel Debbuging* you can return to how the previous UI lookled like.

We cal also sabe the entire application state in a file and reload the application from it later.

The tool *Log Rocket* gives you an always on Redux Dev Tools in production for everyone of your users, so if a user encounters a proble you can reload the application in the same state as the user and see what's going on. It's very powerful.

Another benefit of Redux is that it allows you to cash or preserve paid state, like download all the app, so whenever you change screen it doesn't pull anything from the server averything is there.

**Pros**
* Predictable state changes
* Centralize state
* Easy debbuging
* Preserve page state
* Implement Undo / Redo features easily
* Great ecosystem of add-ons

**Cons**
* Introduces Complexity
* Verbosity

### Is Redux for you?
In every project or app you need to understand whay problem you're trying to solve, what your constrains are and what solution optimally solves the problem according to those constrains

**When NOT to use Redux**
* Yight budget
* Small to medium-size apps
* Simple UI / data flow
* Static data

### Functional Programming
Functional programming is one of the many programming paradigms or styles of programming

**Programming Paradigms**
* Functional
* Object-oriented
* Procedural
* Event-driven

Each of these paradigms has certain rules about how you should structure your code to solve problems. Functional Programming was invented in the 1950s but it has become quite trendy over the few years.

In a nutshell functional programming is about decomposing a problem into a bunch of small and reusable functions that take some input and return a result. They don't don't mutate or change data. With this structure we can compose these functions to build more complex functions. 

The benefit of this is that these small functions are more concise, easier to debug, easier to test and more scalable because we can run many function call in parallel and take advantage of multiple cores  of a CPU

There are languages that are specifically designed for functional programming such as 
* Clojure 
* Haskell

JavaScript is a multi-paradigm programming language, it's not a pure functional language, so it has some *caveats* that you need to be aware but we can still apply frunctional programming principles

#### Functions are first class citizens
* Functions can be assigned to a variable
* Functions can be passed as an argument
* Functions could be returned from other functions

#### Higher order functions
Is a function that takes a function as an argument or returns one or both
```javascript
setTimeout(() => console.log("Hello"), 1000);
```
#### Function Composition
The idea of Functional programmins it to write a bunch of small reusable functions and then compose them to build more complex functions for solving real world problems.

For example let's say we have an input and what we want to accomplish in an output:
```javascript
let input = "   Javascript  "
let output = "<div>" + input + "</div>";

```
The above example of output is a NON functional way of solving the problem, now let's return the same result by using Functional programming:
```javascript
const trim = str => str.trim();
const wrapInDiv = str => `<div> ${str}</div>`
// Let's add that we want the string to be lowercase
const toLowerCase = str => str.toLowerCase();

const result = wrapInDiv(toLowerCase(trim(input)));
```
This is called Composition

#### Composing and Piping
**Lodash** is a javaScript utility library for JavaScript, which has a package with functions for functional programming

```javascript
import { compose, pipe } from "lodash/fp";

const trim = str => str.trim();
const wrapInDiv = str => `<div> ${str}</div>`
const toLowerCase = str => str.toLowerCase();

//const result = wrapInDiv(toLowerCase(trim(input)));
const transform = compose(wrapInDiv, toLowerCase, trim) //Higher order function 
transfor(input);
```
With this new function from Lodash we have cleaner functions, but we still need to reed from righ to left to follow for the string transform. This can be changed with *pipe*
```javascript
const transform = pipe(trim, toLowerCase,wrapInDiv) 
transfor(input);
```

#### Currying
Named after Haskell Curry. Let's same that name we want a String in a Span, so we create the small function for it
```javascript
const trim = str => str.trim();
const wrapInDiv = str => `<div> ${str}</div>`;
const wrapInSpan =  str => `<span> ${str}</span>`;
const toLowerCase = str => str.toLowerCase();

const result = wrapInDiv(toLowerCase(trim(input)));
```
Now we have a bit of duplication, so it would be nice it we could parametize this function