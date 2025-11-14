Linux Shell Scripting Project -- Yagyansh Singh Ahlawat (Roll
No. 2501010120)

Project Overview and Purpose

This project demonstrates the fundamental skills of using Linux commands
and writing shell scripts to automate tasks. By completing this
assignment, the student learns to navigate the Linux filesystem, manage
files and permissions, monitor system processes, and handle networking
tools. Shell scripting enables automating repetitive tasks (like backups
or monitoring), which saves time and reduces human error. This project
specifically covers 20 essential Linux commands and three practical
scripts (backup, monitoring, downloader) to build real-world system
administration skills.

Linux Installation (Ubuntu via VirtualBox or WSL)

Ubuntu Linux can be installed on a Windows host either by using a
virtual machine (e.g. VirtualBox) or the Windows Subsystem for Linux
(WSL). VirtualBox is a widely used, cross-platform virtualizer that lets
you run Ubuntu in a VM on Windows or macOS. To install via VirtualBox,
download the installer from the official VirtualBox website and follow
the setup instructions. Alternatively, on Windows 10/11 you can enable
virtualization (Virtual Machine Platform) and install Ubuntu through
WSL. For example, open PowerShell as Administrator and run wsl
--install, then reboot to complete the setup. This will install Ubuntu
from the Microsoft Store and give you a Linux terminal on Windows
without needing a full VM.

Linux Commands

Navigation Commands

pwd: Prints the current working directory (i.e., shows your current
location in the filesystem).

Syntax: pwd

Example output:

\$ pwd /home/yagyansh

ls: Lists files and directories in the current directory. It can show
details like permissions, ownership, size, and modification dates.

Syntax: ls \[options\] \[directory\]

Example output:

\$ ls -l total 8 drwxr-xr-x 2 user user 4096 Nov 10 10:00 Documents
drwxr-xr-x 2 user user 4096 Nov 10 10:00 Downloads

cd: Changes the current directory (moves you into a specified folder).
You can use cd `<path>`{=html} to switch to that directory; cd .. goes
up one level, and cd \~ goes to your home directory.

Syntax: cd \[directory\]

Example:

\$ cd Downloads \$ pwd /home/yagyansh/Downloads

mkdir: Creates a new directory with the given name. This lets you
organize files into folders.

Syntax: mkdir \[directory_name\]

Example:

\$ mkdir projects \$ ls projects

File Management Commands

cp: Copies files or directories from one location to another. If the
destination exists, it will be overwritten. Use -r to copy directories
recursively.

Syntax: cp \[source\] \[destination\]

Example:

\$ echo "Hello" \> a.txt \$ cp a.txt b.txt \$ ls a.txt b.txt

mv: Moves (or renames) files and directories. This removes the original
from the source location and places it in the destination.

Syntax: mv \[source\] \[destination\]

Example:

\$ mv b.txt renamed.txt \$ ls a.txt renamed.txt

rm: Removes (deletes) files or directories. This command permanently
deletes the specified files. Use -r to remove directories recursively,
and -f to force removal without prompting.

Syntax: rm \[options\] \[file\]

Example: (no output if successful)

\$ rm renamed.txt \$ ls a.txt

cat: Concatenates and displays file contents. It is commonly used to
view text files in the terminal or to combine files.

Syntax: cat \[file\]

Example:

\$ echo "Linux scripting" \> notes.txt \$ cat notes.txt Linux scripting

Permissions Commands

chmod: Changes file or directory permissions (mode). Each file has read,
write, execute permissions for owner, group, others. chmod modifies
these settings (e.g., chmod 755 file makes it executable by all and
writable by owner).

Syntax: chmod \[options\] \[mode\] \[file\]

Example:

\$ ls -l script.sh -rw-r--r-- 1 user user 0 Nov 10 10:00 script.sh \$
chmod 700 script.sh \$ ls -l script.sh -rwx------ 1 user user 0 Nov 10
10:00 script.sh

