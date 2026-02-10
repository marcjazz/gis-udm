---
marp: true
theme: gaia
class: lead
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
color: #455a64
---

# **Logic & Control Structures**

## Making Scripts Think

### Session 4

---

## **Today's Mission**

<!--
_class: invert
-->

We move from **linear** scripts to **intelligent** tools.
We teach our scripts to make decisions and handle errors.

1. **The `if` Statement:** Conditional execution.
2. **Tests & Operators:** Checking files, strings, and numbers.
3. **The `case` Statement:** Multi-way branching.
4. **Loops:** Automating repetitive tasks.
5. **Exit Codes:** Understanding success and failure.

---

## **1. The `if` Statement**

"Only do this **if** that is true."

```bash
if [ -f "$LOG_FILE" ]; then
    echo "Log file exists. Proceeding..."
fi
```

### **Interactive Challenge 💬**

- What does `[` actually mean in Linux?
- Why do we need the `; then`?
- How do we close the block?

---

## **2. `if / else` & `elif`**

Handling the "otherwise" scenario.

```bash
if [ -d "/etc/config" ]; then
    echo "Directory found."
elif [ -f "/etc/config" ]; then
    echo "It's a file, not a directory!"
else
    echo "Nothing found at /etc/config."
fi
```

### **Quick Poll 📊**

What happens if we forget the `fi`?

---

## **3. Comparison Operators**

| Type | Operator | Meaning |
| :--- | :---: | :--- |
| **File** | `-f` / `-d` | Is it a File? / Is it a Directory? |
| **String** | `==` / `!=` | Equal? / Not Equal? |
| **Numeric** | `-eq` / `-gt` | Equal? / Greater Than? |

> **⚠️ Warning:** Never use `>` or `<` for numbers in `[ ]`. Use `-gt` and `-lt`.

---

## **4. The `case` Statement**

Cleaner than 10 `if` statements. Perfect for menus or flags.

```bash
case "$1" in
  --verbose)
    echo "Verbose mode ON"
    shift
    ;;
  --help)
    echo "Usage: ./script.sh [option]"
    ;;
  *)
    echo "Unknown option: $1"
    ;;
esac
```

What does the `*)` pattern represent?

---

## **5. `for` Loops**

"Do this for **every** item in a list."

```bash
for user in "alice" "bob" "charlie"; do
    echo "Creating home for $user..."
done
```

### **Try it! 🚀**

How would you loop through all files in the current directory?
*(Hint: Use `*`)*

---

## **6. `while` Loops**

"Keep doing this **while** the condition is true."

```bash
while [ ! -f "/tmp/stop" ]; do
    echo "Waiting for stop signal..."
    sleep 2
done
```

What does the `!` operator do in the test?

---

## **7. Exit Status (`$?`)**

Every command leaves a "receipt" (0 = Success, 1+ = Failure).

```bash
grep "error" /var/log/syslog
if [ $? -eq 0 ]; then
    echo "Errors found!"
fi
```

### **Short-circuiting ⚡**

- `mkdir /data && echo "Success"`
- `ls /missing || echo "Failed"`

---

<!--
_class: invert
-->

# **Live Coding**

## Let's build the "File Guard"

---

## **Lab: The "File Guard"**

**Your Task:** Write a script `guard.sh` that:

1. Accepts a **filename** as an argument.
2. **Validates:** If no argument is provided, print usage and exit.
3. **Checks:**
    - If it's a **directory**, list its contents.
    - If it's a **file**, check if it's readable.
    - If it doesn't exist, ask if the user wants to create it.
4. **Case Logic:** If it's a file, use `case` to identify `.sh` files and suggest making them executable.

**Commands you'll need:**
`if`, `case`, `read`, `[ ]`, `$1`, `exit`
