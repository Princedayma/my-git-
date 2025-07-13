# Kubernetes PersistentVolume and PersistentVolumeClaim (AKS Compatible)

This example demonstrates how to use PersistentVolumeClaim (PVC) in Azure Kubernetes Service (AKS) with dynamic provisioning.

## 📁 Files

- `pvc.yaml`: Creates a PersistentVolumeClaim using the default StorageClass (e.g., AzureDisk or AzureFile).
- `pod-using-pvc.yaml`: Deploys an NGINX Pod and mounts the PVC to `/usr/share/nginx/html`.

## 🔧 How It Works

1. **PVC is created** and requests 1Gi storage.
2. **AKS dynamically provisions** a PersistentVolume using Azure-managed storage.
3. **Pod uses PVC** to mount the persistent volume inside the container.

## 🧪 Commands

```bash
# Apply PVC and Pod
kubectl apply -f pvc.yaml
kubectl apply -f pod-using-pvc.yaml

# Check PVC and PV status
kubectl get pvc
kubectl get pv

# Enter the pod and write test data
kubectl exec -it mypod -- /bin/bash
echo "Hello from PVC!" > /usr/share/nginx/html/index.html
cat /usr/share/nginx/html/index.html
```

## 🧹 Clean Up

```bash
kubectl delete pod mypod
kubectl delete pvc my-pvc
```

---