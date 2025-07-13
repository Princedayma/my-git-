
# 🚀 DevOps Assignment 1: Kubernetes App Deployment via Minikube (Cloud VM + SSH Tunnel)

## 📝 Objective
Deploy a Kubernetes cluster using **Minikube** on an **Azure Ubuntu VM**, run an NGINX app inside it, expose the app via **NodePort**, and access it on the local browser using **SSH port forwarding**.

---

## 🧱 Setup Overview

- **Cloud VM:** Ubuntu 22.04 (Azure)
- **Kubernetes tool:** Minikube with Docker driver
- **App:** NGINX (via Deployment)
- **Service:** NodePort
- **Access method:** SSH tunnel (Localhost ➝ Minikube Service)

---

## ⚙️ Step-by-Step Setup

### 🔹 1. Install Minikube inside Azure VM

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

### 🔹 2. Start Minikube Cluster

```bash
minikube start
```

> Automatically uses Docker as a driver and sets up Kubernetes inside the VM.

---

### 🔹 3. Deploy NGINX App

```bash
minikube kubectl -- create deployment nginx --image=nginx
```

---

### 🔹 4. Expose the Deployment as a Service

```bash
minikube kubectl -- expose deployment nginx --type=NodePort --port=80
```

---

### 🔹 5. Check Service Details

```bash
minikube kubectl -- get svc
```

Example output:
```
NAME         TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
nginx        NodePort   10.102.25.165   <none>        80:31592/TCP     45m
```

---

### 🔹 6. Verify Pod Status

```bash
minikube kubectl -- get pods
```

Example:
```
nginx-5869d7778c-r6nk7   1/1     Running   0   45m
```

---

## 🌐 Access the App via SSH Port Forwarding

### 🔹 Create SSH Tunnel from Local System

```bash
ssh -L 8888:192.168.49.2:31592 azureuser1@<VM_PUBLIC_IP>
```

> Maps your local `localhost:8888` → Minikube's internal `192.168.49.2:31592`

---

### 🔹 Open in Browser (On Local Machine)

```
http://localhost:8888
```

✅ This should load the **Nginx welcome page** running inside Kubernetes on the VM.

---

## ✅ Troubleshooting

### 🔸 Port 8080 Already in Use?
Use a different port like `8888`, `8889`, `9090`.

### 🔸 App not opening?
Run inside VM:
```bash
curl http://192.168.49.2:<NodePort>
```

### 🔸 Missing kubectl?
Use built-in:
```bash
minikube kubectl -- get pods
```

---

## 🏁 Summary

| Task | Done |
|------|------|
| Install Minikube | ✅ |
| Create Deployment | ✅ |
| Expose with NodePort | ✅ |
| Setup SSH Tunnel | ✅ |
| Access in Browser | ✅ |

---

## 📌 Author
Prince Dayma  
DevOps Internship Assignment – Kubernetes with Minikube  
MBM University, Jodhpur  
June 2025
