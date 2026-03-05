---
marp: true
paginate: true
size: 16:9
theme: default
title: AI in Administrative Tasks - Session 3
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

## Session 3 – AI-Assisted Script Generation

From single commands  
to automation systems.

---

# Session Goals

By the end of today:

- Generate complete Bash scripts using AI
- Specify logic and constraints clearly
- Add validation and error handling
- Refine scripts iteratively

---

# Recap

Session 1 → What AI is  
Session 2 → Command precision  
Session 3 → Automation engineering

Today we move from:

One command  
to  
Structured logic.

---

# What Makes a Good Script?

A proper admin script must:

- Validate inputs
- Handle errors
- Log actions
- Avoid destructive defaults
- Be readable

AI must be guided to include these.

---

# Weak Script Prompt

```
Write a script to create users
```

Result?
Minimal. No validation. No safety.

---

# Strong Script Prompt

```
Create a bash script that:
- Reads users from a CSV file (username,password)
- Validates input format
- Skips existing users
- Logs successes and failures
- Does not overwrite existing home directories
```

Precision creates quality.

---

# Script Anatomy Refresher

Basic structure:

```bash
#!/bin/bash

set -e
set -u

LOGFILE="script.log"

function log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') $1" >> "$LOGFILE"
}
```

AI can generate structure,  
but you must understand it.

---

# Demo – Generate a Script Skeleton

Prompt:

```
Generate a bash script template with:
- error handling
- logging function
- argument validation
```

Discuss:

- Did it use set -e?
- Did it trap errors?
- Is logging consistent?

---

# Important: Error Handling

Ask AI explicitly:

- Handle missing file errors
- Validate arguments
- Exit with proper codes

Example:

```bash
if [[ ! -f "$1" ]]; then
  echo "File not found"
  exit 1
fi
```

If you don’t request it, AI may skip it.

---

# Practical Lab 1

## User Creation Script

Goal:

Generate a script that:

- Reads users from users.csv
- Checks if user exists
- Creates home directory
- Logs activity

Constraints:

- Must not crash on malformed lines
- Must skip duplicates

---

# Lab 1 – CSV Example

Example file:

```
alice,password123
bob,password456
invalidline
```

Students must:

- Ask AI to handle malformed lines
- Test with fake users

---

# Iterative Refinement

Round 1:
Generate script.

Round 2:
Ask AI:

- Add better logging
- Improve error handling
- Add summary at end

Round 3:
Ask AI:

- Refactor for readability

Show how iteration improves quality.

---

# Practical Lab 2

## Backup Automation Script

Goal:

Create a script that:

- Archives /etc
- Compresses with tar.gz
- Adds timestamp
- Prevents overwrite
- Logs output

Example expected filename:

```
etc-backup-2026-03-04.tar.gz
```

---

# Refinement Challenge

Give them a flawed AI script:

Missing:

- Quoting variables
- Error checking
- Exit codes

Ask:
What is wrong?

Fix it using AI.

---

# AI Hallucination Risks in Scripts

AI might:

- Use incorrect syntax
- Forget quoting
- Use unsafe paths
- Assume root access

Teach them to check:

- Quoted variables
- Absolute paths
- Exit codes

---

# Script Security Considerations

Always consider:

- Input injection risks
- Privilege escalation
- File permissions
- Hardcoded credentials

Ask AI explicitly:
“Review this script for security vulnerabilities.”

---

# Advanced Prompt Example

```
Review this bash script for:
- security vulnerabilities
- error handling issues
- performance problems
Explain each issue clearly.
```

This transforms AI into a reviewer.

---

# Mini Evaluation

1. Why must variables be quoted?
2. Why avoid hardcoded passwords?
3. What does set -e do?

Practical:
Ask students to fix a small broken script.

---

# Key Takeaways

AI generates structure.  
You enforce safety.  
Iteration improves quality.  
Verification prevents disasters.

Automation is power.  
Use it responsibly.

---

# Next Session

Session 4:

AI as a debugging and refactoring partner.

We move from creation  
to improvement.
