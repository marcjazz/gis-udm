---
marp: true
paginate: true
size: 16:9
theme: default
title: AI in Administrative Tasks - Session 2
style: |
  section {
    background: #0b1220;
    color: #e6edf3;
    font-family: "Inter", "Segoe UI", sans-serif;
  }
  h1, h2 {
    color: #60a5fa;
  }
  h3 {
    color: #fbbf24;
  }
  code {
    background: #111827;
    color: #34d399;
  }
  strong {
    color: #f87171;
  }
---

# AI in Administrative Tasks  
## Session 2 – Command Generation & Explanation

Precision.  
Control.  
Verification.

---

# Session Goals

By the end of today:

- Craft high-precision prompts  
- Compare AI command outputs  
- Detect unsafe suggestions  
- Refine outputs iteratively  

---

# Quick Recap

What is an LLM?

- Predicts next token  
- Uses attention  
- Does NOT reason like a human  

Why must we verify commands?

---

# Live Demo – Weak vs Strong Prompt

Weak prompt:

```
Give me a command to clean logs
```

Strong prompt:

```
Generate a safe Linux command to list log files older than 30 days in /var/log, preview them first, and do not delete directories.
```

Precision changes everything.

---

# The Sysadmin Prompt Formula

A strong prompt includes:

1. Objective  
2. Scope  
3. Constraints  
4. Safety rules  
5. Output format  

More clarity = better output.

---

# Example – File Search

Weak:

```
Find big files
```

Better:

```
Generate a Linux command to find files larger than 500MB inside /home excluding .cache directories, sorted by size, without deleting anything.
```

Notice the specificity.

---

# Prompt Type 1 – Explanation

```
Explain this command step by step and describe each flag:
rsync -avz --delete /source /backup
```

Ask:
- What does -a include?
- What does --delete imply?

---

# Prompt Type 2 – Discovery

```
Find a command that lists all active network connections with associated process IDs.
```

Expected tools:
ss or netstat

Verify with:
man ss

---

# Prompt Type 3 – Safer Alternative

```
Suggest a safer alternative to rm -rf for cleaning temporary directories.
```

Goal:
Train AI to think in safeguards.

---

# Prompt Type 4 – Optimization

```
Optimize this find command for performance on large file systems.
```

AI can improve efficiency.

But verify.

---

# Practical Lab 1 – Challenge 1

## Disk Usage Investigation

Goal:
Find top 10 largest directories in /var sorted by size.

Expected tools:
du  
sort  
head  

Verify correctness manually.

---

# Practical Lab 1 – Challenge 2

## SSH Log Analysis

Goal:
Extract failed SSH attempts from auth.log and count occurrences per IP.

Tools:
grep  
awk  
sort  
uniq  

Watch for hallucinated flags.

---

# Practical Lab 1 – Challenge 3

## Permission Audit

Find world-writable files in /tmp.

Expected:

```
find /tmp -type f -perm -002
```

Verify with man find.

---

# Practical Lab 2 – Refinement

Task:

Create a command to backup /etc daily with compression and timestamp.

Round 1:
Basic prompt.

Round 2:
Add constraints:
- Logging
- No overwrite
- Error handling

Compare outputs.

---

# Critical Thinking Exercise

AI Suggests:

```
find /var/log -mtime +30 -delete
```

Questions:

- What is missing?
- What is dangerous?
- How would you fix it?

---

# Common AI Mistakes in CLI Tasks

AI may:

- Invent flags  
- Use outdated syntax  
- Suggest destructive defaults  
- Ignore edge cases  
- Overcomplicate solutions  

Your job:
Detect and correct.

---

# Interactive Discussion

Ask:

- Did AI hallucinate today?
- Did anyone catch an unsafe suggestion?
- Did prompt refinement improve quality?

---

# Mini Evaluation

1. Why does specificity matter in prompts?
2. What makes a command unsafe?
3. How do you validate a command?

Bonus:

Is this safe?

```
rsync -avz --delete /prod /backup
```

Why or why not?

---

# Key Takeaways

AI is powerful.

But:
- You define constraints.
- You validate output.
- You are responsible.

---

# Next Session

Session 3:

From single commands  
to complete automation scripts.

We level up.