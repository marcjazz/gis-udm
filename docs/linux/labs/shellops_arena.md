# ShellOps Arena

Welcome to ShellOps Arena! This is a gamified environment designed to help you practice your Linux system administration and troubleshooting skills.

## Getting Started

To dive into the arena, you can run the environment using Docker. Use the following command:

```bash
docker run -it ghcr.io/marcjazz/shellops-arena
```

Once the container starts, you will be automatically logged in as the `student` user. This is your playground for the duration of the session.

## How to Play

ShellOps Arena consists of multiple levels, each presenting a unique system challenge or "incident" that you need to resolve.

### Checking Progress

The most important tool in your arsenal is the `check_level` command. Run it at any time to:

- See your current level and objective.
- Check if you have successfully completed the level.
- Get hints if you are stuck.

Simply type:

```bash
check_level
```

## Hints

Don't worry if you get stuck! Here are some general tips to help you navigate the arena:

- **Explore the System:** Use standard Linux tools to see what's happening. Some useful commands include `ls`, `cat`, `ps`, `top`, `lsof`, `netstat`, and `journalctl`.
- **Understand the Objective:** Each level has a specific goal. Use `check_level` to make sure you know exactly what you're trying to achieve.
- **Think Like a SysAdmin:** Look for unusual processes, missing files, or misconfigured services.
- **Persistence Pays Off:** Some challenges might require a bit of investigation, but the solution is always within reach!

Good luck, and have fun mastering the shell!
