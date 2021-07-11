# MySQL guide sheet

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

---
### ▶ Run MySQL commands from the file :

* Create a file with `.sql` file extension
* `cd` into the file directory
* Run MySQL in that directory with this command `mysql -u root -p`
* To run the SQL commands from the file run `source file_name.sql`
---


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


## Updating data
The `UPDATE` statement is used to update existing data in a **table**.
 
### ▶ Update/Alter existing data in a table :
```
UPDATE <table_name>
SET column1=value, column2=value2
WHERE <some_column>=<some_value>;
```

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

-----
## MySQL string functions :

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


-----
## Extras :

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