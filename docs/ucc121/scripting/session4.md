# Session 4: Logic and Control Structures

This session introduces the essential building blocks for creating dynamic and decision-making shell scripts: conditional logic and exit code handling.

## Learning Objectives

- Implement conditional logic using `if`, `elif`, and `else` structures.
- Understand and utilize various test operators for file, string, and numeric comparisons.
- Master the use of the `case` statement for multi-way branching.
- Learn to check and utilize command exit codes (`$?`) for flow control.

## Topics Covered

### 1. Conditional Execution with `if` Statements

- **Structure:** The standard `if ... then ... elif ... else ... fi` block.
- **The Test Command:**
  - `[ ... ]`: Standard POSIX test. Needs quoting for variables.
  - `[[ ... ]]`: Modern Bash test. Handles empty variables better and supports pattern matching.
- **Pattern Matching (Advanced):**
  
  ```bash
  if [[ "$filename" == *.jpg ]]; then
    echo "It is a JPEG image."
  fi
  ```

- **Regex Matching (Advanced):**

  ```bash
  if [[ "$email" =~ ^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}$ ]]; then
    echo "Valid email format."
  fi
  ```

### 2. Comparison Operators

- **File Tests:** Checking for existence, type (file/directory), and permissions (`-f`, `-d`, `-r`, `-x`).
- **String Comparisons:** Equality (`=`), inequality (`!=`), and emptiness (`-z`, `-n`).
- **Numeric Comparisons:** Using `-eq`, `-ne`, `-gt`, `-lt` (must use these for numbers, not standard operators like `>`, `<`).

### 3. The `case` Statement

- **Multi-way Branching:** Much cleaner than multiple `if` statements when checking one variable.
- **Pattern Matching & Fall-through:**

  ```bash
  case "$extension" in
    jpg|jpeg|png) echo "Image file" ;;
    mp3|wav|flac) echo "Audio file" ;;
    *)            echo "Unknown format" ;;
  esac
  ```

### 4. Exit Statuses and Short-Circuiting

- **Boolean Logic:**
  - `cmd1 && cmd2`: Run `cmd2` only if `cmd1` succeeded.
  - `cmd1 || cmd2`: Run `cmd2` only if `cmd1` failed.
- **The `!` operator:** Negating a condition.

  ```bash
  if ! grep -q "secret" config.txt; then
    echo "Security check passed."
  fi
  ```

## Lab/Assessment Focus

**Goal:** Create a robust `file_checker.sh`.

1. **Validation:** Use `[[ -z "$1" ]]` to check if an argument was provided.
2. **Logic:** Check if the path exists (`-e`) and if it's a directory (`-d`).
3. **Permissions:** Check if it's readable (`-r`) and writable (`-w`).
4. **Case Statement:** Use a `case` statement to handle different file extensions if the user passes a file instead of a directory.
5. **Output:** Use `&&` to print success only if the previous checks passed.

---

## Advanced Topic References

- [Bash Conditional Expressions](https://www.gnu.org/software/bash/manual/html_node/Conditional-Expressions.html): Official Bash documentation on tests.
- [When to use `[ ]` vs `[[ ]]` in Bash](https://mywiki.technical-assistance.ro/index.php/Bash_Shell_Scripting:_When_to_use_[]_vs._[[]]): A comparison of test syntaxes.
- [Exit Codes Explained](https://linux.die.net/man/0/exit): Understanding process termination values.
