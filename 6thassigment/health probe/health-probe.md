# Configure Health Probes in Kubernetes (AKS)

## 🎯 Objective
Create a pod in Azure Kubernetes Service (AKS) that includes liveness and readiness probes to monitor container health.

---

## 📁 YAML File: `health-probe-app.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: health-probe-app
  labels:
    app: health-probe-app
spec:
  containers:
  - name: health-probe-container
    image: nginxdemos/hello
    ports:
    - containerPort: 80
    livenessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 10
    readinessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 5
```

---

## 🔍 Probe Explanation

- **Liveness Probe**: Checks if the container is alive. If it fails repeatedly, Kubernetes restarts the container.
- **Readiness Probe**: Checks if the app is ready to receive traffic. If it fails, traffic is not routed to the pod.

---

## 🚀 Commands to Deploy

```bash
kubectl apply -f health-probe-app.yaml
kubectl describe pod health-probe-app
kubectl get pods
```

---

## ✅ Verification

- Check `kubectl describe pod health-probe-app` for probe status.
- Logs will show container startup and probe results.