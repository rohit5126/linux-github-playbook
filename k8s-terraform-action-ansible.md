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







