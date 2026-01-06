---
marp: true
theme: gaia
class: lead
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
color: #455a64
---

# **Scripting 101**
## From Consumer to Creator
### UCC121 - Session 2

---

## **Today's Mission**

<!--
_class: invert
-->

We stop **typing** commands one by one.
We start **building** tools that work for us.

1.  **The Script Anatomy:** What makes a text file a program?
2.  **Permissions:** Why Linux blocks you (and how to fix it).
3.  **Variables:** Storing data like a pro.
4.  **Interaction:** Making scripts talk back.

---

## **1. The Shebang (`#!`)**

It's not just a hashtag. It's an instruction.

```bash
#!/bin/bash
echo "I am a script!"
```

- **`#`**: "Ignore this line" (Comment)
- **`!`**: "...except you, Operating System."
- **`/bin/bash`**: "Use this interpreter."

> **Rule:** Always the very first line. No spaces before it.

---

## **2. Execution & Security**

You created `myscript.sh`. You type `./myscript.sh`.
**Error:** `Permission denied`.

### **Why?**
Linux assumes text files are for *reading*, not *running*. This prevents you from accidentally executing a love letter or a config file.

### **The Fix**
```bash
chmod +x myscript.sh
```
*(Change Mode: Add eXecute)*

---

## **3. Variables: The Memory**

Store data once, use it everywhere.

```bash
# Define (NO SPACES!)
app_name="SuperApp"

# Use (Prefix with $)
echo "Deploying $app_name..."
```

---

## **The "Quotes" Trap ⚠️**

This is where 90% of beginners fail.

| Type | Symbol | Behavior | Example |
| :--- | :---: | :--- | :--- |
| **Weak** | `"` | **Expands** variables | `"Hi $user"` -> `Hi Marco` |
| **Strong** | `'` | **Literal** text | `'Hi $user'` -> `Hi $user` |

> **Pro Tip:** When in doubt, use Double Quotes `""`.

---

## **4. Command Substitution**

Want to save the *result* of a command?
Use **`$( command )`**.

**Bad (Old School):**
`now=`date`` (Don't use backticks!)

**Good (Modern):**
```bash
now=$(date +%H:%M)
files=$(ls | wc -l)

echo "At $now, we have $files files."
```

---

## **5. Interactivity**

Stop hardcoding values. Ask the user.

```bash
echo "Who are you?"
read username

echo "Welcome, $username. Let's work."
```

Or the compact version:
```bash
read -p "Enter version: " version
```

---

<!--
_class: invert
-->

# **Live Coding**
## Let's put it all together.

---

## **Lab: The "Project Starter"**

**Your Task:** Write a script `init_project.sh` that:

1.  Asks for a **Project Name**.
2.  Creates a folder with that name.
3.  Creates a `README.md` inside it.
4.  Writes a timestamped log entry into the README.
5.  Prints "Project [Name] initialized successfully."

**Commands you'll need:**
`read`, `mkdir`, `echo`, `date`, `chmod`

