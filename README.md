# MySQL guide sheet
1. [Basic MySQL commands](#basic-mysql-commands)
    * [List all available dabaseses](#-list-all-available-dabaseses-)
2. [Table](#table)
3. [Inserting Data](#inserting-data)
4. [Selecting/Retrieving/Reading data](#selectingretrievingreading-data)
5. [Filtering data/records](#filtering-datarecords)
6. [Updating data](#updating-data)
7. [Deleting data](#deleting-data)
8. [Selection Refining](#selection-refining)
9. [MySQL string functions](#mysql-string-functions)
10. [Aggregate Functions](#aggregate-functions)
11. [Extras](#extras)

## Basic MySQL commands

### ▶ List all available dabaseses :
```
show databases;
```

### ▶ Command for creating a database :
```
CREATE DATABASE <database_name>;
```

### ▶ To drop(delete) a database :
```
DROP DATABASE <database_name>;
```

### ▶ For using(selecting) a database :
```
USE <database_name>;
```

### ▶ Show currently using(selected) database :
```
SELECT database();
```

### ▶ Display information about errors, warnings, and notes :
> This command will display information about the conditions (errors, warnings, and notes) resulting from executing a statement in the current session.

```
SHOW WARNINGS;
```

----------------------------------------------------------------------------------------------
### ▶ Run MySQL commands from the file :

* Create a file with `.sql` file extension
* `cd` into the file directory
* Run MySQL in that directory with this command `mysql -u root -p`
* To run the SQL commands from the file run `source file_name.sql`

----------------------------------------------------------------------------------------------

----------------------------------------------------------------------------------------------
## Table 

### ▶ Generic version of creating a table :
```
CREATE TABLE <table_name>
(
    <column_name1> <data_type>,
    <column_name2> <data_type>
);
```
> By default with the command above, the table column cell will accept `Null` values. But we can disable accepting `NULL` values while creating table by the command bellow:

```
CREATE TABLE <table_name>
(
    <column_name1> <data_type> NOT NULL,
    <column_name2> <data_type> NOT NULL
);
```
> To set default values to the columns while creating a table we can use the command bellow: (Default value must have to match with the data type)

```
CREATE TABLE <table_name>
(
    <column_name1> <data_type> DEFAULT <default_value>,
    <column_name2> <data_type> DEFAULT <default_value>
);
```
> Example :

```
CREATE TABLE cats
(
    name VARCHAR(100) NOT NULL DEFAULT 'unnamed',
    age INT NOT NULL DEFAULT 00
);
```

### ▶ Creating table with primary key :
> The `PRIMARY KEY` uniquely identifies each record in a table. A table can have only **One** Primary key. Primary keys must contain **Unique** values, and it can not contain **Null values**

> Example: 

```
CREATE TABLE unique_cats 
(
    cat_id INT NOT NULL,
    name VARCHAR(50), 
    age INT,
    PRIMARY KEY (cat_id)
);
```

> Alternative Example :

```
CREATE TABLE unique_cats 
(
    cat_id INT NOT NULL PRIMARY KEY,
    name VARCHAR(50), 
    age INT
);
```
> We can also add `AUTO_INCREMENT` to the primary key so that the primary key value can automatically increment. 
> Example:

```
CREATE TABLE unique_cats 
(
    cat_id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(50), 
    age INT,
    PRIMARY KEY (cat_id)
);
```

### ▶ Show all the tables in a database :
```
SHOW TABLES;
```

### ▶ Show all the columns form a specific table :
```
SHOW COLUMNS FROM <table_name>;
```
> Alternative (Describing a table)

```
DESC <table_name>;
```

### ▶ Droping(Deleting) a table :
```
DROP TABLE <table_name>;
```
----------------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------------
## Inserting Data 

### ▶ Inserting `single` data into the table :
```
INSERT INTO <table_name> (column_name)
VALUES (value);
```

> Example :

```
INSERT INTO cats (name, age)
VALUES ('Mini', 12);
```

### ▶ Inserting `Multiple` data into the table :
```
INSERT INTO <table_name> (column1_name, column2_name)
VALUES  (column1_value1, column2_value1),
        (column1_value2, column2_value2),
        (column1_value3, column2_value3);
```
----------------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------------
## Selecting/Retrieving/Reading data
The `SELECT` statement is used to fetch data from a database **table**.
 
### ▶ Fetch all the available column data from the table :
```
SELECT * FROM <table_name>;
```
> In here, `*` means give all the available columns from the table.


### ▶ Fetch specific column/columns data from the table :
```
SELECT <col_name> FROM <table_name>;

or,

SELECT <col1_name>, <col2_name> FROM <table_name>;
```

----------------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------------
## Filtering data/records
### ▶ Fetch column/columns data from the table with condition using `WHERE` :
> The `WHERE` clause is used to specify a condition while fetching the data from a single table or by joining with multiple tables. If the given condition is satisfied, then only it returns a specific value from the table.

```
SELECT column1, column2
FROM table_name
WHERE [condition];
```

> The `WHERE` clause is not only used in the `SELECT` statement, but it is also used in the UPDATE, DELETE statement etc.

### ▶ `AND`, `OR` and `NOT` Operators :
The WHERE clause can be used with `AND`, `OR`, and `NOT` operators.

* The `AND` operator displays a record if all the conditions separated by `AND` are TRUE.
* The `OR` operator displays a record if any of the conditions separated by `OR` is TRUE.
* The 'NOT' operator displays a record if the condition(s) is NOT TRUE.



```
SELECT column1, column2, ...
FROM <table_name>
WHERE condition1 AND condition2 AND condition3;

---------------------------

SELECT column1, column2, ...
FROM <table_name>
WHERE condition1 OR condition2 OR condition3;

---------------------------

SELECT column1, column2, ...
FROM <table_name>
WHERE NOT condition;
```

> We can also use AND, OR and NOT operators together.


### ▶ `BETWEEN` Operator :
The `BETWEEN` operator selects values within a given range. The values can be numbers, text, or dates. The `BETWEEN` operator is inclusive: begin and end values are included.

```
SELECT <column_name>
FROM <table_name>
WHERE <column_name> BETWEEN value1 AND value2;
```

> We can also use AND, OR and NOT operators with BETWEEN.

----------------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------------
## Updating data
The `UPDATE` statement is used to update existing data in a **table**.
 
### ▶ Update/Alter existing data in a table :
```
UPDATE <table_name>
SET column1=value, column2=value2
WHERE <some_column>=<some_value>;
```
----------------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------------
## Deleting data
The `DELETE` statement is used to delete records from a **table**:
 
### ▶ Delete `Single` data from a table :
```
DELETE FROM <table_name>
WHERE <some_column> = <some_value>;
```
### ▶ Delete `Every/all` data from a table :
```
DELETE FROM <table_name>;
```
----------------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------------
## Selection Refining

### ▶ Using `DISTINCT` :
> The `SELECT DISTINCT` statement is used to return only distinct (different/unique) values from a collumn.

```
SELECT DISTINCT <col1_name> FROM <table_name>;
```
Or,
```
SELECT DISTINCT <col1_name>, <col2_name> FROM <table_name>;
```

### ▶ Sorting data with `ORDER BY` :
> The `ORDER BY` keyword is used to sort the result-set in **ascending** or **descending** order. It sorts the records in **ascending** order by default. To sort the records in descending order, use the `DESC` keyword.

```
SELECT <col1_name>, <col2_name>
FROM <table_name>
ORDER BY <col1_name>, <col2_name>, ... ASC|DESC;  
```
Examples:
```
SELECT * FROM Customers
ORDER BY Country;

Or,

SELECT * FROM Customers
ORDER BY Country DESC; 

Or,

SELECT
    title,
    released_year, 
    pages
FROM
    books
ORDER BY
    released_year DESC,
    pages ASC;
```

### ▶ Using `LIMIT` :
> The `LIMIT` clause is used in the `SELECT` statement to specify the number of records to return. The general syntax is given bellow:

```
SELECT <col1_name>, <col2_name>
FROM <table_name>
ORDER BY <col1_name>
LIMIT <offset>, <row_count>
```
Examples:
```
SELECT title, released_year FROM books
ORDER BY released_year DESC LIMIT 10;

Or,

SELECT title, released_year FROM books
ORDER BY released_year DESC LIMIT 10, 50;
```

### ▶ Searches with `LIKE` :
> The `LIKE` operator is a logical operator that tests whether a string contains a specified pattern or not. It is  is used in a `WHERE` clause.

There are two wildcard characters often used for constructing patterns. 

* The percent sign (%) represents zero, one, or multiple characters
* The underscore sign (_) represents one, single character


| LIKE Operator | Description |
|------|------|
| WHERE CustomerName LIKE `a%` | Finds any values that starts with "a" |
| WHERE CustomerName LIKE `%a` | Finds any values that ends with "a" |
| WHERE CustomerName LIKE `%or%` | Finds any values that have "or" in any position |
| WHERE CustomerName LIKE `_r%` | Finds any values that have "r" in the second position |
| WHERE CustomerName LIKE `a__%` | Finds any values that starts with "a" and are at least 3 characters in length |
| WHERE ContactName LIKE `a%o` | Finds any values that starts with "a" and ends with "o" |

> Note: If we want to  search something where string contains percent sign (%) or underscore sign (_) then we have to use backslash (\\) before it. Example: `%\%%` Or, `%\_%`

Syntax :
```
SELECT <col1_name>, <col2_name>
FROM <table_name>
WHERE <col1_name>
LIKE <pattern>
```
Examples:
```
SELECT title FROM books WHERE title LIKE '%the%';

Or, 

SELECT title, author_fname FROM books WHERE author_fname LIKE 'da%';
```

----------------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------------
## MySQL string functions

### ▶ Concatination/Combining :
> We can cancat/combine multiple fields' value together with `CONCAT()`string function. It returns concatenated string. The general syntax is given bellow.

```
CONCAT(col1_name, col2_name, col3_name)
```

> We can also use text in between

```
CONCAT(col1_name, 'text', col2_name, 'text')
```

> `CONCAT()` must have to use with `SELECT`

```
SELECT CONCAT(col1_name, col2_name) FROM <table_name>;
```
Or,
```
SELECT CONCAT(col1_name, col2_name) AS <alias_name> FROM <table_name>;
```

### ▶ Concatination/Combining with separator :
> `CONCAT_WS()` Same as the `CONCAT()` but the first argument is the separator for the rest of the arguments. The separator is added between the strings to be concatenated.

```
CONCAT_WS('<separator>', col1_name, col2_name, col3_name)
```
```
SELECT CONCAT_WS('<separator>', col1_name, col2_name) AS <alias_name> FROM <table_name>;
```

### ▶ Substring :
> `SUBSTRING()` Or `SUBSTR()` used to get the parts of the string. The general syntaxes are:

```
SUBSTRING(<string>, <position>)
```
```
SUBSTRING(<string> FROM <position>)
```
```
SUBSTRING(<string>, <position>, <length>)
```
```
SUBSTRING(<string> FROM <position> FOR <length>)
```

**Examples:**

```
mysql> SELECT SUBSTRING('Quadratically',5);
        -> 'ratically'
mysql> SELECT SUBSTRING('foobarbar' FROM 4);
        -> 'barbar'
mysql> SELECT SUBSTRING('Quadratically',5,6);
        -> 'ratica'
mysql> SELECT SUBSTRING('Sakila', -3);
        -> 'ila'
mysql> SELECT SUBSTRING('Sakila', -5, 3);
        -> 'aki'
mysql> SELECT SUBSTRING('Sakila' FROM -4 FOR 2);
        -> 'ki'
```

### ▶ Replace :
> `REPLACE()` function replaces all occurrences of a substring within a string, with a new substring.

**Syntax:**

```
> REPLACE(<string>, <from_string>, <new_string>)

> SELECT REPLACE(<column_name>, <from_string>, <new_string>) FROM <table_name>;
```

> Note: It performs a case-sensitive match when searching for `<from_string>`

**Examples:**

```
mysql> SELECT REPLACE('Hello World', 'l', '7');
        -> 'He77o Wor7d'
mysql> SELECT REPLACE('Hello World', 'o', '0');
        -> 'Hell0 W0rld'
```

**_The full reference of the string functions can be found_** [here](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html "MySQL string functions").

----------------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------------
## Aggregate Functions

### ▶ SQL `COUNT` :
> The COUNT() function returns the number of records returned by a select query.

Examples:
```
SELECT COUNT(*) FROM books;
```
```
SELECT COUNT(author_fname) FROM books;
```
```
SELECT COUNT(DISTINCT author_fname) FROM books;
```
```
SELECT COUNT(DISTINCT author_fname, author_lname) FROM books;
```
```
SELECT COUNT(*) AS count FROM books WHERE title LIKE '%the%';
```

### ▶ SQL `GROUP BY` :
> The `GROUP BY` statement groups rows that have the same values into summary rows, like "find the number of customers in each country".

> The `GROUP BY` statement is often used with aggregate functions `COUNT(), MAX(), MIN(), SUM(), AVG()` to group the result-set by one or more columns.

Examples:
```
SELECT author_lname, COUNT(*) FROM books
GROUP BY author_lname;
```
```
SELECT author_fname, author_lname, COUNT(*) FROM books
GROUP BY author_fname, author_lname;
```
```
SELECT released_year, COUNT(*) AS count FROM books 
GROUP BY released_year ORDER BY count DESC;
```

### ▶ SQL `MIN()` and `MAX()` Functions :
> The `MIN()` function returns the smallest value of the selected column.

> The `MAX()` function returns the largest value of the selected column.

Examples:
```
SELECT MIN(pages) AS smallest_book, MAX(pages) AS largest_book FROM books;
```
With Subqueries:
```
SELECT title, pages FROM books WHERE pages = (SELECT MAX(pages) FROM books);
```
With `GROUP BY`:
```
SELECT
    CONCAT_WS(' ', author_fname, author_lname) AS 'author_name',
    COUNT(*) AS 'book_count',
    MIN(released_year) AS 'first_book',
    MAX(released_year) AS 'last_book'
FROM books
GROUP BY 
    author_fname,
    author_lname;
```

### ▶ `SUM()` Function :

> The `SUM()` function calculates the sum of a set of values.

Syntax:
```
SUM(DISTINCT expression)
```

> The `DISTINCT` option instructs the `SUM()` function to calculate the sum of only distinct values in a set.

Examples:
```
SELECT SUM(pages) FROM books;
```
```
SELECT 
    author_fname,
    author_lname,
    Sum(pages)
FROM books
GROUP BY
    author_lname,
    author_fname;
```

### ▶ `AVG()` Function :

> The MySQL `AVG()` function is an aggregate function that allows you to calculate the average value of a set.

Syntax:
```
AVG(DISTINCT expression)
```

> You use the `DISTINCT` operator in the `AVG` function to calculate the average value of the distinct values.

Examples:
```
SELECT AVG(pages) FROM books;
```
```
SELECT
    author_fname,
    author_lname,
    AVG(pages)
FROM books
GROUP BY 
    author_lname,
    author_fname;
```

----------------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------------
## Extras

### ▶ SQL Aliases :
> SQL aliases are used to give a table, or a column in a table, a temporary name. An alias is created with the `AS` keyword. 

> Column Syntax: 

```
SELECT <column_name> AS <alias_name>
FROM <table_name>;
```
> Table Syntax:

```
SELECT <column_name>
FROM <table_name> AS <alias_name>;
```