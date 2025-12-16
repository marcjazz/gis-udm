# UCC121-1, Session 1: Course Content
## Topic: Mastering the Shell Environment

---

### 1. What is a Shell?

A **shell** is a program that provides the user with a direct interface to the operating system. It takes your commands, interprets them, and asks the operating system to perform the requested action.

- **Interface:** It's a Command-Line Interface (CLI).
- **Role:** Sits between you (the user) and the operating system's core (the **kernel**).
- **Default Shell:** On most Linux systems, the default shell is `bash` (the **B**ourne **A**gain **SH**ell).

You can find out what shell you are using with the command: `echo $SHELL`

### 2. The `.bashrc` File: Your Personal Toolbox

When you start an interactive shell, it automatically runs a script to set up your environment. This script is `.bashrc` (located in your home directory, `~/.bashrc`).

- **Purpose:** To store all your personal customizations: aliases, functions, and environment variables.
- **Activation:** Changes made to `.bashrc` are not applied automatically to your current session. You must load them by either:
    1.  Starting a new shell session.
    2.  Running the command `source ~/.bashrc`.

### 3. Aliases: Your Command-Line Shortcuts

An alias is a simple way to create a shortcut for a longer command. They are perfect for commands you use often.

**Syntax:** `alias shortcut_name='the_long_command'`

**Common & Useful Examples:**

```bash
# Make 'ls' more informative and colorful
alias ls='ls --color=auto'
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'

# Shortcuts for system updates (Debian/Ubuntu)
alias update='sudo apt update && sudo apt upgrade'

# Show open ports
alias ports='netstat -tulpn'
```

**How to add them:** Open `~/.bashrc` with a text editor (like `nano` or `vim`) and add these lines. Then run `source ~/.bashrc`.

**Removing an alias:** `unalias shortcut_name`

### 4. Functions: Super-Powered Aliases

Functions are like aliases, but they are more powerful. They can accept arguments (parameters), contain multiple commands, and use logic.

**Syntax:**
```bash
function_name() {
  # command 1
  # command 2
  # use $1, $2 for arguments
}
```

**Example: The `mkcd` function**

A common task is to create a directory and then immediately navigate into it.
- **Problem:** `mkdir new_dir` followed by `cd new_dir`.
- **Solution:** A function that does both!

```bash
# Creates a directory and changes into it
mkcd() {
  mkdir -p "$1" && cd "$1"
}
```

- `mkdir -p "$1"`: Creates the directory. `-p` ensures it doesn't fail if the directory exists and also creates parent directories if needed. `"$1"` is the first argument you provide to the function.
- `&&`: This is a logical AND. The `cd "$1"` command only runs if the `mkdir` command was successful.

### 5. Environment Variables: The Shell's Memory

Environment variables are dynamic values that affect the processes and programs running in the shell. By convention, their names are in uppercase.

**Key Variables to Know:**

#### `PATH`
- **What it is:** A colon-separated list of directories that the shell searches through when you type a command.
- **How it works:** When you type `ls`, the shell looks for an executable file named `ls` in each directory listed in `$PATH`.
- **View it:** `echo $PATH`
- **Modify it:** To add a custom scripts folder (e.g., `~/bin`) to your PATH, you would add this to `.bashrc`:
  `export PATH="$HOME/bin:$PATH"
  This tells the shell to look in `~/bin` first, then in all the other standard locations.

#### `PS1`
- **What it is:** The Primary Prompt String. This variable controls what your command prompt looks like.
- **Customization:** You can use special backslash-escaped characters to insert dynamic information.
- **View it:** `echo $PS1`
- **Common `PS1` codes:**
    - `\u`: Username
    - `\h`: Hostname (the computer's name)
    - `\w`: The current working directory
    - `\t`: The current time (HH:MM:SS)
    - `\$`: Displays a `#` if you are the root user, `$` otherwise.

**Example `PS1` Customization:**

