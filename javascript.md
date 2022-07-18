# JavaScript
-----

Author: Sheila Anguiano

-----
# Table of Contents 
1. [Basics](#basics)
2. [Numbers](#numbers)
3. [Functions](#functions)
4. [Loops](#loops)
5. [Arrays](#arrays)
6. [Objects](#objects)
7. [The Landscape of JavaScript](#landscape)
8. [JavaScript and the DOM](#dom)
9. [Interacting with the DOM](#interacting-dom)
10. [Debbuging javaScript in the Browser](#debbuging-browser) 
11. [String Manipulation in javaScript](#string-manipulation)
12. [Callback Functions in JavaScript](#callback-functions)
13. [AJAX](#ajax)
14. [Asyncronous Programming with JavaScript](#asyncronous-js)
15. [Working with the Fetch API](#fetch)
16. [Object Oriented JavaScript](#ooj)
17. [The JavaScript Ecosystem](#js-ecosystem)

## Basics <a name="basics"></a>
A programming language’s **syntax** is the different commands, special words and punctuation you use to put together a program.

Every **browser** has a **JavaScript interpreter** built into it. This is the part of the browser that reads, understands and runs the instructions in a JavaScript program.

When a browser reads and acts on a JavaScript program, we call that running the program or executing the program

You can use JavaScript in HTML in 2 ways:

-   A separate scripts.js file, linked to the HTML file, using the  `<script>`  element nested inside the head element or just before closing the body element (BEST OPTION):  `<script src=”scripts.js”> </script>`
    
-   Or write the JS statements inside the HTML document using the  `<script> </script>`  tags nested inside the HTML head element

A **variable** is a way of storing and keeping track of information in a program. JavaScript has three kinds of variable declarations

**var**  Declares a variable, optionally initializing it to a value. Still used in old JS development but has been replaced with const and let. 
**let** works similar to _var_ but prevents you from declaring a variable more than once or in other words it declares a block-scoped, local variable. The `let` keyword is especially useful in for loops.Using var to define the counter in a for loop can lead to some really confusing and unexpected outcomes.
**const** which is short for constant, let’s you protect the variable for being over written. It declares a block-scoped, read-only named variable. However `const` doesn’t prevent complex objects like arrays and objects from being modified. (push method or adding by .notation). It just prevents from being reassigned or over written completely.

**Programming Note**: Is good practice to follow **indentation** when coding as a best practice

```JavaScript
var score; // Initializing a Variable  
let variable = 'value'; // Assigning a value to a variable
```
When naming variables there are certain **keywords** and **reserved words** that you cannot use, so to be safe you can follow the following naming conventions:
-   Can’t start with numbers
-   Names can only contain letters, numbers and the  `$`  and  `_`  characters
-   Use descriptive names for variables, even if it requires more typing, your programs will be a lot easier to understand. As a programmer you should strive to write understandable, readable code.
- `variableCamelCase`

The information stored in a **variable** is called a **value**, these values come in many different types called **data types** that are built-in the language and treated in different way

### Data Types

- **String** : The JavaScript engine treats _strings_ as objects, this unlocks a slew of additional functionalities you can use with strings using what are called _properties_ and _methods_.
```JavaScript
/* Strings are a series of letters, digits, and other characters 
   inside a single or double quotation marks.
*/
const msg = "Hello World!";

//Example of a string with a escaped character
const msg2 = 'Hello again, I\'m a programmer!';
```
Different types of objects have different properties, and you can access a property of an object using a dot. A **property** is kind of like a variable, it holds information. A property is dynamic and can change, whereas a **method** is something that you can do with an object, and action that you can perform on a string

```JavaScript
//Example of an object PROPERTY
const passphrase = "I have Spoken";
console.log(passphrase.toUpperCase()); // "I HAVE SPOKEN";

//Example of an object METHOD
const name = prompt('What is your name?');
alert(name);

/*
STRING CONCATENATION is the process of combining two or more
strings
*/
const name = prompt("What's your name?");
let msg = "Hello " + name;

/*
TEMPLATE LITERALS is a more intuitive way to combine strings
where whatever is inside the curly braces gets evaluated by the 
JavaScript engine and added, this process is called INTERPOLATION
*/
const message = `Hello, ${name}. Welcome to my music site.
It's ${2+ 3} o'clock`;
console.log(message);
```
**Programming Note**: You can display information on the webpage using
```JavaScript
`document.querySelector('html element tag').innerHTML = '<h2>This is a H2</h2>';`
```

- **Boolean**: is a logical data type that can have only the values `true` or `false` and are particularly important in **conditional statements** along with **comparison operators** to control the flow of a program

The most important part of a conditional statement is the condition itself. It's a test that checks to see if something is either true or false
```JavaScript
// The condition is a test whose answer is either true or false.
if(condition1){
	//code block that runs IF the condition is true
} elseif(condition2){
   // statement2
}else {
	// code block that runs IF the condition is NOT true
}
```
**COMPARISON OPERATORS**
| Operator  |            | 
|----------|:---------:|-
| > | Greater than |
| >= | Greater Than or Equal To|
| < | Less Than |
| <= | Less Than or Equal To|
| == | Equal To|
| === | Strict Equal To|
| != | Not Equal To|
| !== | Strict Not Equal To|
| && | And|
| !== | Strict Not Equal To|

Try to keep your conditional statements short and precise. When conditionals become too long or complicated, they can be challenging to track and manage. In some circumstances, it may be unavoidable.

A good rule of thumb is: if you find yourself creating a lengthy and overly complicated conditional, it might be worth taking the time to work out a more explicit, alternative approach.

**Notes**: 
- Strict Equalities compares type as well as value.

## Numbers <a name="numbers"></a>
In JavaScript, data types like strings, booleans and numbers are formally called **Primitive Datat Types**, because they’re basic values built into the language. A String or number primitive, by itself, cannot be altered or manipulated. JavaScript automatically adds a _special wrapper_ around most primitive types so that you’re able to alter them, that wrapper is called an **object**,

- You can perform most mathematical calculations
- Use shorthand version of arithmetic operations `score +=10`
- Whole numbers  are called **integers** `9`
- Decimal numbers are **floating point numbers** `9.0`
- Use scientific notation `9e-6``
- Verify the data type with `typeOf` and parse from string to num with`parseInt()` method or `parseFloat()`, but the **unary plus** (`+`)  method is becoming the preferred method to convert from string to number

In addition to arithmetic operators, JavaScript has a built-in [Math Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) used to perform complex mathematical operations on numbers like creating random numbers, rounding and more.

```JavaScript
//Gives a random number multiplied by the 6 faces of the die
Math.random() * 6;
/* Math.floor will round down to the nex integer, 
while the +1 will help avoid getting 0 as 
a random number.*/
Math.floor(Math.random * 6) + 1

/*
In this case, you might think to use Math.ceil and avoid the `+1` but that will, also cause to also return 0
*/
```

## Functions <a name="functions"></a>
JavaScript functions let you create reusable chunks of code. They make programming faster, easier, and less error-prone. At its simplest, a function is a set of instructions that you want to run over and over again.

-   Function change the flow of the program.
-   It’s common for programmers to write functions at the top of the file (in single file apps)

Functions can return a value, creating a **return statement** and can be combined with if statements to have multiple return values BUT  when a `return` statement runs, it causes the JavaScript engine to exit the function immediately, so it should be the last line of code you want to run in a function.  
In addition, the return statement can only return a single value
```javascript
//1. Create the function
function  goToCoffeeShop(){  
	return  "Your coffee is on its way";  
}  
//2. Call the function
GoToCoffeShop();

// Esxample of funcion with multiple return statements
function  ifFieldEmpty () {  
	const field = document.querySelector('#info');
	 if(field.value ===  ''){  
	 // It could also be written as if(!field.value) 
		 return  true;  
	}  else  {  
		 return  false;  
	} 
} 
```
### Functions Parameters and Arguments
JavaScript functions can also accept information called **arguments** which you pass to the function. To have a function accept an argument you add what’s called a **parameter** inside the parentheses when creating a function. The parameter works just like a variable. You can name it anything you want but need to follow the same rules when naming the parameter as you do when naming a variable.

When you pass information to a function is called  _passing an argument to the function_

You're able to pass multiple arguments to the function BUT passing more than 5 parameters can make your function tedious to use and harder to read.

JavaScript provides separate "scopes" for each function. Any variables created within a function(**Local Scope**) are not accessible outside (**Global Scope**) that function, and cannot interact with variables created in another function.

It's generally not recommended to access global variables from inside your functions, as it makes keeping track of variables and debugging difficult.

```JavaScript
function goToCoffeShop(drink){
  alert(`Your ${drink} is on the way!  `);
}

function getArea(width, length, unit){
  const area = width * length;
  return `${area} ${unit}`
}

goToCoffeeShop('Espresso');

getArea(10, 20, 'sq ft');
```
### Function Declarations and Function Expressions.
A function expression lets you assign a function to a variable, using an **anonymous function** ( a function without a name after the function keyword)

```JavaScript
//FUNCTION DECLARATION
// This type of function gets hoisted
function getArea(width, length, unit){
  const area = width * length;
  return `${area} ${unit}`
}

//FUNCTION EXPRESSION
const getArea = function(width, length, unit){
  const area = width * length;
  return `${area} ${unit}`
};

// You call them exactly the same
console.log(getArea(2, 5, meters))
```
Function declarations and function expressions work in much the same way, except for one subtle but important difference. You can call a function declaration before it's defined, because function declarations load before any code is executed. When the JavaScript file loads, the JavaScript engine behind the scenes moves all function declarations to the top of their current scope, like the global scope. Since the JavaScript engine immediately knows about any function declarations, you're able to call a function before it's declared in the file. This behavior is called **hoisting**.

The approach of  writing functions is a matter of preference, but pick one and try to stick with it through your script. Now some developers prefer the structure that functions expressions provide to their code, since you're not able to call a functions expression before is declared, it requires that you write your functions up top, in a specific order, otherwise, they won't work, an any code that calls and runs functions gets placed toward the bottom, which make your code more readable and predictable.

### Arrow Functions
Arrow functions are similar to function expressions; they're appropriately called **"arrow function expressions."**

```JavaScript
const getArea = (width, length, unit) => {
	const area = width * length; 
	return `${area}  ${unit}`; 
 };

// When arrow functions have one parameter 

const square = x => {
  return x * X;
}
// You can make them one line
const square = x => { return x * x};

// Or use an IMPLICIT RETURN, avoiding even the curly brackets
const square = x =>  x * x;
 ``` 

### Default Function Parameters
JavaScript lets you assign default values to your function parameters. That way if for any reason you don't pass a certain argument to a function, the function user or falls back to the default value.

```JavaScript
function sayGreeting(name){
  return `Good morning, ${name}!`;
}

sayGreeting();
// Good morning, undefined!
```

```JavaScript
function sayGreeting(name = 'student'){
  return `Good morning, ${name}!`;
}

sayGreeting();
sayGreeting('Maria');
// Good morning, student!
// Good morning, Maria!
```
When you have multiple parameters in your functions, you just have to be mindful of the order or which arguments you omit to pass
```JavaScript
function sayGreeting(greeting, name = 'student'){
  return `${greeting}, ${name}!`;
}

sayGreeting();
sayGreeting('Buenos dias','Maria');
// undefined, student!
// Buenos dias, Maria!
```
### Descriptive Comments for Functions
Developers often use descriptive comments in their programs for function documentation. The comments provide a high-level overview of what a function does, its parameters, and return value.

There is a standard syntax you can use to document functions -- it's known as [JSDoc](https://jsdoc.app/index.html), and the format looks like this:
```JavaScript
/**
 * [A short description of the myFunc function] 
 * 
 *  @param {[param type]} param1 - [parameter description] 
 * @param {[param type]} param2 - [parameter description] 
 * @returns {[return type]} [documents the function's return value] 
 */   

function myFunc( param1, param2 ) {
 // function returns a value... } 
```
When using the JSDoc approach, place a comment immediately before the function you are documenting. Each comment begins with  `/**`. Let's go over each line in the comment sequence:

-   The first part of the comment is a  [short and simple description](https://jsdoc.app/about-getting-started.html)  of what the function does. Below the description, you add more information with  `@`  tags.
-   The  [`@param`](https://jsdoc.app/tags-param.html)  tag provides the name, type, and description of a function parameter. Use one  `@param`  tag for each parameter you define.
-   The  [`@returns`](https://jsdoc.app/tags-returns.html)  tag (also  `@return`) documents the value the function returns with a type and description.

Besides  `@param`  and  `@returns`, there are other useful tags like  [`@throws`](https://jsdoc.app/tags-throws.html),  [`@example`](https://jsdoc.app/tags-example.html),  [`@author`](https://jsdoc.app/tags-author.html), and  [many more](https://jsdoc.app/index.html#block-tags)

```JavaScript
/**
 * Calculates and returns the area of a rectangle. 
 *  
 * @param {number} width - The width of the rectangle. 
 * @param {number} length - The length of the rectangle. 
 *  @param {string} unit - The unit of measurement. 
 * @returns {string} The area of the rectangle and unit of measure. 
 */   

function getArea(width, length, unit) {
 const area = width * length; return `${area}  ${unit}`; } 
```
Besides its descriptive format, the JSDoc tool itself has other useful and powerful features. JSDoc is also a documentation generator for JavaScript.

For example, when you add documentation comments directly to your source code, JSDoc can scan your code and  [generate an HTML documentation website](https://jsdoc.app/about-getting-started.html#generating-a-website)  for you.

JSDoc also has built-in support in text editors like  [Visual Studio Code](https://code.visualstudio.com/). VS Code can use the  [JSDoc annotations](https://code.visualstudio.com/docs/languages/javascript#_jsdoc-support)  to provide code completion, hover information, and function signature information to help you write code more quickly and correctly.

Using a consistent and descriptive commenting approach makes your functions more predictable. Other developers who need to learn about your functions will have a faster and easier way to identify each part of a function.

### Function Challenge
My Solution
```JavaScript
function randomNum(lower, upper){
  const random = Math.floor(Math.random() * (upper - lower)) + lower;  
  return console.log(random)
```
Teacher solution
```JavaScript
function getRandomNumber(lower, upper){
  return Math.floor(Math.random() * (upper - lower + 1)) + lower;
}
console.log( getRandomNumber(2,28));
console.log(`${getRandomNumber(10,100)} is a random number between 10 and 100`);
     
```
In the teacher's answer, he can use `return` because all the operation returns a value

### Testing for Number Arguments
```JavaScript
function getRandomNumber(lower, upper){
  if(isNaN(lower) || isNaN(upper)){
    throw Error('Both arguments must be numbers');
  }
  return Math.floor(Math.random() * (upper - lower + 1)) + lower;
}
```
## Loops <a name="loops"></a>
A **loop** repeat the same set of actions a certain number of times or until a specific condition is true

### While Loop
Use the `while` statement to create a loop that executes code as long as a condition evaluates to true.

```JavaScript
//code 10 random numbers

function getRandomNumber(upper){
  return Math.floor(Math.random() * upper) + 1;
}

let counter = 0;
while( counter < 10 ){
  console.log(`The random number is ${getRandom(10)}`);
  counter += 1;
}
```
### The do...while Loop
Use `do...while` to create a loop that executes code until the test condition evaluates to false, with the difference that `do...while` will always execute the do

So use `do...while` when  you need your loop to execute at least one time.
```JavaScript
//code 10 random numbers

function getRandomNumber(upper){
  return Math.floor(Math.random() * upper) + 1;
}

let counter = 0;
do {
  console.log(`The random number is ${getRandom(10)}`);
  counter += 1;
} while ( counter < 10 );
```
### The For Loop
The `for` loop is a more compact variation of the while loop, with similar parts, and it’s useful when you know how many times you want to repeat an action.

```JavaScript
function getRandomNumber(upper){
  return Math.floor(Math.random() * upper) + 1;
}

for(let counter = 0; counter <10; counter++){
  console.log(`The random number is ${getRandom(10)}`);
}

for (let i = 0; i < 10; i++){
 console.log(`The random number is ${getRandom(10)}`);
}
```
- It's so common in JavaScript to increment a number value by one that there's a shorthand operator (called the "increment operator") that's used frequently with loops. Use it on your variables by replacing `+= 1` with two plus symbols (`++`).
- Beware of infinite loops. You need a way to break out of the loop. In other words, something has to change inside the loop to stop it from running. There are a few ways to do this. One way is with a keyword you'll learn about in the next stage called `break`.

```JavaScript
const secretWord = 'tomato'; 
let message = 'Access denied :(';

for ( let i = 5; i >= 1; i-- ) {  
 let guess = prompt(`Enter the secret word. You have ${i} tries.`); 
 
 if ( guess === secretWord ) { 
 message = 'Welcome to the secret loop world!'; 
 break;  // immediately terminate the loop 
	 } 
}   

alert(message);
```
### Refactor
Review and improve code by using the DRY (Don't Repeat Yourself) principle. Loops and functions help with DRY.

Programmers call the process of improving and simplifying code without changing its behavior refactoring
- Programmers first write a program that works perfectly well, and later rewrite it to be less repetitive, more efficient and maintainable.
- Improving code also might mean making it run faster, easier to read or adding comments

## Arrays <a name="arrays"></a>
Arrays provide a way to store multiple pieces of information. An array is a list of values: numbers, strings, boolean values, or even other arrays

**array literal**: Is a list of zero or more expressions, which represent and array element enclosed in square brackets (`[]`). When you create an array using an array literal, it is initialized with the specified values as its elements, and its `length` is set to the number of arguments specified.

```JavaScript
//array literal
const shoppingList = ['bread', 'butter', 'milk'];

// A better way to write more legible and easier to edit arrays
const planets = [
  'Mercury',
  'Venus',
  'Earth',
  'Mars'
 ];
```

### Access Elements in an Array
An array doesn't quite represent a single value. It's a list of multiple values, or **array elements** . To access a single element within an array, you use what's called an **index** value, which is a number that indicates the position of an element in an array. Making us think of an array as a numbered list. We just need to remember that JavaScript is **zero indexed** or **zero based**. This means that the index of the first element inside an array is not 1, it's 0.

```JavaScript
const planets = [
  'Mercury',
  'Venus',
  'Earth',
  'Mars'
 ];

console.log(planets[2]);
// Earth
```
### Add Elements to an Array
In JavaScript, an array is not only a type of data structure, is also considered a special kind of object that has properties and methods you can use on it.
```JavaScript
const instruments = ['piano', 'drums', 'trumpet'];

//push adds an elements at the end of an array
instrument.push('guitar', 'violin');

//unshift add elements at the beggining of an array
instrument.unshift('cowbell', 'tuba');
```  
### Remove Elements from an Array
```JavaScript
const shoppingList = ['bread', 'butter', 'milk'];
//pop pops and returns the last element of a list
//pop doesn't accept any argument
let lastItem = shoppingList.pop();

//shift pops and returns the first element of an array
let firstItem = shoppingList.shift();
```
The push and shift methods are often used together to create highly organized data structures called **queues** or list of items that follow the logic _first out_, which is often called **FIFO**

### Copy and Combine Arrays with the Spread Operator
The spread operator (`...`), a special syntax JavaScript provides to build, combine, and manipulate arrays quickly and more seamlessly.
```JavaScript
const middle = ['lettuce', 'cheese', 'patty'];
const burger = ['top bun', ...middle, 'bottom bum'];
console.log(burger);
// ['top bun', 'lettuce', 'cheese', 'patty', 'bottom bum'] 
```
You can also use the spread operator to pass arrays as arguments
```JavaScript
const numbers = [10, 20, 30, 40];

// the max function returns the largets number from a set of number values passed into it
console.log(Math.max(numbers));
//NaN

console.log(Math.max(...numbers));
//40

```
[Spread_syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
[6 Great Uses of Spread Operator](https://davidwalsh.name/spread-operator)

### Loop through arrays
The `for` loop provides one way to loop (or iterate) through the elements in an array.
```JavaScript
const students = ['Lee', 'Mali', 'Sariah'];
for( let i = 0; i < students.length; i++ ){
  console.log(students[i]);
}
// Lee
//Mali
//Sariah
```
Another example of Loops through arrays and inserting into HTML

```JavaScript
const playlist = [
  'So What',
  'Respect',
  'What a Wonderful World'  
];

function cretaeListItems(arr) {
  let items = ''
  for ( let i = 0; i < arr.lenght; i++ ){
    items += <li>${ arr[i] }</li>;
  }
  return items;
}

document.querySelector('main').innerHTML= `
  <ol>
    ${ createListItems(playList)}
  </ol>
`;
```
Getting an average of an Array of Scores
```JavaScript
const scores = [ 20, 50, 75, 100, 115 ]; 
let total = 0;   

for ( let i = 0; i < scores.length; i++ ) {
	total += scores[i]; 
}   
console.log( total / scores.length );
```

[Common array_operations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Common_operations)

### Useful Array Methods
* `join()` takes an array and returns a string holding all the elements in the array, separated by a supplied character, like a comma or a colon. This is a great way to display all the elements in a single line.
```JavaScript
const daysInWeek = [
 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday' ];
daysInWeek.join('')
//"MondayTuesdayWednesdayThursdayFridaySaturdaySunday"
```
* `includes()`  determines whether an array includes a certain value among its entries, and returns either tru or false. This method is case sensitive
```JavaScript
const fruit = [
 'apple', 'orange', 'grapefruit', 'pineapple', 'strawberry' ];

fruits.includes('Apple');
//false
fruits.includes('apple');
//true
```
* `indexOf()`  to return the index or position of an element inside an array.
```JavaScript
const fruit = [
 'apple', 'orange', 'grapefruit', 'pineapple', 'strawberry' ];

fruits.indexOf('apple');
//0
fruits.indexOf('pear');
//-1
```
### Exercise: Search for a value in an array
```JavaScript
const inStock = [
	'pizza',
	'cookies',
	'eggs',
	'apples',
	'milk'
];

const search = prompt('Search for a product.');
let message;

if(inStock.includes(search)){  
  message = `Yes, we have: <strong>${search}</strong>`;
} else {
  message = `Sorry, we do not have <strong>${search}</strong>`;
}

document.querySelector('main').innerHTML = `<p>${ message }</p>`
```
A more polished solution, taking in consideration getting null strings and case sensitivity

```JavaScript
const inStock = [
	'pizza',
	'cookies',
	'eggs',
	'apples',
	'milk'
];

const search = prompt('Search for a product.');
let message;

//checks for falsy values(null, empty string,etc)
if(!search){
  //If the users doesn't pass anything or we get and empty string, the following msg
  //will display a list of all the items, separated by a space and a comma  
  message = `<strong> In Stock: </strong> ${ inStock.join(', ')}`;
} else if(inStock.inclues(search.toLowerCase())){
  message = `Yes, we have ${ search }. It's #${ inStock.indexOf(search.toLowerCase()) + 1} on the list.}` ;
} else {
  message = `Sorry, we do not have ${ message }`;
}

document.querySelector('main').innerHTML = `<p>${ message }</p>`
```
### Multidimensional Arrays (Two dimensional array)
You can place an array within an array, even create an array that contains nothing but other arrays. An array inside an array is called a "multidimensional array".

```JavaScript
const playlist = [
  ['So What', 'Miles Davis', '9:04'],
  ['Respect', 'Aretha Franklin', '2:45'],
  ['What a Wonderful World', 'Louis Armstrong', '2:21'], 
  ['At Last', 'Ella Fitzgerald', '4:18'], 
  ['Three Little Birds', 'Bob Marley and the Wailers', '3:01'], 
  ['The Way You Look Tonight', 'Frank Sinatra', '3:21']
];

const myArtists = `${playlist[0][1]}, ${playlist[1][1]}, ${playlist[5][1]}`;

function  cretaeListItems(arr)  {  
	let items =  '';  
	for  (  let i =  0; i < arr.lenght; i++  ){ 
		items +=  <li>${ arr[i][0], by ${ arr[i][1] } - ${ arr[i][2] } }</li>`;  
	}  
    return items;  
}

document.querySelector('main').innerHTML=` <ol> ${ createListItems(playList)} </ol> `;
```


## Objects<a name="objects"></a>
Objects are an essential part of JavaScript; they provide a flexible way to keep track of data by associating a name with a particular value.

In JavaScript, anything that is not a primitive type (`undefined`, `null`, `boolean`, `number`, or `string`) is an **object**.

JavaScript is often referred to as an object-based programming language, which means that the language is made up of different types of objects.

One of the simplest ways to think of an object is something that has **properties** and **methods**. 

A property is like a variable that belongs to the object, and a method is something that objects can do or that can be done to the objects.

You've already worked with two ways of storing data in JavaScript: 
* assigning a value to a variable
* storing a list of values in an array.

JavaScript objects let you store data as what are called **key value pairs** or property value pairs. 

A key, or property name, is like a variable, and a value is like the value of that variable.

To make object literals more readable, developers place each key value pair on its own line.
```JavaScript
const person = {
  name: 'Edward',
  city: 'New York',
  age: 37,
  isStudent: true,
  skills: ['JavaScript', 'HTML', 'CSS']
};
```
[Objects Basics](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics)
[Object_literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#Object_literals)

### Access Object Properties
JavaScript Objects let you store multiples pieces of information in a single variable. There are two different ways to access the value inside an object


```JavaScript

const student = {
  name: 'Arnold',
  age: 24
}

/****  Providing the property's name as a string ****/

student['name']

/**** Or with Dot Notation ****/

student.name
/**** And can be used like this  ****/

const message = `Hi, I'm ${student.name}.`
console.log(message);

```

[Objects_and_properties](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Objects_and_properties)


### Set the Value of Object Properties
You can also use dot notation to set the value of an object's properties
```JavaScript
...
person.nickname = 'Duke'

const person = {
  name: 'Edward',
  city: 'New York',
  age: 37,
  isStudent: true,
  skills: ['JavaScript', 'HTML', 'CSS']
  nickname = 'Duke'
};
```
You can also use math to update properties or methods.
```JavaScript

const message = `Hi, I'm ${person.name}. 
				I live in ${person.city}. 
				Most know me as ${person.nickname. 
				My age is $person.age + 1}. 
				I have ${person.skills.length} skills: ${person.skills.join(', ')}`

console.log(message);
```

### Loop through Objects using the special `for in` loop

```JavaScript
const student = {
  name: 'Jesse',
  grades: [80, 85, 90, 95]
};

for (let propName in student){
  console.log(student[propName]);
  console.log(`${propName}: ${student[propName]}`);
}
// > Jesse
// > (4)[80, 85, 90, 95]

for (let propName in student){
  console.log(`${propName}: ${student[propName]}`);
}
//> name: Jesse
//> grades
```
### Useful JavaScript Object Methods
The **`Object.keys()`** method returns an array containing the property names (or keys) of an object.
```JavaScript
const person = {
	 name: 'Reggie', 
	 role: 'Software developer', 
	 skills: ['JavaScript', 'HTML', 'CSS'], 
	 isTeacher: true 
};   
// Store the keys of the `person` object in `personProps` 
const personProps = Object.keys(person); 
console.log(personProps);
```
```console
> (4) ["name", "role", "skills", "isTeacher"]
```
To check the **length of an object** or in other words the num of properties:
```JavaScript
console.log( Object.keys(person).length );  // 4 
```
The **`Object.values()`** method returns an array of a given object's property  values, in the same order as provided by a `for...in` loop.
```JavaScript
const personVals = Object.values(person); 
console.log(personVals);
```
```console
> (4) 
[ 
	"Reggie", 
	"Software developer", 
	["JavaScript","HTML","CSS"], 
	true 
]
```
You can also use the **spread operator**
```JavaScript
const name = {
	firstName: 'Reggie', 
	lastName: 'Williams', 
};   
const role = {
	title: 'Software developer', 
	skills: ['JavaScript', 'HTML', 'CSS'], 
	isTeacher: true 
};   

// merge `name` and `role` into a `person` object 
const person = {  
 ...name, 
 ...role 
}; 
console.log(person);
```
```console
{ 
	firstName: "Reggie", 
	lastName: "Williams", 
	title: "Software developer", 
	skills: ["JavaScript", "HTML", "CSS"], 
	isTeacher: true 
}
```
### Store Objects in Arrays
```JavaScript
const questions = [
   { 
    question: 'How many planets are in the Solar System?', 
    answer: '8' 
    }, 
   { 
    question: 'How many continents are there?', 
    answer: '7' 
   }, 
   {
    question: 'How many legs does an insect have?', 
    answer: '6' 
  }, 
  { 
    question: 'What year was JavaScript created?', 
    answer: '1995' 
   } 
];

// 2. Store the number of questions answered correctly
const correct = [];
const incorrect = [];
let correctAnswers = 0;
/*
3. Use alop to cycle through each questions
  - Present each question to the user
  - Compare the user's response to answer in the array
  - If the response matches the answer, the number of answered questions increments by 1
*/

for (let i =0; i< questions.length; i++) {
  let questions = questions[i].question;
  let answer = questions[i].answer;
  let response = prompt(question);

  if (response === answer){
    correctAnswer++;
    correct.push(question);
    } else {
      incorrect.push(question);
    }
  } 
```
### Object Challenge
Data File
```JavaScript
const pets = [
  {
    name: 'Joey',
    type: 'Dog',
    breed: 'Australian Shepherd',
    age: 8,
    photo: 'img/aussie.jpg'
  },
  { 
    name: 'Patches',
    type: 'Cat',
    breed: 'Domestic Shorthair',
    age: 1,
    photo: 'img/tabby.jpg'
  },
  { 
    name: 'Pugsley',
    type: 'Dog',
    breed: 'Pug',
    age: 6,
    photo: 'img/pug.jpg'
  },
  { 
    name: 'Simba',
    type: 'Cat',
    breed: 'Persian',
    age: 5,
    photo: 'img/persian.jpg'
  },
  { 
    name: 'Comet',
    type: 'Dog',
    breed: 'Golden Retriever',
    age: 3,
    photo: 'img/golden.jpg'
  }
];
```
Directory File
```JavaScript
let html = '';

for(let i = 0; i < pets.length; i++){
  let pet = pets[i];  
  
    html+= `
    <h2>${pet.name}</h2>
    <h3>${pet.type} | ${pet.breed}</h3>
    <p>Age: ${pet.age}</p>
    <img src="${pet.photo}" alt="${pet.breed}"> 
  `;
}

document.querySelector('main').insertAdjacentHTML('beforeend', html); 
```
The `insertAdjacentHTML()` is a more efficient method to insert data than `innerHTML` which is why we're using it in this case.

[insertAdjacentHTML( )](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML)


## Landscape of JS <a name="landscape"></a>
JavaScript is a cross-platform language. It's used in web and native application development, virtual reality, even to build voice-controlled bots, games, and just about anything you can think up.

In 1995 Marc Andressen, the founder of Netscape gave Brendan Eich an engineer the job to develop a new scripting language. In 10 days he designed and created a new programming language named, Mocha, which was subsequently changed to LiveScript during beta releases of Netscape 2.0 and finally changed to JavaScript as a marketing ploy to cash in on the popularity of Java at the time.

JavaScript's design decisions were mostly influenced by programming languages such as [Self](https://en.wikipedia.org/wiki/Self_(programming_language))  and  [Scheme](https://en.wikipedia.org/wiki/Scheme_(programming_language)). The object-oriented and prototype-based programming language Self inspired JavaScript’s prototypal inheritance, and Scheme likely influenced its [functional](https://en.wikipedia.org/wiki/Functional_programming)  and [imperative](https://en.wikipedia.org/wiki/Imperative_programming) styles of programming.

### JavaScript as a Cross-Platform Language
Although originally designed to run in the browser, JavaScript is now a cross-platform language. Once you understand the basics, you can begin to work with JavaScript in all sorts of fascinating ways!

* IoT Device (Internet of Things Device): Any physical device with and on/off swith that can be connected to the internet and with other IoT devices.

**JavaScript in Google Apps and Microsoft Office**
[https://docs.microsoft.com/en-us/office/dev/add-ins/overview/office-add-ins](https://docs.microsoft.com/en-us/office/dev/add-ins/overview/office-add-ins)
[https://developers.google.com/apps-script/add-ons/](https://developers.google.com/apps-script/add-ons/)

 **JavaScript in native, and cross-platform desktop applications**
[https://facebook.github.io/react-native/](https://facebook.github.io/react-native/)
[https://electronjs.org/](https://electronjs.org/)

**JavaScript and VR**
[https://facebook.github.io/react-360/](https://facebook.github.io/react-360/)
[https://medium.com/airbnb-engineering/prototyping-with-react-vr-4d5ab91b6f5a](https://medium.com/airbnb-engineering/prototyping-with-react-vr-4d5ab91b6f5a)
[https://www.youtube.com/watch?v=8M7DhNEQcfs](https://www.youtube.com/watch?v=8M7DhNEQcfs)

**JavaScript and the Internet of Things**
[https://teamtreehouse.com/library/javascript-and-the-internet-of-things](https://teamtreehouse.com/library/javascript-and-the-internet-of-things)

 **JavaScript in Machine Learning**
[https://js.tensorflow.org/](https://js.tensorflow.org/)

**JavaScript in Space**
[https://vimeo.com/168064722](https://vimeo.com/168064722)
[https://space.stackexchange.com/questions/9243/what-computer-and-software-is-used-by-the-falcon-9](https://space.stackexchange.com/questions/9243/what-computer-and-software-is-used-by-the-falcon-9)

**Run JavaScript outside of the browser**
[https://en.wikipedia.org/wiki/Node.js](https://en.wikipedia.org/wiki/Node.js)

### The Evolution of JavaScript
1995 - Birth of JS
1996 - Standardization of JS, renamed ECMAScript and the creation of the Ecma TC39 committee
1997- First edition of EcmaScript, followed by edition 2 and 3, by 2003 the Ecma TC39 disbanded
2008 - The EcmaTC39 reunited and introduced ECMAScript 5
2016 - Saw the 6th release of ECMAScript officially renamed ECMAScript 2015

[https://www.ecma-international.org/](https://www.ecma-international.org/)
[https://en.wikipedia.org/wiki/ECMAScript](https://en.wikipedia.org/wiki/ECMAScript)
[https://github.com/tc39](https://github.com/tc39)

### The Different Flavors of JavaScript
-  ** Vanilla, Plain or Pure JS** : The use of JavaScript without any frameworks or libraries. In other words, native, standard-based JavaScript
-   **Type Checkers for JavaScript**: Developer use type checking languages in libraries like TypeScript and Flow in favor of pure JavaScript because they help catch mistakes early and identify certain types of problems before they run their code.
	-   TypeScript - Developed by Microsoft. Needs to be compiled
	-   Flow - Developed by facebook
-  **CoffeeScript** is a simple languages that adds syntactic sugar to JavaScript which means that is designed to make JavaScript easier to read in Express, with a clear and concise syntax. It also needs to be compiled
- **Dart** is an object-oriented programming language developed by Google. Developers use Dart to create complex and highly scalable apps for the web, mobile devices, and for the Internet of Things or IoT devices. Dart was even approved by ECMA

### JavaScript Tools and Workflows
JavaScript is a dynamic programming language also referred as an scripting language. A **Dynamic Programming Language** is a language that executes at runtime, runtime meaning the period of time which a program is running. There are different runtime environments for JavaScript, the most common is a web browser. Browsers have a built-in JavaScript interpreter that reads, understands the instructions in a JavaScript program. The interpreter is also referred to as the browser’s JavaScript engine

JavaScript engines
-   SpiderMonkey powers firefox
-   Chakra powers IE and Edge
-   V8 is a powerful open source engine for Google Chrome

The job of the JavaScript engine is to parse and execute JavaScript code. It takes the JavaScript code you write and converts it to a fast optimized code that can be interpreted by a browser all in the shortest possible time. Modern JS engines have a built-in compiler called JIT, or Just in Time Compiler. It compiles your JavaScript code into machine code, or code specifically designed for the browser, on the fly. This makes JS run faster by monitoring the code it’s running, resulting in performance improvements for your applications, and this process is also called run-time compilation.

[https://en.wikipedia.org/wiki/Dynamic_programming_language](https://en.wikipedia.org/wiki/Dynamic_programming_language)
[https://en.wikipedia.org/wiki/JavaScript_engine](https://en.wikipedia.org/wiki/JavaScript_engine)
[https://nodejs.org/en/](https://nodejs.org/en/)
[https://teamtreehouse.com/library/nodejs-basics-2](https://teamtreehouse.com/library/nodejs-basics-2)
[https://en.wikipedia.org/wiki/Just-in-time_compilation](https://en.wikipedia.org/wiki/Just-in-time_compilation)

### Text Editors
When building a JavaScript project, it all starts with the text editor.
-   Sublime
-   Atom
	-   Linters and Formatters: A linter reads your code to help you avoid problems and spot possible errors and a code formatter forces a consistent style important when working on a team.
-   Visual Studio Code

Atom and Visual Studio Code were built using JavaScript, with the Electron framework

### JavaScript Build Tools

As projects grow, they become more complex. When starting a new JavaScript project, one of the first things developers do is set up a build system to help manage all of the moving parts of a project.

#### Package Managers
Many JavaScript applications rely on external dependencies like libraries, frameworks and other time-saving tools, which help developers avoid having to rewrite their own solutions to common problems. Libraries, frameworks and other software are created and shared by the JavaScript community and brought into a projects using a package manager.

Package managers install and keep track of all the dependencies of a project. They also simplify the process of upgrading, configuring and removing dependencies. The most popular JavaScript package manager is npm (node package manager). Another commonly used package manager is Yarn, which was created by facebook.

#### Module Bundlers

Since JavaScript applications often use frameworks, libraries and other external dependencies, the JavaScript source code is usually split between a number of files or modules.

Module Bundlers combine all of your source code (and all of its dependencies) into a single, minified JavaScript file before it’s served to the browser. Module bundlers commonly used today in JavaScript development are **Webpack**, Roolup and Browserify.

#### Compilers
JavaScript runtime environments (like the browser) only understand standard JavaScript. Modern, complex JavaScript applications often required more than pure JavaScript. For instance, you may want to take advantage of new, cutting-edge JavaScript features that are not supported yet by all browsers. Or, you’re using a library or framework that uses a special syntax that’s not understood by browsers (like React’s [JSX](https://reactjs.org/docs/introducing-jsx.html))

  
A compiler is a tool that translate source code written using a special type of syntax into a code that can work in the browser. Typescript, for instance, has a built-in compiler that convert a TypeScript file to plain JavaScript. Babel is the most popular javaScript compiler used by developers , and it’s the most reliable way to use features from ES2015 and beyond while supporting older browsers.

#### Task Runners
JavaScript programming is challenging enough. The less work you have to do when performing repetitive tasks, the easier your job becomes. Task runners define and run common tasks in your projects. Anything you might want to do manually over and over again could be automated and handed off to a task runner, such as: 
-   Minifying your JavaScript so it can be loaded quickly and efficiently into the browser
-   Running test on your code 
-   Starting up a development server on your computer to run your app
-   Automatically reloading the browser whenever a JavaScript file is saved
-   Compiling source code from one type of syntax to another

**Gulp** is a common task runner, and **npm** (the node package manager) can also run automated tasks and is now the preferred tak runner of many.

### JavaScript Development Workflow
For larger more advanced applications with complex user interfaces and features, you’ll likely set up a build system to automate your workflow, and install a JavaScript library or framework to help increase efficiency and build your projects faster
-   [React](https://reactjs.org/) a JS library developed by facebook
-   [Vue](https://vuejs.org/) a JS framework
- [Angular](https://angular.io/) a complete JavaScript framework

Many of the frameworks and libraries provide a tool called a CLI that makes it easier to create an application without configuring any tools. They come with the tools you need to get started working on your project

## JavaScript and the DOM <a name="dom"></a>
### The Browser Environment
#### Interactive Web Pages with JavaScript
JavaScript was initially designed to run in the browser, to make webpages responsive to mouse clicks and other visitor input. It's one of the essential tools for creating fun, interactive, and useful web applications.

To make static pages interactive with JavaScript, you'll start by breaking interactivity into distinct actions:
-   Selecting elements on the page -> read or change elements 
-   Manipulating elements
-   Listening for user actions

#### What is the DOM
JavaScript runs and can be found in many places or environments these days, but the most common environment is the browser. Every browser has a built-in JavaScript engine that read, understands, and runs the instructions in a JavaScript  program. The browser environment provides ways to access and change different parts of the web page with JavaScript, but this requires an understanding of the **Document Object Model or DOM**.

You've learned that almost everything in JavaScript is an object or can be treated as an object. These objects can have properties which define their characteristics
- Properties of objects can also be accessed or set in programs we write
- Objects also have methods or properties in ab object that are functions 
- Methods allow actions ti be performed on an object.

 The DOM represents a web-page or HTML document as a tree-like structure made of objects with its own built in properties and methods, which can be read and modified with JavaScript. Just about every element or item within this document tree is referred as a **node**

Developers describe the relationship between DOM nodes in family like terms, thus the  `html` element is the `root node` of the tree and is the parent of the `head` and `body` nodes. Text nodes, the text content inside elements are the most deeply nested nodes in the tree and they do not contain other nodes.

So the source code or static HTML sent by the server is parsed by the browser and transformed into the DOM

#### The Browser's Global Window Object
The environment in which JavaScript runs is called the **host** or **global environment**. The browser as a global environment provides variables, objects, and functions additional to those in the core JavaScript language to make this happen inside the browser window.

We can explore this browser environment through the browser's developer tools.

```javascript
// alert is a browser function
alert('Hellow from the Developer Tools')
// shows the tab location
location.href
//You can look at all the properties of the window object
window
```
The browser has a global object called the `window` object containing al properties and methods available to the current browser window or what you're viewing on the browser's tab

[Web API - Window](https://developer.mozilla.org/en-US/docs/Web/API/Window)
[Web API - Document](https://developer.mozilla.org/en-US/docs/Web/API/Document)

#### Accessing the DOM
The window object also contain a really important property named `document`, which is an object and its the entry point into the DOM loaded in the current window. We can use the `document` object and some of its common properties  to select and control elements on the webpage.
```javascript
//Changes the backgroundcolor of body
document.body.style.backgroundColor= ='tomato'
```

Document – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document)
Review this  [Common CSS Properties Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference)  to learn what CSS properties look like when converted to camelCase
[`Element.remove()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/remove)

#### Introduction to Browser Events
When you load a web page in your browser and start interacting with it, you're generating all kinds of events or actions that the browser is listening for and registering behind the scenes. To have the browser do something in response to one of these events, we have to write some JavaScript to lister for a specific event, handle  and respond to it.

```javascript
//This event listener,will wait for clicks to fire up the message on the console
document.body.addEventListener('click', () => {
  console.log('You clicked the body of the page');
} )
```

### Getting a Handle on the DOM
The first step of making a web page interactive is grabbing ahold of elements you want the user to interact with. This is called selection. There are a number of ways to select elements on a web page. 

#### Select an Element by ID
There is a two-set sequence when controlling an element in the DOM with JavaScript
1- Access the element 
2- Either read its contents or manipulate it in some way
```javascript
 document.getElementById('headline').style.border = 'solid 2px red';
```
You'll usually assign the element or collection of elements returned by selection methods to a variable. It makes your code more manageable and easier to read, and let's you reuse the selected elements throughout your program

```javascript
const headline = document.getElementByid(‘headline ’);

headline.style.border = 'solid 2px red';
```
Now,  what if we set this function to a button  
```javascript
const headline = document.getElementByid(‘headline’);
const btnUpdate= document.getElementById('btn-main');

btnUpdate.addEventListener (‘click’, ( ) => {
	headline.style.color =’solid 2px red’;
});
```
#### Select Elements by Tag Name
In case you want to select an element that doesn't have an ID, or you want to select multiple elements, you can use `.getElementsByTagName()`. This method returns something called a `HTMLCollection`, this is an array-like collection of elements listed in the order they appear on the page. This collections have their own properties and methods, some which are like those of an array, such as the `.length()` property.
```javascript
//This will throw and error, because a Collection doesn't have a style property
document.getElementsByTagName(`h1`).style.color = 'yellow';

//However, this one will change the color of the first h1 on the website
document.getElementsByTagName(`h1`)[0].style.color = 'yellow';
```
An we can iterate over a collection with a Loop, like this one that assigns a different color to each `<li>` element
```javascript
const colors = ["#C2272D", "#F8931F", "#FFFF01", "#009245", "#0193D9", "#0C04ED", "#612F90"];
let listItems = document.getElementsByTagName('li');

for ( let i = 0; i < colors.length; i++ ) {
  listItems[i].style.color = colors[i];    
}
```
`document.getElementsByTagName()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByTagName)
[`HTMLCollection`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection)
[`HTMLCollection.length`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection/length)
[How to Loop Through an HTMLCollection](https://dev.to/isabelxklee/how-to-loop-through-an-htmlcollection-379k)
[Using a  `for`  Loop to Iterate Over an Array](https://teamtreehouse.com/library/using-a-for-loop-to-iterate-over-an-array)

#### Select Elements by Class Name
The document object provides a way for us to select elements in the DOM with a given class name `document.getElementsByClassName()` whichs also returns an HTMLCollection and we can iterate through it with a `for` loop, or a `for..of` loop

```javascript
const highlights = document.getElementsByClassName('highlight');

for( const highlight of highlights){
  highlight.style.bakgroundColor = 'cornsilk';
}
```
[`document.getElementsByClassName()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)
[`for...of`  – MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
[`for…of`  loop. Should I use  `const`  or  `let`?](https://stackoverflow.com/questions/58483101/for-of-loop-should-i-use-const-or-let)
[For Loops, For...Of Loops and For...In Loops in JavaScript](https://www.digitalocean.com/community/tutorials/for-loops-for-of-loops-and-for-in-loops-in-javascript)

#### Use CSS Queries to Select Page Elements
he last selectors we'll look at are `document.querySelector()` and `document.querySelectorAll()`, these are the most flexible of all the DOM selector. They accept IDs, classes, tag names and just about any valid CSS selector. They specifically work well with descendant and attribute selectors.

The `document.querySelector()` method returns the first element that matches the specified  selector as you would write it in CSS.

`document.querySelectorAll()` returns a collection of all elements or nodes matching the given selector, returning a `NodeList` which like an HTMLCollection it resembles an array, but the `Nodelist` is more flexible than an HTMLCollection

**NodeList**
- Contains element nodes and text nodes
- Iterate over it with for, for..of and forEach()

**HTMLCollection**
- Contains HTML elements only
- You can
- You can't loop over it exactly as you would an array

**NodeList vs HTMLCollection**
- HTML Collection is a live data structure and NodeList is a static data structure
- When a new elements gets appended to the DOM, an HTMLCollection will recognize the new element while a NodeList will not

[Locating DOM elements using selectors](https://developer.mozilla.org/en-US/docs/Web/API/Document_object_model/Locating_DOM_elements_using_selectors)
[`querySelector()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
[`querySelectorAll()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)
[CSS selectors – MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_Started/Selectors)
[NodeList – MDN](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)
 [HTMLCollection – MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection)
[Difference between HTMLCollection and NodeList](https://dev.to/jharteaga/difference-between-htmlcollection-and-nodelist-25bp)

### Making Changes to the DOM
#### Get and Set Content with textContent and innerHTML
`node.textContent` enables you to read or set the `textContent` of an element in the DOM
`Element.innerHTML` can do more than `node.textContent` since it can get or set the actual HTML markup contained within an element
```javascript
btnUpdate.addEventListener('click', ()  => {
	const headline =  document.getElementById('headline');
	const input =  document.querySelector('.input-main');

	headline.textContent = input.value;
	// after setting the new heading we clean up the input field
	input.value =  '';
});
```


[Invisible Content Just for Screen Reader Users](https://webaim.org/techniques/css/invisiblecontent/)
[Labeling Controls](https://www.w3.org/WAI/tutorials/forms/labels/)
[`Node.textContent`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent)
[`Element.innerHTML`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)
[`value`  property – MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLDataElement/value)
[Variable scope inside functions](https://teamtreehouse.com/library/variable-scope-3)

#### Change Element Attributes
Like the `href` attribute of an anchor element or the `action` attribute of a form element, attributes exists as properties of those element objects.
```javascript
const btnUpdate =  document.querySelector('.btn-main');

btnUpdate.addEventListener('click', ()  => {
	const headline =  document.getElementById('headline');
	const input =  document.querySelector('.input-main');
  
	headline.className =  'grow';
	headline.textContent = input.value;
	// after setting the new heading we clean up the input field
	input.value =  '';
});
```

[Standard HTML element attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes)
[Reserved keywords in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#keywords)

#### Set Inline Styles with the Style Property
  
Like most other attributes, you can get and set the inline style of an element in the DOM with the `Element.style.property`  however, unlike most other attributes, the `style` property returns an object containing a list of CSS style properties.

```javascript
//Updates the bottom border of the button  on our DOM Project
btnUpdate.style.borderBottom = '5px solid deeppink'
```
One common use for setting a style with JavaScript is to hide and unhide elements on a page
```javascript
const btnToggle =  document.querySelector('.btn-toggle');

btnToggle.addEventListener('click', ()  => {
	//Select the div to hide
	const listContainer =  document.querySelector('.list-container');
	//Create a Conditional statement to show both states of the Div
	if (listContainer.style.display ===  'none') {
		btnToggle.textContent =  'Hide List';
		listContainer.style.display =  'block';
	} else {
		btnToggle.textContent =  'Show List';
		listContainer.style.display =  'none';
	}
});
```

[Common CSS Properties Reference – MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference)
[`HTMLElement.style`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style)
[`CSSStyleDeclaration`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration)
[`removeAttribute()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/removeAttribute)
[HTML DOM  `style`  Property](https://www.w3schools.com/jsref/prop_html_style.asp)

#### Create new DOM Elements
There are various ways you might add elements to the DOM with JavaScript 
1. First we create the element
```javascript
//Selecte the Elemnt that will listen
const btnCreate =  document.querySelector('.btn-main');

btnCreate.addEventListener('click', ()  => {
	const input =  document.querySelector('.input-main');
	// We create a variable that will create an empty <li>
	const item =  document.createElement('li');
	
	//we add the content from the input elememt into the created <li>	
	item.textContent = input.value;
	input.value =  '';
});
```
[`createElement()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)
[JavaScript HTML DOM Elements](https://www.w3schools.com/js/js_htmldom_nodes.asp)

#### Append Nodes
After creating the new element we need to add it to the DOM tree, we'll do this by specifying an existing parent node like a `<ul>` and using the `ParentNode.append(child)` method. The append method will always add something at the end of the list, in case you want to do it before, you can use the `prepend()` method.

It's important to alert screen readers anytime elements are dynamically updated and added to the DOM, like items in an unordered list. The `aria-live` attribute let's screen readers know that content in a particular element will change dynamically, and that it should pay attention to it and announce those changes to the user.
```javascript
//Select the Element that will listen
const btnCreate =  document.querySelector('.btn-main');

btnCreate.addEventListener('click', ()  => {
	const input =  document.querySelector('.input-main');
	const list =  document.querySelector('ul');
	// We create a variable that will create an empty <li>
	const item =  document.createElement('li');
	
	//we add the content from the input elememt into the created <li>	
	item.textContent = input.value;
	input.value =  '';
	list.append(item);
});
```


[`Element.append()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/append)
[`Element.prepend()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/prepend)
[ARIA live regions – MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions)
[Free axe DevTools Browser Extensions](https://www.deque.com/axe/browser-extensions/)
[axe DevTools - Web Accessibility Testing in Chrome](https://chrome.google.com/webstore/detail/axe-devtools-web-accessib/lhdoppojpmngadmnindnejefpokejbdd?hl=en-US)
**Browser compatibility**

The methods  `append()`  and  `prepend()`  are  [not supported in Internet Explorer](https://developer.mozilla.org/en-US/docs/Web/API/Element/append#browser_compatibility).  [`appendChild()`](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild)  is an alternative method supported in IE; it adds a node to the end of the list of children of a specified parent node.

#### Insert HTML at Specified Positions
The `.insertAdjacentHTML` method provides more control over inserting HTML inside a parent. You pass it the HTML and text content to create as a string, and then that string gets parsed and inserted into the DOM at the position you specify
```javascript
btnCreate.addEventListener('click', ()  => {
	const input =  document.querySelector('.input-main');
	const list =  document.querySelector('ul');

	list.insertAdjacentHTML(
		'afterbegin',
		`<li>${input.value}</li>`
		);
		input.value =  '';
});
```
This method, in many cases is faster and more efficient than other insertion methods

[`insertAdjacentHTML()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML)

#### Remove Nodes
With the `ChildNode.remove()` method, you specify the child node to remove from the DOM and
```javascript
const btnRemove =  document.querySelector('.btn-remove');

btnRemove.addEventListener('click', ()  => {
	const lastItem =  document.querySelector('li:last-child');
	lastItem.remove();
});
```
[`remove()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/remove)
[`:last-child`  CSS pseudo-class – MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/:last-child)

The `remove()` method is [not supported in Internet Explorer](https://developer.mozilla.org/en-US/docs/Web/API/Element/remove#browser_compatibility). Use `removeChild()`as an alternative method supported in IE.

Might need to ADD https://teamtreehouse.com/library/interacting-with-the-dom

## Interacting with the DOM <a name="interacting-dom"></a>
### Responding to Events
#### What's an Event
Events can be anything from a click, scrolling the page, an error or even loading a page is an event.

[W3schools: JavaScript Events](https://www.w3schools.com/js/js_events.asp)
[MDN Comprehensive List of Events](https://developer.mozilla.org/en-US/docs/Web/Events#event_listing)

#### Functions as Parameters 
Functions are often called first class citizens in JavaScript, this means like other data, they can be stored in variables and most importantly passed into other functions.

Functions passed to other functions to be run at a certain time is are called **callback functions**

#### Listening to Events with .addEventListener()
`.addEventListener()` takes an event type (one of the 500 listen on MDN) and a callback function, this callback function is often called an **event handler** because it's purpose is to handle events. When `.addEventListener()` runs, it registers the handler on the event target, setting the target up to fire the handler anytime that event takes place. Using event handlers, you can make your website plagarism proof, well somewhat.
```javascript
document.addEventListener('copy', (event) => {
 alert('Please be sure to credit the author') });
```
-   [Linters in Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript#_linters)
-   [Beautify Tools : JavaScript Validator](https://beautifytools.com/javascript-validator.php)

#### The Event Object
In JavaScript, each event triggers the creating of an event object. The event object is generated by the browser and has some useful information about it, when an event handler is called, it receives an event object as its first argument, this object also give us access to methods and properties we can use to help us work with the event inside the handler.
```javascript

document.addEventListener('click', (event)=>{
  console.log(event);
});
```
### Traversing the DOM
Relationships between elements or nodes  in the DOM are described in family terms:
parent > child > grandchild
parent> child + child (siblings)

[MDN page for the Event Object](https://developer.mozilla.org/en-US/docs/Web/API/Event)

#### Even Bubbling and Delegation
We refer to events traveling from children to ancestors as **bubbling**. The reverse is **capture** where elements from the document down to the target are checked for event listeners. This means if a child receives an event which its parent has a listener for, the parent's event listener will also be triggered.

> One of the most powerful event handling patters is called **delegation**

What bubbling allows us to do is listen for events on ancestor elements, thus allowing us to write much more powerful handlers. For example, when we set a click handler on the unordered list or callback will trigger it whenever any of its children list items are clicked

For example, we wrote code to loop through all the list items and attached individual handlers to each item
```javascript
const listItems = document.getElementsByTagName('li');

for(let i =0; i< listItems.lenght; i++){
  listItems[i].addEventListener('mouseover', () =>{
    listItems[i].textContent = listItems[i].textContent.toUpperCase();
  });
}
```
With bubbling, we could just do this once on an ancestor of these list items and all events would still be caught and handle as they bubble up. This would make our code much simper to implement as well as using less of the browser's memory for all those individual listeners

> When trying to decide which element to use, remember it has to be an ancestor of the target elements for the sake of performance. In other words, a tag or element that wraps around or contains the element you're interested in.

In our exercise we'll attach it to the `DIV` and not the `UL` element
```javascript
const taskList =  document.querySelector('.list-container ul');

taskList.addEventListener('mouseover', (event)  => {
	if(event.target.tagName ===  'LI'){
		event.target.textContent = event.target.textContent.toUpperCase();
	}
});
```
#### Getting All Children of a Node with children
You'll often have times when you already have a reference to one element, and you need to get a hold of another element nearby, this is called **DOM traversal**. Traversal is just a way to move from one part of the DOM to another and select an element based on its relationship with another element.

You can get all children elements of a node with the `element.children` property, this will only return HTML elements. 

Example: Let's say we want to add  button to  list item, instead of hardcoding them, we can use the existing function that added the user's input to a list to the when  clicking a button
```javascript
btnCreate.addEventListener('click', ()  => {
	let ul =  document.getElementsByTagName('ul')[0];
	const input =  document.querySelector('.input-main');
	let li =  document.createElement('li');

	li.textContent = input.value;
	ul.appendChild(li);
	input.value =  '';
});
```
So first, we'll create separate function that attached the *remove button*
```javascript
function  attachRemoveButton(li){
	let removeBtn =  document.createElement('button');
	remove.className =  'remove';
	remove.textContent =  'X';
	li.appendChild(remove);
}
```
And now we can add it to our refactored function
```javascript
btnCreate.addEventListener('click', ()  => {
	let ul =  document.getElementsByTagName('ul')[0];
	const input =  document.querySelector('.input-main');
	let li =  document.createElement('li');

	li.textContent = input.value;
	attachRemoveButton(li);
	ul.appendChild(li);
	input.value =  '';
});
```
This will only add the new button to any new addition to the list thus we need to also add it to the previous items, by selecting all items using `element.children` and using a for loop to attach the button to every previous list item
```javascript
const taskList =  document.querySelector('.list-container ul');
const listItems = taskList.children;

for(let i =  0; i < listItems.length; i++){
	attachRemoveButton(listItems[i]);
}
```
####  Traversing up the DOM with `parentNode`
We can add the remove functionality, using the read-only `node.parentNode` property
```javascript
const taskList =  document.querySelector('.list-container ul');

taskList.addEventListener('click', (event)  => {
	if(event.target.tagName ===  'BUTTON'){
		const button = event.target;
		const li = button.parentNode;
		
		li.remove();
	}
});
```
[MDN : parentNode](https://developer.mozilla.org/en-US/docs/Web/API/Node/parentNode)
[W3Schools : parentNode](https://www.w3schools.com/jsref/prop_node_parentnode.asp)

DOM Traversing Exercises
```javascript
// STARTING POINT
const list = document.querySelector('.list');

// 1: Store the first child of the `ul` in the variable `firstItem`
const firstItem = list.firstElementChild;
firstItem.style.backgroundColor = '#04c5e6';

// 2: Using traversal, store the second list item in a variable named `nextItem`
const nextItem = firstItem.nextElementSibling; 
nextItem.style.backgroundColor = '#b7c7d0';

// 3: Store the last child of the `ul` in a variable named `lastItem`
const lastItem = list.lastElementChild;
lastItem.style.backgroundColor = '#57d6ab';

// 4: Using traversal, store the second-to-last list item in a variable named `prevItem`
const prevItem = lastItem.previousElementSibling;
prevItem.style.backgroundColor = '#f36f49';

// 5: Store the nested div in a variable named `banner`
const banner = list.previousElementSibling;
banner.className = 'banner';

// 6: Using traversal, store the wrapper div in a variable named `wrapper`
const wrapper = list.parentNode;
wrapper.style.backgroundColor = '#fcfcfc';

// 7: Using traversal, store the body in a variable named `body`
const body = wrapper.parentNode;
body.style.backgroundColor = '#f8fdf3';

```
## Debugging JavaScript in the Browser <a name="debbuging-browser"></a>
 Debbuging effectively requires 
 1. Stop execution at a given line
 2. Explore values while the apps is paused
 3. Step through code, line by line
 4. Fix bug
### Breaking on Events and Basic Stepping
Chrome Dev Tools > Sources Tab
In the sources tab, you'll find 3 panes, sometimes you might need to refresh it, so chrome updates any changes
- left pane: a file tree
- Debugging tools that we can use to Debug our code

On the right panel you can activate Breakpoint (to pause the program and different stages, using the bottom item *Even Listener Breakpoints*

[MDN page explaining "this"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
[MDN page on functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions)

### Basic and Conditional Line Breakpoints

https://developer.chrome.com/docs/devtools/

## String Manipulation with JavaScript <a name="string-manipulation"></a>
The string type describes variables made up of letters and other sequences of characters wrapped in quotation marks, Strings in Javascript are treated as Immutable (unable to be altered or updated). javaScript treats the string  similar to an object, providing properties and built in methods that allow us to access and manipulate string values. These methods can't change the value of a string once it's defined, but instead, return a completely new strTomatoTimering object.

```javascript
string = "guadalajara";
string.toUpperCase(); // GUADALAJARA
string[2] // a
```
### Search Methods
A smaller piece of a larger string is called **substring**, there is multiple ways to find a substring> JavaScript provides multiple options for searching substrings
`.indexOf()`  returns the position of the first occurrence of a specified value in a string. If the substring is present the method returns the index where it occurs. If not the method returns the value of `-1`
`.lastIndexOf()` This methods search for a substring starting from the end character
`.includes()` Includes takes a search string and an optional index to start searching. It returns `true` if the search string is present and false if not
`.startsWith()` Search if something starts with a string
`.endsWith()`

### Modification Methods
JavaScript provides methods for altering values such by separating, combining, converting or removing characters

- `.trim()` removes all white space after or before characters, but not between
- `.substring()` In some cases, we may only want to access part of a string or substring. The substring method to return a substring between two indexes or to the end of a string
- `.slice()` method extracts a section of a string and returns it as a new string, without modifying the original string.
- `.replace()` The **`replace()`** method returns a new string with some or all matches of a `pattern` replaced by a `replacement`. The `pattern` can be a string or a [`RegExp`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp), and the `replacement` can be a string or a function called for each match. If `pattern` is a string, only the first occurrence will be replaced.
- `.replaceAll()` replaces all instances of the string.
- `.split()` allows us to break a string into an array
- `.join()` if you need to convert the array back into a string, this is the method 
- `.parseInt()` takes a string and converts it to a number and we can go back using the `.toString` method.


## Callback Functions in JavaScript <a name="callback-functions"></a>
Callback functions are a foundational concept in JavaScript. Callbacks are used in timers, user interaction events, loading data from a server and used in Node.js


## AJAX Basics <a name="ajax"></a>
AJAX is an important front-end web technology that lets JavaScript communicate with a web server. It lets you load new content without leaving the current page, creating a better, faster experience for your web site’s visitors

AJAX lets you build web pages that ask some information from a web server. The web server returns data to the web browser, and JavaScript processes that data to selectively change parts of the webpage. The amount of data the server returns is usually much less than that sent when you ask for a full webpage.

The process of asking a server for information is technically called making a **REQUEST** to a server. And when the server sends back its answer, that’s called **RESPONSE**. The web is built upon browsers, also called **CLIENTS**, sending requests to the web servers, and servers sending responses back

AJAX has been around a long time, Microsoft first introduced it in 19999 with Internet Explorer 5. AJAX is the process of using JavaScript to send requests to a web server, and receive a response back, and then do something with that response. What you send to the web server with AJAX can be a simple request for a web page, a text file a search sent to a database, or a complete form full of information.

**A**  Asynchronous
**J**  JavaScript
**A**  And
**X**   XML or Extensible Markup Language

You can break the AJAX programming process into 4 steps:

1.  Create an XMLHTTPRequest Object. This step tells the browser to get ready. You want to send an AJAX request and the web browser needs to create an object that has all the methods you’ll need to send and receive data
2.  Define a callback function. This is the programming you want to run when the server returns its response. The callback is where you process the returned data and update the HTML on the page. 
3.  Open a request. In this step you give the browser two pieces of information, the method the browser will use to send the request, usually either get or post, and the URL where the request is sent
4. Send the request. The last step is finally sending the request. The previous three steps gave the web browser all the information it needs so we can finally send off the request to the web server.

[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)

#### A Simple AJAX Request
1.  Create an XMLHttpRequest object. For each AJAX request, you should creta a new XHR object. For example if you wanted to use AJAX twice on a page, to request data for a sidebar, and another to process a form submission.
    
2.  Create a callback function. This is the most complicated part of the AJAX process. The callback function is the programming you want the browser to run when the server sends back its response. For example in the case of Twitter’s endless list of tweets, the callback function adds the newly retrieved tweets to the end of the webpage. Think of a callback like a note you leave the browser “give me a call when you’re ready”. When the web browser send off its ajax request it continues doing other things. This is the ASYNCHRONOUS part of AJAX. There is another strange thing about the asynchronous nature of AJAX. If you make multiple AJAX request, you’ll never know which request will be handled first.

To trigger the callback , we use a special browser event. For example, when a user submits a form, you can check to see if they filled it out correctly. The event here is submitting the form. Checking the form data is a program that runs in reaction to the event. We can add programming to respond to those events. The most important is the `onreadystatechange` event. This event is triggered whenever there’s a change in an AJAX request. We create our callback to respond to that request
```javascript
var xhr = new XMLHttpRequest();

xhr.onreadystatechange = function(){
};
```
This programming sets up a function that runs each time there is a change in the state of the AJAX request. Each step in the AJAX process, like opening a new request or sending out that request triggers a change of state. For this call-back function we’re only interested in the final change of state. That’s when the server sends back its response. We want to get that response and then update our webpage. The XMLHttp request objects keeps track of the state using a special property named `readyState`. That property contains a number including the current state of the request and that property holds the number `4`, then the request is done and the server has sent back a response. Let’s add a conditional statement to test for that state. So here we’re checking if the `readyState` is equal to 4, that means we’ve got the response back. We take the full AJAX response and place it into the web page. The date we get back is going to be a chunk of HTML and we’ll place it inside a div tag that has the ID of AJAX. Every XMLHttp request object has a property called `responseText`. This is the information that the web server sends back.
```javascript
<script>

var xhr = new XHLHttpRequest();

xhr.onreadystatechange = function(){
	if (xhr.readyState === 4){
		document.getElementById('ajax').innerHTML = xhr.responseText;
	}
};
</script>
```
3. Open a request. An HXR object has a method or function called `open`. This function prepares the browser for sending the request. You give the function two pieces of information. The first is the HTTP method that you’re going to use, the most common are `GET` and `POST`, but there are others, such as `PUT` and `DELETE`.You’ll use GET if you want to send a request for data and POST if you’re sending the data. Like information from a form, for the server to save in the database, the URL is where the request is going. This could point to a file or a server-side program on your web server. In our example, this is pointing to a file in the project folder. We’ll load to file into the page. The open function just gets the browser ready to make a request and send that request.

4. Send the request. The previous three steps gave the web browser all the information it needs, so we can finally send off the request to the web server. In our case, since we’re request a chunk of HTML, we don’t provide the send method with any information, but when you need to submit information to the server like the users input from a web form. You can pass the send method that data
```javascript
<script>
var xhr = new XMLHttpRequest();

xhr.onreadystatechange = function() {
	if (xhr.readyState === 4){
		document.getElementById('ajax').innerHTML = xhr.responseText;
	}
};

xhr.open('GET', 'sidebar.html');
xhr.send();
</script>
```
But this is not very interactive therefore we’d add a button that will trigger AJAX and delete the button
```javascript
<script>
var xhr = new XMLHttpRequest();

xhr.onreadystatechange = function(){
	if (xhr.readyState === 4){
		document.getElementById('ajax').innerHTML = xhr.responseText;
	}
};

xhr.open('GET', 'sidebar.html');

function sendAJAX(){
	xhr.send();
	document.getElementById('load').style.display = "none";
}
</script>
```
#### MAC : Local PHP Dev Environment
Most developers prefer to build applications locally on their own computers rather than on a hosted server. Working locally allows you to work more quickly because you don’t have to wait for changes to be saved to a remote server and you don’t have to worry about issues like internet connectivity. Working with files locally also allows tighter integration with development tools, now while all these reasons are good, the most important reason for having a local development environment is you should never be working directly on a PRODUCTION SERVER, always test your code before it goes live.

#### GET and POST
There are two common methods for sending HTTP requests:

-   GET - Used for most requests. Browser uses the GET method whenever it requests a new web page, CSS file, image, and so on. Use GET when you want to "get" something from the server.
-   POST - Used frequently with web forms to send data to store in a database. Use POST when sending data that will store, delete or update information from a database.
   
For a server site program to send you customized information, like the map of your current location or photos from your flickr account, you need to send the server some information. You may have seen urls that look something like this:

[http://website.com/employees.php?lastName=Jones](http://website.com/employees.php?lastName=Jones)

The part after the question mark is called a `query string`. A query strings appear at the end of a URL and provides a way to send additional information that a web server can use to control the output of its response. Commonly, the data in a query string is used to search a database of information and return just a single record or a small subset of information.

A query string is made up of one or more name value pairs: Property and value.

There are some requirements for query strings, for example some characters like the ampersand, equal, space and quote marks have special meaning in a URL. So if you send information that includes those special characters you need to encode them. That is, translate them into a set of symbols that are safe and don’t conflict with their URL specific version.

For example:    &  %26

The **GET** method is a simple way to send data to a web server. However, there are some down sides to it.

1.  All of the data sent in the URL (including sensitive information) will appear in the computer’s browser history and show in the web server files, which is not the most secure solution
2.  There is only so much information you can put into an URL, for example IE can only handle URLs that are 2083 characters long
     
That’s why http offers another method called **POST**. The **POST** methods sends data differently than **GET**, whereas gets puts all its information in the url, the post method sends data separate from the IRL, in what’s called the **body of the request**. Not only is this more secure, it also lets you send more information to the server. The post method does require special encoding, just like get request. In addition, you need to set up a special header for the request. That’s an instruction, sent to the server, telling it what kind of data it should expect.

[https://www.mamp.info/en/](https://www.mamp.info/en/)
[https://whatismyipaddress.com/port](https://whatismyipaddress.com/port)
[https://documentation-4.mamp.info/en/MAMP-PRO-Mac/Settings/Hosts/General/](https://documentation-4.mamp.info/en/MAMP-PRO-Mac/Settings/Hosts/General/)
[http://www.url-encode-decode.com/](http://www.url-encode-decode.com/)
[https://developer.mozilla.org/en-US/docs/Web/HTTP#HTTP_request_methods](https://developer.mozilla.org/en-US/docs/Web/HTTP#HTTP_request_methods)

#### AJAX Response Formats
After you send an AJAX request, your callback function waits for a response. Web servers usually reply to AJAX request with a text response. This could be a simple message:
-   Ok
-   Message received
-   Error submitting the form.

But sometimes, you get a lot of information from the server. Perhaps 100 search results, 50 tweets, or a long list of company employees. For dealing with lots of data, it's a good idea to have a structured data format. By structured, I mean data that is ordered consistently, has identifiers that indicate what the data is, and is easy for JavaScript to analyze and use.

Two common data interchange formats are XML and JSON. **XML** stands for **extensive markup language**, which is very similar to HTML, and like HTML uses tags to structure data. For example, say you wanted to store a list of contact names and phone numbers, XML allows you to make your own tags to structure such information:
```xml
<contacts>
	<contact>
		<name>You</name>
		<phone>415-250-9999</telephone>
	</contact>
</contacts>
```
The benefit of a structured format like XML is that the data is clearly and consistently organized, making it easy for a computer to split the data up to usable chunks. The process of breaking a file up into easily accessed parts is called PARSING. XML is a very common format for exchanging data between computers. Most server-side languages handle XML easily. However, using XML data with JavaScript isn’t so easy it involves several steps, including analyzing or parsing the XML document, then going through each of its nodes to extract data from the tags. For many AJAX applications, there’s a better, more JavaScript-like data format called **JSON**

[Parsing_and_serializing_XML](https://developer.mozilla.org/en-US/docs/Web/Guide/Parsing_and_serializing_XML)
[jQuery.parseXML()/](http://api.jquery.com/jQuery.parseXML/)

#### AJAX Security Limitation
Web browsers prevent certain types of AJAX requests, such as requests to other websites. Learn the rules of a web browser "same-origin" policy and ways to work around these limitations

AJAX is normally limited by a web browser’s same origin policy, which controls how JavaScript can access content from a web server. In general, you can use AJAX to communicate from one page to another on the same web server but not to access other web servers. In other words, a webpage on your site can’t use AJAX to communicate with someone else’s bank. An a webpage on another site can’t use JavaScript to access content on your site.

For example, you can use AJAX to talk to a PHP file on that server, but you cannot request data from another website if it’s not from the same server, you cannot switch protocols, ports or hosts

This limitation shouldn’t cause you any trouble when you simply want to make your webpages more responsive and load new information from your own site. But if you want to add your tweets or photos from flickr all of those assets are in different domains than your own.

Fortunately, there are a few ways to circumvent the same origin policy. First you can create a **WEB PROXY**. Web servers aren’t limited by the same origin policy, so a web server can request data from servers at other domains. Because of this, you can set up a script in PHP, or using Ruby on Rails on your server, which ask for information from another web server. Then you can use AJAX to talk to the script on your site, which talks to the other site, and returns the data to your page. This makes sure the AJAX part stays within the same website, an abides by the same origin rule

**READ ABOUT CORS, JSONP MIGHT BE DEPRECATED**
Another common technique uses something called **JSONP**, which stands for JSON with Padding. It’s not traditional AJAX, it actually relies on the ability to link to JavaScript files across domains. Browsers actually do allow many types of cross domain links. For example, you can link to photos on other websites, you can link to CSS files, link jQuery through CDN. JSONP relies on this feature, instead of actually using AJAX to contact another web server, you load a JavaScript file from the other site. This is perfectly okay with a web browser. That JavaScript file contains the information you’re after. There are a few techniques for using JSONP. And as you’ll see, jQuery provides a really easy way to use JSONP

Finally, there’s a new method for making AJAX request across domains, is called CORS- Cross-Origin Resource Sharing. It’s a w3C recommendation and is already implemented in most current browsers. It does require some set up on the server part. But allows the server to accept requests from other domains. It even allows for more complex types of authentication that require the web browser to supply credentials before the web server will provide any information.

**There is one last AJAX limitation you need to keep in mind. Ajax doesn’t work unless you’re viewing your page through a web server**

[same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)
[CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

#### Programming AJAX
We'll be building a page element for a company's intranet. Using AJAX you'll display a list of employees who are in or out of the office.
-   Intranet - An intranet is an internal website that only the people that work for the company can see and use.

How AJAX Works
1.  Create an XMLHttpRequest object
2.  Create a call back function
3.  Open a request
4.  Send the request
Each of these steps, involves what’s called a ready state. When a browser reaches a new step in the process, the ready state of the request changes. In the last exercise we created a callback that responds to a change in that state. A callback function is also an event handler. The readyState property holds a number from 0 to 4. The number represents each state of the AJAX request. The numbers zero to three represent early stages in the AJAX process, from just after the XMLHttpRequest object is created, 0 all the way to when the response is coming, 3. In other words, the ready state change event fires off multiple times in the process of setting up and making an AJAX request, in our previous example we were interested only in state 4, but sometimes checking for a ready state of 4 isn't enough, there are things that might go wrong, such as:

-   Web server cannot connect to a database
-   Web program handling the request crashes
-   The AJAX request points to a URL that’s no longer around

If there are errors like these, the web browser won’t receive any useful information and we won’t be able to update our web page correctly. To handle possible errors, we can expand the conditional statement by adding the status property
```javascript
<script>
var xhr = new XMLHttpRequest();

xhr.onreadystatechange = function() {
	if (xhr.readyState === 4 && xhr.status === 200){
		document.getElementById('ajax').innerHTML = xhr.responseText;
	}
};

xhr.open('GET', 'sidebar.html');
xhr.send();
</script>
```
The status property is a number sent from the server, 200 means okay, and is the standard response for successful HTTP requests. Other numbers usually aren’t good. You can add additional statements, by adding status text.
```javascript
...
xhr.onreadystatechange = function() {
	if (xhr.readyState === 4 && xhr.status === 200){
		document.getElementById('ajax').innerHTML = xhr.responseText;
	} else {
		alert (xhr.statusText);
	}
};
...
```
So far we’ve just received a small chunk of HTML and placed it on the page, but HTML isn’t the most common data format for AJAX requests. More commonly we’ll receiving data in format like XML, which we looked at in the last stage, or JSON.

#### Introducing JSON
JSON, or JavaScript Object Notation is a simple data format that uses sets of key/value pairs to store information.

There are 2 different ways you can format JSON, using an array notation or object notation. And as you’ll see, it’s common to combine both

-   Array : [ “eggs”, 2, true, false, [1,2,3], “hello”]    
-   Object:  { “Name” : “Jim”,
				    “Phone” : “415-350-8160”
				}

The problem with arrays is that you don’t really know what the data means. A JavaScript Object is a set of key value pairs, also called property value pairs. The key is the name you can use to identify a property, and the value is the value you want to give that property. Because objects let you include property name, it’s really easy to identify the different parts of an object.

Correctly formatted JSON data must follow these rules:
-   Double quotes around the property and value data, single quotes won’t work. You can validate your file using a validator like JSON Lint   
-   A comma after the first value pair and after each object
```json
[
	{
		"title" : "My Way",
		"artist" : "Frank Sinatra"
	},
	{
		"title" : "Gimme No Majo",
		"artist" : "Masanori Takumi"
	},
	{
		"title" : "Vogue",
		"artist" : "Ayumi Hamasaki"
	}
]
```
You probably won’t ever need to worry about writing your own JSON by hand. It’s something that will be produced programmatically by the web server. Still, it’s a good idea to know how it works.

[https://jsonlint.com/](https://jsonlint.com/)

#### Parsing JSON Data
JSON is transmitted over the web as plain text. To make it useful for a JavaScript program, you need to parse it, or convert it from a string to JavaScript.

With AJAX the browser sends out a request to the web server and the web server sends a response. The response is just plain text, even though the server sends back information that looks like HTML, XML or JSON. To a web browser those responses are just a string of characters, in other words, even though JSON is formatted to look like JavaScript, it isn’t JavaScript, it’s a plain string, just a bunch of letters, numbers, and punctuation marks with no magical significance to your web browser.

In order to use JSON data, we need to take the string and convert it into JavaScript. This process is known as PARSING. Fortunately, it’s really easy to do. All current web browsers can do it using a single command.
```javascript
// Step 1. We start by creating an XML HTTP Request object. This new variable XR holds the XMLhttprequest object, which has its own set of properties and functions. Functions of an object are also called methods.
var xhr = new XMLHttpRequest();

// Step 2-Callback function. We start with the “readystatechange” event and we add our function, or callback, to it. Stage 4 let’s us make sure we’ve received all of the JSON data.
xhr.onreadystatechange = function(){
	if ( xhr.readyState === 4){
		console.log(xhr.responseText)
	}
};

//Step 3.Open a Request - In this case we're using the GET method to load a file with JSON data named employees.json stored in the data folder of the project. Now in a real world application, we'd point to a server side script that would dynamically generate this JSON data with the most current information on our employees
xhr.open('GET', 'data/employees.json');

//Step 4
xhr.send();
```
The information the web server returns is contained in a property named reponseText. It’s a property of our xmlhttprequest object, so we access it using .syntax

Using the JavaScript console, this would let us look what it seems like JSON file, but if you include the type of operator before, you will see that is a string:
```javascript
xhr.onreadystatechange = function(){
	if ( xhr.readyState === 4){
		console.log(typeof xhr.responseText)
	}
		
//XHR finished loading: GET
//string
```
We can’t access the bits and pieces of the data in a string like this. We need to turn this string into real JavaScript and here is how:
```javascript
var xhr = new XMLHttpRequest();

xhr.onreadystatechange = function(){
	if ( xhr.readyState === 4){
		var employees = JSON.parse(xhr.responseText);
	}
};

xhr.open('GET', 'data/employees.json');
xhr.send();
```
`JSON.parse` is a method that is built into all current web browsers, even back to IE8. This method takes a string and tries to convert it into a JavaScript object.

Remember that JSON formatted data must be an array of items or an object full of key value pairs or a combination of those two. In addition keys in JSON formatted objects must have double quotes. The JSON. parse method won’t work unless the string is formatted as correct JSON. I you try to parse a regular old string, like “this is a string” you’ll end up with a JavaScript error

When the JSON.parse method is complete, it returns a JavaScript object
[JSON.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)

#### Processing JSON Data
Now that we’ve converted our JSON data into usable JavaScript. It’s time to look at how we will output that information to our web page. At this point, we can put aside our programming skills and put on our web designer hats. We need to think about the HTML and CSS we’ll use to effectively present this list on our page. A simple way is to create an HTML and CSS mockup of your final design, the way the page will look after you’ve updated it’s content with JavaScript and AJAX.
```html
<!-- HTML MOCKUP -->
<div id=”employeeList”>
	<ul class=”bulleted”>
		<li class=”out”>Aimee</li>
		<li class=”out”>Amit</li>
		<li class=”in”> ETC </li>
	</ul>
</div>
```
To generate the HTML, we need to build one list item for each employee in the company. In other words, we want to take our JSON data and convert it into this HTML. To do this we’ll need to look at each employee in the list and do the following:
1.  Create a new HTML list item    
2.  Check the “in-office” property
3.  Get the vlue for the “name” property; insert it inside the <li> tag
4.  Close the <li> tag
```javascript
var xhr = new XMLHttpRequest();

xhr.onreadystatechange = function(){
	if ( xhr.readyState === 4){
		var employees = JSON.parse(xhr.responseText);
		var statusHTML = '<ul class ="bulleted">';
		
		for (var i=0; i<employees.length; i+=1){
			if (employees[i].inoffice === true ){
				statusHTML+= '<li class="in">';
			} else {
				statusHTML+= '<li class="out">';
			}
		statusHTML+= employees[i].name;
		statusHTML+='</li>';
		}
		
		statusHTML+= '</ul>';

		document.getElementById('employeeList').innerHTML = statusHTML;
	}
};

xhr.open('GET', 'data/employees.json');
xhr.send();
```
[Pseudo elements](https://teamtreehouse.com/library/pseudoelements-before-and-after)

### JQuery and AJAX
JQuery simplifies AJAX programming
Previos Example:
```javascript
<script>
var xhr = new XMLHttpRequest();

xhr.onreadystatechange = function () {
	if (xhr.readyState === 4) {
		document.getElementById('ajax').innerHTML = xhr.responseText;
	}

};

xhr.open('GET', 'sidebar.html');

function sendAJAX() {
	xhr.send();
	document.getElementById('load').style.display = 'none';
}
</script>
```
Same example using JQuery:
```javascript
<script
	src="http://code.jquery.com/jquery-3.3.1.min.js"
	integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
	crossorigin="anonymous">
</script>

<script>
	function sendAJAX() {
		$('#ajax').load('sidebar.html');
	}
</script>
```
[JQuery](https://jquery.com/)
[JQuery | .load()](https://api.jquery.com/load/)

STILL MISSING SOME INFORMATION FROM THE SOURCE DOC
 

## Asyncronous Programming with JavaScript <a name="asyncronous-js"></a>
### What is Asynchronous Programming?
#### Introduction to Asynchronous JavaScript

JavaScript is a synchronous single-threaded language, which means that it can process and execute only one task at a time. If there’s a major delay between the start and end of an operation and nothing else can run during that time, it’s going to create issues in your app, which negatively affect performance and the overall user experience.

Any time you have code that needs to execute after some period of time in response to an event, like a mouse click, or upon receiving the data it needs, you’re introducing asynchronous behavior into your program. JavaScript and its runtime environment prove efficient ways to handle async operations

#### Understanding Synchronous and Asynchronous Code
In a synchronous programming model, two or more things cannot happen at the same time. Only one thing is able to run to completion at any given time. Like waiting for water to boil, and each egg to cook one at a time, before making toast or coffee.

In an asynchronous model a block of code cans start to run, and even if that block of code is expected to finish what it needs to do at some point later, other code is able to run in the meantime. When the chunk of code is finally ready to complete what it needs to do, the program or the JavaScript engine for example, gets back to it and executes the task. That’s like making coffee and toast while your eggs cook and getting back to the eggs when the timer goes off.

Not letting one task block the completion of another task is how JS can seemingly do more than one thing at a time.

Examples of Synchronous and Asynchronous Code
* Runtime environment
*  setTimeout()

[MDN: Introducing Asynchronous JS](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing)
[while statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while)
[WindowOrWorkerGlobalScope.setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)
[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
[JSONPlaceholder - Fake Online REST API for Testing](https://jsonplaceholder.typicode.com/)
[Synchronous_and_Asynchronous_Requests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Synchronous_and_Asynchronous_Requests)
[Medium Blog Post: JS Runtime Environment](https://medium.com/@olinations/the-javascript-runtime-environment-d58fa2e60dd0)

#### The JavaScript Call Stack
JavaScript runtime (or host) environments like the browser and Node have a built-in interpreter that executes JavaScript code. It's called the JavaScript engine. The engine has a mechanism, called the **call stack**, for keeping track of the order of function calls and where it is in a program at any given moment.

For example, the call stack manages the current function that's being called, as well as any functions that are called from within that function, and other subsequent functions. The call stack itself can process only one function call at a time (it's single-threaded)

The call stack handles asynchronous tasks in a different way than synchronous tasks. Whenever the JavaScript environment encounters code that needs to run and execute at a later time, like a setTimeout() callback or a network request, that code is handed off to a special **Web API** that processes the async operation. Meanwhile, the call stack moves on to other tasks then revisits the async task when it's ready to be dealt with.

It's important to note that the asynchronous behavior of JavaScript does not come from the JavaScript engine itself. JavaScript engines like Chrome's V8, for instance, do not have asynchronous capabilities. Asynchronicity actually comes from the runtime environment. Runtime environments (like web browsers and Node) provide APIs that let JavaScript run tasks asynchronously.

[Call stack](https://developer.mozilla.org/en-US/docs/Glossary/Call_stack)
[Concurrency model and Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#Queue)
[JavaScript Debbuging Reference](https://developers.google.com/web/tools/chrome-devtools/javascript/reference#call-stack)
[Web APIs](https://developer.mozilla.org/en-US/docs/Web/API)

#### The Callback Queue and Event Loop
You learned that web APIs are what actually process async operations while keeping the call stack clear of blocking operations. When a web API is done processing an async task, it's not immediately executed on the call stack. Instead, its associated callback function gets pushed into something called the callback queue, which is a list (or line) containing all the async task callbacks waiting to be executed.

You can think of the callback queue as a holding area for all the callbacks that are waiting to be put on the call stack and eventually executed. Only callbacks for (non-blocking) operations that are scheduled to complete execution at a later time like `setTimeout()`, `setInterval()` and AJAX requests, for example, are added to the callback queue.

The web APIs add each async task to the callback queue where they wait to be pushed onto the call stack and executed one at a time. So where does the event loop come in, and why is it important?

The event loop has one important job: monitor the call stack and callback queue. Anytime the call stack is empty, the event loop takes the first task from the callback queue and pushes it onto the call stack, and runs it.
![Event Loop](https://felixgerschau.com/static/79486d91b22a7c1b4044fce88a4cae20/29007/js-event-loop-explained.png)

[call stack/event loop/callback queue visualisation](http://latentflip.com/loupe/?code=JC5vbignYnV0dG9uJywgJ2NsaWNrJywgZnVuY3Rpb24gb25DbGljaygpIHsKICAgIHNldFRpbWVvdXQoZnVuY3Rpb24gdGltZXIoKSB7CiAgICAgICAgY29uc29sZS5sb2coJ1lvdSBjbGlja2VkIHRoZSBidXR0b24hJyk7ICAgIAogICAgfSwgMjAwMCk7Cn0pOwoKY29uc29sZS5sb2coIkhpISIpOwoKc2V0VGltZW91dChmdW5jdGlvbiB0aW1lb3V0KCkgewogICAgY29uc29sZS5sb2coIkNsaWNrIHRoZSBidXR0b24hIik7Cn0sIDUwMDApOwoKY29uc29sZS5sb2coIldlbGNvbWUgdG8gbG91cGUuIik7!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D)

### Asynchronous JavaScript with Callbacks
Asynchronous code is typically structured in a different way than synchronous code. One of the most fundamental ways to structure async programs in JavaScript is with callback functions.

#### Introducing the Project
In this step, you'll learn and practice writing asynchronous JavaScript by building a simple API mashup, which is a site or app that’s created using two data sources, in this case the Open Notify API and the Wikipedia API. The app fetches and displays data about every astronaut who is currently in space.

A call back is a function that is passed to another function as an argument, and it only runs after its parent function has finished executing.

[OPEN APIs from Space](http://open-notify.org/)
[Wikipedia REST API](https://en.wikipedia.org/api/rest_v1/#/)

#### Callback Review
A callback function is a function passed into another function as an argument. The function that receives the callback function is often referred to as the "parent" function. The parent function will, at some point in the future, execute or call the callback.

```JavaScript
//Example 1
function  add(a,b, callback)  {
callback(a + b);
}

add(2, 4, function(sum)  {
console.log(sum);  // 6
});

//Example 2
function  getUserName(callback)  {
	const  name = prompt('What is your name?');
	callback(name);
}

function  greeting(name)  {
	alert('Hello, ' + name);
}

getUserName(greeting);  // a reference to the greeting function is passed to the function
```

**DOM Events**
Callbacks are used in both synchronous and asynchronous functions, so you might already be familiar with the concept of callbacks. For example, you use callbacks every time you listen for DOM events
```JavaScript
btn.addEventListener('click',  ()  =>  {
// Perform some action on click inside this callback
console.log('I was clicked!');
});
```
**Iteration Methods**
Array iteration methods like `map()`, `filter()`, and `forEach()` accept a callback function that processes each item in the original array. For example, convert each item in the fruits array to uppercase:
```JavaScript
const  capitalizedFruits = fruits.map(  fruit  =>  fruit.toUpperCase()  );
```

```JavaScript
//Returns a new array containing only those items in the sNames array that begins with the letter ‘S’
const  sNames = names.filter(  name  =>  {
return  name.charAt(0) === 'S';
});
```
**Continuation-passing style (CPS)**
With callbacks, you can also create a chain of function calls (or a sequence of tasks) where one task runs after another is completed. This is referred to as as continuation-passing style (CPS).

For example, each function takes a callback(or continuation function) as its last argument:

```JavaScript
function  add(x,  y,  callback)  {
  callback(x + y)
}

function  subtract(x,  y,  callback)  {
callback(x - y);
}

function  multiply(x,  y,  callback)  {
callback(x * y);
}

function  calculate(x,  callback)  {
callback(x);
}

calculate(5,  (n)  =>  {
  add(n,  10,  (n)  =>  {
    subtract(n,  2,  (n)  =>  {
	    multiply(n,  5,  (n)  =>  {
			console.log(n);  // 65
			});
		});
	});
});
```
The functions gets invoked and processed in a sequence. As you’ll soon learn, this kind of code lead to what’s referred to as **“callback hell”** or the **“pyramid of doom”**, which can make your program difficult to follow and maintain.

#### Async Programming and Callback Functions
Let's start by working with callbacks to fetch data. Fetching data is one of the most common ways you will write asynchronous programs in JavaScript.

```JavaScript
const astrosUrl = 'http://api.open-notify.org/astros.json';
const wikiUrl = 'https://en.wikipedia.org/api/rest_v1/page/summary/';
const peopleList = document.getElementById('people');
const btn = document.querySelector('button');

// Make an AJAX request
function getJSON(url) {
	const xhr = new XMLHttpRequest();
	xhr.open('GET', url);
	xhr.onload = () => {
		if(xhr.status === 200) {
			let data = JSON.parse(xhr.responseText);
			console.log(data);
			}
		};
	xhr.send();
}

// Generate the markup for each profile
function generateHTML(data) {
	const section = document.createElement('section');
	peopleList.appendChild(section);
	section.innerHTML = `
	<img src=${data.thumbnail.source}>
	<h2>${data.title}</h2>
	<p>${data.description}</p>
	<p>${data.extract}</p>
	`;
}

//Ajax request test
//getJSON(astosUrl);
btn.addEventLisnetner(‘click’, () => getJSON(astrosUrl));
```
#### Implement a Callback
Now that we’re successfully getting data asynchronously from the Open Notify API, let’s use it to make another AJAX call, this time to the Wikipedia API.

You’ve learned that a function can be passed to another function as an argument. To do that, we need to specify as a regular function parameter. So let’s have getJSON accept a function as it second argument. I’ll provide getJSON with a second parameter named CALLBACK. This represents a function that’s going to be passed into any JSON function call. It’s going to get callback and executed at a later time using the value returned by the AJAX call. It should be called as soon as the server sends back the response and it gets parsed to JSON.

```JavaScript
// Make an AJAX request
function getJSON(url, callback) {
	const xhr = new XMLHttpRequest();
	xhr.open('GET', url);
	xhr.onload = () => {
		if(xhr.status === 200) {
			let data = JSON.parse(xhr.responseText);
			return callback(data);
			}
		};
	xhr.send();
}
```
`getJSON` is now what’s called a **higher order function**. A higher order function takes one or more functions as arguments or returns a function as its result. It can also do both. In our case, `getJSON` is going to use the first argument, URL to make an AJAX request. If there is a valid response from the server, it's going to call the function that gets passed as the second argument, and provided it the return data in JSON format.
  
Now in our eventListener, let’s pass a callback to getJSON that will iterate over the return data and make a get request to the Wikipedia API for each person returned.

We’ll iterate over the returned people array (that you can see if you log the astrosUrl) using map. The map callback will take the parameter of person to represent each person object in the array. Inside this callback we’ll pass the Wikipedia EndPoint as the first argument, and we’ll concatenate the value of a person objects name property on each iteration. There are currently 6 people objects, so this should make six network requests.

```JavaScript
btn.addEventListener('click', () => {
	getJSON(astrosUrl, (json) => {
		json.people.map(person => {
			getJSON(wikiUrl + person.name);
		});
	});
});
```
Once the function returns the requested data will pass that data on to generate HTML function, so that it can create and append new DOM elements and display each astronaut on the page. Finally, let’s improve the UI by having the button disappear form the page once clicked

**Note**
I had a bit of a problem with my code, as a couple of the astronauts information wasn't showing giving me the following error:
`Uncaught TypeError: Cannot read property 'source' of undefined`
Because an image couldn't be found due to the fact that the endpoint directed to a disambiguation page, the solution that I found was to use a ternary operator to add the image to the page OR link to the wikipedia disambiguation page.

```JavaScript
function generateHTML(data) {
	const section = document.createElement('section');
	peopleList.appendChild(section); 
	// use the ternary operator 
	// to add the image to the page 
	// or a link to the Wikipedia disambiguation page
	section.innerHTML = ` ${data.type === 'standard' ? 
	`<img src=${data.thumbnail.source}>` : 
	`<a href=${data.content_urls.desktop.page}>Wikipedia disambiguation page</a>`} 
	<h2>${data.title}</h2> 
	<p>${data.description}</p> 
	<p>${data.extract}</p> `; }
```

#### Stepping through Async Code
  
Use the Chrome DevTools debugger to step through the code you've written and highlight the flow of code execution.

Stepping through code is when you execute code one line or function at a time to observe changes in the data and in the page, which helps you understand exactly what's happening in your program. It's also incredibly helpful for debugging code.

In the sources panel we'll set what's called a breakpoint, which is the spot in the code you want to pass execution of the program

Chrome Dev Tools >Sources Panel> Event Listener Breakpoints> Mouse> Click

Now we can click on the button on our page, and see that the program is paused on event listener button.click

The call stack panel here, represents the current call stack, which is keeping track of the order a function calls

[Debugging JS in the browser](https://teamtreehouse.com/library/debugging-javascript-in-the-browser)
[Event Listener breakpoints](https://developers.google.com/web/tools/chrome-devtools/javascript/breakpoints#event-listeners)
[View the current call stack](https://developers.google.com/web/tools/chrome-devtools/javascript/reference#call-stack)

#### Managing Nested Callbacks
We could have nested the entire program inside the `btn.addEventListener` and that would have created a *callback hell* 
Separating the code into functions with descriptive names does make the code easier to read. Still, having to manage all the different functions could make the program's flow hard to follow and could make it easier to introduce bugs. For instance, someone looking at this code for the first time might have to peruse through the details of each function, especially the callback sequence to figure out exactly what the program is trying to do.

In addition, callbacks along with the XML http request API can be a bit too complex to use and manage compared to the modern data fetching API tools and syntax JavaScript introduced in ES2015 and ES2017. 

### Understanding Promises
Promises in javaScript offer a more elegant and human-readable way to manage asynchronous code.

#### What is a Promise
A `Promise` represents the eventual completion of an asynchronous operation. Promises provide a straightforward alternative for composing and managing asynchronous code, without having to write too many callbacks, or spend extra time figuring out what the program should do

Following the previous analogy, let's say that instead of making breakfast yourself , you're in the mood to order breakfast and there a 2 ways to do this:

* **Order by phone and have it delivered**: In this scenario, you call your favorite place an order, provide your phone and address. The order taker says -I'll put your oder now and call you back when is ready and on its way.  At this point, you can go on and do other things while breakfast gets there, that's convenient. But you're also left waiting for a call back from the restaurant. You really don't have control over when they're going to call you. You receive nothing in exchange. Yo just want for them to call and deliver your food at around the time they said they would. In this scenario, you've handed control over whether or not you will have breakfast to the person taking your order. You expect it to happen, but maybe they wrote down the wrong phone number, and they can call back or they call, but your food never makes it to you. Perhaps they even deliver the wrong order. Now, most of these problems could be eventually rectified, but it's a messy process. A process which hands the control back to you when, and only when breakfast is delivered successfully. This is similar to working with callback functions. You're in some ways handing over control of your function to a callback expecting something else to be called and executed. Like callbacks, the process could be more susceptible to errors and harder to debug if something goes wrong.
* **Order at the Restaurant and Pick it up yourself**: In this scenario, yo go to the breakfast place, put in your order and pay for it. The cashier hands you something back in return, a receipt with an order number and a pager that buzzes to let you know that your order is ready. At that point, you may go off and do other things while you wait, like grab a coffee. You're still waiting for the pager to buss, but by  just having the pager in hand, you now have more control over whether or not you will have breakfast. The pager represents the promise that something is going to happen as a result of ordering breakfast. With that said, the promise is pending because you're waiting, so one of two things can happen.
	* The pager buzzes, your order is available to you.
	* The pager buzzes, to inform you that your food cannot be made and the reason why your order was rejected

A promise, like a pager, represents a value that can be handled at some point later, like picking up your order.
While a callback may leave us with some uncertainties about that value, a promise will promise or guarantee a future value and nothing can change it, regardless of whether or not it comes back fulfilled or rejected.

[Promises: An Introduction](https://developers.google.com/web/fundamentals/primers/promises)
[Master the JS Interview: Promises](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261)

#### Create a Promise
A promise is always going to be in one of three possible states:
* **Pending**: Is the like a waiting state. It's the default state of a promise
* **Fulfilled**: means that the operation was completed successfully
* **Rejected**: the operation failed

Working with promises is a three step sequence.
1. You create a promise instance using  the `Promise()` constructor
2. You then define what should happen when the promise is fulfilled or rejected.
3. Call one of the methods provided by the promise API to either consume the value of a fulfilled promise, or provide a rejection reason for a rejected promise.

We'll create a new Promise called breakfast promise. The breakfast constructor takes one argument, a callback with two parameters: **resolve** when the promise is fulfilled, and **reject** for when it's rejected. Within the callback, we'll write an async task using the `setTimeout()` method. I'll pass it a callback and set a delay value of 3000 milliseconds, or 3 seconds.

```JavaScript
const breakfastPromise = new Promise((resolve, reject)=>{
  setTimeout(()=>{
  }, 3000);
});  
```
 Our promise constructor is all set up. This function is going to return a promise object that is either pending, resolved or rejected. For example if we `console.log(breakfastPromise)` then in the terminal. Notice how the console outputs a promise object, which is currently pending.

```
node promises-breakfast.js
Promise{<pending>}
```
Now inside the constructor, we can either call resolve to return a promise objects that is resolved with a given value, or reject to return a promise object that is rejected with a given reason. Both of these functions are provided by the constructor. So first, inside setTimeout, we'll call resolve to change the status of the promise. We can pass resolve a value which becomes the fulfillment value of the promise. So when the asynchronous task completes successfully, it's going to return a resolved promise object. To get the value out of the promise object, or consume the promise, we use one of the methods from the Promise API. The two we'll most like use are `then()` and `catch()` 

`then()` can be called to handle both fulfilled and rejected promises. It accepts two functions as its arguments, one for fulfilled promises, and an optional one for rejected promises. In this case, we'll call it to handle fulfilled promises, and later use the `catch()` method to handle rejected promises.

So to get the resolve value (`'Your oder is ready..'`). We'll pass `then()`an arrow function that takes the fulfillment value as a parameter, we'll name it `val` and logs it to the console.

```JavaScript
const breakfastPromise = new Promise((resolve, reject)=>{
  setTimeout(()=>{
  resolve('Your order is ready. Come and get it!');
  }, 3000);
});

console.log(breakfastPromise);
breakfastPromise.then(val => console.log(val));  
```

[Using_promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
[Promise.resolve( )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve)
[Promise.reject( )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject)
[Promise.prototype.then( )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)


#### Reject a Promise and Handle Errors
If an error occurs, the Promise status changes from pending to a rejected, or  failed state. The good thing is that promises give you the opportunity to handle the error with the `catch()` method. Then we can chain it with the `then()` method. The function passed to catch takes one argument, which is the rejection reason, or the error message to display. We'll pass `catch()` an arrow function that takes the parameter, `err`, and logs it to the console. 


```JavaScript
const breakfastPromise = new Promise((resolve, reject)=>{
  setTimeout(()=>{
  reject('Oh no! There was a problem with your order');
  }, 3000);
});

console.log(breakfastPromise);
breakfastPromise.then(val => console.log(val)).catch(err => console.log(err));  
```

Keep in mind that if you don't specify reject and a catch method, the promise will fail silently. Errors will be swallowed up with no side effects to the rest of your app. Now we can pass an `if statement` to handle both scenarios. Notice how on the reject method we are  passing an `Error` object instead of only a string. While is not required, it does help with debugging because it will display the stack trace alongside the rejection reason.

To test this, we'll initialize a variable named order to true.

```JavaScript
const order = true;

const breakfastPromise = new Promise((resolve, reject)=>{
  setTimeout(()=> {
  if (order) {
	  resolve('Your oder is ready.Come and get it!');
	  } else {
	  reject(Error('Oh no! There was a problem with your order'));
	  }
  }, 3000);
});

console.log(breakfastPromise);
breakfastPromise.then(val => console.log(val)).catch(err => console.log(err));  
```

Also to make you're code mode readable, we can place each catch call on a separate line like this

```JavaScript
breakfastPromise
	.then(val => console.log(val))
	.catch(err => console.log(err)); 

```

#### Promises Review
* A promise is a regular JavaScript objects that changes from a pending state to either a fulfilled or rejected state.
* You're able to call methods on the `Promise` object, like `then()` and `catch()`
* When the status of a promise changes to *resolved*, the functions passed to `then()` gets called
* When the status chnages to *rejected*, the function passed to `catch()` is invoked 
* It's best to specify a rejection reason and call `catch()` on a promise -if you don't, the promise will silently fail.

**Named Functions**
You're also not restricted to using anonymos functions within the method call of `then()` or `catch()`. You can pass then and catch references named functions.

For example, create two functions: `onResolve ` and `onReject` each logs a message to the console
```JavaScript
function onResolve() {
  console.log(`Your order is ready. Come and get it!`);
  }
function onReject(){
	console.log(Error('Oh noes! There was a problem with your order.'));
}
```
In the `Promise` constructor, call `resolve()` if order is `true`, and `reject()` if it's `false`:

```JavaScript
const breakfastPromise = new Promise((resolve, reject) => {
	setTimeout(() =>{
		if(order){
			resolve();
		} else {
		  reject();	
		}
	}, 3000);
});
```

### From Callbacks to Promises
Remember, a `promise` is the eventual value or result of an asynchronous operation.Looking at our program, which part of it is set to execute at some point later once it has the data it needs. 

In the function `getJSON` the callback function assigned to onload (`xhr.onload`) is invoked once data is returned from the API, so we can convert this to a promise.
```JavaScript
function  getJSON(url, callback) {
const  xhr  =  new  XMLHttpRequest();
xhr.open('GET', url);
xhr.onload  = () => {
	if(xhr.status  ===  200) {
		let  data  = JSON.parse(xhr.responseText);
		return  callback(data);		
		}
	};
xhr.send();
}
```
First, We'll set `getJSON` to return a promise using the Promise constructor. We'll pass the constructor a callback with the parameters `resolve` and `reject`, and place the body of `getJSON` within the promise constructor callback.

Next, when the API data loads, if the status of the response is 200, we'll parse that data to JSON and instead of invoking a callback, we're going to call `resolve` and pass it the variable `data`, which will change the status of the promise from pending to fulfilled, else if the status code is something other than 200, we'll reject the promise by calling `reject` and we'll use again the `Error` constructor to display the stack trace. Now we can delete the `callback` parameter from the getJSON function signature, since i no longer requires a callback function passed to it.

Now if at some point there's a network connectivity issue, a status code wouldn't be provided, so we'll also use the `onerror` event handler on the xhr object to reject the promise if the http Request fails due to connectivity issues.

```JavaScript
function  getJSON(url) {
	return  new  Promise((resolve, reject) => {
	const  xhr  =  new  XMLHttpRequest();
	xhr.open('GET', url);
	xhr.onload  = () => {
		if(xhr.status  ===  200) {
			let  data  =  JSON.parse(xhr.responseText);
			resolve(data);
		} else {
			reject(Error(xhr.statusText));
			}
		};
		xhr.onerror  = () =>  reject (Error('A newtwork error occurred')
		xhr.send();
});
```
`getJson` is now all set to return a promise object. Next, in the event listener we no longer need to provide `getProfiles` as a callback, instead we can call `then()` on the `getJSON` promise and pass it a reference to `getProfiles`. Promises get executed in sequence. Each `then()` method that is chained on to the main promise, returns a promise of its own and each gets executed sequentially, once the previous promise is fulfilled. In other words, something happens after something else is resolved

```JavaScript
btn.addEventListener('click', (event) => {
	getJSON(astrosUrl)
		.then(getProfiles)
		.then(data  =>  console.log(data))
		.catch(err  =>  console.log (err))
		
event.target.remove();
});
```

Also, we need to make a few changes in the getProfiles function. First, we'll omit the callback passed to `getJSON`, then specify the return keyword, since we're now returning a promise object during each iteration of map and we'll capture the result of map in a variable named `profiles`, then have the function return `profiles`

```JavaScript
function  getProfiles(json) {
	const  profiles  =  json.people.map( person  => {
		return  getJSON(wikiUrl  +  person.name);
		});
	return  profiles;
}
```
So instead of 6 separate promise objects, we need getProfiles to return a single resolved promise when all the promises from the `.map()` function have resolved

[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
[Chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises#Chaining)

### Handle multiple promises with Promise.all
JavaScript promises provide an efficient way to fire off and keep track of multiple asynchronous operations with the `Promise.all` method. `Promise.all` is useful when your program needs to wait for more than one promise to resolve.

We're getting an array of multiple resolved promise objects back from the `getProfiles` function. What we need is a single resolve promise we can pass to generate HTML. JS promises provide an efficient way to fire off and keep track of multiple asynchronous operations with the `Promise.all` method.  This method is useful when your program needs to wait for more than one promise to resolve.

```JavaScript
function  getProfiles(json) {
	const  profiles  =  json.people.map( person  => {
		return  getJSON(wikiUrl  +  person.name);
		});
	return  Promise.all(profiles);
}
```
Now that we're getting the JSON data back from wikipedia, let's replace the in-line error function in the second `.then()` method, to generate HTML, but since generateHTML now receives an array of objects as datam we need to make a change to the function. The function now needs to iterate over the array of objects and create HTML for each object in the array, for this we'll use the `.map()` array iteration method, and in the map callback, we'll use the parameter `person` to represent each person object

```JavaScript
function  generateHTML(data) {
	data.map( person  => {
		const  section  =  document.createElement('section');
		peopleList.appendChild(section);
		section.innerHTML  =  `
			${person.type === 'standard' ?
			`<img src=${person.thumbnail.source}>` :
			`<a href=${person.content_urls.desktop.page}>Wikipedia disambiguation page</a>`
				}
			<h2>${person.title}</h2>
			<p>${person.description}</p>
			<p>${person.extract}</p>
			`;
	})
}
```
Keep in mind that `.Promise.all` is an all or nothing operation, that means that it's going to reject as soon as any of the promises passed to it fail. So either of all of the promises succeed or none does.

[Promise.all](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

```JavaScript
//Another Example of Promise.all
const func1 = getJSON('...'); const func2 = getJSON('...');   
Promise.all([func1, func2])
 .then(results => { console.log('Array of results', results); 
 }) 
 .catch(error => { console.error(error); 
 })
```

### Perform cleanup with finally( )
The `finally()` method is a new addition to promises. It gets called once a promise is fully settled, regardless of whether it's fulfilled or rejected. Finally is useful when you need to do some clean up after the promise sequence finished. 

The finally method in this case removes the button from the page after the data is fetched and process, regardless of whether or not that operation succeeded. Because of that, if an error occurs we can use catch to display a user-friendly message to let them know something went wrong

```JavaScript
btn.addEventListener('click', (event) => {
	event.target.textContent  =  "Loading..."
	getJSON(astrosUrl)
		.then(getProfiles)
		.then(generateHTML)
		.catch(err  =>{ 
			peopleList.innerHTML  ='<h3>Something went wrong!</h3>';
console.log (err)
				})
		.finally(()=>  event.target.remove())
});
```

Promises offer a more intuitive flow, whereas callback nesting request to jump around to comprehend the code's flow, promises let you chain methods to achieve sequential tasks providing a more linear reading experience.

[Promise.prototype.finally( )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/finally)

#### Using Fetch
Learn a new, easier way to make network requests with the Fetch API. 
ES2015 introduced a more elegant and friendlier data fetching interface that's native to the browser called the `fetch API` Fetch uses JavaScript promises to let you handle the results returned from the server.

To make a fetch request, you use the global fetch method. Fetch takes one mandatory argument, the path to the resource you want to fetch. 

In our project, we can use `.fetch()` to replace or whole getJSON function. The fetch method itself returns a promise, and once fetch makes a request and the data finishes loading the fetch promise is fulfilled, it's also going to return a response object containing information  about the response like the status code and the corresponding status message. In order to access and use the data, we need to parse it to JSON first, and we'll do this using an arrow function.
```JavaScript
btn.addEventListener('click', (event) => {
	event.target.textContent  =  "Loading..."
	fetch(astrosUrl)
		.then(response => response.json())
		.then(getProfiles)
		.then(generateHTML)
		.catch(err  =>{ 
			peopleList.innerHTML  ='<h3>Something went wrong!</h3>';
console.log (err)
				})
		.finally(()=>  event.target.remove())
});
```

It's usually best to handle error and fetch request or any promise sequence as high up in the chain as possible. For example, we can handle an error in the Wikipedia fetch separately by chaining a catch.

```JavaScript
function  getProfiles(json) {
	const  profiles  =  json.people.map( person  => {
	const  craft  =  person.craft;
	return  fetch(wikiUrl  +  person.name)
		.then(response  =>  response.json())
		.then(profile  => {
			return {...profile, craft }
		})
		.catch(err  =>  console.log('Error fetching Wiki',err))
});
return  Promise.all(profiles);
}
```

And finally, we'll display another piece of data to the user, which is the spacecraft each astronaut is on, which is almost always the ISS (International Space Station)

While promises seem like a clear improvement over callbacks, mainly because they increase the readability of async code. They still do not entirely get rid of callback functions in your program, and that's okay because your code will likely use callbacks in some way, it's the deep nesting that could cause problems. In addition, your promise based program may require lots of then methods, with anonymous functions or function references to handle each different task. That can make your code somewhat confusing and there's a chance that you still may end up writing code that resembles the pyramid of doom style structure.

[Fetch_API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
[Body.json()](https://developer.mozilla.org/en-US/docs/Web/API/Body/json)
[Spread_syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)


#### Exploring Async/Await
The keywords `async` and `await`, together, provide a special syntax that makes working with promise-based code easier and more intuitive –– you write asynchronous code that looks more like synchronous code. In this stage, you'll learn how to combine async/await with traditional promises, and common ways to handle exceptions when working with async/await.

#### What is Async/ Await?
JavaScript continues to provide new and improved ways to do the exact same thing. So far we've experienced the progression of asynchronous code from callbacks, to promises and fetch. ES2017 introduced async/wait to further simplify how you work with promises.

Async/await and promises are fundamentally the same under the hood. It all happens with two special keywords `async` and `await`.

The function below for example is going to make a fetch request. Inside we'll use the `await` keyword to wait for a promise. The fetch method for example, returns a promise by placing await in front of fetch, the function is awaiting a resolved promise returned by fetch. Once resolved, the fulfilled value, which is the response object, is assigned to the variable response. The next step is to parse the response to json. This task is also asynchronous and returns a promise.

```Javascript
async function fetchData(url){
	const response = await fetch(url);
	const data = await response.json();
	return data;	
}
```

**await**
* Pauses the execution of an async function and waits for the resolution of a promise
* Resumes execution and returns the resolved value
* Pausing execution is not going to cause blocking behavior. The JS engine can run and execute other tasks in the meantime via the event loop.
* Valid only inside functions marked async

Also is important to remember that **An async function always returns a promise. That promise resolves with the value returned by the async function, or rejects with an error thrown from within the function**

[async_function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
[await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await)

#### Convert Promise Handling to Async / Await
In the previous section we're calling fetch in the `EventLisneter` to kick off an AJAX request, then following a sequence of then methods to manage and distribute the returned data to other functions like getProfiles. So what we're going to do now is write one async function that will handle each of this tasks, then we'll call the function in the EventListener passing it the URL to fetch

We'll declare an async function named `getPeopleInSpace`. This function is going to first make a fetch request to the open notify API, then use those results to make fetch requests to the Wikipedia API. Remember the `async` keyword is used for the function declaration and takes the parameter URL for the url to fetch. In the body of the function we'll start by making the first network request using the fetch method to the Open Notify API, we'll capture this in a variable `peopleResponse`, then we'll paste the response from fetch to JSON capture in the variable `peopleJSON`

Then, we'll make the next set of network requests. This is where we'll map over the array of objects stored in peopleJSON and fetch data from wikipedia API based on the returned names of people in space.

Finally, we'll use `Promise.all` to wait on all of those individual promises, join them in a single promise that gets resolved when all are fulfilled.

```JavaScript
async  function  getPeopleInSpace(url){
	const  peopleResponse  =  await  fetch(url);
	const  peopleJSON  =  await  peopleResponse.json();
	
	const  profiles  =  peopleJSON.people.map(async (person) => {
		const  craft  =  person.craft;
		const  profileResponse  =  await  fetch(wikiUrl  +  person.name);
		const  profileJSON  =  await  profileResponse.json();
	
	return {...profileJSON, craft};
	});
	
return  Promise.all(profiles);
}
```
So now, in the event listener, there are a couple of ways to approach calling the `getPeopleInSpace` function and passing the returned promise to the `generateHTML` function. We could use async/await or chained promises. For example, we'll use async/await by declaring a variable named astros for that will store the results of  `getPeopleInSpace`, passing it the open notify API end point stored in the variable astrosUrl, since this returns a promise, we'll include the `await` keyword. Now we can invoke `generateHTML` and pass it the value of astros.

```JavaScript
btn.addEventListener('click', async (event) => {
	event.target.textContent  =  "Loading...";
	const  astros  =  await  getPeopleInSpace(astrosUrl);
	generateHTML(astros);
	event.target.remove();
});
```
[Body.json( )](https://developer.mozilla.org/en-US/docs/Web/API/Body/json)
[Spread_syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

Examples of async/await patterns

```JavaScript
// Anonymous async function 
const getData = (async function() {
	const response = await fetch('...');
})();

// Async function assignment 
const getData = async function() {
	const response = await fetch('...');
};   

// Arrow functions 
const getData = async () => {
	const response = await fetch('...');
};

// Async Function as an argument 
btn.addEventListener('click', async () => {
 const response = await fetch('...');
});
```

#### Combine Async / Await with Promises
Async/await is not meant to replace promises -- it's actually syntactic sugar (**syntax** within a programming language that is designed to make things easier to read or to express) for creating functions that return and wait for promises. In this video, you'll learn how to use a combination of promises and async/await to produce code that's more readable.

We have learned how async-await simplifies the process of working with promises. We're able to write asynchronous code in a way that resembles synchronous code, which in some ways might enhance the readability and flow of code.

An async is just a function that returns a promise, whether you use `await` or not. So, now we'll use a combination of async-await to produce code that might be a little more readable.

####  Error Handling with try...catch
Currently our async/await function and promise sequence doesn't handle exceptions and rejected promises, so it's best to call the `.catch` method. We could catch them in our fetch calls
```javascript
...
  const peopleResponse = await fetch(url).catch(e => console.log('Error fetching data'));
```
But this can get messy; instead we're going to catch all exceptions in one place by writing a separate async functions that handles the fetching and parsing of data, and since it would look like synchronous code, we can use a try/catch statement
```javascript
async function getJSON(url){
  try{
    const response = await fetch(url;)
	    return await response.json();
  } catch (error){
		throw error;
  }  
}

//With the previous function we can refactor 
// our getPeopleInSpace function
async function getPeopleInSpace(url){
  const peopleJSON = await getJSON(url);
  const profiles = peopleJSON.people.map(async (person) =>{
	const craft = person.craft;
	const profileJSON = await getJSON(wikiUrl + person.name);
    return { ...profileJSON, craft};
	});
	return Promise.all(profiles)
;}
```
Finally, to handle any other errors which may occur in our async code and display an user friendly message, we'll once again chain a `.catch()` method on the promise returned, just above the `.finally()` method
```javascript
...
...
getPeopleInSpace(astrosUrl)
	.then(generateHTML)
	.catch(e =>{
		peopleList.innerHTML ='<h3>Something went wrong!</h3>';
		console.error(e);
		})
	.finally() => event.target.remove()
...
```
[try...catch – MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)
[return  `await promiseValue`  vs.  `return promiseValue`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function#return_await_promiseValue_vs._return_promiseValue)
[`throw`  – MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw)
[`console.error()`  – MDN](https://developer.mozilla.org/en-US/docs/Web/API/Console/error)


## Working with the Fetch API <a name="fetch"></a>
### What is the Fetch API
Learn an easier way to make network requests and handle responses with the Fetch API(Application Programming Interface). Fetch provides a modern, friendly data-fetching interface that's native to the browser.

Most website applications retrieve and send information to and from a remote server using JavaScript. For example, make a request to an API and use the return data to update the contents of a page. Or post data submitted by a forum to a server.

* AJAX provides a combination of technologies that give developers a way to send and received data asynchronously, in the background. Without reloading the page, which makes your app feel fast and responsive, but the XHR object can be a little too complex to write, read and remember. 
* You can also use JQuery that provides a wrapper around the XHR object
* Or we can use **Fetch**

*Advantages of Fetch API*
* Easy to use and understand
* Completely promised-based
* Cleaner, simpler code compared to XHR
* Built into the browser, not having to load an external library to simplify how yoy make async request

*Since IE doesn't support Fetch you can use Github polyfill to still use it*

[Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
[Using_Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
[Using_promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
[Fetch Polyfill](https://github.com/github/fetch)

### Write a Basic Fetch Request
Let's get started by writing a basic fetch request using the global `fetch()` method. Then we'll use JavaScript promises to handle the results returned from the server.

Fetch API provides an easier way to make network requests in the browser and handle responses

 ```JavaScript
 fecth('myapi.com/endpoint')
 ```

Testing getting a response from an endpoint.  With this, fetch returns a response object containing information about the response, like the status code and the corresponding status message. 
 
 ```JavaScript
 const  select  =  document.getElementById('breeds');
const  card  =  document.querySelector('.card');
const  form  =  document.querySelector('form');
  
// ------------------------------------------
// FETCH FUNCTIONS
// ------------------------------------------
fetch('https://dog.ceo/api/breeds/image/random')
	.then(response  =>  console.log(response))
 ```

The actual data we want is in the body property of the response object. Since the API we're using returns data in JSON, we need to parse it to JSON.

 ```JavaScript

// ------------------------------------------
// FETCH FUNCTIONS
// ------------------------------------------
fetch('https://dog.ceo/api/breeds/image/random')
	.then(response  =>  response.json())
	.then(data  =>  console.log(data))
 ```

So, `response.json()` reads the response and returns a promise that resolves to json, and because we're using a single line arrow function, the promise returned form the response.json method call will be implicitly returned from our arrow function, and this allows us to chain another `.then()` method onto our existing one. Inside this method we'll pass a function that takes the json data via a parameter we'll call `data` and log it to the console for now.

This will show us the JSON data. In the JSON object there's a property name "message" and the value is the URL to an image. So to access the value of message, we'll log `data.message` . Which is exactly what we need, the URL as a string.

Keep in mind that by default, fetch won't send or receive any cookies from the server, and this will affect you dealing with the user authentication. So the fetch method also accepts an optional second parameter, an init options object you can use to customize the HTTP request. So for example you can send a request with credentials included, or make a post request instead if the default get request


[Dog API](https://dog.ceo/dog-api/)
[Using_Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
[then()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
[Response Methods](https://developer.mozilla.org/en-US/docs/Web/API/Response#Methods)
[Sending_a_request_with_credentials_included](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#Sending_a_request_with_credentials_included)
[Sending Cookies with fetch()](https://github.com/github/fetch#sending-cookies)

### Displaying the Content
In this video, we'll display the image on the page, and fetch the list of breeds to display the `<select>` menu options.

We'll create a couple of helper function to display our image using the second `.then()` method call. These separate functions keep the code cleaner and modular.

```JavaScript
// ------------------------------------------
// FETCH FUNCTIONS
// ------------------------------------------

fetch('https://dog.ceo/api/breeds/image/random')
	//.then(response => console.log(response))
	.then(response  =>  response.json())
	.then(data  =>  generateImage(data.message))

// ------------------------------------------
// HELPER FUNCTIONS
// ------------------------------------------
function  generateImage(data){
	const  html  =  `
		<img src='${data}' alt>
		<p>Click to view images of ${select.value}s</p>
		`;
	card.innerHTML  =  html;
}
```

Next, we'd like to use the `breeds/list` endpoint to return a list of all the master breeds inside the select menu.

```JavaScript
// ------------------------------------------
// FETCH FUNCTIONS
// ------------------------------------------
fetch('https://dog.ceo/api/breeds/list')
	.then(response  =>  response.json())
	.then(data  =>  generateOptions(data.message))

fetch('https://dog.ceo/api/breeds/image/random')
	//.then(response => console.log(response))
	.then(response  =>  response.json())
	.then(data  =>  generateImage(data.message))

// ------------------------------------------
// HELPER FUNCTIONS
// ------------------------------------------
function  generateOptions(data){
	const  options  =  data.map(item  =>  `
		<option value='${item}'>${item}</option>
		`);
select.innerHTML  =  options;
}

function  generateImage(data){
	const  html  =  `
		<img src='${data}' alt>
		<p>Click to view images of ${select.value}s</p>
		`;
	card.innerHTML  =  html;
}
```
The map function returns an array with all the option elements separated with a comma, and those commas also get inserted into the markup. As you can inspect the HTML using DevTools. So to remove the commas, we'll call join() on map() passing it a set of quotes to remove them, like so:

```JavaScript
function  generateOptions(data){
	const  options  =  data.map(item  =>  `
		<option value='${item}'>${item}</option>
		`).join('');
select.innerHTML  =  options;
}
```
We'll later connect the menu option to the image displayed.

Resources
[map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
[innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)
[join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

### Create a Reusable Fetch Function
Learn how to simplify your fetch requests by creating a reusable data-fetching function that runs the fetch, returns the response in JSON, and more.

This is a wrapper function around `fetch()`  and we'll chain a `.then()` method that parses to JSON. 

```JavaScript
// ------------------------------------------
// FETCH FUNCTIONS
// ------------------------------------------
function  fetchData(url){
	return  fetch(url)
		.then(res  =>  res.json())
}
```
After this, we'll create another helper function that will connect the select menu to pick a breed and display photos only of that breed using event listeners

```JavaScript
function  fetchData(url){
	.then(checkStatus)
	.then(res  =>  res.json())
	.catch(error  =>  console.log('Looks like there was a problem', error))
}

// ------------------------------------------
// EVENT LISTENERS
// ------------------------------------------
select.addEventListener('change', fetchBreedImage);
card.addEventListener('click', fetchBreedImage);
```

### Handling Errors
What would happen if a fetch gets rejected or returns in a failed state? To handle these types of errors, you use the `.catch()` method, which deals with rejected cases only.

```JavaScript
// ------------------------------------------
// FETCH FUNCTIONS
// ------------------------------------------
function  fetchData(url){
	return  fetch(url)
		.then(checkStatus)
		.then(res  =>  res.json())
		.catch(error  =>  console.log('Looks like there was a problem', error))

// ------------------------------------------
// HELPER FUNCTIONS
// ------------------------------------------
function  checkStatus(response){
	if(response.ok){
		return  Promise.resolve(response);
	} else {
		return  Promise.reject(new  Error(response.statusText));
	}
}
```

[.catch()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
[Promise.resolve()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve)
[Promise.reject()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject)
[handling-http-error-statuses](https://github.com/github/fetch#handling-http-error-statuses)

### Manage Multiple Request with Promise.all
JavaScript promises provide an easier, more efficient way to fire off and keep track of multiple async operations at the same time with `Promise.all`. `Promise.all` joins two or more promises and returns only when all the specified promises have completed or been rejected.

```JavaScript
Promise.all([
	fetchData('https://dog.ceo/api/breeds/list'),
	fetchData('https://dog.ceo/api/breeds/image/random')
	])
.then(data  => {
	const  breedList  =  data[0].message;
	const  randomImage  =  data[1].message;	
	
	generateOptions(breedList);
	generateImage(randomImage);
})
```
*REMEMBER that there are no hard and fast rules about when or how to use Promise.all. How you use it is specific to your situation*

### Posting Data with Fetch
The default HTTP method for making fetch requests is `GET`, which retrieves data from a server. You can make requests other than `GET` (like `POST`, `DELETE` and `PUT`) by passing additional information to `fetch()`.

Now, we'll create a function that uses fetch to post the name and comment form data to a server on submit

We'll create function named `postData` which takes the parameter `e`, for the event. Inside the function we'll first cancel the browser's default behavior,  with `e.proventDefault`. Then we'll assign the value of the name input field and the comment `textarea` to the constant name and comment. 

We're going to submit the contents of the form to the JSONPlaceholder API. This is a Fake Online REST API for testing and prototyping. We're going to use the comment endpoint. Which, if you click on it, you can see it contains 500 fake comments, and when you post to this endpoint JSONPlaceholder API sends you this submitted data back with an id attached

The fetch method accepts a second parameter, a configuration object that lets you control a number of different settings you can apply to the request like choosing a different HTTP method. So in our fetch method after the urL, we'll pass an object, and in that object add 3 properties
 
```JavaScript
form.addEventListener('submit', postData); 

// ------------------------------------------
// POST DATA
// ------------------------------------------
function  postData(e){
	e.preventDefault();
	const  name  =  document.getElementById('name').value;
	const  comment  =  document.getElementById('comment').value;

	fetch('https://jsonplaceholder.typicode.com/comments', {
		method:  'POST',
		headers: {
			'Content-Type':  'application/json'
			},
		body:  JSON.stringify({name, comment}),
	})
	.then(checkStatus)
	.then(res  =>  res.json())
	.then(data  =>  console.log(data))
}
```
In ES2015 there is a shorthand notation you can use in an object whenever a key and a value are the same. 
Also to make things easy to manage and read, we can write the config object separately

```JavaScript
function  postData(e){
	e.preventDefault();
	const  name  =  document.getElementById('name').value;
	const  comment  =  document.getElementById('comment').value;
  
  const config = {
     	method:  'POST',
		headers: {
				'Content-Type':  'application/json'
			},
		body:  JSON.stringify({name:  name, comment:  comment}),
		}

	fetch('https://jsonplaceholder.typicode.com/comments', config)
	.then(checkStatus)
	.then(res  =>  res.json())
	.then(data  =>  console.log(data))
}
```
[JSON Placeholder](https://jsonplaceholder.typicode.com/)
[HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

## Object Oriented JS <a name="ooj"></a>
### Intro
#### What is an Object, and why do we care?
An object is a net and tidy package of information about something you want to use in your code. This package contains a group of properties and functions that work together to represent something in your program.

-   **Objects’ properties**: a series of key value pairs that hold information about the object    
-   **Objects’ methods**:  its functions. Methods let your object do something or let something be done to it.

The term object oriented programming is really just describing a programming paradigm. Or a way of thinking about in designing computer program that uses objects as its core.
A lot of developers find it helpful to think of objects in a code as a way to model real life objects. Real like objects have states and behaviors and so the javaScript objects. In JavaScript states are represented by the objects properties and behaviors are represented by the objects methods. For example we can make a radio object with properties like station and volume and methods like turn off or change station.

The idea of mimicking or modeling real life objects is pretty good way to try to think about objects when we’re first learning about them. But more often, our objects are a little more abstract or less analogous to things we might use in everyday life. Most of the time when we design objects we are creating an easy way to store information about something via properties. And access, manipulate or utilize that information via methods. These objects are more like data containers than abstractions of real life objects

#### JavaScript Objects
Everything in JavaScript is an object or can be treated like one. Learn about familiar JavaScript objects to get a deeper understanding of why objects are useful.

The **DOM** - An object that represent the HTML document your JavaScript interact with. DOM Elements are objects that you can 
* Apply Properties: `element.style`, `element.innerHTML` ,  `element.parentNode`
* Apply methods: `.getElementbyId()` `.appendChild()`
    
What’s great about these objects is that they’ve abstracted away a lot of the details for you. In other words, they created an interface that lets you use the object without having to know what’s going on under the hood. You can use the method, getElementbyId, over and over without having to know how that works or rewrite all the code that’s underneath it.

[JavaScript/Data_structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)

#### Object Literals and Components of Objects
Objects give us a way to package information about something we want to use in our code. This package is made up of a group of properties and functions, called methods, that work together to represent something in our program.

Properties are like object specific variables that store information in a series of key value pairs. Methods are object specific functions that let your object do something or let something be done to it.

Objects literals are one way to create an object and they’re really great when you’re modeling one single specific thing.
```javascript
const earnie = {
	animal : ‘dog’, //property
	age: 1, //property
	breed: ‘pug’, //property
	
	Bark: function () {  //method  
		console.log(‘Woof!’) 
		};
}
```
Putting all of these properties and methods into a package and attaching it to a variable is called **encapsulation**.


### Dot Notation & Bracket Notation
Learn how to access properties and methods using dot and bracket notation.
```javascript
// Dot Notation
const fruits = [‘apple’, ‘pear’, ‘melon’];
fruistLenght = fruits.length //3 ;

//Bracket Notation
fruits[0];  // apple
```  
Using our ernie example
```javascript
const earnie = {
	animal : ‘dog’, //property
	age: 1, //property
	breed: ‘pug’, //property
	
	Bark: function () {    
		console.log(‘Woof!’) //method
		};
}

console.log (ernie.age); // 1
ernie.bark(); // Woof!
console.log(ernie[‘age’]);// 1
ernie[‘bark’]();// Woof!
```

With bracket notation, you could store a property name inside a variable and use bracket notation with the variable instead. This is really useful if you need to use or generate dynamic properties for example
```javascript
console.log(ernie[‘age’]); // 1
ernie[‘bark’](); // Woof!

var prop = ‘breed’;
ernie[prop];
```
**Object Literals Referring to Themselves** : Many times when writing methods for objects, you might want to refer to one of the object’s properties. For example consider the following code:
```javascript
const teacher = {  
	firstName : "Ashley",  
	lastName : "Boucher"  
};
```
I may want to add a method to this object literal called printName() that will log both the first and last name properties of the teacher variable to the console. To access the value of these properties inside the method, I’ll use the `this` keyword instead of the variable name. This way, you’ll always  access the property values attached to that particular object:
```javascript
const teacher = {  
	firstName : "Ashley",  
	lastName : "Boucher"
	
	printName: function (){
		console.log(this.firstName + this.lastName);
	}  
};
```
  

[**Template Literals**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals): Template literals are literals delimited with backtick (`) characters, allowing for [multi-line strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#multi-line_strings), for [string interpolation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#string_interpolation) with embedded expressions, and for special constructs called [tagged templates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#tagged_templates).

**JSON and bracket Notation**. JSON ( [JavaScript Object Notation](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)), is a data-interchange format. It has a special syntax that looks a lot like a syntax for JavaScript objects. Sometimes, keys in JSON might be more than one word:

```json
var data = {
	“First Name” : “John”,
	“Last Name” : “Doe”
}
```
To access the first name or last name properties of this JSON data, you would use bracket notation:
```javascript
var first = data[‘First Name’];
var last = data[‘Last Name’];
```

####  Changing and Adding Properties
Update and add new properties to object literals using dot and bracket notation.
```javascript
const earnie = {
	animal : ‘dog’, //property
	age: 1, //property
	breed: ‘pug’, //property
	
	Bark: function () {    
		console.log(‘Woof!’) //method
		};
}

// UPDATE WITH DOT OR BRACKET NOTATION 
earnie.age = 2;
earnie[‘age’] = 2;
// ADD NEW PROPERTY
earnie.color = ‘black’;
```

### Working with Classes in JavaScript
#### When Object Literals aren't Enough
Object literals are a handy way to encapsulate data about something specific. But they aren’t great when you want to represent multiples of something with the same or similar properties and methods. If you look at the object literals below, you can see that each of these object literals has a ton of overlap, breaking the rule of **DRY**
```javascript
const ernie = {
	animal: 'dog',
	age: '1',
	breed: 'pug',
	bark: function(){
		console.log('Woof!');
	}
}

const vera = {
	animal: 'dog',
	age: 8,
	breed: 'Border Collie',
	bark: function(){
		console.log('Woof!');
	}
}

const scofield = {
	animal: 'dog',
	age: 6,
	breed: 'Doberman',
	bark: function(){
		console.log('Woof!');
	}
}
```
Imagine a scenario where I’m using objects to manage all of these users on a web app, or all of the books in a library’s online catalog. It’s really easy to see how difficult things can get when you’re using object literals for all of your object needs. Luckily, object literals are just the tip of the OOJS iceberg.

Enter JS class syntax, A class in Object Oriented programming, is a sort of blueprint for an object. It’s a specification. When you write a class, you provide it with a base set of properties and methods. These properties and methods are then available on any object created of that class type. Class syntax is new to JS in ES2015 and is what developers call syntactic sugar.

JavaScript uses something called **prototypes** and the syntax for creating prototypes before ES2015 was complicated and confusing for many developers. Prototypes are less common in classes among other programming languages. To make object oriented JavaScript easier to understand, the class syntax was developed. This syntax, while simple, pretty, and easier to use, has the same functionality as the prototype syntax.

Even though the syntax resembles class based programming, we’re still using prototypes under the hood.

#### Writing your First Class
We’ll create objects for each of the pets that aren’t object literals. To do this, we’re going to write a class, and then create an object of that class type for each of the animals mentioned.
```javascript
const ernie = {
	animal: 'dog',
	age: '1',
	breed: 'pug',
	bark: function(){
		console.log('Woof!');
	}
}

const vera = {
	animal: 'dog',
	age: 8,
	breed: 'Border Collie',
	bark: function(){
		console.log('Woof!');
	}
}

const scofield = {
	animal: 'dog',
	age: 6,
	breed: 'Doberman',
	bark: function(){
		console.log('Woof!');
	}
}
```
Each of these object literals has the same properties, animal, age, and breed. They also have the same method, bark. The value for the animal property in each of them is dog. Because dog is a common value among each of these object literals, it’s a viable option for the name or type of our class. When we’re designing and writing classes, it’s helpful to start by looking for these types of patterns and commonalities among the things we’re trying to model. We could also choose to create a class called pet or even animal. Each of these options is more broad than the last and they each would have slightly different properties and methods. As a developer, how you make these choices is really up to you, but it’s important to keep in mind how you plan to use the object, and what other objects will interact with it, and how your objects might change in the future.

-   It’s wise to keep classes general to save a lot of possible rewriting efforts.
-   Capitalizing the first letter of a class name in its declaration is a common convention in programming
-   constructor() methods goes at the top, inside a class. This is a special method and it’s where you outline the properties that your class will have. When you create an object from this class later on, what you’re doing is invoking this constructor method, and like regular methods, you can pass in parameters.
```javascript
class Pet {
	constructor(){};
}
``` 
[Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
[Classes#Class_body_and_method_definitions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#Class_body_and_method_definitions)

#### Adding Properties inside the Constructor Method
Add properties to the class blueprint using the constructor method.

```javascript
class Pet {
	constructor(animal, age, breed){
		this.animal = animal;
		this.age = age;
		this.breed= breed;
	}
}
```
[this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

#### Instantiating a Pet Object
Now that we’ve finished our constructor method, we’re ready to create or **instantiate** a pet object. Creating an instance of a class is really easy, and you might have seen this syntax when using the JavaScript date object, or when creating a new array.

```javascript
class Pet {
	constructor(animal, age, breed){
		this.animal = animal;
		this.age = age;
		this.breed= breed;
	}
}

const earnie = new Pet('dog', 1, 'pug');
const vera = new Pet('dog', 1, 'border collie');

console.log(earnie);
```

#### Adding Methods to our class

```javascript
class Pet {
	constructor(animal, age, breed, sound){
		this.animal = animal;
		this.age = age;
		this.breed= breed;
		this.sound = sound;
	}
	speak(){
		console.log(this.sound);
	}
}

const earnie = new Pet('dog', 1, 'pug', 'yip yip');
const vera = new Pet('dog', 1, 'border collie', 'woof woof');

earnie.speak();
vera.speak();
```
Another Example: Method that will add a course to a student schedule
```javascript
class Student {
	constructor (gpa, courses){
		this.gpa = gpa
		this.courses = courses
	}
	printGPA(){
		console.log(this.gpa);
	}
}
const ashley = new Student (3.9); 
// -----------

addCourse(course){
	this.courses.push(course)
	}

```

### Getters and Setters
#### Getters
In JavaScript, there are two special methods called getters and setters. These methods allow us to create and retrieve or update an object’s properties respectively. We know that we can do this with bracket or dot notation, but the getter and setter methods increase flexibility.

With getter and setter methods, you have the option to include logic when retrieving or setting the value of a property while still enjoying the simple syntax of accessing and setting these properties directly.

So what is a getter method? In JavaScript (JS) it’s a special method used when you want to have a property that has a dynamic or computed value. The value of the property is computed in the getter method. And even though it’s not stored or attached to the object it can be accessed just like a regular property.

For example, we’re going to add the activity property to the pet class. This property should tell us what our pet is up to based on the time of the day. Unfortunately, we can’t set that property in our constructor method, because its value is dynamic. It changes depending on what time it is

```javascript
class Pet {
	constructor(animal, age, breed, sound){
		this.animal = animal;
		this.age = age;
		this.breed= breed;
		this.sound = sound;
		}
	get activity (){
		const today = new Date();
		const hour = today.getHours();
		
		if (hour > 8 && hour <= 20){
			return 'playing';
		} else {
			return 'sleeping';
		}
	}
	speak(){
		console.log(this.sound);
	}
}

const earnie = new Pet('dog', 1, 'pug', 'yip yip');
const vera = new Pet('dog', 1, 'border collie', 'woof woof');

console.log(earnie.activity);
```
[Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)

Universal Time is the global time standard based on the earth’s rotation. The local time where you live is converted from Universal Time. In JS, you may have to make conversions from UTC to local time.

#### Setters
You learned previously that when a getter method is called, a property value is computed and returned,but this value is not ever updated or stored anywhere. A setter method, on the other hand, receives a value and can perform logic on that value if need be. Then either updates an existing property with that value or stores the value to a new property.

For this example, we’re going to add a setter method that sets an owner property for the pet class. A setter method is created by typing the keyword `set` followed by the name of the property being set, which in our case is *owner*. And then our usual parentheses and curly braces. Setters always receive exactly one parameter. The parameter is the value of the property that’s in we’d like to set. In this example, it will be the owner’s name. Inside our method, we have to set an owner property equal to the parameter we passed in. But there’s a little snag. The name of a property can never be the same as the name of a getter or setter method. We have to create a property name that’s different from owner to hold the value of owner. This is called a **backing property**. And while we can name the backing property however we would like, convention dictates to use the name of the setter function but with an underscore behind it.

To add a value to the setter method, you write it, just like you’d write it just like setting a property value using dot notation.

The setter method is storing the value in a backing property (_owner). When we try to retrieve the value of owner using ernie.owner we get undefined, meaning the owner property has no assigned value. To solve this, we’ve got to create a getter method called owner that returns the value of the backing property, we add this before of setter method

```javascript
//...
get owner(){
	return this._owner;
}

set owner(owner) {
	this._owner = owner;
	console.log (`setter called: ${owner}`);
}
  
speak(){
	console.log(this.sound);
}
}
const ernie = new Pet('dog', 1, 'pug', 'yip yip');
const vera = new Pet('dog', 1, 'border collie', 'woof woof');

ernie.owner = 'Ashley'; // We set our owner property using a setter method
console.log(ernie.owner); // With this we access the property
```
[Working_with_Objects#Defining_getters_and_setters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Defining_getters_and_setters)

```javascript
//Another Example
class Student {
	constructor(gpa, credits){
		this.gpa = gpa;
		this.credits = credits;
	}
  
	stringGPA() {
		return this.gpa.toString();
	}
	
	get level() {
		if (this.credits > 90 ) {	
			return 'Senior';
		} else if (this.credits > 60) {
			return 'Junior';
		} else if (this.credits > 30) {
			return 'Sophomore';
		} else {
			return 'Freshman';
		}
	}
	get major (){
		return this._major;
	}
	set major(major) {
		if (this.level === 'Junior'|| this.level === 'Senior'){
			this._major = major;
		} else {
			this._major = 'None';
		}
	}
}

var student = new Student(3.9, 60);
```
#### Object Interaction
Regular Expressions, or Regex are powerful way to search and match string combinations. The format can be a little complicated, so save this documentation for reference.

[Regular_Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)


## Object Oriented JavaScript: Challenge

## The JavaScript Ecosystem <a name="js-ecosystem"></a>
### JavaScript Outside the Browser
#### Client-Side vs. Server-Side JavaScript
JavaScript was originally designed to run in the browser, but it can be found in other places. JavaScript is the only web-based programming language that can run on both the front end and the back end.

Writing JavaScript that runs on the front end or client side means you're writing JavaScript run in the browser which allows interactivity in web pages. JavaScript is interpreted and executed by the browser's JavaScript engine againts browser specific APIs like the DOM.

Writing back end or server-side JavaScript means that instead of writing code that executes in the browser, you're writing code that executes on the server. Server side javaScript is used for building APIs, databases, web servers, and more. Instead of dealing with the rendered page only, server-side javaScript can be used to provide customized experiences for each's user's request to a website.

Writing JavaScript for both the front end and back en portions of an application is known as Full-Stack Development.

How was JavaScript able to run in different enviroments? Well, **host objects** are supplied by the environment, that way JavaScript code can execute in that specific enviroment.

JavaScript's **native objects** are buitl-in objects that are part of the JavaScript programming language. They're available in both the browser and server-side environments.

[Standard built-in objects - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)
[JS Interview Question: What’s the difference between host objects and native objects?](https://rlynjb.medium.com/js-interview-question-what-s-the-difference-between-host-objects-and-native-objects-b395f7c5fbf1)
[The Landscape of JavaScript - course](https://teamtreehouse.com/library/the-landscape-of-javascript)

#### What is Node.js?
Node is a cross platform runtime environment for developing server-side applications with JavaScript.
Since Node provides a way to run JavaScript outside of the browser, you can use it to build anything from command line tools to frameworks, web servers and more.

Node.js is based on Google Chrome's V8 open source JavaScript engine. but eventhough Chrome's browser and Node use the same JavaScript engine, they're two different run time enviroments.
Node shine's for it's ability in building real-time multi-user applications that handle many events or user actions at the same time. Like tap apps for instance, also multi-player games, collaboration tools, vide-conferencing apps and more.

One of the best parts about Node is its driving ecosystem of free-open source tools. **npm** the node package manager, allows for the sharing and reuse of code and softwarenwritten by other developers in the JavaScript community.

Now, since Node is a runtime enviroment, it does little out of the box, so to make it easier to get setup and working with Node, developers often user a **Node framework** and one of the most popular is Express. Node and Express go hand in hand.
**Express** allows developers to build scalable feature rich applications, wbesites and more on top of Node. Express provides built in tools and functionality to take care of common tasks like routing or handling request at different URL paths. Also serving static files and dynamic templating to render HTML pages.

Developers can also built REST APIs with Express and simple servers that talk to browsers

#### Build Native Applications with JavaScript
Node is really useful to building interactive Command-Line applications or Command-Line interfaces, like *Create React App* the *vue-cli* or *Angular CLI* were built with Node.
You use these command line tols to quickly spin up a project with basic conffiguration and run, build, test and deploy the project to production. Even command line interfaces for module bundlers like **Webpack** and task runners like **Gulp** wre created with Node.

Node makes it possible to build native apps that run on your iOS and android devides. With the framework **React Native** you don't have to worry about learning a language like objective C, Swift or Java.

There's also an amazing framework called **Elecron** that's used for building cross-platform desktop applications using HTML, CSS and JavaScript, which was used to build:
- Visual Studio Code
- Slack
- Skype
- GitHub desktop
- The terminal Hyper
- React 360

### JavaScrip Frameworks, Libraries and Developer Roles
#### JavaScript Frameworks and Libraries
You can do some really complex things with JavaScript, and there are many ways to do the exact same thing.

To help you make some of the low level decision, increase efficiency, and build projects faster, developers often use a frontend JavaScript encrypted framework or library. Many frameworks and libraies help you write clean modern JavaScript, and they allow you to use reliable and effective software design patters frm the start. 

A common use case for a JavaScript framework is to build single page web applications (SPA) that run in the browser.

**React** developed by Facebook is one of the most popular JavaScript libraries. It makes building and mantaining the user intergace of your application faster and easier by breaking it up into smaller reusable componets.

React started out as a UI library form the web browser, but the patters and tools it provides are so useful that's it's been extended to mobile developemnt with the React Native framework

**Vue** shares many similarities with react, except that if offers more tools out of the box, it's smaller in file size and a little easier to pick up. It also makes it easier to create your entire UI or just build and enhance only small parts of your project's UI.

**Angular** is a full-fedged JavaScript framework with more functionality than most JavaScript frameworks and libraries out there. It' maintained by Google and referred a a complete solution because it comes with all the tools necessary to build complex, single page web apps without dependency on any other frameworks or plug-ins.

React, Vue and Angular are traditionally client side frameworks and libraries, they run in the browser and by default produce DOM as output and manipulate the DOM of the rendered page, but also have their server side counterparts built by the open source JavaScript coomunity

**Next.js** is a popular framework for server rendered React apps, it includes a lot of complex configuration right out of the box. Like routing, preventing unecessary code from loading, easy deployment to production, and lots more.

**Nux** is a higher lever framwork for creating server side rendered apps with Vue.It makes it easier to share code between the client and the server, so you can focus on your application logic.

To implement server side rendering in an Angular application, developers use the **Angular Universa**l library

#### Testing JavaScript
Testing helps developers avoid introducing bugs and defects in their projects, which if deployed to production could cost them or their company money and returning users.
Manual testing process work but it can be slow and error prone. In many cases developers programatically test the code and features in their project to ensure expected behavior. They wirte special functions called **unit tests* to check if each part of their program works, even in edge cases or extreme operating parameters.

They first identify the expected outcomes of every part of their program, individual functions for example, and write test againts them to make sure those parts work as inteed.

Writing JavaScript unit tests from scratch, especially on big projects, tend to be limited, hard to implement, and time consuming, so the JavaScript community have created libraries and frameworks that ley you quickly write automated unit tests

**Mocha** runs on Node, its flexible and extendable libary provides the base structure for setting up you tests and it can be easily integrated with other testing libraries

**Jasmine** another popular unit testing framework that does not depend on any other JS framework, popular for testing Angular apps

**Jest** is a feature-rich testing library created by Facebook, many react developers test with it.Many React developers test with Jest because it's lready set up when you create a project with Create React App, but you can test any JavaScript application with Jest It's built for unit and integration testing.

**Enzyme** is a JavaScript testing utility for react, created and used by Airbnb. It's also built to be compatible with other testing libraries.

Writing unit test can help you improve your code, before you vene start writing it, and can serve as a valuable documentation for how your application is supposed to work.

As javaScript developer Eric Elliot stated, tests are your first and best line of defense agains software defects.

#### The Different Types of JavaScript Developers
A typical software development team is made up several different roles;
- *Junior Developer*: Is ususally how new developers get their foot in the door. They likely won't be setting up and coding a project end to end ot work from scratch, rather they'll usually contribute to existing code bases. They'll often learn the ropes by ficing bugs and adding additional features and functionality to existing projects.
- *Senior Developer*: Handle most of project's development life-cycle end to end. They're team multipliers and make people around them better. They'll provide guidance and direction to junior developers through mentorship, code reviews and pair programming sessions, where the junior and senior developers program together at one work station.

Both junior and senior may contribute regularly to the developer community.

Developers might work along roles such as:
- *Architech*: A typical senior technical role responsible for coming up with the strategy and technical solutions for a project, communicating it with a team and making sure it's successfully executed. The architech also has the technical  knowledge and the skills to know what's possible and not possible in a project.

They might decide on what tools will be used by the developers to build the project and often have coding skills to create early prototypes.
- *Software Development Manager*: Usually keeps the development team on track and oversees project through completition

- *QA testers*: Make sure that every part of the software does what it was inteded to do. They test the project for defects and bugs and report and document any technical issues. They also communicate with the developers frequently to make sure all errors are corrected before shipping the project.
- *Designerss*: Work on visual design
- *Front End Developers*: Create the HTML and CSS and often times the client-side JavaScript that makes the interface interactive
- *Product Manager*: Works cross-functionally or with just about everyone on the team. They figure out what products to make for the company and make sure that those products get made.
They'll often lead the team form a project's conception all the way thorugh to its launch, working with customer research, problem identification, user experience research, wireframing, and more.

As a developer, you'l be counted on to solve problems and might do a little bit of everything from prototyping and testing to fixing bugs and implementing the business logic of a program.


