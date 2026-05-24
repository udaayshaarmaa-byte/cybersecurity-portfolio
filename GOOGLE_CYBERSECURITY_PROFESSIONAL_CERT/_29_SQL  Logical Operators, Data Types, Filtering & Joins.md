# SQL | Logical Operators, Data Types, Filtering & Joins
---

## 1. Logical Operators  AND, OR, NOT

Used to combine or negate conditions in a `WHERE` clause.

### AND both conditions must be true
```sql
SELECT firstname, lastname, email, country, supportrepid
FROM customers
WHERE supportrepid = 5 AND country = 'USA';
```

### OR either condition (or both) must be true
```sql
SELECT firstname, lastname, email, country
FROM customers
WHERE country = 'Canada' OR country = 'USA';
```
Note: even when filtering the same column twice, write each condition in full.

### NOT negates a condition
```sql
SELECT firstname, lastname, email, country
FROM customers
WHERE NOT country = 'USA';
```
Equivalent alternatives:
```sql
WHERE country <> 'USA'
WHERE country != 'USA'
```

### Combining operators:
```sql
-- Exclude both Canada and USA
SELECT firstname, lastname, email, country
FROM customers
WHERE NOT country = 'Canada' AND NOT country = 'USA';
```


## 2. Data Types in SQL

| Data Type | Description | Examples |
|---|---|---|
| **String** | Ordered sequence of characters (numbers, letters, symbols) | usernames, country codes, office names |
| **Numeric** | Numbers supports mathematical operations | login attempt counts, volume of data transferred |
| **Date/Time** | Represents a date and/or time | login timestamps, patch dates, hire dates |

**Syntax rule:** strings, dates, and times use **quotation marks**. Numbers do **not**.

```sql
WHERE country = 'USA'          -- string — quotes
WHERE login_attempts > 5       -- numeric — no quotes
WHERE login_time > '18:00'     -- time — quotes
WHERE patch_date > '2021-03-01' -- date — quotes
```

---

## 3. Comparison Operators

| Operator | Meaning | Type |
|---|---|---|
| `=` | Equal to | Inclusive |
| `!=` or `<>` | Not equal to | Exclusive |
| `>` | Greater than | Exclusive |
| `<` | Less than | Exclusive |
| `>=` | Greater than or equal to | Inclusive |
| `<=` | Less than or equal to | Inclusive |

**Exclusive** = does not include the boundary value.
**Inclusive** = includes the boundary value.

### Security analyst examples:
```sql
-- Login attempts after 6 PM (suspicious after-hours activity)
SELECT *
FROM log_in_attempts
WHERE time > '18:00';

-- Employees born after Jan 1 1970 (exclusive — not including that date)
SELECT firstname, lastname, birthdate
FROM employees
WHERE birthdate > '1970-01-01';
```

---

## 4. BETWEEN Operator

Filters for values within a range — **inclusive** on both ends.

```sql
-- Machines patched between two dates
SELECT *
FROM machines
WHERE OS_patch_date BETWEEN '2021-03-01' AND '2021-09-01';

-- Employees hired in a specific year
SELECT firstname, lastname, hiredate
FROM employees
WHERE hiredate BETWEEN '2002-01-01' AND '2003-01-01';
```

Format: `WHERE column BETWEEN 'start' AND 'end'`

---

## 5. SQL Joins — Combining Tables

**Why joins matter:** security decisions often require data from multiple tables. Example: join an OS vulnerabilities table with a machines table to get a list of all vulnerable machines in the company.

### Syntax for referencing columns from two tables:
Use `table_name.column_name` when the same column name exists in both tables:
```sql
employees.employee_id
machines.employee_id
```

### NULL in SQL
`NULL` = a missing value in a field (e.g. a machine not assigned to any employee).

---

## 6. Types of Joins

### INNER JOIN — only matching rows from both tables

```
[ Left Table ] ∩ [ Right Table ]  ← only the intersection
```

```sql
SELECT username, operating_system, employees.device_id
FROM employees
INNER JOIN machines ON employees.device_id = machines.device_id;
```
- Returns only rows where `device_id` matches in both tables
- Non-matching rows from either table are excluded

---

### LEFT JOIN — all rows from left table + matching rows from right

```
[ Left Table (all) ] + [ Right Table (matches only) ]
```

```sql
SELECT *
FROM employees
LEFT JOIN machines ON employees.device_id = machines.device_id;
```
- All employees returned; only machines with a matching device_id included
- Employees with no assigned machine → `NULL` in machine columns

---

### RIGHT JOIN — all rows from right table + matching rows from left

```
[ Left Table (matches only) ] + [ Right Table (all) ]
```

```sql
SELECT *
FROM employees
RIGHT JOIN machines ON employees.device_id = machines.device_id;
```
- All machines returned; only employees with a matching device_id included
- Machines with no assigned employee → `NULL` in employee columns

---

### FULL OUTER JOIN — all rows from both tables

```
[ Left Table (all) ] + [ Right Table (all) ]
```

```sql
SELECT *
FROM employees
FULL OUTER JOIN machines ON employees.device_id = machines.device_id;
```
- Every row from both tables is returned
- Non-matching rows get `NULL` in columns from the other table

---

## 7. Join Type Summary

| Join | Returns | NULL appears when... |
|---|---|---|
| **INNER JOIN** | Only matching rows from both tables | Never (non-matches excluded entirely) |
| **LEFT JOIN** | All from left + matches from right | Right table has no match for a left row |
| **RIGHT JOIN** | All from right + matches from left | Left table has no match for a right row |
| **FULL OUTER JOIN** | All rows from both tables | Either table has no match for a row |

---

## 8. Full Query Templates

```sql
-- Logical operators + numeric filter
SELECT *
FROM log_in_attempts
WHERE country = 'USA' AND login_attempts > 3
ORDER BY login_attempts DESC;

-- Date range filter
SELECT *
FROM machines
WHERE OS_patch_date BETWEEN '2021-01-01' AND '2021-06-30';

-- INNER JOIN example
SELECT username, office, operating_system
FROM employees
INNER JOIN machines ON employees.employee_id = machines.employee_id;

-- LEFT JOIN — all employees + their machine (if any)
SELECT employees.employee_id, username, device_id, operating_system
FROM employees
LEFT JOIN machines ON employees.employee_id = machines.employee_id;
```

---

## Key Terms

| Term | Definition |
|---|---|
| AND | Both conditions must be true |
| OR | Either condition (or both) must be true |
| NOT | Negates a condition |
| String | Data type: ordered sequence of characters |
| Numeric | Data type: numbers; supports math operations |
| Date/Time | Data type: represents a date and/or time |
| BETWEEN | Filters a range (inclusive on both ends) |
| Exclusive operator | Does not include the boundary value (e.g. `>`, `<`) |
| Inclusive operator | Includes the boundary value (e.g. `>=`, `<=`, `BETWEEN`) |
| INNER JOIN | Returns only rows that match on the specified column in both tables |
| LEFT JOIN | All rows from left table + matching rows from right |
| RIGHT JOIN | All rows from right table + matching rows from left |
| FULL OUTER JOIN | All rows from both tables |
| NULL | Missing value in SQL |
| ON | Keyword specifying which column to join on |