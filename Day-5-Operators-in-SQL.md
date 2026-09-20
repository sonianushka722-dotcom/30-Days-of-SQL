# SQL Day 5 — Operators in SQL

Today I continued learning SQL and covered different types of operators.

The topics I learned today were:

* Comparison Operators
* Logical Operators
* Membership Operators
* Range Search Operators
* Search Operator (`LIKE`)

At first, these operators seemed pretty simple, but remembering when to use each one was a little confusing.

---

## 1. Comparison Operators

Comparison operators are used to **compare values**.

Some commonly used comparison operators are:

| Operator | Meaning                  |
| -------- | ------------------------ |
| `=`      | Equal to                 |
| `!=`     | Not equal to             |
| `>`      | Greater than             |
| `<`      | Less than                |
| `>=`     | Greater than or equal to |
| `<=`     | Less than or equal to    |

### Example:

```sql
SELECT *
FROM customers
WHERE age > 25;
```

This will return customers whose age is greater than 25.

Another example:

```sql
SELECT *
FROM customers
WHERE age = 25;
```

This will return customers whose age is exactly 25.

So basically, comparison operators help us put a **condition** on our query.

---

## 2. Logical Operators

Logical operators are used when we have **multiple conditions**.

The main ones are:

* `AND`
* `OR`
* `NOT`

### AND

`AND` means **both conditions must be true**.

```sql
SELECT *
FROM customers
WHERE age > 20 AND age < 30;
```

Here, both conditions have to be satisfied.

---

### OR

`OR` means **at least one condition should be true**.

```sql
SELECT *
FROM customers
WHERE city = 'Nagpur' OR city = 'Pune';
```

This will return customers from either Nagpur or Pune.

---

### NOT

`NOT` is used to reverse a condition.

```sql
SELECT *
FROM customers
WHERE NOT city = 'Nagpur';
```

This means customers whose city is not Nagpur.

---

## 3. Membership Operators

Membership operators are used when we want to check whether a value belongs to a given list of values.

The main operators here are:

* `IN`
* `NOT IN`

### IN

Instead of writing multiple `OR` conditions:

```sql
SELECT *
FROM customers
WHERE city = 'Nagpur'
OR city = 'Pune'
OR city = 'Mumbai';
```

We can use `IN`:

```sql
SELECT *
FROM customers
WHERE city IN ('Nagpur', 'Pune', 'Mumbai');
```

This is much shorter and easier to read.

`IN` basically means:

**"Is this value present in this list?"**

---

### NOT IN

`NOT IN` does the opposite.

```sql
SELECT *
FROM customers
WHERE city NOT IN ('Nagpur', 'Pune', 'Mumbai');
```

This returns customers whose city is not in the given list.

---

## 4. Range Search Operators

For searching values within a particular range, we can use:

### BETWEEN

`BETWEEN` is used to find values within a specified range.

```sql
SELECT *
FROM customers
WHERE age BETWEEN 20 AND 30;
```

This searches for customers whose age is between 20 and 30.

It is similar to:

```sql
SELECT *
FROM customers
WHERE age >= 20 AND age <= 30;
```

One important thing I learned:

`BETWEEN` includes the starting and ending values.

So:

```sql
BETWEEN 20 AND 30
```

includes both `20` and `30`.

---

### NOT BETWEEN

We can also use `NOT BETWEEN`:

```sql
SELECT *
FROM customers
WHERE age NOT BETWEEN 20 AND 30;
```

This returns values outside that range.

---

## 5. Search Operator — LIKE

This was the part I found a little more confusing.

The `LIKE` operator is used when we want to **search for a particular pattern in text**.

For example:

```sql
SELECT *
FROM customers
WHERE first_name LIKE 'A%';
```

This searches for names that start with `A`.

### Wildcards

There are two important wildcards used with `LIKE`:

### `%`

`%` represents **zero or more characters**.

Example:

```sql
WHERE first_name LIKE 'A%'
```

Means the name starts with `A` and can have any number of characters after it.

---

### `_`

`_` represents **exactly one character**.

Example:

```sql
WHERE first_name LIKE 'A_'
```

This means:

* First character is `A`
* There is exactly one character after `A`

---

### More LIKE examples

**Starts with A:**

```sql
WHERE first_name LIKE 'A%'
```

**Ends with a:**

```sql
WHERE first_name LIKE '%a'
```

**Contains "an":**

```sql
WHERE first_name LIKE '%an%'
```

**Starts with A and has exactly one character after it:**

```sql
WHERE first_name LIKE 'A_'
```

**Starts with A, followed by one character, and then anything:**

```sql
WHERE first_name LIKE 'A_%'
```

The main thing I need to remember is:

```text
%  →  zero or more characters

_  →  exactly one character
```

---



