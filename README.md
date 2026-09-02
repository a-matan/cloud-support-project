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

### What I learned
## Day 2 - Linux Logs & Troubleshooting

## Day 2 - Linux Logs & Troubleshooting

### What I Practiced
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
### Why It Matters

Cloud Support engineers need to navigate Linux systems, inspect system resources, troubleshoot processes, manage services, understand permissions, and remotely administer Linux servers.

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
