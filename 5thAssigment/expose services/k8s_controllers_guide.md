# Kubernetes Controllers Deployment Guide

This guide explains how to deploy **ReplicationController**, **ReplicaSet**, and **Deployment** in Kubernetes using YAML files.

---

## ✅ 1. ReplicationController

**File:** `my-rc.yaml`

### 🔧 Command to Apply
```bash
kubectl apply -f my-rc.yaml
```

### ✅ Advantages
- Ensures the specified number of pod replicas are running.
- Simple controller to maintain pod count.

### ❌ Disadvantages
- Old and less flexible.
- Doesn't support rolling updates or rollback.

---

## ✅ 2. ReplicaSet

**File:** `my-replicaset.yaml`

### 🔧 Command to Apply
```bash
kubectl apply -f my-replicaset.yaml
```

### ✅ Advantages
- Supports label selectors (`matchLabels`, `matchExpressions`).
- Ensures specified replica count.
- Used by Deployments under the hood.

### ❌ Disadvantages
- Not commonly used directly—Deployments offer more features.

---

## ✅ 3. Deployment

**File:** `my-deployment.yaml`

### 🔧 Command to Apply
```bash
kubectl apply -f my-deployment.yaml
```

### ✅ Advantages
- Provides rolling updates and rollback.
- Automatically manages ReplicaSets.
- Most recommended for production.

### ❌ Disadvantages
- Slightly more complex than ReplicaSet or RC.

---

## 🛰️ Verifying Resources

### View All Running Resources
```bash
kubectl get all
```

---

## 🌐 Access via Services

You can expose deployments using:

### ClusterIP (default, internal only)
```bash
kubectl expose deployment my-deployment --type=ClusterIP --port=80 --target-port=80
```

### NodePort (accessible via Node IP + port)
```bash
kubectl expose deployment my-deployment --type=NodePort --port=80 --target-port=80
```

### LoadBalancer (get external IP)
```bash
kubectl expose deployment my-deployment --type=LoadBalancer --port=80 --target-port=80
```

---

## 🧹 Cleanup

```bash
kubectl delete -f my-rc.yaml
kubectl delete -f my-replicaset.yaml
kubectl delete -f my-deployment.yaml
```

---

> 📘 Use Deployments for most production workloads. RC and RS are useful for learning or legacy setups.