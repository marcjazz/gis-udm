---
marp: true
theme: default
paginate: true
size: 16:9
style: |
  section {
    background: #0f172a;
    color: #e2e8f0;
    font-family: "Inter", "Segoe UI", sans-serif;
  }
  h1, h2 {
    color: #38bdf8;
  }
  h3 {
    color: #fbbf24;
  }
  code {
    background: #1e293b;
    color: #22d3ee;
  }
  strong {
    color: #f87171;
  }
---

# AI in Administrative Tasks
## Session 1 – Introduction to AI for System Administration

Linux + AI  
Automation + Intelligence  
Human + Verification

---

# Session Objectives

- Understand what an LLM is  
- Discover AI use cases in system administration  
- Learn safe AI usage principles  
- Execute first AI-assisted tasks  

---

# What Is an LLM?

LLM = Large Language Model  

It predicts the next token based on patterns learned from massive datasets.

It does not think.  
It predicts.

---

# How an LLM Works (Conceptual View)

User Prompt  
⬇  
Tokenization  
⬇  
Neural Network Layers  
⬇  
Probability Prediction  
⬇  
Generated Output  

---

# LLM Architecture (Simplified Diagram)

```
[User Prompt]
      |
      v
[Tokenizer]
      |
      v
[Transformer Model]
  - Attention Layers
  - Hidden Layers
      |
      v
[Probability Distribution]
      |
      v
[Generated Tokens]
```

---

# What Is a Transformer?

Core idea: **Attention**

The model decides:
"What words in this sentence matter most to predict the next word?"

Attention allows:
- Context understanding
- Long-range dependencies
- Code generation

---

# Why Sysadmins Should Care

AI can:

- Explain commands
- Generate scripts
- Analyze logs
- Suggest configs
- Draft documentation

It is your accelerator.

Not your brain.

---

# AI Safety Rules

Never:
- Run unknown destructive commands
- Execute as root without review
- Trust without verification

Always:
- Use sandbox
- Read the command
- Check with man pages

---

# Demo – Explaining a Command

```bash
find /var/log -type f -mtime -7
```

Ask AI:

"Explain this command step by step."

Verify using:
- man find
- Testing in /tmp

---

# Demo – Generating a Command

Prompt:

Generate a safe command to list files >100MB in /home sorted by size.

Expected example:

```bash
find /home -type f -size +100M -exec ls -lh {} \; | sort -k5 -h
```

Now we verify.

---

# Prompt Engineering for Sysadmins

Weak prompt:
"Give me a command."

Strong prompt:
"Generate a safe Linux command to list files larger than 100MB in /home, sorted by size, without deleting anything."

Precision changes results.

---

# Practical Lab

Explain:

```bash
grep -r "Failed password" /var/log/auth.log
```

Then ask AI:
- What does -r mean?
- Why auth.log?

---

# AI Limitations

AI may:
- Invent flags
- Suggest unsafe commands
- Produce inefficient solutions

You are the final validator.

---

# Mini Quiz

1. What is an LLM?
2. What is attention?
3. Why must we verify AI output?

---

# Next Session

Command Generation Deep Dive

More complexity.  
More verification.  
More control.