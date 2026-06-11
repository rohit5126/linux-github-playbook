# 🐧 Linux + DevOps Cheat Sheet

## 🔹 Linux Commands

### 1. Find lines with "error" (case-insensitive) + line numbers

```bash
grep -in "error" app.log
```

---

### 2. Extract IP addresses

```bash
grep -oE "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b" app.log
```

---

### 3. Top 5 IPs with maximum requests

```bash
grep -oE "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b" app.log | sort | uniq -c | sort -rn | head -n 5
```

---

### 4. Extract username and shell

```bash
awk -F':' '{print $1, $6}' users.txt
```

---

### 5. Top 5 processes by memory usage

```bash
ps aux --sort=-%mem | head -n 6
```

---

### 6. Find files larger than 100MB

```bash
find /var/log -type f -size +100M
```

---

### 7. Count unique HTTP status codes

```bash
grep -oE '\b[1-5][0-9]{2}\b' app.log | sort -u | wc -l
```

---

### 8. File permission

```
-rwxr-x---
```

* Numeric: 750
* Owner: read, write, execute
* Group: read, execute
* Others: no permission

---

### 9. Count lines NOT containing "success"

```bash
grep -ivc "success" data.txt
```

---

### 10. Top 5 largest directories

```bash
du -sh */ | sort -hr | head -5
```

---

## 🔹 DevOps Scenarios

### 11. Nginx down – first check

```bash
systemctl status nginx
```

---

### 12. Nginx not running

```bash
ps aux | grep nginx
sudo systemctl start nginx
```

---

### 13. Port 80 already in use

```bash
sudo netstat -tulnp | grep :80
```

---

### 14. kill vs kill -9

* `kill` → graceful (SIGTERM)
* `kill -9` → force (SIGKILL)

---

### 15. Website not accessible

* Check security group (port 80, CIDR)

```bash
journalctl -u nginx -n 30
```

---

### 16. Connection timeout

```bash
systemctl status nginx
systemctl is-enabled nginx
```

---

### 17. Backend / port not listening

* Verify backend config and interface
* Check upstream connectivity

---

### 18. Permission denied

```bash
sudo <command>
```

---

### 19. chown www-data

* Assigns ownership to web server user (`www-data`)

---

### 20. System resource check

```bash
free -h
df -h
top
```

---

## 🚀 Tips

* Use `find` for file search
* Sort before `uniq`
* Avoid unnecessary `cat`
* Always check logs first
* Troubleshoot flow: service → port → logs → network → permissions

---
