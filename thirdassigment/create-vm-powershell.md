
# 💻 Create Azure Virtual Machine using PowerShell

## 🎯 Objective

Use PowerShell to create an Azure Virtual Machine with custom network settings, credentials, and allowed region (westeurope).

---

## 🔹 Step 1: Login to Azure

```powershell
Connect-AzAccount -UseDeviceAuthentication
```

---

## 🔹 Step 2: Create a Resource Group

```powershell
New-AzResourceGroup -Name "PrinceRG" -Location "westeurope"
```

---

## 🔹 Step 3: Enter VM Credentials

```powershell
$cred = Get-Credential
```

You will be prompted to enter a username and password.

### 🔐 Password Rules (Must meet at least 3 of the following):

- At least one **uppercase** character (A–Z)
- At least one **lowercase** character (a–z)
- At least one **number** (0–9)
- At least one **special character** (e.g., @ # $ % !)
- ❌ Control characters (Enter, Tab, etc.) are not allowed

✅ Example: `Prince@2025`

---

## 🔹 Step 4: Create the VM

```powershell
New-AzVM `
  -ResourceGroupName "PrinceRG" `
  -Name "princetest" `
  -Location "westeurope" `
  -VirtualNetworkName "PrinceVNet" `
  -SubnetName "PrinceSubnet" `
  -SecurityGroupName "PrinceNSG" `
  -PublicIpAddressName "PrincePublicIP" `
  -Credential $cred `
  -OpenPorts 3389
```

---

## 🔹 Step 5: Connect to Your VM

1. Go to Azure Portal → Virtual Machines → `princetest`
2. Note the **Public IP**
3. Use:
   - RDP for Windows VM: `mstsc` or Remote Desktop App
   - SSH for Linux VM: `ssh username@public-ip`

---

## ✅ Output

- ✔️ VM created using PowerShell
- ✔️ Networking and credentials configured
- ✔️ Login ready using provided username/password

---

## 📌 Notes

- Use `westeurope` or allowed region (as per applied policy)
- If needed, remove/modify Azure policy to allow other locations

---

## 🔧 Troubleshooting

If you see:
```
The supplied password must be between 8-123 characters long...
```
→ Make sure your password meets the complexity rules listed above.
