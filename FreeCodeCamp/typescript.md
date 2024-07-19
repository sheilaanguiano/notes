# TypeScript
https://www.youtube.com/watch?v=SpwzRDUQ1GI&t=471s

Typescript is a superset of JavaScript meaning all JS code is also valid in Typescript, however Typescript enhances your coding experience by enabling you to code with better confidence in the stability and longevity of your projects

## Introduction
Why learn TypeScript?
* **Confidence**: App crashing run errors are dramatically reduced by Typescript, which checks the code at compile time before it ever gets deployed
* **Productivity**: Using Typescript "turns on" a number of neat features that make your life as a developer a lot easier, Autcomplete, refactoring capabilities, immediate error checking , and more. All greatly improve the Developer Experience(DX).
* **Employability**: TypeScript is considered "table stakes" by many companies, even if it isn't explicitly listed in the job descriptions. Knowing even a little of TypeScript can set you apart from other junior developer candidates.

Analogy: blueprints before building

## Intro to Pizza App
We're going to make a console based restaurant app in JavaScript
```
const menu = [
  {name: "Marguerita", price: 8},
  {name: "Pepperoni", price 10},
  {name: "hawaiian", price 10},
  {name: "Veggie", price 9},
]

const cashInRegister = 100;
const orderQueue= []
const nextOrderId = 1;

function addNewPizza(pizzaObj){
  menu.push(pizzaObj)
}

function placeOrder (pizzaName){
  const selectedPizza = menu.find((pizzaObject) => pizzaObject.name === pizzaName );
  cashRegister += selectedPizza.price;
  const newOrder = {pizza: selectedPizza, status:"ordered", id: nextOrderId++ };
  orderQueue.push(newOrder);
  return newOrder;
}

function completeOrder (orderId){
  const order = orderQueue.find((order) => order.id === orderId);
  order.status = "completed";
  return order;
}

```


