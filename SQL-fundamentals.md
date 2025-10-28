
# SQL Fundamentals

**Database types**
  - relational: SQL
  - non-relational: noSQL

Tables, rows, columns

**TABLES** store the information
**COLUMNS** define what piece of information is going to be contained
**ROWS** represent each record of a table

<img width="837" height="456" alt="image" src="https://github.com/user-attachments/assets/2b84000a-b537-4ffd-b7bf-0d8a08e4d6dd" />


There are primary keys and foreign keys

**Primary keys** are unique to that database so they can be identified
**Foreign keys** are keys for items that exist within another database 

Databases are controlled using a DBMS (Database Management System) like MangoDB, Oracle, MySQL, Maria DB, etc. 

DBMS serve as an interface between a database and an end user
SQL is what you use to interact with a relational database

CREATE DATABASE - creates a new database
SHOW DATABASES - returns a list of all created databases
USE databasenamee - allows you to interact with a database you know to exist
DROP databasename - allows you to delete a database you no longer want to exist

CREATE TABLE - allows you to create a table in a database. You need to add the different columns in order to create the entire table. 
```
CREATE TABLE shoes (
    shoe_id INT AUTO_INCREMENT PRIMARY KEY,
    color VARCHAR(255) NOT NULL,
    release_date DATE
  )
```
  






