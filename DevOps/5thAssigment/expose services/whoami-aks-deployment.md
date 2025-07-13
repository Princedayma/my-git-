# 🚀 AKS Deployment: `traefik/whoami` App

## 📦 Purpose

Deploy the public Docker image `traefik/whoami` to Azure Kubernetes Service (AKS) using a `Deployment` and expose it with a `LoadBalancer` service.

---

## 🛠️ Kubernetes YAML Used

### ✅ whoami.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: whoami
spec:
  replicas: 2
  selector:
    matchLabels:
      app: whoami
  template:
    metadata:
      labels:
        app: whoami
    spec:
      containers:
      - name: whoami
        image: traefik/whoami
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: whoami-svc
spec:
  type: LoadBalancer
  selector:
    app: whoami
  ports:
    - port: 80
      targetPort: 80
```

---

## 🧪 Deployment Steps

### 1. Create the YAML file
```bash
nano whoami.yaml
# Paste the content above, then save with CTRL+O, ENTER, CTRL+X
```

### 2. Apply the configuration
```bash
kubectl apply -f whoami.yaml
```

---

## 🐞 Error: `ImagePullBackOff`

### ❌ Error
```bash
STATUS             ImagePullBackOff
```

### ✅ Solution
- The image you used might be private or invalid.
- Replace with a **public Docker image**, like `traefik/whoami`.

---

## 🔐 Error: `The server has asked for the client to provide credentials`

### ❌ Error
```bash
error: error validating data: failed to download openapi...
```

### ✅ Solution
```bash
az aks get-credentials --resource-group MyLinuxVM_group --name myAKScluster --overwrite-existing
```

---

## 🧼 Cleaning Up Old Deployments

```bash
kubectl delete deployment nginx-deployment myapp-deployment hello-deployment
kubectl delete svc nginx-clusterip nginx-nodeport nginx-lb myapp-service hello-service
```

---

## ✅ Accessing the App

### Step 1: Get Service Info
```bash
kubectl get svc whoami-svc
```

Expected output:
```bash
NAME          TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)        AGE
whoami-svc    LoadBalancer   10.0.165.77     20.233.168.155    80:xxxx/TCP    Xm
```

### Step 2: Open in Browser

Visit:
```
http://<EXTERNAL-IP>
```

You’ll see something like:
```json
Hostname: whoami-xxxxx
IP: 10.244.x.x
Headers: ...
```

---

## 🧰 Bonus: Port-Forward (if LoadBalancer not working)

```bash
kubectl port-forward svc/whoami-svc 8080:80
```

Then access:
```
http://localhost:8080
```

---

## ✅ Summary

- You deployed a **visually interactive microservice** in AKS
- You resolved `ImagePullBackOff` and `auth` issues
- You exposed it publicly with `LoadBalancer`

---

Made by: Prince Dayma 🌐