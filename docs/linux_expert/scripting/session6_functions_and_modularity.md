# Session 6: Functions and Modularity

This session teaches how to structure large scripts effectively by creating and utilizing reusable functions, improving readability, maintainability, and reducing code duplication.

## Learning Objectives

- Define and call simple Bash functions.
- Understand and manage variable scope within functions (local vs. global).
- Pass arguments to functions and handle return values.
- Learn to modularize scripts by sourcing function definitions from external files.

## Topics Covered

### 1. Defining Functions

- **Syntax:** Defining functions using `function name { ... }` or the more portable `name () { ... }`.
- **Execution:** Calling a function simply by its name within the script.

### 2. Function Arguments and Return Values

- **Arguments:** Functions treat arguments just like scripts, using `$1`, `$2`, etc.
- **Passing Arrays (Advanced):**

  ```bash
  my_func() {
    local -a arr=("${@}")
    echo "First element: ${arr[0]}"
  }
  list=("apple" "banana")
  my_func "${list[@]}"
  ```

- **Return Values:**
  - Functions return an **exit code** using `return` (0-255).
  - Data can be "returned" via `echo` and command substitution.
  - **Namerefs (Very Advanced):** Using `declare -n` to modify a variable passed by name.

### 3. Variable Scope and Best Practices

- **Global vs Local:** Always use `local` for variables inside functions to avoid "polluting" the global namespace.
- **The `main` Pattern:** For larger scripts, wrap your logic in a `main()` function.

  ```bash
  main() {
    setup
    execute_task
  }
  main "$@"
  ```

### 4. Script Modularity

- **Sourcing Files:** Using the `source` command or the dot operator (`.`) to execute another script file in the _current_ shell environment, making its functions available. This is key for creating script libraries.

## Lab/Assessment Focus

**Goal:** Create a modular calculator tool.

1. **`lib_math.sh`**: Create a library containing functions for `add`, `multiply`, and a recursive `factorial` function.
2. **`app.sh`**:
    - Sources `lib_math.sh`.
    - Uses a `main()` function to parse arguments.
    - Checks if the first argument is "fact" or "calc".
    - Calls the appropriate function and handles errors if the input is not a number.

---

## Advanced Topic References

- [Bash Function Best Practices](https://www.linuxjournal.com/content/use-functions-bash-scripts): Best practices for complex function design.
- [The Bash `local` Keyword Explained](https://www.gnu.org/software/bash/manual/html_node/Shell-Functions.html#Shell-Functions): Official documentation on variable scope.
- [Sourcing vs Executing Scripts](https://mywiki.technical-assistance.ro/index.php/Sourcing_vs._Executing_Scripts): When to use `source` vs `./script.sh`.
