# practice question

<img width="943" height="345" alt="image" src="https://github.com/user-attachments/assets/1970814b-5195-4c37-a533-fe420b4d0a68" />

Key Interview Line

"Terraform only applies changes when it detects drift between configuration and state. If no diff is found, it assumes infrastructure is already in desired state."

💡 Correct Explanation

If Terraform says:

“No changes. Infrastructure is up-to-date.”

even after modifying the instance type, common reasons are:

1️⃣ Change not detected due to wrong attribute
You might have changed a value that doesn't actually differ
Example: same instance type already applied
2️⃣ Change made in wrong file / not loaded
File not in working directory
File not matching *.tf
3️⃣ Using variables but not updated properly
Value overridden in:
terraform.tfvars
CLI -var
Environment variables
4️⃣ Terraform state mismatch (important)
Terraform compares state file vs config
If state already has that value → no change

---

<img width="943" height="345" alt="image" src="https://github.com/user-attachments/assets/941ad5cf-069a-4411-85d6-54dda504d2da" />

.
💡 Complete Answer (Ideal Explanation)

A container exits immediately because:

1️⃣ Main process (PID 1) finishes
Containers run one main process
If it completes → container stops

📌 Example:

CMD ["echo", "Hello"]

→ prints and exits instantly

2️⃣ Incorrect CMD or ENTRYPOINT
Wrong command
Script ends instead of running continuously
3️⃣ Application crash
App fails due to:
Missing env vars
Port issues
Dependency errors

🚀 Interview One-Liner

"A Docker container exits when its main process (PID 1) stops. Ensuring a long-running foreground process is key to keeping it alive."

---

<img width="952" height="368" alt="image" src="https://github.com/user-attachments/assets/c0f98e7c-d562-4023-b6e1-55d7fd3326a3" />

🚀 Interview One-Liner

"GitHub Actions evaluates workflows from the target branch of the PR, so if the workflow file isn't present there or branch filters don't match, it won’t trigger."

---

<img width="952" height="368" alt="image" src="https://github.com/user-attachments/assets/47416f20-3061-4509-8144-0b5bc2a6d71e" />

🚀 Interview One-Liner

"Ansible UNREACHABLE errors are usually due to SSH connectivity issues—so validating manual SSH access is always the first debugging step."

---

<img width="952" height="368" alt="image" src="https://github.com/user-attachments/assets/c7c25302-9b45-40dd-be4c-0b438c7106a4" />

🧩 1️⃣ Application Layer (Inside Container)

✔️ (You already did this well)

Check app is running:
ps aux
ss -tulnp
Test locally inside container:
curl localhost:<app_port>
🐳 2️⃣ Container Layer

✔️ (Also well covered)

Check running containers:
docker ps
Check port mapping:
docker ps  # PORTS column
Logs:
docker logs <id>
🖥️ 3️⃣ Host / Server Layer
Check if port is exposed on host:
ss -tulnp | grep <port>
Firewall:
ufw status
☁️ 4️⃣ Infrastructure Layer (Terraform)

This is where you can improve 👇

Check:
Security Groups / Firewall rules
Port 80/443 open?
Correct public IP?

👉 Very common issue:

Infra created, but port not खुला (open)

⚙️ 5️⃣ Configuration Layer (Ansible)
Was app actually deployed correctly?
Check:
Service installed?
Config files correct?
Nginx / reverse proxy working?
🔄 6️⃣ CI/CD Layer (GitHub Actions)
Verify:
Latest code deployed?
Correct image version?
Pipeline logs

👉 Sometimes:

Pipeline succeeds, but old image still running

🌐 7️⃣ Network / Browser Layer
Try:
curl http://<public-ip>:<port>
DNS issues?
Load balancer misconfigured?
🧠 Golden Debug Strategy

Inside → Container → Host → Network → Cloud → CI/CD

🚀 Interview One-Liner

"I debug layer by layer—starting from the application inside the container, then container runtime, host networking, infrastructure security rules, and finally CI/CD to ensure the correct version is deployed."

⚡ Small Improvement Tip

You missed:

Security groups / firewall (very common real issue)
CI/CD validation

