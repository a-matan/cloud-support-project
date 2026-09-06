# Cloud Support Project

## Goal

Build practical Linux administration, networking, AWS, and Cloud Support skills through a hands-on project.

This project documents my progression from Linux fundamentals to Linux administration and eventually managing workloads in AWS.

---

## Linux User Fundamentals

Before moving into Linux administration, I practiced the core skills needed to work comfortably as a Linux user.

### Navigation and Files
- `pwd` - identify the current directory
- `ls` - list files and directories
- `cd` - navigate between directories
- `mkdir` - create directories
- `touch` - create files
- `cp` - copy files
- `mv` - move or rename files
- `rm` - remove files
- `rmdir` - remove empty directories

### Reading and Searching Files
- `cat`
- `less`
- `head`
- `tail`
- `grep`

### Permissions
- Understand user, group, and others
- Read, write, and execute permissions
- Modify permissions with `chmod`
- Understand why `Permission denied` occurs
- Use `sudo` when administrative privileges are actually required

### Processes and System Resources
- `ps` - view processes
- `top` - monitor processes and system activity
- Understand Process IDs (PID)
- Basic process termination with `kill`
- `free -h` - inspect memory and swap
- `df -h` - inspect filesystem usage
- `du -sh *` - investigate disk usage

---

## Day 1 - Linux Administration: Services

### What I Learned

- `systemd` manages services on the Linux system.
- `systemctl` is used to inspect and control services.
- `systemctl status <service>` - inspect a service
- `systemctl start <service>` - start a service
- `systemctl stop <service>` - stop a service
- `systemctl restart <service>` - restart a service
- `systemctl is-active <service>` - check whether a service is running
- `systemctl is-enabled <service>` - check automatic startup configuration
- Active means a service is running now.
- Enabled means a service is configured for automatic startup.
- SSH allows remote administration of a Linux server.
- `systemctl --type=service --state=running` shows running services.

### Hands-On Practice

- Installed and configured an Ubuntu Server VM.
- Connected to the server remotely using SSH.
- Inspected the SSH service.
- Stopped and started the SSH service.
- Restarted the SSH service.
- Identified the SSH service's PID.
- Observed SSH connection information in service logs.
- Listed currently running services.
 

## Day 2 Linux Administration: Logs and Troubleshooting

## Day 2 - Linux Logs & Troubleshooting

- Investigated SSH service logs using `journalctl`.
- Viewed recent logs and filtered logs by time.
- Explored Linux log files under `/var/log`.
- Inspected `/var/log/auth.log` for SSH authentication activity.
- Used `grep` to filter SSH-related log entries.
- Reviewed file ownership and permissions to determine whether my user could read a log file.

### Troubleshooting Practice
I practiced troubleshooting service failures by first checking the service status, then reviewing logs to identify the actual cause before taking action.

Examples included:
- Identifying failed SSH password authentication from logs.
- Recognizing a port conflict from an "Address already in use" error.
- Identifying a file permission problem when an application could not write data.

### Key Lesson
A failed service is the result, not necessarily the root cause. Check the logs for evidence before restarting or changing the system.


## Day 3 - Users, Groups, Permissions, sudo, and SSH

### What I practiced
- Used `id` to inspect user and group membership.
- Created a new Linux user with `adduser`.
- Added users to supplementary groups with `usermod -aG`.
- Used `su -` to switch between users.
- Practiced owner, group, and others permissions.
- Used `chown` to change ownership and `chmod` to change permissions.
- Created a shared `support` group for Mohamed and Adam.
- Configured `/shared-lab` so members of the support group can write to it.
- Tested permissions by creating a file as Adam.
- Connected to the server through SSH as different Linux users.

### Troubleshooting lessons
- Check both file permissions and parent directory permissions.
- Directory `x` permission controls whether a user can traverse the directory.
- A user can access a resource through group permissions when they belong to the resource's group.
- If SSH login succeeds but file access fails, investigate Linux permissions.
- If SSH authentication fails before getting a shell, investigate authentication/login access first.

### Key lesson
Linux access is determined by user identity, group membership, ownership, and permissions. Troubleshoot where the failure actually occurs instead of immediately using sudo or changing permissions.

