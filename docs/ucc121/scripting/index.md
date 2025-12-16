# Detailed Course Plan: UCC121-1

This document outlines the course plan for the "Shells, Scripting, and Data Management" module.

---

# UCC121-1: Shells, Scripting, and Data Management

## Course Information Sheet
- **Title:** Shells, Scripting, and Data Management
- **Code:** UCC121-1
- **Prerequisites:** Basic proficiency with the Linux command line (UCC111 or equivalent).
- **Duration:** 12 hours (8 sessions of 1.5 hours each).
- **Objectives:**
    - Master advanced command-line tools.
    - Create robust and modular shell scripts for automation.
    - Manipulate text data and interact with a simple database.
- **Assessment:** Continuous assessment (Practical Labs), scripting project, final exam.

## 8-Session Breakdown

### Session 1: Mastering the Shell Environment
- **Lesson:** Fundamentals of the Bash shell, customizing `.bashrc`, managing aliases, functions, and environment variables (`PATH`, `PS1`).
- **Lab/Assessment:** Create useful aliases, write a function to automate a simple task (e.g., `mkcd`), and customize the command prompt.

### Session 2: Text Processing Tools: `grep`, `sed`, `awk`
- **Lesson:** Introduction to regular expressions. Using `grep` for searching, `sed` for substitution, and `awk` for column extraction.
- **Lab/Assessment:** Extract all IP addresses from a log file. Replace a string in a series of configuration files.

### Session 3: Bash Scripting Fundamentals
- **Lesson:** Anatomy of a script (shebang, permissions), variables, reading user input (`read`), handling parameters (`$1`, `$@`), command substitution `$(...)`.
- **Lab/Assessment:** Write a script that takes a filename as a parameter and displays its first 3 lines.

### Session 4: Logic and Control Structures
- **Lesson:** `if/elif/else` conditions, file and string tests `[[ ... ]]`. The `case` statement. Handling exit codes (`$?`).
- **Lab/Assessment:** Write a script that checks if a user exists in `/etc/passwd`.

### Session 5: Loops and Iteration
- **Lesson:** `for` loops (over lists, sequences, files), `while` loops (to read a file line-by-line), and `until` loops.
- **Lab/Assessment:** Write a script that bulk renames all `.jpeg` files in a folder to `.jpg`.

### Session 6: Functions and Modularity
- **Lesson:** Declaring and calling functions, variable scope (local/global), passing arguments, and returning values. Sourcing function files.
- **Lab/Assessment:** Transform a monolithic script into a modular script using functions.

### Session 7: Introduction to Data Management with SQL
- **Lesson:** Principles of relational databases. Using `sqlite3` for `CREATE TABLE`, `INSERT`, `SELECT`, `UPDATE`, `DELETE`.
- **Lab/Assessment:** Create a simple inventory database and write a shell script to query it.

### Session 8: Process Management and Automation with `cron`
- **Lesson:** Managing background jobs (`&`, `jobs`, `fg`, `bg`, `nohup`). Scheduling tasks with `cron`.
- **Lab/Assessment:** Launch a script as a background task. Schedule a backup script to run every night.

---

# Glossary of Terms

- **`awk`**: A powerful command-line tool for processing and analyzing column-based text data.
- **`alias`**: A custom shortcut for a longer command. Defined in shell configuration files.
- **`Bash` (Bourne Again SHell)**: The default command-line interpreter on most Linux systems.
- **`.bashrc`**: A script file that is executed every time a new interactive shell is started. Used for personal customizations.
- **`cron`**: A time-based job scheduler in Unix-like operating systems. Used to automate repetitive tasks.
- **`crontab`**: The file or command used to specify the schedule of cron jobs.
- **Environment Variable**: A dynamic named value that can affect the way running processes will behave on a computer. `PATH` and `HOME` are examples.
- **`grep`**: A command-line utility for searching plain-text data sets for lines that match a regular expression.
- **`function`**: A reusable block of code that is more powerful than an alias and can accept arguments.
- **`PATH`**: An environment variable specifying the set of directories where executable programs are located.
- **`PS1`**: The primary prompt string environment variable, which controls the appearance of the command prompt.
- **Regular Expression (Regex)**: A sequence of characters that specifies a search pattern in text.
- **`sed`**: A "stream editor" utility for parsing and transforming text.
- **`Shebang` (`#!`)**: The first two characters of a script, which tell the system what interpreter to use to run it (e.g., `#!/bin/bash`).
- **`Shell`**: A user interface for access to an operating system's services. In this context, a command-line interface (CLI).
- **`SQL` (Structured Query Language)**: A standard language for managing and manipulating data in relational databases.
- **`sqlite3`**: A command-line interface to a self-contained, serverless, zero-configuration, transactional SQL database engine.
