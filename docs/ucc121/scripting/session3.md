# Session 3: Bash Scripting Fundamentals

This session builds upon basic shell operations by introducing the core concepts of writing executable Bash scripts.

## Learning Objectives

- Understand the structure and execution requirements of a shell script.
- Learn how to use the shebang line, manage script permissions, and handle standard input/output streams.
- Master the use of variables, both local and environment-specific.
- Effectively utilize command substitution for capturing command output.

## Topics Covered

### 1. The Anatomy of a Script

- **The Shebang Line (`#!`):** Understanding `#!/bin/bash` and why it's essential for script execution context.
- **Script Permissions:** Using `chmod +x script_name.sh` to make a script executable.
- **Comments:** Using the `#` symbol for documenting script logic.

### 2. Variables and Data Types

- **Declaring Variables:** `MY_VAR="hello"` (No spaces!). Use `readonly MY_VAR` to prevent modification.
- **Referencing Variables:** Use `${MY_VAR}` to avoid ambiguity (e.g., `${USER}_file`).
- **Arithmetic Expansion:** Use `$(( ... ))` for basic math.
  
  ```bash
  count=5
  echo "Next is $((count + 1))"
  ```

- **Parameter Expansion (Advanced):**
  - `${VAR:-default}`: Use `default` if `VAR` is unset or empty.
  - `${VAR:0:5}`: Extract the first 5 characters.
  - `${#VAR}`: Get the length of the string.
  - `${VAR/old/new}`: Replace the first occurrence of `old` with `new`.

### 3. Input and Output

- **Reading User Input:** Using the `read` command to prompt the user for data dynamically.
- **Command Substitution:** Capturing the output of a command using backticks (`` `command` ``) or modern `$()` syntax (e.g., `CURRENT_DATE=$(date)`).

### 4. Script Arguments (Positional Parameters)

- **Accessing Arguments:** `$0` (script name), `$1`...`$9`. For arguments above 9, use `${10}`.
- **Special Parameters:**
  - `$#`: Number of arguments passed.
  - `$@`: All arguments as separate quoted strings (Recommended!).
  - `$*`: All arguments as a single string.
  - `$$`: Process ID (PID) of the current script.
  - `$!`: PID of the last background job.

## Lab/Assessment Focus

**Goal:** Create an enhanced `user_info.sh` script.

1. **Argument Handling:** Check if a username was provided as `$1`. Use parameter expansion `${1:-$DEFAULT_USER}` to set a default if none is provided.
2. **Input:** If no argument is provided, prompt for it with a 10-second timeout.
3. **Command Substitution:** Capture the User ID (`id -u $USER`) and the number of currently logged-in users (`who | wc -l`).
4. **Math:** Calculate how many more users can join if the limit is 100 using `$((100 - user_count))`.
5. **Output:** Display a detailed summary including the script's own PID (`$$`).

---

## Advanced Topic References

- [`ShellCheck` Guide](https://www.shellcheck.net/): Static analysis tool for shell scripts.
- [Advanced Bash-Scripting Guide - Variables](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_01.html): Detailed variable documentation.
- [The difference between `$*` and `$@` in Bash](https://stackoverflow.com/questions/14059679/the-difference-between-and-in-bash): Understanding argument expansion.
