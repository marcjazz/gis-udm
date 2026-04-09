---
marp: true
theme: default
paginate: true
header: 'AI in System Administration Exam'
footer: 'Time Allowed: 1h 30min | 1.5 min per question'
---

# AI in System Administration Exam
**Duration:** 1 hour 30 minutes
**Total Questions:** 60
**Format:** Multiple Choice

---

## Session 1: Introduction to AI for System Administration

### Question 1
What does the acronym LLM stand for in the context of AI tools like ChatGPT or Claude?
A) Linux Logic Manager
B) Large Language Model
C) Local Load Monitor
D) Linked List Mapper

---

### Question 2
In system administration, what is a primary risk of "hallucinations" in AI outputs?
A) The AI might become self-aware.
B) The AI might suggest syntactically correct but non-existent or dangerous commands.
C) The AI might slow down the network.
D) The AI might refuse to answer technical questions.

---

### Question 3
What is the most critical safety rule when using AI-generated commands?
A) Always run them as root to ensure they work.
B) Copy and paste them as quickly as possible.
C) Never execute an AI-generated command without manually verifying it first.
D) Only use AI for commands you already know perfectly.

---

### Question 4
How can an AI assistant most effectively help a sysadmin with an unfamiliar command like `ipmitool`?
A) By executing the command automatically on the server.
B) By explaining the command's flags and providing common usage examples.
C) By replacing the need for the `man` command entirely.
D) By rewriting the kernel to support the command.

---

### Question 5
Which of the following is a valid ethical consideration when using cloud-based AI for administration?
A) AI tools are too expensive for small businesses.
B) Sharing sensitive system logs or configuration files with a cloud AI might leak private data.
C) AI cannot understand Linux file permissions.
D) Using AI makes shell scripting too easy for students.

---

### Question 6
Which tool is an example of an AI assistant specifically integrated into code editors or terminals?
A) GitHub Copilot
B) Vim-Plug
C) GNU Screen
D) Tmux

---

### Question 7
Why is AI considered a "force multiplier" for experienced system administrators?
A) It replaces the need for an operating system.
B) It can automate the physical installation of servers.
C) It accelerates repetitive tasks like writing boilerplate scripts or documenting code.
D) It eliminates the need for security patches.

---

## Session 2: Command Generation and Explanation

### Question 8
What is "Prompt Engineering" in the context of using AI for Linux administration?
A) Rewriting the shell's source code.
B) Crafting specific, clear instructions to get the most accurate and useful output from an AI.
C) Optimizing the hardware performance of an AI server.
D) Installing a new command-line prompt like Oh My Zsh.

---

### Question 9
If you ask an AI "How do I find files larger than 100MB?", which command is it most likely to suggest?
A) `ls -lh / | grep 100M`
B) `find / -type f -size +100M`
C) `du -sh / | filter 100`
D) `search --size 100MB /`

---

### Question 10
When an AI provides an explanation for a command like `tar -czvf backup.tar.gz /var/www`, what does the `-z` flag typically represent?
A) Zero-compression
B) Zoom into directory
C) Compress the archive using gzip
D) Zap (delete) the source files

---

### Question 11
You want to synchronize two directories using `rsync` but exclude the `.git` folder. Which prompt is most likely to give you a precise command?
A) "Rsync these folders but no git."
B) "How do I use rsync?"
C) "Show me a safe rsync command to sync /src to /dest while excluding the .git directory."
D) "Sync folders."

---

### Question 12
Why might an AI suggest two different commands for the same task (e.g., using `awk` vs `cut`)?
A) Because the AI is confused.
B) Because Linux often provides multiple tools to achieve the same result with different levels of flexibility.
C) Because one tool is for Debian and the other is for Red Hat.
D) Because the AI is trying to test the user's knowledge.

---

### Question 13
What should you do if an AI suggests a command you don't recognize, such as `ncdu`?
A) Run it immediately to see what happens.
B) Ask the AI to explain what `ncdu` is and verify its existence using `man` or a package manager.
C) Assume the AI made up the command.
D) Report the AI for providing "fake" information.

---

### Question 14
Which AI-generated command would be most appropriate for "finding all files modified in the last 7 days"?
A) `find . -mtime -7`
B) `find . -ctime +7`
) `ls -la --days=7`
D) `check-updates --last-week`

---

## Session 3: AI-Assisted Script Generation

### Question 15
When asking an AI to generate a Bash script, why is it useful to specify the "Shebang"?
A) It makes the script run faster.
B) It ensures the AI generates code compatible with a specific interpreter (e.g., `#!/bin/bash` vs `#!/bin/python`).
C) It is a secret code that unlocks AI "pro" features.
D) It prevents the AI from adding comments.

---