```bash
# A prompt showing user@host:directory
export PS1='[\u@\h \w]\$ '

# A prompt with colors (this can look complex!)
export PS1='[\033[01;32m\]\u@\h[\033[00m]:[\033[01;34m\]\w[\033[00m]\$ '
```

### 6. Lab Exercises (TP/CC)

1.  **Open `~/.bashrc`:** Use a text editor like `nano ~/.bashrc`.
2.  **Add Aliases:** Add the `ll` and `update` aliases shown in the examples above.
3.  **Add a Function:** Add the `mkcd` function.
4.  **Customize your Prompt:** Add the colored `PS1` export line from the example.
5.  **Activate Changes:** Save the file and run `source ~/.bashrc`.
6.  **Test Everything:**
    - Type `ll`. Does it show a detailed file listing?
    - Type `type update`. Does it show that `update` is an alias?
    - Use your new `mkcd` function: `mkcd test_directory`. Did it create the folder and move you inside it?
    - Does your prompt look different and colorful?
# UCC121-1: Shells, Scripting, and Data Management
## Session 1: Mastering the Shell Environment

---

## What is a Shell?

A program that takes your commands and tells the operating system what to do.

**You -> Shell -> OS Kernel -> Hardware**

It is your primary interface for controlling the system. We will be using **Bash** (Bourne Again SHell).

---

## Your Toolbox: `~/.bashrc`

An essential configuration file in your home directory.

- **Purpose:** Stores your personal customizations.
- **Execution:** Runs automatically every time you open a new terminal.
- **Rule:** After editing, you must run `source ~/.bashrc` to apply changes to your current session.

---

## Aliases: Your Command-Line Shortcuts

Create short, memorable names for long, complex commands.

**Syntax:** `alias name='long_command'`

```bash
# Example
alias ll='ls -alF'
```

---

## Useful Alias Examples

```bash
# For detailed, human-readable file listing
alias ll='ls -alFh'

# For system updates (Debian/Ubuntu)
alias update='sudo apt update && sudo apt upgrade'

# To quickly show all active network ports
alias ports='netstat -tulpn'
```

---

## Functions: Super-Powered Aliases

For when an alias is not enough.

- Can contain multiple commands.
- Can accept arguments (`$1`, `$2`, etc.).
- Can include logic.

**Syntax:**
```bash
function_name() {
  commands
}
```

---

## Function Example: `mkcd`

A common workflow: create a directory, then `cd` into it.

```bash
# Add this to your ~/.bashrc
mkcd() {
  mkdir -p "$1" && cd "$1"
}
```
**Usage:** `mkcd my_new_project`

---

## Environment Variables

Dynamic, named values that programs use to configure their behavior.

- Conventionally named in `UPPERCASE`.
- View any variable with `echo $VARIABLE_NAME`.
- Set them with `export VARIABLE_NAME="value"`.

---

## The `PATH` Variable

How does the shell find commands like `ls` or `grep`? It searches the `PATH`.

- `$PATH` is a colon-separated list of directories.
- `echo $PATH`
- To add your own script directory (e.g., `~/bin`):
  `export PATH="$HOME/bin:$PATH"`
  *(Add this to `~/.bashrc`)*

---

## The `PS1` Variable: Your Prompt

This variable controls what your command prompt looks like.

**Special Characters:**
- `\u` : Username
- `\h` : Hostname
- `\w` : Current Directory
- `\$` : `$` for normal users, `#` for root.

**Example:** `export PS1='[\u@\h \w]\$ '`
**Result:** `[user@hostname ~]$`

---

## Lab Time!

1.  Open `~/.bashrc` with a text editor.
2.  Add the `ll` alias.
3.  Add the `mkcd` function.
4.  Add a custom `PS1` variable to make your prompt colorful.
    - `export PS1='[\033[01;32m\]\u@\h[\033[00m]:[\033[01;34m\]\w[\033[00m]\$ '`
5.  Run `source ~/.bashrc`.
6.  Test that your alias, function, and new prompt all work correctly.

---

## Questions?

**Next Session:** Text Processing Tools: `grep`, `sed`, and `awk`
