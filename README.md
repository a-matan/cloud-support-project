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

### Why It Matters

Cloud Support engineers need to navigate Linux systems, inspect system resources, troubleshoot processes, manage services, understand permissions, and remotely administer Linux servers.