### Question 16
What is a major advantage of using AI to write boilerplate code for a script (e.g., log file rotation logic)?
A) The AI always writes bug-free code.
B) It saves the administrator time spent on repetitive, standard logic.
C) AI-generated code doesn't require permissions to run.
D) AI code is automatically encrypted.

---

### Question 17
You need a script to create 50 users from a list. How can AI best assist with "Input Validation"?
A) By automatically checking if the CSV file exists and is readable before processing.
B) By deleting the CSV file after use to save space.
C) By guessing the passwords for the users.
D) By rewriting the `/etc/passwd` file directly.

---

### Question 18
Which prompt is most effective for generating a robust script?
A) "Write a backup script."
B) "Write a bash script that backups /data to /mnt/backup, uses rsync, logs the output to /var/log/backup.log, and sends an email on failure."
C) "Backup my files now."
D) "Give me code for rsync."

---

### Question 19
If an AI provides a script with a loop like `for file in $(ls *.log)`, what is a common improvement it might suggest if you ask for "better practices"?
A) "Use `find` with `-print0` and `xargs -0` to handle filenames with spaces."
B) "Use a `while` loop with `read` for better performance."
C) "Don't use loops in Bash; use Python instead."
D) "Remove the `ls` and use `cat`."

---

### Question 20
How can AI help in making a script "modular"?
A) By combining all functions into a single 5,000-line file.
B) By suggesting how to break the script into smaller, reusable functions.
C) By requiring the script to be run on multiple modules (servers) simultaneously.
D) By converting the script into a binary executable.

---

### Question 21
When an AI generates a script that uses a command you don't have installed, what is the best course of action?
A) Delete the script.
B) Manually install the missing tool or ask the AI to rewrite the script using standard tools like `grep` or `sed`.
C) Edit the script to remove the command and hope it still works.
D) Complaints to the AI provider.

---

### Question 22
Which of the following is a key feature of an "AI-assisted" workflow for script development?
A) One-shot generation where the first output is always perfect.
B) Iterative refinement: asking the AI to add features, fix bugs, or explain specific lines.
C) Letting the AI run the script on your production server.
D) Using the AI to hide your code from other administrators.

---

## Session 4: Iterative Code Refinement and Debugging

### Question 23
You have a script that is failing with a "syntax error near unexpected token 'fi'". How can AI help?
A) It can automatically fix the error on your server via SSH.
B) You can paste the script into the AI and ask it to "Identify and fix the syntax error."
C) The AI will tell you to delete the script and start over.
D) AI cannot help with syntax errors.

---

### Question 24
What does "Refactoring" a script mean when working with an AI?
A) Changing the script's purpose entirely.
B) Restructuring existing code to improve readability or efficiency without changing its behavior.
C) Converting a Bash script into a Word document.
D) Deleting all comments to make the code shorter.

---

### Question 25
Why should you ask an AI to "add error handling" to a basic script?
A) To make the script harder to read.
B) To ensure the script exits gracefully and provides useful feedback if a command (like `cd` or `mount`) fails.
C) Because Linux requires error handling for all scripts to execute.
D) To increase the script's file size.

---

### Question 26
When an AI suggests a fix for a bug, what is the safest way to test it?
A) Run it directly on the production database.
B) Test it in a sandbox or virtual machine environment first.
C) Trust the AI's "confidence level" and skip testing.
D) Ask another AI if the first AI's fix is correct.

---

### Question 27
How can AI assist in "Documenting" a complex legacy script?
A) By deleting the script and replacing it with a new one.
B) By analyzing the logic and generating human-readable comments for each section.
C) By translating the script into another programming language.
D) By encrypting the script so no one can read it.

---

### Question 28
An AI suggests using `[[ ... ]]` instead of `[ ... ]` in a Bash conditional. What is a likely reason?
A) `[[` is newer and provides more features like regex matching and less word splitting issues.
B) `[` is deprecated and will be removed in the next Linux kernel.
C) `[[` makes the script run 10x faster.
D) The AI is hallucinating; `[[` is not valid Bash.

---

### Question 29
If a script is running slowly, what prompt could you use to improve performance?
A) "Make this script faster."
B) "Analyze this bash script and suggest optimizations to reduce execution time or resource usage."
C) "Why is my computer slow?"
D) "Convert this script to assembly."

---

### Question 30
What is a "Pair Programming" approach with AI?
A) Having two AIs write the same script.
) Working alongside the AI, where you provide the logic/goals and the AI provides suggestions, corrections, and boilerplate.
C) Requiring two human admins to review every AI prompt.
D) Using two computers to run one AI.

---

## Session 5: AI-Augmented Log Analysis

### Question 31
Why is AI particularly useful for analyzing `/var/log/auth.log`?
A) It can read the file faster than `cat`.
B) It can quickly identify patterns, such as multiple failed login attempts from the same IP, which might indicate a brute-force attack.
C) It can automatically ban users without your permission.
D) It can delete the logs to hide security breaches.

