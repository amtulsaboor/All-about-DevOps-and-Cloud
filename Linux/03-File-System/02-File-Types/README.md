# 📘 Linux File Types

Everything in Linux is treated as a file.

---

# 📂 Types of Files

| Symbol | File Type |
|---|---|
| - | Regular file |
| d | Directory |
| l | Soft link |
| c | Character device |
| b | Block device |
| s | Socket |
| p | Named pipe |

---

# 📘 Check File Type

```bash
ls -l
```

Example:

```bash
drwxr-xr-x
```

"d" means directory.

---

# 📘 Regular File

Example:

```bash
file.txt
```

---

# 📘 Directory

Stores files and folders.

Example:

```bash
mkdir project
```

---

# 📘 Soft Link

Shortcut to another file.

```bash
ln -s original.txt link.txt
```

---

# 📘 Hard Link

Creates another inode reference.

```bash
ln file1 file2
```

---

# 📘 Device Files

Stored in:

```bash
/dev
```

Examples:

```bash
/dev/sda
/dev/xvda
```

---

# 🚀 Real World Example

Docker containers use Linux namespaces and filesystem isolation.

Kubernetes volumes depend heavily on Linux filesystem concepts.

