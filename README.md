# Linux Shell Scripting Project

**Author:** Yagyansh Singh Ahlawat  
**Roll No:** 2501010120

---

## Table of Contents

- [Project Overview and Purpose](#project-overview-and-purpose)
- [Linux Installation](#linux-installation-ubuntu-via-virtualbox-or-wsl)
- [Linux Commands](#linux-commands)
  - [Navigation Commands](#navigation-commands)
  - [File Management Commands](#file-management-commands)
  - [Permissions Commands](#permissions-commands)
  - [Process Monitoring Commands](#process-monitoring-commands)
  - [Networking Commands](#networking-commands)
- [Shell Scripts Developed](#shell-scripts-developed)
- [Reflection](#reflection)
- [References](#references)

---

## Project Overview and Purpose

This project demonstrates the fundamental skills of using Linux commands and writing shell scripts to automate tasks. By completing this assignment, the student learns to navigate the Linux filesystem, manage files and permissions, monitor system processes, and handle networking tools. 

Shell scripting enables automating repetitive tasks (like backups or monitoring), which saves time and reduces human error. This project specifically covers 20 essential Linux commands and three practical scripts (backup, monitoring, downloader) to build real-world system administration skills.

---

## Linux Installation (Ubuntu via VirtualBox or WSL)

Ubuntu Linux can be installed on a Windows host either by using a virtual machine (e.g., VirtualBox) or the Windows Subsystem for Linux (WSL).

### VirtualBox Installation
VirtualBox is a widely used, cross-platform virtualizer that lets you run Ubuntu in a VM on Windows or macOS. To install via VirtualBox:
1. Download the installer from the official VirtualBox website
2. Follow the setup instructions
3. Create a new virtual machine and install Ubuntu

### WSL Installation
On Windows 10/11, you can enable virtualization (Virtual Machine Platform) and install Ubuntu through WSL:

1. Open PowerShell as Administrator
2. Run: `wsl --install`
3. Reboot to complete the setup

This will install Ubuntu from the Microsoft Store and give you a Linux terminal on Windows without needing a full VM.

---

## Linux Commands

### Navigation Commands

#### `pwd` - Print Working Directory
Prints the current working directory (i.e., shows your current location in the filesystem).

**Syntax:** `pwd`

**Example:**
```bash
$ pwd
/home/yagyansh
```

#### `ls` - List Directory Contents
Lists files and directories in the current directory. It can show details like permissions, ownership, size, and modification dates.

**Syntax:** `ls [options] [directory]`

**Example:**
```bash
$ ls -l
total 8
drwxr-xr-x 2 user user 4096 Nov 10 10:00 Documents
drwxr-xr-x 2 user user 4096 Nov 10 10:00 Downloads
```

#### `cd` - Change Directory
Changes the current directory (moves you into a specified folder). You can use `cd <path>` to switch to that directory; `cd ..` goes up one level, and `cd ~` goes to your home directory.

**Syntax:** `cd [directory]`

**Example:**
```bash
$ cd Downloads
$ pwd
/home/yagyansh/Downloads
```

#### `mkdir` - Make Directory
Creates a new directory with the given name. This lets you organize files into folders.

**Syntax:** `mkdir [directory_name]`

**Example:**
```bash
$ mkdir projects
$ ls
projects
```

---

### File Management Commands

#### `cp` - Copy Files/Directories
Copies files or directories from one location to another. If the destination exists, it will be overwritten. Use `-r` to copy directories recursively.

**Syntax:** `cp [source] [destination]`

**Example:**
```bash
$ echo "Hello" > a.txt
$ cp a.txt b.txt
$ ls
a.txt  b.txt
```

#### `mv` - Move/Rename Files
Moves (or renames) files and directories. This removes the original from the source location and places it in the destination.

**Syntax:** `mv [source] [destination]`

**Example:**
```bash
$ mv b.txt renamed.txt
$ ls
a.txt  renamed.txt
```

#### `rm` - Remove Files/Directories
Removes (deletes) files or directories. This command permanently deletes the specified files. Use `-r` to remove directories recursively, and `-f` to force removal without prompting.

**Syntax:** `rm [options] [file]`

**Example:**
```bash
$ rm renamed.txt
$ ls
a.txt
```

#### `cat` - Concatenate and Display Files
Concatenates and displays file contents. It is commonly used to view text files in the terminal or to combine files.

**Syntax:** `cat [file]`

**Example:**
```bash
$ echo "Linux scripting" > notes.txt
$ cat notes.txt
Linux scripting
```

---

### Permissions Commands

#### `chmod` - Change File Mode
Changes file or directory permissions (mode). Each file has read, write, execute permissions for owner, group, others. `chmod` modifies these settings (e.g., `chmod 755 file` makes it executable by all and writable by owner).

**Syntax:** `chmod [options] [mode] [file]`

**Example:**
```bash
$ ls -l script.sh
-rw-r--r-- 1 user user 0 Nov 10 10:00 script.sh
$ chmod 700 script.sh
$ ls -l script.sh
-rwx------ 1 user user 0 Nov 10 10:00 script.sh
```

#### `chown` - Change File Owner
Changes file ownership to a new user and/or group. Only root (or the file's owner) can change ownership.

**Syntax:** `chown [options] new_owner[:new_group] file(s)`

**Example:**
```bash
$ sudo chown root:ausers data.txt
$ ls -l data.txt
-rwxr----- 1 root ausers 0 Nov 10 10:00 data.txt
```

#### `sudo` - Superuser Do
Runs a command with elevated (superuser) privileges. It allows permitted users to perform administrative tasks without logging in as root.

**Syntax:** `sudo [command]`

**Example:**
```bash
$ sudo whoami
root
```

---

### Process Monitoring Commands

#### `ps` - Process Status
Lists currently running processes on the system. By default, `ps` shows processes for the current shell. Options like `-e` or `-aux` list all processes with details.

**Syntax:** `ps [options]`

**Example:**
```bash
$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 Oct10 ?        00:01:23 /sbin/init
user      1024  1000  0 Oct10 pts/0    00:00:00 bash
user      1100  1024  0 Oct10 pts/0    00:00:00 ps -ef
```

#### `top` - Display System Performance
Displays real-time system performance, showing active processes, CPU and memory usage, load averages, etc. It runs interactively; press `q` to exit.

**Syntax:** `top [options]`

**Example:**
```bash
$ top -b -n 1 | head -n 5
top - 12:00:00 up  2:00,  1 user,  load average: 0.01, 0.05, 0.10
Tasks:  85 total,   1 running,  84 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2.0 us,  1.0 sy,  0.0 ni, 97.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   2048.0 total,    512.0 free,    768.0 used,    768.0 buff/cache
```

#### `free` - Display Memory Usage
Shows the amount of free and used memory (RAM and swap) on the system. Useful for quickly checking memory usage.

**Syntax:** `free [options]`

**Example:**
```bash
$ free -h
              total        used        free      shared  buff/cache   available
Mem:           2.0G        500M        1.0G         50M        512M        1.4G
Swap:          1.0G          0B        1.0G
```

---

### Networking Commands

#### `ping` - Test Network Connectivity
Checks network connectivity by sending ICMP echo requests to a host. It reports round-trip time and packet loss, verifying if a server is reachable.

**Syntax:** `ping [options] host_or_IP`

**Example:**
```bash
$ ping -c 2 www.google.com
PING www.google.com (142.250.64.78): 56 data bytes
64 bytes from 142.250.64.78: icmp_seq=1 ttl=118 time=15.3 ms
64 bytes from 142.250.64.78: icmp_seq=2 ttl=118 time=15.1 ms

--- www.google.com ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
```

#### `ip` - Network Configuration
A versatile tool for network configuration and management (replacement for older `ifconfig`). It can show interfaces, addresses, and routes.

**Syntax:** `ip [options] OBJECT {COMMAND}`

**Example:**
```bash
$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 ...
    inet 127.0.0.1/8 scope host lo
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 ...
    inet 192.168.1.10/24 brd 192.168.1.255 scope global eth0
```

#### `netstat` - Network Statistics
Displays network status, including active connections, listening ports, and routing tables. Useful for troubleshooting network issues.

**Syntax:** `netstat [options]`

**Example:**
```bash
$ netstat -tuln
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address    Foreign Address  State
tcp        0      0 0.0.0.0:22       0.0.0.0:*        LISTEN
tcp6       0      0 :::80            :::*             LISTEN
```

#### `ssh` - Secure Shell
Secure Shell protocol for securely connecting to a remote server. Opens a secure terminal session on another machine over the network (default port 22).

**Syntax:** `ssh [user@]hostname`

**Example:**
```bash
$ ssh user@server.example.com
user@server.example.com's password:
```

#### `wget` - Web File Downloader
A non-interactive command-line downloader for retrieving files from the web. It supports HTTP, HTTPS, FTP, and can run in the background or resume transfers.

**Syntax:** `wget [options] URL`

**Example:**
```bash
$ wget -O example.html http://example.com/sample.php
--2025-11-10 10:00:00--  http://example.com/sample.php
Resolving example.com... 93.184.216.34
Connecting to example.com|93.184.216.34|:80... connected.
Saving to: 'example.html'
100%[====================================>] 127         --.-K/s   in 0s
```

#### `curl` - Transfer Data
A command-line utility for transferring data over networks (HTTP, HTTPS, FTP, etc.). It is often used to download files or test HTTP endpoints.

**Syntax:** `curl [options] URL`

**Example:**
```bash
$ curl -I https://example.com
HTTP/2 200 
content-type: text/html; charset=UTF-8
date: Wed, 12 Nov 2025 10:00:00 GMT
```

---

## Shell Scripts Developed

### 1. Directory Backup Script (`backup_script.sh`)

This Bash script automates backing up a given directory by copying it with a timestamp. It ensures that directory backups are quick and consistent (important for routine data protection).

```bash
#!/bin/bash
# backup_script.sh - Create a backup copy of a directory

# Usage check
if [ -z "$1" ]; then
    echo "Usage: $0 <source_directory>"
    exit 1
fi

src="$1"
if [ ! -d "$src" ]; then
    echo "Error: $src is not a directory"
    exit 1
fi

timestamp=$(date +'%Y%m%d_%H%M%S')
dest="${src}_backup_$timestamp"

cp -r "$src" "$dest" && echo "Backup of '$src' completed: $dest"
```

**Instructions:**

1. Make the script executable: `chmod +x backup_script.sh`
2. Run it by providing the directory to back up:
   ```bash
   $ ./backup_script.sh projects
   ```
3. This creates a backup folder named `projects_backup_<timestamp>`

---

### 2. CPU/Memory Monitoring Logger (`mem_logger.sh`)

This script logs CPU and memory usage at regular intervals, appending to a log file. It automates system monitoring, useful for tracking resource usage over time.

```bash
#!/bin/bash
# mem_logger.sh - Log CPU and memory usage periodically

LOGFILE="system_usage.log"
interval=60  # seconds between logs

echo "Logging CPU and Memory usage to $LOGFILE (every $interval seconds)..."
echo "Time, CPU_Usage(%), Mem_Used(MB)/Mem_Total(MB)" > "$LOGFILE"

while true; do
    timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    cpu=$(top -b -n1 | grep "%Cpu" | awk '{print $2+$4}')
    mem_used=$(free -m | awk '/Mem:/ {print $3}')
    mem_total=$(free -m | awk '/Mem:/ {print $2}')
    echo "$timestamp, $cpu, $mem_used/$mem_total" >> "$LOGFILE"
    sleep "$interval"
done
```

**Instructions:**

1. Make the script executable: `chmod +x mem_logger.sh`
2. Run the logger in the background (or a separate terminal):
   ```bash
   $ ./mem_logger.sh
   ```
3. It will append entries to `system_usage.log` every minute

---

### 3. Automated File Downloader (`downloader.sh`)

This script downloads a file from a given URL using `curl`. It automates file retrieval, which is useful for batch downloads or setting up environments.

```bash
#!/bin/bash
# downloader.sh - Download a file from a URL

if [ "$#" -ne 2 ]; then
    echo "Usage: $0 <URL> <output_file>"
    exit 1
fi

url="$1"
output="$2"

curl -L -o "$output" "$url" && echo "Downloaded $url -> $output"
```

**Instructions:**

1. Make it executable: `chmod +x downloader.sh`
2. Run with URL and output filename:
   ```bash
   $ ./downloader.sh http://example.com/data.csv data.csv
   ```
3. The script saves the file (`data.csv`) in the current directory

---

## Reflection

Completing this project posed challenges such as remembering command syntax, debugging script errors, and setting up the Linux environment. Initially, understanding permission bits (`chmod`) and ownership (`chown`) required careful reading of documentation, while writing the scripts involved testing and correcting logic.

However, through this work the student gained confidence in using the Linux command line and Bash scripting. The hands-on experience helped solidify the importance of automation: shell scripting is a valuable skill for automating tasks like backups and monitoring.

In real-world scenarios, these skills translate to efficiencies in system administration and DevOps. For example:
- Automated backups prevent data loss
- Monitoring scripts help keep servers healthy without manual intervention

Overall, this assignment deepened understanding of Linux fundamentals and provided practical tools for managing systems more effectively.

---

## References

1. [Introduction to Linux Shell and Shell Scripting - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/introduction-linux-shell-shell-scripting/)
2. [Key Skills You'll Gain from a Linux Scripting Course for Beginners - CertLibrary Blog](https://www.certlibrary.com/blog/key-skills-youll-gain-from-a-linux-scripting-course-for-beginners/)
3. [How to run an Ubuntu Desktop virtual machine using VirtualBox 7 | Ubuntu](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox)
4. [Install Ubuntu on WSL 2 - Ubuntu on WSL documentation](https://documentation.ubuntu.com/wsl/latest/howto/install-ubuntu-wsl2/)
5. [Install WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/install)
6. [File System Navigation Commands in Linux - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/file-system-navigation-commands-in-linux/)
7. [File Management in Linux - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/file-management-in-linux/)
8. [How to Copy Files and Directories in Linux | cp Command - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/cp-command-linux-examples/)
9. [How to Move File in Linux | mv Command - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/mv-command-linux-examples/)
10. [rm command in Linux with examples - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/rm-command-linux-examples/)
11. [Cat Command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/cat-command-in-linux-with-examples/)
12. [chmod Command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/chmod-command-linux/)
13. [chown Command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/chown-command-in-linux-with-examples/)
14. [sudo Command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/sudo-command-in-linux-with-examples/)
15. [How to List Running Processes in Linux | ps Command - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/ps-command-in-linux-with-examples/)
16. [top Command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/top-command-in-linux-with-examples/)
17. [free Command in Linux with examples - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/free-command-linux-examples/)
18. [How to Check Network Connectivity in Linux | ping Command - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/ping-command-in-linux-with-examples/)
19. [ip Command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/ip-command-in-linux-with-examples/)
20. [Network configuration and troubleshooting commands in Linux - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/network-configuration-trouble-shooting-commands-linux/)
21. [How to use SSH to connect to a remote server in Linux | ssh Command - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/ssh-command-in-linux-with-examples/)
22. [Wget Command in Linux/Unix - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/wget-command-in-linux-unix/)
23. [curl Command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/curl-command-in-linux-with-examples/)

---

**Project Completed By:** Yagyansh Singh Ahlawat (Roll No. 2501010120)
