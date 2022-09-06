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
6. [Inheritance](#inheritance)
7. [Interfaces](#interfaces)
8. [Generics](#generics)
9. [Java Lists](#list)
10. [Java Maps](#maps)


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

### Everything inherits from Object
When thinking about Inheritance think of **IS** a Dog is an Animal. And everything in Java IS an OBJECT

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
So we can declare Dog as `Animal dog = new Dog()` or even as an object `Object dog = new dog();` but we'll lose the ability to call `makesound`, since the Object class doesn't have that method, luckly we can get our dog back by using something called **cast**
Now imagine that we create a list of Objects with a new Dog and New food
```java
public class Main {
    public static void main(String[] args) {

       Object[] list = {new Dog(), new DogFood()};
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
class DogFood{}
```
### Casting Instances
We just saw how we can group together different objects bu ysing an array with a common base class. 

If we create a new dog variable like the example bleow, it will give us an *incompatible error*

```java
public class Main { 
    public static voi d main(String[] args) {

       Object[] list = {new Dog(), new DogFood()};
       Dog dog = list[0];
        dog.makeSound();

    }
}

```
A cast or **type casting** is when you tell java that an object os a more specific descendant of that object. Essentially moving the object up its family tree. Tou use a cast, you just write the name of the class between parentheses. To write a cast, you just write it between parentheshis.  

 ```java
public class Main { 
    public static voi d main(String[] args) {

       Object[] list = {new Dog(), new DogFood()};
       Dog dog = (Dog)list[0];
        dog.makeSound();

    }
}
```
But if we try to merge those to lines an make something like below, won't work becyase the call to `.makeSound()` happens before the cast
 ```java
public class Main {  
    public static voi d main(String[] args) {

       Object[] list = {new Dog(), new DogFood()};
     
        (Dog)list[0].makeSound();

    }
}
```
So to make sure that the cast happens first, we just need to use some parenthesis.
 ```java
public class Main {  
    public static voi d main(String[] args) {

       Object[] list = {new Dog(), new DogFood()};
        ((Dog)list[0]).makeSound();

    }
}
```
Now this only works, because we know exactly whe our dog is in the array. So we can loop theough our list array and only call `makeSound` if the object actually has a `makesSeound` method. Using the `instaceof` operator allows us to checi if one object is an instance of another
```java
public class Main {
    public static void main(String[] args) {

       Object[] list = {new Dog(), new DogFood()};
       for (Object object: list){

           if(object instanceof Animal){
               ((Animal) object).makeSound();
           }
       }

    }
}
```
### Object Methods
If you look at the instance of one of your objects, you will see the fields and methods for the specific object (like the Dog objects), but also methods that come from class, some of this are:
* `getClass()` method: When you call the getClass method on an object, it returns a class object that contains information about the class itself, like the class name and what package it's in.
* `toString()` when you call it on an object. It returns a string with information about the object.
```java
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        System.out.println(dog.toString());
     }
}
//This returns     Dog@28a418fc

```
In IntelliJ whenever you want to take a deeoer look at something, you just put your cursor on it and use `cmd +B` to jump to its declaration 

* `.hashCode()` when you call this method on an object, you get back an integer representing that object, and the important thing to remember about this, it that it'll return a different integer for every object, so is helpful when checking equality.
* `.equals` a method that returns a boolean indicating if the two object are equal

### Super Override
In Java an override is when a child class has a method with the exact same signature as one in the parent class, but with a different implementation, for example we'll create a `toString` method in our animal class that will have a different implementation, that the one that comes from `Object`.
```java
 class Animal {
    //String field
    String sound = "";

    void makeSound(){
        System.out.println(sound);
    }
    @Override
    public String toString(){
        return getClass().getSimpleName() + ": sound = " + sound;
    } 
}
// Dog: sound = bark 
``` 
The `@Override` annotation isn't strictly required, but it lets Java know that we're attempting to override an already existing method. Now there is another way we could have done this: `ctrl + O ` opens the override menu, pick up the `toString()` method and accept it, returning the following
```java
  @Override
     public String toString() {
         return super.toString();
     }
```
`super` keywbord refres to the parent class, meaning this is calling the `.toString()` method of the object class.

But, why do we need the `super` keyword. Let's say that every time a dog makes a sound , it should also wag its tail. To do this, we'll need to override the makeSound method in our dog class.
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

     @Override
     public String toString() {
         return getClass().getSimpleName() + ": sound = " + sound;
     }
 }
class Dog extends Animal {
    Dog(){
        sound = "bark";
    }

    @Override
    void makeSound() {
        super.makeSound();
        System.out.println("wags tails");
    } 
}
class DogFood{}

//bark
//wags tail
```
Now, when we call the `makeSound()` method on a Dog object, it'll first call animal make sound method and then print out wags tail

Another place, you might see the `super` keyword is in a constructor. Let's see how that works by making sure that every animal has a sound. We'll add a constructor to the animal class and making sure it takes on a string parameter
```java
 class Animal {
    //String field
    String sound = "";

    //constructor
    Animal(String sound){
        this.sound = sound;
    }

    void makeSound(){
        System.out.println(sound);
    }

     @Override
     public String toString() {
         return getClass().getSimpleName() + ": sound = " + sound;
     }
 }
```
This will give us an error in our Dog class, since Animal now requires a sound in its contructor, we need to call through to that constructor in order to have a valid animal
```java
class Dog extends Animal {
    Dog() {
        super("bark");
    }

    @Override
    void makeSound() {
        super.makeSound();
        System.out.println("wags tails");
    }
}
class DogFood{}
```
### Abstracting Abstract Classes
Inheritance is a powerful concept and it gives a huge amount of freedom with how we develop apps. However, someties, it makes sense to limit some of that freedom. Right now if we wanted to, we could create a new animal object, this might not seem like an issue, but what does a generic animal look like
**Abstract Classes**
I. Cannot be instantiated. You can't use the `new` keyword with an abstract class
II. Can have abstract methods, which are methods without a method body. You can think of them as pretty much a forced override.

We're gonna make our animal class abstract and maken an abstract method `.findfood()`, then we'll need to override that method in our dog class, luckily IntelliJ already know how to do this, so we can use (option + enter) to implement the method:
```java
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.findFood();
     }
}

 abstract class Animal {
    //String field
    String sound = "";

    Animal(String sound){
        this.sound = sound;
    }
    abstract void findFood();

    void makeSound(){
        System.out.println(sound);
    }

     @Override
     public String toString() {
         return getClass().getSimpleName() + ": sound = " + sound;
     }
 }
class Dog extends Animal {
    Dog() {
        super("bark");
    }

    @Override
    void findFood() {
        System.out.println("*looks at human*");
        makeSound();
    }

    @Override
    void makeSound() {
        super.makeSound();
        System.out.println("wags tails");
    }
}
class DogFood{}
/*
returns the following after compilation:
 *looks at human*
 bark
 wags tails
*/
```
### Object Equality
When talking about objects, there's typically two ways to think about equality. There is strict equality, which makes sure they're literally the same object and there's looks like equality, where as long as the two things have the same properties, then they are the same, which can be accomplished by overriding the equals and hash code methods.
```java
public class Main {
    public static void main(String[] args) {
        Dog dog1 = new Dog();
        Dog dog2 = new Dog();
        System.out.println(dog1.equals(dog2));

     }
}
// false
```
So now, we need to change our animal class so that the equality will be based only on the properties of the class, which, for us is just the sound property. To do this, we'll need to override the equals and hash code methods based on the sound property. However, this typically isn't done by hand, so let's use the shortcut, add some space at the bottom of the class and then hit `command + N` to bring up the generate dialog (IntelliJ), then pick up `equals() and jashCode()` and just keep hitting enter, now we can compile our code again:
```java
mport java.util.Objects;

public class Main {
    public static void main(String[] args) {
        Dog dog1 = new Dog();
        Dog dog2 = new Dog();
        System.out.println(dog1.equals(dog2));

     }
}

 abstract class Animal {
    //String field
    String sound = "";

    Animal(String sound){
        this.sound = sound;
    }
    abstract void findFood();

    void makeSound(){
        System.out.println(sound);
    }

     @Override
     public String toString() {
         return getClass().getSimpleName() + ": sound = " + sound;
     }
    //Autogenerated code by IntelliJ to override equals and hashCode
     @Override
     public boolean equals(Object o) {
         if (this == o) return true;
         if (o == null || getClass() != o.getClass()) return false;
         Animal animal = (Animal) o;
         return Objects.equals(sound, animal.sound);
     }

     @Override
     public int hashCode() {
         return Objects.hash(sound);
     }
 }
class Dog extends Animal {
    Dog() {
        super("bark");
    }

    @Override
    void findFood() {
        System.out.println("*looks at human*");
        makeSound();
    }

    @Override
    void makeSound() {
        super.makeSound();
        System.out.println("wags tails");
    }
}
class DogFood{}
// true
```
And with this, both are the same dog. Now if we want them to make different dogs, they'll need to make different sounds, thus we'll update the contructor to take in a sound
```java
...
class Dog extends Animal {
    Dog(String sound) {
        super(sound);
    }
...
```
And now we need to define different sound for our dogs, and if we run the code, they'll again no longer be the same dog
```java
public class Main {
    public static void main(String[] args) {
        Dog dog1 = new Dog("bark");
        Dog dog2 = new Dog("woof");
        System.out.println(dog1.equals(dog2));

     }
}
```


## Interfaces in Java <a name="interfaces"></a>
### Introducing Interfaces
You can think of interfaces just as a more restricted abstract class. When creating an interface you start with the `interface` keyword followed by a name. Inside an interface, there's really only two things you can do, you can
1. Declare a constant
2. Declare an abstract method

Since we're limited to just constants and abstarct methods inside an interface, we don't need to specify static final for our variables or abstract for our functions, it will just be that way by default. 

Once we created the interface, we associate it with a class by using the `implements` keyboard. Then since interface methods are abstract we need to override each of those methods in the class. This is one of the big advantages of interfaces, since thet can't contain any mentod implementations, it's impossible to run into the **diamond problem**. Which mean we should have no problem implementing from more than one interface

A good way to think about interfaces is as job postings for Objects, is a list of actions that an object has to do to get the job. For example, if we have Pilot interface with a `flyPlane()` method, then any object implementing that `flyPlane()` method will be able to get the job of Pilot. This gives us a ton of flexibility about who can be pilots (A human pilot, dog pilot, toaster pilot). Having the pilot's functionality in an interface instead of a class give us a lot more flexibility when writting our code. This principle is called **Composition over Inheritance**. When you're creaeting an application, rather than attaching functionality to a class and requiring it to be inherited, you should put that functionality into an interface and then create classes composing of the required interfaces.

Being able to separate out what something does versus how it does it gives us a lot more flexibility with writting our programs

## Generics in Java <a name="generics"></a>
<T> stands for a Type parameter


## Java Lists <a name="lists"></a>
A list is pretty much just a more flexible array, the items are indexed and we can access them by their index, we also get some helpful methods like:
* `.contains()` returns a boolean telling us if a list contains a certain item
* `.indexOf()`which searches the list for an item and returns the item, if it's found, or negative one if it's not

### Adding, Removing and Accesing
```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> groceryLine = new ArrayList<>();
        groceryLine.add("Jerome");
        groceryLine.add("Beth");
        groceryLine.add("Sam");
        System.out.println(groceryLine);
        groceryLine.remove("Beth");
        // groceryLine.remove(1) --> Will work the same as above
        System.out.println(groceryLine);

        String jerome = groceryLine.get(0);
        System.out.println(jerome);

    }
}
// [Jerome, Beth, Sam]
//[Jerome, Sam]
// Jerome
```
### The Rest
```java

int samIndex = groceryLine.indexOf("Sam");
System.out.println(samIndex);
//1

int pamIndex = groceryLine.indexOf("Pam"); // doesn't exist
System.out.println(pamIndex);
//-1
```
It's important to remember that `indexOf` starts from the beggining of the list, so if our list have two repetead items, it'll give us the index of the first one that it finds
* `.size()` is similar to `lenght()` but for Lists
* You can use Lists with a `for each loop`
```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> groceryLine = new ArrayList<>();
        groceryLine.add("Jerome");
        groceryLine.add("Beth");
        groceryLine.add("Sam");
        System.out.println(groceryLine);
        groceryLine.remove("Beth");
        // groceryLine.remove(1) --> Will work the same as above
        System.out.println(groceryLine);

        String jerome = groceryLine.get(0);
        System.out.println(jerome);

        int samIndex = groceryLine.indexOf("Sam");
        System.out.println(samIndex);
        System.out.println(groceryLine.size());
        for (String name: groceryLine){
            System.out.println(name);
        }

    }
}
```

## Java Maps <a name="maps"></a>
In Java a map is a data type that lest us store key value pairs. Our keys can be any type we'd like, which means when you create a map you not only need to specify a type.
- A map is an interface that takes in two type parameters, one for the key and one for the value.
- Since Map is an interface we won't be able to use it to create a new Map obkject. Instead we'll need to use a class that implements the map interface. It's just what we had to do with our lists except instead of using list and array list here we'll be using map and HashMap
```java
import java.util.HashMap;
import java.util.Map;

