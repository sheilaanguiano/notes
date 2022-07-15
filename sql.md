# JavaScript
-----

Author: Sheila Anguiano

-----
# Table of Contents 
1. [SQL Basics](#sql)
2. [Modifying Data with SQL](#modifiying-sql)

## SQL Basics <a name="sql"></a>
### Data, Databases and SQL
#### Data is Everywhere

SQL the specialized programming language to get information from databases

#### Data is Everywhere
Databases are everywhere. Information is data and there a multiple implementation examples. Amazon item lists, reviews, etc

A database is a tool for storing massive amounts of information that can be retrieved at a later point in time.

#### Talking to Databases with SQL
In order to communicate with a database, you've got to speak it's language. SQL (Structured Query Language) is a specialized programming language used for interacting with databases for example, reading information from a database.

Querying - Reading data from a database

There are many databases that understand SQL, such as:
* MySQL
* PostgreSQL
* SQLite
* Microsoft SQL Server
* Oracle

Other Databases that used more specialized methods, such as this NoSQL databases
 * MongoDB
 * CouchBase
 * Redis

[https://en.wikipedia.org/wiki/SQL](https://en.wikipedia.org/wiki/SQL)

#### Organizing Data with Databases
Databases allow users to store data in well defined sections. This keeps the data uniform. However, the SQL you write can show the data in different ways which is handy for reporting subsets of data.

There are two important components to each database:
* The information that's stored in it, called **data**
* How the data is organized called **the schema**

The schema establishes how that data should be stored and divided into different sections, and it further determines how each of the sections relates to other sections. These sections are called **tables**. **Rows** run from left to right horizontallu, and the **columns** run top to bottom vertically.

Typically, each table contains data for a specific type of thing 

[https://en.wikipedia.org/wiki/Database_schema](https://en.wikipedia.org/wiki/Database_schema)

#### Types of Data
There are good reasons why your data should be categorized in to different types

-   Text Type Examples
    -   TEXT - Store names and descriptions
    -   VARCHAR
-   Numeric Type Examples
    -   INT
    -   INTEGER
-   Date Type Examples
    -   DATETIME
    -   DATE
    -   TIMESTAMP

Having correct data types in your database not only helps with sorting but it also comes in handy for many other applications such as generating mathematical operations on numeric type data.

[MySQL data typesl](https://dev.mysql.com/doc/refman/5.7/en/data-types.html)
[SQLite data typesl](https://www.sqlite.org/datatype3.html)
[PostgresSQL data typesl](https://www.postgresql.org/docs/8.4/datatype.html)
[Microsoft data types](https://docs.microsoft.com/en-us/sql/t-sql/data-types/data-types-transact-sql?redirectedfrom=MSDN&view=sql-server-ver15)

### Getting Data form a Database
Reading information is the most common operation performed on a database. Whether you're a Business Analyst, Web Developer or Mobile App developer reading from databases is a must have skill.
#### Your first SQL statement

**Syntax**  The vocabulary and grammatical rules surrounding the structure of your code.

**Keywords**  The vocabulary words of a programming language used to issue commands to a computer.

**Statement or Query** Lines of SQL code

* Running a QUERY or executing the SQL  
```sql
SELECT * FROM <table name>;
```
The asterisk or star symbol (`*`) means all columns.
The semi-colon (`;`) terminates the statement like a period in sentence or question mark in a question.

#### Retrieving Specific Columns of Information
Retrieving a single column:

```sql
SELECT <column name> FROM <table name>; 
```
Examples:
```sql
SELECT email FROM users;
SELECT first_name FROM users;
SELECT name FROM products;
SELECT zip_code FROM addresses;
```
Retrieving multiple columns:
```sql
SELECT <column name 1>, <column name 2>, ... FROM <table name>;
```
Examples:

```sql
SELECT first_name, last_name FROM customers;
SELECT name, description, price FROM products;
SELECT title, author, isbn, year_released FROM books;
SELECT name, species, legs FROM pets;
```

[SQL Basics Cheatsheet](https://github.com/treehouse/cheatsheets/blob/master/sql_basics/cheatsheet.md)

#### Categorizing your Output with 'AS'
You're not restricted to displaying the column names from the table at the top of your results. You can specify your own names for result sets.

Be mindful that SQL in different settings may have slight variations in syntax.

```sql
SELECT <column name> AS <alias> FROM <table name>;
SELECT <column name> <alias> FROM <table name>;
```

Examples:

```sql
SELECT username AS Username, first_name AS "First Name" FROM users;
SELECT title AS Title, year AS "Year Released" FROM movies;
```

People use uppercase keywords to help you distinguish the different parts of the query, making it an industry best practice.
```sql
-- This is a SQL comment.
```

### Finding the Data you Want
Instead of getting all the information back at once isn't always what you want. Finding the information want by writing specialized SQL queries is the way to do it.

##### A  `WHERE`  Clause
```sql
SELECT <columns> FROM <table> WHERE <condition>;
```
##### Equality Operator
Find all rows that a given value matches a column's value.
```sql
SELECT <columns> FROM <table> WHERE <column name> = <value>;
```
Examples:
```sql
SELECT * FROM contacts WHERE first_name = "Andrew";
SELECT first_name, email FROM users WHERE last_name = "Chalkley";
SELECT name AS "Product Name" FROM products WHERE stock_count = 0;
SELECT title "Book Title" FROM books WHERE year_published = 1999;

```
##### Inequality Operator
Find all rows that a given value doesn't match a column's value.
```sql
SELECT <columns> FROM <table> WHERE <column name> != <value>;
SELECT <columns> FROM <table> WHERE <column name> <> <value>;
```

The not equal to or inequality operator can be written in two ways  `!=`  and  `<>`. The latter is  _less_  common.

Examples:

```sql
SELECT * FROM contacts WHERE first_name != "Kenneth";
SELECT first_name, email FROM users WHERE last_name != "L:one";
SELECT name AS "Product Name" FROM products WHERE stock_count != 0;
SELECT title "Book Title" FROM books WHERE year_published != 2015;
```

#### Filtering by Comparing Values
##### Relational Operators

There are several relational operators you can use:

-   `<`  less than
-   `<=`  less than or equal to
-   `>`  greater than
-   `>=`  greater than or equal to

These are primarily used to compare  _numeric_  and  _date/time_  types.

#### SQL Used

```sql
SELECT <columns> FROM <table> WHERE <column name> < <value>;
SELECT <columns> FROM <table> WHERE <column name> <= <value>;
SELECT <columns> FROM <table> WHERE <column name> > <value>;
SELECT <columns> FROM <table> WHERE <column name> >= <value>;

```

Examples:

```sql
SELECT first_name, last_name FROM users WHERE date_of_birth < '1998-12-01';
SELECT title AS "Book Title", author AS Author FROM books WHERE year_released <= 2015;
SELECT name, description FROM products WHERE price > 9.99;
SELECT title FROM movies WHERE release_year >= 2000;
```

Filtering on 

## Modifiying Data with SQL <a name="modifying-sql"></a>
At the heart of a dynamic application is a database. Whether the application is an eCommerce, sports team, social network or a productivity app on your phone the data needs to change over time.

In this course we'll take a look at the underpinning SQL statements that are needed for every dynamic application.
### Adding Data to a Database
#### Introduction to CRUD
##### Adding a Row to a Table
[Cheatsheet](https://github.com/treehouse/cheatsheets/blob/master/modifying_data_with_sql/cheatsheet.md)
#### Adding Multiple Rows in a Single Statement
You tend to see multiple statements like this in files that set up the initial state of a database called **database seed files**. You're seeding files into the database.

### Updating Data in a Database
With dynamic applications, things change all the time. For example, the stock counts of products or the scores in a live soccer match. We need a way to update the data. In this stage we'll discover how to do just that.
#### Updating All Rows in a Table
The equal sign in this case is not doing the same thing as what it would do in a condition in a WHERE clause. In the WHERE clause, it's the equal to and equality operator. In the UPDATE statement, it's known as an assignment operator.

### Deleting Data From a Database
There will come a time where you don't need certain data anymore. In this stage we'll look at removing all of the data from a table and how to remove specific rows too.
#### Removing Data from al Rows in a Table
It's important to note, that once you delete a table, you **CAN'T undo this** without a backup of your data, you can't restore it.
#### Removing Specific Rows
The change is permanent, so be sure  you're deleting exactly what you want to be removed.

### Handling Errors when Manipulating Data
Sometimes you need to do multiple CRUD operations in a single go. This is where errors can occur. We'll tackle this with something called transactions.
#### Introduction to Transactions
When you write a statement that performs one of the CRUD operations, you need to be certain that the SQL statement you write and run is exactly what you want to get executed. 
In a production environment, it can be difficult to revert to an earlier state, this is because in most circumstances your statements are run in autocommit mode, meaning what you execute gets committed or saved to disk. Most databases have autommit switched on by default. You may not want this to happen all of the time, specially when you want something like batch operations, meaning you want to do multiple statements that get executed together.

Imagine youre populating a database for the first time or **seeding**. Running multiple statements are normally prepared in a SQL file, also known as a **script**, and the computer freezes, if we run the script again, we can get duplicates or an error. So the way to disable autocommit and commit at the end of the batch, using transactions

Switch autocommit off and begin a transaction:
```sql
BEGIN TRANSACTION;
```

Or simply:
```sql
BEGIN;
```

To save all results of the statements after the start of the transaction to disk:
```sql
COMMIT;
```
 
#### Rolling Back from Transactions
 Sometimes errors happen in the middle of a transaction. How do you recover from that? This video shows you how!

#### Databases with Frameworks
Many developers, while using databases, aren't required to write a single line of SQL code. They use special software libraries called ORMs. It's a way for developers to yse another programming language other than SQL to interface with a database and perform CRUD operations.

In this course, you've learned all CRUD operations , or what's called DML or data manipulation language. There's a lot more to SQL, such as database design and maintenance, but this si where you'll spend most of your time.


[Hibernate for Java](http://hibernate.org/)
[CoreData for Swift](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/index.html)
[ActiveRecord for Ruby](https://api.rubyonrails.org/classes/ActiveRecord/Base.html)
