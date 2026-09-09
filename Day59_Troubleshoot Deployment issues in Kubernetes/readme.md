# Kubernetes Troubleshooting: Fixing Broken Redis Deployment

## 📌 Task Overview
The `redis-deployment` in the Kubernetes cluster was failing to launch pods due to a configuration error made during a recent update. The goal was to diagnose the issue and restore the Redis deployment to a `Running` state.

---

## 🔍 Root Cause Analysis
Upon inspecting the pod events using `kubectl describe`, the following error was identified:
- **Error:** `MountVolume.SetUp failed for volume "config" : configmap "redis-conig" not found`
- **Issue:** The deployment volume reference contained a typo in the ConfigMap name (`redis-conig` instead of `redis-config`).

---

## 💻 Exact Commands Executed

### 1. Diagnose the Issue
Inspect pod events to locate the volume mount failure:
```bash
# Describe the pod to review error events
kubectl describe pod <failing-pod-name>
```
2. Apply the Fix
Edit the deployment configuration directly in the cluster to correct the ConfigMap name typo:
```
Bash
# Edit deployment configuration
kubectl edit deploy redis-deployment
Updated redis-conig to redis-config.
```
3. Verify Deployment & Pod Status
Confirm that the deployment rollout succeeded and the pod is running:

Bash
# Check deployment status
kubectl get deploy

# Check pod status and restarts
kubectl get po
✅ Final Result
Deployment: redis-deployment (1/1 READY)

Pod Status: redis-deployment-5476b4ddd6-p682g is Running (0 Restarts)
