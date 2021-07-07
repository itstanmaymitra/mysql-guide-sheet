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


## Retrieving data
 