# Day 2 of SQL
## How SQL Queries works and what are they !
#### CREATE TABLE

## 30 Days of SQL — #SQLwithAnushka

Today I continued my SQL journey by moving from basic concepts to actually **writing and practicing SQL queries**.

I learned how to create and modify tables, retrieve specific data, filter records, sort results, group data, and use aggregate functions.

I also made mistakes while practicing today. Instead of just copying the correct queries, I tried to understand **why my query was wrong and how to fix it**. That made today's practice much more useful.

---

## Topics I Learned Today

* `CREATE TABLE`
* Adding columns using `ALTER TABLE`
* `SELECT`
* `WHERE`
* `ORDER BY`
* `GROUP BY`
* Aggregate Functions
* `SUM()`
* `GROUP BY` with `SUM()`

---

# 1. CREATE TABLE

The `CREATE TABLE` command is used to create a new table in a database.

Before storing data, we need to define the structure of the table — what columns it will have and what type of data each column can store.

### Syntax

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype
);
```

### Example

```sql
CREATE TABLE students (
    student_id INT,
    name VARCHAR(50),
    age INT,
    course VARCHAR(50)
);
```

### Understanding the Example

* `students` → Name of the table
* `student_id` → Column for student ID
* `name` → Column for student name
* `age` → Column for age
* `course` → Column for course
* `INT` → Used for whole numbers
* `VARCHAR(50)` → Used for text with a maximum length of 50 characters

###  What I Understood

I think of `CREATE TABLE` as **creating the structure or blueprint of my table**.

It tells the database what kind of information I want to store.

---

# 2️. Adding Columns Using ALTER TABLE

Sometimes we create a table and later realize that we forgot to add a column.

Instead of creating the table again, we can modify the existing table using `ALTER TABLE`.

### Syntax

```sql
ALTER TABLE table_name
ADD COLUMN column_name datatype;
```

### Example

Suppose I already have:

```sql
CREATE TABLE students (
    student_id INT,
    name VARCHAR(50),
    age INT
);
```

Later, I decide that I also need a `course` column.

I can add it using:

```sql
ALTER TABLE students
ADD COLUMN course VARCHAR(50);
```

I can also add another column:

```sql
ALTER TABLE students
ADD COLUMN marks INT;
```

###  What I Understood

`ALTER TABLE` is used when I want to **change the structure of an existing table**.

Adding a column means adding a new field/attribute to the table, not adding a new row.

---

# 3️. SELECT Query

`SELECT` is one of the most important SQL commands.

It is used to retrieve data from a table.

### Selecting All Columns

```sql
SELECT *
FROM students;
```

The `*` means **all columns**.

So this query basically asks:

> "Show me everything from the students table."

### Selecting Specific Columns

Instead of selecting everything, I can select only the columns I need.

```sql
SELECT name, course
FROM students;
```

This will return only the `name` and `course` columns.

###  What I Understood

I think of `SELECT` as:

> **What data do I want to see?**

---

# 4️. WHERE Clause

The `WHERE` clause is used to **filter records** based on a condition.

### Example

```sql
SELECT *
FROM students
WHERE age = 20;
```

This returns only the students whose age is 20.

Another example:

```sql
SELECT name, marks
FROM students
WHERE marks > 70;
```

This returns the names and marks of students who scored more than 70.

### Common Operators Used with WHERE

 Operator | Meaning                  
 -------- | ---------------------------
 `=`      | Equal to                 
 `>`      | Greater than             
 `<`      | Less than                
 `>=`     | Greater than or equal to 
 `<=`     | Less than or equal to    
 `<>`     | Not equal to             

### Example

```sql
SELECT *
FROM students
WHERE marks >= 60;
```

This retrieves students who scored 60 or more.

###  What I Understood

I think of `WHERE` as:

> **Which records do I actually want?**

It helps me filter out unnecessary records.

---

# 5️. ORDER BY

`ORDER BY` is used to **sort the result of a query**.

It can sort data in:

* Ascending order → `ASC`
* Descending order → `DESC`

### Ascending Order

```sql
SELECT *
FROM students
ORDER BY marks ASC;
```

For numbers, the result would look like:

```text
10
20
30
40
50
```

### Descending Order

```sql
SELECT *
FROM students
ORDER BY marks DESC;
```

The result would look like:

```text
50
40
30
20
10
```

### Example

```sql
SELECT name, marks
FROM students
ORDER BY marks DESC;
```

This displays students from the highest marks to the lowest.

###  What I Understood

I think of `ORDER BY` as:

> **In what order do I want my result?**

---

# 6️. GROUP BY

`GROUP BY` is used to **group rows that have the same value** in a particular column.

It becomes especially useful when working with aggregate functions.

### Example

Suppose I have a `sales` table:

 product | category    | amount 
 ------- | ----------- | -----: 
 Laptop  | Electronics |  50000 
 Mouse   | Electronics |   1000 
 Shirt   | Clothing    |   1500 
 Jeans   | Clothing    |   2500 

If I use:

```sql
SELECT category
FROM sales
GROUP BY category;
```

The categories will be grouped together.

The result would be:

```text
Electronics
Clothing
```

### Why is GROUP BY useful?

Imagine having hundreds or thousands of records.

Instead of analyzing every individual row, I might want to analyze the data category-wise.

For example:

* Total sales by category
* Total salary by department
* Number of students in each course
* Average marks by subject

###  What I Understood

I think of `GROUP BY` as:

> **Put similar records into groups so I can analyze each group.**

---

# 8️. SUM()

`SUM()` is used to calculate the **total of a numeric column**.

### Example

```sql
SELECT SUM(amount)
FROM sales;
```

Suppose the amount values are:

```text
1000
2000
3000
```

Then:

```text
SUM(amount) = 6000
```

So SQL adds all the values together.

# 9️. GROUP BY + SUM()

This was one of the most useful combinations I practiced today.

Suppose my sales table contains:

 category    | amount 
 ----------- | -----: 
 Electronics |  50000 
 Electronics |   1000 
 Clothing    |   1500 
 Clothing    |   2500 

If I use only:

```sql
SELECT SUM(amount)
FROM sales;
```

I get the total amount of **all sales together**.

But if I want the total sales for each category, I can use:

```sql
SELECT category, SUM(amount)
FROM sales
GROUP BY category;
```

The result would be:

| category    |   sum |
| ----------- | ----: |
| Electronics | 51000 |
| Clothing    |  4000 |

###  How This Query Works

There are two important parts:

### Step 1 — GROUP BY

```sql
GROUP BY category
```

This groups the rows according to their category.

### Step 2 — SUM()

```sql
SUM(amount)
```

This calculates the total amount inside each group.

So, in simple words:

> `GROUP BY` → Creates the groups
> `SUM()` → Calculates the total for each group

---

#  GROUP BY vs SUM()

### Without GROUP BY

```sql
SELECT SUM(amount)
FROM sales;
```

8 Gives the total amount from the entire table.

### With GROUP BY

```sql
SELECT category, SUM(amount)
FROM sales
GROUP BY category;
```

* Gives the total amount **for each category separately**.

This helped me understand why aggregate functions and `GROUP BY` are often used together.



#  Mistakes I Made While Practicing

One thing I noticed today is that **my queries did not always work on the first attempt.**

I made mistakes while writing some queries and sometimes got errors or unexpected results.

Instead of simply copying a corrected query, I tried to understand:

* What did I write incorrectly?
* Which part of the query caused the problem?
* Did I use the correct column name?
* Did I use the correct syntax?
* Why was the output different from what I expected?

This made me realize that **errors are also part of learning**.

Every time I corrected a query, I understood the concept a little better.

**Day 2 completed successfully** 




