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
