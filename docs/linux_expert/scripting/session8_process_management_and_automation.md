# Session 8: Process Management and Automation with `cron`

This final session covers how to manage long-running tasks and schedule scripts to run automatically at predefined times, which is crucial for system administration and automation.

## Learning Objectives

- Understand Unix process states and how to view them (`ps`, `top`).
- Learn techniques for running commands reliably in the background (`nohup`, `&`).
- Master the use of `crontab` for scheduling recurring tasks.
- Understand the logging implications of automated jobs.

## Topics Covered

### 1. Process Control and Signals

- **Viewing Processes:**
  - `ps aux`: Full process list.
  - `top` / `htop`: Real-time monitoring.
  - `pgrep` / `pkill`: Finding or killing processes by name.
- **Signals (Advanced):**
  - `SIGINT` (2): Interrupt (Ctrl+C).
  - `SIGTERM` (15): Graceful termination.
  - `SIGKILL` (9): Immediate forced termination.
- **The `trap` Command (Advanced):** Handling signals within scripts for cleanup.

  ```bash
  trap "echo 'Cleaning up...'; rm -f temp_file; exit" SIGINT SIGTERM
  ```

- **Foreground/Background:** `fg`, `bg`, and the `&` operator.
- **Reliability:** Using `nohup` or `tmux`/`screen` for persistent sessions.

### 2. Task Scheduling with `cron`

- **`crontab` Access:** `crontab -e` (edit), `crontab -l` (list).
- **Cron Syntax:** `Minute Hour DayOfMonth Month DayOfWeek command`.
- **Advanced Scheduling:**
  - `*/15 * * * *`: Every 15 minutes.
  - `0 9-17 * * 1-5`: Hourly during work hours (Mon-Fri).
- **`anacron` (Less Common):** Useful for servers or laptops that are not running 24/7; ensures jobs run even if the system was off at the scheduled time.

### 3. Script Automation Context

- **Environment in `cron`:** Understanding that cron jobs run with a minimal, non-interactive environment. This often means using absolute paths for commands and scripts inside crontabs.
- **Redirecting Output in Cron:** Explicitly redirecting standard output and error to log files (`>> logfile 2>&1`).

## Lab/Assessment Focus

**Goal:** Automate a robust background task.

1. **Script with Cleanup:** Create `monitor.sh` that writes system stats to a log file. Use `trap` to ensure it logs "Monitoring stopped" when interrupted.
2. **Background Execution:** Run `monitor.sh` using `nohup` and verify it continues after closing the terminal.
3. **Process Control:** Find the PID of `monitor.sh` using `pgrep` and terminate it gracefully using `kill -15`.
4. **Cron Automation:** Schedule a job that runs every Sunday at midnight to archive the logs created during the week. Use absolute paths and redirect both `stdout` and `stderr` to a central log file.

---

## Advanced Topic References

- [The `crontab` Reference](https://crontab.guru/): An interactive guide for building cron schedules.
- [Understanding Linux Process Management](https://www.howtogeek.com/694352/how-to-view-and-kill-processes-on-linux/): Deep dive into `ps` and signal handling.
- [Running Commands Reliably with `nohup` and `disown`](https://www.redhat.com/sysadmin/nohup-command-linux): Techniques for detaching processes.
