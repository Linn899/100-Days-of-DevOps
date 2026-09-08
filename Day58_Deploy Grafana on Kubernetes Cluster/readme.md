# Day 58: Deploy Grafana on Kubernetes Cluster

This repository contains the Kubernetes manifests to deploy a Grafana application and expose it via a NodePort Service on port 32000.

## Manifest Files

### 1. `deployment.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-xfusion
  labels:
    app: grafana-deployment-xfusion
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana-deployment-xfusion
  template:
    metadata:
      labels:
        app: grafana-deployment-xfusion
    spec:
      containers:
      - name: grafana
        image: grafana/grafana:latest
        ports:
        - containerPort: 3000
```
### 2. service.yaml
```
YAML
apiVersion: v1
kind: Service
metadata:
  name: grafana-deployment-xfusion
  labels:
    app: grafana-deployment-xfusion
spec:
  type: NodePort
  selector:
    app: grafana-deployment-xfusion
  ports:
  - port: 3000
    targetPort: 3000
    nodePort: 32000
    protocol: TCP
```
## 🚀 Execution & Verification
### 1. Deploy the Application & Service
```Bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```
### 2. Verify Resources
```Bash
kubectl get deployment grafana-deployment-xfusion
kubectl get svc grafana-deployment-xfusion -o wide
kubectl get pods -l app=grafana-deployment-xfusion
```
