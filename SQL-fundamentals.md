
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

- CREATE DATABASE - creates a new database
- SHOW DATABASES - returns a list of all created databases
- USE databasenamee - allows you to interact with a database you know to exist
- DROP databasename - allows you to delete a database you no longer want to exist

- CREATE TABLE - allows you to create a table in a database. You need to add the different columns in order to create the entire table. 
```
CREATE TABLE shoes (
    shoe_id INT AUTO_INCREMENT PRIMARY KEY,
    color VARCHAR(255) NOT NULL,
    release_date DATE
  )
```

- SHOW TABLES will show you the tables in a database
- DESCRIBE tablename will show you what columns are within a table. It returns a detailed view of a table. 
- ALTER TABLE tablename allows you to alter a table if you want to make changes.
- DROP tablename allows you to remove a table from a database

CRUD (Create Read Update Delete)

INSERT INTO tablename - creates a new row into a table
```
INSERT INTO shoes (id, color, releasedate)
  VALUES(1, "blue", "2024-10-20");
```
SELECT operation allows you to read an item
`SELECT * FROM shoes`
UPDATE operation allows you to update an item
DELETE operation deletes an item from the table
`DELETE FROM shoes WHERE id = 2`

<hr />

## Clauses

A clause is apart of a statement that specifies criteria of the data being manipulated, usually by an initial statement. Some of these clauses are FROM, WHERE, DISTINCT, GROUP BY, etc. 

**DISTINCT** clause is used to avoid duplicate records when doing a query. 

example: If you try `SELECT * FROM shoes` and there are two stilleto entries, both of these are going to appear on the results. 
If you only want to know what are the different types of shoes you have without sifting through duplicate entries, you can enter `SELECT DISTINCT shoetype FROM shoes` and it'll give you a list of the different shoe types you have on a table without listing duplicates. 

**GROUP BY** clause aggregates data from multiple records and groups the query results in columns. 

example: `SELECT shoetype, COUNT(*) FROM shoes GROUP BY shoetype`
This is going to output a list like the following where it's going to list the different shoe types and count how many you have in the table. 
```
+----------------------------+----------+
| shoetype                   | COUNT(*) |
+----------------------------+----------+
| Tennis shoes               |        1 |
| Heels                      |        1 |
| Flats                      |        1 |
| Sandals                    |        1 |
| Stilletos                  |        2 |
+----------------------------+----------+
```

**ORDER BY** clause is going to sort data from ascending to descending order. Using functions like ASC or DESC can help accomplish that. 

example: `SELECT * FROM shoes ORDER BY release_date ASC` will return:

```
+----+----------------------------+----------------+--------------------------------------------------------+
| id | shoe                       | release_date   | description                                            |
+----+----------------------------+----------------+--------------------------------------------------------+
|  1 | Prada Stripe Tennis Shoes  | 2014-10-14     | White Leather Prada Tennis Shoes with Pink Stripe      |
|  3 | Versace Sandals Black      | 2016-02-25     | Versace Leather Black Sandals with Gold Logo           |
|  5 | Miu Miu Stilletos          | 2021-11-02     | Black MiuMiu Stilletos with Pink Flower                |
|  6 | Prada Stilletos            | 2021-11-02     |                                                        |
|  2 | YSL Heels Purple           | 2021-11-16     | YSL strappy heels, shiny purple with YSL logo as heel  |
|  4 | Christian Loubiton Heels   | 2021-12-21     | Classic Black Christian Loubiton Heels                 |
+----+----------------------------+----------------+--------------------------------------------------------+
```

**HAVING** clause is used with other clauses to filter groups or results of records based on a condition. 

example: `SELECT shoe, COUNT(*) FROM shoes GROUP BY shoe HAVING shoe LIKE '%Prada%';

```
+-----------------------+--------------+
| shoe                      | COUNT(*) |
+-----------------------+--------------+
| Prada Stripe Tennis Shoes |        1 |
| Prada Stilletos           |        1 |
+-----------------------+--------------+
```
<hr />

## OPERATORS

**Logical Operators** test the truth of a condition and return either TRUE or FALSE

**LIKE** operator is used in conjunction with **WHERE** to filter for specific patterns within a column. 
`SELECT shoe FROM shoes WHERE shoe LIKE %Stilletos%`

**AND** operator uses multiple conditions to fulfill a requirement

**OR** operator combines multiple possible conditions and returns TRUE if one of these conditions are true.

**NOT** operator reverses the value of a boolean operator and excludes items with a specific condition

**BETWEEN** operator allows you to test a condition if it fits within a defined range. 

**COMPARISON OPERATORS** used to compare specific values to see if they fit a criteria 

**=** is going to check if it has an exact match 

**!=** checks if a value is not equal and returns what doesn't match that

**<** Less than operator

**>** Greater than operator

**<=** less than or equal to

**>=** greater than or equal to








