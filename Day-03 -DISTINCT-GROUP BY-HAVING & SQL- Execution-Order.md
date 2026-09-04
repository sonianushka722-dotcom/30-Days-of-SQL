# Day 03 - Learning DISTINCT, GROUP BY, HAVING & ORDER BY

Today I learned some more SQL concepts.
At first, **GROUP BY + HAVING** was a little confusing to me, especially understanding which one works first.

I also learned about **DISTINCT** and something interesting called **SQL execution order**.

---

##  What I learned today

* DISTINCT
* GROUP BY
* HAVING
* ORDER BY
* Aggregate Functions
* GROUP BY + HAVING
* SQL Coding Order
* SQL Execution Order

---

# 1. DISTINCT

`DISTINCT` is used when I don't want duplicate values in my result.

For example, suppose I have a customer table and many customers are from the same country.

```sql
SELECT country
FROM customers;
```

This can give something like:

```text
India
India
USA
UK
India
USA
```

If I only want each country once:

```sql
SELECT DISTINCT country
FROM customers;
```

Now the result can be:

```text
India
USA
UK
```

So basically:

> **DISTINCT = remove duplicate results**

### Example

```sql
SELECT DISTINCT gender
FROM customers;
```

This will show each different gender only once.

---

# 2. GROUP BY

`GROUP BY` is used to **group rows having the same value**.

It is mostly useful when working with aggregate functions like:

* `SUM()`
* `AVG()`
* `COUNT()`
* `MIN()`
* `MAX()`

For example, if I have sales data:

| category | amount |
| -------- | ------ |
| Mobile   | 500    |
| Laptop   | 1000   |
| Mobile   | 700    |
| Laptop   | 1500   |

If I want the total amount for each category:

```sql
SELECT category, SUM(amount)
FROM sales
GROUP BY category;
```

The database groups the same categories together and then calculates the sum.

Result:

```text
Mobile     1200
Laptop     2500
```

So I understood it like:

> **GROUP BY = make groups of similar values**

---

# 3. Aggregate Functions

Aggregate functions are functions that perform calculations on multiple rows.

Some common ones are:

### SUM()

Used to calculate the total.

```sql
SELECT SUM(amount)
FROM sales;
```

---

### AVG()

Used to find the average.

```sql
SELECT AVG(amount)
FROM sales;
```

---

### COUNT()

Used to count rows.

```sql
SELECT COUNT(*)
FROM customers;
```

---

### MIN()

Used to find the smallest value.

```sql
SELECT MIN(amount)
FROM sales;
```

---

### MAX()

Used to find the largest value.

```sql
SELECT MAX(amount)
FROM sales;
```

---

# 4. GROUP BY + Aggregate Function

This was one of the important things I practiced today.

Suppose I want to find the total sales for every category.

```sql
SELECT category, SUM(amount)
FROM sales
GROUP BY category;
```

Here:

* `category` tells SQL what I want to make groups of
* `SUM(amount)` calculates the total
* `GROUP BY category` creates a separate group for each category

Basically:

```text
Same category
      ↓
Make a group
      ↓
Calculate SUM
      ↓
Get result
```

---

# 5. HAVING

This was a little confusing for me at first 

`HAVING` is used to **filter groups**.

It is generally used with `GROUP BY`.

For example:

```sql
SELECT category, SUM(amount)
FROM sales
GROUP BY category
HAVING SUM(amount) > 1000;
```

Here SQL first makes groups based on category.

Then it calculates the total amount.

After that, `HAVING` keeps only the groups where the total is greater than 1000.

So:

> **HAVING = filter the groups**

---

# 6. WHERE vs HAVING

This is something I need to remember properly.

### WHERE

`WHERE` is used to filter **individual rows**.

Example:

```sql
SELECT *
FROM customers
WHERE country = 'India';
```

Here SQL checks each row and keeps the rows where country is India.

---

### HAVING

`HAVING` is used to filter **groups**.

Example:

```sql
SELECT country, COUNT(*)
FROM customers
GROUP BY country
HAVING COUNT(*) > 5;
```

Here SQL first creates groups based on country.

Then it checks which groups have more than 5 customers.

### Easy way to remember:

```text
WHERE  → filters rows
HAVING → filters groups
```

This was one of the main things I learned today.

---

# 7. GROUP BY + HAVING

We can use both together.

Example:

