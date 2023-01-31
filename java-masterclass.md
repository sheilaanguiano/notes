# Java Programming Masterclass
-----

Author: Sheila Anguiano
Course: Java Masterclass(Udemy)
Instructor: Tim Buchalka

-----

# Table of Contents

1. [Programming Tools and Setup](#2)
2. [First Steps](#3)
3. [IntelliJ Basics](#4)
4. [Expressions, Statements, Codeblocks, Methods](#5)
5. [Control Flow](#6)
6. [Objtec Oriented Programming Part1 - Inheritance](#7)


## Section 2: Programming Tools and Setup <a name="2"></a>
### Confirming Installation and intro to JShell
* Check in your terminal your java version `java -version`
* IntelliJ is an integrated development environment or IDE to develop Java code.
* JShell became a standard component of the JDK (Java Development Kit) in Java9 it's a REPL.
* Launch jshell writting in the terminal `jshell`
    * `jshell>/help intro`
    * `/exit` to exit jshell


## Section 3: First Steps <a name="3"></a>
### Hello World
`jshell> System.out.print("Hello World");`

A **statement** is a complete command to be executed. It can include one or more **expressions**.

### Variables
* Keywords
* Java is case sensitive, `int` is not the same as `Int`
* **Variables** are a way to store information. Can be accessed by a name given to them and the computer makes the decision of where to store them in RAM (random access memory)
* **Data Type**: there are a lot of different types of data, some data types are keywords
* To define a variable, we need to specify the data type, give the variable a name and optionally add an expression, to initialize the variable with a value `int myFirstNumber = 5;`
* This statement `int myFirstNumber = 5;` is an specific kind of statement **Declaration statement**. A declaration statement is used to define a variable by indicating the data type, and the name, then optionally to set the variable to a specific value;
* JShell allows to redeclared variables, something not allowed in normal Java programming

### Starting out with Expressions
**Expression** is the code segment that is on the right side of the equals sign in an assigment or delcaration statement.
If you type `/var` in Jshell it will list all your declated variables and their values

### Primitive Types
In java, primitive types are the most basic data types:
**Whole Numbers**
- byte
- short
- int
- long
**Real Number (Floating point or decimal)**
- float
- double
**Single Character**
- char
**Boolean Value**
- boolean

Consider these types as the building blocs of data manipulation and that these are simply placeholders in memory for a value.

There's a specified range of values allowed for the int, which is true for most data types. What this means, is that the allowable range of values is NOT finite. There is a defined minimum, and maximum value for each data type.

You can get that min and max value programatically
```java
int myMinValue = Integer.MIN_VALUE;
int myMaxValue = Integer.MAX_VALUE;

System.out.print("Integer Minimum Value = " + myMinValue); //Using concatenation 
```
`int` is a primitive type that only gives us the option to set the varaible's value. `Integer` on the other hand, is what's called a **wrapper class**, but first we need to undertsand what's a class

A class is a building block for object oriented programming, and allows us to build custom data types. Java uses the concept of wrapper class, for all of its eight primitive data types. A warpper class provides simple operations , as well as some basic information about the primitive data type, which cannot be stored on the primitive itself.

![Wrapper Classes](https://www.google.com/imgres?imgurl=https%3A%2F%2Fmedia.geeksforgeeks.org%2Fwp-content%2Fcdn-uploads%2F20200806191733%2FWrapper-Class-in-Java.png&imgrefurl=https%3A%2F%2Fwww.geeksforgeeks.org%2Fwrapper-classes-java%2F&tbnid=jIV1eid8Ox3knM&vet=12ahUKEwiK2cPz6Iv8AhV-NUQIHRIgC0MQMygAegUIARDEAQ..i&docid=S1QNIcwYVfjelM&w=1000&h=511&q=primitive%20and%20wrapper%20classes%20in%20java&ved=2ahUKEwiK2cPz6Iv8AhV-NUQIHRIgC0MQMygAegUIARDEAQ)

**Overflow** If you try to put a value larger than the maximum value into an int.
**Underflow**If you try to put a value smaller than the minimum value into an int.

These situation are also know as integer wraparounds.The max value when it overflows, wraps around to the maximum value, and just continues processing without an error. You need to be aware that this could happen.

```java
int willThisCompile = (Integer.MAX_VALUE + 1); //Yes
int willThisCompile = (2147483647 + 1); // yes

int willThisCompile = 2147483648; //This will give an error

```

In Java, you cannot put commas in a numeric literal `int myMaxIntTes = 2,147,483,647;` so Java provided an alternative to improve readability, the undescore: `int myMaxIntTes = 2_147_483_647`. You can put the underscore anywhere you want a comma, but CANNOT be at the beggining or end of the numeric literal.

### byte, short, long and width

- byte : has the smallest range (-128 to 127). Can store 256 numbers and occupies 8 bits
- short:  with a range of -32768 to 32767. Occupies 16 bits and has a width of 16
- int: Java's default daya type for whole numbers. Occupies 32 bits and has the same width.
- long: has the largest range -9223372036854775808 to 9223372036854775807 

**Size of Primitive Types and Width**
Size or width, is the amount of space that determines (or limits) the range of values we've been discussing

In the case of `long myLongvalue = 100;` while the expression is not wrong is a bit misleading. The number `100` by default is an `int`. Java allows certain numeric literals to have a suffix appended to the value, to force it to be a different data type from he default type. The long is one of these types and it's suffix is an `L` either upper or lowercase, so the right way would be `long myLongvalue = 100L;` to avoid any confusion as it easier to read and doesn't get confused with a `1`
```java
long myLongvalue = 100L;
System.out.print("A long has a width of " + Long.SIZE);
// A long has a width of 64
```

### Casting in Java
Casting means to treat or convert a number, from one type to another. We put the type we want the number to be.
**Rules for declaring multiple variables in one Statement**
- You cannot declare variables with different data types in a single statement
- If you delcare multiple variables of the same data typ in a single statement, you must specify the data type only once before any variable names.

The Java compiler doesn't attempt to evaluate the value, in a variable, whe it's used in a calculation, so it doens't know if the value fits, and throws an error
`byte myNewByteValue = (myMinByteValue /2);`
If your calcilations uses literal values, Java can figure out the end result at compile time, and whether it fits into the variable, and won't throw an error if it does.
`byte myNewByteValue = (-128/2);`
In both examples, an int result is being returned from the calculation, but in the second example, Java knows the returned value can fit into a byte. We know, that if we simply assign a literal value to a byte variable, and the literal value fits, there's not problem, but here we've got an expression, that uses a variable that's been divided by 2. That's the difference compared to what we've done previously, when we've used a literal value. Java can make assumptions about literal values, that it can't make about expressions with variables. This problem comes about because the dafault whole number used by Java, is an int and that's why we've got an error here, so we let Java know by using casting
```
(byte) (myMinByteValue/2);
short myNewShortValue = (short)(myMinShortValue/2);
```

### Float and Double Primitives
- float: 32 bits, with a Min Value of 1.43-45 and a Max value of 3.4028235E38
- double. This is is Java's default type for any decimal or real numbers. 64 bits

Scientific noration can be translated into more familiar temrs, by replacing the E in the number, whith the phrase "times 10 to the power of"

1.4e-45 is the same as 1.4x 10^-45 and 3.4E38 is the same as 3.4x10^38

While the **double** data type is Java's default type for real numbers, this can be specified as a numeric literal with a suffix of either lower or uppercase `D`, but this is optional. You can do the same with the **float** data type.
```java
float myFloat = 5; double myDouble = 5;

myfloat = 5f;
myDouble = 5d;

float myOtherFloat = 5.25;  //This will give you an error because of the default type
float myOtherFloat = (float) 5.25; //Fixed using casting
float myOtherFloat = 5.25f; // Another way to fix the problem
```

### Floating Point Precision
The double is a better choice in most circumstances
- It's more precise
- Modern computers deal with these numbers faster than the equivalent float
- Java librries are often written to process and return doubles
- In general, float and double are grea floating point operations, but neither should be used when precise calculations are required - this is due to the limitation with how floating point numbers are stored. Java has the **Big Decimal** that overcomes this.

### The char and bolean Primitive Type
The char could be any single character, a letter, a digit or any other character, but it is different from a string.

- A char occupies two bytes of memory, or 16 bits and this. 
- You can store a unicode character `char myUnicode = '\u044' //unicode for letter "D"`
- There are 3 ways to assign a value to a char. Each ogf these methods represents storing letter D in memory
```java
char myChar = 'D';
char myChar = '\u0044';
char myChar = 68;

```

Developers will often use the word **is** as a prefix for a boolean variable name. This creates a name that seems to ask a question , which makes reading the code more intuitive, such as
- isCustomerOverTwentyOne
- isElegibleDiscount
- hasValidLicense, etc


### Primitive Types Recap and the String Data Type
You'll use Java's primitive data types, Java built-in classes (Big decimal)
and probably some combination of your own custom classes and somebody else's.

A String is a sequence of characters. In the case of the **char**, it could contain a **single character** only (a regular character or Unicode character). Technically  it's limited by memory or the MAX_VALUE of an **int** which was 2.14 billion.

Strings in Java are immutable. That measn you can't change a String after it's created, what happen is a new String is created.

java has another class aside from string that is more efficient if you're doing a lot of appending of multiple strings or values. The **StringBuilder** class is mutable, but does not share the String's special features, such as being able to assign it as a String literal or use the `+` operator on it.

The String is so intrinsic to the Java language, it can be used like a 9th primitive type, but it's not a primitive type, it's a class.

### Operators, Operands and Expressions
**Operators** in Jave are special symbols that perfomr specific operations on one, two or more operands, and then return a result.
An **operand** is a term used to describe any object that is manipulated by an **operator**. 
An **expression** is formed by combining variables, literals, method return values and operators.

```java
double mySalary = hoursWorked * hourlyrate;
```
In the statement above, `hoursWorked * hourlyRate` is the expression. 

**Comments** are ognored ny the computer and are added to a program to help descrive something. Comments are there for humans.

### Ternary Operator
This operator is a shortcut to assigning one of two values to a variable depending on a given condition.
```java
boolean wasCar = isCar ? true : false;
 
```
### Operator Recapt and Operator Precedence

[Summary of Operators](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/opsummary.html)
[Java Operator Precedence](https://www.cs.bilkent.edu.tr/~guvenir/courses/CS101/op_precedence.html)


```java
// Operator Challenge

double myFirstValue = 20.00d;
double mySecondValue = 80.00d;
double myThirdValue = (myFirstValue + mySecondValue) * 100d;
double theRemainder = myThirdValue % 40.00d;
boolean isNoRemainder = (theRemainder == 0) ? true : false;

```
## Section 4: IntelliJ Basics <a name="4"></a>

## Section 5: Expressions, Statements, Code blocks, Methods <a name="5"></a>
Java has 50 reserved keywords.
Exressions are essntially building blocks of all Java Programs. Expressions are built with values, variables, operators and method calls.
```java
int score = 100;
if(score>99){
    System.out.println("You got the high score");
    score = 0;
}
```
In the code above, just the following parts are expressions:
- score > 99
- "You got the high score"
- score = 0

Now in the case of `int myVariable = 50;` that's a Java **statement**. 

 ### Code Blocks and the IF-ELSE control statements

 ```java
 public class Main {
    public static void main(String[] args) {
        boolean gameOver = true;
        int score = 5000;
        int levelCompleted = 5;
        int bonus = 100;

//        if(score <= 5000) {
//            System.out.println("Your score was less than 5000");
//        } else {
//            System.out.println("Got here");
//         }
        if(gameOver == true){
            int finalScore = score + (levelCompleted * bonus);
            System.out.println("Your final score was " + finalScore);
        }
        

    }
}
 ```
 ### Methods
 When you're creating a method and you're defining **parameters** of a certain type and a name, you then don't have to create them as regular variables.. Because Java will automatically create variables with the appropiate data type for use, and they'll be deleted when the process goes back to the line after


 ```java
  public static void main(String[], args){
    
    //Method
    public static void calculateScore(bolean gameOver, int score, int levelCompleted, int bonus){
        int finalScore = score + (levelCompleted * bonus);
        finalScore += 20000;
        System.out.println("Your final score was " + finalScore);


    }
 }

 ```
 **void** is used when you want that your method doesn't return, otherwise you use the type of value you want it returned
 ```java
   public static void main(String[], args){
    
    public static int calculateScore(boolean gameOver, int score, int levelCompleted, int bonus){
        int finalScore = score + (levelCompleted * bonus);
        finalScore += 20000;
        System.out.println("Your final score was " + finalScore);
        return finalScore
    }
 }

 ```
 In programming terms `-1` is conventionally used to indicate an error and in searching algorithms `-1` indicates an invalid valye or value not found.

 A void method can also be known as a **procedure**, and a method generally speaking can also be known as a **function**.

 ```java
//Challenge
    public static void displayHighScorePosition(String player1, String player2, ){

        System.out.println("managed to get into position"+ "on the highscore table");

    }

    public static int calculateHighScorePosition(score){
        if(score >= 1000){
            return 1;
        }else if (score >= 500 && score < 1000 ){
            return 2;
        } else if (score >= 100 && score < 500){
            return 3;
        } else {
            return 4;
        }
    }
 ```
 
 ### Diff Merge Tool
 DiffMerge is a program that will help you to visually compare and merge files on any operating system
 
 ### Method Overloading
 Overloading is when you use the same method name, but with different parameters. So it is the ability to create multiple methods od the same name with different implementations. Calls to an overloaded method will rin a specific implementation of that method.

 ```java
 public class Main {

    public static void main(String[] args){
        calculate Socre("Tim", 500);
    }

    public static int calculateScore(String playerName, int score){
        System.out.println("Player " = playerName + " socre " + score + " points");
        return score * 1000;
    }

 }
// Player Tim scored 500 points

 ```
 Now you can use that in some other way
 ```java
 public class Main {

    public static void main(String[] args){
       int newScore = calculate Socre("Tim", 500);
       System.out.println("New score is " + newScore);
    }

    public static int calculateScore(String playerName, int score){
        System.out.println("Player " = playerName + " socre " + score + " points");
        return score * 1000;
    }

 }
// Player Tim scored 500 points
// New Score is 500000

 ```
 Now, let's go over Overloading
  ```java
 public class Main {

    public static void main(String[] args){
       int newScore = calculate Socre("Tim", 500);
       System.out.println("New score is " + newScore);
    }

    public static int calculateScore(String playerName, int score){
        System.out.println("Player " = playerName + " socre " + score + " points");
        return score * 1000;
    }

 }
// Player Tim scored 500 points
// New Score is 500000

 ```
 When we're overloading a method, we need to create aunique method signature, (just changing the data type of the return type of data that's goung to be returned from the method doesn't change the overall signature )
 ```java
 public class Main {
    public static void main(String[] args) {
        int newScore = calculateScore("Tim", 500);
        System.out.println("New score is " + newScore);
        calculateScore(75);
    }

    public static int calculateScore(String playerName, int score){
        System.out.println("Player " + playerName + " score " +
                score + " points.");
        return score * 1000;
    }

    public static int calculateScore( int score){
        System.out.println("Unnamed Player score " +
                score + " points.");
        return score * 1000;
    }

    public static int calculateScore(){
        System.out.println("No player name, no player score");
        return 0;
    }
//    This one, wouldn't work
//    public static void calculateScore( int score){
//        System.out.println("No player name, no player score");
//    }
    
} 
 ```

A **constant** is a variable that we cannot change once is assigned
```java
private static final String INVALID_VALUE_MESSAGE = "Invalid Value";
``` 
They cannot be changed

## Section 6: Control Flow <a name="6"></a>
### The Switch Statement
Switch is good to use if you're testing the same variable and you want to test different values for that variable
```java
public class Main {
    public static void main(String[] args) {
        int value = 1;
        if(value ==  1){
            System.out.println("Value was 1");
        } else if(value == 2){
            System.out.println("Value was 2");
        } else {
            System.out.println("Was not 1 or 2");
        }

        int switchValue = 1;
        switch(switchValue) {
            case 1:
                System.out.println("Value was 1");
                break;
            case 2:
                System.out.println("Value was 2");
                break;
            case 3: case 4: case 5:
                System.out.println("Was 3, or 4 or 5");
                 System.out.println("Actually it was a " + switchValue); 
            default:
                System.out.println("Was not 1 or 2");
                break;
        }
    }
}
```
The switch statement can be used with 4 primitive types: byte, short, char and int. Strings were added in jdk7
```java
//Single commas are used for char values, not double or you'll get an error
char charValue = 'D';
        switch(charValue) {
            case 'A':
                System.out.println("Letter A was found");
                break;
            case 'B':
                System.out.println("Letter B was found");
                break;
            case 'C': case 'D': case 'E':
                System.out.println(charValue + " was found");
                break;
            default:
                System.out.println("Could not found A, B, C, D, or E");
                break;
```
To takecare of String consitency, you can add methods
```java
String month = "JanuaRy";
switch(month.toLowerCase()){
    case "january";
    System.out.println("Jan");
    break;
}
```
### The for Statement
The basic format for the statement is as follows: `for(init; termination/condition; increment)`

Calculate prime numbers and add them to a counter until it reach 3 primer numbers
```java
  int totalPrime = 0;
    for(int i = 0; i<=50; i ++){
        if(isPrime(i)){
            totalPrime ++;
            System.out.println("Number " + i " is a primer number");
            if(totalPrime == 3){
                System.out.println("Exiting for loop");
                break;
            }
        }

    }

    public static boolean isPrime(int n){
        if(n == 1){
            return false;
        }
        for(int i=2; i <= n/2; i++){
            if(n % i == 0){
                return false;
            }
        }
        return true;
    }
 
```
There is another more efficient way to go about this problem using square root for the `isPrime`
```java
  int totalPrime = 0;
    for(int i = 0; i<=50; i ++){
        if(isPrime(i)){
            totalPrime ++;
            System.out.println("Number " + i " is a primer number");
            if(totalPrime == 3){
                System.out.println("Exiting for loop");
                break;
            }
        }

    }

    public static boolean isPrime(int n){
        if(n == 1){
            return false;
        }
        for(int i=2; i <= (long) Math.sqrt(n); i++){
            if(n % i == 0){
                return false;
            }
        }
        return true;
    }

```
### The While and do while statements
In the `while` loop this code executes if the condition is true. If we want to increment a variable, we have to do it manually inside the loop.If youe want to use a variable
- The **while** loop checks the condition at the start before executing the block

```java
while(condition){
    //statements
}
```
The `do..while` loop will execute at least once and then the condition is checked, if it executes once and checks
- With the **do while** loop the code block is executed at least once and then the condition is checked.
- Be careful with conditions, it is easy to end up with endless loop
- We can interrup the loop by using `continue` and/or a `break` statement.
- With the `continue` keyword the loop witll bypass the part of code block
that is below the `continue` keyword and continue with the next iteration.
- With the `break` keyword we can exit the loop depending on the condition that we are checking


```java
do {
    //statements
} while(condition);

```


A while loop that records the total number of even numbers found ina range and breaks, after 5 of them have been found

```java
int number = 4;
int finishNumber = 20;
int evenNumbersFound = 0;

while (number <= finishNumber>){
    number ++;
    if(!isEvenNumber(number)){
        continue;
    }
     System.out.println("Even number " + number);

    evenNumbersFound++;
    if(evenNumbersFound >=5){
        break;
    }
   
}
System.out.println("Even number" + number);

public static boolean isEvenNumber(int number){
    if((number % 2) == 0){
        return true;
    } else{
        false;
    }
}

```

### Parsing Values from a String
One use case, when we need to convert a String to another data type is when 
reading input from a user. One way to convert a string into a number is by means of parsing method, now with these methods we can convert as string into various primitive types depending on the specific pase we choose to use
```java
public class Main {
    public static void main(String[] args) {
        String numberAsString = "2018";
        System.out.println("numberAsString= " + numberAsString);

        // Integer in this case is a class. This is a wrapper class
        // that contains useful static methods
        int number = Integer.parseInt(numberAsString);
        System.out.println("number =" + number);
    }
}
```
- `double number = Double.parseDouble(numberAsString);` converts to a Double

### Reading User Input
The goal of this section is to  is to make an interactive application where a user will enter his or her name and year of birth and then the application will calculate the current age of the user.

* `Scanner`Which is a simple text scanner that can parse both Primitive types and Strings.
So essentially scanner uses methods like parse Int Internally.It is one of Java's built-in classes that allows you to read user input. After you're done using scanner you need to close it, to release the underlying memory that was using internally
* `Next` returns a string allowing us to save the returned value to a variable.
* `System.in` allows you to type into the console which then gets returned back to the program

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.our.println()
        System.out.println("Enter your name: ");
        String name = scanner.nextLine();

        System.out.println("Your name is " + name);
        scanner.close(); //
    }
    
}
```

When coding with age, we might encounter a bug when the program skips the name input, that can be solver with `scanner.nextLine()`

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        
        Scanner scanner = new Scanner(System.in);
        System.out.println("enter your year of birth: ");
        int yearOfBirth = scanner.nextInt(); //Immediately converts String to Int
        scanner.nextLine(); //Handle next line character (Enter key)

        System.out.println("Enter your name: ");
        String name = scanner.nextLine();
        int age = 2022 - yearOfBirth;
        if(age >= 0 && age <= 120){
            System.out.println("Your name is " + name + ", and you are " + age + " year old.");
        scanner.close();
        } else {
            System.out.print.ln("Invalid year of birth");
             
        }

    }

}

```
### Problems and Solutions
What if in the above code, people entered other data type instead of the expected one. For example if you enter name instead of your year of birth, you'll get a `input mismatch exception`
- `.hasNextInt()` checks to see if the next input entered is a number in this case, however it won't remove it from the scanner, so it allow us to avoid generating type errors

Now we have a program with some validation
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        System.out.println("enter your year of birth: ");
        boolean hasNextInt = scanner.hasNextInt();
        if(hasNextInt){
            int yearOfBirth = scanner.nextInt(); //Immediately converts String to Int
            scanner.nextLine(); //Handle next line character (Enter key)

            System.out.println("Enter your name: ");
            String name = scanner.nextLine();
            int age = 2022 - yearOfBirth;
            if(age >= 0 && age <= 120){
                System.out.println("Your name is " + name + ", and you are " + age + " year old.");

            } else System.out.println("Invalid year of birth");

        } else {
            System.out.println("Unable to parse year of birth");
        }

        scanner.close();
    }

}

```
### Reading User Input Challenge
* Read 10 numbers from the console entered by the user and print the sum of those numbers
* Create a Scanner 
* Use the `hasNextInt()` method to check if the user entered a `int` value. If false, print the "Invalid Number" message and continue reading until you have 10 numbers
* Before the user enter each number, print the message "Enter number #x:" whee "x" represents the count
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        int counter = 0; // Count the valid numbers
        int sum = 0;    // Sum of the counted nums

        while(counter < 10){
            int order = counter + 1;
            System.out.println("Enter number #" + order + ":" );
            boolean isAnInt = scanner.hasNextInt();

            if(isAnInt){
                int number = scanner.nextInt();
                counter ++;
                sum += number;

                if(counter == 10){
                    break;
                }
            } else {
                System.out.println("Invalid Number");
            }
            scanner.nextLine(); // handle end of line(Enter key)
        }
        System.out.println("sum = " + sum);
        scanner.close();
    }
}
```

### Min and Max Challenge
* Read the number from the console entered by the user and print the minimum and maximum number the user has entered
* Before the user enters the number, print the message: "Enter number: "
* If the user enters an invalid number, break out of the loop and print the min and max number
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int min = 0;
        int max = 0;
        boolean first = true; // flag

        while(true){
            System.out.println("Enter number: ");
            boolean isAnInt = scanner.hasNextInt();

            if(isAnInt){
                int number = scanner.nextInt();

                if(first){
                    first = false;
                    min = number;
                    max = number;
                }

                if(number > max){
                    max = number;
                }
                if (number < min){
                    min = number;
                }

            } else {
                break; // In case the input is not a number
                }
            scanner.nextLine(); //handle input
        }
        System.out.println("min =" + min + ", max= " + max);
        scanner.close();

    }
}
```
Alternatively, you can set min and max to the max and min values the data type `int` can hold, and that way, you won't need to use the flag
```java
  int min = 2147483647;
  int max = -2147483647;
```
Or you can use constants
```java
  int min = Integer.MAX_VALUE;
  int max = Integer.MIN_VALUE;
```

## Section 7: Object Oriented Programming Part 1 - Inheritance <a name="7"></a>
### Introduction to Classes and Objects
Object oriented programming is a way to model real world objects, as software objects, which contain both data and code. It's sometimes called class based programming. Class based programming starts with classes, which become the blue prints for objects

Objects have 2 major components:
- State : Characteristics about the item that can describe it.
- Behavior: Actions that can be perfomed by the objects, or upon the object

A **class** is like a template or a blueprint for creating objects. A software object store its state in **fields** which can also be called variables, or attributes. And  objecst expose their behavior with **methods**

The class describes the data(fields), and the behavior (methods), that are relevant to the real world objects we want to describe. These are called class members. A class member can be a field, a method or some other type of dependend element.

If a field is **static**, there is only one copy in memory, and this value is associated with the class, or template itself. If a field is not statics, it's called an **instance field**, and each object may have a different value stored for this field.

A static method can't be dependent on any one object's state, so it cant'e reference any instance members. In other words, any method that operates on instance fields, need to be non-static

A **class** is like a template or a blueprint for creating objects. Class could be thought of as a powerful user-defined data type, sort of an extra data type, this is not correct in the true meaning, but it give us an idea  of what classes really 

- Classes should start with uppercase letters
- Classes can be organized into logical groupings, which are called packages. You declare a package name in the class using the package statement, if you don't declare a package, the class implicitly belongs to the default package.
- A class is said to be a top-level class, if it is defined in the source code file, and not enclosed in the code block of another class, type, or method.
- A top level class has only two valid access modifier options: public or none.
- **public** is an access modifier. This modifier determines what access we want to allow others to have to this new class. So in this case **public** means unrestricted access to the class.
- When the modifier is omitted, this has special meaning, called **package-private acess**, meaning the class is accesible only to classes in the same package.
- **private** is for where no other class can access that class.
- **protected** which allows classes in this package to access your class
- Local variables are only used inside the method they have been initialized.

Classes allow us to create variables that can be seen and are accesible from anywhere within the class that we're creating. These are know as **class or member variables** but most commonly referred as **fields**. When creating a field for a class, you need to also specify an access modifier that works the same way as the access modifier for a class definition. As a general rule, when you're defining fields in Java in a class, you go with the access modifier **private** , unlike the class where we've gone with *public*

So what private means when talking about fields, what we're really doing with it is we're adhering to **encapsulation**, which is a key fundamental rule of object-oriented programming. So encapsulation in Java is used to hide the fields and methods from access publicly.

Encapsulation in Object Oriented Programminh usually gas two meanings:
- Bundling of behaviour abd attributes on a single object
- Hiding fields, and some methods from public access

### Introduction to Classes, using Getter Methods
```java
// car.java
public class Car {
  private String make;
  private String model;
  private String color;
  private int doors;
  private boolean convertible;

  public void describeCar(){
    System.out.println(door + "-Door " +
    color + " " + 
    make + " " + 
    model + " " +
    ( convertible ? "Convertible" : ""));
  }

}
```
**null** is a special word in Java, meaning the variable or attributes has a type, but no reference to an object. That means no instance, or object is assigned to the variable or field. Fields with primitive data types are never null.

Fields with a primitive data type. will be assigned a default value by Java.

Now we can assign some default values to our class:

```java
public class Car {
  private String make = "Tesla";
  private String model = "Model X";
  private String color = "Gray";
  private int doors = 2;
  private boolean convertible = true;

```
This means that every objects that's instantiated, will get assgiend the default values we declared, instead of Java's implicit values.

```java
public class Main {
    public static void main(String[] args) {
        Car car = new car();
        car.describeCar();
    
    //2-Door Gray Testla Model X Convertible
}
```
So now how do we set each field with a different value, since we set the fields to private we cannot use dot notation. `car.make = "Porsche"` we can set them to Public, but this is a BAD practice. So what we're going to do is allow access to this data, either to SET it or GET it through method of this class.

A **getter** is a method on a class, that retrieves the value of a private field, and returns it. You could have getter methods for attributes that are not really declared on your class, but that are devided in some way.
A **setter** is a method on a class, that sets the value of a private field. A setter method may simply just assign the argument passed to the attribute, but it often contains code to validate data, check addtitional security requirements, ensure immutability of the field value, or any other code required to protect and validate an object's state.

The purpose of these methods is to control, and protect access to private fields.

```java
// car.java
public class Car {

  private int doors;
  private boolean convertible;
  ...
  public String getMake(){
    return make;

  }

  public void describeCar(){
   
  }

}
```
So our getter is set to public, but we don't use tge word **static**. When writting methods that use non static fields, you method can't be declared static

### Classes, using Setters and Creating Objects
We talked about best practices for fields, that in general fields of classes should be private, and a getter method should be created to access those fields, this provides encapsultation of the internals of our class and supports maintenance of a public interface that doesn't have to chance even though our class might

```java
public void setMake(String make){
    make = make;
}
```
The code above will give us several warnings , but we can solve it using the word `this`. which is a special keyqord in Java. What it really refers to is the instace that was created when the object was instantiated. So `this` is a special reference name for the object or instance, which it can use to describe itself. And we can use `this` to access fields on the class.
```java
public void setMake(String make){
    this.make = make;
}
```
Now we can update our `car` object
```java
public class Main {
    public static void main(String[] args) {
        Car car = new car();
        car.setMake("Porsche");
}
```
With Setters you can do validation:

```java
public void setMake(String make){
    if(make == null) make = "Unknown";
    String lowercaseMake = make.toLowerCase();
    switch(lowercaseMake){
        case "holden", "porsche", "tesla" -> this.make = make;
        default -> {
            this.make = "Unsupported";
        }
    }
}
```
BY using a setter method we force thme to go through a controlled way of setting up the data on the object and make sure that the data in our objects is valid data.

When we use the `new` keyword, we've saud that created the object and is called **instantiation**, but another term you'll hear fro this process is, constructing the object



### Contructors
A constructor is used in the creation of an object, that's an instance of a class. It's a special type of code block that has a specific name and parameters, much like a method.

It has the same name as the class itself and it doesn't return any values.

You never include a return type from a constructor, not even void.

You can, and should specify an appropiate access modifier, to ocntrol who should be able to create new instances of a class.

```java
public class Account{ // This is the class declaration

  public Account(){  //This is the constructor declaration

  }

}
```
If a class contains no contructor declarations, then a default contructor is implicitly declared. This constructor has no parameters, and is often called the *no-args* (no arguments) contructor. If a class constains any other constructor declarations, then a default constructor is NOT implicitly declared



Imagine that we have the following 2 classes, to set bank accounts
```java
public class Account {
    private String number;
    private double balance;
    private String customerName;
    private String customerEmail;
    private String customerPhone;

    public void deposit(double depositAmount) {
        this.balance += depositAmount;
        System.out.println("Deposit of " + depositAmount + " made. New balance is " + this.balance);
    }

    public void withdrawal(double withdrawalAmount){
        if(this.balance - withdrawalAmount <= 0){
            System.out.println("Only " + this.balance + " available. Withdrawal not processed" );
        } else {
            balance -= withdrawalAmount;
            System.out.println("Withdrawal of " + withdrawalAmount + " processed. Remaining balance = " + balance);
        }

    }

    public String getNumber() {
        return number;
    }

    public void setNumber(String number) {
        this.number = number;
    }

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        this.balance = balance;
    }

    public String getCustomerName() {
        return customerName;
    }

    public void setCustomerName(String customerName) {
        this.customerName = customerName;
    }

    public String getCustomerEmail() {
        return customerEmail;
    }

    public void setCustomerEmail(String customerEmail) {
        this.customerEmail = customerEmail;
    }

    public String getCustomerPhone() {
        return customerPhone;
    }

    public void setCustomerPhone(String customerPhone) {
        this.customerPhone = customerPhone;
    }
}
```
And the main one, where we set the new Account
```java
public class Main {
    public static void main(String[] args) {
        Account bobsAccount = new Account();
        bobsAccount.setNumber("12345");
        bobsAccount.setBalance(0.00);
        bobsAccount.setCustomerName("Bob Brown");
        bobsAccount.setCustomerEmail("bob@email.com");
        bobsAccount.setNumber("(087)123-4567");
    
        //Test
        bobsAccount.deposit(50.0);
        bobsAccount.withdrawal(100.0);
        bobsAccount.deposit(51.0);
        bobsAccount.withdrawal(100.0);
       }
}
```
The first part can be taken care with a **constructor** to set the initial values of fields
```java
// Account class w/contructuor
public class Account {
    private String number;
    private double balance;
    private String customerName;
    private String customerEmail;
    private String customerPhone;


    public Account(){
        System.out.println("Empty constructor called");
    }

    public Account(String number, double balance, String customerName, String customerEmail, String customerPhone){
        this.number = number;
        this.balance = balance;
        this.customerName = customerName;
        this. customerPhone = customerPhone;
    }


    public void deposit(double depositAmount) {
        this.balance += depositAmount;
        System.out.println("Deposit of " + depositAmount + " made. New balance is " + this.balance);
    }
...
```
And now we can go to main, and use the contructor:
```java
public class Main {
    public static void main(String[] args) {
        Account bobsAccount = new Account("12345", 0.00, "Bob Browb", "bob@email.com", "(087)123-4567");
//        bobsAccount.setNumber("12345");
//        bobsAccount.setBalance(0.00);
//        bobsAccount.setCustomerName("Bob Brown");
//        bobsAccount.setCustomerEmail("bob@email.com");
//        bobsAccount.setNumber("(087)123-4567");

```
So the purpose of a constructor is to, essentially initialize the object that we're creating, and do whatever ekse we need to happen, while the object is being instantiated. So it's only ever called once at the start when we're creatng the object. A class have one or many constructors, one of which can be the No-ARGS contructor

Now we'' add another constructor, and this time we'll declare some parameters. doint this will let us pass values to the constructor. We can use these valyes to assign data to our fields, instead of calling a bunch of setters

**Constructot overloading** is declaring multiple constructor, with different formal parameters. The number of parameters can be different between contructors. Or if the number of parameters is the same between two contructors, theyr types or oder of the types must differ.

### Constructors Part 2
**Constructor chaining with this()**
Constructor chaining is when one constructor explicitly calls another overloaded constructor.
You can call a contructor only from another constructor
You must use the special statement `this()` to execute another constructor, passing it arguments if required.
And `this()` must be the first executable statement, if it's used from another constructor

As in the example below, you need to make sure when chaining constructors  that the `this()` statement is the first line in the contructor

```java
public class Account {
    private String number;
    private double balance;
    private String customerName;
    private String customerEmail;
    private String customerPhone;


    public Account(){
        System.out.println("Empty constructor called");
    }

    public Account(){
        //Here we're calling a constructor within another constructor
        //In this case with default values if none is provided
        this("56789", 2.50, "Default name", "Default address", "Default phone");
        System.out.println("Empty constructor called");
    }

    public Account(String number, double balance, String customerName, String customerEmail,
                   String customerPhone){
        System.out.println("Account constructor with arameter called");
        this.number = number;
        this.balance = balance;
        this.customerName = customerName;
        this. customerPhone = customerPhone;

    }

```
You can also use the setters in the constructors, with the advangate that if you have validation in u setters, then your constructor, would like:
```java

public Account(String number, double balance, String customerName, String customerEmail,
                   String customerPhone){
        System.out.println("Account constructor with arameter called");
        setNumber(number);
        this.balance = balance;
        this.customerName = customerName;
        this. customerPhone = customerPhone;

    }

    ublic void setNumber(String number) {
        this.number = number;
    }

```
But there is conflicting opinions regarding wich is the best approach, but it seems the BEST appoach is to do it directly and not use the `setter`, because there can be some scenarios where that code isn't executed

Here is another class with overloading constructors:
```java
public class VipCustomer {
    private String  name;
    private double creditLimit;
    private String email;

    public  VipCustomer(){
        this("Default name", 50000.00, "default@email.com");
    }

    public VipCustomer(String name, double creditLimit) {
      this(name, creditLimit, "unknown@email.com");
    }

    public VipCustomer(String name, double creditLimit, String email){
        this.name = name;
        this.creditLimit = creditLimit;
        this.email = email;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getCreditLimit() {
        return creditLimit;
    }

    public void setCreditLimit(double creditLimit) {
        this.creditLimit = creditLimit;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```
### Reference vs Object vs Instance vs Class
 Let's use the analogy of buidling a house to understand Classes
 * A **class** is basically a blueprint for a house, using the blueprint we can build as many houses as we like based on those plans.
 * Each house you build (in other words **instantiate** using the **new** operator) is an `object` also know as an **instance**
 * Each house you build has an address (a physical location). in other words if you want to tell somone where you live, you give them your address (perhaps written on a piece or paper). This is known as a **reference** 
 * You can copy that reference as many times a syou like but there is still just one house. In other words we are copying the paper that has address on it not the house itself.
 * We can pass references as parametes to constructors and methods


Here we have a class HOuse with an instance variable(field) color.

 ```java
 class House{
    private String color;

    public House(String color){
        this.color = color;
    }

    public String getColor(){
        return color;
    }

    public void setColor(String color){
        this.color = color;
    }
 }
 ```

 ```java
 public class Main{

    public static void main(String[] args){
        House blueHouse = new House("blue");
        House anotherHouse = blueHouse;
    }
 }
 ```
 The line `House blueHouse = new House("blue");` creates a new instance of the House class, that we're assigning it to the `blueHouse` **variable**. In other words it is a **reference** to the object in memory. `House anotherHouse = blueHouse;` creates another reference to the same object in memory. Here we have 2 references to that one object.

 ### Static vs Instance Variables
 **Static Variables**
 * Declared by using the word static
 * Static variables are also know as static member variables
 * Every instance of the class shares the same static variable
 * So if changes are made to that variable, all other instances of that class will see the effect of that change
* It is considered best practice to use the Class name, and not the reference variable to access a static variable
```java
class Dog{
  static String genus = "Canis";
  void printData(){
    Dog d = new Dog();
    System.out.println(d.genus); // Confusing
    System.out.println(Dog.genus); //Clearer
  }
}
```
An instance isnt't required to exist, to access the value of a static variable.
```java
class Dog{
  static String genus = "Canis";
}

class Main{
    public static void main(String[] args){
        System.out.println(Dog.genus); // No instance of Dog needs to exist, in order to access a static variable
    }
}

```
Static variables aren't used very often, but can sometimes be very useful. They can be used for:
* Storing counters
* Generatiing unique ids
* Storing a constant value that doesn't change like PI
* Creating and controlling access to a shared resource
```java
class Dog{
    private static String name;
    public Dog(String name){
        Dog.name = name;
    }
    public void printName(){
         System.out.println("name = " + name); //Using Dog.name would have made this code less confusing
    }
}

class Main{
    public static void main(String[] args){
        Dog rex = new Dog("rex"); //Creates instance (rex)
        Dog fluffy = new Dog("fluffy"); // Creates instance (fluffy)
        rex.printName();      // prints fluffy
        fluffy.printName(:)   //prints fluffy
    }
}
```
**Instance Variables**
* They don't use the static keyword
* They're also known as fields, or member variables
* Instance variables belogn to a specific instance of a class
* Each instance hast its own copy of an instance variable
* every instance can have a different value
* Instance variables represent the state of a specific instance of a class
```java
class Dog{
    private String name;
    public Dog(String name){
        Dog.name = name;
    }
    public void printName(){
         System.out.println("name = " + name); //Using Dog.name would have made this code less confusing
    }
}

class Main{
    public static void main(String[] args){
        Dog rex = new Dog("rex"); //Creates instance (rex)
        Dog fluffy = new Dog("fluffy"); // Creates instance (fluffy)
        rex.printName();      // prints rex
        fluffy.printName(:)   //prints fluffy
    }
}
```

### Static vs Instance Methods
**Static Methods**
- Static methods are declares using the static modifier
- Static methods can't acccess instance methods and instance variables directly
- Theyre usually used for operations that don't require any data from an instance of the class(from `this`)
- If you rememeber, the this keyword is the current instance of a class
- So inside a static method,  we can't use the this keyword
- Whenever you see a method that doesn't use instance variables, that method should probably be declared as a static method
- For example, main is a static method, and it's called by the java virtual machine when starts the java application

```java
class Calculator{
    public static void printSum(int a, int b){
        System.out.println("sum = " + (a + b));
    }
}
public class Main{
    public static void main(String[] args){
       Calculator.printSum(5,10);
       printHello();  //Shorter from main.printHello();
    }
    public static void printHello(){
        System.out.println("Hello");
    } 
}
```
So as you can see, to call the `printSum` method, we just need to type the class name or like in `printHello` we can just type the method name with parentheses, which will automatically call the static method, becase it's invoked from a static method itself, so static methods dont require an instance to be created, we can just type the class name, and ise the do notation, with the method name to acess them

**Instance Methods**
- Instance methods belong to an instance of a class
- To use an instance method, we have to instantiate the class first
- Instance methods can access instance methods and instance variables directly
- Instance methods can lasso access static methods and static variables directly
```java
class Dog{
    public void bark(){
        System.out.println("woof");
    }
}
public class Main{
    Dog rex = new Dog(); //Create instance
    rex.bark(); //call instance method
}
```
**Static or Instance Method**
Shoul a method be static -> Does it use any fields( instance variables) or instance methods:
- Yes, then it should probably be an instance method
- No, tne it should probably be static method

### The POJO
- A plain old java object (whose acronym is POJO)is a class that generally only has instance fields. 
- It's used to house data, and pass data between functional classes. 
- It usually has few, if any methofs other than getters and setters
- Many database frameworks use POJO's to read data from, or to write data to databases, files or streams
- A POJO also might be called a bean or a JavaBean
- A JavaBean is just a POJO, with some extra rulea applied to it
- A POJO is sometimes called an Entity, becuase it mirrors database entities
- Another acronym is DTO, for Data Transfer Object
- It's a description of an object, that can be modeled as just data
- There are many generation tools that will turn a data model into generated POJO's or JavaBeans
- You've seen an example of similar code generation in intelliJ, which allowed us to generate getters, setters, and constructors in a uniform way

A POJO in int's simples form, required a way to populate data, and we can do this with a constructor

```java
public class Student{
    private String id;
    private String name;
    private String dateOfBirth;
    private String classList;

    //using intelliJ, we create the following contructor
    public Student(String id, String name, String dateOfBirth, String classList ){
        this.id = id;
        this.name = name;
        this.dateOfBrth = dateOfBirth;
        this.classList = classList;
    }
    @Override
    public String toString(){
        return "Student{" +
        ....}
    }
}

public class Main{
    public static void main(String[] args){
      for(int i = 1; i <= 5; i++){
        Student s = new Student("S92300" + i,
        switch(i){
            case 1 -> "Mary";
            case 2 -> "Carol";
            case 3 -> "Tim";
            case 4 -> "Harry";
            case 5 -> "Lisa";
            default -> "Anonymous";
        },
        "05/11/1985",
        "Java Masterclass");
      }


    } 
}

```
`toString` is a special method in Java, we can implement this method in any class we create, and odint this lets us print out the current state of our object.

**Annotation**
- Annotation are a type of metadata
- Metadata is a way of formally describing addtional information about our code
- Annotations are more structured, and have more meaning than comments. This is because they can be used by the compiler or other types or pre-processing functions, to get information about the code.
- Medata doesn't affect how the code runs, s this code will still run with or without the annotation

**Overriden Method**
An overriden method, is not the same thing as an overloaded method
An overriden method is a psecial method in Java, the other classes can implement, if they use a specified method signature

If we add setter and getter methods, our code has all we need to manipulate data, setting, updating and retrieving it.

### Java's Implicit POJO Type, the Record
We talk about the POJO and how it comes with a lot of what we call boilerplate code. It's code that's repetitive and follows certain rules.
Once created, this code is rarely looked at, or modified. In fact, there are tools that'll just regenerate all of this code, if your underlying fata, or domain model changes. Even better though, Java introduced a new type, the **record** which becase part of the official language, in JDK16

**The Record Type**
The record was introduced in JDK14, and became oficially part of Java in JDK16
It's purpose is to replace the boilerplate code of the POJO, but to be more restrictive. Java calls them "plain data carriers". The word carrier is an important term, because it means the record has more rules built-in than a POJO would

The recor is a special class that contains data, that's not mean to be altered. In other words, it seeks to achieve inmmutability, for the data in its members. It contains only the most fundamental methods, such as constructors and accessors (getters). Best of all, you the developer, don't have to write or generate any of this code.
```java
public record LPAStudent(String id, String name, String dateOfBirth, String classList ){

}
```
```java
public class Main{
    public static void main(String[] args){
      for(int i = 1; i <= 5; i++){
        LPAStudent s = new LPAStudent("S92300" + i,
        switch(i){
            case 1 -> "Mary";
            case 2 -> "Carol";
            case 3 -> "Tim";
            case 4 -> "Harry";
            case 5 -> "Lisa";
            default -> "Anonymous";
        },
        "05/11/1985",
        "Java Masterclass");
      }
    } 
}
```
We've replaced 56 lines of code that we had in `Student.java` with these 2 lines of code. Now `LPAStudent` doens't have our support setter method, but the other functionality calling the constructor with 4 params, and printing the data out,, is implicitly part of the record

What does Java tells us aboit what is implicitly created, when we declare a record as we did in this code `public record LPAStudent(String id, String name, String dateOfBirth, String classList ){}`
First, it's importa to undertand that the part that's in parentheses is called the *record header*. The record header consist of record components, a comma delimited list of components

For each component in the header Java generates:
- A field with the same name and declared type as the record component
- The field is declared private and final. (It means the field can't be modified)
- The field sometimes refrered to as component field.
- Java generates a toString method that prints out each atribute in a formatted String
- In addition to creating a private final field for each component. Java generates a public accessor method for each component. This method has the same name and type of the component, but it doesn't have any kind of special prefix, not get or is for example.

```java
public class Main{
    public static void main(String[] args){
      ...
      Student pojoStudent = new Student("S9223006", "Ann", "05/11/1985", "Java Masterclass");
      LPAStudent recordStudent = new LPAStudent("S9223007", "Bill", "05/11/1985", "Java Masterclass");
    } 

    System.out.println(pojoStudent.getName() + " is taking " + pojoStudent.getClassList());
    System.out.println(recordStudent.name() + " is taking " + recordStudent.classList());
}
```
That's how we use accessor methods, which we've called getters up until now because traditionally , the prefix get was used for the accessor method

Now if we want to set data in these 2 types of students, it would only work in the POJO student
```java
pojoStudent.setClassList(pojoStudent.getClassList() + ", Java OCP Exam 829");
```
Why is the record built to be immutable. There are more use casses for immutable data transfer objects, and keeping them well encapsulated. You want to protect the data from unintended mutations.

If you want to modify data on your class, you won't be using the record. You can use the code generation options for the POJO. But if you're reading a whole of of records, from a database or file source, and simply passing this data around, then the record is a big improvement.

### Inheritance Part 1
We could look at inheritance as a form of code re-use
It's a way to organize classes into a parent-child hierarchy, which lets the child inherit(re-use) fields and methods from it's parent

If we look at the Animal kingdom, we can look at this hierarchy. The most generic, or base class starts at the top of the hierarchy. Every class below is a subclass. A parent class can have multiple children, but a child can only have one direct parent in Java, but it'll inherit for its parent class's parent, and so on.

A **class diagram**, allows us to design our classes before we built them.
![class diagram example](https://miro.medium.com/max/1400/1*szU8ngrWSXmBNPYReMyK5w.webp)

```java
/********
  BASE CLASS
 ***********/
public class Animal {
    //fields
   private String type;
   private String size;
   private double weight;
    
    //constructor
    public Animal(String type, String size, Double weight){
        this.type = type;
        this.size = size;
        this.weight = weight;
    }
    //We'll also autogenerate all getter and setters along with toString method
    @Overrride
    public String toString(){
        return  "Animal{" +
                "type = ' " + type + '\'' +
                ", size = '" + size + '\'' +
                ", weight = '" + weight + '\'' +
                '}';
    }

    public void move(String speed){
        System.out.println(type + " moves " + speed);
    }

    public void makeNoise(){
        Systen.out.println(type + " makes some kind of noise " + speed);
    }
}
```
Now we create another class using **extends**. Using exteds specifies the superclass (or parent class) of the class we're declaring. A class can specify one, and only one class in its extends clause

At first, when we extend the class we'll get an error, because there is no default constructor in Animal (meaning we never created a constructor, with no arguments) and this matter to our Dog class because Java has already created an implicit constructor in our Dog class, so we'll create one

```java
public class Dog extends Animal{

    public Dog(){
        super();
    }
}

```
You'll rememeber that we use the `this` keyword, followed by parentheses and param as a way to call anothe constructor in the same class, well `super()` is similar to that. It's a way to class the constructo on the parent class, or super class
- `super()` is a lot like `this()`
- It's a way to call a constructor on the superclass, directly from the subclass constructor
- Like `this()`, it has the be the first statement in the constructor. Because of that rule, `this()` and `super()` can never be called from the same constructor 
- If you don't make a call to super(), then Java makes it for you, using super's default constructor
- If your super class doesn't have a default constructor, then you must explicitly call `super()` in all of your constructors, passing the right arguments to that constructor.

So we add the empty constructor in Animal, and everything s

```java
/********
  BASE CLASS
 ***********/
public class Animal {
    //fields
   private String type;
   private String size;
   private double weight;
    
    public Animal(){}
    //constructor
    public Animal(String type, String size, Double weight){
        this.type = type;
        this.size = size;
        this.weight = weight;
    }
  ...
}
```
Before, we create any instances, I want to create a method on the Main class, that'll take any Animal object, and execute its three methods

```java
public class Main{
    public static void main(String[] args){
        Animal animal = new Animal("Generic Animal", "Huge", 400);
        doAnimalStuff(animal, "slow");

        Dog dog = new Dog();
        doAnimalStuff(dog, "fast");
     
    }
    public static void doAnimalStuff(Anima animal, String speed){
        animal.makeNoise();
        animal.move(speed);
        System.out.println(animal);
        System.out.println("_ _ _ _ _ _ _");
        
    }
}

/*
Generic Animal makes some kind of noise
Generic Animal moves slow
Animal{type='Generic Animal', size='Huge', weight= 400.00}
-------
null makes some kind of noise
null moves fast
Animal{type='null', size='null', weight= 0.0}

*/
```
We crated dog with a default constructor (no arguments passsed) so nothing got on this class, but at least it has inherit all of Animal's attributes

```java
public class Dog extends Animal{
    public Dog(){
        super("Mutt", "Big", 50);
    }
}
```
And if we run the code in main again this will change to the params we passed to Dog.  

### Inheritance Part 2
Now, we're going to make Dog different from Animal, by declaring the methods that are specific to it.
```java
public class Dog extends Animal{
    private String earShape;
    private String tailShape;

    public Dog(){
        super("Mutt", "Big", 50);
    }
    //We're going to remove the size parameter, and derive it with weight, passing it to the super call
    //This constructor has a combinatin of the Dog and Animal fields in its arguments list
    //We're calling the super contructor to set some of our fields, the Animal specific fields
    //Since we cannot do anything before super, we ca do it as an expression in the argument list. This is one way to perfom calculations, in your constructor and pass the result to the super call
    public Dog(String type, double weight, String earShape, String tailShape){
        super(type, weight < 15 ? "small" : (weight < 35 ? "medium" : "large"),
        weight);
        this.earShape = earShape;
        this.tailShape = tailShape;
    }

    public Dog(String type, double weight){
        this(type, weight, "Perky", "Curled");
    }

    @Override
    public String toString(){
        return Dog...
        ..
        "} " + super.toString();
    }
}
```
**Overriding a method** is when you crate a method on a subclass, which has the same signature as a method on the superclass. Remember that a **method signature** consists of the method name, and the number and types of parameters.

You override a parent class method, when you want the child class to show different behavior for that method
> IntelliJ has a feature to override methods

The overriden method can do one of three things:
1. It can implement completely different behavior, overriding the behavior of a parent
2. It can simply call the parent's class method, which is somewhat reduntant
3. Or the metod can call the parent class's method, and include other code to run, so it can extend the functionality for the Dog, for that behavior

```java
public class Dog extends Animal{
    ...

    @Override
    public move(String speed){
        super.move(speed);
        System.out.println("Dogs walk, run and wag their tail");
    }
}
```
### Inheritance Part 3
Now, we're going to create some methods for the Dog subclass
```java
public class Dog extends Animal {

    public void move (String speed){
        super.move(speed);
        if( speed == "slow"){
            walk();
            wagTail();
        } else {
            run();
            bark();
        }
        System.out.println();
    }

    private void bark(){
        System.out.println("Woof!");
    }
    private void run(){
        System.out.println("Dog running");
    }
    private void walk(){
        System.out.println("Dog walking");
    }
    private void wagTail(){
        System.out.println("tail wagging");
    }
}
```
Now, we're going to change or `makeNoise` method in our Dog class again.
```java
public class Dog extends Animal {
    ...
    public void makeNoise(){
        if (type == "Wolf"){
            System.out.println("Ow woooo!");
        }
        ...
    }
```
This will give us a compiler error, because `type` has `private` access in Animal, but there is a modifier that allows access for subclasses, and that's the `protected` modifier. What this modifier says is, let any class that is a subclass, access this field. This is **conditional encapsulation** we're allowing some limited access to our internal fields. Protected access also means that any classes in the same package, will also have access

### What is the jav.lang.Object
evry class in Java, intrisically extends a special Java class. This class is named **Object**, and it's in the java.lang.package.
Class Object is the root of the class hierarchy, every class has Object as a superclass. All objects, including arrays, implement the methods of this class

> Remember only one class in Java source file can be public
```java
public class Main extends Object{
    public static void main(String[] args){
      Student max = new Student("Max", 21);
      System.out.println(max.toString());
     
    }

    class Student {
        //instance variables
        private String name;
        private int age;
        //constructor
        Student(String name, int age){
            this.name = name;
            this.age = age;
        }
    }
   
}
```
If we run this code, we'll get something like `Student@65ab7765`. The code in the `toString()` method in the Object class prints out the class name(which in our case is Student), followed by an @ sign, then the hash code of the Object. A **hash Code** is an integer, that is unique to an instance(in the currently executing code). When an instance is created, it's assigned a hashcode, and that hashCode is what can tell us if our multiple references are pointing to a single instance. It's a mechanism for comparison.
```java
public class Main extends Object{
    public static void main(String[] args){
      Student max = new Student("Max", 21);
      System.out.println(max.toString());

     
    }

    class Student {
        //instance variables
        private String name;
        private int age;
        //constructor
        Student(String name, int age){
            this.name = name;
            this.age = age;
        }
        // This call the code that Java would implictly do for us
        // @Override
        // public String toString(){
        //     return super.toString();
        // }
        @Override
        public String toString(){
            return "Student{" +
                    "name= '" + name + '\'' +
                    ", age= " + age +
                    '}';
        }

    }
   
}
```
Java also implictly calls the to String method on an objects, if you simply pass your object to System.out.println
```java
public class Main extends Object{
    public static void main(String[] args){
      Student max = new Student("Max", 21);
      System.out.println(max);

    PrimarySchoolStudent jimmy = new PrimarySchoolStudent("Jimmy", 8, "Carole");
    System.out.println(jimmy);
     
    }

    class Student {
        //instance variables
        private String name;
        private int age;
        //constructor
        Student(String name, int age){
            this.name = name;
            this.age = age;
        }
        @Override
        public String toString(){
            return name + " is " + age;
        }
    }

    class PrimarySchoolStudent extends Student{
        private String parentName;

        PrimarySchoolStudent(String name, int age, String parentName){
            super(name, age);
            this.parentName = parentName;
        }
        public String toString(){
            return parentName + "'s kid, " + super.toString();
        }
    }
}
// Max is 21
// Carole's kid, Jimmy is 8
```


 ### this vs super
 * The keyword **super** is used to access or call the parent class members(variables and methods)
 * The keyword **this** is used to class the current class members (variables and methods). `this` is required when we have a parameter with the same name as an instance variable (field).

We can use either of them anywhere in a class, except for static elements, like an static method. Any attempt to do so will lead to complie-time errors.

The keyword **this** is commonly used with constructors and setters, an optionally in getters(easier for begginers). In the example below we are using the `this` keyword in the contructor and setter since there is a parameter with the same name. In the getter we don't have any parameters so the keyword is optional.
 ```java
 class House{
    private String color;

    public House(String color){
        //this keyword is REQUIRED, sames parameter name as field
        this.color = color;
    }

    public String getColor(){
        //this is optional
        return color; //same as return this.color;
    }

    public void setColor(String color){
        //this keyword is REQUIRED , same parameter name as field
        this.color = color;
    }
 }
 ```
 The keyword `super` is commonly used with method overriding, when we call a method with the same name from the parent class. In the example below we have a method `printMethod` that call `super.printMethod`.

 Without adding the keyword `super()` it would end up being a recursive call. What that means is that the method will call itself forever or until memory is fully used in your computer


 ```java
 class SuperClass { //parent class aka super class
    public void printMethod(){
        System.out.println("Printed in Superclass");
    }

    class SubClass extedns SuperClass{
        //overrides method from parent
        @Override
        public void printMethod(){
            super.printMethod(); //Calls method in SuperClass (parent)
            System.out.println("Printed in SubClass");
        }
    }

    class MainClass {
        public static void main(String[] args){
            SubClass s = new SubClass();
            s.printMethod();
        }
    }

 }
 ```

 * In Java we have the `this()` call and the `super()` call. Notice the braces it is known as a call since it looks like a regular method call, although we're calling certain constructors. 
* Use `this()` to call a constructor from another overloaded constructor in the same class.
* The call to `this()` can only be used in a constructor, and it must be the first statement in a constructor. It's used with constuctor chaining, in other words when one constructor calls another constructor, and helps to reduce duplicated code.
* The only way to call a aprent constructor is by calling `super()`, which calls the parent constructor.
* The Java Compiler puts a default call to `super()` if we don't add it, and it s always the no-args super which is inserted by compiler (constructor without arguments.)
* The call to super() must be the first stamenet in each constructor
* Even abstract classes have constructors, although you can never instatiate and abstract class using the `new` keyword.
* An abstract class is stull a super class, so its constructors run when someone makes an instance of a concrete subclass.
* A constructor can have a call to `super()` or `this()` but never both.
```java
// BAD EXAMPLE OF CONSTRUCTORS
class Rectangle{
    private int x;
    private int y;
    private int width;
    private int height;

    public Rectangle(){
        this.x = 0;
        this.y = 0;
        this.width = 0;
        this.height = 0;
    }

    public Rectangle(int width, int height){
        this.x = 0;
        this.y = 0;
        this.width = width;
        this.height = height;
    }
    public Rectangle(int x, int y, int width, int height){
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }
}
```

Below, is what's known as **constructor chaining**, where the last constructor has the responsbility to initialize variables

```java
//GOOD EXAMPLE OF CONSTRUCTORS
class Rectangle{
    private int x;
    private int y;
    private int width;
    private int height;

    //1st Constructor
    public Rectangle(){
        this(0,0);  //calls 2nd constructor
    }

    //2nd Constructor
    public Rectangle(int width, int height){
        this(0, 0, width, height); // calls 3rd constructor
    }

    //3rd constructor
    public Rectangle(int x, int y, int width, int height){
        this.x = x;
        this.y = y;
        this.widht = width;
        this.height = height;
    }
}
```
In the following example we use both `super()` and `this()`
```java

class Shape {
    private int x;
    private int y;

    public Shape (int x, int y){
        this.x = x;
        this.y = y;
    }
}

   
class Rectangle extends Shape {
    private int width;
    private int height;

     //1st Constructor
     public Rectangle(int x, int y){
        this(x,y, 0,0);  //calls 2nd constructor
    }

    public Rectangle (int x, int y, int width, int height){
        super(x, y); //calls constructor from parent (Shape)
        this.width = width;
        this.height = height;
    }
}
```

### Method Overriding vs Overloading
**Method overloading** means providing two or more separate methods in a class with the same name but different parameters.
Method return type may or may not be different and that allows us to reuse the same method name.
Overloading is very handy, it reduces duplicate code and we don't have to remember multiple method names

We can overload static, or instance methods

To the code calling an overloaded methods, it looks like a single method can be called with different sets of arguments.

In actuality, each call that's made with a different set of arguments, is calling a separate method. 

Java developers often refer to method overloading, as compile-time polymorphism. This means the compier is determining the right method to call, based on the method name and argument list

Usually overloading happens within a single class, but methods can also be overloaded by subclasses. That's because, a subclass inherits over version of the method from the parent class then the subclass can have another overloaded version of that method.

**Method Overloading Rules**
Methods will be considered overloaded if both methods follow these rules:

- Methods must have the same method name
- Methods must have different parameters
- If methods follow the rules above thet may or may not
    * Have diffferent return types
    * Have different access modifier
    * Throw different checked or unchecked exceptions


**Method overriding** means defining a method in a child class that already exists in the parent class with the same signature(Same name, same arguments)
By extending the parent class the child class gets all the methods definied in the parent class(those methods are also known as *derived methods*)
Method overriding is also known as **Runtime Polymorphism** and **Dynamic Method Dispatch**, because the method that is going to be called is decided at runtime by the JVM
When we override a method it's recommended to put @Override immediately above the method definition. The @Override statement is not required, but its'a way to get the compiler to flag an error if you don't actually properly override this method. We will get an error, if we don't follow the overriding rules correctly
 
**Method Overriding Rules**
 Method will be considered overriden if we follow these rules:
    - It muust have same name and same arguments
    - Return type can be a subclass of the return type in the parent class
    - It can't have a lower access modifier: For example, if the parent method is protected then using private in the child is not allowed but using public in the child would be allowed.

There are also important point about method overriding to keep in mind:
- Only inherited methods can be overriden, in other word methods can be overriden only in child classes
- Contructors and private methods cannot be overriden.
- Methods that are final cannot be overriden.
- A subclass can use `super.methodname()` to call the superclass version of an overriden method.

```java
// OVERRIDING
class Dog{
    public void bark(){
        System.our.println("woof");

    }
}

class GermanSheperd extends Dog{
    
    @Override
    public void bark(){
        System.out.println("woof woof woof");    }
}
```

```java
// OVERloading
class Dog{
    public void bark(){
        System.our.println("woof");
    }

    public void bark(int number){
        for(int i =0; i < number; i++){
            System.out.println("woof");
        }
    }
}

```

**Covariant return type**
The return type of an overriden method can be the same type as the parent method's declaration. But it can also be a sublcass. The term, covariant return type is more appropiate.

We briefly mentioned, that there's a clone method on the class Object, that all classes inherit from.

A simplified look at this declaration, is shown below
```java
protected Object clone() throws CloneNotSupportedException
```
And if you override this method, by using IntelliJs code generation tools, it would generate this code in your class:
```java
@Override
protected Object clone() throws CloneNotSupportedExceptions{
    return super.clone();
}
```
But in general, when you're cloning an instance, you're going to want to return an Object, that's the same type as the Object you're cloning.
We sid all classes ultimately have Object, as a base class, so every class
can be said to be a covariant of Object.

```java
//The clone method overriden in a Person class
// This is calid override of Object's clone method
class Person {
    private String name;
    private String birthDat;

    public Person(String name, String birthDate){
        this.name = name;
        this.birthDate = birthDate;
    }
    @Override
    public Person clone(){
        return new Person(name, birthDate);
    }
}

```

