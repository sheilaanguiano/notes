# React and TypeScript - The Practical Guide

---

Platform: Udemy
Instructor: Maximilian Schwarzmuller
Author: Sheila Anguiano

---

# Table of Contents

1. [Introduction](#intro)
2. [TypeScript Basics & Core Concepts](#basics)
3. [Using TypeScript with React](#using-typescript-with-react)

## Introduction <a name="intro"></a>

### Why React and TypeScript?

TypeScript builds on JavaScript and extends its syntax by adding strong typing.
TypeScript helps you catch & fix type-related errors-earlier, but sometimes that comes at the expenses of having to define complex value types

## TypeScript Basics & Core Concepts <a name="basics"></a>

### TypeScript Setup & Using TypeScript <a name="using-typescript-with-react"></a>

To use TypeScript in any project you need to install it using node in your project either as a package or install it globally `npm install - typescript` and the run `npx tsc` to compile any `tsc` file you're targeting to JS.

### Working with Types: Type Inference & Explicit Type Annotations

```
let userName = "Midnight" // Type Inference: It assumes the type is a string
let userAge: number = 34 // Explicit Type: We tell is going to be a number
```

- Vanilla JS is accepted in a TypeScript file
- Types are enforced

### Basic Pimitive Types, Invoking the TypeScript Compiler and Combining Types Union Types

- Basic Primitive types: `string`, `number` and `boolean`
- Invoking TypeScript Compiler `npx tsc file-name.ts`
- Sometimes you will have a variable that should not be limited to a specific type

```typescript
//In this case, UserID can be either a string OR a number;
let userID: string | number = "abc1";
userID = 123;
```

### Working with Object Types

Another type is `object` that could be used the following way: `let user: object;`, but that's not the best way to store it.

If we want to make sure that the object must have a certain structure the way to do it, is this way:

```javascript
//Here, we're setting the type as well as defining the types for the different keys
let user: {
  name: string,
  age: number,
  isAdmin: boolean,
  id: string | number,
};

user = {
  name: "Max",
  age: 34,
  isAdmin: true,
  id: "abc",
};
```

### Working with Array Types

You can declare `let hobbies: Array`, but you also need to suplement the complementary data type to specify what type of data is going to be in said array

```typescript
let hobbies: Array<string>; // hobbies is an array of strings
hobbies = ["Sports", "Cooking", "Reading"];
```

BUT there is also a shortcut `let hobbies: string[]` so for example you can have an array of object with the following structure: `{name: string; age: number}[]`

### Adding Types to Functions - Parameter & Return Value Types

- You usually don't assing Type to a `const` because is inferred that is going to be an explicit, unique type such as `const API_KEY = 'abc'` and it won't be re-assigned.
- You can use types for function parameters as well as the return type, that could be for example `undefined` as shown below, becasue the function doesn't return anything.

```typescript
function add(a: number, b: number): undefined {
  const result = a + b;
  console.log(result);
}
```

But for this specific scenario we have a better return type, that you should use instead if you have a function without a return statement, and that's the `void` type, which is another type built into Typescript thats meant to be used if you have a function without a return statement or if your function doesn't return anything.

Now if it means to return something, you could leave it to be infered or make it explicit

```typescript
function add(a: number, b: number): number {
  const result = a + b;
  return result;
}
```

### Defining Function Types

Now, let's say that we create the function `calculate` that for example receives 2 numbers and then a function as a third argument

```typescript
function add(a: number, b: number): number {
  const result = a + b;
  return result;
}

function calculate(
  a: number,
  b: number,
  calcFn: (a: number, b: number) => number // Here we're defining the Type of calcFn as a function
) {
  calcFn(a, b);
}

calculate(2, 5, add);
```

So, when we call `calculate()` we can pass add or any other function that has any similar signature

### Creating Custom Types / Types Aliases

A problem with the function definitions is that sometimes they can get quite long.

```typescript
function add(a: number, b: number): number {
  const result = a + b;
  return result;
}

function calculate(
  a: number,
  b: number,
  calcFn: (a: number, b: number) => number
) {
  calcFn(a, b);
}
```

So you can create a custom type or to be more precise to assign an alias by using the `type` keyword

```typescript
function add(a: number, b: number): number {
  const result = a + b;
  return result;
}

type AddFn = (a: number, b: number) => number;

function calculate(a: number, b: number, calcFn: AddFn) {
  calcFn(a, b);
}

calculate(2, 5, add);
```

This a very important TypeScript feature that we'll use a lot, for example we could use it here:

```
let userID: sring | number = 'abc1';
userID = 123;
```

we coul create a type alis here

```
type StringOrNum = string | number;

let userID: StringOrNum = 'abc1';
userID = 123;
```

Another scenario would be to create a `User` type.

### Defining Object Types with Interfaces

We mentioned that with aliases you can create your custom Types, so an object could be defined like this:

```typescript
type User = {
  name: string;
  age: number;
  isAdmin: boolean;
  id: string | number;
};

let user: User;
```

But another option is to crete an `interface`. The interface type is essentially for creating objects

```typescript
interface Credentials {
 password: string;
 email: string;
}

let creds: Credentials; // The variable creds is of type Credentials

creds = {
    password: 'abc';
    email: 'something@smething.com'
}
```

You can also use `interface` to define a function

### Interfaces vs Custom Types

You can use interfaces as contracts that classes have to adhere to, if you're implementing them.

```typescript

interface Credentials {
 password: string;
 email: string;
}

let creds: Credentials; // The variable creds is of type Credentials

creds = {
    password: 'abc';
    email: 'something@smething.com'
}

class AuthCredentials implements Credentials {
    email: string;
    password: sting;
    userName: string;
}
function login(credentiasl: Credentials){

}

login(new AuthCredentials())

```

Another reasont to use interfaces is that they're esily expandable. This is called _Declaration Merging_

```typescript
interface Credentials {
  password: string;
  email: string;
}

interface Credentials {
  mode: string;
}
```

### Merging Types

Imagine you have 2 types that need to be separated, but a third one that is the combination of both, of course you could create a third type:

```javascript
type Admin = {
  permissions: strings[],
};

type AppUser = {
  userName: string,
};

type AppAdmin = {
  permissions: strings[],
  userName: string,
};
```

But that's too cumbersome, so the better way is to merge:

```javaScript
type Admin = {
  permissions: strings[]
};

type AppUser = {
 userName: string;
};

type AppAdmin = Admin & AppUserl

let admin: AppAdmin

admin = {
  permission:['login'],
  userName: 'Max'
}
```

You can also do the same with interfaces:

```javascript
interface Admin {
  permissions: strings[];
}

interface AppUser {
  userName: string;
}

interface AppAdmin extends Admin, AppUser {}

let admin: AppAdmin;

admin = {
  permission: ["login"],
  userName: "Max",
};
```

### Being Specific with literal Types

Let's say we want to make a variable `role` that will be of type `string` but not any type string, an exact string or strings:

```javascript
let role: "admin" | "user" | "editor";
role = "admin";
role = "user";
role = "abc"; // This string will throw an error
```

### Adding Type Guards

When working with Union Types, sometimes you may want to check the exact value. For example lets say we want to create Function only applicable when the role is `admin`

```javascript
type Role = "admin" | "user" | "editor";

let role: Role;

function perfomAction(action: string, role: Role) {
  if (role === "admin") {
    //Do something only if the role is admin
  }
}
```

The above Type Safeguard is a common pattern. When using "Type Guards" TypeScript performs so-called "Type Narrowing".

You CANNOT check if a value meets the definition of a custom type(type alias) or interface type

### Making Sense of Generic Types

Generic Types like "Array" are types that work with another types such as:

```javascript
let roles: Array<Role>;
roles = ["admin", "editor"]; // This will only accept the roles strings and not any other.
```

We could also write this like this:

```javascript
let roles: Role[];
```

Nonetheless this is an example of a **generic type**, a **built-in** generic type, but we can also built our own generic types As we mentioned before, generic types are types that work with another types.

But let's say that we create a custom type `DataStorage`, that will have extra type information that we don't know yet. So we'll need a `Generic Type`, so we'll create it like this

```typescript
//This is a custom generic type to create multiple storages for different data
type DataStorge<T> = {
  storage: T[],
  add: (data: T) => void,
};

const textStorage: DataStorage<string> = {
  storage: [],
  add(data) {
    this.storage.push(data);
  },
};

const userStorage: DataStorage<User> = {
  storage: [{name: 'Max', age: 34, isAdmin: true, id: 'abc1'}],
  add(user)
};


```

So, now we have a `custom generic type` that is flexible, because now we can have multiple storages for different data. It's worth noting that in Typescript that this is not the only way to create a custom generic type. You can not just define generic types like this with help of the `type` keyword, instead you can for example also define a so-called generic function

```typescript
function merge<T, U>(a: T, b: U) {
  return {
    ...a,
    ...b,
  };
}

const newUser = merge<{ name: string }, { age: number }>(
  { name: "Max" },
  { age: 34 }
);

newUser.name; //Max
```

Now, since we have such a generic function, we can omit some information that could be easily inferred by the compiler

```typescript
function merge<T, U>(a: T, b: U) {
  return {
    ...a,
    ...b,
  };
}
const newUser = merge({ name: "Max" }, { age: 34 });
newUser.name; //Max
```

## Using TypeScript with React <a name="typescript-with-react)"></a>

### Creating a React + TypeScript Project

Now we're going to switch to a React project where the compiler will be part of that project and where it will actually be part of a build pipeline that can be invoked when we want to prepare our overall application for production.

### Understanding the role of tsconfig.json

This file not only contains TypeScript configuration, it will also be picked by the IDE (Integrated Development Environment) in this case Visual Studio Code (VSC) that will adjust how to show errors based on the setting of this file.

### Defining Component Props Types

```javaScript
export default function CourseGoal ({title, description}: {
    title: string;
    description: string;

}) {
    return(
    <article>
        <div>
            <h2>{title}</h2>
            <p>{description}</p>
        </div>
        <button>DELETE</button>
    </article>
)}
```

By using `{title, description}` JS destructiong syntax, we don't have to write `props.title, props.description`

### Defining a Type for Props with children

You can use

```typescript
//the TYPE decorator is a special decorator use in TypeScript projects to make it clear to the built tool that this is an IMPORT that can be removed

import { type ReactNode } from "react";

interface CourseGoalProps {
    title: string;
    children: ReactNode; //Type
};

export default function CourseGoal ({
    title,
    children
}: CourseGoalProps) {
...}
```

Our use `PropsWithChildren`

```javascript
type CourseGoalProps = PropsWithChildren<{ title: string }>;
```

### Components Props & the special "key" prop

All React components (built-in components and also your custom components) do accept a special key prop which is used by React to track specific component instances.

For example, the key prop should always be set when outputting a list of components.

This key prop can be set on custom components even if you didn't specify it in your props type!

For example, the following component code will work:

```javascript
type UserProps = {
  name: string,
};

function User({ name }: UserProps) {
  return <li>User: {name}</li>;
}

function App() {
  const users = [{ name: "John" }, { name: "Mary" }, { name: "Luke" }];

  return (
    <>
      <ul>
        {users.map((user, index) => (
          <User key={user} name={user.name} />
        ))}
      </ul>
    </>
  );
}
```

### Another Way of Typing Components

The type FC stands for Funtional Component, and this tells React that the function we do assing in this variable or constant will be such functional component.
FC is also a generic type where the connected type is the props type

```typescript
import { type FC, type ReactNode } from "react";

interface CourseGoalProps {
  title: string;
  children: ReactNode; //Type
}

const CourseGoal: FC<CourseGoalProps> = ({ title, children }) => {
  return (
    <article>
      <div>
        <h2>{title}</h2>
        <p>{children}</p>
      </div>
      <button>DELETE</button>
    </article>
  );
};
export default CourseGoal;
```

### Header Component

```javascript
import { type ReactNode } from "react";

type HeaderProps = {
  image: {
    src: string,
    alt: string,
  },
  children: ReactNode,
};

export default function Header({ image, children }: HeaderProps) {
  return (
    <header>
      <img src={image.src} alt={image.alt} />
      {children}
    </header>
  );
}
```

Or we can shorther the image element by distributing the image object `<img {...image} />`

### Using useState() and TypeScript

When we initially set `useState` like this: `const [goals, setGoals] = useState([]);` and hover over `goals` we would notice that it says is a `never[]` which is an array of unknown types, therefore we'll never be able to tweak it.

### Handling and Type Events

`FormEvent` is a type provided by React, that we using only during development to type properly an event:

```javascript
import { type FormEvent } from "react";

export default function NewGoal(){
    function handleSubmit(event: FormEvent){
        event?.preventDefault();
    }
```

This makes it clear that the event is NOT undefined, that this event will always be set.
It's important to underdstand that sometimes your vent handling functions must be typed properly to correctly reflect the type of event that is being emitted.

If we have defined our function inside the form element, TypeScript would have inferred the type of event`<form onSubmit={(event)=>{}}>`

### Working with Generic Event Types

Now, that we got our base for set up, we need to extract the entered information. We got a couple of options:

- Use `useState` and two-way binding to get the current value
- Use the built-in `FormData` class that is provided by the browser
  The `FormEvent` is a Generic type and can be enriched with extra type information about a related type. In this case the related type of the form event is the HTML element or the type of HTML element that is responsible for this event.

```javascript
function handleSubmit(event: FormEvent<HTMLFormElement>) {
  event.preventDefault();
}
```

### Using useRef() with TypeScript

- When debbugging typescript is usually the most nested message the one that will give you the most information about what you neeed to fix.
  Refs `const goal = useRef();` by default contain `undefined`as a default starting value and the ref prop is internally types such that it does not accept such refs that contain this type of value. So, well add `null` as a starting value here, and while it might seem to same is not. Undefined means that there is NO value at all, while null means that we don't have one YET.

```javascript
import { useRef, type FormEvent } from "react";

export default function NewGoal(){
    const goal = useRef<HTMLInputElement>(null);
    const summary = useRef<HTMLInputElement>(null);


    function handleSubmit(event: FormEvent<HTMLFormElement>){
        event.preventDefault();
        // By adding ! we signal that while this is NULL at the moment, one a user clicks submit this will have a value for certain
        const enteredGoal = goal.current!.value;
        const enteredSummary = summary.current!.value;
    }

    return (
    <form onSubmit={handleSubmit}>
        <p>
            <label htmlFor="goal">Your goal</label>
            <input type="text" id="goal" ref={goal} />
        </p>
        <p>
            <label htmlFor="summary">Short summary</label>
            <input type="text" id="summary" ref={summary} />
        </p>
        <p>
            <button>Add Goal</button>
        </p>
    </form>
    )
}
```
