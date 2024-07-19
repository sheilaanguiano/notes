# Python

## Basics

Python is a general purpose language, so it can be use to be built almost anything.

hello.py
```python
print("Hello World")
```
You might notice that when referring to files, they're usually called *script*, that'e because we're going to pass this file to what is known as the **Python Interpreter** which will evaluate the file.

From the terminal we could run this scrip using

```terminal
python hello.py
```

### Python Shell

You can use the interpreter in a more exploratory interctive way with thePython REPL (Read, Evaluate, Print, Loop), which is often referred ad the **Python Shell**. 

- To open it, you simply need to write `Python` in the terminal, which you'll see it open when you see three chevrons (>>>)
- Remember to only use lowercase, Python is case sensitive
Press `Q` to get out of it, or type `exit()` or Ctrl+ D

### Variables
Python uses (snake_case)[https://en.wikipedia.org/wiki/Snake_case] to name variables
```python
first_name = "Ada"
print (first_name, "is learning Python")  #Ada is learning Python
```
#### Input
```python
first_name = input("What is your first name?  ")
print("Hello,", first_name)
print(first_name, "is learning Python)

``` 
### Types and Branching
Python has the following data types built-in by default, in these categories:
In Python, the data type is set when you assign a value to a variable


Text Type:	`str`
Numeric Types:	`int`, `float`, `complex`
Sequence Types:	`list`, `tuple`, `range`
Mapping Type:	`dict`
Set Types:	`set`, `frozenset`
Boolean Type:	`bool`
Binary Types:	`bytes`, `bytearray`, `memoryview`
None Type:	`NoneType`



#### Numeric
```
>>> int (“11”) 
11
>>> float(“11”)
11.0
>>>float (11)
11.0
>> int(11.9)
11
>>> 23/3
7.666666667
>>> 23 // 3
7
>>> 23 % 3
2

```

#### String and Operators
* Strings are immutable
* String literals can be made with single or double quotes
* You can use triple quotes, when your string uses single or double quotes
