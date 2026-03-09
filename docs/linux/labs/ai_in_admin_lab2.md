# Guided Lab Series – Advanced Linux Administration with AI Assistance

These labs explore lesser-discussed aspects of Linux administration.

Each exercise builds on the previous one and requires investigation, experimentation, and careful verification of AI-generated commands.

You may use AI as an assistant, but you must validate all commands before executing them.

---

## Lab 1 – Process Introspection and Zombie Processes

Linux systems can accumulate abnormal processes such as zombies or orphaned processes.

Your goal is to investigate process states and understand how they occur.

Start by exploring the process table using `ps`.

Identify processes that are in unusual states such as:

Z (zombie)  
D (uninterruptible sleep)

Use commands that allow you to visualize process trees and parent-child relationships.

Observe how a process becomes a zombie by writing a small script that creates a child process which exits before its parent calls `wait()`.

Use tools such as:

ps  
pstree  
top

Explain what happens internally when a zombie process appears.

Then design a small script that periodically scans for zombie processes and logs them.

---

## Lab 2 – Understanding the Linux /proc Filesystem

The `/proc` filesystem exposes internal kernel state.

Explore `/proc` and investigate how process information is stored.

Choose a running process and inspect its directory under `/proc`.

Identify files such as:

cmdline  
status  
fd  
maps

Explain what each file represents.

Use shell tools to extract useful information from `/proc`.

Try to answer the following questions through experimentation:

Which processes consume the most memory?

How can you determine the open files of a process?

How can you inspect the environment variables of a running process?

Write a small script that reports:

The PID  
The command name  
The memory usage

for the top five memory-consuming processes.

---

## Lab 3 – File Descriptor Investigation

Linux programs communicate with files, sockets, and devices through file descriptors.

Choose a running process and explore its file descriptors through `/proc/<PID>/fd`.

Determine which descriptors correspond to:

standard input  
standard output  
network sockets  
regular files

Use `lsof` and `/proc` to compare the information obtained.

Try to identify a process that has many open files.

Consider what might happen if a program leaks file descriptors.

Write a script that scans running processes and reports those that exceed a large number of open file descriptors.

---

## Lab 4 – Linux Capabilities and Privilege Separation

Traditional Linux permissions rely on root privileges.

Modern Linux systems also support **capabilities**, which divide root privileges into smaller units.

Investigate Linux capabilities using the `capsh` or `getcap` utilities.

Identify binaries that have special capabilities assigned.

Explore how capabilities such as:

CAP_NET_BIND_SERVICE  
CAP_SYS_ADMIN

affect program behavior.

Try to determine how a program could bind to a low network port without running as root.

Use AI assistance to help generate commands that list all binaries with capabilities on the system.

Discuss the security implications of these capabilities.

---

## Lab 5 – Namespace Exploration

Namespaces are a fundamental building block of containers.

Investigate Linux namespaces on your system.

Use tools such as:

lsns  
unshare

Explore the different types of namespaces:

mount  
pid  
network  
user  
ipc

Create a new process in a separate PID namespace and observe how the process tree differs.

Experiment with `unshare` to create an isolated environment.

Observe how processes inside the namespace view the system differently.

Document what changes when the namespace is created.

---

## Lab 6 – Control Groups (cgroups)

Linux control groups allow administrators to limit and monitor resource usage.

Investigate the cgroup hierarchy on your system.

Explore directories under:

/sys/fs/cgroup

Determine how CPU and memory limits can be applied.

Create a simple process that consumes CPU resources.

Place the process into a cgroup with limited CPU usage.

Observe the behavior difference before and after applying the limit.

Explain how container platforms use cgroups to isolate workloads.

---

## Lab 7 – Systemd Unit Analysis

Systemd manages services and system initialization.

Investigate systemd units and dependencies.

Use commands such as:

systemctl list-units  
systemctl list-dependencies

Choose a service such as ssh or cron and analyze its unit file.

Identify directives such as:

ExecStart  
Restart  
After  
Requires

Modify or create a custom systemd service that runs a simple script.

Ensure the service:

starts automatically  
logs its output  
restarts on failure

Test and observe its behavior.

---

## Lab 8 – Kernel Log Investigation

Kernel logs provide insight into low-level system behavior.

Use tools such as:

dmesg  
journalctl

Explore the kernel log history.

Look for entries related to:

device initialization  
memory allocation  
driver loading

Identify the most recent warnings or errors.

Try to trace how hardware devices are detected during boot.

Use filters in `journalctl` to isolate specific services or time ranges.

Document at least one event that occurred during system startup.

---

## Lab 9 – Network Socket Analysis

Network activity can be inspected through system tools.

Investigate active network connections using tools such as:

ss  
netstat

Identify:

listening ports  
active connections  
associated processes

Determine which processes are exposing network services.

Try to trace a connection back to the responsible process.

Write a script that periodically reports:

listening ports  
the associated program  
the PID

Discuss how this information could be used in a security audit.

---

## Lab 10 – Building a System Diagnostic Toolkit

Combine the techniques learned in previous labs.

Create a diagnostic script that performs the following tasks:

inspect system resource usage  
list processes with high memory consumption  
detect zombie processes  
report open network ports  
summarize failed login attempts

The script should produce a clear diagnostic report.

Use AI to help structure the script, but verify every part before running it.

Ensure the script includes:

logging  
error handling  
clear output formatting

Reflect on which parts of the script were easiest to generate with AI and which required manual reasoning.