chown: Changes file ownership to a new user and/or group. Only root (or
the file's owner) can change ownership.

Syntax: chown \[options\] new_owner\[:new_group\] file(s)

Example: (requiring sudo)

\$ sudo chown root:ausers data.txt \$ ls -l data.txt -rwxr----- 1 root
ausers 0 Nov 10 10:00 data.txt

sudo: Runs a command with elevated (superuser) privileges. It allows
permitted users to perform administrative tasks without logging in as
root.

Syntax: sudo \[command\]

Example:

\$ sudo whoami root

Process Monitoring Commands

ps: Lists currently running processes on the system. By default, ps
shows processes for the current shell. Options like -e or -aux list all
processes with details.

Syntax: ps \[options\]

Example: (truncated sample of ps -ef)

\$ ps -ef UID PID PPID C STIME TTY TIME CMD root 1 0 0 Oct10 ? 00:01:23
/sbin/init user 1024 1000 0 Oct10 pts/0 00:00:00 bash user 1100 1024 0
Oct10 pts/0 00:00:00 ps -ef

top: Displays real-time system performance, showing active processes,
CPU and memory usage, load averages, etc.. It runs interactively; press
q to exit.

Syntax: top \[options\]

Example: (first lines of top batch output)

\$ top -b -n 1 \| head -n 5 top - 12:00:00 up 2:00, 1 user, load
average: 0.01, 0.05, 0.10 Tasks: 85 total, 1 running, 84 sleeping, 0
stopped, 0 zombie %Cpu(s): 2.0 us, 1.0 sy, 0.0 ni, 97.0 id, 0.0 wa, 0.0
hi, 0.0 si, 0.0 st MiB Mem : 2048.0 total, 512.0 free, 768.0 used, 768.0
buff/cache

free: Shows the amount of free and used memory (RAM and swap) on the
system. Useful for quickly checking memory usage.

Syntax: free \[options\]

Example: (human-readable output)

\$ free -h total used free shared buff/cache available Mem: 2.0G 500M
1.0G 50M 512M 1.4G Swap: 1.0G 0B 1.0G

Networking Commands

ping: Checks network connectivity by sending ICMP echo requests to a
host. It reports round-trip time and packet loss, verifying if a server
is reachable.

Syntax: ping \[options\] host_or_IP

Example: (-c 2 sends 2 pings)

\$ ping -c 2 www.google.com PING www.google.com (142.250.64.78): 56 data
bytes 64 bytes from 142.250.64.78: icmp_seq=1 ttl=118 time=15.3 ms 64
bytes from 142.250.64.78: icmp_seq=2 ttl=118 time=15.1 ms

--- www.google.com ping statistics --- 2 packets transmitted, 2 packets
received, 0% packet loss

ip: A versatile tool for network configuration and management
(replacement for older ifconfig). It can show interfaces, addresses, and
routes.

Syntax: ip \[options\] OBJECT {COMMAND}

Example: (show all interfaces and addresses)

\$ ip addr show 1: lo: \<LOOPBACK,UP,LOWER_UP\> mtu 65536 ... inet
127.0.0.1/8 scope host lo 2: eth0: \<BROADCAST,MULTICAST,UP,LOWER_UP\>
mtu 1500 ... inet 192.168.1.10/24 brd 192.168.1.255 scope global eth0

netstat: Displays network status, including active connections,
listening ports, and routing tables. Useful for troubleshooting network
issues.

Syntax: netstat \[options\]

Example: (list listening TCP ports)

\$ netstat -tuln Active Internet connections (only servers) Proto Recv-Q
Send-Q Local Address Foreign Address State tcp 0 0 0.0.0.0:22 0.0.0.0:\*
LISTEN tcp6 0 0 :::80 :::\* LISTEN

ssh: Secure Shell protocol for securely connecting to a remote server.
Opens a secure terminal session on another machine over the network
(default port 22).

Syntax: ssh \[user@\]hostname

Example:

\$ ssh user@server.example.com user@server.example.com's password:

wget: A non-interactive command-line downloader for retrieving files
from the web. It supports HTTP, HTTPS, FTP, and can run in the
background or resume transfers.

Syntax: wget \[options\] URL

Example: (download a file and save as example.html)

\$ wget -O example.html http://example.com/sample.php --2025-11-10
10:00:00-- http://example.com/sample.php Resolving example.com...
93.184.216.34 Connecting to example.com\|93.184.216.34\|:80...
connected. Saving to: 'example.html'
100%\[====================================\>\] 127 --.-K/s in 0s

curl: A command-line utility for transferring data over networks (HTTP,
HTTPS, FTP, etc.). It is often used to download files or test HTTP
endpoints.

Syntax: curl \[options\] URL

Example: (fetch HTTP headers)

\$ curl -I https://example.com HTTP/2 200 content-type: text/html;
charset=UTF-8 date: Wed, 12 Nov 2025 10:00:00 GMT

Shell Scripts Developed

1.  Directory Backup Script (backup_script.sh)

This Bash script automates backing up a given directory by copying it
with a timestamp. It ensures that directory backups are quick and
consistent (important for routine data protection).

#!/bin/bash \# backup_script.sh - Create a backup copy of a directory

# Usage check

if \[ -z "\$1" \]; then echo "Usage: \$0 `<source_directory>`{=html}"
exit 1 fi

src="$1" if [ ! -d "$src" \]; then echo "Error: \$src is not a
directory" exit 1 fi

timestamp=$(date +'%Y%m%d_%H%M%S') dest="${src}*backup*\$timestamp"

cp -r "$src" "$dest" && echo "Backup of '\$src' completed: \$dest"

Instructions: Make the script executable (chmod +x backup_script.sh).
Run it by providing the directory to back up, for example:

\$ ./backup_script.sh projects

This creates a backup folder named
projects_backup\_`<timestamp>`{=html}. (Screenshot: Directory Backup
script output placeholder)

2.  CPU/Memory Monitoring Logger (mem_logger.sh)

This script logs CPU and memory usage at regular intervals, appending to
a log file. It automates system monitoring, useful for tracking resource
usage over time.

#!/bin/bash \# mem_logger.sh - Log CPU and memory usage periodically

LOGFILE="system_usage.log" interval=60 \# seconds between logs

echo "Logging CPU and Memory usage to \$LOGFILE (every
$interval seconds)..." echo "Time, CPU_Usage(%), Mem_Used(MB)/Mem_Total(MB)" > "$LOGFILE"

