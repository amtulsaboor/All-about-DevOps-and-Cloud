# Linux Storage and Disk Management for DevOps Engineers

# Introduction

Storage management is one of the most important infrastructure responsibilities in production environments.

Applications depend on storage for:
- logs
- databases
- container images
- backups
- persistent volumes
- CI/CD artifacts

Storage issues can cause:
- application crashes
- Kubernetes failures
- Jenkins outages
- database corruption
- node failures

DevOps engineers must understand:
- Linux filesystems
- partitions
- LVM
- RAID
- mount points
- swap
- disk performance
- persistent storage

---

# Understanding Linux Storage

Linux treats storage devices as files.

Examples:

```bash
/dev/sda
/dev/xvda
/dev/nvme0n1
```

---

# Disk Naming Conventions

| Device | Description |
|---|---|
| /dev/sda | SATA/SCSI disk |
| /dev/xvda | AWS Xen virtual disk |
| /dev/nvme0n1 | NVMe SSD |
| /dev/sdb | Second disk |

---

# Important Storage Concepts

| Concept | Meaning |
|---|---|
| Partition | Logical disk section |
| Filesystem | Method to organize data |
| Mount Point | Directory attached to filesystem |
| LVM | Logical Volume Manager |
| RAID | Redundant storage |
| Swap | Virtual memory |
| Inode | Metadata structure |

---

# View Storage Devices

```bash
lsblk
```

Example output:

```bash
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0  20G  0 disk
├─xvda1 202:1    0  20G  0 part /
```

---

# View Disk Usage

```bash
df -h
```

---

# View Inode Usage

```bash
df -i
```

---

# View Filesystem Type

```bash
blkid
```

---

# Check Disk Partitions

```bash
fdisk -l
```

---

# Creating Partitions

Open disk utility:

```bash
sudo fdisk /dev/xvdb
```

Commands inside fdisk:

| Command | Purpose |
|---|---|
| n | new partition |
| p | primary |
| d | delete |
| w | write changes |
| q | quit |

---

# Create Filesystem

ext4:

```bash
sudo mkfs.ext4 /dev/xvdb1
```

xfs:

```bash
sudo mkfs.xfs /dev/xvdb1
```

---

# Mount Filesystem

Create mount point:

```bash
sudo mkdir /data
```

Mount:

```bash
sudo mount /dev/xvdb1 /data
```

---

# Verify Mount

```bash
df -h
```

or

```bash
mount | grep xvdb1
```

---

# Persistent Mounting

Edit:

```bash
sudo vim /etc/fstab
```

Example:

```bash
/dev/xvdb1 /data ext4 defaults 0 0
```

---

# Filesystem Types

| Filesystem | Usage |
|---|---|
| ext4 | Default Linux filesystem |
| xfs | High performance |
| tmpfs | Memory filesystem |
| nfs | Network storage |
| overlay | Docker/Kubernetes |

---

# ext4 vs xfs

| ext4 | xfs |
|---|---|
| Common | High scalability |
| Stable | Better performance |
| Easier recovery | Better for large files |

---

# Swap Memory

Swap acts as overflow RAM.

View swap:

```bash
swapon --show
```

Check memory:

```bash
free -h
```

---

# Create Swap File

```bash
sudo fallocate -l 2G /swapfile
```

Permissions:

```bash
sudo chmod 600 /swapfile
```

Format:

```bash
sudo mkswap /swapfile
```

Enable:

```bash
sudo swapon /swapfile
```

---

# LVM — Logical Volume Manager

LVM allows flexible storage management.

Components:
- Physical Volume (PV)
- Volume Group (VG)
- Logical Volume (LV)

---

# Create Physical Volume

```bash
sudo pvcreate /dev/xvdb
```

---

# Create Volume Group

```bash
sudo vgcreate devops_vg /dev/xvdb
```

---

# Create Logical Volume

```bash
sudo lvcreate -L 5G -n data_lv devops_vg
```

---

# Format Logical Volume

```bash
sudo mkfs.ext4 /dev/devops_vg/data_lv
```

---

# Extend Logical Volume

```bash
sudo lvextend -L +5G /dev/devops_vg/data_lv
```

Resize filesystem:

```bash
sudo resize2fs /dev/devops_vg/data_lv
```

---

# RAID Concepts

RAID improves:
- redundancy
- performance
- availability

---

# RAID Levels

| RAID | Purpose |
|---|---|
| RAID 0 | Performance |
| RAID 1 | Mirroring |
| RAID 5 | Parity |
| RAID 10 | Performance + redundancy |

---

# Check RAID

```bash
cat /proc/mdstat
```

---

# Disk Performance Monitoring

Install tools:

```bash
sudo apt install sysstat iotop -y
```

---

# Check Disk IO

```bash
iostat
```

---

# Real-time Disk Usage

```bash
iotop
```

---

# Find Large Files

```bash
find / -type f -size +500M
```

---

# Find Largest Directories

```bash
du -sh /* | sort -hr
```

---

# Inode Exhaustion

Check:

```bash
df -i
```

Problem:
- millions of tiny files

---

# Filesystem Repair

Unmount:

```bash
sudo umount /dev/xvdb1
```

Repair:

```bash
sudo fsck /dev/xvdb1
```

---

# Read-Only Filesystem Issue

Symptoms:
- cannot write files
- applications crash

Check kernel logs:

```bash
dmesg
```

Possible Causes:
- filesystem corruption
- disk failure

---

# AWS EBS Concepts

