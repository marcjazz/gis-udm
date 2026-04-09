---
marp: true
theme: default
paginate: true
header: 'Linux Shell Scripting & Automation Exam'
footer: 'Time Allowed: 1h 30min | 1.5 min per question'
---

# Linux Shell Scripting and Automation Exam
**Duration:** 1 hour 30 minutes
**Total Questions:** 60
**Format:** Multiple Choice

---

## Session 1: Mastering the Shell Environment

### Question 1
Which file is used to store system-wide aliases and functions for bash users?
A) `~/.bashrc`
B) `/etc/bashrc` (or `/etc/bash.bashrc`)
C) `~/.bash_profile`
D) `/etc/profile`

---

### Question 2
What is the purpose of the `export` command in a shell environment?
A) To save a file to disk.
B) To make a shell variable available to child processes (as an environment variable).
C) To send a variable over the network.
D) To permanently save a variable across reboots.

---

### Question 3
Which of the following commands correctly creates an alias named `ll` for `ls -la`?
A) `alias ll ls -la`
B) `alias ll="ls -la"`
C) `set alias ll="ls -la"`
D) `alias "ls -la" ll`

---

### Question 4
What does the `$PATH` environment variable do?
A) It specifies the home directory of the current user.
B) It stores the location of the bash executable.
C) It contains a colon-separated list of directories the shell searches for executable commands.
D) It stores the history of recently executed commands.

---

### Question 5
How do you temporarily modify the `$PATH` to include `/opt/bin` for the current session only?
A) `PATH=$PATH:/opt/bin`
B) `export PATH=/opt/bin:$PATH`
C) `set PATH=$PATH:/opt/bin`
D) Both A and B are acceptable (B makes it an environment variable).

---

### Question 6
Which file is executed only for login shells?
A) `~/.bashrc`
B) `~/.bash_profile` (or `~/.profile`)
C) `/etc/bashrc`
D) `~/.bash_logout`

---

## Session 2: Introduction to Shell Scripting

### Question 7
What is a "shebang" in shell scripting?
A) A comment used to explain code.
B) A character sequence (`#!`) at the start of a script that specifies the interpreter to use.
C) A command to force script execution.
D) The exit status of a failed command.

---

### Question 8
Which of the following is the correct shebang for a standard bash script?
A) `#bash`
B) `#!/bin/sh`
C) `#!/bin/bash`
D) `!#/bin/bash`

---

### Question 9
Before executing a newly created shell script `myscript.sh`, what permission must be granted?
A) Read (`chmod +r myscript.sh`)
B) Write (`chmod +w myscript.sh`)
C) Execute (`chmod +x myscript.sh`)
D) SUID (`chmod +s myscript.sh`)

---

### Question 10
If the current directory (`.`) is not in your `$PATH`, how must you run an executable script named `script.sh` located in your current directory?
A) `script.sh`
B) `bash script.sh`
C) `./script.sh`
D) Both B and C are correct ways to execute it.

---

### Question 11
What is the purpose of adding comments to a shell script using `#`?
A) To improve execution speed.
B) To encrypt the code.
C) To explain the logic and make the script readable for humans.
D) To hide syntax errors from the interpreter.

---

### Question 12
Which command is used to display output from a shell script to the terminal?
A) `print`
B) `echo`
C) `display`
D) `write`

---

## Session 3: Bash Scripting Fundamentals

### Question 13
How do you declare and initialize a variable named `name` with the value `John` in bash?
A) `name = "John"`
B) `name="John"`
C) `set name="John"`
D) `let name="John"`

---

### Question 14
Which of the following correctly accesses the value of the variable `name`?
A) `&name`
B) `@name`
C) `$name`
D) `%name`

---

### Question 15
What are the `$1`, `$2`, `$3` special variables used for in a shell script?
A) They represent the script's exit codes.
B) They store the results of the last three commands.
C) They represent the positional parameters (command-line arguments) passed to the script.
D) They are reserved variables for user passwords.

---

### Question 16
Which special variable holds the total number of arguments passed to the script?
A) `$*`
B) `$@`
C) `$?`
D) `$#`

---

### Question 17
What is the difference between single quotes (`'...'`) and double quotes (`"..."`) in bash?
A) Single quotes allow variable expansion, double quotes do not.
B) Double quotes preserve the literal value of all characters, single quotes do not.
C) Double quotes allow variable expansion (`$var`), single quotes treat everything literally.
D) There is no difference.

---

### Question 18
Which variable holds the exit status of the last executed command?
A) `$$`
B) `$!`
C) `$?`
D) `$0`

---

### Question 19
What does an exit status of `0` typically indicate in Linux?
A) General failure
B) Command not found
C) Success
D) Syntax error

---

