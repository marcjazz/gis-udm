# Session 5: Loops and Iteration

This session focuses on automating repetitive tasks within shell scripts using various looping constructs available in Bash.

## Learning Objectives

- Implement `for` loops to iterate over lists, sequences, and file sets.
- Utilize `while` loops for processing streams of data, such as reading files line-by-line.
- Understand the application of `until` loops.
- Learn flow control statements within loops (`break` and `continue`).

## Topics Covered

### 1. The `for` Loop

- **Iterating Over a List:** `for item in item1 item2 item3; do ... done`.
- **Iterating Over Sequences:** Using brace expansion, e.g., `for i in {1..10}` or `seq`.
- **C-Style For Loop (Advanced):**

  ```bash
  for ((i=0; i<10; i++)); do
    echo "Iteration $i"
  done
  ```

- **File Globbing:** Iterating directly over files matched by a pattern (e.g., `for file in *.log; do ... done`).

### 2. The `while` Loop

- **Reading Input:** The standard pattern for processing files: `while IFS= read -r line; do ... done < input_file`.
  - **`IFS=`**: Prevents word splitting.
  - **`-r`**: Prevents backslash interpretation.
- **Conditional Loops:** Using `while` with a command whose exit status determines continuation (e.g., `while ping -c 1 google.com; do ... done`).
- **Infinite Loops:**

  ```bash
  while true; do
    echo "System pulse check..."
    sleep 5
  done
  ```

### 3. The `until` Loop

- **Inverted Condition:** Executes as long as the command's exit status is **non-zero** (i.e., executes _until_ the command succeeds).

### 4. Loop Control & Advanced Techniques

- **`break`**: Exiting the loop immediately.
- **`continue`**: Skipping the remainder of the current iteration.
- **The `select` Loop (User Menus):**

  ```bash
  PS3="Choose an option: "
  select opt in "Update" "Status" "Quit"; do
    case $opt in
      "Update") sudo apt update ;;
      "Status") uptime ;;
      "Quit") break ;;
    esac
  done
  ```

## Lab/Assessment Focus

**Goal:** Create an advanced `bulk_rename.sh`.

1. **Safety:** Before renaming, use `[[ -w "$1" ]]` to verify write permissions.
2. **Iterate:** Use a `for` loop to find all `.log` files.
3. **String Manipulation:** Use `${file%.log}_backup.log` to generate the new name.
4. **Batching:** Add a `while` loop that asks the user "Are you sure?" before each rename, unless the `-y` flag is passed as the second argument.
5. **Menu:** At the end, use a `select` loop to ask the user if they want to view the renamed files or exit.

---

## Advanced Topic References

- [Bash `while read` Loop Best Practice](https://unix.stackexchange.com/questions/110701/best-practice-for-reading-a-file-line-by-line-in-a-bash-script): In-depth look at safe file reading.
- [Bash For Loop Variations](https://linuxhandbook.com/for-loop-bash/): Comprehensive examples of `for` loop usage.
- [Loop Flow Control in Bash](https://www.cyberciti.biz/faq/bash-break-continue-loop-control-statements/): How to control loop execution.
