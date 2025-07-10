# Assignment: Configure Horizontal Pod Autoscaling in AKS

## ✅ Objective
Automatically scale pods based on CPU utilization.

## 🧱 Step-by-step Process

### 1. Deploy the App with CPU Limits
Use the following YAML to deploy an `nginx` app that includes CPU resource limits.

```
kubectl apply -f nginx-autoscale-deployment.yaml
```

### 2. Enable Autoscaling
```
kubectl autoscale deployment nginx-autoscale --cpu-percent=50 --min=1 --max=5
```

### 3. Verify HPA
```
kubectl get hpa
```

### 4. (Optional) Generate Load
```
kubectl run -i --tty load-generator --image=busybox /bin/sh
# Inside shell:
while true; do wget -q -O- http://nginx-autoscale; done
```

### 5. Cleanup (Optional)
```
kubectl delete deployment nginx-autoscale
kubectl delete hpa nginx-autoscale
```

## 📌 Notes
- HPA requires Metrics Server (already enabled in AKS).
- Horizontal scaling helps maintain application performance under load.