---

### Question 32
What is a "Log Summarization" task?
A) Deleting 90% of the log file.
B) Using AI to condense thousands of lines of log data into a brief report of key events and anomalies.
C) Changing the log format to JSON.
D) Rotating the logs daily.

---

### Question 33
If you paste a snippet of a "Kernel Panic" log into an AI, what is its most likely contribution?
A) It will fix the hardware remotely.
B) It will explain the likely cause (e.g., driver conflict, memory error) based on the specific error codes.
C) It will tell you to reinstall Linux immediately.
D) It will ignore the input as logs are too complex for AI.

---

### Question 34
How can AI help correlate events across different log files (e.g., `syslog` and `apache_access.log`)?
A) By merging them into a single file and sorting by name.
B) By identifying events happening at the same timestamp across files that might be related to a single issue.
C) By deleting one file if it doesn't match the other.
D) AI cannot look at two files at once.

---

### Question 35
Which prompt would be best for finding security threats in a log?
A) "Search for 'error' in this file."
B) "Analyze these Apache logs and identify any patterns that look like SQL injection or path traversal attempts."
C) "Is my server safe?"
D) "Show me all the lines in the log."

---

### Question 36
What is a limitation of using a standard web-based AI (like ChatGPT) for log analysis?
A) It doesn't know how to read text.
B) Context window limits: it might not be able to "read" a 2GB log file at once.
C) It only understands logs from Windows.
D) It requires a GUI to see logs.

---

### Question 37
How can a sysadmin use AI to create a "Log Parser"?
A) By asking the AI to write a Python or Bash script that uses Regex to extract specific fields (like IP or status code) from a custom log format.
B) By letting the AI manually edit the log file.
C) By buying an AI-powered monitor.
D) Log parsing is not possible with AI.

---

## Session 6: AI for Configuration and Security

### Question 38
How can AI assist in securing an SSH server?
A) By generating a new `sshd_config` file with hardened settings (e.g., disabling root login, changing default port).
B) By automatically generating and sharing your private keys.
C) By disabling the network if it detects a login.
D) By guessing your users' passwords to see if they are weak.

---

### Question 39
You need to set up a reverse proxy in Nginx. How can AI help?
A) It can log into your server and edit `/etc/nginx/nginx.conf`.
B) It can provide a template configuration block and explain what each directive (like `proxy_pass`) does.
C) It can replace Nginx with an AI-based web server.
D) It can browse your website to see if it's working.

---

### Question 40
What is a "Security Audit" prompt?
A) "Is my password 'password123' safe?"
B) "Review this `iptables` configuration and identify any rules that are too permissive or pose a security risk."
C) "Delete all my firewall rules."
D) "Make my server unhackable."

---

### Question 41
Why should you be careful when using AI-generated configurations for SSL/TLS (e.g., Certbot or OpenSSL)?
A) AI might suggest outdated or weak encryption ciphers that are no longer secure.
B) SSL doesn't work with AI.
C) AI-generated certificates are not legally valid.
D) AI cannot generate long strings of characters.

---

### Question 42
How can AI help with "Compliance" (e.g., ensuring a system follows CIS Benchmarks)?
A) By automatically passing the audit for you.
B) By suggesting specific system changes or scripts that align with documented security best practices.
C) By lying to the auditors.
D) Compliance is not related to system administration.

---

### Question 43
If an AI suggests a configuration change, which command should you run to verify it's syntactically correct for Nginx?
A) `nginx -t`
B) `systemctl restart nginx`
C) `rm -rf /etc/nginx`
D) `ls -l /etc/nginx`

---

### Question 44
Can AI help you write `sudoers` file rules?
A) No, that's too sensitive.
B) Yes, it can help you write specific rules (e.g., "Allow user 'backup' to run '/usr/bin/rsync' without a password") and explain the security implications.
C) Yes, by adding `ALL=(ALL) NOPASSWD: ALL` to every user.
D) Only if the AI is running as root.

---

### Question 45
What is the risk of asking an AI to "Fix my firewall"?
A) It might block your own SSH access if you are not specific about which ports to keep open.
B) The firewall might become too smart and start its own rules.
C) Firewalls don't support AI.
D) There is no risk.

---

## Session 7: Concepts of Predictive Monitoring

### Question 46
What is the core idea of AIOps (Artificial Intelligence for IT Operations)?
A) Replacing all humans with AI.
B) Using AI/Machine Learning to analyze system telemetry (CPU, RAM, Disk) to predict and prevent failures before they happen.
C) Running the entire OS inside an AI model.
D) Using AI to write emails to the support team.

---

