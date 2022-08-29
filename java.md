# Java
----------
Author: Sheila Anguiano
Teachers:
Platform: Threehouse
-----------

# Table of Contents
1. [Java Basics](#basics)
2. [Java Objects](#objects)
3. [The Thing About Strings](#the-thing-about-strings)
4. [Feeling Loopy with Java](#loops)
5. [Arrays](#arrays)
6. [Inheritance](# Inheritance)


## Java Basics <a name="basics"></a>
### Getting Started with Java
#### Introductiont to the tools

Every Java program has some setup that needs to happen
```java
import java.io.Console;
 
public class Introductions {
  
    public static void main(String[] args) {

        // This line below, reates a Java object, which has a method
        // that allows us to write out text to the terminal 
        Console console = System.console();
         console.printf("Hello, my name is Sheila");
  }
}

```
Java is a compile language, which means that we have to run a compiler program to make it readable for the machine. Therefore  we run `javac nameOfFile.java` this will convert or file into an executable one and you'll have a new file named `nameOfFile.class`, now we can run or program by writing `java nameofFile` and you'll print the message in your terminal.

#### Strings and Variables
A **variable** is a way to store data into a named location that you can use to reference later In Java, you mst specify what data type you're planning on storing so it know how to store that information
```java
import java.io.Console;
 
public class Introductions {
  
    public static void main(String[] args) {
        Console console = System.console();
        String firstName ="Sheila";
        console.printf("Hello, my name is Sheila\n");  //\n are scaped characters
        console.printf("Sheila is learning how to write Java\n"); 
     
  }
} 
```
- The `printF` method prints Formated text. It takes multiple options or parameters. The first parameter is the *format string*. When using methods, you can add additional parameters by separating them with a coma. Those additonal parameters are used to replace the format specifiers 
- You need to define the type of a variable first
- Use camelCase for variables in Java

```java
import java.io.Console;
 
public class Introductions {
  
    public static void main(String[] args) {
        Console console = System.console();
      
        String firstName = "Momo";
        console.printf("Hello, my name is %s\n", firstName);  //\n are scaped characters
        console.printf("%s is learning how to write Java\n", firstName); 
     
  }
} 

```



[Escaped Sequences](https://docs.oracle.com/javase/tutorial/java/data/characters.html)
[Data Types](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html)

#### Receiving Input
The `readline` method prints text out, and then captures whatever the user types afterwards, so it can be used to prompt the user for their name and the capture what the type. So the `readline` method give us a string or in other words returns a value 
```java
import java.io.Console;
 
public class Introductions {
  
    public static void main(String[] args) {
        Console console = System.console();
        //Create a string variable
        String firstName = console.readLine("What is your name? ");
      
        console.printf("Hello, my name is %s\n", firstName);  //\n are scaped characters
        console.printf("%s is learning how to write Java\n", firstName); 
     
  }
} 
```
Now, the program can dynamically change base on inpu from the user.This combination of Input and Output is often referred as **IO**

If you look at the top of the file, we're importing the console type from the *java.io** package. Java packages are used o bundle related functionality and programs

### Using your New Tools
#### Multiple Strings
```java
import java.io.Console;
 
public class TreeStory {
    
    public static void main(String[] args) {
        Console console = System.console();
        /* 
            THIS IS AN EXAMPLE OF A MULTILINE COMMENT

            Some terms:
            noun - Person, place or thing
            verb - An action
            adjective - A description used to modify or describe a noun
            Enter your amazing code here!
        */
      String name = console.readLine("Enter your name:  ");
      String adj = console.readLine("Enter an adjective:  ");
      
      console.printf("%s is very %s", name, adj);
      
    }
    
}
```
Also you can run both commands in the terminal, they will run in order until one fails:
```
javac TreeStory.java && java TreeStory
```
#### Coding the Prototypes
Madlibs Prototype
```java
import java.io.Console;
 
public class TreeStory {
    
    public static void main(String[] args) {
        Console console = System.console();
        /*  Some terms:
            noun - Person, place or thing
            verb - An action
            adjective - A description used to modify or describe a noun
            Enter your amazing code here!
        */
      
      //__Name is a __adjective__ __noun__.They are always __adverb__ __verb__.

      int age = 12;

      
      String name = console.readLine("Enter a name:  ");
      String adjective = console.readLine("Enter an adjective:  ");
      String noun = console.readLine("Enter a noun:  ");
      String adverb = console.readLine("Enter an adverb:  ");
      String verb = console.readLine("Enter a verb ending in -ing:  ");
      
      console.printf("Your TreeStory: \n --------------\n");
      console.printf("%s is a %s %s.", name, adjective, noun);
      console.printf("They are always %s %s.\n", adverb, verb); 

    }
    
}
```
After testing our code, we might notice some errors that are not syntax errors, but more about the logic like if we input the following data and received this:
```
Marco is a cool husband. They are always handome programming
```
Since these types of errors can only be found when the program is running, they are called **runtime errors**

### Perfecting the Prototype
#### Reviewing Ou feedback
We'll add an age restriction with a condition to our madLips program

```java
int age = 12;
      if(age < 13){
        //insert exit code
        console.printf("Sorry you must be at least 13 to use this program.\n");
        System.exit(0);
      }
```
The global system object has a method whcih is called `exit`, which causes the program to exit. The `exit` method takes an argument for the status code, which zero means that the system exited intentionally, we had control of it. Any other non-zero value represents a status code that is use to state that exited abnormally.

When a data type is lowecase like is the case of`int` it means is a special type of data type called **Primitive** data types that come out of the box with Java:
* int
* double
* long
* byte
* char
* float
* short
* boolean
All other non-primitive data types are called **object data types**

#### Parsing Integers
```java

      
      String ageAsString = console.readLine("How old are you?  ");
      int age = Integer.parseInt(ageAsString); // parse string to Int
      if(age < 13){
        //insert exit code
        console.printf("Sorry you must be at least 13 to use this program.\n");
        System.exit(0);
      }
```
Parsing is also referred to as converting a string to an integer. Switching between types is often called **casting**
`Integer.parseInt` classes static method to generate a primitive `int`. This `Integer` is what is know as a **wrapper type** or a **boxed type** that provides some methods that we can use to manipulate and produce integers, so primitives doesn't have methods, but they do have wrapper types.

#### Censoring Words - Using String equality

```java
String name = console.readLine("Enter a name:  ");
      String adjective = console.readLine("Enter an adjective:  ");
      String noun = console.readLine("Enter a noun:  ");
      if(noun.equalsIgnoreCase("dork") ||
          noun.equalsIgnoreCase("jerk")){
          console.printf("That language is not allowed. Exiting \n\n");
          System.exit(0);
      }
```


[String data type](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html)

#### Censoring Words Using Logical ORs
We can check multiple conditions by using what is know as logical or expression
[Relational Operators](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/op2.html)

#### Looping until the value passes
In the example below, we would get an error because the `noun` variabled used to create the output only exist inside the scope of the loop
```java
import java.io.Console;
 
public class TreeStory {
    
    public static void main(String[] args) {
        Console console = System.console();
        /*  Some terms:
            noun - Person, place or thing
            verb - An action
            adjective - A description used to modify or describe a noun
            Enter your amazing code here!
        */
      
      //__Name is a __adjective__ __noun__.They are always __adverb__ __verb__.
      
      String ageAsString = console.readLine("How old are you?  ");
      int age = Integer.parseInt(ageAsString); // parse string to Int
      if(age < 13){
        //insert exit code
        console.printf("Sorry you must be at least 13 to use this program.\n");
        System.exit(0);
      }
      
      String name = console.readLine("Enter a name:  ");
      String adjective = console.readLine("Enter an adjective:  ");
      //do while loop
      do{
         String noun = console.readLine("Enter a noun:  ");
         if(noun.equalsIgnoreCase("dork") ||
            noun.equalsIgnoreCase("jerk")){
            console.printf("That language is not allowed. Try again \n\n"); 
        }
      } while(noun.equalsIgnoreCase("dork") || noun.equalsIgnoreCase("jerk"));
      
      
      String adverb = console.readLine("Enter an adverb:  ");
      String verb = console.readLine("Enter a verb ending in -ing:  ");
      
      console.printf("Your TreeStory: \n --------------\n");
      console.printf("%s is a %s %s.", name, adjective, noun);
      console.printf("They are always %s %s.\n", adverb, verb); 

    }
    
}

```
Therefore we need to create it outside of it and we can make cleaner code by defining a variable that will returm a boolean value


```java
String noun;
boolean isInvalidWord;
      //do while loop
      do{
         noun = console.readLine("Enter a noun:  ");
         isInvalidWord = noun.equalsIgnoreCase("dork") ||
            noun.equalsIgnoreCase("jerk");
         
        if(isInvalidWord){
            console.printf("That language is not allowed. Try again \n\n"); 
        }
      } while(isInvalidWord);
      
```

## Java Object <a name="objects"></a>
### Meet Objects
#### Welcome Back
Jshell is the Java REPL
ctrl + L clears the screen
tab   Autoflling
`.toLowerCase().contains()` methods chaining
ctrl + d exits the REPL

#### Creating Classes
Objects and software allow us to express and model things that we have and use in real life. Programmers have discovered that all real world objects share 2 important characteristics: they have *state and behavior*. By creating an object in cde that maintains its own state and presents its behavior for usage it allows us to hide how things are actually working from users of your object

The blueprint used to create objects in Jaca is called a **class**

So far be have being using the `java.io` console object before to take input and write out to the screen, but there is another way called `System.out`. Console is actually convenient wrappers around system out and system in.

System is a class that's automatically imported writes a system and it provides a static public field named `out`. Out is a print stream and it exposes some methods that we've seen before on the console object

*PezDispenser.java*
```java

class PezDispenser{
// This block of code is the class scope
  
  //This is a field or a member of variable
  String characterName = "Yoda";

}

```
*Example.java*
```java
public class Example {
 
  public static void main(String[] args) {
    // Your amazing code goes here...
    //print.ln or print lne
    System.out.println("We are making a new PEZ Dispenser");
    
    //Here we create an instance of type Pez Dispenser
    PezDispenser dispenser = new PezDispenser();
    System.out.printf("The dispenser is %s %n", 
                       dispenser.characterName);
  }
}

```
This will also create a new file named `PezDispenser.java`

Strangely, we can change the name of the character Name
```java
public class Example {
 
  public static void main(String[] args) {
    // Your amazing code goes here...
    //print.ln or print lne
    System.out.println("We are making a new PEZ Dispenser");
    
    //Here we create an instance of type Pez Dispenser
    PezDispenser dispenser = new PezDispenser();
    dispenser.characterName = "Darth Vader";
    System.out.printf("The dispenser is %s %n", 
              
                       dispenser.characterName);
  }
}

```
#### Access Level Modifiers
We never want people to misuse the oject that we allow them to create. We should mak it as clear as possible to consumers of our class how we intend them to use it.

So in order to communicate how you intend people to use your objects, you can add some addtional qualifications to your statements. In Java these are called **access level modifiers** there are keywords that you can add your field definition to furher specify who is intended to access the information.

In orderto ensure that cde in the same folder cannot access our field, we're gonna used the `private` modifier.

```java
class PezDispenser{
// This block of code is the class scope
  
  private String characterName = "Yoda";

}
```
Now our code won't compile and throw an error, showing that's not even accesing the value. This kind of hiding is used for very deliberate purposes. This is called **encapsulation**

#### Methods
*Fields* usually are used to express `state` and its methods help us t express *behavior*, so you can think of fields as characteristics of the object and methods as the verbs or actions that your object can perform 
PezDispenser.java
```java
class PezDispenser{
// This block of code is the class scope
  private String characterName = "Yoda";
  
  //String.contains
  //public boolean contains (Strings matchingText)
  public String getCharacterName(){
    //return a value of its expected type which is a String
    return characterName;
  
  }

}
```
Example.java
```java
public class Example {
 
  public static void main(String[] args) {
    // Your amazing code goes here...
    //print.ln or print lne
    System.out.println("We are making a new PEZ Dispenser");
    
    //Here we create an instance of type Pez Dispenser
    PezDispenser dispenser = new PezDispenser();
    System.out.printf("The dispenser is %s %n", 
                       dispenser.getCharacterName()
                     );
  }
}
```

The prefexi of `get` is a very common pattern. It's a getter. So methods that are used to change the state of these objects or set a field value are prefixed with *set* or *get*. These are called properties in other languages



[Controlling Acess to Members of a Class](https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html)

#### Constructor
A constructor is a method that will run when you instantiate the class. Instantiation happens when you create the new instance of the class using the new keyboard. A contructor is a great place to stick required information aboot the initial set up o the object
```java
class PezDispenser{
// This block of code is the class scope
  private String characterName;
  
  public PezDispenser(String name){
    characterName = name;
  }
 
  public String getCharacterName(){
    //return a value of its expected type which is a String
    return characterName;
  
  }

}
```

If no contructors are defined a default contructor that takes no parameters is automatically assumed, which is why our previous exercised worked.However, when at least one constructor is defined, you must use one of those explicitly defined constructors

We know is a **constructor** because it has the same name as the class.

But if you notice inside the constructor parameters we pased `name` instead of `characterName` in order to avoid **naming collision**, but we can solve this with the word `this`

```java
class PezDispenser{
// This block of code is the class scope
  private String characterName;
  
  public PezDispenser(String characterName){
    this.characterName = characterName;
  }
 
  public String getCharacterName(){
    //return a value of its expected type which is a String
    return characterName;
  
  }

}
```
There is also the way they do it in Android, but you should follow the code style of your team
```java
class PezDispenser{
// This block of code is the class scope
  private String mCharacterName;
  
  public PezDispenser(String characterName){
    mCharacterName = characterName;
  }
 
  public String getCharacterName(){
    //return a value of its expected type which is a String
    return mCharacterName;
  
  }

}\
```

#### Final
When you want a variable to be assigned once and ony once, you mark it with the `final` keyword
```java
class PezDispenser{
// This block of code is the class scope
  final private String characterName;
  
  public PezDispenser(String characterName){
    this.characterName = characterName;
  }
 
  public String getCharacterName(){
    //return a value of its expected type which is a String
    return characterName;
  
  }

}
```
You can use the final kewyword not only for fields, but for methods and classes.


### Harnessing the Power of Objects
#### Constants
Values that do not change are often referred to as **constants**. A namin conventin that helps explain that a variable is a constant is to make all letters uppercase and separate the words with and underscore.

jshell allows you to open classes which is pretty cool. So to open your code you just do a `/open NameOfClassFile.java` 
```java
class PezDispenser{
  public static final int MAX_PEZ = 12;
  

  final private String characterName;
  
  public PezDispenser(String characterName){
    this.characterName = characterName;
  }
 
  public String getCharacterName(){
    //return a value of its expected type which is a String
    return characterName;
  
  }

}
```

Now, if we look at the box type `Integer` we would notice that it comes with some methods, such as `Integer.MAX_VALUE` but can we do that for our PezDispenser at the level class and not on the instance.
```jshell
PezDispenser.MAX_PEZ
 Error:
 non-static vaiable MAX_PEX cannot be referenced from a static context.


```
This can be solved with the keyword `static`.
There asre sometimes also referred to as class level variables because you can access them at the class leve, as opposed to the instance. The class level is calle the `static context` versus the instance context. Te word static actually refers to how the variable itself is stored in Memory, this allows to provide variables and methods directly off your class as opposed to having them on the instance.


```java
class PezDispenser{
  public static final int MAX_PEZ = 12;
  

  final private String characterName;
  
  public PezDispenser(String characterName){
    this.characterName = characterName;
  }
 
  public String getCharacterName(){
    //return a value of its expected type which is a String
    return characterName;
  
  }

}
```
```java
public class Example {
 
  public static void main(String[] args) {
    // Your amazing code goes here...
    //print.ln or print lne
    System.out.println("We are making a new PEZ Dispenser");
    System.out.printf("FUN FACT: There are %d PEZ allowed in every dispenser", PezDispenser.MAX_PEZ);
    //Here we create an instance of type Pez Dispenser
    PezDispenser dispenser = new PezDispenser("Donatello");
    System.out.printf("The dispenser is %s %n", 
                       dispenser.getCharacterName()
                     );
  }
}
```
#### Filling the Dispenser
Thinking through these limits is always a good practice.
We wanns store a state, how many PEZ are actually in the dispenser and if you're not sure if this should be public or private, always start with `Private` switch to `public` when you have a need

So we'll initialize `pezCount` and add it to our constructor, without the word `this` because is not talking about the same Count.

Then we'll create a method `fill` that is somethig that we want to expose and shouldn't return anything, so we're going to mark it as `void`
```java
class PezDispenser{
  public static final int MAX_PEZ = 12;
  final private String characterName;
  private int pezCount;
  
  public PezDispenser(String characterName){
    this.characterName = characterName;
    pezCount = 0;
  }
  
  public void fill(){
    pezCount = MAX_PEZ; 
  }
 
  public
  public String getCharacterName(){
    //return a value of its expected type which is a String
    return characterName;
  
  }

}
```
```java
public class Example {
 
  public static void main(String[] args) {
    // Your amazing code goes here...
    //print.ln or print lne
    System.out.println("We are making a new PEZ Dispenser");
    System.out.printf("FUN FACT: There are %d PEZ allowed in every dispenser %n", PezDispenser.MAX_PEZ);
    //Here we create an instance of type Pez Dispenser
    PezDispenser dispenser = new PezDispenser("Donatello");
    System.out.printf("The dispenser is %s %n", 
                       dispenser.getCharacterName()
                     );
    System.out.printf("Filling the dispenser with delicious Pez...");
    dispenser.fill();
  }
}
```
#### Abstraction at Play
One nice thing that we can do as proactive developers, is to add methods that provide functionality or information that we expect might be a common question about our object. By gathering common functionality, we can help to reduce code duplication for ourselves, and for consumers of our code.
We can use methods to provide conceptal state about our instance that other developers, and us included don't actually need to worry about when using the object

```java
class PezDispenser{
  public static final int MAX_PEZ = 12;
  final private String characterName;
  private int pezCount;
  
  public PezDispenser(String characterName){
    this.characterName = characterName;
    pezCount = 0;
  }
  
  public void fill(){
    pezCount = MAX_PEZ; 
  }
  
  public boolean isEmpty(){
    return pezCount == 0;
   
  }
 
  public String getCharacterName(){
    //return a value of its expected type which is a String
    return characterName;
  
  }

}

```

```java
public class Example {
 
  public static void main(String[] args) {

    System.out.println("We are making a new PEZ Dispenser");

    System.out.printf("FUN FACT: There are %d PEZ allowed in every dispenser %n", PezDispenser.MAX_PEZ);
    //Here we create an instance of type Pez Dispenser

    PezDispenser dispenser = new PezDispenser("Mario");
    System.out.printf("The dispenser is %s %n", 
                       dispenser.getCharacterName()
                     );
    if(dispenser.isEmpty()){
      System.out.printf("Dispenser is Empty %n");
    }
    
    System.out.printf("Filling the dispenser with delicious Pez...%n");
    dispenser.fill();
    
    if(!dispenser.isEmpty()){
      System.out.printf("Dispenser is full %n");
    }
    
  }
}

```
#### Incrementing and Decrementing
Since eerything can be modeled as an object, so **YAGNI** or "you ain't gonna need it". Not overengineer before you actually need it, also KISS (Keep it simple smarty pants?)
```java
//new method in our class
  public boolean dispense(){
    boolean wasDispensed = false;
    if(!isEmpty()){
      pezCount--;
      wasDispensed = true;
    }
    return wasDispensed;
  }
```

```java
//Check our pez is full and eat all of them
if(!dispenser.isEmpty()){
      System.out.println("Dispenser is full %n");
    }
    while(dispenser.dispense()){
      System.out.println("Chomp!");
    }
    if(dispenser.isEmpty()){
      System.out.println("Ate all the PEZ");
    }

```
#### Method Overloading
Overoading helps remove the need to come up with other method names that do similar things. You just use one method, but accept different arguments. So since are different methods, you can use it to assign default values.
So multiple methods, same name is **overloading**
```java
  public void fill(){
    fill(MAX_PEZ); 
  }
  
  public void fill(int pezAmount){
    pezCount += pezAmount;
  }
  
```

#### Exceptions
With exceptions is possible for us to tell the consumer that we're having problems with how they're using our object, or in other words we can let them know that an exceptional event has ocurred. Since we're dealing with a case where an argument that was passed into our method will actually break the object, we can use the **illegal argument exception**
```java
class PezDispenser{
  public static final int MAX_PEZ = 12;
  final private String characterName;
  private int pezCount;
  
  public PezDispenser(String characterName){
    this.characterName = characterName;
    pezCount = 0;
  }
  
  public void fill(){
    fill(MAX_PEZ); 
  }
  
  public void fill(int pezAmount){
    int newAmount = pezCount + pezAmount;
    if(newAmount > MAX_PEZ){
      throw new IllegalArgumentException("Too many PEZ!!");
    }
    pezCount = newAmount;
  }
  
  public boolean dispense(){
    boolean wasDispensed = false;
    if(!isEmpty()){
      pezCount--;
      wasDispensed = true;
    }
    return wasDispensed;
  }
  
  public boolean isEmpty(){
    return pezCount == 0;
   
  }
 
  public String getCharacterName(){
    //return a value of its expected type which is a String
    return characterName;
   
  }

} 
```
Now to avoid a ugly stack trace we use a `try..catch` block. The IllegalArgument Exceptions is another runtime exception, and thus we don't need to declare it at method level.

By anticipating how things might go wrong, we ca provide a stable, testable object that can easily integrate into exisiting products.

```java
public class Example {
 
  public static void main(String[] args) {

    System.out.println("We are making a new PEZ Dispenser");

    System.out.printf("FUN FACT: There are %d PEZ allowed in every dispenser %n", PezDispenser.MAX_PEZ);
    //Here we create an instance of type Pez Dispenser

    PezDispenser dispenser = new PezDispenser("Mario");
    System.out.printf("The dispenser is %s %n", 
                       dispenser.getCharacterName()
                     );
    if(dispenser.isEmpty()){
      System.out.printf("Dispenser is Empty %n");
    }
    
    System.out.printf("Filling the dispenser with delicious Pez...%n");
    dispenser.fill();
    
    if(!dispenser.isEmpty()){
      System.out.println("Dispenser is full %n");
    }
    while(dispenser.dispense()){
      System.out.println("Chomp!");
    }
    if(dispenser.isEmpty()){
      System.out.println("Ate all the PEZ");
    }
    dispenser.fill(4);
    dispenser.fill(2);
    while(dispenser.dispense()){
      System.out.println("More chomp!");
    }
    
    try{
      dispenser.fill(400);
    }catch(IllegalArgumentException iae){ //This will only catch those exceptions
      System.out.println("Whoa there!");
      System.out.printf("The error was %s", iae.getMessage());
    }
    
    
  }
}
```
## The Thing about Strings <a name="the-thing-about-strings"></a>
This little program below, is gonna help us explore some concepts about strings
We have a method called `explore` and it takes an `assumption` about what we are going to be exploring and an expression. The expression is expected to always be true. It'll generate a `result` letting us know if we're correct

When you create a string, `"like this"` we're creating what is know as a **string literal**, and since strings are immutable, the compiler does some tricks to optimize. Since it knows the string won't change, just creates a single instance of that string and makes all variables refer to that single instance. It keeps these special references in a special place in memory called the **string pool**

One fina trick that you might see used is a process called **string interning**. You can actually take a user inpted strin an add it to the same string pool, and you do that by using a method on strings called **intern**

```java 
public class Thing {
  public static final String ANSI_RESET = "\u001B[0m";
  public static final String ANSI_RED = "\u001B[31m";
  public static final String ANSI_GREEN = "\u001B[32m";
  
  public static void explore(String assumption,
                             boolean result) {
    StringBuilder sb = new StringBuilder();
    if (result) {
      sb.append(String.format("%sYAY!%s", 
                             ANSI_GREEN, 
                             ANSI_RESET));
    } else {
      sb.append(String.format("%sWAT???!%s",
                             ANSI_RED,
                             ANSI_RESET));
    }
    sb.append("  ");
    sb.append(assumption);
    if (!result) {
      sb.append(" (Your assumption is incorrect)");
    }
    System.out.println(sb.toString());
 }
  
  public static void main(String[] args) {
    // First Assumptions
    int firstNumber =12;
    int secondNumber= 12;
    explore("Primitives use double equals",
           firstNumber == secondNumber); //Console: YAY! Primitives use double equals
    
    //Second Assumption
    Object firstObject = new Object();
    Object secondObject = new Object();
    explore("Object references  work just like primitives",
            firstObject == secondObject); //Console: WAT!! Objects work just like primitives(Your assupmtion is incorrect)
    Object sameObject = firstObject;
    explore("Object references must refer to the same object to use double equals", 
           firstObject == sameObject);//YAY! Object references must refer to the same object to use double equals 
    
    //Third Assumption
    String firstString = "Craig";
    String secondString= "Craig";
    explore("Strings are objects and work like objects", 
           firstString != secondString);// WAT??! ..(Your assumption is incorrect)
    explore("Strings literals are actually referring to the same object", 
           firstString == secondString);// WAT??! ..(Your assumption is incorrect)
    
    String differentString = new String("Craig");
    explore("String objects that contain the same characters but point to different objects cannot use double equals", 
          firstString != differentString);
    
    String anotherString = new String("Craig");
    explore("String interning add to the same String Pool where literals live, so you get back the same reference",
           anotherString.intern() == firstString); //YAY
     
    explore("All objects should use equals to check equality", 
           firstString.equals(differentString));  //YAY, All objects should use equals to check equality
    
  }
} 
```
## Feeling Loopy with Java <a name="loops"></a>
*While Loops* ar commonly used when you have an unknown number of times of iterations to perform. java provides both a pre-check as well as a post-check style
Pre-check offers the ability to actually never loop

Pseudo-code
```
anyQuestions = ask "Are there any questions?"
while anyQuestions
    answer question
    anyQuestion = ask "any more questions?
next slide
```
```java
import java.io.Console;

public class Questions {
  public static void main(String[] args){
    Console console = System.console();

    String anyQuestions = console.readLine("Are there any questions?  ");

    while(anyQuestions.equals("yes")){
      String question = console.readLine("Whats is your question?  ");
      console.printf("I do not understand: %s", question);
      anyQuestions = console.readLine("Are there any more questions");
    }
    console.printf("Next slide...");
  }

}
```
*Do while Loops*
1. Same concept as the while loop, yo do not know how many iterations it will take
2. It foes a post check
3. Useful when you want to ensure the loop does a minimum of one iteration

Pseudo- Code
```
do
  ballInHole = puttPutt
  until ballInHole
```
```java
int numberOfPutts = 0;
boolean ballInHole = false;

do {
  console.printf("Putt putt %n");
  ballInHole = luck.nextBoolean();
  numberPutts++;
} while(!ballInHole);

console.

```



## Java Arrays <a name="arrays"></a>
### Creation
#### Meet and Declaring Arrays
Arrays are container objects that can be used to store multiple values
All elements if that array have to be of the same type

The java language does a really great job of abstracting a way your need to think about how all these variables that we're creating are stored in the computer memory. Wen you declare a variable and specify its type what Java actually does for you is to reserve a spot in memory for you that is big enough to store your data on initialization.

java needs to know how many elements your array is going to have when it's created, so it can go a reserve the right amount of memory.

Note: When you declare an object and you do not initialize its value, it defaults to `null`. Primitive data dafaults like `int` and `bool` have different defaul values.

```java
//jshell

String[] friends = new String[3];
// friends ==> String[3]{null, null, null}

```
In the example above, all elements in the array have been defaulted to null.

#### Accesing Items
Java is 0 based
```java
friends[0]="Pasan";
Systems.out.println(friends[0] + " is awesome!"); //Pasan is awesome
//You can also use expressions
friends[friends.length - 3] // Pasan
```
#### Array Litearal Shortcut
When you know the values of all the elements in an array, you should use an Array literal

String[] friends = {"Pasan", "Alena", "Ben"};


### Iteration
#### Enhanced For Loop
```java
public class Explore {
 
  public static void main(String[] args) {
    //Create a new friends aray  
    String[] friends = {"Ben", "Alena", "Pasan"};
    
    //Enhanced for loop
    for(String friend: friends){
      System.out.printf("Hey %s! The movie starts at 7, C U there! %n", friend);
    
    }
  }  
}
//Hey Be! The movie starts at 7, C U there!...
```
#### Ye Olde Unenhanced Loop
```java
// initialize expression, then set the condition, finally the increment or after thought
for(int i = 0; i< friends.length; i++ ) {
  String friend = friend[i];
  System.out.printf("Hey %s! The movie starts at 7, C U there! %n", friend);

}
```
Exercise

The `%d` specifies that the single variable is a decimal integer. The %n is a platform-independent newline character.

```java
public class Programmers {

  public void printMenu() {
    String[] programmers = {
            "Yukihiro Matsumoto",
            "David Nolen",
            "Grace Hopper",
            "Linus Torvalds",
            "You"
    };

    System.out.println("Choose a programmer:");
    for(int i=0; i<programmers.length;i++){
      System.out.printf(" %d. %s%n ",i+1,programmers[i]);
    }

    // TODO: Print out a menu by looping through the programmers array.
    /*
      The menu should be in the form of (each on a line of its own, starting with 1):
      1. Yukihiro Matsumoto
      2. David Nolen
      ...
    */
  }
}
```
#### Multidimentional Arrays
2D arrays are super handy at helping describe things in rows and columns
```java
int[][] scoreCards ={
{1, 2, 4, 2, 6, 5, 4, 3, 3, 2, 5, 7, 2, 7, 8, 4, 3, 2},
{2, 3, 5, 1, 1, 2, 3, 1, 1, 2, 4, 1, 3, 3, 2, 6, 3, 2},
{4, 4, 2, 1, 2, 2, 1, 4, 2, 2, 2, 3, 2, 5, 8, 1, 2, 2}  
}; 
```
### Looping Over 2D Array
```java
public class Explore {
 
  public static void main(String[] args) {
    //Create a new friends aray  
    String[] friends = {"Ben", "Alena", "Pasan"};
    
    int[][] scoreCards ={
      {1, 2, 4, 2, 6, 5, 4, 3, 3, 2, 5, 7, 2, 7, 8, 4, 3, 2},
      {2, 3, 5, 1, 1, 2, 3, 1, 1, 2, 4, 1, 3, 3, 2, 6, 3, 2},
      {4, 4, 2, 1, 2, 2, 1, 4, 2, 2, 2, 3, 2, 5, 8, 1, 2, 2}  
    };
    
    //for each friend
    //print their name
        //for each hole print score  
    for(int i = 0; i < friends.length; i++){
      System.out.printf("%s %n -----------------%n", friends[i]);
      for(int j= 0; j <scoreCards[i].length; j++ ){
        System.out.printf("Hole#%d: %d %n", j+1, scoreCards[i][j]);
      }
    }
         
    }
  } 
  /*
  Example of what this loop returns:
  Alena                                                
 -----------------                                    
Hole#1:2                                              
Hole#2:3                                               
*/
```
### Gotchas and Wins
#### Adding and Removing Items Means Copying
The lenght of an array is inmmutable, so we have an starting array in our `scratch.java file`
```java
String[] friends = {"Ben", "Alena", "Pasan"};
```
And opent it on Jshell, and in Jshell we initialize a new array with the new number of elements that we want
```shell
String[] friendsAndMe = new String[4];
```
This of course will default all elements to `null` . So now we want to copy all of the elements of the original array into this new one.

*Note: After double tab after a signature jshell is going to give you help about it, like the arguments it accepts:
`Systems.arraycopY(Object src, int srcPos, Object dest...`*

```shell
System.arraycopy(friends, 0, friendsAndMe, 0, friends.length)
// This will return:
// friendsAndMe ==> String[4]{"Ben", "Alena", "Pasan", null}
```
So now we can add the new member:
```java
friendsAndMe[3]="Craig";
```
There is another approach, with a helper class which provides a lot of helpful methods, but we need to import it to use it.
There is also a static helper method of this class called copy of, and makes a copy of your Array
```java
//Still in jshell
import java.util.Arrays
String[] friendsAndMe2 = Arrays.copyOf(friends, friends.length + 1)

```
As the old saying says: "If it hurst when you do that, don't do that". When using arrays, you actually very rarely ever doa ny adding or removing of elements, this is because in practice, there is another data structure that is known as a *list*. It is intended for dynamically adding and removing values
[Using Packages](https://docs.oracle.com/javase/tutorial/java/package/usepkgs.html)
[List Implementations](https://docs.oracle.com/javase/tutorial/collections/implementations/list.html)

#### Sorting
In addition to copying, the arrays utility class also lets you sort an array
```java
import java.util.Array;

String[] friends = {
  "Treasure",
  "Ben", 
  "Alena", 
  "Pasan",
  "Craig"
  };
```
Now in we open the file in jshell and do `Arrays.sort(friends)` we'll get an Array with everyone in alplhabetical order. This modifies the array.

You can sort an array of any object as long as that objects marks itself as being comparable and provides a methods called `comparedTo` that retursns these same values.
 
```
"Apple".compareTo("Banana") // -1
```
The way this works is if the item on the left is less than the item on the right it returns a negative number. If it's equal it returns zero. So the array sort method uses this on each element in our array until it's in the correct order.


If you don't want to `sort` like that this methods takes a second parameter whichs is of type comparator, first you import the `java.util.Comparator`. The methods's parameter expect yo to define how to get the value that is to be compared. The Comparator class has a static method named `comaparing` that will return a new comparator. The method's parameter expects you to define how to get the value that is to be compared, so we can use a **method reference**. We know that our elements in our friends array are all strings and all strings have the `.length` method
```
Arrays.sort(friends, Comparator.comparing(String::length));
Arrays.sort(friends, Comparator.comparing(String::length).reversed());
```
##### Array Usage in Method Declarations
When you declare your methods you have a couple of options to help users of your program, or API undertand what you're expecting. Now aside form the ypical `type` declaration, there is a clear pattern. In the standard boilerplate java program. You can see what looks like to declare a method that expects an array

Like our example that is defining an array named `args`
```terminal
jshell> char[] letters = "treehouse".toCharArray();                        
letters ==> char[9] { 't', 'r', 'e', 'e', 'h', 'o', 'u', 's', 'e' } 
shell> Arrays.sort(letters)                                               
                                                           
jshell> letters                                                            
letters ==> char[9] { 'e', 'e', 'e', 'h', 'o', 'r', 's', 't', 'u' }   

```
jshell let's you create methods wherever, so we'll use it lo learn about  `varargs`, whichs allows user to provide zero or more of this type of variable.
Radom is another utility that comes with another great method named `next int` that gets an integer between zero and some upper bound, which is perfect because arrays start at zero and the random number will go up and tell the number that you specify, which is pretty perfect for choosing a random array index. And it excludes the tip number

## Inheritance in Java <a name="inheritance"></a>
### Introducing Inheritance
**Inheritance** is a class using another class as its foundation 

- Typically we put each class i its own file.
- While you can have moe than one class in a file, all public classes need their own files, which is why we're not making our class `public`
```java
public class Main {
    public static void main(String[] args) {

        Dog dog = new Dog();
        dog.makeSound();

    }
}
 class Animal {
    //String field
    String sound = "";

    void makeSound(){
        System.out.println(sound);
    }
}
class Dog extends Animal {
    Dog(){
        sound = "bark";
    }
}

```