## Day 4 - Packages, Environment Variables, and Cron

### What I practiced
- Used `which` to check whether a command is available.
- Used APT to refresh package information, inspect upgrades, install software, and remove software.
- Troubleshot an `apt update` failure caused by incorrect VM system time.
- Used `date`, `timedatectl`, and `chronyc tracking` to investigate time synchronization.- Created and exported environment variables.
- Tested how exported variables are inherited by child shells.
- Made an environment variable persistent using `~/.bashrc`.
- Used `crontab` to schedule and verify an automatic job.

### Troubleshooting lessons
- `apt update` refreshes package information but does not upgrade installed software.
- Inspect available upgrades before changing a production system.
- A variable must be exported if child processes need to inherit it.
- Cron uses the server's time, so incorrect system time can affect scheduled jobs.
- Test a command manually before scheduling it with cron.
- Read the error message and investigate the root cause before making changes.

### Key lesson
Package management, environment configuration, scheduling, and accurate system time are important parts of reliable Linux administration.

## Day 5 - AWS EC2 and Linux Administration

### What I practiced
- Launched an Ubuntu EC2 instance in AWS.
- Used a t2.micro instance with an 8 GiB gp3 EBS root volume.
- Created an SSH key pair and protected the private key with `chmod 400`.
- Configured the Security Group to allow SSH from my public IP.
- Connected from my Mac to EC2 using SSH public-key authentication.
- Verified identity and server information using `whoami`, `hostname`, and `pwd`.
- Checked disk and memory resources using `df -h` and `free -h`.
- Inspected the SSH service using `systemctl`.
- Investigated SSH logs using `journalctl`.
- Inspected user and group membership using `id`.
- Refreshed APT package information and inspected available upgrades.
- Verified the EC2 server time zone.
- Created and tested a cron job on EC2.
- Cleaned up the cron test after verification.
- Terminated the EC2 instance and verified its EBS volume was deleted.
- Removed the lab Security Group, AWS key pair, and local private key.

### Troubleshooting Lessons
- A running EC2 instance does not guarantee that SSH is reachable.
- Security Groups control whether network traffic such as SSH on port 22 can reach an instance.
- `Permission denied (publickey)` points toward SSH authentication, username, or key problems.
- `df -h` checks filesystem usage, while `free -h` checks memory.
- `top` helps identify processes consuming CPU or memory.
- Investigate production systems before restarting services, killing processes, or applying upgrades.
- Cron follows the server's configured time zone.

### Key Lesson
The Linux administration skills practiced locally transfer directly to cloud servers. AWS provides the infrastructure, while Linux tools are used to inspect, troubleshoot, and administer the operating system.

### Why It Matters

Cloud Support engineers need to navigate Linux systems, inspect system resources, troubleshoot processes, manage services, understand permissions, and remotely administer Linux servers.

### Networking Fundamentals — Ports, Protocols & Security Groups

- Learned that an IP address identifies the network destination, while a port identifies the service/application.
- Learned common ports:
  - SSH: TCP 22
  - DNS: UDP/TCP 53
  - HTTP: TCP 80
  - HTTPS: TCP 443
- Used `ss -tln` and `ss -tuln` to inspect listening TCP and UDP sockets.
- Learned the difference between TCP `LISTEN` and UDP `UNCONN`.
- Learned how service binding affects reachability:
  - `127.0.0.1` = local/loopback only
  - `0.0.0.0` = all local IPv4 interfaces
  - A specific IP = bound to that local interface/address
- Learned that a listening service does not automatically mean remote traffic can reach it.
- Learned how AWS Security Groups control inbound and outbound traffic.
- Learned that Security Group rules consider protocol, port, and source/destination.
- `/32` represents one IPv4 address.
- `0.0.0.0/0` represents all IPv4 addresses.
- AWS Security Groups are stateful, so return traffic for an allowed connection is automatically allowed.
- Practiced troubleshooting by separating:
  1. Network reachability
  2. Security Group rules
  3. Listening ports
  4. Service status and logs

**Why this matters:**  
Cloud Support engineers must determine whether a connection problem is caused by networking, firewall/security rules, or the application itself instead of making changes or restarting services without evidence.
