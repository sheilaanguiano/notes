# React and TypeScript - The Practical Guide

---

Platform: Udemy
Instructor: Maximilian Schwarzmuller
Author: Sheila Anguiano

---

# Table of Contents

1. [Introduction](#intro)
2. [TypeScript Basics & Core Concepts](#basics)

## Introduction <a name="intro"></a>

### Why React and TypeScript?

TypeScript builds on JavaScript and extends its synta by adding stront typing.
TypeScript helps you catch & fix type-related errors-earlier, but someties that comes at the expenses of having to define complex value types

## TypeScript Basics & Core Concepts <a name="basics"></a>

### TypeScript Setup & Using TypeScript

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

You can delare `let hobbies: Array`, but you also need to suplement the complementary data type to specify what type of data is going to be in said array

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

But for this specific scenario we have a better return type, that you should use instead if you have a function without a return statement, and that's the `void`type, which is another type built into Typescript thats meant to be used if you have a function without a return statement or if your function doesn't return anything.

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

A problem with the function definitions is that sometimes they can get quite long. So you can create a custom type or to be more precise to assung an alias to some other type

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

interfcace Crendentials {
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
let admin: AppAdminl

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

### Addint Type Guards

When working with Union Types, sometimes you may want to check the exact value. For example lets say we want to create Function only applicable when thereole es `admin`

```javascript
type Role = "admin" | "user" | "editor";

let rike: Role;

function perfomAction(action: string | number, role: Role) {
  if (role === "admin" && typeof action === "string") {
  }
}
```

The above Type Safeguard is a common pattern. When using "Type Guards" TypeScript performs so-called "Type Narrowing".

You CANNOT check if a value meets the definition of a custom type(type alias) or interface type

### Making Sense of Generic Types

Generic Types lile "Array" are types that work with another types such as:

```javascript
let roles: Array<Role>;
roles = ["admin", "editor"];
```

But let's say that we create a custom type `DataStorage`, that will have extra type information that we don't know yet. So we'll need a `Generic Type`, so we'll create it like this

```javascript
type DataStorge<T> = {
  storage: T[],
  add: (data: T) => void,
};

const textStorage: DataStorage<string> = {
  storage: [],
  add(data) {},
};
```

So, now we have a `custom generic type` that is flexible, because now we can habve multiple storages for different data. Go back to Min 6
