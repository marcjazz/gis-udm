# UCC121-1, Session 2: Introduction to Shell Scripting

## Topic: From User to Creator - Writing Your First Scripts

---

### 1. The Anatomy of a Script

In Session 1, we customized our environment. Now, we will write standalone programs. A shell script is simply a text file containing a sequence of commands that the shell executes for you.

#### The "Shebang" (`#!`)
Every script should start with a specific line called the **shebang**. It tells the system *which interpreter* should be used to execute the file.

```bash
#!/bin/bash
```

- `#!`: The magic bytes that mark the file as a script.
- `/bin/bash`: The path to the interpreter.

> **Pro Tip:** While `#!/bin/sh` exists, it is often a stricter, POSIX-compliant shell. We use `#!/bin/bash` to unlock modern features like arrays and better string handling.

#### Comments
Comments are lines ignored by the shell, starting with `#`. Use them to explain *why* your code does something, not *what* it does.

```bash
#!/bin/bash

# This script greets the user
# Author: Marco
echo "Hello, World!"
```

### 2. Making it Executable

Creating the file isn't enough. Linux has a permission model that prevents text files from being executed as programs by default.

**The Command:** `chmod` (Change Mode)

```bash
chmod +x my_script.sh
```

- `+x`: Adds **eXecutable** permission.

**Running the Script:**
Once executable, you run it by specifying its path:

```bash
./my_script.sh
```

- Why `./`? Because for security reasons, the current directory (`.`) is usually *not* in your `$PATH`. You must explicitly tell the shell "run the file *right here*".

### 3. Variables & Quoting: The "Gotchas"

In scripting, how you handle text matters immensely.

#### Defining and Using Variables
```bash
name="Alice"      # No spaces around the = sign!
echo "Hello, $name"
```

#### The Quote War: `"` vs `'`
This is the most common source of bugs for beginners.

- **Double Quotes (`"`):** "Weak" quoting. Variables (`$name`) are **expanded** (replaced with their value).
- **Single Quotes (`'`):** "Strong" quoting. Everything inside is treated literally. **No expansion happens.**

**Example:**
```bash
user="Bob"
echo "My name is $user"  # Output: My name is Bob
echo 'My name is $user'  # Output: My name is $user
```

### 4. Interactivity with `read`

Scripts are boring if they don't talk to you. The `read` command pauses execution to get input from the keyboard.

```bash
echo "What is your project name?"
read project_name

echo "Creating project: $project_name..."
mkdir "$project_name"
```

**Optimization:** You can provide a prompt directly inside `read`:
```bash
read -p "Enter username: " user_var
```

### 5. Exit Codes: The Language of Success

Every command in Linux returns a status code when it finishes.
- **`0`**: Success.
- **`1-255`**: Error.

You can access the exit code of the *last* command run using the special variable `$?`.

```bash
mkdir new_folder
echo "The exit code was: $?"
```

If `new_folder` didn't exist, `mkdir` succeeds (0). If it already existed, `mkdir` fails (1), and `$?` will hold `1`.

We can use this to make our scripts smart (which we will cover in depth in Session 3 with `if` statements).

### 6. Command Substitution

Sometimes you want to save the *output* of a command into a variable. We use the `$()` syntax.

```bash
# Save the current date into a variable
current_date=$(date +%F)

# Save the number of files in the current dir
file_count=$(ls | wc -l)

echo "Report for $current_date: Found $file_count files."
```

> **History Lesson:** You might see backticks \`date\` in old tutorials. Avoid them. `$()` is nestable and cleaner.

---

### Lab Exercises (TP)

**Goal:** Create a "New Project Generator" script.

1.  Create a file named `start_project.sh`.
2.  Add the Shebang.
3.  Ask the user for a **Project Name**.
4.  Ask the user for an **Author Name**.
5.  Create a folder with the Project Name.
6.  Inside that folder, create a `README.md` file.
7.  Write the text "Project: [Name] created by [Author]" into the `README.md`.
8.  Make the script executable and run it.

**Bonus:**
Display "Success! Project created at [Path]" using the `pwd` command substitution.

---

### External Resources
- [ShellCheck.net](https://www.shellcheck.net/): The absolute best tool for finding bugs in your scripts. Paste your code there!
- [Explainshell.com](https://explainshell.com/): Type a command line to see a visual breakdown of what each flag does.
