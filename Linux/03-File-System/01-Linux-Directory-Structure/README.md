# 📂 Linux Directory Structure

Linux follows a hierarchical directory structure.

Everything starts from:

```bash
/
```

This is called the ROOT directory.

---

# 📘 Important Directories

| Directory | Purpose |
|---|---|
| / | Root |
| /home | User files |
| /etc | Configuration files |
| /var | Logs and variable data |
| /tmp | Temporary files |
| /bin | Basic commands |
| /sbin | System commands |
| /usr | User applications |
| /opt | Optional software |
| /dev | Device files |
| /proc | Process information |
| /sys | Kernel information |
| /boot | Boot files |

---

# 📂 /etc

Contains configuration files.

Examples:

```bash
/etc/passwd
/etc/ssh/sshd_config
/etc/fstab
```

---

# 📂 /var

Contains logs and application data.

Examples:

```bash
/var/log
/var/lib/docker
/var/lib/jenkins
```

---

# 📂 /proc

Virtual filesystem.

Contains running process information.

Examples:

```bash
/proc/cpuinfo
/proc/meminfo
```

---

# 📂 /tmp

Temporary files.

Files may get deleted after reboot.

---

# 📂 /home

Stores user files.

Example:

```bash
/home/ubuntu
```

---

# 🚀 Real World Example

Docker stores data in:

```bash
/var/lib/docker
```

Jenkins stores data in:

```bash
/var/lib/jenkins
```

Kubernetes stores pod data in:

```bash
/var/lib/kubelet
```

---

# 📘 Commands

## List root directories

```bash
ls /
```

---

## Check current directory

```bash
pwd
```

---

# 📘 Interview Questions

## Q1:
What is the difference between /bin and /sbin?

## Q2:
Why is /var important?

## Q3:
What is stored in /proc?