### Question 20
How do you capture the output of a command and assign it to a variable?
A) `var=command`
B) `var=$(command)` (Command substitution)
C) `var={command}`
D) `var=[command]`

---

## Session 4: Logic and Control Structures

### Question 21
Which syntax is correct for a basic `if` statement in bash?
A) `if [ condition ]; then ... fi`
B) `if ( condition ) then ... end`
C) `if { condition } then ... fi`
D) `if [ condition ] then ... end if`

---

### Question 22
Which operator is used to check if two strings are equal in a single-bracket test `[ ... ]`?
A) `==` or `=`
B) `-eq`
C) `<=>`
D) `===`

---

### Question 23
Which operator is used to numerically compare if one value is strictly greater than another?
A) `>`
B) `-gt`
C) `>=`
D) `-ge`

---

### Question 24
What does the condition `[ -f "$file" ]` test?
A) If `$file` is a directory.
B) If `$file` exists and is a regular file.
C) If `$file` is readable.
D) If `$file` exists and has a size greater than zero.

---

### Question 25
What does the condition `[ -d "$dir" ]` test?
A) If `$dir` is empty.
B) If `$dir` exists and is a directory.
C) If `$dir` has executable permissions.
D) If `$dir` has been deleted.

---

### Question 26
Which operator performs a logical AND operation between two test conditions?
A) `&&` or `-a`
B) `||` or `-o`
C) `+`
D) `&`

---

### Question 27
Which structure is best suited for testing a single variable against multiple possible string values?
A) Nested `if` / `else`
B) `case` / `esac`
C) `for` loop
D) `while` loop

---

### Question 28
In a `case` statement, what symbol is used to denote the end of a specific case block?
A) `;`
B) `;;`
C) `break`
D) `done`

---

## Session 5: Loops and Iteration

### Question 29
Which loop is ideal for iterating over a known list of items, such as files in a directory or words in a string?
A) `while` loop
B) `until` loop
C) `for` loop
D) `do...while` loop

---

### Question 30
What is the correct syntax for a `for` loop iterating from 1 to 5?
A) `for i in 1 2 3 4 5; do ... done`
B) `for i in {1..5}; do ... done`
C) `for ((i=1; i<=5; i++)); do ... done`
D) All of the above

---

### Question 31
Which loop continues to execute as long as its condition evaluates to true (exit status 0)?
A) `for` loop
B) `while` loop
C) `until` loop
D) `select` loop

---

### Question 32
Which loop continues to execute as long as its condition evaluates to false (non-zero exit status)?
A) `for` loop
B) `while` loop
C) `until` loop
D) `break` loop

---

### Question 33
How do you safely read a file line-by-line in a bash script?
A) `for line in $(cat file.txt); do ... done`
B) `while IFS= read -r line; do ... done < file.txt`
C) `cat file.txt | for line; do ... done`
D) `read file.txt > line`

---

### Question 34
What does the `break` command do when used inside a loop?
A) It pauses the loop for a specified number of seconds.
B) It skips the rest of the current iteration and jumps to the next one.
C) It completely terminates the loop and resumes execution after the `done` keyword.
D) It exits the entire script immediately.

---

### Question 35
What does the `continue` command do when used inside a loop?
A) It exits the entire script.
B) It completely terminates the loop.
C) It stops the loop to wait for user input.
D) It skips the remaining commands in the current iteration and begins the next iteration of the loop.

---

### Question 36
If you run an infinite `while` loop in a script by mistake, how can you forcefully stop it from the terminal?
A) Press `Ctrl+C`
B) Press `Ctrl+Z`
C) Press `Esc`
D) Press `Ctrl+D`

---

## Session 6: Functions and Modularity

### Question 37
How do you declare a function named `my_func` in bash?
A) `function my_func() { ... }`
B) `my_func() { ... }`
C) Both A and B are valid
D) `def my_func(): ...`

---

### Question 38
How do you call (execute) a function named `backup_files` within a script?
A) `call backup_files`
B) `backup_files()`
C) `backup_files`
D) `run backup_files`

---

### Question 39
How are arguments passed to a function in a bash script?
A) Inside parentheses: `my_func(arg1, arg2)`
B) They are read from standard input using `read`.
C) Space-separated after the function name: `my_func arg1 arg2`
D) Via environment variables only.

---

### Question 40
Inside a function, how do you access the first argument passed specifically to that function?
A) `$1`
B) `$@`
C) `$_1`
D) `ARG1`

---

### Question 41
By default, what is the scope of variables declared inside a bash function?
A) Local (only accessible within the function).
B) Global (accessible throughout the entire script after execution).
C) Exported (accessible to child processes).
D) Read-only.

---

### Question 42
How do you declare a variable inside a function so that it does not affect a variable with the same name outside the function?
A) `var="value"`
B) `private var="value"`
C) `local var="value"`
D) `set var="value"`

