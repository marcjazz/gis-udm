# **AI in Administrative Tasks – Course Syllabus**

**Duration:** 12 hours (8 sessions × 1.5 hours)
**Prerequisites:** Solid Shell Scripting skills
**Assessment:** Continuous lab exercises, final project, and quiz checkpoints

---

## **Course Objectives**

By the end of this course, students will be able to:

1. Use AI assistants to accelerate command discovery, script generation, and debugging.
2. Apply AI to real administrative tasks: log analysis, security auditing, configuration, and monitoring.
3. Understand and practice prompt engineering tailored to system administration.
4. Critically evaluate AI outputs for correctness, security, and efficiency.

---

## **Session Breakdown**

### **Session 1 – Introduction to AI for System Administration**

**Learning Outcomes:**

* Understand what LLMs are and how they can assist Linux admins.
* Recognize the potential, limitations, and ethical considerations of AI tools.

**Lesson Topics:**

* Overview of AI for CLI and automation.
* Examples of AI use in real sysadmin tasks.
* Safety reminder: Never blindly execute AI-generated commands.

**Lab / Assessment:**

* Install AI tool for CLI (e.g., GitHub Copilot, local LLM).
* Prompt AI: “Explain what `find /etc -name '*.conf'` does.”
* Verify AI’s output manually.

**Example Prompt:**

```text
Explain this Linux command step by step: find /var/log -type f -mtime -7
```

---

### **Session 2 – Command Generation and Explanation**

**Learning Outcomes:**

* Formulate effective AI prompts for command discovery.
* Understand AI-generated command outputs and their safety implications.

**Lesson Topics:**

* Techniques for prompting AI (“explain,” “find command for,” “show me examples”).
* Compare different AI-generated commands for same task.

**Lab / Assessment:**

* Ask AI for commands to:

  * List large files >100MB
  * Copy files with `rsync` excluding specific directories
  * Find and remove old log files safely
* Test and validate AI suggestions in a sandbox directory.

**Example Prompt:**

```text
Generate a safe rsync command to sync /var/www to /backup excluding logs/ and cache/
```

---

### **Session 3 – AI-Assisted Script Generation**

**Learning Outcomes:**

* Transform AI-generated commands into full scripts.
* Implement error handling and input validation with AI assistance.

**Lesson Topics:**

* From single command → functional script.
* AI guidance for loops, conditionals, and logging.

**Lab / Assessment:**

* Generate a script to add new users from a CSV file with:

  * Input validation
  * Home directory creation
  * Logging of successes/failures

**Example Prompt:**

```text
Create a bash script to add users from a CSV with username,email,password, log errors, and skip duplicates
```

---

### **Session 4 – Iterative Code Refinement and Debugging**

**Learning Outcomes:**

* Use AI as a “pair programming partner” to improve and debug scripts.
* Evaluate AI suggestions critically.

**Lesson Topics:**

* Refactoring, commenting, and adding error handling with AI.
* Debugging AI-suggested code safely.

**Lab / Assessment:**

* Provide a buggy backup script. Students ask AI to:

  * Fix errors
  * Add logging
  * Simplify and comment code

**Example Prompt:**

```text
Improve this bash script to handle errors and add detailed logging
```

---

### **Session 5 – AI-Augmented Log Analysis**

**Learning Outcomes:**

* Use AI to analyze large log files efficiently.
* Identify anomalies, correlate events, and summarize results.

**Lesson Topics:**

* Log summarization strategies (auth.log, syslog).
* Detecting brute-force attempts, failed logins, or unusual activity.

**Lab / Assessment:**

* AI-assisted analysis of `/var/log/auth.log` and `/var/log/syslog`
* Generate a CSV or markdown report with anomalies
* Optional: visualize results with simple graphs

**Example Prompt:**

```text
Analyze /var/log/auth.log from the last week and summarize failed login attempts by user
```

---

### **Session 6 – AI for Configuration and Security**

**Learning Outcomes:**

* Generate and audit configuration files using AI.
* Identify potential security issues in system configurations.

**Lesson Topics:**

* Generating secure configs for Nginx, Apache, SSH
* Auditing existing configurations with AI recommendations
* Verifying AI suggestions with validation commands

**Lab / Assessment:**

* Generate a secure Nginx configuration for a static website
* Audit `sshd_config` for weak settings and suggest improvements
* Test configs using `nginx -t` and `sshd -T`

**Example Prompt:**

```text
Suggest improvements for this sshd_config to enhance security without breaking connections
```

---

### **Session 7 – Concepts of Predictive Monitoring**

**Learning Outcomes:**

* Understand AIOps concepts for proactive system monitoring.
* Predict system issues based on historical metrics.

**Lesson Topics:**

* Collecting CPU, RAM, disk metrics
* Predictive alerts and anomaly detection with AI
* Data-driven prompt engineering for monitoring

**Lab / Assessment:**

* AI-assisted creation of metric collection script
* Ask AI to analyze historical CPU/RAM data and predict spikes
* Discuss integrating alerts with email or Slack

**Example Prompt:**

```text
Analyze this CSV of CPU and RAM usage for the past month and suggest possible future spikes
```

---

### **Session 8 – Synthesis Project and Future of AI**

**Learning Outcomes:**

* Combine AI, scripts, and analysis to solve complex administrative tasks.
* Present findings and reflect on the role of AI in sysadmin work.

**Lesson Topics:**

* Reusing prior labs’ outputs
* Ethical considerations and AI limitations
* Emerging AI tools for Linux admins

**Lab / Assessment:**

* Build a small intelligent system diagnostic tool:

  * Combine log analysis, monitoring, and automated scripts
  * Generate a final report
* Present project to class and explain AI contribution

**Example Prompt:**

```text
Create a script that monitors disk, CPU, and memory, logs anomalies, and suggests actions in markdown
```

---

### **General Safety and Ethics Reminders**

* Always review AI-generated commands before execution.
* Avoid running AI suggestions as root without verification.
* Be aware of AI hallucinations: AI may suggest syntactically correct but unsafe commands.
