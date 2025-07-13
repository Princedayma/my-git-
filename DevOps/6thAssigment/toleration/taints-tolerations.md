# Assignment: Configure Taints and Tolerations in Kubernetes (AKS)

## 🎯 Objective
To understand how to apply **taints** on nodes and configure **tolerations** in pods to control pod scheduling behavior.

---

## 🧠 What are Taints and Tolerations?

- **Taints** are applied to nodes to **repel** pods that don’t tolerate the taint.
- **Tolerations** are applied to pods, allowing them to **tolerate** the taint on a node and get scheduled.

### ⛔ Taint Syntax:
```bash
kubectl taint nodes <node-name> key=value:effect
# Example:
kubectl taint nodes mynode team=dev:NoSchedule
```

### ✅ Toleration Example in a Pod YAML:
```yaml
tolerations:
- key: "team"
  operator: "Equal"
  value: "dev"
  effect: "NoSchedule"
```

---

## 📄 Steps to Configure

### Step 1: Identify Node Name
```bash
kubectl get nodes
```

### Step 2: Taint a Node
```bash
kubectl taint nodes <node-name> team=dev:NoSchedule
```

### Step 3: Deploy a Pod with Toleration
```bash
kubectl apply -f taint-toleration-pod.yaml
```

### Step 4: Verify Scheduling
```bash
kubectl get pods -o wide
```

---

## ✅ Expected Output
- Your pod should get scheduled on the tainted node because it tolerates the taint.

---

## 📌 Note:
- Pods **without** tolerations won’t be scheduled on tainted nodes (with `NoSchedule`).
- Useful for **workload isolation**, like running critical workloads on dedicated nodes.

---

## 📂 Files Included
- `taint-toleration-pod.yaml` – Pod manifest with toleration.
- `taints-tolerations.md` – This assignment file with explanation and steps.
