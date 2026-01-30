# Session 7: Introduction to Data Management with SQL

This session bridges the gap between shell scripting and structured data management by introducing the basics of working with relational databases directly from the command line using SQLite.

## Learning Objectives

- Understand the core principles of Relational Database Management Systems (RDBMS).
- Learn the essential SQL commands for data definition and manipulation (DDL/DML).
- Use the `sqlite3` command-line utility to interact with a database file.
- Integrate database operations into Bash scripts.

## Topics Covered

### 1. Relational Database Concepts

- **Tables, Rows, and Columns:** Defining the basic structure.
- **Primary Keys and Data Types:** Brief overview of common types (INTEGER, TEXT, REAL).

### 2. Essential SQL Commands (Using `sqlite3`)

- **Data Definition Language (DDL):**
  - `CREATE TABLE`: Defining a new table structure.
- **Data Manipulation Language (DML):**
  - `INSERT INTO`: Adding new records.
  - `SELECT`: Querying data (including `WHERE` clauses for filtering).
  - `UPDATE`: Modifying existing records.
  - `DELETE FROM`: Removing records.

### 3. Command-Line Database Interaction

- **Invoking `sqlite3`:** Opening a database file (`sqlite3 inventory.db`).
- **Executing SQL:**
  - **Inline:** `sqlite3 db.sqlite "SELECT * FROM users;"`
  - **Heredoc (Recommended for Scripts):**

    ```bash
    sqlite3 inventory.db <<EOF
    INSERT INTO Products (Name, Quantity) VALUES ('Apples', 50);
    SELECT * FROM Products WHERE Quantity < 100;
    EOF
    ```

- **Output Formatting:** Use `-csv`, `-column`, or `-json` flags to get data in a format scripts can easily parse.
- **SQLite Dot-Commands (Advanced):**
  - `.mode csv`: Switch output to CSV.
  - `.import file.csv table`: Import data from a CSV file.
  - `.schema`: Show the database structure.

### 4. Transactions and Integrity (Advanced)

- **Transactions:** Grouping multiple commands for safety.

  ```sql
  BEGIN TRANSACTION;
  UPDATE Accounts SET balance = balance - 100 WHERE id = 1;
  UPDATE Accounts SET balance = balance + 100 WHERE id = 2;
  COMMIT;
  ```

## Lab/Assessment Focus

**Goal:** Build a scriptable inventory manager.

1. **Initialize:** Create a script that initializes `inventory.db` using a Heredoc.
2. **Import:** Export sample data from a CSV file into the `Products` table using `.import`.
3. **Query:** Write a function `get_low_stock()` that queries the database for products with quantity less than a threshold passed as an argument.
4. **Format:** Use the `-json` output format and pipe it to a script that simulates sending an alert (just echo for now).
5. **Transaction:** Implement an `update_stock` function that uses a transaction to ensure data integrity.

---

## Advanced Topic References

- [SQLite Command Line Shell Tutorial](https://www.sqlite.org/cli.html): Official guide to the `sqlite3` utility.
- [SQL Tutorial for Beginners](https://www.w3schools.com/sql/): Comprehensive SQL language reference.
- [Bash Scripting and SQLite Integration](https://www.sitepoint.com/using-sqlite-from-bash/): Examples of piping data into the CLI tool.
