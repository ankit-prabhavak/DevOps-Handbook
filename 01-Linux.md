# Linux Commands for DevOps

## Navigation & Directory Structure

Print current working directory path:
```bash
pwd
```

List directory contents:
```bash
ls
```

List all files including hidden files with detailed information:
```bash
ls -la
```

List files sorted by modification time, oldest first, in long format:
```bash
ls -ltr
```

Change directory to a specific folder:
```bash
cd folder
```

Move up one directory level:
```bash
cd ..
```

Change directory to the current user's home directory:
```bash
cd ~
```

## File & Directory Operations

Create a new directory named project:
```bash
mkdir project
```

Create an empty file or update the timestamp of an existing file:
```bash
touch app.log
```

Copy a file from source to destination:
```bash
cp source.txt destination.txt
```

Move or rename a file:
```bash
mv old.txt new.txt
```

Remove a file:
```bash
rm file.txt
```

Forcefully and recursively remove a directory and its contents:
```bash
rm -rf folder
```

## Search & Text Filtering

Find files in the current directory matching a specific pattern:
```bash
find . -name "*.log"
```

Search for exact string matching case-sensitively in a file:
```bash
grep "ERROR" app.log
```

Search for a string case-insensitively in a file:
```bash
grep -i "exception" app.log
```

Search for a string and show 5 lines after (A) and 2 lines before (B) the match:
```bash
grep -A 5 -B 2 "CRITICAL" app.log
```

## Log Inspection

View the last 10 lines of a file:
```bash
tail app.log
```

Follow the log file in real-time as new lines are appended:
```bash
tail -f app.log
```

View the first 10 lines of a file:
```bash
head app.log
```

Open a file for interactive reading, allowing upward and downward navigation:
```bash
less app.log
```

## Service & Systemd Management

Check the current operational status of a service:
```bash
systemctl status nginx
```

Start a stopped service:
```bash
systemctl start nginx
```

Stop a running service:
```bash
systemctl stop nginx
```

Stop and then immediately start a service again:
```bash
systemctl restart nginx
```

Enable a service to start automatically during system boot:
```bash
systemctl enable nginx
```

View the last 50 log lines for a specific systemd service without pagination:
```bash
journalctl -u nginx --no-pager | tail -n 50
```

## Resource Monitoring (CPU, Memory, Disk)

Display disk space usage of all mounted filesystems in human-readable format:
```bash
df -h
```

Display total size of files and folders in the current directory:
```bash
du -sh *
```

Display total, used, and free memory in megabytes:
```bash
free -m
```

Display real-time system resource usage and active processes:
```bash
top
```

Interactive, visual process viewer and system monitor:
```bash
htop
```

## Process Management

List all running processes on the system:
```bash
ps -ef
```

Find specific running processes matching a search term:
```bash
ps -ef | grep java
```

Forcefully terminate a process using its Process ID (PID):
```bash
kill -9 PID
```

Find the process ID listening on a specific network port:
```bash
lsof -i :8080
```

## Permissions & Ownership

Grant execution permissions to a script file:
```bash
chmod +x script.sh
```

Set explicit read, write, and execute permissions using octal notation:
```bash
chmod 755 script.sh
```

Change the user and group ownership of a file:
```bash
chown root:root file.txt
```

## Networking, Connectivity & Utilities

Fetch only the HTTP response headers from a web address:
```bash
curl -I https://google.com
```

Send 4 network packets to an IP to test network connectivity:
```bash
ping -c 4 8.8.8.8
```

List all listening TCP and UDP ports with numerical addresses:
```bash
netstat -tuln
```

Modern alternative to netstat for listing listening TCP and UDP ports:
```bash
ss -tuln
```

Display system network interfaces and assigned IP addresses:
```bash
ip addr show
```

Query DNS to find the IP address corresponding to a domain name:
```bash
nslookup google.com
```

Scan if a specific port is open on a target host without sending data:
```bash
nc -zv 127.0.0.1 22
```

Trace the network path packets take to reach a destination host:
```bash
traceroute google.com
```

Download a file from the web over HTTP/HTTPS/FTP:
```bash
wget https://example.com
```

Extract files from a compressed tarball archive:
```bash
tar -xvf file.tar.gz
```

Connect to a remote server securely using an SSH private key:
```bash
ssh user@remote-ip -i key.pem
```

Securely copy a file from the local machine to a remote server:
```bash
scp file.txt user@remote-ip:/path/
```

Synchronize directories efficiently between local and remote locations:
```bash
rsync -avz local-dir/ user@remote-ip:/remote-dir/
```

Display the Linux distribution and version details:
```bash
cat /etc/os-release
```

Search the shell command history for past docker commands:
```bash
history | grep docker
```

Print detailed system information including kernel version and architecture:
```bash
uname -a
```

Show how long the system has been running along with current load averages:
```bash
uptime
```

Display the username of the current active shell session:
```bash
whoami
```
