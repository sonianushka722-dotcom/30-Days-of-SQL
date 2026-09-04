# DAY 01 OF BASICS OF SQL
Today i started my SQL journey and learned the fundamentals of database and SQL.
## WHAT I LEARNED
### 1. What is Database ?
A database is an organized collection of data that can be easily stored, manages, accessed and retrieved. Database is like a container in which data is 
stored in an organized manner.
 Example:
  An company may store:
-Employee information
-Employee Name
-Address
-salary
-Department,etc.
So if somebody asks a question to find the total salary of all the employees rather than checking each files one by one, we can find the total salary
simply by giving SQL commands.
#### SQL stands for Structures Query Language

### 2. Types of Databases
Some common types of databases are -
 #### Relational Database 
  Tells us how the tables are related to each others. It is like a spreadsheet consists of rows and columns.
    -MySQL
    -PostgreSQl
    -Microsoft SQL Server
    (SQL databse)
 #### Key-Value database
  It is a pair of keys and values just like in a dictionary there is a key words and it stores its meaning or definition inside it.
    -Redis
    -Amazon DynamoDB
#### Column-Based database
Group the data into columns instead of rows. Main purpose is to search the data  from a huge collection of data. Advanced database.
    -Apache Cassandra
    -amazon Redshift
#### Graph database
Focuses on relationship between objects. Focuses on how to connect data points
    -Neo4j
#### Document Database
It is a database where the structure of database is not important but it focuses on fitting all the data in one document.
    -MOngoDB

### what are columns
Columns also known as  Attribute.IT represents a particular property or  a characterstics of an entity.
### What are rows
Row is stores the information about an attribute.
 Example:
 we have a table named as "student" and have column as student name, student class, student marks, subjects
The information stored in these columns tells us more about the table "student" and also about the each student present in a class.
 ### These tables have a primary key. What is a primary key?
Primary key in table is a key that uniquely identify each column and record

### Datatypes in SQL
#### Numeric - 
- `INT` = 1,2,3
- `DECIMAL` = 3.14, 100.50
#### Text -
- `CHAR` = 'MARIAH' (usually have limit)
- `VARCHAR` = 'E5A6'
#### Date & Time -
- `DATE` = '2026-10-30'
- `TIME` = '09:30:00'

### Types of SQL Commands

#### DDL - Data definition language
       - CREATE
       - ALTER
       - DROP
#### DML - Data Manipulation language
      -  INSERT
      -  UPDATE
      -  DELETE
#### DQL - Data Query language
      -  SELECT
