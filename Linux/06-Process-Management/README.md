# Linux Process Management for DevOps Engineers

# Introduction

Every application running on Linux is executed as a process.

Examples:
- Jenkins
- Docker
- Kubernetes
- Nginx
- Apache
- Java Applications
- Python Applications

All production debugging starts with process analysis.

Understanding process management is mandatory for:
- Production troubleshooting
- Performance tuning
- Incident management
- High availability systems
- Kubernetes node debugging
- CI/CD troubleshooting

---

# What is a Process?

A process is an executing instance of a program.

Example:

When you run:

```bash
nginx
```

Linux creates a process.

Each process gets:
- PID
- memory allocation
- CPU allocation
- file descriptors
- execution state

---

# Process Lifecycle

Process States:

| State | Meaning |
|---|---|
| R | Running |
| S | Sleeping |
| D | Uninterruptible sleep |
| T | Stopped |
| Z | Zombie |
| X | Dead |

---

# Understanding PID

PID = Process ID

Check current shell PID:

```bash
echo $$
```

View all processes:

```bash
ps -ef
```

---

# Important Process Commands

# View Processes

```bash
ps
ps -ef
ps aux
```

---

# Real-time Process Monitoring

```bash
top
```

Better alternative:

```bash
htop
```

Install:

Ubuntu:

```bash
sudo apt install htop -y
```

RHEL:

```bash
sudo yum install htop -y
```

---

# Find Specific Process

```bash
ps -ef | grep nginx
```

---

# Find PID

```bash
pidof nginx
```

---

# Kill Process

Graceful termination:

```bash
kill PID
```

Force kill:

```bash
kill -9 PID
```

---

# Kill by Process Name

```bash
pkill nginx
```

---

# Background Processes

Run in background:

```bash
nohup java -jar app.jar &
```

View jobs:

```bash
jobs
```

Bring to foreground:

```bash
fg
```

---

# Process Priority

# Nice Value

Lower value = Higher priority

View:

```bash
top
```

Start process with priority:

```bash
nice -n 10 process
```

Change running process priority:

```bash
renice -n 5 PID
```

---

# Process Tree

View hierarchy:

```bash
pstree
```

---

# Thread Analysis

View threads:

```bash
top -H
```

or

```bash
ps -eLf
```

---

# CPU Usage Monitoring

```bash
top
```

Sort by CPU:

```bash
ps aux --sort=-%cpu
```

---

# Memory Usage Monitoring

Sort by memory:

```bash
ps aux --sort=-%mem
```

Check RAM:

```bash
free -h
```

---

# File Descriptor Monitoring

Check process file descriptors:

```bash
lsof -p PID
```

Count open files:

```bash
lsof | wc -l
```

---

# Process Scheduling

View scheduling:

```bash
chrt -p PID
```

---

# Foreground vs Background Processes

Foreground:
- attached to terminal

Background:
- detached from terminal

Run background:

```bash
command &
```

---

# Daemons

Daemon = background service process.

Examples:
- sshd
- systemd
- nginx
- dockerd

---

# systemd and systemctl

Most modern Linux distributions use systemd.

---

# Service Management Commands

Start service:

```bash
sudo systemctl start nginx
```

Stop service:

```bash
sudo systemctl stop nginx
```

Restart service:

```bash
sudo systemctl restart nginx
```

Enable at boot:

```bash
sudo systemctl enable nginx
```

Disable:

```bash
sudo systemctl disable nginx
```

Check status:

```bash
sudo systemctl status nginx
```

---

# Journal Logs

View logs:

```bash
journalctl
```

Follow logs:

```bash
journalctl -f
```

Logs for service:

```bash
journalctl -u nginx
```

---

# OOM Killer

OOM = Out Of Memory

When RAM becomes full:
Linux kills processes automatically.

Check logs:

```bash
dmesg | grep -i oom
```

---

# Zombie Processes

Zombie = dead process waiting for parent cleanup.

View zombies:

```bash
ps aux | grep Z
```

---

# Orphan Processes

Orphan process = parent terminated.

Adopted by:
- init
- systemd

---

# Signal Handling

| Signal | Meaning |
|---|---|
| SIGTERM | Graceful stop |
| SIGKILL | Force kill |
| SIGHUP | Reload |
| SIGSTOP | Pause |
| SIGCONT | Continue |

---

# Send Signals

```bash
kill -15 PID
kill -9 PID
kill -1 PID
```

---

# CPU Load Average

Check:

```bash
uptime
```

Example:

```bash
load average: 2.10, 1.90, 1.50
```

---

# Understanding Load Average

- 1 minute
- 5 minute
- 15 minute averages

High load indicates:
- CPU bottleneck
- IO bottleneck
- stuck processes

---

# Disk IO Monitoring

Install:

```bash
sudo apt install sysstat -y
```

Check IO:

```bash
iostat
```

---

# Network Process Monitoring

```bash
netstat -tulpn
```

Modern:

```bash
ss -tulpn
```

---

# Process Environment Variables

View:

```bash
cat /proc/PID/environ
```

