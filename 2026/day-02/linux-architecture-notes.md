# Day 02 – Linux Architecture Notes

## What is Linux?

Linux is an open-source operating system that manages computer hardware and software resources. It acts as a bridge between applications and hardware.

---

# Core Components of Linux

## 1. Kernel

The **Kernel** is the core of the Linux operating system.

### Responsibilities
- Manages CPU scheduling
- Manages memory
- Controls hardware devices
- Manages processes
- Handles file systems
- Provides security

---

## 2. Shell

The **Shell** is a command-line interpreter that allows users to communicate with the Linux operating system.

### Responsibilities
- Accepts user commands
- Executes programs
- Runs shell scripts
- Passes commands to the kernel

### Examples
- Bash
- Zsh
- Fish

---

## 3. Applications

Applications are software programs that run on Linux.

### Examples
- Docker
- Nginx
- Git
- VS Code
- Firefox

Applications interact with the kernel through the shell and system calls.

---

# Linux Architecture

```text
Applications
      │
      ▼
    Shell
      │
      ▼
    Kernel
      │
      ▼
   Hardware
```

---

# Process Creation and Management

- Every running program is called a **Process**.
- Every process has a unique **PID (Process ID)**.
- A process is created whenever a command or application is executed.
- The Linux kernel schedules and manages all running processes.

---

# Process States

| State | Description |
|--------|-------------|
| **Running (R)** | Process is currently executing on the CPU. |
| **Sleeping (S)** | Waiting for an event or resource. |
| **Stopped (T)** | Process has been paused or stopped. |
| **Zombie (Z)** | Process has finished execution but its parent has not collected its exit status. |

---

# What is systemd?

**systemd** is the default service manager in most Linux distributions.

It is responsible for:

- Starting services during boot
- Stopping services
- Restarting failed services
- Managing background services
- Collecting and managing system logs

---

# Useful systemd Commands

| Command | Purpose |
|---------|---------|
| `systemctl status nginx` | Check whether the Nginx service is running. |
| `systemctl start nginx` | Start the Nginx service. |
| `systemctl stop nginx` | Stop the Nginx service. |
| `systemctl restart nginx` | Restart the Nginx service. |
| `systemctl enable nginx` | Start Nginx automatically after every boot. |
| `systemctl disable nginx` | Prevent Nginx from starting automatically after boot. |
| `journalctl -u nginx` | Display logs for the Nginx service. **`-u` = Unit (service name).** |

---

# 5 Linux Commands I Use Daily

| Command | Purpose |
|---------|---------|
| `ls` | Lists files and directories in the current directory. |
| `cd` | Changes the current working directory. |
| `ps -ef` | Displays all running processes. **`-e` = Show every process. `-f` = Show full-format details (UID, PID, PPID, CPU time, command).** |
| `top` | Displays real-time CPU usage, memory usage, and running processes. |
| `systemctl status <service>` | Checks whether a service is running and displays its status. |

---

# Why This Matters for DevOps

Understanding Linux architecture helps a DevOps engineer to:

- Troubleshoot crashed services
- Monitor CPU and memory usage
- Manage system services
- Analyze logs efficiently
- Resolve production issues quickly

---

# Key Takeaways

- The **Kernel** is the core of Linux and manages system resources.
- The **Shell** provides an interface between the user and the kernel.
- Applications use the kernel to perform tasks.
- Every application runs as a process with a unique PID.
- **systemd** manages Linux services, while **systemctl** is used to control them.
- **journalctl** is used to view service logs during troubleshooting.