Types:
- gp2
- gp3
- io1
- io2
- st1

---

# Attach EBS Volume

Steps:
1. Create EBS volume
2. Attach to EC2
3. Format disk
4. Mount disk
5. Add to /etc/fstab

---

# Kubernetes Persistent Storage

Concepts:
- PV
- PVC
- StorageClass

---

# Check Persistent Volumes

```bash
kubectl get pv
```

Check PVC:

```bash
kubectl get pvc
```

---

# Docker Storage

Docker stores data in:

```bash
/var/lib/docker
```

---

# Kubernetes Storage Paths

```bash
/var/lib/kubelet
```

---

# Log Storage Problems

Huge logs often fill disks.

Check:

```bash
du -sh /var/log/*
```

---

# 50 Most Used Storage Commands

```bash
lsblk
df -h
df -i
du -sh
fdisk -l
parted
mkfs.ext4
mkfs.xfs
mount
umount
blkid
fsck
tune2fs
xfs_info
xfs_repair
swapon
swapoff
free -h
iostat
iotop
lsof
find
fallocate
dd
pvcreate
vgcreate
lvcreate
lvextend
lvdisplay
vgdisplay
pvdisplay
resize2fs
xfs_growfs
mdadm
cat /proc/mdstat
mount -a
journalctl
dmesg
ncdu
rsync
scp
tar
gzip
gunzip
zip
unzip
quota
repquota
edquota
smartctl
hdparm
fio
```

---

# Real World Production Scenarios

# Scenario 1 — Disk Full in Jenkins Server

Symptoms:
- builds failing
- no space left on device

Investigation:

```bash
df -h
du -sh /var/*
```

Root Cause:
- old build artifacts
- Docker images

Fix:

```bash
docker system prune -a
```

---

# Scenario 2 — Kubernetes Node Disk Pressure

Symptoms:
- node NotReady
- pods evicted

Check:

```bash
df -h
journalctl -u kubelet
```

Root Cause:
- container logs
- image cache

Fix:

```bash
docker system prune
```

---

# Scenario 3 — Inode Exhaustion

Symptoms:
- cannot create files

Check:

```bash
df -i
```

Root Cause:
- millions of tiny temp files

---

# Scenario 4 — Filesystem Corruption

Symptoms:
- read-only filesystem

Check:

```bash
dmesg
```

Repair:

```bash
fsck
```

---

# Scenario 5 — EBS Volume Not Mounting

Check:

```bash
lsblk
blkid
mount
```

Possible Causes:
- wrong UUID
- missing filesystem
- bad fstab entry

---

# Production Troubleshooting Workflow

# Step 1 — Check Disk Space

```bash
df -h
```

---

# Step 2 — Check Inodes

```bash
df -i
```

---

# Step 3 — Find Large Files

```bash
find / -type f -size +500M
```

---

# Step 4 — Check Disk IO

```bash
iostat
iotop
```

---

# Step 5 — Check Mounts

```bash
mount
```

---

# Step 6 — Check Logs

```bash
journalctl
dmesg
```

---

# Security Best Practices

- encrypt sensitive volumes
- use backups
- use RAID
- monitor storage usage
- rotate logs
- restrict mount permissions
- avoid world writable mounts

---

# Performance Best Practices

- use xfs for large workloads
- monitor disk latency
- optimize IO patterns
- separate logs and databases
- use SSDs for critical workloads

---

# 50 Linux Storage Interview Questions

## Beginner

1. What is a filesystem?
2. What is partition?
3. What is mount point?
4. Difference between ext4 and xfs?
5. What is swap memory?
6. What is inode?
7. What is RAID?
8. What is LVM?
9. Difference between hard disk and SSD?
10. What is disk IO?

---

## Intermediate

11. Explain filesystem hierarchy.
12. How mounting works in Linux?
13. What is UUID in Linux storage?
14. Explain /etc/fstab.
15. Difference between RAID 0 and RAID 1?
16. What is thin provisioning?
17. Explain LVM architecture.
18. What causes inode exhaustion?
19. What is journaled filesystem?
20. Explain disk latency.

---

## Advanced

21. How xfs internally works?
22. What is filesystem corruption?
23. Explain fsck.
24. What is write amplification?
25. Difference between block storage and object storage?
26. What is SAN storage?
27. What is NAS?
28. Explain overlay filesystem in Docker.
29. How Kubernetes PV works?
30. Explain EBS architecture.

---

## Production Based

31. Server disk became full. How to troubleshoot?
32. Kubernetes node under disk pressure.
33. Docker consuming huge disk space.
34. Filesystem suddenly became read-only.
35. Jenkins builds failing due to storage.
36. How to debug high disk IO?
37. Database latency due to storage bottleneck.
38. EBS volume mount failure.
39. RAID disk failure handling.
40. Backup restoration strategy.

---

## Scenario Based

41. Application cannot write logs.
42. Disk usage suddenly increased.
43. Millions of small files created accidentally.
44. EC2 volume detached unexpectedly.
45. Kubernetes PVC stuck pending.
46. Docker overlay filesystem corrupted.
47. Swap memory usage too high.
48. System boot failure due to fstab.
49. Database storage completely full.
50. Explain your storage troubleshooting approach.

---

# Summary

Storage and disk management are foundational infrastructure skills.

Senior DevOps engineers must know:
- filesystem internals
- storage troubleshooting
- Kubernetes persistent storage
- AWS EBS
- performance tuning
- disaster recovery
- production debugging
