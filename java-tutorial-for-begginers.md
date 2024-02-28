# Java Tutorial for Beginners
-----

Author: Sheila Anguiano
Course: Java Tutorial for Beginners
Instructor: Bro Code Channel

-----

# Table of Contents

1.  [Java Tutorial for beginners](#java-beginner)
2.  [Variables in Java](#variables)
3.  [How to swap 2 variables](#swap-two-variables)
4.  [How to accept user input in Java](#user-input)
15. [Java Arrays](#arrays)
16. [Java 2D arrays](#2d-arrays)
17. [Java String Methods](#string-methods)
18. [Java Wrapper Classes](#wrapper-classes)
21. [Java for-each Loop](#for-each-loop)
22. [Java Methods](#java-methods)
23. [Java Overloaded Methods](#overloaded-methods)
24. [Java printf](#java-printf)
25. [Java final keyword](#final-keyword)
26. [Java Objects](#objects)
27. [Java Constructors](#java-constructors)
28. [Java Variable Scope](#variable-scope)
29. [Java Overloaded Constructors](#overloaded-constructors)
30. [Java toString Method](#tostring)
31. [Java Array of Objects](#array-of-objects)
32. [Java Object Passing](#object-passing)
33. [Java Static Keyword](#static)
34. [Java Inheritance](#inheritance)
35. [Java Method Overriding](#overriding)
36. [Java Super keyword](#super)
37. [Java Abstraction](#abstraction)
38. [Java Access Modifiers: public, protected, private](access-modifiers)
39. [Java Encapsulation](#encapsulation)
40. [Java Copy Objects](#copy-objects)
41. [Java Interface](#jave-interface)
42. [Java Polymorphism](#polymorphism)
43. [Java Dynamic Polymorphism](#java-dynamic-polymorphism)
44. [Java Exception Handling](#exception-handling)

## Java Tutorial for Beginners <a name="java-begginer"></a>
Computer languages are on a spectrum between being low level or High-level. Computers only understand  binary which is a low-level language referred **machine code**.
To create machine code, we write in a format called **source code** which is undertsandable by humans and then is **compiled** (transalated) to machine code. 

When we create java code the file ends with `.java` extension. When we compile our source code to machine code it's machine specific, but java has a solution for this problem, an intermediary step where we can compile our source code into `bytecode`. Bytecode is cross platforma dn ends with a `.class` file extension.

To read the bytecode, the machine uses a **JVM** (Java Virtual Machine) to translate the bytecode to machine code. You het a JVM with a **JDK** (Java Development  Kit) which contains development tools as well as a **JRE** (Java Runtime Enviroment) which contains a library, toolkits and the JVM which transaltes java bytecode to our machine specific machine code.

CONTINUE FROM 8:21MIN

## How to Swap 2 Variables<a name ="swap-variables"></a>
Imagine that you have 2 glasses of water filled, one with water and the other with KoolAid.
```java
public class Main {
  public static void main( String[] args) {
    String x = "water";
    String y = "Kool-Aid";

    x=y;

    System.out.println("x: " +x); //x: Kool-Aid
    System.out.println("y: " +y); //y: Kool-Aid
  
  }
}
```
If we try to do this with the glasses, the Y one, would overflow, so we need an extra glass that we'll call `temp`
```java
public class Main {
  public static void main( String[] args) {
    String x = "water";
    String y = "Kool-Aid";
    String temp;

    temp=x;
    x=y;
    y=temp;

    System.out.println("x: " +x); //x: Kool-Aid
    System.out.println("y: " +y); //y: water
  }
}
```


## Arrays <a name="arrays"></a>
An array is used to store multiple values in a single variable.
- They have to be the same data type.


```java
public class Main {
  String[] cars = {"Camaro", "Corvette", "Tesla"};

  cars[0] = "Mustang"
  System.out.println(cars[0]); //Returns Mustang
  System.out.println(cars[3]); //Returns "Index out of bounds"
}
```
There is an additional way to create an array and that is by first allocating the amount of elements that we'll need and then storing the values later on in the program so this is an additional way to write an array.

Now we can use a for loop to iterate through all of the elements in an array.

```java
public class Main {
  String[] cars = new String[3];
  
  cars[0] = "Camaro";
  cars[1] = "Corvette";
  cars[2] = "Tesla"

  System.out.println(cars[2]); // Corvette

  for(int i=0; i < cars.length; i++){
    System.out.println(cars[i]);
  }

}
```

## 2D Arrays <a name="2d-arrays"></a>
A dynamic list of separate lists. You can change the size of these lists during runtime, which is an advantage of array list over just standard arrays.

We're going to create separate shopping lists and at the end we're going to add them.
Array lists store objects so we need to use the wrapper class

```java
import java.util.*;

public class Main {
  public static void main( String[] args {
    
    ArrayList< ArrayLists<String>> = groceryList = new ArrayList();

    ArrayList<String> bakeryList = new ArrayList();
    bakeryList.add("pasta");
    bakeryList.add("garlic bread");
    bakeryList.add("donuts");

    ArrayList<String> produceList = new ArrayList();
    produceList.add("tomatoes");
    produceList.add("zucchini");
    produceList.add("peppers");

    ArrayList<String> drinkList = new ArrayList();
    drinkList.add("soda");
    drinkList.add("coffee");

    groceryList.add(bakeryList);
    groceryList.add(produceList);
    groceryList.add(drinkList);

    System.out.println(bakeryList.get(0)); // pasta
    System.out.println(groceryList.get(0).get(0)); //pasta


  })
}
```

## Java String Methods <a name ="string-methods"></a>
**String** a reference data type that can store one or more characters. Reference data types jave access to useful methods.
```java
import java.util.*;

public class Main {
  public static void main( String[] args {
    
    String name = "Momo";

    boolean  result = name.equals("Momo");
    System.out.println(result); //true
    
    int result2 = name.length();

  })
}
```
 https://www.w3schools.com/java/java_ref_string.asp


## Java Wrapper Classes <a name ="wrapper-classes"></a> 
A **wrapper class** provides a way to use primitive data types as reference data types. 
- Reference data types contain useful methods 
- Can be used with collections (ex. ArrayLists)
- Refrence data types are slower to access 

**Primitive**     **Wrappe**r
boolean           Boolean
char              Character
int               Integer
double            Double

Java has this feature called
**autoboxing**: the automatic conversion that the Java compiler makes beteen the primitive types and their corresponding object wrapper class.
**unboxing**: the reverse of autoboxing. Automatic conversion of wrapper class to primitive

```java
Boolean a = true; // This is autoboxing, converting automatically a primite type
Character b = '@';
Integer c = 123;
Double d = 3.14;
String e = "Noelle"

//Now you can use dot notation to use specific methods based on the data type.

if (a== true){ // Here Java is performing unboxing
  System.our.println("This is true);
}
 
```

## java for-each loop  <a name ="for-each-loop"></a>
A for each loop is a traversing technique to iterate through the elements in an array/collection.
- This technique takes less steps and is more flexible
- BUT is less flexible

1. Start by listing the data type of the data type you're hoing to iterate

```java
import java.util.*;

public class Main {
  public static void main( String[] args {
   
   String[] animals = {"cat", "dog", "rat", "bird"};
  // For every index in our array of animals
   for(String i : animals){
    System.out.println(i);
   }
  })
}
```
```java
import java.util.ArrayList;

public class Main {
  public static void main( String[] args {
 
    ArrayList<String> animals = new ArrayList<String>();

    animals.add("cat");
    animals.add("dog");
    animals.add("rat");
    animals.add("bird");
  
   for(String i : animals){
    System.out.println(i);
   }
  })
}
```

## Java Methods<a name ="java-methods"></a>

A methods is a block of code that is executed whenever it is called upon

When we begin our program an execute it, we begin by calling the `main` method, so anything between that set of curly brackets, is part of the main method.

To begin creating a method, we'll need a return type, that we'll go over later.
```java

public class Main {
  public static void main( String[] args) {
    hello();
  }
}

void hello(){
  System.out.println("Hello");
}
```
If we try to run the code above, we'll run in one problem, which is: `we cannot make a static reference to the non-static method hello() from the type Main`, so this means that we need to precede this method with the keyword `static` because we're calling 
the `hello` method from the `static` method of main.
```java

public class Main {
  public static void main( String[] args) {
    hello();
  }
}

static void hello(){
  System.out.println("Hello");
}
```
So normally we do not need to add this keyword.
One feature available to methods is that you can pass a value or a variable when we call it
The variables you're sending to a method are know as **arguments** but in order for this to work, you need to match this with the **parameters** you use to set up the method.


```java

public class Main {
  public static void main( String[] args) {
    String name = "Midnight"
    int age = 2;
    hello(name, age);
  }
}

static void hello(String name){
  System.out.println("Hello " + name);
  System.out.println("You are " +age);
}
```
Now going back to **return types** we can return a value back to the area in which we called a method for example:
```java

public class Main {
  public static void main( String[] args) {
    
    int x = 3;
    int y = 4;
    System.out.println(add(x,y));

  }
}
// Since we want to return an integer, int would be the return type
//Since this has a return type, it would need a return statement
static int add(int x, int y){
  return x+y;
}
```

## Java Overloaded Methods <a name ="overloaded-methods"></a>
Overloaded Methods, are methods that share the same name but have different parameters, this is allowed becase each method needs its own unique **method signature** that is the method's name plus it's parameters. They can share the same name but they will need different parameters to give them each a unique method signature

```java

public class Main {
  public static void main( String[] args) {
    int x = add(1,2,3);
    double y = add(2.5,2.3);
    System.out.println(x);
     System.out.println(y);

  }
}

static int add(int a, int b){
  System.out.println("This is overloaded method #1")
  return a + b;
}
static int add(int a, int b, int c){
  System.out.println("This is overloaded method #2")
  return a+b+c;
}
static int add(int a, int b, int c, int d){
  System.out.println("This is overloaded method #3")
  return a+b+c+d;
}

static int add(double a, double b){
  System.out.println("This is overloaded method #4")
  return a+b+c+d;
}
```
Some factors that are taken into account with parameters are the number of parameters, the data type and the order of the values.


## Java printf <a name ="printf"></a>
The `printf` is an optional method to control, format, and display text to the console window
- It needs two arguments = format string + (object/variable/value)

```java
public class Main {
  public static void main( String[] args) {
    System.out.printf("This is a format string %d", 123); //This is a format string 123
  }
}
```
So we can format some value and place it at some position in the string to wherever wer add a format specifier wich is represented by a *%* sign
%d = Add a decimal value 
Depending on the `%[flags][precision][width][conversion character]` that's how it going to be displayed
```java
public class Main {
  public static void main( String[] args) {
   boolean myBoolean = true;
   char myChar ='@';
   String myString = "shei";
   int myInt = 50;
   double myDouble = 1000;

  //[conversion-character]
   System.out.printf(%b, myBoolean);
   System.out.printf(%c, myChar);
   System.out.printf(%s, myString);
   System.out.printf(%d, myInt);
   System.out.printf(%f, myDouble);
 //[width]
 //minimum number of characters to be written as output
 System.out.printf("Hello %10s", myString); //Hello         Bro
 System.out.printf("Hello %-10s", myString); //This will justofy the text and leave the space to the right empty

 //[Precision]
 //sets number fo digits precision when outputting floating-point values
 System.out.printf("You have this much money %.2f", myDouble); //You have this money 1000.00

 //[Flags]
 // adds an effect to output based on the flag added to format specifier
 // - : left-justify
 // + : output a plus (+) or minus sign for a numeric value
 // 0 : numeric values are zero-padded
 // , : comma grouping separator if numbers > 100)
 System.out.printf("You have this much money %+f", myDouble) //You have this money +1000.00

  System.out.printf("You have this much money %020f", myDouble) //You have this money +1000.00 
  System.out.printf("You have this much money %,f", myDouble) //You have this money 1,000.00000 
  }
}
```
So in order to display a certain object you need a matching conversion specifier

## Final Keyword <a name ="final-keyword"></a>
Anything that is declared final cannot be changed or updated in the program
```java
public class Main {
  public static void main(String[] args){
    double pi = 3.14159
    pi = 4;
    System.out.println(pi); // 4.0
  }
  }
}
```
When we print `pi` the value change to 4, because we updated the value, but if we use the `final` keyword:
```java
public class Main {
  public static void main(String[] args){
    final double PI = 3.14159
    pi = 4;
    System.out.println(pi); // 4.0
    }
  }
}
```
We'd get a compilation error, because once anything is assigned `final`cannot be re-assigned.

## Java Objects and Object Oriented Programing (OOP) <a name ="objects"></a>
An object is an instance of a class that may contain attributes and methods.

```java
public class Car {

  String make = "Chevrolet";
  String model = "Corvette";
  int year = 2020;
  String color = "pink";
  double price = 50000.00;

  void drive(){
    System.out.println("You drive a car");
  }
  void brake(){
    System.out.println("You step on the brakes");
  }

}
```
```java

public class Main {
  public static void main(String[] args){
    Car myCar = new Car();
    System.out.println(myCar.model); // Corvette
    myCar.drive(); // You dirve a car
    
    }
  }
}
```
We can reuse a class to instantiate multiple instances of this class. Now with this we run into the problem that all the car will have the same attributes, and we can solve this with Constructors

## Java Constructors<a name ="java-constructors"></a>
A constructor is a special method that is called when an object is instantiated (created). We can pass it arguments when we instantiated so they can be assigned to the object we're creating
```java
public class Human {
  
  String name;
  int age;
  double weight;


  //constructor
  Human(String name, int age, double weight){
    name = name;
    age = age;
    weight = weight
  }

}
```
```java
public class Main {
  public static void main(String[] args){
    Human human = new Human("Rick", 65, 70);
    System.out.println(human.name); //null
    }
  }
```
Now if we try to run the code, like this, we'll get `null` so we need to use `this`.
```java
public class Human {
  
  String name;
  int age;
  double weight;

  //constructor
  Human(String name, int age, double weight){
    name = this.name;
    age = this.age;
    weight = this.weight
  }

  void eat(){
    System.out.println(this.name+" is eating")
  }
}
```
```java
public class Main {
  public static void main(String[] args){
    Human human = new Human("Rick", 65, 70);
    System.out.println(human.name); // Rick
    }
  }
```

## Java Variable Scope <a name ="variable-scope"></a>
Local = declared inside a method, visible only to that method
Global = declared outside a methid, but within a class visible to all parts of the class.

```java
import java,util.Random;
public class DiceRoller {
  DiceRoller(){
    Random random = new Random();
    int number = 0;  // this is local variable
    roll(random, number);
  }

  void roll(random random, int number ){
    number = random.nextInt(6)+1;
    System.out.println(number);
  }

}
```
```java
import java,util.Random;
public class DiceRoller {
  Random random;
  int number = 0;
  
  DiceRoller(){
    Random random = new Random();
    roll();
  }

  void roll(random random, int number ){
    number = random.nextInt(6)+1;
    System.out.println(number);
  }
}
```
```java
public clas Main {
  public static void main(String[] args){
    DiceRoller diceroller = new DiceRoller();
  }
}
```

## Java Overloaded Constructors <a name ="overloaded-constructors"></a>
Overloaded constructors are multiple constructors within a class with the same name but have different parameters.When you combine a costructor name plus it's parameters you have a **signature**

```java
public class Pizza {
  String bread;
  String sauce;
  String cheese;
  String topping;

 Pizza(String bread, String sauce, String cheese, String topping){ 
    this.bread = bread;
  this.sauce = sauce;
  this.cheese = cheese;
  this.topping = topping;
  
  System.out.println("This are the ingredientes of your pizza:");
  System.out.println(pizza.bread);
  System.out.println(pizza.sauce);
  System.out.println(pizza.cheese);
  System.out.println(pizza.topping;  
 
 }
Pizza(String bread, String sauce){ 
  this.bread = bread;
  this.sauce = sauce;  
  System.out.println("This are the ingredientes of your pizza:");
  System.out.println(pizza.bread);
  System.out.println(pizza.sauce);
 }
Pizza(String bread, String sauce){ 
  this.bread = bread;
  this.sauce = sauce; 
  this.cheese = cheese; 
  
  System.out.println("This are the ingredientes of your pizza:");
  System.out.println(pizza.bread);
  System.out.println(pizza.sauce);
  System.out.println(pizza.cheese);
 }
}
```
```java
public class Main{
  public static void main(String[] args){
    Pizza pizza = new Pizza("thick crust", "tomato", "mozarella", "pepperoni");
  }  
}
```

## Java toString method <a name ="tostring"></a>
A special method that all objects inherit that returns a string that "textually represents" an object, can be used both implicitly and explicitly.
```java
public class Car {
  String make = "Chevrolet";
  String model = "Corvette";
  int year = 2020;
  String color = "pink";
  double price = 50000.00;
}
```
```java

public class Main {
  public static void main(String[] args){
    Car myCar = new Car();
    System.out.println(myCar.model); // Corvette
    System.out.println(myCar.make);
    System.out.println(myCar.year);
    }
  }
}
```
Now if you tried to run `System.out.println(car);` you'll get something lile `Car6%$^&%` which is the address of that car object in memory and you will get the same information if you write `car.toString()` but we can *override* to instead print a textual representation

```java
public class Car {
  String make = "Chevrolet";
  String model = "Corvette";
  int year = 2020;
  String color = "pink";
  double price = 50000.00;

  public String toString(){
    String myString = make + "\n" + model+"\n"+year;
    return myString;

    //Or you can write it in one line
    //return make + "\n" + model+"\n"+year;
  }
}
```
So now if we call the method implictly  `car.toString()` or explicitly `System.out.println((car.toString())``


## Java Array of Objects <a name ="array-of-objects"></a>
The standard formula to create an array
```java
           int[] numbers = new int[]
// data type[]    name          data Type [size]
```
So let's create now an array of objects
```java
public class Main {
  public static void main (String[] args) {    
    Food[] refrigerator = new Food[3];

    Food food1 = new Food("Pizza");
    Food food2 = new Food("Hamburger");
    Food food3 = new Food("Hot dog");

    refrigerator[0]= food1;
    refrigerator[1]= food2;
    refrigerator[2]= food3;
  
    System.out.println(refrigerator[0]); //This will return the address Fppd@36baudh
    System.out.println(refrigerator[0].name); //Pizza
  }
}
```
```java
public class Food{
  String name;
  //constructor
  Food (String name){
    this.name = name;
  }
}
```
Now there is another way to set up our array of objects
```java
public class Main {
  public static void main (String[] args) {    

    Food food1 = new Food("Pizza");
    Food food2 = new Food("Hamburger");
    Food food3 = new Food("Hot dog");

    Food[] refrigerator = {food1, food2, food3};
  
    System.out.println(refrigerator[0]); //This will return the address Fppd@36baudh
    System.out.println(refrigerator[0].name); //Pizza
  }
}
```

## Java Object Passing as arguments <a name ="object-passing"></a>
```java
public class Main {
  public static void main (String[] args) {    
    Garage garage = new Garage();
    Car car = new Car("BMW");
    Car car2 = new Car("Tesla);

    garage.park(car); // The BMW is parked in the garage
    garage.park(car2); // The Tesla is parked...

  }
} 
```
```java
public class Garage {
   
   void park(Car){
    System.out.println("The "+car.name+" is parked in the garage");
   }
}
```
```java
public class Car {
  String name;
  Car( String name){
    this.name = name;

  }
}
```
In conclusion you can pass objects as arguments to a method but when you declare that method you have to have the parameters accept objects of that data type

## Java Static Keyword <a name ="static"></a>
This is a keyword modifier that can be applied to a variable, method or even classes. Anything that is *static* is also known  as a static member. A good way to think about this is that the class that contains the static member, OWNS it.
So anything that the class owns is shared by all instances of that class, meaning if we create objects from this class they all have to share this variable or method

```java
public class Friend {
  String name;
  static int numberOfFriend;

  Friend(String name){
    this.name = name;
  }
}
```
```java
public clas Main{
  public static void main(String[] args){
    System.out.println(Friend.numberOfFriends); //0
  }
} 
```
Now, we'll create some Friends

```java
public class Friend {
  String name;
  static int numberOfFriend;

  Friend(String name){
    this.name = name;
    numberOfFriends++;
  }
}
```

```java
public clas Main{
  public static void main(String[] args){
    Friend friend1 = new Friend("Spongebob");
    Friend friend2 = new Friend("Patrick");
    Friend friend3 = new Friend("Squidward);

    System.out.println(Friend.numberOfFriends); //3
  }
}
```
Now is entirely possible to accessa static variable using an object instance name itself ` System.out.println(friend2.numberOfFriends);` but is not recommended and you, the only this could work is by deleting the `static` word from the class `int numberOfFriend;` so that each of the Friend objects has their very own copy of the number of friends variable.

Let's create a static method
```java
public class Friend {
  String name;
  static int numberOfFriend;

  Friend(String name){
    this.name = name;
    numberOfFriends++;
  }
  static void displayFriends(){
    System.out.println("You have "+numberOfFriends+" friends");
  }

}
```
The preferring name of calling a static method is by the class name and not by the name of one of its instances
```java
public clas Main{
  public static void main(String[] args){
    Friend friend1 = new Friend("Spongebob");
    Friend friend2 = new Friend("Patrick");
    Friend friend3 = new Friend("Squidward);

    Friend.displayFriends();
  }
}
```
Another example is the `.round` method of the class `Math`

## Inheritance <a name ="inheritance"></a>
The process where one class acquires the attributes and methods of another.
So,here we have everything related to vehicles whitin the vehicle class and we would like that `Car` and  `Bicycle` class to receive these attributes and methods from the vehicle class, se we'll use `extense`

Now, the bicycle and Car classes are subclasses of Vehicle, also known as `child classes` and the `vehicle` class is the **super class** or **parent class**

```java
public class Vehicle {
  double speed;
   void go(){
    System.out.println("This vehicle is moving");
   }

   void stop(){
     System.out.println("This vehicle is stopped");
   }
  

}
```
```java
public class Car extends vehicle {
}
```
```java
public class Bicycle extends vehicle {
  
}
```
```java
public clas Main{
  public static void main(String[] args){
    Car car = new Car();
    car.go() // This vehicle is moving
    Bicycle bike = new Bicycle();

    System.out.println(bike.speed); // 0.0
  }
}
```
Now the child classes can have their own unique additional attributes and methods
```java
public class Car extends vehicle {
  int wheels = 2;
  int doors = 4;
}
```

```java
public clas Main{
  public static void main(String[] args){
    Car car = new Car();
    car.go() // This vehicle is moving
    Bicycle bike = new Bicycle();

    System.out.println(bike.speed); // 0.0
    System.out.println(car.doors); // 4
  }
}
```

## Method Overriding <a name ="overriding"></a>
Declaring a method in a sub-class, which is already present in the parent class. This is so that a child class can give its own implementation
```java
public class Animal{
  void speak(){
    System.out.println("The animal speaks");
  }
 
}
```
```java
@Override
public class Dog extends Animal {
  void speak(){
    System.out.println("The dog barks");
  }

 
}
```
```java
public clas Main{
  public static void main(String[] args){
    Dog dog = new Dog();
    dog.speak() // The dog barks
 
  }
}
```
Now our `speak` method under the `Dog` class is considered the *overriding method* and the one it inherents from its parent is considered the *overriden method*.
And if we're overriding a method, it should have the `@Override` which is not necessary, but is a GOOD PRACTICE to let others know that this is an overriding method

## Java Super <a name ="super"></a>
The `super` keyword refers to the superclass (parent) of an (that's assuming you're assuming inheritance) object very similar to the "this" keyword
```java
public class Person {
  String name;
  int age;
  Person(String name, int age){
    this.name = name;
    this.age = age;
  }
}
```
```java
public class Hero extends Person {
  String power
  Hero(String name, int age, String power){
    super();
    this.power = power;
  }
}
```
```java
public clas Main{
  public static void main(String[] args){
   Hero hero1 = new Hero("Batman", 42, "$$$");
  
  System.out.println(hero1.name); //Batman
  }
}
```
Another use of the `super` keyword is to call a method within the super class.
```java
public class Person {
  String name;
  int age;
  Person(String name, int age){
    this.name = name;
    this.age = age;
  }
  public String toString(){
    return this.name +"\n" + this.age+"\n"
  }
}
```
```java
public class Hero extends Person {
  String power
  Hero(String name, int age, String power){
    super();
    this.power = power;
  }
   public String toString(){
    return super.toString()+this.power;
  }
}
```
```java
public clas Main{
  public static void main(String[] args){
   Hero hero1 = new Hero("Batman", 42, "$$$");
  
  System.out.println(hero1.toString); //Batman 42 $$$
  }
}
```

## Java Abstraction <a name ="abstraction"></a>
This is a keyword that can be applied to both classes and methods when you define them.
An `abstract class` cannot be instantiated but they can have a subclass that can be
```java
public class vehicle{}
```
```java
public class Car exteds Vehicle {}
```
And at this point we can create instances of both classes, but we might not want that. By adding the `abstract` keyword, we add a layer of security. Ex. Let's pretend that we work at a car delarship, and someone say that they want a vehicle, but that doesn't tells us if that means a Car, a bike, etc. 
So we prevent someone for instanciating something that may be too generic by adding the abstract word.

```java
public abstract class vehicle{}
```
And that way we can no longer can create a instance of the class.

An `abstract method` is declared without implementation
```java
public abstract class vehicle{
  abstract void go(){}
}
```
So now we need to implement it in the child class
```java
public class Car exteds Vehicle {
  @Override 
  void go(){
    System.out.println("The car goes BRRR");
  }
}
```


## Java Access Modifiers <a name ="access-modifiers"></a>
Access modifiers add a layer of security to our programs, and we'll cover:
- public
- protected
- private
 And to demostrate these we'll need a couple of packages. A **Packages** is a collection of classes whereas a *class* is a collection of code.
 We're going to create 2 packages and 2 classes within each package:

 Package1
 ```java
 package package1;
 import package2.*;

 public class A {
   public static void main(String[] args){

   }
 }
```
```java
package package1;
import package2.*;

 public class B { }
 ```

 Package2
 ```java
 package package2;

 public class C { }
 ```
 ```java
 package package2;
 import package1.*; // The asteriks means import everything

 public class Asub exteds A{ }
 ```
 So from the `Asub` class we can inherit everything from the A class.
 So first `default`:

 ```java
 package package2;

 public class C {
    String defaultMessage = "This is the defauly";
  }
 ```
 
 In the above class, we're not using any access modifier
 
 ```java
 public class A {
   public static void main(String[] args){
    C c = new C();
    System.out.println(d.defaultMessage);
   }
 }
```

The above code in Class A will give us an error, because anything using the *deafult* access modifier is only visible to anything within the same package

But if we copy-pasted it in the **Asub** class:

 ```java
 package package2;
 import package1.*; // The asteriks means import everything

 public class Asub exteds A{
   public static void main(String[] args){
    C c = new c();
    System.out.println(c.defaultMessage);
   }
  }
 ```
 This will work because it's within the package (Class C and Asub)

 **Public Modifier**
  ```java
 package package2;

 public class C {
    public String publicMessage = "This is public";

    String defaultMessage = "This is the default";
  }
```
Anything that is *public* is available or visible to other packages

```java
 public class A {
   public static void main(String[] args){
    C c = new C();
    System.out.println(d.publicMessage);
   }
 }
```
 **Protected Modifier**
 Something that is *protected* is accesible to a different class in a diferent package  as long as that class is a subclass of whatever class contains that contains that protected member

```java
 package package2;

 public class C {
    protected String  protectedMessage = "This is protected";
    public String publicMessage = "This is public";
    String defaultMessage = "This is the default";
  }
```


 ```java
 package package2;
 import package1.*; // The asteriks means import everything

 public class Asub exteds A{
   public static void main(String[] args){
   Asub asub = new Asub();
   }
  }
 ```
**Private Access Modifiers**
Something that is private is only visible to the class that contains itself

```java
 package package2;

 public class C {
    protected String  protectedMessage = "This is protected";
    public String publicMessage = "This is public";
    String defaultMessage = "This is the default";
    private String privateMesssage = "This is private"
  }
```
```java
package package1;
import package2.*;

 public class B { 
  private String privateMesssage = "This is private";
 }
 ```

 ```java
 public class A {
   public static void main(String[] args){
      B b  = new B();
      System.out.println(b.publicMessage); // This won't be visible
   }
 }
```

## Java Encapsulation
This is the concept of attributes of a class will be hiden or private and can only be acccessed through methods (getters & setters).
You should make attributes private if you don't have a reason to make them public.

```java
public class Car {
  private String make;
  private String model;
  private int year;

  Car(String make, String model, int year){
    this.make = make; 
    this.model = model;
    this.year = year;
  }
}
```
 ```java

public class Main {
  public static void main(String[] args){
   Car car = new Car("Checvrolet", "Camaro", 2021);
   System.out.println(car.make); // This will throw an exception because that field is not visible, because is private.
   }
  }
 ```
For that we use a `getter` method.

```java
public class Car {
  private String make;
  private String model;
  private int year;

  Car(String make, String model, int year){
    this.make = make; 
    this.model = model;
    this.year = year;
  }

  public String getMake(){
    return make;
  }
public String getModel){
    return model;
  }
  public int getYear(){
    return year;
  }
}
```
So now we can use ` System.out.println(car.getMake());`. And to change the fields, we would need to use a Setter method and update our class:

```java
public class Car {
  private String make;
  private String model;
  private int year;

  Car(String make, String model, int year){
    this.setMake(make); 
    this.setModel(model);
    this.setYear(year);
  }

  public String getMake(){
    return make;
  }
public String getModel){
    return model;
  }
  public int getYear(){
    return year;
  }
  public void setMake(String make){
    this.make = make;
  }
  public void setModel(String model){
    this.model = model;
  }
  public void setYEar(int year){
    this.year = year;
  }
}
```

## Java Copy Objects <a name="copy-objects"></a>
We're going to copy some cars
```java
public class Car {
  private String make;
  private String model;
  private int year;

  Car(String make, String model, int year){
    this.setMake(make); 
    this.setModel(model);
    this.setYear(year);
  }

  public String getMake(){
    return make;
  }
public String getModel){
    return model;
  }
  public int getYear(){
    return year;
  }
  public void setMake(String make){
    this.make = make;
  }
  public void setModel(String model){
    this.model = model;
  }
  public void setYEar(int year){
    this.year = year;
  }
}
```

```java
public class Main {
  public static void main(String[] args){
   Car car1 = new Car("Checvrolet", "Camaro", 2021);
   Car car2 = new Car ("Ford", "Mustang", 2022);

   System.out.println(car1); // Car@36baf  this are the address in memory
   System.out.println(car2); // Car@7a811
   System.out.println(car1.getMake());
   }
  }
 ```
 Now, let's say that we want that car2 has the same attributes as car1, we might want to do `car2 = car1`, but what this do, is give car1 two different names, because it has teh same place in memory

So the correct way to do this is creating a copy method in our Car class, so in the main method we write: `car2.copy(car1)`
```java
public class Car {
  private String make;
  private String model;
  private int year;

  Car(String make, String model, int year){
    this.setMake(make); 
    this.setModel(model);
    this.setYear(year);
  }

  public void setYEar(int year){
    this.year = year;
  }
  public void copy(Car x){
    this.setMake(x.getMake());
    this.setModel(x.getModel());
    this.setYear(x.getYear());
  }
}
```
Now another way to do this is by creating a `copy` constructor, we start by instantiating it in Main: `Car car2 = new Car(car1)`

```java
public class Car {
  private String make;
  private String model;
  private int year;

  Car(String make, String model, int year){
    this.setMake(make); 
    this.setModel(model);
    this.setYear(year);
  }

  Car(car x){
    this.copy(x);
  }

  //...
public void copy(Car x){
    this.setMake(x.getMake());
    this.setModel(x.getModel());
    this.setYear(x.getYear());
  }
```

## Java Interface <a name="interface"></a>
Think of interfaces as a template that can be applied to a class. Similar to inheritance, but specifies what a class has/must do. 
Classes can apply more than one interface, inheritance is limited to 1 super

With interfaces you can declare variables normally like you can do with inheritance. You can also declare some methods and you don't need to create a body for these methods.

```java
public interface Prey { void flee(); }
```
```
public interface Predator { void hunt(); }
```
So when a class is implementing one of these interfaces they need to implement and define what the method is gonna do in a class, which is basically Overriding
```java
public class Rabbit implements Prey {
 @Override
 public void flee(){ System.out.printLn("The Rabbit is fleeing") }
}
```
```java
public class Hawn implements Predator {
  @Override
  public void hunt(){ System.out.printLn("The Hawk is hunting"); }
}
```
```java
public class Fish implements Prey, Predator{
  @Override
  public void flee(){System.out.printLn("The Fihs is fleeing")}

  @Override
  public void hunt(){ System.out.printLn("This Fish is hunting smaller fish")}
}
```

## Java Dynamic Polymorphism