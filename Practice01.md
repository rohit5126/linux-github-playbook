
# 🐧 Linux + DevOps Cheat Sheet

---

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

## 🔹 DevOps Scenario-Based Questions (Corrected)

### 11. Nginx is reported down after SSH

**Answer:**

```bash
systemctl status nginx
```

---

### 12. Nginx process not running

**Answer:**

```bash
ps aux | grep nginx
sudo systemctl restart nginx
```

---

### 13. Nginx fails to start – port 80 already in use

**Answer:**

```bash
sudo ss -tulnp | grep :80
sudo kill <PID>   # or stop conflicting service
sudo systemctl start nginx
```

---

### 14. kill vs kill -9

**Answer:**

* `kill` → sends SIGTERM (graceful shutdown)
* `kill -9` → sends SIGKILL (force kill, no cleanup)

---

### 15. Website not accessible from browser

**Answer:**

```bash
systemctl status nginx
ss -tulnp | grep :80
curl -I localhost
journalctl -u nginx -n 50
```

* Also check security group / firewall rules (port 80 open, correct CIDR)

---

### 16. Connection timeout (site not reachable)

**Answer:**

```bash
systemctl status nginx
ss -tulnp | grep :80
sudo systemctl enable nginx
```

* Check firewall / security group / network ACLs

---

### 17. Port not listening / backend connectivity issue

**Answer:**

```bash
ss -tulnp | grep <backend_port>
curl http://localhost:<backend_port>
```

* Verify nginx upstream config and backend service status

---

### 18. Permission denied error

**Answer:**

```bash
ls -l <file>
sudo chown -R www-data:www-data <dir>
sudo chmod -R 755 <dir>
```

---

### 19. What does chown www-data do?

**Answer:**

* Changes ownership to `www-data` (default web server user for nginx/apache)
* Required so web server can read/write files

---

### 20. Check system resource usage

**Answer:**

```bash
free -h
df -h
top
```

---

## 🚀 Troubleshooting Flow (Important)

1. Check service

```bash
systemctl status <service>
```

2. Check port

```bash
ss -tulnp
```

3. Check logs

```bash
journalctl -u <service>
```

4. Check network/firewall
5. Check permissions

---

### 17. Backend / port not listening

* Verify backend config and interface (local interface:127.0.0.1 #only accessible from the machine)
  (all network interface:0.0.0.0 #accessible from everywhere)
* Check upstream connectivity

---


### 19. chown www-data

* Assigns ownership to web server user (`www-data`)
  
  `chown -R www-data:www-data /ver/log/nginx`

  check for the user name in `ps -aux | grep nginx`
  

---


## 🚀 Tips

* Use `find` for file search
* Sort before `uniq`
* Avoid unnecessary `cat`
* Always check logs first
* Troubleshoot flow: service → port → logs → network → permissions

---
