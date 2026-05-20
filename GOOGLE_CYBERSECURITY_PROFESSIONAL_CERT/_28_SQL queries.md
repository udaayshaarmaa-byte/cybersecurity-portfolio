# SQL Queries, Filtering & Wildcards

---

## 1. Basic SQL Query Structure

Two essential keywords in every SQL query:

```sql
SELECT column1, column2
FROM table_name;
```

- **SELECT**  indicates which columns to return
- **FROM** indicates which table to query
- **Semicolon (`;`)**  marks the end of the query
- Keywords are **not case-sensitive** (SELECT = select), but capitalising is convention for readability
- **Line breaks** are optional but improve readability

### Select all columns:
```sql
SELECT *
FROM employees;
```

`*` = wildcard meaning "all columns"  use sparingly on large tables as it can be slow and hard to read.

---

## 2. ORDER BY  Sorting Results

```sql
SELECT customerid, city, country
FROM customers
ORDER BY city;
```

- Default = **ascending** (A→Z, smallest→largest)
- Add `DESC` for **descending** (Z→A, largest→smallest):

```sql
ORDER BY city DESC;
```

- Sort by **multiple columns**  SQL sorts by the first, then breaks ties using the second:

```sql
ORDER BY country, city;
```

---

## 3. WHERE  Filtering Results

**Filtering** = selecting only data that matches a certain condition.

```sql
SELECT *
FROM log_in_attempts
WHERE country = 'USA';
```

- `WHERE` comes after `FROM`
- Semicolon goes after the filter (end of full statement)
- Use `=` operator for exact matches

### Security analyst use cases:
- Filter login attempts by country, time, or username
- Find machines missing a specific patch version
- Identify unusual access patterns

---

## 4. Operators

An **operator** = symbol or keyword representing an operation.

| Operator | Meaning | Example |
|---|---|---|
| `=` | Equal to | `WHERE country = 'USA'` |
| `!=` or `<>` | Not equal to | `WHERE country != 'USA'` |
| `>` | Greater than | `WHERE attempts > 5` |
| `<` | Less than | `WHERE attempts < 3` |
| `>=` | Greater than or equal | `WHERE login_time >= '08:00'` |
| `<=` | Less than or equal | `WHERE login_time <= '17:00'` |
| `LIKE` | Pattern match (use with wildcards) | `WHERE title LIKE 'IT%'` |

---

## 5. LIKE & Wildcards  Pattern Filtering

When you need to match a **pattern** rather than an exact value, use `LIKE` instead of `=`.

### Two wildcards:

| Wildcard | Substitutes | Example pattern | Returns |
|---|---|---|---|
| `%` | Any number of characters (0 or more) | `'East%'` | East-120, East-290, Eastern |
| `_` | Exactly one character | `'N_'` | NY, NV, NS, NT |

### Pattern examples:

| Pattern | What it matches |
|---|---|
| `'a%'` | Anything starting with 'a': apple123, art, a |
| `'%a'` | Anything ending with 'a': pizza, Z6ra, a |
| `'%a%'` | Anything containing 'a': Again, back, a |
| `'a_'` | 'a' followed by exactly one char: as, an, a7 |
| `'_a_'` | One char + 'a' + one char: Car, ban, ea7 |

### Example queries:

```sql
-- All login attempts from US or USA (inconsistent data)
SELECT *
FROM log_in_attempts
WHERE country LIKE 'US%';

-- All offices in the East building
SELECT *
FROM employees
WHERE office LIKE 'East%';

-- All employees with IT title (IT Staff, IT Manager, etc.)
SELECT lastname, firstname, title, email
FROM employees
WHERE title LIKE 'IT%';

-- States with 2-letter abbreviation starting with N
SELECT firstname, lastname, state, country
FROM customers
WHERE state LIKE 'N_';
```

> {`LIKE 'US%'` is a great real-world example — logs often have inconsistent data entry. Using a wildcard instead of exact match means you catch all variations without needing to know every format.}

---

## 6. Full Query Template

```sql
SELECT column1, column2        -- what to return
FROM table_name                -- where to look
WHERE column = 'value'         -- filter condition
ORDER BY column DESC;          -- sort order
```

---

## Key Terms

| Term | Definition |
|---|---|
| Query | A request for data from a database table or combination of tables |
| SELECT | Keyword indicating which columns to return |
| FROM | Keyword indicating which table to query |
| WHERE | Keyword indicating the filter condition |
| ORDER BY | Keyword that sorts query results by a specified column |
| DESC | Sorts in descending order (Z→A, largest→smallest) |
| Operator | Symbol or keyword representing an operation (=, >, LIKE, etc.) |
| LIKE | Operator used with WHERE to search for a pattern |
| Wildcard | Special character substituted for unknown characters (% or _) |
| `%` | Wildcard matching any number of characters |
| `_` | Wildcard matching exactly one character |
| Filtering | Selecting only data that matches a condition |

