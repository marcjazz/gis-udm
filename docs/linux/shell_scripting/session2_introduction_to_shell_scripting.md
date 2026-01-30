# Session 2: Introduction to Shell Scripting

## Topic: From User to Creator - Writing Your First Scripts

---

### 1. The Anatomy of a Script

In Session 1, we customized our environment. Now, we will write standalone programs. A shell script is simply a text file containing a sequence of commands that the shell executes for you.

#### The "Shebang" (`#!`)

Every script should start with a specific line called the **shebang**. It tells the system _which interpreter_ should be used to execute the file.

```bash
#!/bin/bash
```

- `#!`: The magic bytes that mark the file as a script.
- `/bin/bash`: The path to the interpreter.

> **Advanced Tip: Portability**
> Instead of `#!/bin/bash`, you might see `#!/usr/bin/env bash`. This is more portable because it finds `bash` wherever it is in the system's `$PATH`, which is useful on systems where bash isn't in `/bin` (like macOS or BSD).

#### Comments

Comments are lines ignored by the shell, starting with `#`. Use them to explain _why_ your code does something, not _what_ it does.

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

- Why `./`? Because for security reasons, the current directory (`.`) is usually _not_ in your `$PATH`. You must explicitly tell the shell "run the file _right here_".

### 3. Variables & Quoting: The "Gotchas"

### 4. Debugging Your Scripts

When things go wrong, you need to see what the shell is doing.

- **Trace Mode:** Add `set -x` at the top of your script (after the shebang). It will print every command before executing it.
- **Exit on Error:** Add `set -e` to make the script stop immediately if any command fails.

```bash
#!/bin/bash
set -x  # Enable debugging
set -e  # Stop on errors
```

### 5. Variables & Quoting: The "Gotchas"

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

### 6. Interactivity and Multi-line Output

#### Advanced `read` usage

The `read` command has several useful flags:

- `-p`: Display a prompt.
- `-s`: Silent mode (useful for passwords).
- `-t 5`: Timeout after 5 seconds if no input is provided.

```bash
read -s -p "Enter your secret key: " secret_key
```

#### Heredocs: Multi-line Text Blocks

Instead of using many `echo` commands, use a **Heredoc** to output large blocks of text or create files.

```bash
cat <<EOF > welcome.txt
Welcome to the system, $USER!
Today is $(date)
Enjoy your stay.
EOF
```

### 7. Exit Codes: The Language of Success

Every command in Linux returns a status code when it finishes.

- **`0`**: Success.
- **`1-255`**: Error.

You can access the exit code of the _last_ command run using the special variable `$?`.

```bash
mkdir new_folder
echo "The exit code was: $?"
```

If `new_folder` didn't exist, `mkdir` succeeds (0). If it already existed, `mkdir` fails (1), and `$?` will hold `1`.

We can use this to make our scripts smart (which we will cover in depth in Session 3 with `if` statements).

### 8. Command Substitution

Sometimes you want to save the _output_ of a command into a variable. We use the `$()` syntax.

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

1. Create a file named `start_project.sh`.
2. Add the Shebang (`#!/usr/bin/env bash`).
3. Enable debug mode with `set -x`.
4. Ask the user for a **Project Name**.
5. Ask the user for an **Author Name**.
6. Create a folder with the Project Name.
7. Use a **Heredoc** to create a `README.md` file inside that folder with the project and author info.
8. Make the script executable and run it.

**Bonus:**
Display "Success! Project created at [Path]" using the `pwd` command substitution.

---

### External Resources

- [ShellCheck.net](https://www.shellcheck.net/): The absolute best tool for finding bugs in your scripts. Paste your code there!
- [Explainshell.com](https://explainshell.com/): Type a command line to see a visual breakdown of what each flag does.