Add those next time → your answer becomes senior-level.

---

<img width="968" height="153" alt="image" src="https://github.com/user-attachments/assets/73f12e18-9d47-4a2e-93ae-3853e2d9f9a5" />

<img width="1038" height="861" alt="image" src="https://github.com/user-attachments/assets/c34a8f93-6705-421d-8ccf-b9dce4cc3d0e" />

---

<img width="1023" height="165" alt="image" src="https://github.com/user-attachments/assets/d6b82e29-fa15-47ad-89c9-e19fd323fc87" />

<img width="1013" height="877" alt="image" src="https://github.com/user-attachments/assets/a9df422a-2359-4599-8dca-863b4ba9844a" />

---

<img width="1034" height="175" alt="image" src="https://github.com/user-attachments/assets/82264407-a923-4423-ab2c-5c2801cd9f00" />


**⚠️ What’s missing (this is where interviews get strict)**
You didn’t verify endpoints (CRITICAL)

**This is the first thing to check when Service not working:**

`kubectl get endpoints <service-name>`

If empty → label mismatch / pod not ready

**You didn’t test connectivity inside cluster**

Need to confirm if service works internally:

`kubectl run test --rm -it --image=busybox -- sh`

`wget <service-name>:<port>`

Pod readiness / probes

Pod can be Running but not Ready

Service won’t route traffic

`kubectl get pods`

Service type awareness

NodePort / ClusterIP / LoadBalancer matters

If NodePort:

`curl <node-ip>:<nodeport>`

kube-proxy / networking (advanced edge)

Rare but strong signal in interviews

---

<img width="1034" height="175" alt="image" src="https://github.com/user-attachments/assets/52072b80-74d5-45c4-85e8-0503c661ad38" />


<img width="1014" height="850" alt="image" src="https://github.com/user-attachments/assets/d197b0e0-cc6c-42ec-8a72-5ea64fdc60f6" />

<img width="1045" height="867" alt="image" src="https://github.com/user-attachments/assets/3a55d6a0-342d-4390-a01a-4b5947b76114" />

<img width="1031" height="518" alt="image" src="https://github.com/user-attachments/assets/e6237f6d-3bb9-47b1-ad99-4df83157db90" />

---

<img width="841" height="233" alt="image" src="https://github.com/user-attachments/assets/b0fb9dab-a2e8-48ee-822c-479825265740" />

Ideal SRE-Level Answer

Check system load
```
top / htop
uptime
```
Identify top CPU consumers
```
ps -aux --sort=-%cpu | head -n 10
```
Inspect the process
```
ps -fp <PID>
top -p <PID>
```
Check logs
```
journalctl -u service_name
```
Check recent changes

Deployment?
Traffic spike?
Cron jobs?

Check resource constraints

Docker:
```
docker stats
```
System:
```
free -m
vmstat
Temporary mitigation (careful)
```
Restart only if needed:
```
systemctl restart service
```
Or limit CPU:
```
docker update --cpus=1 <container>
```

Permanent fix
Optimize code
Add autoscaling
Fix memory leaks / loops

---

<img width="841" height="233" alt="image" src="https://github.com/user-attachments/assets/72af9d19-a961-4126-8c68-9e46b0026a05" />


🔥 Complete SRE-Level Answer

If:

ping google.com ✅ works
curl https://google.com ❌ fails

Then possible issues are:

1. Firewall / Security Groups (Your Answer ✅)
ICMP allowed, HTTP/HTTPS blocked

Check:
```
iptables -L
ufw status
```
2. DNS vs HTTP difference
Ping uses DNS + ICMP
Curl uses DNS + TCP

Test:
```
nslookup google.com
curl 8.8.8.8
```

3. Proxy issue (VERY COMMON in companies)
Server may require proxy

Check:
```
env | grep -i proxy
```

4. Port 80/443 blocked (network level)

Test:
```
telnet google.com 80
nc -zv google.com 443
```
5. SSL / CA certificate issue
   
Curl fails due to cert validation

Test:
```
curl -v https://google.com
```
6. Outbound routing issue
Wrong route table

Check:
```
ip route
```





