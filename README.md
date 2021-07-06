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