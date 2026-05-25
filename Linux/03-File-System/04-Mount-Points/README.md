# 📘 Mount Points in Linux

A mount point connects a storage device to the filesystem.

---

# 📘 Check Mounted Filesystems

```bash
mount
```

or

```bash
df -h
```

---

# 📘 Important Mount Locations

| Mount Point | Purpose |
|---|---|
| / | Root filesystem |
| /boot | Boot partition |
| /mnt | Temporary mounts |
| /media | External devices |

---

# 📘 Mount a Disk

```bash
mount /dev/xvdf /mnt
```

---

# 📘 Unmount

```bash
umount /mnt
```

---

# 📘 Persistent Mount

Edit:

```bash
/etc/fstab
```

---

# 🚨 Real Production Issue

# Problem:
Server failed to boot.

# Root Cause:
Wrong entry in /etc/fstab

---

# 📘 Troubleshooting

Boot in recovery mode.

Fix:

```bash
vi /etc/fstab
```