---

### Question 43
What command is used to exit a function and optionally return a numeric status code to the caller?
A) `exit`
B) `return`
C) `break`
D) `yield`

---

### Question 44
What happens if a script calls `exit 1` inside a function?
A) Only the function terminates.
B) The loop containing the function terminates.
C) The entire script immediately terminates with exit status 1.
D) The function returns 1 and the script continues.

---

## Session 7: Introduction to Data Management with SQL

### Question 45
Although shell scripts manipulate files well, when is an SQL database preferred?
A) For simple text manipulation.
B) When managing structured, relational data requiring complex queries and concurrency.
C) When listing files in a directory.
D) When scheduling cron jobs.

---

### Question 46
Which command-line tool is commonly used in bash scripts to execute queries against a MySQL/MariaDB database?
A) `mysql`
B) `psql`
C) `sqlite3`
D) `dbquery`

---

### Question 47
How can you pass a simple SQL query to a database client non-interactively within a script?
A) `mysql -u user -p pass -e "SELECT * FROM table;"`
B) `echo "SELECT * FROM table;" | mysql -u user -p pass`
C) Using a Here-Doc (`<<EOF ... EOF`)
D) All of the above are valid methods.

---

### Question 48
Which SQL statement is used to retrieve data from a database table?
A) `FETCH`
B) `GET`
C) `SELECT`
D) `PULL`

---

### Question 49
What is a common risk when constructing SQL queries dynamically using bash variables (e.g., `mysql -e "SELECT * FROM users WHERE user='$VAR'"`)?
A) Buffer overflow
B) SQL Injection
C) Cross-Site Scripting (XSS)
D) Path Traversal

---

### Question 50
Which lightweight, file-based database is excellent for simple local script data storage without needing a separate database server?
A) Oracle
B) PostgreSQL
C) SQLite
D) Redis

---

## Session 8: Process Management and Automation

### Question 51
Which bash operator is used to run a command in the background?
A) `;`
B) `|`
C) `&`
D) `&&`

---

### Question 52
If you start a long-running process and suspend it with `Ctrl+Z`, which command will resume it in the background?
A) `fg`
B) `bg`
C) `jobs`
D) `resume`

---

### Question 53
Which command lists all background jobs currently managed by the active shell session?
A) `ps`
B) `top`
C) `jobs`
D) `tasks`

---

### Question 54
Which command ensures a script or process continues running even after the user logs out or closes the terminal?
A) `nohup`
B) `keepalive`
C) `systemctl`
D) `bg`

---

### Question 55
What is the primary tool used in Linux to schedule scripts to run automatically at specific times or intervals?
A) `at`
B) `cron`
C) `systemd-timer`
D) Both B and C

---

### Question 56
What is the format of a cron schedule expression?
A) `minute hour day_of_month month day_of_week command`
B) `hour minute month day_of_month day_of_week command`
C) `second minute hour day month command`
D) `day month year time command`

---

### Question 57
Which crontab entry runs a backup script every day at 2:30 AM?
A) `30 2 * * * /path/to/backup.sh`
B) `2 30 * * * /path/to/backup.sh`
C) `0 2 30 * * /path/to/backup.sh`
D) `* * 2 30 * /path/to/backup.sh`

---

### Question 58
Which command opens the user's crontab file for editing?
A) `cron -e`
B) `crontab -e`
C) `edit-cron`
D) `vi /etc/crontab`

---

### Question 59
What happens to the standard output and standard error of a cron job by default?
A) They are discarded to `/dev/null`.
B) They are printed to the active console.
C) They are emailed to the user account that executed the cron job.
D) They are saved in `/var/log/cron.log`.

---

### Question 60
To redirect both standard output (stdout) and standard error (stderr) of a cron job to a log file, which syntax should you append to the command?
A) `> /var/log/script.log 2>&1`
B) `>> /var/log/script.log`
C) `2> /var/log/script.log`
D) `| out /var/log/script.log`

---

## Answer Key

**1-10:** 1. B | 2. B | 3. B | 4. C | 5. B | 6. B | 7. B | 8. C | 9. C | 10. D
**11-20:** 11. C | 12. B | 13. B | 14. C | 15. C | 16. D | 17. C | 18. C | 19. C | 20. B
**21-30:** 21. A | 22. A | 23. B | 24. B | 25. B | 26. A | 27. B | 28. B | 29. C | 30. D
**31-40:** 31. B | 32. C | 33. B | 34. C | 35. D | 36. A | 37. C | 38. C | 39. C | 40. A
**41-50:** 41. B | 42. C | 43. B | 44. C | 45. B | 46. A | 47. D | 48. C | 49. B | 50. C
**51-60:** 51. C | 52. B | 53. C | 54. A | 55. D | 56. A | 57. A | 58. B | 59. C | 60. A