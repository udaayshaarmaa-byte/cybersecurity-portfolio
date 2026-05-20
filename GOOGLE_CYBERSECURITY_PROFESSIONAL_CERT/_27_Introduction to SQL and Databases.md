# Databases, SQL & Linux vs SQL Filtering — Note

## 1. What is a Database?

A **database** = an organised collection of information or data.

| | Spreadsheet | Database |
|---|---|---|
| Users | Single user or small team | Multiple simultaneous users |
| Data volume | Limited | Massive scale |
| Complex tasks | Limited | Supported |
| Example | Google Sheets | SQL database |

As a security analyst, you'll regularly query databases containing: login attempts, software update status, machine inventories, user accounts.

---

## 2. Relational Databases

A **relational database** = structured database containing tables that are related to each other.

### Structure:
- **Table** = organised set of related data
- **Column (Field)** = a category of data (e.g. `employee_id`, `username`, `department`)
- **Row (Record)** = a single entry of data (e.g. one employee's full record)

### Keys connecting tables:

| Key Type | Description | Rules |
|---|---|---|
| **Primary Key** | Uniquely identifies every row in a table | No duplicates; no null/empty values; one per table |
| **Foreign Key** | A column that is a primary key in another table | Can have duplicates and empty values; used to connect tables |

**Example:**
- `employees` table: `employee_id` is the **primary key**
- `machines` table: `employee_id` is a **foreign key** — links each machine to its owner

A table can have **only one primary key** but **multiple foreign keys**.

> {Primary key = the unique ID for that table. Foreign key = a reference pointing to another table's primary key. This is how relational databases link data across tables without duplicating it everywhere.}

---

## 3. SQL Structured Query Language

**SQL** = programming language used to create, interact with, and request information from a database.

**Query** = a request for data from a database table or combination of tables.

Nearly all relational databases use some version of SQL  versions differ only slightly (e.g. placement of quotation marks).

### Why SQL matters for security analysts:

| Use case | Example |
|---|---|
| Log retrieval | Pull all login attempts from the last 24 hours |
| Anomaly detection | Find unusual access patterns in web server logs |
| Patch management | Identify machines that haven't received the latest update |
| Maintenance scheduling | Find when machines are least used to plan updates |

SQL searches millions of data points in seconds with a single query  essential for handling large security logs.

---

## 4. Accessing SQL via Linux

- SQL can be accessed directly from the Linux command line
- Example: type `sqlite3` in the terminal to launch SQLite
- Once inside SQL, commands are directed to the database, not the Linux shell

---

## 5. Linux vs SQL Filtering Key Differences

| Dimension | Linux | SQL |
|---|---|---|
| **Purpose** | Filter files and directories on a system | Filter structured data within a database |
| **Common tools/keywords** | `grep`, `find`, `sed`, `cut`, `awk` | `SELECT`, `WHERE`, `JOIN` |
| **Structure** | Free-form text output | Organised into columns and rows |
| **Readability** | Data returned as lines of plain text | Data returned as a structured table |
| **Joining data** | Cannot link data across files | Can join multiple tables in one query |
| **Best for** | Text files, logs not in database format | Database-stored logs, structured records |

### When to use which:

- **SQL** → data is stored in a database (most enterprise security logs)
- **Linux** → data is in a text file or format incompatible with SQL (e.g. raw `.log` files, config files)

> {Both are essential skills. In the real world, some logs land in a SIEM database (SQL), some are raw text files on a server (Linux grep). You need both  and you already have Linux command line experience from your home labs.}

---

## Key Terms

| Term | Definition |
|---|---|
| Database | Organised collection of information or data |
| Relational Database | Database with multiple tables that are connected to each other |
| Table | Organised set of data within a database |
| Column / Field | Category of data in a table (e.g. username) |
| Row / Record | A single entry in a table |
| Primary Key | Uniquely identifies every row; no duplicates or nulls; one per table |
| Foreign Key | References the primary key of another table; used to connect tables |
| SQL | Structured Query Language used to query and interact with databases |
| Query | A request for data from a database |
| SQLite | A lightweight version of SQL; accessible via `sqlite3` in Linux |

