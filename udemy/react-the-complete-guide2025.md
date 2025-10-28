# React - The Complete Guide 2024

---

Platform: Udemy
Instructor: Maximilian Schwarzmuller
Author: Sheila Anguiano

---

# Table of Contents

1. [Getting Started](#intro)
2. [JavaScript Refresher](#refresher)
3. [React Essentials - Components, JSX, Props, State and More](#essentials)
4. [React Essentials - Deep Dive](#deepdive)

---

## 1. Getting Started <a name="intro"></a>

### ReactJS vs Vanila JS

React = Declarative UI Programming.
With React, you define the target UI state(s)- not the steps to get there. Instead, React will figure out & perform the necessary steps.

When you write vanilla JavaScript, you write Imperative code, which means, you're not defining the goal, but the steps neeeded to get there.

https://codesandbox.io/p/sandbox/first-react-app-start-7ec9fd?file=%2Fsrc%2Findex.js

### Creating React Projects

- Code Sandbox: Type `react.new` in the browser URL bar, to have a react workspace with an in-browser development environment

- Use vite `npm create vie@latest react-project-name`, followed by `npm install` and then run `npm run dev` to start a development server
- Use create-react-app

## 2: JavaScript Refresher <a name="refresher"></a>

### Module Introduction

There is another way to add the javascript file aside from adding it right before the closing body tag, which is inside the head:

```
<head>
<script src="assets/scripts/apps.js" defer></script>
</head>
```

In moder JavaScript you might also find the same script tag with a `type="module"`

And if you're treating your JavScript as modules, this unlocks a very important syntax, which is using the word `import`.

In the context of building React apps, you will almost never add these scripts tags to your HTML file on your own, because React projects almos always use a **build process** which as part of that build process, injects these script tahs into the HTML code for you.

## 3. React Essentials - Components, JSX, Props, State and More <a name="essentials"></a>

### It's all about Components

React and its ecosystem provide dozens of useful and important features and concepts, but arguably the most important concept is the concept of a Component.

Components are UI Building Blocks.So React apps are in the end built by combining Components

- Reusable Building Blocks
  - Create small building blocks and compose the UI from them
  - Reuse a building block in different parts of the UI
- Related Code Lives Together
  - Related HTML and JS code stored together
- Separation of concerns
  - Different components handle different data and logic
  - Vastly simplifies the process of working on complex apps

This concept is so popular and useful that you'll find it in other popular front-end frameworks like Angular, Vue or Svelte.
Or even in mobile development frameworks like Flutter.

### JSX & React Components (Core Concept)

- JSX : JavaScript Syntax Extension
- With React, you write declarative code. You define the target HTML structure & UI, not the steps to get there
- In React a component is really just a JavaScript function, though in order to be recognized and used as a Component by React, it needs to follow 2 rules:
  - The function name must start with an uppercase character
  - Must return a renderable value, typically the to-be-rendered HTML markup
- VSC Shortcut: Shift + option + F = Format Document (Text needs to be highlighted)

```javascript
function Header() {
  return (
    <header>
      <img src="src/assets/react-core-concepts.png" alt="Stylized atom" />
      <h1>React Essentials</h1>
      <p>
        Fundamental React concepts you will need for almost any app you are
        going to build!
      </p>
    </header>
  )
}

function App() {
  return (
    <div>

      <main>
        <h2>Time to get started!</h2>
      </main>
    </div>
  );
}

export default App;
```
After creating a component like `Header`, you would think to execute it like Header(), but that's not the case, the React library is the one in charge of calling it

### JSX &  Ract Components
Run the project with `npm run dev`
JSX (JavaScript Syntax eXtension)
React projects come with a build process that transforms JSX code to code that works in borwsers

In react, a component is reallly just a JavaScript function that needs to follow 2 rules:
1. Name starts with and Uppercase character
2. Returns  "renderable" value or content

### Components & File Extensions

.jsx is a file extension that's not supported by the browser! It's working because you're working in a React project that supports this special extension. Because this extension "tells" the underlying build process (which is running behind the scenes when the development server is running) that a file contains JSX code (which is also not supported by browsers).

It's important to understand that it's really just that build process that cares about this extension.

And therefore, you'll also find React projects that don't use .jsx but instead just .js as a file extension. And in those .js files, you'll also find JSX code. Because it simply depends on the underlying build process which extension is expected when using this JSX syntax in a file.

Since it doesn't work in the browser either way, there is no hard rule regarding this. Instead, you'll find projects that require .jsx (like the project setup we use in this course) and you'll find projects that also support .js (with JSX code inside).

I'm emphasizing this here so that you're not confused if you encounter React projects that don't use .jsx files.

In addition, you'll also find projects that require the file extension as part of file imports (e.g., import App from './App.jsx') and you'll find other projects that don't require this (i.e., there, you could just use import App from './App').

This, again, has nothing to do with the browser or "standard JavaScript" - instead it simply depends on the requirements of the code build process that's part of the project setup you chose.

### How React Handles Components & How it Builds A Component Tree

If we open our project in the browser and look at the `source code` we'll see that the `index.jsx` file is loaded:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <script type="module">
import RefreshRuntime from "/@react-refresh"
RefreshRuntime.injectIntoGlobalHook(window)
window.$RefreshReg$ = () => {}
window.$RefreshSig$ = () => (type) => type
window.__vite_plugin_react_preamble_installed__ = true
</script>

    <script type="module" src="/@vite/client"></script>

    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React Essentials</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/index.jsx"></script>
  </body>
</html>

```

and if we click to `src/index.jsx` we'll be redirected to our transpiled code.

index.jsx

```javascript
import ReactDOM from "react-dom/client";

import App from "./App.jsx";
import "./index.css";

const entryPoint = document.getElementById("root");
ReactDOM.createRoot(entryPoint).render(<App />);
```

In the above file we don't have components. This JSX code is not getting returned by some function. Instead, it's getting used as a value, as an argument for the `render` method. This file acts as the main entry point of our React app since it is the first file to be loaded by the HTML file.

And it's in this place where the React app boots up, you could say. This render method, however, is being called on an object that's created with another method, the `createRoot` method.
This method takes an existing HTML element as an input, so an element that's not being created by React but that instead is part of the index.html file already.

React goes ahead and injects a React component, the App component in this case, including any nested components

So you end up with a component hierarchy or a Tree of Components, but what's important to understand about this tree is that your custom components are not shwoing up in the actual rendered DOM though. There you only find default HTML elements.

\*\* So your tree of components its in the end analyzed by React, and React then combines all the JSX code to generate the overall DOM, which is why you need to write your components with Uppercase letters, this does not just prevent potential name clashes, but it also changes how React handles a component. Built-in component like `<header>`, `<image>`, `<p>` are rendered as DOM nodes by React. On the other hand, custom components like our `<Header>` are just functions and are therefore executed as by React and then it just takes the returned value and analyzes it until it ends up with only built-in elements which are rendered to the screen.

**Built-in components**

- Name starts with a lowercase character
- Only valid, officially defined HTML elements are allowed
- Are renders as DOM nodes by React (ie. displayec on the screen)
  **Custom Components**
- Name starts with uppercase character
- defined by you, "wraps" built-in or other custom components
- React "traverses" the component tree until it has only built-in components left

### Using & Outputting Dynamic Values

**Static Content**

- Content that's hardcoded into the JSX code
- Can't change at runtime

**Dynamic Content**

- Logic that produces the actual value is added to JSX
- Content/value is derived at runtime

Note: if-statements, for-loops, function definitions and other block stateents are not allowed in the curly braces below. Only expressions that directly produce a value

```javascript
const reactDescriptions = ["Fundamental", "Crucial", "Core"];

function getRandom(max) {
  return Math.floor(Math.random() * max + 1);
}

function Header() {
  return (
    <header>
      <img src="src/assets/react-core-concepts.png" alt="Stylized atom" />
      <h1>React Essentials</h1>
      <p>
        {reactDescriptions[getRandom(2)]} React concepts you will need for
        almost any app you are going to build!
      </p>
    </header>
  );
}
```

### Setting HTML Attributes Dynamically & Loading Image Files

Importing an Image the way you do in an HTML, might cause some problems during the bundling process. 

Image files, when loaded like this, might be ignored by the bundling process and therefore they might get lost during deployment as well as not take advantage of extra optimization steps.

```javascript
function Header() {
  return (
  <header>
        <img src="src/assets/react-core-concepts.png" alt="Stylized atom" />
        <h1>React Essentials</h1>
        ...)}
```

So is better to use a JS variable:

```javascript
import reactImg from './assets/react-core-concepts.png';

function Header() {
  return (
  <header>
        <img src={reactImg} alt="Stylized atom" />
        <h1>React Essentials</h1>
         ...)}
```

This is a more optimal way of loading an image

### Making Components Reusable with Props
One of the main advantages of components is that they are reusable and will often build components which might be reusable in theory, but indeed are only meant to be used once but other whole purpose is to be reusable with different data.

React allows you to pass data to components via a concept called "Props".
This props parameter will be set by React because it's React that will execute this function. remember you're not calling these components function yourself in your code, instead you're using them as html elements and under the hood React will call the actual functions.


```javascript
function CoreConcept(props) {
  return (
    <li>
      <img src={props.image} alt={props.title} />
      <h3>{props.title}</h3>
      <p>{props.description}</p>
    </li>
  );
}
function App() {
  return (
    <div>
      <Header />
      <main>
        <section id="core-concepts">
          <h2>Core Concepts</h2>
          <ul>
            <CoreConcept
              title="Components"
              description="The core UI building block"
              image={componentsImg}
            />
            <CoreConcept />
            <CoreConcept />
          </ul>
        </section>
      </main>
    </div>
  );
}

export default App;
```

Therefore, React will pass a value for this props parameter to this function when it calls it and the value that will be passed is an object that has all the value pairs.

### Alternative Props Syntaxes

We're going to add a `data.js` file that we're going to import the following way `import { CORE_CONCEPTS } from './data.js';` since `CORE_CONCEPTS` is a named export in that file, so you need to use curly braces.
So our CoreConcept component would look like this:

```javaScript
<CoreConcept
              title={CORE_CONCEPTS[0].title}
              description={CORE_CONCEPTS[0].description}
              image={CORE_CONCEPTS[0].image}
            />
```

But this is still not optimal, so you can use the spread operator that means the same thing:

```javascript
 <CoreConcept {...CORE_CONCEPTS[0]} />
 <CoreConcept {...CORE_CONCEPTS[1]} />
```

Now talking about shorter alternatives, there is also an alternative for the component function. Here we're accesing the different props, like `props.title`

```javascript
function CoreConcept(props) {
  return (
    <li>
      <img src={props.image} alt={props.tittle} />
      <h3>{props.title}</h3>
      <p>{props.description}</p>
    </li>
  );
}
```

BUT you can also use another feature in the parameter list, you can use object destructuring and it'll work the same, just less writing:

```javascript
function CoreConcept({ image, title, description }) {
  return (
    <li>
      <img src={image} alt={title} />
      <h3>{title}</h3>
      <p>{description}</p>
    </li>
  );
}
```

### More Prop Syntaxes
Beyond the various ways of setting and extracting props about which you learned in the previous lecture, there are even more ways of dealing with props.

But no worries, you'll see all these different features & syntaxes in action throughout the course!

Passing a Single Prop Object

If you got data that's already organized as a JavaScript object, you can pass that object as a single prop value instead of splitting it across multiple props.

I.e., instead of

<CoreConcept
  title={CORE_CONCEPTS[0].title}
  description={CORE_CONCEPTS[0].description}  
  image={CORE_CONCEPTS[0].image} />
or

<CoreConcept
  {...CORE_CONCEPTS[0]} />
you could also pass a single concept (or any name of your choice) prop to the CoreConcept component:

<CoreConcept
  concept={CORE_CONCEPTS[0]} />
In the CoreConcept component, you would then get that one single prop:

export default function CoreConcept({ concept }) {
  // Use concept.title, concept.description etc.
  // Or destructure the concept object: const { title, description, image } = concept;
}
It is entirely up to you which syntax & approach you prefer.

Grouping Received Props Into a Single Object

You can also pass multiple props to a component and then, in the component function, group them into a single object via JavaScript's "Rest Property" syntax.

I.e., if a component is used like this:

<CoreConcept
  title={CORE_CONCEPTS[0].title}
  description={CORE_CONCEPTS[0].description}  
  image={CORE_CONCEPTS[0].image} />
You could group the received props into a single object like this:

export default function CoreConcept({ ...concept }) { 
  // ...concept groups multiple values into a single object
  // Use concept.title, concept.description etc.
  // Or destructure the concept object: const { title, description, image } = concept;
}
If that syntax is a bit confusing - worry not! You'll also see concrete examples for this syntax (and for why you might want to use it in certain situations) throughout the course!

Default Prop Values

Sometimes, you'll build components that may receive an optional prop. For example, a custom Button component may receive a type prop.

So the Button component should be usable either with a type being set:

<Button type="submit" caption="My Button" />
Or without it:

<Button caption="My Button" />
To make this component work, you might want to set a default value for the type prop - in case it's not passed.

This can easily be achieved since JavaScript supports default values when using object destructuring:

export default function Button({ caption, type = "submit" }) { 
  // caption has no default value, type has a default value of "submit"
}


### Best Practice: Storing Components in Files and Using a Good Project Structure

Separate your project into meaninful parts and you could use
simple `export` or the preferred `export default`
https://www.geeksforgeeks.org/difference-between-default-named-exports-in-javascript/

### Storing Component Style Files next to components

You might want to split the CSS file also into multiple small component specific CSS files. We can cratea `Header.css` and put it in the same place where Header.jsx lives

Splitting can help identify where to some changes need to be made.

```javascript
import reactImg from "../assets/react-core-concepts.png";
const reactDescriptions = ["Fundamental", "Crucial", "Core"];
import "./Header.css";
```

Also, this doesn't make the rules scoped, if there is another Header, this rules will be applied too.

### Component Composition: The special "chilndren" Prop

The special `children` prop, is a prop that's set by React, and it's a prop that's not set with help of attributes.
This prop serves as the content between your component tag

So the children prop content WHICHEVER content you have between your component tag or could be some complex JSX structure

```javascript
export default function TabButton(props) {
  return (
    <li>
      <button>{props.children}</button>
    </li>
  );
}
```

Now we can use it in Apps.jsx notice how if you're using `export default` and whe import it in App, you don't need to add curly braces or it won't render.

```javascript
import TabButton from './components/TabButton.jsx';

<section id="examples">
  <h2>Examples</h2>
  <menu>
    <TabButton>Components</TabButton>
  </menu>
</section>
```

You can use object destructuring:

```javascript
export default function TabButton({ children }) {
  return (
    <li>
      <button>{children}</button>
    </li>
  );
}
```

When a component wraps other Components, it's called Component Composition.

We could definetively could have gone for a different approach:

```javascript
export default function TabButton({ label }) {
  return (
    <li>
      <button>{label}</button>
    </li>
  );
}
```

```javascript
<section id="examples">
  <h2>Examples</h2>
  <menu>
    <TabButton label="Components" />
  </menu>
</section>
```

Both approach works and there is no better or worse among them, is just a manner of preference, but is good to know both approaches.

### Reacting to Events

In vanilla JS this is how you'd listen to an event `document.querySelector('button').addEventListener('click', () => {});`
but in React we don't use imperative code. In react you add event listeners to elements by adding a special attribute, a special prop, because in the end those built-in elements are also just components that are already provided and understood by React. There is a long list of `on` events.

Now the value for this onClick prop or actually for any event prop is a function, because you should point to the function that should be executed when that event ocurrs

```javascript
export default function TabButton({ children }) {
  function handleClick() {
    console.log("Hello Wordl");
  }
  return (
    <li>
      <button onClick={handleClick}>{children}</button>
    </li>
  );
}
```

You can define the handler inside the component to be only available to that component. The advantage of defining these event handler functions inside the component functions is that they then have access to the component's props and state.

You must NOT execute the function `nClick={handleClick()}` because you want to use the function as a value, because this shouldn't be executed by you, but by React when that event happens

### Passing Functions as Values to Props

Now, imagine that we want to add some dynamic content base on the action of the TabButton, that means that we need to make that actions flow from the App -> TabButton ->App again, because you must handle the event in the component that also manages the data that should be changed.

So, in order to make our TabButtons clickable we'll need to set the `onClick` prop from outside of the custom `TabButton` component from inside the App component.

In `TabButton` we accept a new prop, that could be named anything, but by common convetion we will set it to `onSomething`. Starting with `on` here makes it clear that this prop should be set to a function that will ultimately be triggered based on some event whatever the event may be.

```javascript
export default function TabButton({ children, onSelect }) {
  return (
    <li>
      <button onClick={handleSelect}>{children}</button>
    </li>
  );
}
```

```javascript
function App() {
  function handleSelect() {
    console.log("Hello World from App");
  }
  return (
    <div>
      <Header />
      <main>
        <section id="core-concepts">
          <h2>Core Concepts</h2>
          <ul>
            <CoreConcept
              title={CORE_CONCEPTS[0].title}
              description={CORE_CONCEPTS[0].description}
              image={CORE_CONCEPTS[0].image}
            />
            <CoreConcept {...CORE_CONCEPTS[1]} />
            <CoreConcept {...CORE_CONCEPTS[2]} />
            <CoreConcept {...CORE_CONCEPTS[3]} />
          </ul>
        </section>
        <section id="examples">
          <h2>Examples</h2>
          <menu>
            <TabButton onSelect={handleSelect}>Components</TabButton>
            <TabButton>JSX</TabButton>
            <TabButton>Props</TabButton>
            <TabButton>State</TabButton>
          </menu>
        </section>
      </main>
    </div>
  );
}
export default App;
```

What we're doing is passing a pointer at this handle select function, we're passing the function as a value to the `onSelect` prop and in our custom component, we're forwarding that function to the `onClick` prop.
Therefore, when this button is clicked ultimately is this `handleSelect` that will be triggered. An this is a super common and important pattern, because now we're prepared to change the Dynamic content in the App component, because we're reacting to the click event in the same component we want to update the content.

### Passing Custom Arguments to Event Functions

By using an anonymous arrow function with a value we can control how it will be executed. This a very common pattern that's used in React if you wannna define a function that should be executed upon an event, but you also want to control how it's going to be called and which arguments are going to be passed.

```javascript
export default function TabButton({ children, onSelect }) {
  return (
    <li>
      <button onClick={onSelect}>{children}</button>
    </li>
  );
}
```

Part of App.js

```javascript
function App() {
  function handleSelect(selectedButton) {
    //selectedButton => 'Components', 'JSX', 'Props', or 'State'
    console.log(selectedButton);
  }
  return (
    <div>
      <Header />
      <main>
        <section id="core-concepts">
          <h2>Core Concepts</h2>
          <ul>
            <CoreConcept
              title={CORE_CONCEPTS[0].title}
              description={CORE_CONCEPTS[0].description}
              image={CORE_CONCEPTS[0].image}
            />
            <CoreConcept {...CORE_CONCEPTS[1]} />
            <CoreConcept {...CORE_CONCEPTS[2]} />
            <CoreConcept {...CORE_CONCEPTS[3]} />
          </ul>
        </section>
        <section id="examples">
          <h2>Examples</h2>
          <menu>
            <TabButton onSelect={() => handleSelect("components")}>
              Components
            </TabButton>
            <TabButton onSelect={() => handleSelect("aquiles")}>JSX</TabButton>
            <TabButton onSelect={() => handleSelect("bailo")}>Props</TabButton>
            <TabButton onSelect={() => handleSelect("yo")}>State</TabButton>
          </menu>
        </section>
      </main>
    </div>
  );
}
```

### How NOT to update the UI - A Look behind the scenes of React

By default, React components execute only ONCE. You have to "tell" react a component should be executed again

React compated the **old utput** ("old JSX code") of your component function to the new output ("new JSX code") and applies any differences to the actual website UI.

If you add a `console.log("Hello from APP")` and another in the TabButton, you will see this logs, only ONCE even if you click on the buttons.

This is where STATE comes into play.

### Managing State and Using Hooks

The concept of state, is all about registering variables that are handle by React, that will also tell react that data has changed and that will therefore cause React to update the UI.

These special variables as you could call them are created with the help of a special function that must be imported from the React library.

All these functions that start with `use` in React projects are **React Hooks**, and the special thing about them is that despite being regular functions they MUST only be called inside of React component functions or inside of other React Hooks, like custom React Hooks.

So you can call it here:

```javascript
function App() {
  useState()


  function handleSelect(selectedButton) {
    //selectedButton => 'Components', 'JSX', 'Props', or 'State'
    console.log(selectedButton);
  }
  return (...)
```

but, NOT here:

```javaScript
function App() {

  function handleSelect(selectedButton) {
      useState() // WRONG!!!
    console.log(selectedButton);
  }
  return ()}
```

**Rules of Hooks**

1. Only call hooks inside of component functions. React Hooks must not be called outside of React component functions
2. Only call hooks on the top level. React hooks must not be called in nested code statements

```javascript
//const stateArray using array destructuring
const [selectedTopic, setSelectedTopic] = useState("Please click a button");
```

We're naming the first element here, selectedTopic because this first element in this array, which we get back from useState, will be the current data snapshot for this component execution cycle.

So this first element will be the actual data we're managing. Now I named this second element `setSelectedTopic` because this second element in this array we get back from `useState` will always be a function. A function provided by React that can be executed to update this state, so to update this stored value. This function is the one that will tell React to execute that component again and that's why we can use `const` becuause it'll be recreated every time this component function executes

```javascript
import { useState } from "react";
import { CORE_CONCEPTS } from "./data.js";
import Header from "./components/Header.jsx";
import CoreConcept from "./components/CoreConcept.jsx";
import TabButton from "./components/TabButton.jsx";

function App() {
  const [selectedTopic, setSelectedTopic] = useState("Please click a button");

  function handleSelect(selectedButton) {
    //selectedButton => 'Components', 'JSX', 'Props', or 'State'
    setSelectedTopic(selectedButton);
    console.log(selectedTopic);
  }
  return (
    <div>
      <Header />
      <main>
        <section id="core-concepts">
          <h2>Core Concepts</h2>
          <ul>
            <CoreConcept
              title={CORE_CONCEPTS[0].title}
              description={CORE_CONCEPTS[0].description}
              image={CORE_CONCEPTS[0].image}
            />
            <CoreConcept {...CORE_CONCEPTS[1]} />
            <CoreConcept {...CORE_CONCEPTS[2]} />
            <CoreConcept {...CORE_CONCEPTS[3]} />
          </ul>
        </section>
        <section id="examples">
          <h2>Examples</h2>
          <menu>
            <TabButton onSelect={() => handleSelect("components")}>
              Components
            </TabButton>
            <TabButton onSelect={() => handleSelect("aquiles")}>JSX</TabButton>
            <TabButton onSelect={() => handleSelect("bailo")}>Props</TabButton>
            <TabButton onSelect={() => handleSelect("yo")}>State</TabButton>
          </menu>
          {selectedTopic}
        </section>
      </main>
    </div>
  );
}

export default App;
```

Now, there is something funny going on, while the UI updates the log seems to be lagging eventhough is after upating the UI, this is because React schedules this state update and then it then re-executes this component function, is not bad, just something to keep on mind

### Deriving & Outputing Data Based on State

Now, we'll update our `data.js` to crate our tab-content

```javascript

export const EXAMPLES = {
  components: {
    title: 'Components',
    description:
      'Components are the building blocks of React applications. A component is a self-contained module (HTML + optional CSS + JS) that renders some output.',
    code: `
function Welcome() {
  return <h1>Hello, World!</h1>;
}`,
  },
  jsx: {
    title: 'JSX',
    description:

```

We create our div that will update the content based on the selected tab:

```javascript
            <TabButton onSelect={() => handleSelect('state')}>State</TabButton>
          </menu>
          <div id="tab-content">
            <h3>{EXAMPLES[selectedTopic].title}</h3>
            <p>{EXAMPLES[selectedTopic].description}</p>
            <pre>
              <code>
              {EXAMPLES[selectedTopic].code}
              </code>
            </pre>
          </div>

```

### Rendering Content Conditionally

```javascript
<section id="examples">
  <h2>Examples</h2>
  <menu>
    <TabButton onSelect={() => handleSelect("components")}>
      Components
    </TabButton>
    <TabButton onSelect={() => handleSelect("jsx")}>JSX</TabButton>
    <TabButton onSelect={() => handleSelect("props")}>Props</TabButton>
    <TabButton onSelect={() => handleSelect("state")}>State</TabButton>
  </menu>
  {!selectedTopic ? (
    <p>Please select a topic. </p>
  ) : (
    <div id="tab-content">
      <h3>{EXAMPLES[selectedTopic].title}</h3>
      <p>{EXAMPLES[selectedTopic].description}</p>
      <pre>
        <code>{EXAMPLES[selectedTopic].code}</code>
      </pre>
    </div>
  )}
</section>
```

We can also write it in the following this trick of using `&&` and automatically uses the value that comes after it, making sometimes easier to read.

```javascript
  </menu>
  {!selectedTopic &&   <p>Please select a topic. </p>}
  {selectedTopic && (
    <div id="tab-content">
      <h3>{EXAMPLES[selectedTopic].title}</h3>
      <p>{EXAMPLES[selectedTopic].description}</p>
      <pre>
        <code>{EXAMPLES[selectedTopic].code}</code>
      </pre>
    </div>
  )}

```

Another way is using a variable

```javascript
let tabContent = <p>Please select a topic. </p>
if(selectedTopic){
  tabContent = <div id="tab-content">
      <h3>{EXAMPLES[selectedTopic].title}</h3>
      <p>{EXAMPLES[selectedTopic].description}</p>
      <pre>
        <code>{EXAMPLES[selectedTopic].code}</code>
      </pre>
    </div>
}

</menu>
  {tabContent}
```

### CSS Styling & Dynamic Styling

On jsx you use `className` to set up a class attribute, and we can use a ternary expression

```javaScript
export default function TabButton({children, onSelect, isSelected }) {
    return (
        <li>
        <button className={isSelected ? 'active' : undefined} onClick={onSelect} >
            {children}
        </button>
        </li>
     );
    }
```

```javaScript
<TabButton isSelected={selectedTopic === 'components'}
            onSelect={() => handleSelect('components')}
            >
              Components
            </TabButton>

            <TabButton
            isSelected={selectedTopic === 'jsx'}
            onSelect={() => handleSelect('jsx')}
            >
              JSX
            </TabButton>

            <TabButton
            isSelected={selectedTopic === 'props'}
            onSelect={() => handleSelect('props')}
            >
              Props
            </TabButton>

            <TabButton
            isSelected={selectedTopic === 'state'}
            onSelect={() => handleSelect('state')}
            >
              State
            </TabButton>
```

Witht his, the tabs will change to `active` when clicked.

### Outputting List Data Dynamically

The following part could be improved, because we manually repeat this `CoreConcept` component. Also this could break if there's change in the array.

```javascript
<ul>
  <CoreConcept
    title={CORE_CONCEPTS[0].title}
    description={CORE_CONCEPTS[0].description}
    image={CORE_CONCEPTS[0].image}
  />
  <CoreConcept {...CORE_CONCEPTS[1]} />
  <CoreConcept {...CORE_CONCEPTS[2]} />
  <CoreConcept {...CORE_CONCEPTS[3]} />
</ul>
```

JSX is capable of dealing with arrays of renderable data, so by combining that with the `.map` method:

```javascript
<ul>
  {CORE_CONCEPTS.map((conceptItem) => (
    <CoreConcept {...conceptItem} />
  ))}
</ul>
```

Just remember that we need to add a key prop, that needs to be unique, so we'll update it like this:

```javascript
<ul>
  {CORE_CONCEPTS.map((conceptItem) => (
    <CoreConcept key={conceptItem.title} {...conceptItem} />
  ))}
</ul>
```

## 4. React Essentials - Deep Dive <a name="deepdive"></a>

### You don't have to Use JSX

JSX is convenient, but you could also replace JSX code, with this code here, that doesn't use JSX at all, but whihc instead only uses standard JavaScript features:

```javascript
<div id="content">
  <p>Hello World</p>
</div>
```

```javascript
React.createElement(
  "div",
  { id: "content" },
  React.createElement("p", null, "Hello World!")
);
```

By using the `createElement` method exposed by React to create the same structure, that same HTML code in the end.
This method takes a Compomemt type (ex. div), followed by a props object ( ex. { id: 'content'}) and finally child elements

### Working with Fragments

JSX expressions must have a parant element, which in this case is this div:

```javascript
return (
  <div>
    <Header />
    <main></main>
  </div>
);
```

If we delete the div, we'll returning 2 sibling elements, and that doesn't work, because you can't retunr 2 values.
An alternative is a `Fragment`

```javascript
import { useState, Fragment } from "react";

return (
  <Fragment>
    <Header />
    <main></main>
  </Fragment>
);
```

Or you can use an empty tag in newer projects:

```javascript
return (
  <>
    <Header />
    <main></main>
  </>
);
```

### When should you split components

Being able to identify good places for extra components and being able to split up your your big components into a smaller ones and to separate responsabilities is an important skill for every React Developer.

### Spliting Components be Feature and State

Looking into our app, it seems that every section is its own feature, therefore we're going to split it.
Putting different features into differnete components is always a good idea.

### Problem: Props are not forwarded to inner elements

If we look close to our Example project, we could see that both sections have the same structure:

- header
  - content

Therefore, we can create a section component that always enforces thins kind of structure. What we need to undertand is that when you're setting props, or attributes
sort to say on a custom compnent, those props are not forwarded to the JSX code used inside of that component.

### Forwarding Props to Wrapped Elements

When destructuring our props like this, we can also add some special built-in JavaScript `...anyWordYouLike`, this tells JavaScript to collect all other props that might be received on this `Section` Component and merge them into a `anyWordYouLinke` object, most likely named `props`.
This allows is to then forward them here to this Section element, by using the spread operator.

```javascript
export default function Section({ title, children, ...props }) {
  return (
    <section {...props}>
      <h2>{title}</h2>
      {children}
    </section>
  );
}
```

And this can be a very useful pattern when building wrapper components.
We could use the same pattern for the `TabButton`

### Working with Multiple JSX Slots

Another component we could add is a special tabs component area, because we can see that our tabs are a combination of having a menu bar with tab buttons and then the tab conent below that menu bar, and that content could be inside some div or other HTML element.

```javascript
export default function Tabs({ children, buttons }) {
  return (
    <>
      <menu>{buttons}</menu>
      {children}
    </>
  );
}
```

```javascript
return (
        <Section title="Examples" id="examples">
          <Tabs buttons={
            <>
            <TabButton
              isSelected={selectedTopic === 'components'}
              onClick={() => handleSelect('components')}
            >
              Components
            </TabButton>
            <TabButton
              isSelected={selectedTopic === 'jsx'}
              onClick={() => handleSelect('jsx')}
            >
              JSX
            </TabButton>
            <TabButton
              isSelected={selectedTopic === 'props'}
              onClick={() => handleSelect('props')}
            >
              Props
            </TabButton>
            <TabButton
              isSelected={selectedTopic === 'state'}
              onClick={() => handleSelect('state')}
            >
              State
            </TabButton>
            </>
          }>
          {tabContent}
          </Tabs>
          <menu>
          </menu>
        </Section>

```

By setting the buttons as a special prop, might look weird, but is a common patter to make the `Tabs.jsx` component reusable and not having to add more props that will reduce its usability.
While this patter might look redundant, it is a crucial pattern and being able to set multiple slots in components its a crucial concept

### Setting Component Types Dynamically

Going back to our `Tabs`component, that is currently wrap by `<menu>` tags, we might want to make it more flexible. An elegant solution would be to add another prop, to leave it to the developer to set anyway they prefer.

```javaScript
export default function Tabs({ children, buttons, buttonsContainer }) {
    const ButtonsContainer = buttonsContainer;

    return <>
        <ButtonsContainer >
            {buttons}
        </ButtonsContainer>
        {children}
    </>
}
```

So now, the developer, can set the prop as built-in elements such as: `"menu"`, `"ul"` or even a custom component like `{Section}`

```javascript
<Section title="Examples" id="examples">
          <Tabs
          buttonsContainer="menu"
          buttons={
            <>
            <TabButton
              isSelected={selectedTopic === 'components'}
              onClick={() => handleSelect('components')}
            >
```

You can also use a shortcut, by remapping the prop as a CONSTANT

```javaScript
export default function Tabs({ children, buttons, ButtonsContainer }) {
//const ButtonsContainer = buttonsContainer;

    return <>
        <ButtonsContainer >
            {buttons}
        </ButtonsContainer>
        {children}
    </>
}
```

### Setting Default Prop Values

Setting menu as the default value when that prop is not passed

```javascript
export default function Tabs({ children, buttons, ButtonsContainer = "menu" }) {
  return (
    <>
      <ButtonsContainer>{buttons}</ButtonsContainer>
      {children}
    </>
  );
}
```

### Closer Look: public/ vs assets/ for Image Storage

The public/ Folder
As shown in the previous lecture you can store images in the public/ folder and then directly reference them from inside your index.html or index.css files.

The reason for that is that images (or, in general: files) stored in public/ are made publicly available by the underlying project development server & build process. Just like index.html, those files can directly be visited from inside the browser and can therefore also be requested by other files.

If you try loading localhost:5173/some-image.jpg, you'll be able to see that image (if it exists in the public/ folder, of course).

The src/assets/ Folder
You can also store images in the src/assets/ folder (or, actually, anywhere in the src folder).

So what's the difference compared to public/?

Any files (of any format) stored in src (or subfolders like src/assets/) are not made available to the public. They can't be accessed by website visitors. If you try loading localhost:5173/src/assets/some-image.jpg, you'll get an error.

Instead, files stored in src/ (and subfolders) can be used in your code files. Images imported into code files are then picked up by the underlying build process, potentially optimized, and kind of "injected" into the public/ folder right before serving the website. Links to those images are automatically generated and used in the places where you referenced the imported images.

Which Folder Should You Use?
You should use the public/ folder for any images that should not be handled by the build process and that should be generally available. Good candidates are images used directly in the index.html file or favicons.

On the other hand, images that are used inside of components should typically be stored in the src/ folder (e.g., in src/assets/).

### Components instance work in isolation

Even when you're reusing the same component, React creates a new isolated instance

### Conditional Content and suboptimal way of updating content

Setting a condition like this ` setIsEditing(isEditing ? false : true);` is the same as saying `setEditing(!isEditing)` but is still not perfect.

### User input & Two-Way-Binding

This way of listening to a change on the `input` and then feeding that update value back into this input is also called two-way-Binding because were getting a value out of this input and we're feeding a value back into this input.

### Best Practice: Updating Object State Inmutability

```javascript
    function handleSelectSquare (rowIndex, colIndex) {
        setGameBoard((prevGameBoard) => {
            prevGameBoard[rowIndex][colIndex] = 'X';
            return prevGameBoard
        });
```

Just as you shoul use `prevState` updating function when updating your state based on a previous state, it's also recommended that if your tate is an object or array, you udate that state in an nmutable way, which simply means you create a copy of the old state and you just change that copy instead of that existing object or array.
The reason for that if your tate is an object or array, you're dealing with a reference value in JavaScript, and therefore if you would be updating it like this, you would be updating the old value in-memory immediately, even before this scheduled state update was executed by React. This can lead to strage bugs and side effects if you have multiple places in your application that are scheduling state updates for the same state.

```javascript
function handleSelectSquare(rowIndex, colIndex) {
  setGameBoard((prevGameBoard) => {
    const updatedBoard = [
      ...prevGameBoard.map((innerArray) => [...innerArray]),
    ];
    updatedBoard[rowIndex][colIndex] = "X";
    return updatedBoard;
  });
}
```

Now, with this we're updating the state in an inmmutable way.

### Lifting State Up

Lift the state uo to the closest ancestor component that has access to all components tat need to work with that state. In the case of the Tic-Tac-Toe App, this would be the `App` component as it is the closest ancestor to both the Player and GameBoard components.

### Avoid Intersecting states

Sometimes you might need to feel to create an extra set of contants to track an specific state, but if you already have another State that tracks the same information but the newly created state only tracks a bit extra data is something that you might want to avoid.

So instead of doing something like this in the `App` component:

```javascript
import { useState } from "react";
import Player from "./components/Player";
import GameBoard from "./components/GameBoard";
import Log from "./components/Log";

function App() {
  const [gameTurns, setGameTurns] = useState([]);
  const [activePlayer, setActivePlayer] = useState("X");

  function handleSelectSquare() {
    setActivePlayer((currentActivePlayer) => currentActivePlayer === "X" ? "O" : "X");
    setGameTurns();
  }
```

We're going to lift the state from the `GameBoard` component to the `App` Component, but then we'll probably need to do some refactoring of the gameBoard state.

### Prefer computed values & avoid unnecesary state management

So the way to go about lifting state would be like this which:
a. update state in an immutable way
b. don't merge separate states, like for example using the `activePlayer` state

```javascript
import { useState } from "react";
import Player from "./components/Player";
import GameBoard from "./components/GameBoard";
import Log from "./components/Log";

function App() {
  const [gameTurns, setGameTurns] = useState([]);
  const [activePlayer, setActivePlayer] = useState("X");

  function handleSelectSquare(rowIndex, colIndex) {
    setActivePlayer((currentActivePlayer) => currentActivePlayer === "X" ? "O" : "X");
    setGameTurns(prevTurns => {
      let currentPlayer = X;
      if(prevTurns.length > 0 && prevTurns[0].player === "X") {
        currentPlayer = "O";

      }
      const updatedTurns = [
        {square: {row: rowIndex, col: colIndex}, player: currentPlayer},
        ...prevTurns
      ];
      return updatedTurns;
    });
  }
```

### Deriving State from Props

Now that we have this `gameTurns` state, let's used it to derive the gameboard from that array of turns.
1.We start by destructing the information to pull from `turn` 2. Now we can also destructire `square` to extract `row` and `col`

And that's all we don't need to manage extra state, we're **deriving state**.

```javascript
const initialGameBoard = [
    [null, null, null],
    [null, null, null],
    [null, null, null]
];

export default function GameBoard({onSelectSquare, turns}){
    let gameBoard = initialGameBoard;

    for(const turn of turns) {
        const { square, player } = turn;
        const { row, col } = square;

        gameBoard[row][col] = player;
    }
```

So GameBoard is a computed value that is derived from some state, in this case the `gameTurns state` that is manage in the App state.
Yo should manage as little state as needed and try to derive as much information from the availabw state.

### Disabling Buttons Conditionally

```javascript
<button
  onClick={() => onSelectSquare(rowIndex, colIndex)}
  disabled={playerSymbol !== null}
>
  {playerSymbol}
</button>
```

### Outsourcing Data Into A Separate File

In order to determine who wins, we need to test all winning combinations at every turn

### Lifting Up Computed Values

An initial idea would be to create another state, and check at everyturn within `handleSelectSquare`

```javascript
function App() {
  const [gameTurns, setGameTurns] = useState([]);
  const [hasWinner, setHasWinner] = useState(false);

  const activePlayer = deriveActivePlayer(gameTurns);

  function handleSelectSquare(rowIndex, colIndex) {

    setGameTurns((prevTurns) => {
      const currentPlayer = deriveActivePlayer(prevTurns);

```

But that would be a **reduntat state**, because we can derive whether we have a winner or not from `gameTurns`, because the `App` component function will execute after every turn.

### Why Inmutability Matters

In the end our game is controlled by the `gameTurns` state, that's our single source of truth for the entire game. We use it to derive

- Game GameBoard
- activePlayer
- check for winner

Therefore restarting the game means that will should return `gameTurns` to an empty array and all will automatically adjust, but that's not necesarilly true based on how we're updating each turn.
We have to remember that arrays like objest in JavaScript are reference values and that means that they're stored in memory. And if we're using tgem, even if they're stored in different variables, we're always editing that same object or array in memory. Therefore, when we set a certain row-column combination to the plater symbol here, I'm doind that in that original array in memory. Therefore after restarting the game, this array here is not reset, it's still the edited old array. So we now kind of decoupled the gameBoardf from our gameTurns because of how we udpaded this here. Thankfully the solution is simple. We just need to do a deep copy:

```javascript
const initialGameBoard = [
  [null, null, null],
  [null, null, null],
  [null, null, null],
];

let gameBoard = [...initialGameBoard.map((array) => [...array])];
```

### When NOT to lift state

At the moment, the player name information is stored inside of the player component. That's where we're editing and storing the name. And we're not sharing this name wth any other part of the application. So hence we need to make sure that we get those player names out of the player component, into the app component.
Now you could think that you want to lift it up out of this player component into the app one, but that would be wrong.

- It would be wrong because this player name state is used to updaye this input field on ever keystroke, and if we move it out that would mean the entire app component is reevaluated on every keystroke, which also means that the entire gameboard is reevaluated on every keystroke amd that is really redundant and not what we want to do.
- It could also be tricky, because we're using the player component twice and every component should manage it own name
  So therefore, the player component should stay the way it is.

Instead we'lll add a new state where we store the currentlu set player names.

```javascript
function App() {
  const [players, setPlayers] = useState({
    'X': 'Player 1',
    'O': 'Player 2'
  });
```

### An alternative to Lifting State Up

Now, we just need to make sure that handlePlayerNamceChange gets trigerred whenever in the player component this change is confirmed by clicking this button when it says `Save`

```javascript
//Player Component

return (
  <li className={isActive ? "active" : undefined}>
    <span className="player">
      {editablePlayerName}
      <span className="player-symbol">{symbol}</span>
    </span>
    <button onClick={handleEditClick}>{isEditing ? "Save" : "Edit"}</button>
  </li>
);
```

1. We pass a pointer at this `handlePlayerNameChange` function to those player components

```javascript
//App Component
  <main>
      <div id="game-container">
        <ol id="players" className="highlight-player">
          <Player
            initialName="Player 1"
            symbol="X"
            isActive={ activePlayer === "X"}
            onChangeName={handlePlayerNameChange}
            />
          <Player
            initialName="Player 2"
            symbol="O"
            isActive={ activePlayer === "O"}
            onChangeName={handlePlayerNameChange}
            />
```

## 5. React Essentials - Practice Project

## 6. Styling React Components

In this section we'll go over:

- Styling with Vanilla CSS
- Scoping Styles with CSS Modules
- CSS-in-JS with "Styled Components"
- Styling with Tailwind CSS

### Spliting CSS Code across multiple Files

In a typical React projecr, you can import CSS files into JavaScript, and the build tool, in this case Vite, will identify such imports and in the end simply make sure that in gets injected into the webpage, therefore you can include as many vanilla CSS files as you want, so you can split this file into multiple ones where you attached the individual files to the components to which they belong.

### Styling React Apps with Vanilla CSS - Pros and Cons

**Advantages**

- CSS code is decoupled from JSX code
- You write CSS code as you (maybe) know and (maybe) love it
- CSS code can be written by another developer who needs only a minimal amount of access to your code

**Disadvantages**

- You need to know CSS
- CSS code is not scoped to components and CSS rules may clash across components (eg. some CSS class name used in different components for different purposes)

### Vanilla CSS styles are not scoped to components!

if the CSS rules are not scoped correctly even if the stylesheets is divided they will affect a component, for example if you have a rule that says ` header h3` but you delete the word `header` then this rule will apply to all h3 as expected

### Styling react Apps with Inlines Styles

So, how can we achieve scoping? A solution would be to use in-line styles. You can do that in react by setting a `style` prop.

The style prop takes a dinamic value:

```javascript
export default function Header() {
  return (
    <header>
      <img src={logo} alt="A canvas" />
      <h1>ReactArt</h1>
      <p
        style={{
          color: "red",
        }}
      >
        A community of artists and art-lovers.
      </p>
    </header>
  );
}
```

**Advantages**

- Quick and easy to add to JSX
- Styles only affect the element to which you add them
- Dynamic (conditional) styling is simple

**Disadvantages**

- You need to know CSS
- You need to style every element individually
- No separation between CSS and JSX code

### Dynamic and Conditional Inline Styles

```javascript

  const emailNotValid = submitted && !enteredEmail.includes('@');
  const passwordNotValid = submitted && enteredPassword.trim().length < 6;

  return (
    <div id="auth-inputs">
      <div className="controls">
        <p>
          <label>Email</label>
          <input
            type="email"
            style={{
              backgroundColor: emailNotValid ? '#FED2D2' : '#d1d5db'
            }}
            //className={emailNotValid ? 'invalid' : undefined}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        </p>
```

### Dynamic & Conditional Styling with CSS Files & CSS Classes

You can, of course also style elements conditionally when you're using extra css files, typically achieved by adding CSS clases conditionally. `className={emailNotValid ? 'invalid' : undefined}`

Now, its also possible that you want you want to add a class dynamically to an element that also already gas a class that should always be .
So let's say that we hag a `<label>` tag with a class that always should be there `label` but in addition we also have the `invalid` class that should only be applied when a certain condition is met.

```javascript
<label className="label, invalid">Email</label>
```

The previous code will always apply both classes, so to make the second one conditional this should be coded like this:

```javascript
<label className={`label ${emailNotValid ? "invalid" : ""}`}>Email</label>
```

### Scoping CSS Rules with CSS Modules

Allows you to write vanilla CSS code and rules that are scoped. Now, CSS Modules is an approach, a solution you could say, that in the end neesd to be implemented and enforced by the build process that is used in your react project. It's not a default browser or JavaScript feature. Instead, CSS is an approach where the build tool will transform your CSS class names and only those two class names that are guaranteed to be unique per file.

So let's say we have a `className='paragraph'` and we applied it to one of or `<p>` tags inside our `Header.jsx` file, this will apply the rules from the `Header.css`, but then me apply that class in our `AuthInputs.jsx` file, the rules would apply to that tag.

BUT if we rename our file `Header.module.css` this naming, will signal the built process to process the file differently and we also need to import it differently.

This will be a JavaScript object that will ne generated by the underlying build process, which you could name classes or styles. But classes is a fitting name because this object will contain your classnames transformed to unique class names.

```javascript
import logo from "../assets/logo.png";
import classes from "./Header.module.css";

export default function Header() {
  return (
    <header>
      <img src={logo} alt="A canvas" />
      <h1>ReactArt</h1>
      <p className={classes.paragraph}>
        A community of artists and art-lovers.
      </p>
    </header>
  );
}
```

Now if you go to the browser and inspect your project locally you will see that the `<p>` element in questions looks something like this `<p class="_paragraph_wsvrj_28">`. So now this class is unique for this component file and could be dynamicaly and conditionally applied like others.

**CSS Modules: Advantages and Disadvantages**
Advantages:

- CSS code is decoupled form JSX
- You wirte CSS code you know and love
- CSS code can be written by another developer

Disadvantages:

- You need to know CSS
- You might end up with many relatively small CSS files in your projects

### Introducing "Styled Components" (Third-party Package)

The idea behind this package is that you do not define your CSS rules and styles in separate CSS files, but also not as inline styles, but instead in special component that are built with help of a package.

We'll install the package `npm install styled-components`.

`styled` is a javascript object that uses [tagged templates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#tagged_templates)

```javascript
import { styled } from 'styled-components'

const ControlContainer  = styled.div`
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
`
 return (
    <div id="auth-inputs">
      <ControlContainer>
        <p>
          <label className={`label ${emailNotValid ? "invalid" : ""}`}>Email</label>
          <input
            type="email"

```

Under the hood, this style-components packafe creates unique CSS class names and defines rules for theses classes.

### Creating flexible components with styled-components

You can mix and match styled-components with other styling approaches, though typically you will likely go with one approach that you use for the entirety of the app.

We'll know also use styled components for `Label`. These components do not just use the children prop so that you can wrap them around content, but in addtion , they also forward al props you're setting on this styled component (like the dynamic emailNotValid class) to the underlaying built-in JSX element. It then just adds the styles.

```javascript
const Label = styled.label`
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #6b7280;
`
<Label className={`label ${emailNotValid ? "invalid" : ""}`}>Email</Label>
          <input
            type="email"

```

### Dynamic and Conditional Styled Components