---

# 50 Most Used Process Management Commands

```bash
ps
ps -ef
ps aux
top
htop
pstree
pidof
pgrep
pkill
kill
killall
nice
renice
jobs
bg
fg
nohup
free -h
vmstat
iostat
iotop
sar
uptime
dmesg
strace
ltrace
lsof
fuser
watch
journalctl
systemctl
service
systemd-analyze
mpstat
pidstat
ss
netstat
tcpdump
perf
time
timeout
cat /proc/cpuinfo
cat /proc/meminfo
ulimit -a
env
export
printenv
taskset
chrt
top -H
ps -eLf
```

---

# Real World Production Scenarios

# Scenario 1 — Java Application at 100% CPU

Symptoms:
- server slow
- API timeout
- Jenkins jobs stuck

Investigation:

```bash
top
ps aux --sort=-%cpu
top -H -p PID
```

Thread dump:

```bash
jstack PID
```

Root Cause:
- infinite loop
- bad thread handling
- memory leak

---

# Scenario 2 — Kubernetes Node Not Ready

Symptoms:
- pods pending
- kubelet unhealthy

Investigation:

```bash
top
free -h
journalctl -u kubelet
```

Root Cause:
- OOM issue
- CPU exhaustion

---

# Scenario 3 — Jenkins Server Crashing

Symptoms:
- builds failing
- Jenkins restart loop

Investigation:

```bash
systemctl status jenkins
journalctl -u jenkins
top
df -h
```

Root Cause:
- insufficient RAM
- disk full
- Java heap issue

---

# Scenario 4 — Too Many Open Files

Symptoms:
- application crashes
- socket failures

Check:

```bash
lsof
ulimit -n
```

Fix:

```bash
sudo vim /etc/security/limits.conf
```

Increase limits.

---

# Scenario 5 — High Load Average

Symptoms:
- server lagging

Commands:

```bash
uptime
vmstat
iostat
top
```

Possible Causes:
- CPU saturation
- disk IO bottleneck
- stuck NFS mount

---

# Production Troubleshooting Workflow

# Step 1 — Check System Load

```bash
uptime
top
```

---

# Step 2 — Check Memory

```bash
free -h
vmstat
```

---

# Step 3 — Check Disk

```bash
df -h
iostat
```

---

# Step 4 — Check Services

```bash
systemctl status service-name
```

---

# Step 5 — Check Logs

```bash
journalctl -xe
```

---

# Step 6 — Check Network

```bash
ss -tulpn
```

---

# Security Best Practices

- avoid running applications as root
- monitor suspicious processes
- audit cron jobs
- restrict sudo access
- monitor failed services
- rotate logs
- monitor CPU spikes
- limit resource usage

---

# Performance Optimization Best Practices

- tune JVM heap
- optimize thread pools
- use cgroups
- monitor load average
- reduce unnecessary daemons
- optimize disk IO
- use swap carefully

---

# 50 Linux Process Management Interview Questions

## Beginner

1. What is a process?
2. Difference between process and program?
3. What is PID?
4. What is PPID?
5. What is daemon process?
6. Difference between foreground and background process?
7. What is top command?
8. Difference between kill and kill -9?
9. What is load average?
10. What is zombie process?

---

## Intermediate

11. What is orphan process?
12. Difference between SIGTERM and SIGKILL?
13. What is nice value?
14. Explain process scheduling.
15. What is systemd?
16. What is journald?
17. Difference between service and systemctl?
18. How Linux handles memory?
19. What is swap memory?
20. What is virtual memory?

---

## Advanced

21. What happens during OOM?
22. Explain Linux scheduler.
23. What are cgroups?
24. What are namespaces?
25. How Docker uses namespaces?
26. Explain CPU affinity.
27. What is context switching?
28. What is process starvation?
29. What is deadlock?
30. Difference between thread and process?

---

## Production Based

31. Server CPU suddenly reached 100%. What will you do?
32. Application consuming huge memory. How to debug?
33. How to identify memory leak?
34. How to debug stuck Jenkins builds?
35. Kubernetes node under pressure. How to troubleshoot?
36. Too many open files issue?
37. How to debug crashed service?
38. How to investigate OOM kills?
39. How to debug slow Linux server?
40. High IO wait troubleshooting steps?

---

## Scenario Based

41. Production server became unresponsive.
42. SSH login taking too long.
43. Java application randomly crashing.
44. Nginx service failed after reboot.
45. Docker daemon consuming high CPU.
46. Kubernetes kubelet repeatedly restarting.
47. Application stuck in D state.
48. Linux node marked NotReady in Kubernetes.
49. CI/CD pipeline suddenly slow.
50. How would you debug a production outage?

---

# Summary

Process management is one of the most important Linux skills for DevOps engineers.

Strong process debugging skills are essential for:
- production support
- Kubernetes troubleshooting
- CI/CD systems
- cloud infrastructure
- SRE operations
- incident response

Senior DevOps engineers spend significant time analyzing:
- processes
- logs
- CPU usage
- memory usage
- services
- kernel behavior
