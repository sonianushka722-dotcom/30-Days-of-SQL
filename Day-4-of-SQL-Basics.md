# Day 03 - SQL Basics, DDL & DML

Today I continued learning SQL and went a little deeper into the basics.

I learned about **DDL and DML** and also practiced some basic SQL queries.

I also used my **classroom notes** to practice what I was learning, which helped me understand the concepts a little better.

---

##  Topics I learned today

* SELECT
* FROM
* WHERE
* ORDER BY
* DDL
* CREATE
* ALTER
* DROP
* DML
* INSERT
* UPDATE
* DELETE

---

# 1. SELECT

`SELECT` is used to get data from a table.

For example:

```sql
SELECT *
FROM customers;
```

Here `*` means I want to see **all columns**.

So basically:

```text
SELECT → What data do I want?
```

---

## Selecting specific columns

I don't always need all the columns.

I can select only the columns I want.

```sql
SELECT first_name, country
FROM customers;
```

This will only show:

* first_name
* country

So:

```text
SELECT first_name, country
```

means I only want these two columns.

---

# 2. FROM

`FROM` tells SQL **which table I want to get the data from**.

Example:

```sql
SELECT *
FROM customers;
```

Here:

```text
SELECT * → I want all columns

FROM customers → From the customers table
```

Easy way to remember:

> `SELECT` = What do I want?
> `FROM` = Where do I want it from?

---

# 3. WHERE

`WHERE` is used when I want to **filter the data**.

For example:

```sql
SELECT *
FROM customers
WHERE country = 'India';
```

This will show only the customers whose country is India.

Without `WHERE`:

```sql
SELECT *
FROM customers;
```

I get all the customers.

With `WHERE`:

```sql
SELECT *
FROM customers
WHERE country = 'India';
```

I only get the customers matching my condition.

So:

> **WHERE = filter the rows**

---

# 4. Comparison Operators

While using `WHERE`, I can use comparison operators.

Some common ones are:

| Operator | Meaning                  |
| -------- | ------------------------ |
| `=`      | Equal to                 |
| `!=`     | Not equal to             |
| `>`      | Greater than             |
| `<`      | Less than                |
| `>=`     | Greater than or equal to |
| `<=`     | Less than or equal to    |

### Example

```sql
SELECT *
FROM customers
WHERE score > 500;
```

This gives customers whose score is greater than 500.

Another example:

```sql
SELECT *
FROM customers
WHERE score <= 500;
```

This gives customers whose score is less than or equal to 500.

---

# 5. ORDER BY

`ORDER BY` is used to **sort the results**.

We can sort the data in:

* Ascending order → `ASC`
* Descending order → `DESC`

---

## Ascending Order

```sql
SELECT *
FROM customers
ORDER BY score ASC;
```

This sorts the score from:

```text
small → big
```

Example:

```text
100
250
400
600
800
```

---

## Descending Order

```sql
SELECT *
FROM customers
ORDER BY score DESC;
```

This sorts the score from:

```text
big → small
```

Example:

```text
800
600
400
250
100
```

If I just write:

```sql
ORDER BY score
```

ascending order is generally used by default.

---

#  DDL - Data Definition Language

Now comes something new I learned today.

**DDL = Data Definition Language**

DDL is used to work with the **structure of database objects**, such as tables.

The main DDL commands I learned are:

```text
CREATE
ALTER
DROP
```

---

# 6. CREATE

`CREATE` is used to create something new in the database.

For example, I can create a table:

```sql
CREATE TABLE students (
    id INT,
    name VARCHAR(50),
    age INT
);
```

Here I created a table called `students`.

The table has:

```text
id
name
age
```

So basically:

> **CREATE = create something new**

---

# 7. ALTER

`ALTER` is used when I want to **change the structure of an existing table**.

For example, suppose I already have:

```sql
CREATE TABLE students (
    id INT,
    name VARCHAR(50)
);
```

Now I want to add an age column.

I can use:

```sql
ALTER TABLE students
ADD age INT;
```

Now the table has:

```text
id
name
age
```

So:

> **ALTER = change/modify the structure**

---

# 8. DROP

`DROP` is used to remove a database object, such as a table.

Example:

```sql
DROP TABLE students;
```

This removes the table.

