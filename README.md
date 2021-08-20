# MySQL guide sheet
1. [Basic MySQL commands](#basic-mysql-commands)
    * [List all available dabaseses](#-list-all-available-dabaseses-)
2. [Table](#table)
3. [Inserting Data](#inserting-data)
4. [Retrieving/Read data](#retrievingread-data)
5. [Updating data](#updating-data)
5. [Deleting data](#deleting-data)
5. [Selection Refining](#selection-refining)
6. [MySQL string functions](#mysql-string-functions)
6. [Aggregate Functions](#aggregate-functions)
6. [Extras](#extras)

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
## Retrieving/Read data
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

### ▶ Fetch column/columns data from the table with condition using `WHERE` :
> The `WHERE` clause is used to specify a condition while fetching the data from a single table or by joining with multiple tables. If the given condition is satisfied, then only it returns a specific value from the table.

```
SELECT column1, column2
FROM table_name
WHERE [condition];
```

> The `WHERE` clause is not only used in the `SELECT` statement, but it is also used in the UPDATE, DELETE statement etc.

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