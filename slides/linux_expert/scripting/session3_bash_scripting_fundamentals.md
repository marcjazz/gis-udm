---
marp: true
theme: gaia
class: lead
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
color: #455a64
---

# **Bash Scripting Fundamentals**

## Building Your First Tools

### Session 3

---

## **Today's Mission**

<!--
_class: invert
-->

We move from simple commands to **reusable logic**.
We build a script that logs and executes commands.

1. **Recap & Challenge:** The power of `$_`.
2. **The Anatomy:** Shebangs and Permissions.
3. **Arguments:** Making scripts dynamic with `$@`.
4. **Variables & Quotes:** Storing data safely.
5. **Command Substitution:** Capturing the system state.
6. **Exit Codes:** Understanding success and failure.

---

## **1. Recap: The "Last Argument"**

"Remember `_`? What was it for? What about `$_`?"

### **Quick Challenge**

1. Type `ls /etc/passwd`
2. Now type `cat $_`

What did `$_` do? Answer in chat!

---

## **2. Exercise: `log_and_run.sh`**

Let's build a script that logs a command and then runs it.

### **Step 1: The Foundation**

Create a file named `log_and_run.sh`:

```bash
#!/bin/bash
```

- What is this first line called?
- Why is it essential?

---

## **3. Handling Arguments**

How do we tell our script _which_ command to run?

### **The Special Parameter: `$@`**

Add this to your script:

```bash
echo "Running: $@" >> command.log
```

- What does `$@` represent?
- What does `>>` do to `command.log`?

---

## **4. The "Permission Denied" Wall**

### **Try to run it:**

```bash
./log_and_run.sh ls -l
```

- What error did you get?
- **Challenge:** How do we fix it? (Answer in chat)

---

## **5. Execution & Verification**

### **The Fix:**

```bash
chmod +x log_and_run.sh
./log_and_run.sh ls -l
```

- Check the log: `cat command.log`
- Did it record the command?

---

## **6. Adding Variables**

Hardcoding filenames is bad practice. Let's use a variable.

### **Update your script:**

```bash
LOG_FILE="command.log"
echo "Running: $@" >> "$LOG_FILE"
```

- Why do we use `UPPER_CASE` for variables?
- What happens if you put spaces around the `=`? (Try it!)

---

## **7. The "Quotes" Trap ⚠️**

### **Try this command:**

```bash
./log_and_run.sh echo "Hello World"
```

Now check `command.log`. Are the quotes there?

- How do we ensure the script preserves the quotes?
- **Hint:** Look at how we used `"$LOG_FILE"`.

---

## **8. Command Substitution**

Let's add a timestamp to our log.

### **Modern Syntax: `$( ... )`**

Update the `echo` line:

```bash
echo "$(date): Running: $@" >> "$LOG_FILE"
```

- What does `$(date)` do?
- Why is it better than the old backticks `` `date` ``?

---

## **9. Exit Codes: Success or Failure?**

Every command leaves a "receipt" called an exit code.

### **The Challenge:**

1. Run: `./log_and_run.sh ls /nonexistent`
2. Immediately run: `echo $?`

- What number did you get?
- What does `0` mean? What does non-zero mean?

---

<!--
_class: invert
-->

# **Live Coding Lab**

## The "User Info" Script

---

## **Lab: `user_info.sh`**

**Your Task:** Create a script that provides a system snapshot.

1. **Default User:** Use `${1:-$USER}` to pick a target user.
2. **Capture Data:** Use `$(id -u $target)` to get their UID.
3. **Math:** Calculate remaining slots if the limit is 100: `$((100 - $(who | wc -l)))`.
4. **PID:** Print the script's own Process ID using `$$`.
5. **Permissions:** Make it executable and run it!