### Question 47
How can AI help with "Anomaly Detection" in system metrics?
A) By reporting whenever CPU usage is exactly 50%.
B) By learning the "normal" behavior of a server and alerting when current patterns (like a sudden spike in disk I/O at 3 AM) deviate from the norm.
C) By deleting any process that uses more than 10% RAM.
D) By shutting down the server if it gets too hot.

---

### Question 48
You have a CSV file of CPU usage for the last month. How can an LLM assist?
A) It can't; it only reads English, not numbers.
B) It can analyze the data to find trends (e.g., "CPU usage peaks every Monday at 9 AM") and suggest possible causes or resource upgrades.
C) It can increase the CPU speed.
D) It can draw a physical graph on your screen using ASCII art only.

---

### Question 49
What is a "Predictive Alert"?
A) An alert that tells you something happened 5 minutes ago.
B) An alert triggered by the AI based on a prediction that a resource (like disk space) will run out in the near future if current trends continue.
C) An alert that says "I don't know what will happen."
D) A cron job that runs every hour.

---

### Question 50
How can AI help in reducing "Alert Fatigue"?
A) By turning off all alerts.
B) By filtering out "noise" and grouping related alerts into a single actionable incident report.
C) By sending alerts to a separate email that no one checks.
D) By making the alert sounds louder.

---

### Question 51
What kind of script might an AI help you write for monitoring?
A) A bash script that gathers `top` output and saves it to a file.
B) A script that queries a monitoring API (like Prometheus or Zabbix) and uses an AI to summarize the health of the cluster.
C) Both A and B.
D) Neither; AI cannot write monitoring scripts.

---

### Question 52
Why is "Historical Data" important for predictive monitoring?
A) It isn't; only the current second matters.
B) It provides the context needed for an AI to understand what "normal" looks like for a specific system.
C) It allows the AI to delete old files automatically.
D) It makes the AI smarter by letting it read history books.

---

## Session 8: Synthesis Project and Future of AI

### Question 53
In a synthesis project, what does "Combining AI Tools" mean?
A) Using ChatGPT, Claude, and local LLMs together to cross-verify complex script logic or configurations.
B) Using two different keyboards.
C) Running the same command on two different servers.
D) Buying more than one AI subscription.

---

### Question 54
What is a "Local LLM" (e.g., using Ollama or Llama.cpp)?
A) An AI that only knows about your local neighborhood.
B) An AI model that runs entirely on your own hardware, ensuring no data leaves your network.
C) A very small AI that only understands a few words.
D) An AI that you can only use if you are in the same room as the server.

---

### Question 55
As AI evolves, what skill becomes *more* important for a system administrator?
A) Typing speed.
B) Memorizing every flag of every command.
C) Critical thinking and the ability to validate/verify AI-generated solutions.
D) Carrying physical repair tools.

---

### Question 56
What is "Shadow AI" in an organization?
A) Using AI to monitor the shadows in a data center.
B) Employees using AI tools for work without official approval or security oversight.
C) Using an AI that has no name.
D) Running AI only at night.

---

### Question 57
How can AI help in "Knowledge Management" for a sysadmin team?
A) By deleting the documentation.
B) By acting as an interactive interface to search and summarize the team's internal Wiki or documentation.
C) By forcing everyone to learn the same thing.
D) AI cannot help with knowledge.

---

### Question 58
Which of the following is a potential future trend for AI in Linux?
A) AI integrated directly into the shell (e.g., a "smart" terminal that suggests the next command).
B) Linux kernels that optimize themselves using AI.
C) Automated security patching driven by AI analysis.
D) All of the above.

---

### Question 59
What is the best way to "Stay Current" with AI in administration?
A) Stop learning Linux and only study AI.
B) Experiment with new tools in safe environments and follow reputable technical blogs/documentation.
C) Wait for the AI to tell you when to update.
D) Ignore AI until it becomes mandatory.

---

### Question 60
True or False: AI will eventually make the role of a system administrator completely obsolete.
A) True: AI will do everything.
B) False: While AI automates many tasks, the need for human oversight, strategic decision-making, and complex physical/logical troubleshooting remains.

---

## Answer Key

**1-10:** 1. B | 2. B | 3. C | 4. B | 5. B | 6. A | 7. C | 8. B | 9. B | 10. C
**11-20:** 11. C | 12. B | 13. B | 14. A | 15. B | 16. B | 17. A | 18. B | 19. A | 20. B
**21-30:** 21. B | 22. B | 23. B | 24. B | 25. B | 26. B | 27. B | 28. A | 29. B | 30. B
**31-40:** 31. B | 32. B | 33. B | 34. B | 35. B | 36. B | 37. A | 38. A | 39. B | 40. B
**41-50:** 41. A | 42. B | 43. A | 44. B | 45. A | 46. B | 47. B | 48. B | 49. B | 50. B
**51-60:** 51. C | 52. B | 53. A | 54. B | 55. C | 56. B | 57. B | 58. D | 59. B | 60. B
