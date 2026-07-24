# Day 04 – Linux Practice: Processes and Services

## Objective

Practice Linux process management, systemd services, and log analysis by running real Linux commands and understanding what each command does.

---

# Process Checks

## 1. List Running Processes

### Command

```bash
ps -ef
```

### Meaning

- **ps** → Process Status
- **-e** → Display every running process in the system.
- **-f** → Show full details such as:
  - UID (User ID)
  - PID (Process ID)
  - PPID (Parent Process ID)
  - Start Time
  - Terminal (TTY)
  - Command

### Why is it used?

To see all currently running processes and identify which programs are executing.

---

## 2. Search for a Process

### Command

```bash
ps -ef | grep ssh
```

### Meaning

- **ps -ef** → Displays all running processes.
- **| (Pipe)** → Sends the output of one command to another command.
- **grep ssh** → Filters only the lines containing the word **ssh**.

### Why is it used?

To check whether the SSH service is currently running.

---

## 3. Monitor Running Processes

### Command

```bash
top
```

### Meaning

Displays real-time information about:

- CPU usage
- Memory usage
- Running processes
- System load
- Uptime

Press **q** to quit.

### Why is it used?

To identify processes consuming high CPU or memory.

---

# Service Checks

Linux uses **systemd** to manage services.

---

## 1. Check Service Status

### Command

```bash
systemctl status ssh
```

### Meaning

- **systemctl** → Utility used to control systemd services.
- **status** → Shows the current state of the service.
- **ssh** → Name of the service.

Displays:

- Active or inactive
- Running since
- Main PID
- Recent log messages

### Why is it used?

To verify whether the SSH service is running properly.

---

## 2. List Running Services

### Command

```bash
systemctl list-units --type=service
```

### Meaning

- **list-units** → Displays all loaded systemd units.
- **--type=service** → Shows only services.

### Why is it used?

To see every active service running on the Linux system.

---

# Log Checks

Logs help understand what happened inside a service.

---

## 1. View Service Logs

### Command

```bash
journalctl -u ssh -n 20
```

### Meaning

- **journalctl** → Reads logs from systemd journal.
- **-u ssh** → Show logs only for the SSH service.
- **-n 20** → Display the last 20 log entries.

### Why is it used?

To check recent SSH activity or errors.

---

## 2. View Authentication Logs

### Command

```bash
tail -n 50 /var/log/auth.log
```

### Meaning

- **tail** → Shows the end of a file.
- **-n 50** → Display the last 50 lines.
- **/var/log/auth.log** → Authentication log file.

### Why is it used?

To view recent login attempts and authentication events.

---

# Mini Troubleshooting Scenario

## Problem

Unable to connect to the server using SSH.

---

### Step 1 — Check Service Status

```bash
systemctl status ssh
```

**Purpose**

Check whether the SSH service is running.

---

### Step 2 — Check Logs

```bash
journalctl -u ssh -n 20
```

**Purpose**

Look for recent errors or failed login attempts.

---

### Step 3 — Verify Process

```bash
ps -ef | grep ssh
```

**Purpose**

Confirm that the SSH process exists.

---

### Step 4 — Restart Service

```bash
sudo systemctl restart ssh
```

**Meaning**

- **restart** → Stops the service and starts it again.

**Purpose**

Restart the service if it is stuck or not responding.

---

### Step 5 — Verify Again

```bash
systemctl status ssh
```

**Purpose**

Ensure the SSH service is running successfully after the restart.

---

# Commands Learned Today

| Command | Purpose |
|----------|---------|
| `ps -ef` | Display all running processes. |
| `ps -ef \| grep ssh` | Search for the SSH process. |
| `top` | Monitor CPU, memory, and processes in real time. |
| `systemctl status ssh` | Check the status of the SSH service. |
| `systemctl list-units --type=service` | List all active services. |
| `journalctl -u ssh -n 20` | View the last 20 SSH log entries. |
| `tail -n 50 /var/log/auth.log` | View the last 50 authentication log entries. |
| `systemctl restart ssh` | Restart the SSH service. |

---

# Key Learnings

- Learned how Linux manages running processes.
- Understood the difference between processes and services.
- Learned how to inspect services using `systemctl`.
- Learned how to analyze service logs using `journalctl`.
- Practiced a simple troubleshooting workflow for SSH.
- Understood how logs help identify problems before restarting a service.

---

## Summary

Today I practiced Linux process management, service management, and log analysis. These commands are essential for troubleshooting production servers and are widely used in DevOps, System Administration, Docker, Kubernetes, and Cloud environments.