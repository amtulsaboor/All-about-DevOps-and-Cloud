# 📘 Inodes in Linux

An inode is a unique identifier for a file.

It stores:

- File permissions
- Owner
- File size
- File location
- Timestamps

---

# 🚀 Important Concept

File name is NOT stored in inode.

The inode stores metadata only.

---

# 📘 Check Inode Number

```bash
ls -i
```

Example:

```bash
123456 file.txt
```

---

# 📘 Check Inode Usage

```bash
df -i
```

---

# 🚨 Real Production Issue

# Problem:
Disk has free space but server cannot create files.

# Root Cause:
Inodes exhausted.

---

# 📘 Troubleshooting

```bash
df -i
```

Find millions of small files:

```bash
find / -xdev -type f | cut -d "/" -f 2 | sort | uniq -c | sort -n
```

---

# 🚀 Real World Example

Kubernetes clusters often face inode exhaustion because of:

- Container logs
- Small temp files
- Cache files

