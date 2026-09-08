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

## Networking Fundamentals

### Skills Learned

- Understand private vs. public IPv4 addresses
- Understand basic CIDR notation including /16, /24, and /32
- Identify network interfaces and IP addresses with `ip addr`
- Inspect routes and the default gateway with `ip route`
- Test IP reachability with `ping`
- Troubleshoot DNS resolution with `resolvectl`
- Understand common ports and TCP vs. UDP
- Inspect listening TCP/UDP ports with `ss`
- Understand service binding:
  - `127.0.0.1` = loopback/local only
  - `0.0.0.0` = all local IPv4 interfaces
- Understand the difference between a listening service and firewall access
- Configure and troubleshoot Ubuntu UFW firewall rules
- Understand AWS Security Group inbound/outbound rules and stateful behavior
- Apply least-privilege access using CIDR ranges and Security Group references
- Use `curl -v` to trace DNS → TCP → TLS → HTTP
- Distinguish connection timeout, connection refused, and HTTP application errors

### Troubleshooting Approach

I use an evidence-based troubleshooting process rather than changing configuration randomly:

1. Reproduce the problem and determine how far the request gets.
2. Verify IP addressing, routing, and DNS when relevant.
3. Verify Security Group and host firewall rules.
4. Check whether the expected port is listening and correctly bound.
5. Check service status and logs.
6. Follow application dependencies when the network path is working.
7. Fix the identified root cause.
8. Verify the solution from the service back to the original client.

### Key Troubleshooting Tools

- `ip addr` — What IP addresses and interfaces does this host have?
- `ip route` — Where will traffic be sent?
- `ping` — Is there evidence of IP reachability?
- `resolvectl` — Can the hostname be resolved?
- `ss -tln` — Is the expected TCP port listening, and where is it bound?
- `systemctl` — Is the service running?
- `journalctl` — Why is the service failing?
- `ufw` — Does the Linux firewall allow the traffic?
- `curl -v` — How far does the application request get?

### Practical Troubleshooting

Practiced layered troubleshooting across:

Client → DNS → TCP → Security Group → UFW → Listening Port → Service → Application → Database

Used evidence from each layer to determine the next troubleshooting step instead of making configuration changes based on assumptions.


## AWS Networking Fundamentals

### VPC and Subnets
- A VPC (Virtual Private Cloud) is a logically isolated network in AWS.
- The VPC CIDR defines the private IP address range available to the VPC.
- Example: `10.20.0.0/16`
- Subnets divide the VPC into smaller networks, such as `10.20.5.0/24`.
- A VPC spans an AWS Region, while each subnet belongs to one Availability Zone.
- Resources can communicate privately across subnets and Availability Zones within the same VPC when routing and security rules allow it.

### Public and Private Subnets
- A public subnet has a route to an Internet Gateway (IGW).
- A private subnet does not have a direct route to an IGW.
- A resource in a public subnet still needs appropriate public addressing, routing, and security rules to communicate directly with the internet.
- Private resources can use a NAT Gateway for outbound IPv4 internet access without becoming directly internet-reachable.

### Route Tables
Route tables determine where network traffic is sent.

Example public subnet:

    10.20.0.0/16 → local
    0.0.0.0/0    → Internet Gateway

Example private subnet with outbound internet access:

    10.20.0.0/16 → local
    0.0.0.0/0    → NAT Gateway

AWS selects the most specific matching route (longest prefix match).

Traffic between resources inside the VPC uses the local route rather than an Internet Gateway or NAT Gateway.

### Internet Gateway vs NAT Gateway
- Internet Gateway (IGW): provides a path between a VPC and the internet for appropriately configured public resources.
- NAT Gateway: allows private resources to initiate outbound IPv4 internet connections and receive response traffic without making those resources directly reachable from the internet.
- A NAT Gateway normally resides in a public subnet that has a route to an Internet Gateway.

### Security Groups
- Security Groups control permitted traffic at the resource/network-interface level.
- Security Groups are stateful.
- They contain allow rules; traffic not allowed is implicitly denied.
- Security Groups do not create network paths. Routing provides the path; Security Groups provide permission.
- Prefer referencing another Security Group when appropriate instead of relying on individual IP addresses.

Example:

    WEB-SG:
    Inbound TCP 443 from 0.0.0.0/0

    DB-SG:
    Inbound TCP 5432 from WEB-SG

### Network ACLs
- Network ACLs (NACLs) provide subnet-level network filtering.
- NACLs are stateless.
- They support both allow and deny rules.
- Traffic must satisfy both applicable NACL and Security Group controls.

### Availability Zones
- AWS Regions contain multiple Availability Zones (AZs).
- A VPC spans the Region.
- Each subnet exists in one Availability Zone.
- Placing multiple servers in the same AZ provides server redundancy but does not protect against an AZ-level failure.
- Distributing resources across multiple AZs improves availability.

### AWS Network Troubleshooting

Use evidence to determine how far a request traveled before deciding what to investigate.

Mental model:

    Destination
        ↓
    Route / Path
        ↓
    Network ACL
        ↓
    Security Group
        ↓
    OS Firewall
        ↓
    Listening Port / Service
        ↓
    Application

Key troubleshooting principle:

**Path + Permission + Service**

- Route table: Is there a path to the destination?
- Security controls: Is the traffic permitted?
- Service: Is the application running and listening on the expected port?

Examples:
- `Could not resolve host` → investigate DNS first.
- TCP connection timeout → investigate network path and security controls.
- HTTP `500 Internal Server Error` → basic network connectivity is working; investigate the application and its dependencies.

### Example: Web Server to Database

    VPC: 10.20.0.0/16

    Web EC2:
    10.20.5.25

    Database EC2:
    10.20.8.15
    PostgreSQL TCP 5432

The web server and database communicate privately using:

    10.20.0.0/16 → local

The database Security Group can allow:

    TCP 5432 from WEB-SG

A NAT Gateway or Internet Gateway is not required for this private VPC communication.

### Key Lesson

Do not troubleshoot cloud networking by randomly checking components.

Use evidence to determine how far the request traveled, then investigate the next layer.

**Routing provides the path. Security controls provide permission. The service must still be available at the destination.**