public class Main {
    public static void main(String[] args) {
        Map<String, String> meals = new HashMap<>();
        //Adding entries to the map
        meals.put("breakfast", "Waffles");
        meals.put("lunch","Gyros");
        meals.put("dinner","enchiladas");

        System.out.println(meals);
    }
}
// {lunch=Gyros, breakfast=Waffles, dinner=enchiladas}
```
### Map Basics
```java
import java.util.HashMap;
import java.util.Map;

public class Main {
    public static void main(String[] args) {
        Map<String, String> meals = new HashMap<>();
        //Adding entries to the map
        meals.put("breakfast", "Waffles");
        meals.put("lunch","Gyros");
        meals.put("dinner","enchiladas");

        System.out.println(meals);
        //Print only what's for dinner
        System.out.println(meals.get("dinner"));
        String lunch = meals.remove("lunch");
        boolean hasLunch= meals.containsKey("lunch");
        boolean hasGyros = meals.containsValue("Gyros");
        int size = meals.size();

        System.out.println(lunch + " " + hasLunch + " " + hasGyros + " " + size);
    }
}
// {lunch=Gyros, breakfast=Waffles, dinner=enchiladas}
// enchiladas
// Gyros false false 2

```
- Maps cannot have duplicate keys as it will just overwrite the previous value
- When you use strings as keys, you almost always want to be using constants, and intelliJ has a shortcut for creating string constants `psfs`

## Local Development Environments <a name="local-dev-env"></a>
### How it Works
#### Acronyms
* SDK - Software Development Kit - A grouping of tools that allow you to create software locally. Also some times referred to as devkits.
* JDK - Java SE Development Kit - A set of tools specifically for developing Java SE Applications
* Java SE - Standard Edition
* JRE - Java Runtime Environment - A minimum set of tools that allow local Java programs to execute
* Java SE API - Application Programming Interface - A set of libraries provided to build applications.
* JCL - Java Class Library - A synonym for the Java SE API. More info here.
* JVM - Java Virtual Machine - an abstract computing machine.
![JDK](https://i.stack.imgur.com/CBNux.png)
[JDK](https://docs.oracle.com/javase/8/docs/)

#### JVM 
When we run the `javac` command, we're converting the code we wrote into **Java bytecode**. Most compiled languages like C, require the user to take the source code and compile it for every specific environment, and this can be a very tedious and long process, so Java from its inceptions wanted to avoid this frustration, thus the **Java Virtual Machine**. 

Many advantages have been made in the JVM arena sicne the beginning of time, and it a lot of cases, due to a method known as just-in-time compiling, or JIT, each JVM can basically run code almost as fast as natively compiled code.
 
* WORA - Write Once Run Anywhere - Java can be compiled into bytecode and run on any device that has a JVM.
* JIT - Just In Time compilation - A final compilation step that converts bytecode to native machine code during runtime startup

[Java Bytecode](https://en.wikipedia.org/wiki/Java_bytecode)
[Unix Less Command](https://www.thegeekstuff.com/2010/02/unix-less-command-10-tips-for-effective-navigation/)


### Exploring your IDE
### Advanced Tooling