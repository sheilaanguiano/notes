# Java Tutorial for Beginners
-----

Author: Sheila Anguiano
Course: Java Tutorial for Beginners
Instructor: Bro Code Channel

-----

# Table of Contents

1.  [Java Tutorial for beginners](#java-beginner)

15. [Java Arrays](#arrays)
16. [Java 2D arrays](#2d-arrays)
17. [Java String Methods](#string-methods)
18. [Java Wrapper Classes](#wrapper-classes)
21. [Java for-each Loop](#for-each-loop)
22. [Java Methods](#java-methods)
23. [Java Overloaded Methods](#overloaded-methods)



## Java Tutorial for Beginners <a name="java-begginer"></a>
Computer languages are on a spectrum between being low level or High-level. Computers only understand  binary which is a low-level language referred **machine code**.
To create machine code, we write in a format called **source code** which is undertsandable by humans and then is **compiled** (transalated) to machine code. 

When we create java code the file ends with `.java` extension. When we compile our source code to machine code it's machine specific, but java has a solution for this problem, an intermediary step where we can compile our source code into `bytecode`. Bytecode is cross platforma dn ends with a `.class` file extension.

To read the bytecode, the machine uses a **JVM** (Java Virtual Machine) to translate the bytecode to machine code. You het a JVM with a **JDK** (Java Development  Kit) which contains development tools as well as a **JRE** (Java Runtime Enviroment) which contains a library, toolkits and the JVM which transaltes java bytecode to our machine specific machine code.

CONTINUE FROM 8:21MIN

## How to Swap 2 Variables<a name ="swap-variables"></a>


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
## Final Keyword <a name ="final"></a>
## Java Objects <a name ="objects"></a>