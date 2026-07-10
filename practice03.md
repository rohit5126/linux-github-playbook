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


