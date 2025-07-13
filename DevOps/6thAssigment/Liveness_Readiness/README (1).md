# Assignment 1 – Deploying an App with Liveness and Readiness Probes on AKS

## 🎯 Objective

Deploy a sample application in Azure Kubernetes Service (AKS) with liveness and readiness probes configured for container health checks.

---

## 📁 Files

- `aks-deployment-with-probes.yaml`: Deployment file with health probes configured.

---

## 🚀 Deployment Steps

1. **Apply the deployment** to your AKS cluster:
   ```bash
   kubectl apply -f aks-deployment-with-probes.yaml
   ```

2. **Verify pods** are running:
   ```bash
   kubectl get pods
   ```

3. **Describe a pod** to inspect probe activity:
   ```bash
   kubectl describe pod <pod-name>
   ```

4. **Check logs (optional):**
   ```bash
   kubectl logs <pod-name>
   ```

5. **Watch live:**
   ```bash
   kubectl get pods --watch
   ```

---

## 🔍 Explanation

### ✅ Liveness Probe
- Ensures the container is alive.
- Failure restarts the container.
- Endpoint: `/healthz`

### ✅ Readiness Probe
- Ensures the container is ready to receive traffic.
- Failure removes the pod from the service.
- Endpoint: `/ready`

---

## ⚠️ Notes

- App must serve `/healthz` and `/ready` on port `8080`.
- If you use another image (like Python or Node.js), update `image:` and `containerPort`.

---

## ✅ Status Checklist

- [x] Deployment Created
- [x] Liveness Probe Working
- [x] Readiness Probe Working
- [ ] Service Configured (Optional)

---

## 📸 Sample Output

```bash
NAME                            READY   STATUS    RESTARTS   AGE
my-aks-app-6fcd7b6c8b-ktx92     1/1     Running   0          1m
```

---