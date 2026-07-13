✅ Question 1 (Linux + Storage)

Your server suddenly shows “No space left on device”, but when you check disk usage, it doesn’t seem completely full.

How will you troubleshoot this issue step by step?

✅ Ideal Step-by-Step Answer

Check disk usage

df -h
Confirms which filesystem is full

Check inode usage (VERY IMPORTANT)

df -i

👉 Sometimes disk has space, but inodes are full → causes same error

Find large files/directories

du -sh /* 2>/dev/null | sort -h

Check deleted files still in use (classic cause 🔥)

lsof | grep deleted

👉 Logs deleted but still held by a process → space not freed

Check log files

/var/log
Large logs are common cause
Clean up
Remove old logs
Restart services holding deleted files
🔍 Key concept (Interview Gold)

👉 “No space left” ≠ always disk full

Could be:
Inodes full
Deleted files still open
Log explosion

----------------------------------------

✅ Question 2 (Docker + Image Optimization)

Your Docker image size is 1GB+, and it takes too long to pull and deploy.

What steps will you take to reduce the image size?

🔍 Make it interview-perfect (add these points)
Use smaller base images

alpine versions:

node:20-alpine
golang:alpine
Multi-stage build (your answer ✔)
Keep only compiled/built artifacts in final image
Avoid unnecessary files

Use .dockerignore

node_modules
.git
logs
Use npm ci instead of npm install
Cleaner, faster, no extra packages

Remove package manager cache

apt-get clean && rm -rf /var/lib/apt/lists/*
Minimize layers

Combine commands:

RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*

------------------------------------------

✅ Question 3 (Kubernetes – Basics + Debugging)

Your pod is in CrashLoopBackOff state.

What steps will you take to debug this issue?

🔍 Let’s make it a perfect structured answer

Check pod status

kubectl get pods
Confirm CrashLoopBackOff

Check logs

kubectl logs <pod-name>

👉 First place to find root cause (you did this ✔)

Check previous container logs (VERY IMPORTANT)

kubectl logs <pod-name> --previous

👉 Because container keeps restarting

Describe the pod

kubectl describe pod <pod-name>
Look for:
Events
Image issues
Liveness/readiness probe failures
Check configuration issues
Environment variables
Secrets / ConfigMaps
DB connection (your example ✔)

Check resource limits

Pod might be crashing due to OOMKilled
kubectl describe pod <pod-name>

-----------------------------------

✅ Question 4 (CI/CD – GitHub Actions)

Your GitHub Actions pipeline is not triggering on pull request, even though you have defined on: pull_request.

What could be the possible reasons and how will you fix it?

🔍 Final polished answer (what interviewer expects)

If a PR pipeline is not triggering:

Check event configuration

on:
  pull_request:

Check branch filters

branches: [main]
Ensure PR target branch matches

Check workflow location

.github/workflows/
Check if workflow exists in target branch
GitHub reads workflow from base branch, not source branch

Check PR event types (if restricted)

types: [opened, synchronize]

-------------------------------------

✅ Question 5 (Linux + Permissions – Scenario)

A user says they cannot access a file, even though the file has 777 permissions.

What could be the possible reasons?

🔍 Make it interview-perfect (add these)

Directory permission issue (you said ✔)

ls -ld <directory>
File ownership / user mismatch
User might not be expected owner/group

ACL (Access Control List)

getfacl <file>

👉 ACL can override normal permissions

SELinux (VERY ADVANCED 🔥)

sestatus

👉 Can block access even if permissions are 777
---------------------------------------

✅ Question 6 (Docker + Volumes)

You restart a container and all your application data is lost.

Why did this happen, and how will you fix it?

🔍 Make it interview-perfect (polished answer)

Problem:

Containers do not persist data → data stored inside container filesystem is lost when container is removed/recreated

Fix:

Use Docker Volumes (recommended)

docker volume create mydata

docker run -v mydata:/var/lib/mysql mysql

Use Bind Mounts (host mapping)

docker run -v /host/data:/var/lib/mysql mysql
Example (MySQL ✔ as you said)

Persist:

/var/lib/mysql
🔍 Key Interview Line

👉 “Containers are stateless by design, so we use volumes to persist stateful data.”

----------------------------

✅ Question 7 (Kubernetes + Networking)

A service in Kubernetes is not accessible from outside the cluster.

What could be the possible reasons, and how will you fix it?

👉 Answer step-by-step (this is a very common interview scenario 😏)

🔥 Complete Interview Answer (What recruiters expect)
🧠 Possible Reasons + Fixes
1️⃣ Service Type Issue
Default = ClusterIP (internal only)

✅ Fix:

type: NodePort

OR use:

type: LoadBalancer
2️⃣ Wrong Target Port / Port Mapping
Service not forwarding traffic correctly to Pod

✅ Check:

kubectl describe svc <service-name>

✔ Ensure:

port
targetPort
nodePort (if used)
3️⃣ Pod Not Running / Not Ready
Service exists but no healthy backend

✅ Check:

kubectl get pods
kubectl describe pod <pod>
4️⃣ Selector Mismatch (VERY COMMON ⚠)
Service selector doesn’t match pod labels

✅ Check:

kubectl get svc -o yaml
kubectl get pods --show-labels

✔ Fix labels mismatch

5️⃣ Firewall / Security Group Issue
NodePort exposed but blocked externally

✅ Fix:

Open port (e.g., 30080) in firewall / cloud SG
6️⃣ Application Listening on Localhost Only
App listening on 127.0.0.1 instead of 0.0.0.0

✅ Fix:

0.0.0.0:<port>
7️⃣ Ingress Not Configured Properly (if using)
Missing ingress controller or wrong rules
🎯 Final Interview Answer (Perfect Version)

👉 “If a Kubernetes service is not accessible externally, I would check multiple things: service type (ClusterIP vs NodePort/LoadBalancer), 
selector-label mismatch, pod health, correct port mapping, firewall rules, and whether the application is listening on 0.0.0.0. Based on findings, 
I would update the service or infrastructure accordingly.”


-----------------------------------------

✅ Question 8 (Linux + Debugging)

A system is running slow.

How will you troubleshoot it step by step?

🧠 Perfect Step-by-Step Troubleshooting Flow
1️⃣ Check Overall System Health (First step always)

👉 Get a quick snapshot:

Load average
CPU usage
uptime

✔ This tells: Is system actually overloaded?

2️⃣ Check CPU Usage
Identify high CPU processes

✔ If CPU is 100% → bottleneck found

3️⃣ Check Memory Usage
Use free -h
Look for:
Low available memory
High swap usage
4️⃣ Check Disk Usage
df -h → disk full?
du -sh → which directory is large
5️⃣ Check Disk I/O (VERY IMPORTANT ⚠)

👉 Many people miss this

High I/O wait = system slow even if CPU is low
6️⃣ Check Running Processes
Identify top resource consumers
Then decide:
Restart
Kill (graceful → force)
7️⃣ Check Logs
/var/log/syslog
/var/log/messages

✔ Look for:

Errors
Crashes
Repeated failures
8️⃣ Check Network (if applicable)
Slow API / DB calls?
Latency issues?
9️⃣ Check Zombie / Deleted Files
Your lsof point ✔ (very good)
🎯 Final Interview Answer (Strong Version)

👉 “I would start by checking overall system load and CPU usage, then analyze memory and disk usage. Next, I would check disk I/O to identify bottlenecks, followed by identifying high resource-consuming processes. I would review system logs for errors and also check network performance if needed. Based on findings, I would take actions like restarting services, clearing space, or optimizing processes.”

------------------------------------------

✅ Question 9 (Docker + Networking)

Your container is running, but you cannot access the application in the browser.

What all things will you check?

🧠 Complete Step-by-Step Debug Flow
1️⃣ Check if container is actually running
Sometimes container exits immediately

✔ Look for:

Restarting / Exited state
2️⃣ Check container logs
First place to find real error

✔ You already covered this 👍

3️⃣ Check port mapping
Host → Container port mapping

✔ Example:

8080:3000

👉 Access using:

http://<host-ip>:8080
4️⃣ Check application binding (VERY COMMON ⚠)
App must run on:
0.0.0.0

NOT:

127.0.0.1

✔ You nailed this 👌

5️⃣ Check if port is exposed inside container
App might not be listening

✔ Verify inside container:

Is service running?
Is port open?
6️⃣ Check firewall / security group
Port may be blocked externally

✔ Open required port

7️⃣ Check correct URL / endpoint
Wrong path = looks like app not working

✔ Example:

/api vs /api/v1
8️⃣ Check Docker network issues
If frontend calling backend

✔ Use:

container name (not localhost)
9️⃣ Check Dockerfile / EXPOSE (optional but good)
Not mandatory, but good practice
🎯 Final Interview Answer (Perfect)

👉 “I would first check if the container is running, then review logs for errors. Next, I would verify port mapping between host and container, and ensure the application is listening on 0.0.0.0. I would also check if the correct port is exposed and accessible, validate firewall rules, and confirm the correct URL is being used. If multiple containers are involved, I would verify Docker networking and service communication.”

-------------------------------------

✅ Question 10 (Final for today 🔥)

In Linux, what is the difference between:

Soft Link vs Hard Link

✅ Correct Explanation (Simple + Powerful)
🔗 Soft Link (Symbolic Link)
Acts like a shortcut
Points to the file path

✔ If original file is deleted → ❌ link breaks
✔ Can link across filesystems
✔ Has different inode

👉 Example use:

/usr/bin/python → python3
🔗 Hard Link
Points to the same inode (same data on disk)
It is NOT a copy — just another reference

✔ If original file is deleted → ✅ still works
✔ Cannot cross filesystems
✔ Shares same inode number



👉 “A soft link is a symbolic pointer to a file path, so if the original file is deleted, the link becomes invalid. A hard link, on the other hand, points to the same inode as the original file, meaning both share the same data. Even if the original file is deleted, the hard link continues to work since the data still exists.”
