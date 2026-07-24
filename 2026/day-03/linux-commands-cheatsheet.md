# Day 03 – Linux Commands Cheat Sheet

## Objective

Build confidence with essential Linux commands used in DevOps for file management, process monitoring, networking, and system troubleshooting.

---

# 📁 File System

| Command | Description |
|---------|-------------|
| `pwd` | Display the current working directory. |
| `ls -la` | List all files, including hidden files, with detailed information. |
| `cd <directory>` | Change the current working directory. |
| `mkdir -p project/src` | Create nested directories in one command. |
| `cp -r source destination` | Copy directories recursively. |
| `mv old.txt new.txt` | Move or rename a file or directory. |
| `rm -rf directory` | Remove a directory and all of its contents. |
| `touch file.txt` | Create an empty file or update its timestamp. |
| `cat file.txt` | Display the contents of a file. |
| `find . -name "*.log"` | Search for files by name in the current directory. |

---

# 📄 Text Processing

| Command | Description |
|---------|-------------|
| `grep "ERROR" app.log` | Search for a specific pattern inside a file. |
| `awk '{print $1}' file.txt` | Print the first column of each line. |
| `sed 's/foo/bar/g' file.txt` | Replace all occurrences of one string with another. |
| `sort file.txt` | Sort the contents of a file alphabetically. |
| `wc -l file.txt` | Count the total number of lines in a file. |

---

# ⚙️ Process Management

| Command | Description |
|---------|-------------|
| `ps aux` | Display detailed information about all running processes. |
| `pgrep nginx` | Find the Process ID (PID) of a running process. |
| `top` | Monitor CPU, memory, and running processes in real time. |
| `kill <PID>` | Gracefully terminate a running process. |
| `kill -9 <PID>` | Forcefully terminate a process that is not responding. |

---

# 🌐 Networking

| Command | Description |
|---------|-------------|
| `ping google.com` | Test network connectivity to a remote host. |
| `ip addr` | Display network interfaces and assigned IP addresses. |
| `curl https://example.com` | Send an HTTP request and view the server response. |
| `ss -tulnp` | Display listening TCP/UDP ports and associated processes. |
| `lsof -i :8080` | Identify the process using a specific network port. |

---

# 💾 System Monitoring

| Command | Description |
|---------|-------------|
| `df -h` | Display disk space usage in a human-readable format. |
| `du -sh directory` | Display the total size of a directory. |
| `free -h` | Show system memory usage. |
| `uptime` | Display system uptime and load average. |
| `systemctl status nginx` | Check the status of a systemd service. |

---

# ⭐ Most Frequently Used DevOps Commands

- `ls -la`
- `find`
- `grep`
- `cat`
- `tail -f`
- `ps aux`
- `top`
- `kill`
- `systemctl status`
- `journalctl`
- `ping`
- `curl`
- `ip addr`
- `ss`
- `df -h`
- `free -h`

---

# Key Takeaways

- Linux commands are the foundation of DevOps and system administration.
- Process and service monitoring help identify application issues quickly.
- Networking commands assist in debugging connectivity problems.
- File system commands are used daily for managing files and directories.
- System monitoring commands help track CPU, memory, and disk usage.

---

**Day:** 03  
**Repository:** 90DaysOfDevOps  
**Topic:** Linux Commands Cheat Sheet