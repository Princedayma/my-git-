
# 🔐 Azure Key Vault - Store & Retrieve Secrets via Azure Portal (UI)

## 🎯 Objective

- Create an Azure Key Vault using Azure UI (portal)
- Store secrets in the vault
- Configure access policies for users
- Retrieve secrets via portal

---

## 🔹 Step 1: Create Azure Key Vault

1. Go to [https://portal.azure.com](https://portal.azure.com)
2. Search for **"Key vaults"** and click **+ Create**
3. Fill the form:
   - **Subscription**: Your active subscription
   - **Resource group**: Use existing or create new
   - **Key vault name**: `princeKeyVault123` (must be globally unique)
   - **Region**: e.g., East US
4. Click **Review + Create**, then **Create**

---

## 🔹 Step 2: Store a Secret

1. Open the newly created Key Vault
2. Click **Secrets** from the left menu
3. Click **+ Generate/Import**
4. Enter:
   - **Name**: `MySecretKey`
   - **Value**: `ThisIsMySecret123`
5. Click **Create**

---

## 🔹 Step 3: Set Access Policies

1. In Key Vault → Click **Access Policies**
2. Click **+ Create**
3. Set Permissions:
   - Secrets: `Get`, `List`, `Set`, `Delete`
4. Under **Principal**, click **Select Principal**
   - Choose the user to grant access
5. Click **Next**, then **Review + Create**, then **Create**

---

## 🔹 Step 4: Retrieve Secret from UI

1. Go to **Secrets** in your Key Vault
2. Click on `MySecretKey`
3. Click **Current Version**
4. Click **Show Secret Value**

You should see: `ThisIsMySecret123`

---

## ✅ Output

- ✔️ Key Vault created successfully via Azure UI
- ✔️ Secret stored and access policy configured
- ✔️ Secret retrieved securely via portal

---

## 📌 Notes

- Key Vault ensures encryption of secrets at rest and in transit.
- Avoid hardcoding secrets in code — always use Key Vault securely.
