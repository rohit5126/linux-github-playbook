Question 1 (Linux – Intermediate)

A process is running on your system and consuming high CPU. You know the process name is node.

Explain step-by-step:

How will you identify the exact process (PID)?
How will you monitor its CPU usage in real time?
How will you safely stop it (graceful + force)?

💯 Ideal Answer (What interviewer expects)
Find PID using pgrep or ps
Monitor using top -p <PID> or htop
Stop using kill (graceful) → kill -9 (force)

------------------------------------------

✅ Question 2 (Docker – Intermediate)

You have a running container named backend-app.

How will you check logs of the container?
How will you access inside the container?
How will you check which ports are exposed and mapped?

💯 Ideal Interview Answer
Logs → docker logs -f backend-app
Exec → docker exec -it backend-app sh
Ports → docker ps / docker port / docker inspect

--------------------------------

✅ Question 3 (Networking – Intermediate)

Your application is running on port 8080, but it is not accessible from outside the server.

Explain step-by-step how you will troubleshoot this.

(Think like real DevOps: OS level + firewall + cloud + app level)

✅ What You Did Right

✔ Checked port:

nc -zv localhost 8080

✔ Checked listening ports:

ss -tulnp

✔ Identified binding issue (0.0.0.0 vs 127.0.0.1) ✅
👉 This is a very important real-world root cause

❌ What’s Missing (Important Gaps)
Firewall check (very common issue)
Cloud Security Group / NACL (AWS/Azure/GCP)
External connectivity test
Application-level validation
💯 Ideal Interview Answer (Step-by-Step)
1. Check if app is running & listening
ss -tulnp | grep 8080

👉 Ensure:

Port is listening
Bound to 0.0.0.0 (not 127.0.0.1)
2. Test locally
curl localhost:8080

👉 Confirms app is working inside server

3. Check firewall (Linux)
sudo ufw status

or

sudo iptables -L

👉 Allow port if blocked:

sudo ufw allow 8080
4. Check cloud security group (VERY IMPORTANT)

👉 Ensure inbound rule:

Port: 8080
Source: 0.0.0.0/0 (or your IP)
5. Test from outside
curl http://<server-ip>:8080
6. Check application logs
journalctl -u <service>

or app logs

🔥 Pro Tip (Interview Gold)

Mention this line:

“If it's bound to 127.0.0.1, the app will work locally but won’t be accessible externally.”

------------------------------------------------------

✅ Question 4 (Shell Scripting – Intermediate)

Write a shell script to:

Check if a service (e.g., nginx) is running
If NOT running → start the service
Print appropriate message in both cases

```
#!/bin/bash

SERVICE="nginx"

# Check if service is running
if systemctl is-active --quiet $SERVICE
then
    echo "$SERVICE is already running."
else
    echo "$SERVICE is not running. Starting $SERVICE..."
    systemctl start $SERVICE

    # Verify again
    if systemctl is-active --quiet $SERVICE
    then
        echo "$SERVICE started successfully."
    else
        echo "Failed to start $SERVICE."
    fi
fi
```
----------------------------------------------

✅ Question 5 (Linux + Logs – Intermediate)

You are told that a service is failing repeatedly.

How will you check the logs for that service?
How will you check only the last 50 log lines?
How will you follow logs in real-time?

💯 Ideal Interview Answer
# View logs
journalctl -u nginx

# Last 50 lines
journalctl -u nginx -n 50

# Real-time logs
journalctl -u nginx -f

---------------------------------------------

✅ Question 6 (Git + DevOps – Intermediate)

You pushed code, but accidentally committed a file with secrets (.env).

Now it's already in the remote repo.

How will you remove that file from Git history?
How will you prevent it from happening again?

1. Remove file from entire Git history

✔ Best modern way:

git filter-repo --path .env --invert-paths

2. Force push changes
git push origin --force --all

3. Prevent future issues

✔ Add to .gitignore

.env

🔥 MOST IMPORTANT (Interview Gold Point)

👉 You MUST say this:

“After removing the file, I will rotate/revoke the exposed secrets because they are already compromised.”

-----------------------------------------------

✅ Question 7 (Kubernetes – Intermediate)

You deployed a pod, but it is stuck in CrashLoopBackOff.

How will you debug the issue step-by-step?
Which commands will you use?

💯 Ideal Interview Answer (Step-by-Step)
1. Check Pod Status
kubectl get pods

👉 Confirm CrashLoopBackOff

2. Check Logs (VERY IMPORTANT)

✔ Current logs:

kubectl logs <pod-name>

🔥 Previous crash logs (MOST IMPORTANT):

kubectl logs <pod-name> --previous
3. Describe Pod
kubectl describe pod <pod-name>

👉 Look for:

Events (errors, restart reason)
Exit code
Image issues
Probe failures
4. Check Events
kubectl get events --sort-by=.metadata.creationTimestamp
5. Check Common Causes
❌ App crash (bad code / config)
❌ Wrong environment variables
❌ Port mismatch
❌ Liveness/Readiness probe failing
❌ Missing dependencies (DB not reachable)
6. Debug Inside Container (if possible)
kubectl exec -it <pod-name> -- sh
7. Check Resource Issues
kubectl describe pod <pod-name>

👉 Look for:

OOMKilled
CPU limits exceeded
🔥 Interview Gold Line

“I will check --previous logs because CrashLoopBackOff means the container is restarting after failure.”

----------------------------------------------------------------

✅ Question 8 (CI/CD – Intermediate)

Your CI pipeline is failing at the Docker build stage.

How will you debug the issue?
What are common reasons for Docker build failure?

💯 Ideal Interview Answer
1. Debugging Steps
🔍 Check pipeline logs (FIRST step)

👉 Always start here

# Example (GitHub Actions / CI logs)
Check error message in Docker build step
🔍 Validate Dockerfile path
docker build -f Dockerfile .

👉 Ensure correct path in pipeline

🔍 Try building locally
docker build -t test-image .

👉 Helps isolate CI vs code issue

🔍 Check Docker login (for private images)
docker login

👉 Required if:

Pulling private base image
Pushing to registry
🔍 Check build context

👉 Missing files in context often break build

🔍 Check permissions
Runner has Docker installed?
Proper privileges?
2. Common Reasons for Docker Build Failure
❌ Dockerfile issues
Wrong base image
Syntax errors
Wrong COPY paths
❌ Dependency issues
npm install / pip install failing
Network issues
❌ Authentication issues
Private registry access denied
❌ File not found
COPY package.json .

👉 File not in build context

❌ Port / runtime mismatch
App fails during build/test stage
❌ Resource issues
Out of memory in CI runner
🔥 Interview Gold Lines

“I first check CI logs, then try to reproduce locally to isolate the issue.”

“Most Docker build failures are due to incorrect build context or Dockerfile errors.”

-------------------------------------

✅ Question 9 (AWS / Cloud – Intermediate)

You deployed an app on an EC2 instance, but it's not accessible via browser.

What all things will you check (step-by-step)?
Mention AWS-specific components also.

🔥 Interview Gold Summary

“I will check application → port binding → security group → NACL → OS firewall → public IP → logs.”

----------------------------------------
🚀 Final Question (Question 10 – Bonus, Advanced)
Scenario (Real DevOps)

Your production website is suddenly down.

👉 What will be your first 5 actions in the first 5 minutes?



📣 7. Communicate (VERY IMPORTANT)

“Investigating issue, service is down, checking logs and recent changes.”

👉 This is what separates DevOps vs SRE mindset

🔥 Interview Gold Line

“I will not immediately restart the service. First I will identify the root cause and check recent deployments, as most production issues are caused by recent changes.”



