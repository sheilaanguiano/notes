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
With React, you drfine the target UI state(s)- not the steps to get there. Instaed, React will figure out & perform the necessary steps.

When you write vanilla JavaScript, ypu write Imperative code, which means, you're not defining the goal, but the steps neeeded to get there.

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

In the context of building React apps, you will almost necer add these scripts tags to your HTML file on your own, because React projects almos always use a **build process** which as part of that build process, injects these script tahs into the HTML code for you.

## 3. React Essentials - Components, JSX, Props, State and More <a name="essentials"></a>

### It's all about Components

React and its ecosystem provide dozens of useful and important features and concets, but arguably the most important concept is the concept of a Component.

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

### JSX & React Comonents (Core Concept)

- JSX : JavaScript Syntax Extension
- With React, you write declarative code. You define the target HTML structure & UI, not the steps to get there
- In React a component is really just a JavaScript function, though in order to be recognized and used as a Component by React, it needs to follow 2 rules:
  - The function name must start with an uppercase character
  - Must return a renderable value, typically the to-be-rendered HTML markup

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

And it's in this place where the React app boots up, you could say. This render method, however, is being called on an object
that's created with another method, the `createRoot` method.
This method takes an existing HTML element as an input,
so an element that's not being created by React but that instead is part of the index.html file already.

React goes ahead and injects a React component, the App component in this case, including any nesting components

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

Importing an Image the way you do in an HTML, might cause some problems during the bundling process, like it getting deleted.

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

React allows you to pass data to components via a concept called "Props".
This props parameter will be set by React because it's React that will execute this function. remember you'tr not calling these components function yourself in your code, instead you're using them as html elements and under the hood React will call the actual functions.

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
              description="The core UI"
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

### Best Practice: Storing Components in Files and Using a Good Project Structure

Separate your project into meaninful parts and you could use
simple `export` or the preferred `export default`
https://www.geeksforgeeks.org/difference-between-default-named-exports-in-javascript/

### Storing Component Style Files next to components

You might want to split the CSS file also into multiple small component specific CSS files. We can cratea `Header.css` and put it in the same place where Header.jsx lives

So we can go to the original `index.css` file and cut all the related css rules, this will initially break the page, you just need to import it in the Header.jsx to fix it:

```javascript
import reactImg from "../assets/react-core-concepts.png";
const reactDescriptions = ["Fundamental", "Crucial", "Core"];
import "./Header.css";
```

Also, this doesn't make the rules scoped, if there is another Header, this rules will be applied to0.

### Component Composition: The special "chilndre" Prop

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

Now we can use it in Apps.jsx

```javascript
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

You must NOT execute the function `nClick={handleClick()}`

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
While this patter might look redundant, it is a crucial pattern and being able to set multiple slots in components its a cruciak concept
