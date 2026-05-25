# 🐧 Linux Commands For DevOps

# 📂 Navigation Commands

## pwd

Shows current directory.

```bash
pwd
```

---

## ls

List files and folders.

```bash
ls
ls -la
```

---

## cd

Change directory.

```bash
cd /home/ubuntu
```

---

# 📂 File Commands

## touch

Create file.

```bash
touch test.txt
```

---

## mkdir

Create folder.

```bash
mkdir project
```

---

## rm

Delete files.

```bash
rm file.txt
rm -rf folder
```

⚠️ WARNING:
rm -rf can delete entire system.

---

## cp

Copy files.

```bash
cp file1 file2
```

---

## mv

Move or rename files.

```bash
mv old.txt new.txt
```

---

# 📂 Search Commands

## find

```bash
find / -name docker
```

---

## grep

```bash
grep "ERROR" app.log
```

---

# 📂 Monitoring Commands

## top

Shows CPU and memory usage.

```bash
top
```

---

## htop

Better monitoring tool.

```bash
htop
```

---

## free -h

Check RAM usage.

```bash
free -h
```

---

## df -h

Check disk space.

```bash
df -h
```

---

# 📂 Real World Scenario

# Problem:
Server disk is full.

# Commands Used

```bash
df -h
du -sh /*
find / -type f -size +500M
```

# Solution

- Remove old logs
- Compress files
- Delete temp files

---

# 📂 Interview Questions

## Q1:
Difference between soft link and hard link?

## Q2:
What does chmod 777 mean?

## Q3:
Difference between grep and awk?

