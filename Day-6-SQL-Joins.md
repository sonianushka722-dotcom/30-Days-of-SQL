# SQL Day 6 — JOINS

Today I started learning one of the most important topics in SQL — **JOINS**.

Honestly, JOINs looked a little confusing at first because there are different types of joins and I had to understand how tables are connected.

The main idea I understood is:

> **JOIN is used to combine data from two or more tables based on a related column.**

---

## Why do we need JOINs?

In a database, we usually don't keep everything in one huge table.

For example, we can have a `customers` table:

| customer_id | first_name | country |
| ----------- | ---------- | ------- |
| 1           | John       | USA     |
| 2           | Alex       | India   |
| 3           | Sarah      | UK      |

And another `orders` table:

| order_id | customer_id | amount |
| -------- | ----------- | ------ |
| 101      | 1           | 500    |
| 102      | 2           | 700    |
| 103      | 1           | 300    |

Here, both tables have `customer_id`.

So we can use `customer_id` to connect the two tables and get information from both.

---

# Types of JOINS

The main JOINs I learned are:

* INNER JOIN
* LEFT JOIN
* RIGHT JOIN
* FULL JOIN

---

## 1. INNER JOIN

`INNER JOIN` returns only the rows that have a **match in both tables**.

### Example:

```sql
SELECT *
FROM customers
INNER JOIN orders
ON customers.customer_id = orders.customer_id;
```

Here:

```sql
ON customers.customer_id = orders.customer_id
```

tells SQL **how the two tables should be connected**.

So if a customer has an order, their information can be combined.

If there is no matching `customer_id`, that row will not be included.

### Simple way to remember:

**INNER JOIN = only matching data**

---

## 2. LEFT JOIN

`LEFT JOIN` returns:

* All rows from the **left table**
* Matching rows from the right table

Example:

```sql
SELECT *
FROM customers
LEFT JOIN orders
ON customers.customer_id = orders.customer_id;
```

Here, `customers` is the left table.

So **every customer will be included**, even if they don't have an order.

If there is no matching order, the columns from the `orders` table will contain `NULL`.

### Simple way to remember:

**LEFT JOIN = everything from the left table + matching data from the right**

---

## 3. RIGHT JOIN

`RIGHT JOIN` is basically the opposite of `LEFT JOIN`.

It returns:

* All rows from the **right table**
* Matching rows from the left table

Example:

```sql
SELECT *
FROM customers
RIGHT JOIN orders
ON customers.customer_id = orders.customer_id;
```

Here, every order from the right table will be included.

If an order doesn't have a matching customer, the customer columns can show `NULL`.

### Simple way to remember:

**RIGHT JOIN = everything from the right table + matching data from the left**

---

## 4. FULL JOIN

`FULL JOIN` returns **all rows from both tables**.

It includes:

* Matching rows
* Unmatched rows from the left table
* Unmatched rows from the right table

Example:

```sql
SELECT *
FROM customers
FULL JOIN orders
ON customers.customer_id = orders.customer_id;
```

If a row exists only in one table, the columns from the other table will contain `NULL`.

### Simple way to remember:

**FULL JOIN = everything from both tables**

---

# The ON condition

One important thing I learned with JOINs is the `ON` condition.

For example:

```sql
ON customers.customer_id = orders.customer_id
```

This tells SQL which columns should be used to connect the tables.

So basically:

```text
Table 1                     Table 2
customers                   orders

customer_id  <---------->  customer_id
                  |
                JOIN
```

The related column doesn't necessarily have to have the same name, but the values need to represent the relationship we want to join on.

---

# INNER vs LEFT vs RIGHT vs FULL

A simple way I am remembering them:

```text
INNER JOIN
→ Only matching rows

LEFT JOIN
→ Everything from left + matching right

RIGHT JOIN
→ Everything from right + matching left

FULL JOIN
→ Everything from both tables
```

---

# Using table aliases

JOIN queries can become long, so we can use **aliases** to make them easier to write.

For example:

```sql
SELECT *
FROM customers AS c
INNER JOIN orders AS o
ON c.customer_id = o.customer_id;
```

Here:

```text
c → customers
o → orders
```

So instead of writing:

```sql
customers.customer_id
```

we can write:

```sql
c.customer_id
```

This makes bigger queries easier to read.

---

