# Plan for Interactive Sessions 3 & 4: Bash Scripting

## Session 3: Bash Scripting Fundamentals

- **Slide 1: Title Slide**
  - "Session 3: Bash Scripting Fundamentals"
- **Slide 2: Recap & Challenge**
  - **Instructor:** "Remember `_`? What was it for? What about `$_`?" (from Session 2)
  - **Interaction:** Students answer in chat. Instructor shows a quick demo of `$_`.
- **Slide 3: Exercise - `log_and_run.sh`**
  - **Instructions:** "Let's build a script that logs a command and then runs it."
  - **Code:** `#!/bin/bash`
  - **Interaction:** "What's the first line for?" (Students answer). "How do we get all arguments?" (Students answer: `$@`).
- **Slide 4: Building the script**
  - **Code:** `echo "Running: $@" >> command.log`
  - **Interaction:** "What does `>>` do?" (Students answer).
- **Slide 5: Making it executable**
  - **Instructions:** "Run the script with `ls -l`. What happens?"
  - **Interaction:** Students run, get "permission denied". "How do we fix?" (Students answer: `chmod +x`).
- **Slide 6: Running the script**
  - **Code:** `./log_and_run.sh ls -l`
  - **Interaction:** "Check `command.log`. Did it work?"
- **Slide 7: Adding Variables**
  - **Instructions:** "Let's make the log file a variable."
  - **Code:** `LOG_FILE="command.log"`
  - **Interaction:** "Why `UPPER_CASE`?" (Students answer: convention).
- **Slide 8: Quotes**
  - **Instructions:** "Try running with `echo "Hello World"`. What happens in the log?"
  - **Interaction:** Students see the quotes are gone. "How to keep them?" (Students answer: use quotes around `$@`).
- **Slide 9: Command Substitution**
  - **Instructions:** "Let's add a timestamp."
  - **Code:** `echo "$(date): Running: $@" >> "$LOG_FILE"`
  - **Interaction:** "What does `$(...)` do?" (Students answer).
- **Slide 10: Exit Codes**
  - **Instructions:** "Run with a failing command like `ls /nonexistent`. Then run `echo $?`."
  - **Interaction:** "What does the number mean?" (Students answer).

## Session 4: Logic and Control Structures

- **Slide 1: Title Slide**
  - "Session 4: Logic and Control Structures"
- **Slide 2: The `if` statement**
  - **Instructions:** "Let's make our script safer. Only run if the log file exists."
  - **Code:** `if [ -f "$LOG_FILE" ]; then`
  - **Interaction:** "What does `[` mean? What about `-f`?" (Students answer).
- **Slide 3: `if/else`**
  - **Instructions:** "What if the file *doesn't* exist?"
  - **Code:** `else echo "Log file not found!"`
  - **Interaction:** "How do we end the `if` block?" (Students answer: `fi`).
- **Slide 4: `case` statements**
  - **Instructions:** "Let's add a `--verbose` option."
  - **Code:**
    ```bash
    case "$1" in
      --verbose)
        echo "Verbose mode on"
        shift
        ;;
    esac
    ```
  - **Interaction:** "What does `shift` do here?" (Students answer).
- **Slide 5: `for` loops**
  - **Instructions:** "Let's run multiple commands."
  - **Code:** `for cmd in "$@"; do`
  - **Interaction:** "What will this do if we run `./log_and_run.sh ls -l`?" (Students answer).
- **Slide 6: `while` loops**
  - **Instructions:** "Let's create a script that waits for a file to exist."
  - **Code:** `while [ ! -f /tmp/stop ]; do`
  - **Interaction:** "What does `!` do?" (Students answer).
- **Slide 7: Combining it all**
  - **Instructions:** "Let's combine these concepts into a final script."
  - **Interaction:** Collaborative script building session.

This plan focuses on building a single, practical script over the two sessions, introducing new concepts as they are needed. This exercise-driven approach should keep students engaged and minimize instructor talk time.
