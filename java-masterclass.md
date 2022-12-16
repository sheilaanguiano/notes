# Java Programming Masterclass
-----

Author: Sheila Anguiano
Course: Java Masterclass(Udemy)
Instructor: Tim Buchalka

-----

# Table of Contents

1. Programming Tools and Setup (#2)


## Section 2: Programming Tools and Setup <a name="2"></a>
### Confirming Installation and intro to JShell
* Check in your terminal your java version `java -version`
* IntelliJ is an integrated development environment or IDE to develop Java code.
* JShell became a standard component of the JDK (Java Development Kit) in Java9 it's a REPL.
* Launch jshell writting in the terminal `jshell`, inside if you writte `/help` you'll get a list of commands that you can use.



## Section 3: First Steps
### Primitive Types Recap and the String Data Type
A String is a sequence of characters. In the case of the **char**, it could contain a **single character** only (a regular character or Unicode character). Technically  it's limited by memory or the MAX_VALUE of an **int** which was 2.14 billion.

Strings in Java are immutable. That measn you can't change a String after it's created, what happen si a new String is created.

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
## Expressions, Statements, Code blocks, Methods
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

## Section 5: Control Flow
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

## Reading User Input
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

## Section 6 OOP Part 1 - Classes
### Classes
Software objects are a fundamental part of Object-oriented programming. They're very similar to real world objects because they also consist of state and behaviors.

A software object store its state in **fields** and we now fields as variables, and they expose their behavior with **methods**

A **class** is like a template or a blueprint for creating objects. Class could be thought of as a powerful user-defined data type, sort of an extra data type, this is not correct in the true meaning, but it give us an idea  of what classes really 

- Classes should start with uppercase letters
- **public** is an access modifier. This modifier determines what access we want to allow others to have to this new class. So in this case **public** means unrestricted access to the class.
- **private** is wfor where no other class can access that class.
- **protected** which allows classes in this package to access your class
- Local variables are only used inside the method they have been initialized.

Classes allow us to create variables that can be seen and are accesible from anywhere within the class that we're creating. These are know as **class or member variables** but most commonly referred as **fields**. When creating a field for a class, you need to also specify an access modifier that works the same way as the access modifier for a class definition. As a general rule, when you're defining fields in Java in a class, you go with the access modifier **private** , unlike the class where we've gone with *public*

So what private means when talking about fields, what we're really doing with it is we're adhering to **encapsulation**, which is a key fundamental rule of object-oriented programming. So encapsulation in Java is usded to hide the fuelds and methods from access publicly.

```java
public class Car {
    //generally you'll always go with private
    //these variables are the state component for Car
    //This is the sate which we're defining as fields
    private int doors;
    private int wheels;
    public String model;
    private String engine;
    private String colour;

}
```
Now we can go to the *Main* class.
```java
public class Main {
    public static void main(String[] args) {
        //This is how we define an object of type Car
        //When we add the `= new Car` we're initializing
        Car porsche = new Car();
        Car holden = new Car();
        //This is one way to access the data, but NOT a good one as it more or less 
        // violates the rules of encapsulation.
        porsche.model = "Carrera";

    }
}
```
Now, we'll add a method that will let us update the model
```java
public class Car {

    private int doors;
    private int wheels;
    private String model;   //field
    private String engine;
    private String colour;
                                //param
    public void setModel(String model){
        this.model = model;

    }

    public String getModel(){
        return this.model;
    }

}
```
The above code introduces another problem, since you have 2 different types of variables, we have the field in `private String model;` and we have the parameter in our method with the same name, so to distinguish them, in this case we use `this` when you're referring to the field. So now we can set our model correctly with the method
```java
public class Main {
    public static void main(String[] args) {
        Car porsche = new Car();
        Car holden = new Car();
        porsche.setModel("Carrera");

    }
}
```
When you cretae classes, you need to initilize them with the word `new`.
Advantages of Getters and Setters
- Validation


```java
public class Car {
                                //param
    public void setModel(String model){
        String validModel = model.toLowerCase();
        if(validModel.equals("porsche") || validModel.equals(""holden)){
            this.model = model;
        } else {
            this.model = "Unknown";
        }
        

    }
```
### Contructors
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

    public Account(String number, double balance, String customerName, String customerEmail,
                   String customerPhone){
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
- Constructors can be overlaoded, so we can call a constructor from another constructor, like some constructor with some default values
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

### Inheritance
Object Orinetyed programming allows us to create classes to inherit commonly used standard behavior from other classes
```java
/********
  BASE CLASS
 ***********/

public class Animal {
    //fields
    private String name;
    private int brain;
    private int body;
    private int size;
    private int weight;

    //constructor


    public Animal(String name, int brain, int body, int size, int weight) {
        this.name = name;
        this.brain = brain;
        this.body = body;
        this.size = size;
        this.weight = weight;
    }

    //create a Getter for each field


    public String getName() {
        return name;
    }

    public int getBrain() {
        return brain;
    }

    public int getBody() {
        return body;
    }

    public int getSize() {
        return size;
    }

    public int getWeight() {
        return weight;
    }
}
```
In Java terminology, if you want to **inherit** from another class, you use the word `extends`. Now to make it word we need to be able to call the cosntructor from the Animal class to initialize it.
```java
public class Dog extends Animal {
    //Using IntelliJ command+N you can create the constructor
    //What super means is to call the constructor that is for the class that we're
    //extending from.

    public Dog(String name, int brain, int body, int size, int weight) {
        super(name, brain, body, size, weight);
    }
}
```
And now we can add specific characteristics to a dog:
```java
public class Dog extends Animal {
    //Using IntelliJ command+N you can create the constructor
    //What super means is to call the constructor that is for the class that we're
    //extending from.

    private int eyes;
    private int legs;
    private int tail;
    private int teeth;
    private String coat;

    public Dog(String name, int brain, int body, int size, int weight, int eyes, int legs, int tail, int teeth, String coat) {
        super(name, 1, 1,  size, weight);
        this.eyes = eyes;
        this.legs = legs;
        this.tail = tail;
        this.teeth = teeth;
        this.coat = coat;
    }

    private void chew(){
        System.out.println("Dog.chew() called");
    }

    @Override
    public void eat() {
        System.out.println("Dog.eat called");
        chew();
        super.eat();
    }
}
```
We cal also override a method from the Animal class (or super class), additionally by using the word super or not inside a method, you can control what is being called, by using the word super, the method will directly go to the super class ignoring any override methods that could be applicable
```java
    public void walk(){
        System.out.println("Dog.walk() called");
        super.move(5);
    }
// Dog.walk() called
// Animal.move() called. Animal is moving at 5

    public void run(){
        System.out.println("Dog.run() called");
        //We're calling the Animal.move
        move(10);

    }
// Dog.run() called
// Dog.move() called
// Dod.moveLegs() called
// Animal.move() called. Animal is moving at 10

```
### Reference vs Object vs Instance vs Class in the context of Java
 Let's use the analogy of buidling a house to understand Classes
 * A **class** is basically a blueprint for a house, using the blueprint (pnas) we can build as many houses as we like based on those plans.
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

 ### this vs super
 * The keyword **super** is used to access/ call the parent class members(variables and methods)
 * The keyword **this** is used to class the current class members (variables and methofs) is required when we have a parameter with the same nae as an instance variable (field).

We can use both of them anywhere in a class except static areas (the static block or a static method). Any attempt to do so will lead to complie-time errors.

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
 The keyword super is commonly used with method overriding, when we call a method with the sam ename from the parent class. In the example below we have a method `printMethod` that call `super.printMethod`

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

 * In Java we have the `this()` call and the `super()` call. Notice the braces it is known as a call since it looks like a regular method call 
* Use `this()` to call a constructor from another overloaded constructor in the same class.
* The call to `this()` can be used only in a constructor, and it must be the first statement in a constructor. It's used with constuctor chaining, in other words when one constructor calls another constructor, and helps to reduce duplicated code.
* The only way to call a aprent constructor is by calling `super()`. This calls the parent constructor.
* The Java Compiler puts a default call to `super()` if we don't add it, and it s always the no-args super wich is inserted by compiler (constructor without aarguments.)
* The call to super() must be the first stamenet in each constructor
* Even abstract classes have constructors, although you can never instatiate and abstract class using the `new` keyword.
* An abstract class is stull a super class, so its constructors run when someone makes an instance of a concrete subclass.
* A constructor can have a call to `super()` or `this()` but never both.
```java
//GOOD EXAMPLE OF CONSTRUCTORS
class quadrilateral{
    private int x;
    private int y;
    private int width;
    private int height;

    //1st Constructor
    public quadrilateral(){
        this(0,0);  //calls 2nd constructor
    }

    //2nd Constructor
    public quadrilateral(int width, int height){
        this(0, 0, width, height); // calls 3rd constructor
    }

    //3rd constructor
    public quadrilateral(int x, int y, int width, int height){
        this.x = x;
        this.y = y;
        this.widht = width;
        this.height = height;
    }
}
```
In the following example we use both `super()` and `this()`
```java

class shape {
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
* Method **overloading** means providng two or more separate methods in a class with the same name but different parameters.
* Method return type may or may not be different and that allows us to reuse the same method name.
* Overloading is very handy, it reduces duplicate code and we don't have to remember multiple method names
* Overloading does not have anything to do with polymorphism but Java developers often refer to overloading as Compile Time Polymorphism
* In other words the compiler decided which method is going to be called based on the method name, return type and argument list.
* Usually overoading happens inside a single class, but a method can also be treated as overloaded in the subclass of that class
* That is becase a subclass inherits one version of the method from the parent class and then the subclass can have another overloaded version of the method

**Method Overloading Rules**
- Methods must have the same method name
- Methods must have different parameters
- If methods follow the rules above thet may or may not
    * Have diffferent return types
    * Have different access modifier
    * Throw different checked or unchecked exceptions

* Method **overriding** means defining a method in a child class that already exists in the parent class with the same signature(Same name, same arguments)
* By extending the parent class the child class gets all the methods definied in the parent class(those methods are also known as *derived methods*)
* Method overriding is also known as **Runtime Polymorphism** and **Dynamic Method Dispatch**, because the method that is going to be called is decided at runtime by the JVM
* When we override a method it's recommended to put @Override immediately above the method definition. This is an annotation that the compiler reads and will then show us an error i we don't follow overriding rules correctly.
* We can't override static methods only instance methods 

**Method Overriding Rules**
- Method will be considered overriden if we follow these rules:
    - It muust have same name and same arguments
    - Return type can be a subclass of the return type in the parent class
    - It can't have a lower access modifier: For example, if the parent method is protected then using private in the child is not allowed but using public in the child would be allowed.

There are also important point about method overriding to keep in mind:
- Only inherited methods can be overriden, in other word methods van be overriden only in child classes
- Contructors and private methods cannot be overriden.
- Methods that are final cannot be overriden.
- A subclass van use `super.methodname()` to call the superclass version of an overriden method.

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
```java
class Burger{
    // fields, methods...
}

class HealthyBurger extends Burger{
    //fields, methods...
}
```
```java
class BurgerFactory{
    public Burger createBurger(){
        return new Burger();
    }
}

class HealthyBurgerFactory extends BurgerFactory{
    
    @Override
    public HealthyBurger extends BurgerFactory{
        return new HealthyBurger();
    }

}

```
We can notice in the above example how the return types are different and that's know as a **covariant return** type, so in other words the `Burger` class is the parent class and the `HealthyBurger` is child class, so the method create burger in the class `HealthyFactoryBurger` can return any child type of burger, in this case we've just got one child class

### Static vs Instance Methods
**Static Methods**
- Static methods are declared using the **static** modifier
- Static methods can access instance methods and instance variables directly
- They are usually used for operations that don't require any data from an instance of the class (from `this`). The `this` kwyord is the current instance of a class
- In static methods we can't use the this keyword
- Whenever you see a methods that doesn't use **instance variables** that method should be declared a **static method**. For example mian is a static method and it is called by the JVM when it starts an application
```java
class Calculator{
    public static void printSum(int a, int b){
        System.out.println("sum= " + (a+b));
    }
}

public class Main{
    public static void main(String[] args){
        Calculator.printSum(5,10);
        printHelo();
    }

    public static void printHello(){
        System.out.println("Hello");
    }
}

//static methods are called as ClassName.methodName(); or
//methodName(); only if in the same class.
```
**Instance Methods**
- Instance methods belong to an instance of a class
- Tou use an instance method we have to instatiate the class first usually by using the `new` keyword
- Instance methods can access instance methods and instance variables directly
- Instance methods can also access static methods and static variables directly.
```java
class Dog{
    public void bark(){ //Since it doesn't have static, this is a standard instance method
        System.out.println("woof"); 
    }
}
public class Main{
    public static void main(String[] args){
        Dog rex = new Dog();
        rex.bark();
    }
}
```
Should a Method be static: If it uses any fields(isntace variables) or instance methods, it should probably be an *instance method* otherwise it should proably be a *static method*