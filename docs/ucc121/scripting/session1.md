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
  1. Starting a new shell session.
  2. Running the command `source ~/.bashrc`.

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
This tells the shell to look in`~/bin` first, then in all the other standard locations.

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

### 6. Advanced Customization & Less Common Tips

Beyond basic aliases and variables, you can fine-tune the shell's behavior to suit your workflow.

#### Shell Options (`shopt` and `set`)

- **`shopt -s autocd`**: Allows you to change directory by simply typing the path (no `cd` needed).
- **`shopt -s cdspell`**: Automatically corrects minor spelling errors in `cd` command directory names.
- **`set -o noclobber`**: Prevents you from accidentally overwriting an existing file when using redirection (e.g., `>`).

#### The `CDPATH` Variable

Similar to `PATH`, `CDPATH` defines a search path for the `cd` command.

```bash
export CDPATH=".:~:~/Projects"
```

If you are in `/tmp` and type `cd gis-udm`, and `gis-udm` is in `~/Projects`, the shell will find it and move you there immediately.

#### History Management

You can control how your command history is saved to avoid duplicates or sensitive commands.

```bash
export HISTCONTROL=ignoreboth  # Don't save lines starting with space or duplicate lines
export HISTSIZE=10000          # Number of commands to keep in memory
export HISTFILESIZE=20000      # Number of commands to save to the history file
```

#### Git Integration in Prompt

If you work with Git, showing the current branch in your prompt is incredibly useful.

```bash
# Add this function to your .bashrc
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\[\033[32m\]\u@\h \[\033[33m\]\w\[\033[36m\]\$(parse_git_branch)\[\033[00m\]\$ "
```

### 7. Lab Exercises (TP/CC)

1. **Open `~/.bashrc`:** Use a text editor like `nano ~/.bashrc`.
2. **Add Aliases:** Add the `ll` and `update` aliases shown in the examples above.
3. **Add a Function:** Add the `mkcd` function.
4. **Customize your Prompt:** Add the colored `PS1` export line from the example.
5. **Configure Shell Options:** Enable `autocd` and `cdspell` using `shopt`.
6. **Activate Changes:** Save the file and run `source ~/.bashrc`.
7. **Test Everything:**
   - Type `ll`. Does it show a detailed file listing?
   - Type `type update`. Does it show that `update` is an alias?
   - Use your new `mkcd` function: `mkcd test_directory`. Did it create the folder and move you inside it?
   - Does your prompt look different and colorful?