```sql
SELECT category, SUM(amount)
FROM sales
GROUP BY category
HAVING SUM(amount) > 5000;
```

What happens here?

### Step 1

SQL gets the data from the table.

### Step 2

It groups the data by `category`.

### Step 3

It calculates `SUM(amount)` for every category.

### Step 4

`HAVING` checks the total.

### Step 5

Only categories having total sales greater than 5000 are shown.

So the basic idea is:

```text
GROUP BY
   ↓
Make groups
   ↓
Aggregate calculation
   ↓
HAVING
   ↓
Filter groups
```

---

# 8. ORDER BY

`ORDER BY` is used to **sort the result**.

We can sort in:

* Ascending order → `ASC`
* Descending order → `DESC`

### Ascending

```sql
SELECT *
FROM customers
ORDER BY age ASC;
```

This sorts age from smaller to bigger.

Example:

```text
18
20
22
25
30
```

---

### Descending

```sql
SELECT *
FROM customers
ORDER BY age DESC;
```

This sorts age from bigger to smaller.

```text
30
25
22
20
18
```

If I don't write `ASC` or `DESC`, ascending order is generally used by default.

---

# 9. ORDER BY with GROUP BY

We can also sort grouped results.

Example:

```sql
SELECT category, SUM(amount)
FROM sales
GROUP BY category
ORDER BY SUM(amount) DESC;
```

This means:

1. Group the sales by category.
2. Calculate total sales.
3. Sort the result from highest total to lowest total.

This is useful when I want to see which category has the highest sales.

---

# 10. DISTINCT vs GROUP BY

At first these can look similar, but they are not exactly the same.

### DISTINCT

Used to remove duplicate results.

```sql
SELECT DISTINCT country
FROM customers;
```

### GROUP BY

Used to create groups, usually for calculations.

```sql
SELECT country, COUNT(*)
FROM customers
GROUP BY country;
```

Easy way:

```text
DISTINCT → I just want unique results

GROUP BY → I want groups and maybe calculations
```

---

# 11. SQL Coding Order

Today I also learned that the order in which I **write** a SQL query is not the same as the order in which SQL logically processes it.

Normally I write a query like:

```sql
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
```

This is the **coding order**.

Basically, this is the order I type the query.

---

# 12. SQL Execution Order

SQL logically processes the query in a different order.

A simplified logical order is:

```text
FROM
 ↓
WHERE
 ↓
GROUP BY
 ↓
HAVING
 ↓
SELECT
 ↓
DISTINCT
 ↓
ORDER BY
```

This was honestly a little confusing at first because I was writing `SELECT` first, but SQL logically starts with `FROM`.

---

# 13. Example of Execution Order

Consider this query:

```sql
SELECT DISTINCT country, COUNT(*)
FROM customers
WHERE age > 18
GROUP BY country
HAVING COUNT(*) > 2
ORDER BY country;
```

I write it from top to bottom.

But logically, SQL processes it roughly like this:

### 1. FROM

First SQL gets the data from:

```sql
FROM customers
```

### 2. WHERE

Then it filters the rows:

```sql
WHERE age > 18
```

So customers whose age is not greater than 18 are removed.

### 3. GROUP BY

Now the remaining rows are grouped:

```sql
GROUP BY country
```

### 4. HAVING

Now groups are filtered:

```sql
HAVING COUNT(*) > 2
```

Only countries having more than 2 customers remain.

### 5. SELECT

Now SQL selects what I asked for:

```sql
SELECT DISTINCT country, COUNT(*)
```

### 6. DISTINCT

Duplicate result rows are removed if there are any.

### 7. ORDER BY

Finally, the result is sorted:

```sql
ORDER BY country;
```

---

#  Coding Order vs Execution Order

This is something I want to remember:

### Coding order

```text
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
```

### Logical execution order

```text
FROM
WHERE
GROUP BY
HAVING
SELECT
DISTINCT
ORDER BY
```

So basically:

> **I write SQL one way, but SQL logically processes it another way.**

---

#  What confused me today

The main thing I struggled with today was:

**GROUP BY + HAVING**

At first I was confused about why we need `HAVING` when we already have `WHERE`.

Then I understood:

```text
WHERE → filters rows
GROUP BY → makes groups
HAVING → filters those groups
```

The execution order also helped me understand why `WHERE` comes before `GROUP BY` and `HAVING`.

I definitely need more practice with this part.

---


#CodingJourney

-----
**DAY 3 COMPLETE**
