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


## Table 

### ▶ Generic version of creating a table :
```
CREATE TABLE <table_name>
(
    <column_name1> <data_type>,
    <column_name2> <data_type>
);
```
> By default, with the command above the table column cell will accept `Null` values. But we can disable accepting `NULL` values while creating table by the command bellow:
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
> *Example :
```
CREATE TABLE cats
(
    name VARCHAR(100) NOT NULL DEFAULT 'unnamed',
    age INT NOT NULL DEFAULT 00
)
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