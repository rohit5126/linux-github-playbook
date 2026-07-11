# 🧠 DevOps Daily Practice – Day 1

Practice set covering **Linux, Docker, Shell Scripting, and Networking**.  
Format: Interview-style Q&A for quick revision.

---

## 🔹 Q1: What does this command do?
```bash
du -ah /var | sort -rh | head -n 5
```
**Answer:**  
Shows the **top 5 largest files/directories** in `/var`, sorted in **descending human-readable size**.

---

## 🔹 Q2: Difference between `>` and `>>`?
**Answer:**  
- `>` → Overwrites file  
- `>>` → Appends to file  

---

## 🔹 Q3: ENTRYPOINT vs CMD in Docker?
**Answer:**  
- `ENTRYPOINT` → Fixed executable (not easily overridden)  
- `CMD` → Default arguments (can be overridden)  
- CLI args pass to ENTRYPOINT  

---

## 🔹 Q4: Container running but not accessible – debugging steps?
**Answer:**  
```bash
docker ps
docker exec -it <container_name> bash
ss -tulnp
```
Also check firewall / security groups.

---

## 🔹 Q5: What does `docker system prune` do?
**Answer:**  
Removes unused:
- containers  
- networks  
- dangling images  
→ Frees disk space  

---

## 🔹 Q6: What does this command do?
```bash
wc -l *.log
```
**Answer:**  
Counts number of lines in all `.log` files.

---

## 🔹 Q7: Output of script?
```bash
a=5
b=10
echo $((a+b))
```
**Answer:**  
15

---

## 🔹 Q8: netstat vs ss?
**Answer:**  
- `netstat` → older, slower  
- `ss` → faster, modern, more detailed  

---

## 🔹 Q9: What does this command do?
```bash
docker run -d -p 8080:80 nginx
```
**Answer:**  
- Runs Nginx container  
- Detached mode (`-d`)  
- Maps port `8080 (host)` → `80 (container)`  
- Access via: http://localhost:8080  

---

## ✅ Question 10 (Final – Scenario Based 🚀)

Your application is running on a server, but users report “502 Bad Gateway” error.

How will you troubleshoot this issue step by step?

👉 Answer like a real production scenario (this is a very important interview question)





❌ Small correction
502 is NOT mainly an access issue
👉 It usually means: Reverse proxy (Nginx) cannot reach backend service
✅ Ideal Step-by-Step Answer

Check if server is reachable

ping <server-ip>

Check web server (Nginx/Apache) status

systemctl status nginx

Check Nginx logs (very important)

tail -f /var/log/nginx/error.log

👉 This often directly shows the root cause

Check backend service

systemctl status <backend-service>

or if container:

docker ps
docker logs <container>

Check if backend is listening

ss -tulnp | grep <backend-port>

Test backend directly

curl http://localhost:<backend-port>

👉 If this fails → backend issue

Check Nginx config (proxy_pass)

Ensure correct upstream:

proxy_pass http://backend:8080;
Not pointing to wrong host/port
Check firewall / security groups
Ensure required ports are open
🔍 Feedback on your answer:

✔ Good:

Mentioned service check
Mentioned port binding (0.0.0.0)
Thought about firewall

❗ Improve:

Always include Nginx logs (most important)
Mention backend health check (curl)
Clarify that 502 = backend not reachable by proxy
