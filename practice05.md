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

---

What I'd expect you to say in an interview

"Before applying, I would first inspect the Terraform plan carefully and identify which attribute is forcing the EC2 instance replacement. Since this is production, I wouldn't immediately apply the change. I would verify whether the replacement is actually required and check the impact on the application. If replacement is unavoidable, I would plan a safe migration strategy, such as creating the replacement instance before destroying the existing one using create_before_destroy, provided the architecture and resource constraints allow it. I'd also make sure the application data is not tied to the instance and that backups, health checks and rollback procedures are in place. For a production workload, I would review the plan and change through the normal approval process before applying it."

Extra point

If the application is stateful or the EC2 instance contains important data, create_before_destroy doesn't magically migrate that data.

This is why a mature DevOps answer considers:

Terraform change → impact → state/data → availability → backup → rollout → rollback

rather than just:

Terraform wants replacement → add lifecycle → apply.

---

ow would you troubleshoot and resolve the issue?

Walk me through your approach step by step.

i will ssh into the server and check the usage df -h, then I will check which folder is using highest disk space, then I will check the disk usage of log file using du -sh /home/var/log, and if its using alot of space I will delete older log files find and delete it. 

Good start. You have the right first step, but there are a couple of important command corrections and one major troubleshooting point.

What you did well

Your approach:

SSH → df -h → identify where space is being consumed → investigate logs → clean old files

That's correct.

Corrections

You mentioned:

du -sh /home/var/log

The usual system log location is:

/var/log

To find the biggest directories:

sudo du -xh /var/log | sort -h | tail -n 10

Or to find large directories from the root filesystem:

sudo du -xh / --max-depth=1 | sort -h

Then investigate further.

For old log files, don't immediately delete them. First check whether logrotate is configured:

sudo logrotate -d /etc/logrotate.conf

You can also find large files:

sudo find /var -type f -size +500M -ls
Important interview point

Before deleting anything, determine what is consuming the disk. It might be:

Application logs
Docker images/containers
Deleted files still held open
Package caches
Core dumps
Temporary files
Database files

For example, if Docker is involved:

docker system df

And if df shows high usage but du doesn't explain it, check deleted-but-open files:

sudo lsof +L1
Interview-ready flow

"First I would check df -h to identify which filesystem is at 95%. Then I would use du to identify the directories consuming the most space and drill down to the largest files. If logs are responsible, I would check log rotation and safely remove or rotate old logs rather than blindly deleting active log files. I would also check Docker, temporary files, package caches, and deleted files still held open by processes. After cleanup, I would verify the disk usage again with df -h."

Score: 8/10

Your troubleshooting direction is good. The next improvement is to avoid jumping directly to logs—first establish exactly what is consuming the disk.

---

Good answer to finish the test. You correctly identified resource pressure + scaling as one possible cause, and kubectl top pods is a useful command.

But for a production troubleshooting question, you jumped to HPA too early. The interviewer wants to see that you first prove where the bottleneck is.

What you did well
Considered insufficient CPU/memory.

Used:

kubectl top pods
Understood that increased traffic can require more pod replicas.
Correctly identified HPA as a potential solution.
What I'd improve

Don't assume:

"The pods don't have enough resources, so I'll create an HPA."

First determine where the request is becoming slow.

I'd troubleshoot layer by layer:

User
 ↓
Load Balancer / Ingress
 ↓
Frontend
 ↓
Backend/API
 ↓
Database
1. Check whether the problem is widespread
kubectl get pods -A
kubectl get nodes
kubectl top nodes
kubectl top pods -A

Look for CPU/memory pressure, OOM, pod restarts, or unhealthy nodes.

2. Check the ingress/load balancer

Since users are timing out, verify whether requests are reaching Kubernetes and whether the LB/Ingress is reporting errors or high latency.

3. Check frontend/backend

Don't only check frontend logs. Check the backend too:

kubectl logs <frontend-pod>
kubectl logs <backend-pod>

Look for:

Timeout errors
5xx responses
Slow API calls
Connection failures
4. Check services/endpoints
kubectl get svc
kubectl get endpoints

Make sure traffic is actually reaching healthy pods.

5. Check database

If the backend is waiting for the database, adding frontend pods won't solve the problem.

I'd check:

DB CPU/memory
Connection count
Slow queries
Connection pool exhaustion
Database locks
6. Then consider scaling

If metrics prove that pods are CPU/memory constrained and traffic is increasing, then I'd consider HPA.

Also verify that the deployment has appropriate:

resources:
  requests:
  limits:

because HPA commonly relies on resource metrics such as CPU utilization.
