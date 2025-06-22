
# 🧑‍💻 Azure DevOps Internship Assignment – VM Backup & Alerts

This assignment covers:
- Creating Recovery Services Vault
- Scheduling daily VM backup at 3:00 AM
- Configuring CPU alert rules
- Using Azure Backup Center
- Troubleshooting failed backup configurations

---

## ✅ A. Schedule Daily VM Backup (3:00 AM) Using Recovery Services Vault

### 1. Create Recovery Services Vault

1. Go to Azure Portal → Search **Recovery Services vaults**
2. Click **+ Create**
3. Fill:
   - Vault name: `vault123`
   - Resource group: your RG (e.g., `PrinceRG`)
   - Location: same as your VM (e.g., `westeurope`)
4. Click **Review + Create**

---

### 2. Enable VM Backup

1. Go to `vault123` → Click **+ Backup**
2. Select:
   - Workload: `Azure`
   - Type: `Virtual Machine`
3. Click **Backup** → Select your VM
4. Create a new Backup Policy:
   - Frequency: `Daily`
   - Time: `3:00 AM`
   - Retention: `30 days`
5. Click OK → Enable backup

---

## 🔔 B. Create CPU Alert Rule for VM

### 1. Go to Virtual Machine → Alerts

1. Click **+ New Alert Rule**
2. Scope: Your VM
3. Condition:
   - Signal: `Percentage CPU`
   - Logic: Greater than 80%
4. Action Group:
   - Create new group
   - Notification Type: Email
   - Enter your email
5. Name: `HighCPUAlert`
6. Click **Create**

---

## 🔄 C. Use Backup Center to Monitor & Apply Backup

1. Go to Azure Portal → Search **Backup Center**
2. Click **+ Backup**
3. Data source: `Azure Virtual Machines`
4. Vault: `vault123`
5. Apply 3:00 AM policy to your VM

---

## 🚨 D. Troubleshooting – Backup Not Working

### Common Errors:
- `No resource extensions found`
- `Initial backup pending`
- `There are no virtual machines that can be backed up in this vault`

---

### Fix Steps:

#### Step 1: Check VM Extensions

- Go to **VM → Extensions**
- If missing:
  - Add `AzureBackupWindowsWorkload` or `AzureBackupLinuxWorkload`

#### Step 2: Stop Backup & Clean Up

- Go to **vault123 → Backup Items → Azure VM**
- If VM is listed:
  - Click on it → **Stop Backup**
  - Choose **Delete backup data**

#### Step 3: Re-enable Backup Cleanly

- Go back to vault → Click **+ Backup**
- Select your VM again
- Re-apply the 3:00 AM backup policy

#### Step 4: Trigger First Backup

- Go to `Vault → Backup Items → Azure VM → princetest`
- Click **Backup Now**

---

### Optional CLI Cleanup

```bash
az backup protection disable \
  --vault-name vault123 \
  --resource-group PrinceRG \
  --container-name IaasVMContainer;iaasvmcontainerv2;prince-rg;princetest \
  --item-name princetest \
  --delete-backup-data true
```

---

## ✅ Final Outcome

- VM backed up daily at 3:00 AM
- CPU alert rule working for >80%
- Backup Center shows all backup status
- Troubleshooting steps documented
