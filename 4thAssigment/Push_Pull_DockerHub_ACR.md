# 📦 Docker Image Push and Pull (DockerHub & Azure Container Registry)

This README explains how to push and pull Docker images to DockerHub and Azure Container Registry (ACR), along with verification steps.

---

## 🐳 Part 1: DockerHub

### ✅ Step 1: Login to DockerHub

```bash
docker login
```

Enter your DockerHub **username** and **password** when prompted.

---

### ✅ Step 2: Tag the Local Image

```bash
docker tag flask-app princedayma230/flask-app:v1
```

---

### ✅ Step 3: Push to DockerHub

```bash
docker push princedayma230/flask-app:v1
```

---

### ✅ Step 4: Pull from DockerHub (To Test)

```bash
docker pull princedayma230/flask-app:v1
```

---

### 📸 How to Show It

- Go to: [https://hub.docker.com/repositories](https://hub.docker.com/repositories)
- Click on `princedayma230/flask-app`
- Show tags and pull commands
- Or run `docker images` to confirm it's pulled

---

## ☁️ Part 2: Azure Container Registry (ACR)

### ✅ Step 1: Create ACR (Using Azure Portal)

1. Go to [https://portal.azure.com](https://portal.azure.com)
2. Search “Container Registries”
3. Click **+ Create**
4. Fill in:
   - Resource Group: `MyResourceGroup`
   - Registry name: `myacr2025` (must be unique)
   - SKU: `Basic`
   - Location: `eastus` or `centralindia` (as per policy)
5. Click "Create"

---

### ✅ Step 2: Enable Admin User

1. In your ACR, go to **Access Keys**
2. Turn **Admin user: Enabled**
3. Copy **username** and **password**

---

### ✅ Step 3: Login to ACR

```bash
docker login myacr2025.azurecr.io
```

Use the admin username & password

---

### ✅ Step 4: Tag and Push

```bash
docker tag flask-app myacr2025.azurecr.io/flask-app:v1
docker push myacr2025.azurecr.io/flask-app:v1
```

---

### ✅ Step 5: Pull from ACR

```bash
docker pull myacr2025.azurecr.io/flask-app:v1
```

---

### 📸 How to Show It

- In Azure Portal:
  - Go to your ACR
  - Click on **Repositories**
  - Click on `flask-app` to see tags
- Or use Azure CLI (Cloud Shell):

```bash
az acr repository list --name myacr2025 --output table
az acr repository show-tags --name myacr2025 --repository flask-app --output table
```

---

## ✅ Summary

| Registry     | Command Example                                          |
|--------------|----------------------------------------------------------|
| DockerHub    | `docker push princedayma230/flask-app:v1`               |
| ACR          | `docker push myacr2025.azurecr.io/flask-app:v1`         |

Use `docker pull` to verify both work successfully.

