# 🚨 File System Troubleshooting

# Issue 1 — Disk Full

## Symptoms

- Application crash
- Jenkins failure
- Kubernetes pod failure

---

## Commands

```bash
df -h
du -sh /*
```

---

## Resolution

- Delete old logs
- Remove temp files
- Compress backups

---

# Issue 2 — Inode Full

## Commands

```bash
df -i
```

---

# Issue 3 — Read Only File System

## Symptoms

Cannot write files.

---

## Causes

- Disk corruption
- Filesystem errors

---

## Fix

```bash
fsck /dev/xvda1
```