So:

```text
CREATE → Create
ALTER  → Change
DROP   → Remove
```

 I need to be careful with `DROP` because it removes the object itself.

---

#  DML - Data Manipulation Language

Another important thing I learned today was **DML**.

DML stands for:

> **Data Manipulation Language**

DML is used to work with the **data stored inside tables**.

The three commands I learned are:

```text
INSERT
UPDATE
DELETE
```

Easy way to remember:

```text
DDL → Structure

DML → Data
```

---

# 9. INSERT

`INSERT` is used to **add new data into a table**.

For example:

```sql
INSERT INTO students (id, name, age)
VALUES (1, 'Anushka', 21);
```

This adds a new row to the table.

Before:

```text
id | name | age
----------------
```

After:

```text
1 | Anushka | 21
```

So:

> **INSERT = Add new data**

---

# 10. INSERT Multiple Rows

I can also insert more than one row.

Example:

```sql
INSERT INTO students (id, name, age)
VALUES
(1, 'Anushka', 21),
(2, 'Rahul', 20),
(3, 'Priya', 22);
```

Now multiple students are added to the table.

---

# 11. UPDATE

`UPDATE` is used when I want to **change existing data**.

For example:

```sql
UPDATE students
SET age = 22
WHERE id = 1;
```

Here I am changing the age of the student whose `id` is 1.

So:

```text
UPDATE → Change existing data
```

###  Important

I need to be careful with `UPDATE`.

For example:

```sql
UPDATE students
SET age = 22;
```

If there is no `WHERE` condition, this can update the age for **all rows**.

So I should always check my `WHERE` condition when I only want to update specific rows.

---

# 12. DELETE

`DELETE` is used to **remove data from a table**.

For example:

```sql
DELETE FROM students
WHERE id = 2;
```

This removes the row where the ID is 2.

So:

```text
DELETE → Remove data
```

###  Again, be careful 

If I write:

```sql
DELETE FROM students;
```

without a `WHERE` condition, it can delete all rows from the table.

So I need to be careful before running `DELETE`.

---

#  DDL vs DML

This was one of the main things I wanted to understand today.

| DDL                      | DML                        |
| ------------------------ | -------------------------- |
| Data Definition Language | Data Manipulation Language |
| Works with structure     | Works with data            |
| CREATE                   | INSERT                     |
| ALTER                    | UPDATE                     |
| DROP                     | DELETE                     |

### Easy way I remember it:

```text
DDL → Structure of the table

DML → Data inside the table
```

---

# Simple Example

Let's say I want to create a student table.

### Step 1 - CREATE

```sql
CREATE TABLE students (
    id INT,
    name VARCHAR(50),
    age INT
);
```

I created the table structure.

### Step 2 - INSERT

```sql
INSERT INTO students
VALUES (1, 'Anushka', 21);
```

I added data.

### Step 3 - SELECT

```sql
SELECT *
FROM students;
```

I checked the data.

### Step 4 - UPDATE

```sql
UPDATE students
SET age = 22
WHERE id = 1;
```

I changed the data.

### Step 5 - DELETE

```sql
DELETE FROM students
WHERE id = 1;
```

I removed the data.

So the basic flow can be:

```text
CREATE
   ↓
INSERT
   ↓
SELECT
   ↓
UPDATE
   ↓
DELETE
```

---

#  What I understood today

Before learning DDL and DML, I was just seeing different SQL commands and trying to remember their syntax.

Now I'm starting to understand that the commands have different jobs.

For example:

```text
CREATE → Make something

ALTER → Change the structure

DROP → Remove the object

INSERT → Add data

SELECT → See data

UPDATE → Change data

DELETE → Remove data
```

This makes the commands a little easier to remember.

---

#  Little things I need to remember

* `SELECT` is used to retrieve data.
* `FROM` tells which table the data comes from.
* `WHERE` filters rows.
* `ORDER BY` sorts the result.
* `CREATE` creates a database object.
* `ALTER` changes its structure.
* `DROP` removes the object.
* `INSERT` adds new data.
* `UPDATE` changes existing data.
* `DELETE` removes existing data.

And yes... I still need more practice to remember all these without looking at my notes 😭

---
# Day 4 complete !!!

#CodingJourney
