# Kubernetes Environment Variables - Sample Deployment

This repository contains a Kubernetes Pod manifest (`pod.yaml`) configured to demonstrate passing environment variables directly into a container execution command.

## 📌 Pod Configuration

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: print-envars-greeting
spec:
  restartPolicy: Never
  containers:
  - name: print-env-container
    image: bash
    command: ["/bin/sh", "-c", 'echo "$(GREETING) $(COMPANY) $(GROUP)"']
    env:
    - name: GREETING
      value: "Welcome to"
    - name: COMPANY
      value: "xFusionCorp"
    - name: GROUP
      value: "Ltd"
```
🚀 Execution & Verification
1. Deploy the Pod
Bash
kubectl apply -f pod.yaml
2. Verify Output Logs
Bash
kubectl logs -f print-envars-greeting
Expected Output:

Plaintext
Welcome to xFusionCorp Ltd
3. Check Pod Status
Bash
kubectl get pod print-envars-greeting