while true; do timestamp=$(date '+%Y-%m-%d %H:%M:%S')  cpu=$(top -b -n1
\| grep "%Cpu" \| awk '{print \$2+$4}')  mem_used=$(free -m \|
awk'/Mem:/ {print $3}')  mem_total=$(free -m \| awk '/Mem:/ {print
$2}')  echo "$timestamp, \$cpu, $mem_used/$mem_total" \>\>
"$LOGFILE"  sleep "$interval" done

Instructions: Run the logger in the background (or a separate terminal)
by:

\$ chmod +x mem_logger.sh \$ ./mem_logger.sh

It will append entries to system_usage.log every minute. (Screenshot:
CPU/Memory monitoring log output placeholder)

3.  Automated File Downloader (downloader.sh)

This script downloads a file from a given URL using curl. It automates
file retrieval, which is useful for batch downloads or setting up
environments.

#!/bin/bash \# downloader.sh - Download a file from a URL

if \[ "\$#" -ne 2 \]; then echo "Usage: \$0 `<URL>`{=html}
`<output_file>`{=html}" exit 1 fi

url="\$1" output="\$2"

curl -L -o "$output" "$url" && echo "Downloaded \$url -\> \$output"

Instructions: Make it executable and run with URL and output filename,
for example:

\$ chmod +x downloader.sh \$ ./downloader.sh http://example.com/data.csv
data.csv

The script saves the file (data.csv) in the current directory.
(Screenshot: Automated file download output placeholder)

Reflection

Completing this project posed challenges such as remembering command
syntax, debugging script errors, and setting up the Linux environment.
Initially, understanding permission bits (chmod) and ownership (chown)
required careful reading of documentation, while writing the scripts
involved testing and correcting logic. However, through this work the
student gained confidence in using the Linux command line and Bash
scripting. The hands-on experience helped solidify the importance of
automation: as industry sources note, shell scripting is a valuable
skill for automating tasks like backups and monitoring. In real-world
scenarios, these skills translate to efficiencies in system
administration and DevOps. For example, automated backups prevent data
loss, and monitoring scripts help keep servers healthy without manual
intervention. Overall, this assignment deepened understanding of Linux
fundamentals and provided practical tools for managing systems more
effectively.

Sources: The explanations above draw on Linux documentation and
tutorials. Each command description and script rationale is supported by
these sources.

Introduction to Linux Shell and Shell Scripting - GeeksforGeeks

Key Skills You'll Gain from a Linux Scripting Course for Beginners -
CertLibrary Blog

How to run an Ubuntu Desktop virtual machine using VirtualBox 7 \|
Ubuntu

Install Ubuntu on WSL 2 - Ubuntu on WSL documentation

Install WSL \| Microsoft Learn

File System Navigation Commands in Linux - GeeksforGeeks

File Management in Linux - GeeksforGeeks

How to Copy Files and Directories in Linux \| cp Command - GeeksforGeeks

How to Move File in Linux \| mv Command - GeeksforGeeks

rm command in Linux with examples - GeeksforGeeks

Cat Command in Linux with Examples - GeeksforGeeks

chmod Command in Linux with Examples - GeeksforGeeks

chown Command in Linux with Examples - GeeksforGeeks

sudo Command in Linux with Examples - GeeksforGeeks

How to List Running Processes in Linux \| ps Command - GeeksforGeeks

top Command in Linux with Examples - GeeksforGeeks

free Command in Linux with examples - GeeksforGeeks

How to Check Network Connectivity in Linux \| ping Command -
GeeksforGeeks

ip Command in Linux with Examples - GeeksforGeeks

Network configuration and troubleshooting commands in Linux -
GeeksforGeeks

How to use SSH to connect to a remote server in Linux \| ssh Command -
GeeksforGeeks

Wget Command in Linux/Unix - GeeksforGeeks

curl Command in Linux with Examples - GeeksforGeeks
