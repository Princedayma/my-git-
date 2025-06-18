# 📦 Azure Storage & Identity Management Assignment

This project covers various hands-on tasks using Azure services including Storage Accounts, Blob/File/Queue services, Access Tiers, Replication, SAS Tokens, RBAC Roles, Azure Entra ID, and Lifecycle Management.  
All tests and operations are performed using Azure Portal, Azure Storage Explorer, and basic PowerShell/CLI scripts.

---

## ✅ Table of Contents

1. [Storage Account Creation & Blob Upload](#1-storage-account-creation--blob-upload)
2. [Authentication Methods & Testing](#2-authentication-methods--testing)
3. [Azure Storage Explorer Connection](#3-azure-storage-explorer-connection)
4. [Shared Access Signature (SAS)](#4-shared-access-signature-sas)
5. [Stored Access Policy over SAS](#5-stored-access-policy-over-sas)
6. [Access Tiers: Hot / Cool / Archive](#6-access-tiers-hot--cool--archive)
7. [Lifecycle Policy Testing](#7-lifecycle-policy-testing)
8. [Geo Replication (RA-GRS/GZRS)](#8-geo-replication-ra-grsgzrs)
9. [File Share Creation & Mounting](#9-file-share-creation--mounting)
10. [Azure File Sync](#10-azure-file-sync)

---

## 1️⃣ Storage Account Creation & Blob Upload

- Created storage account: `mystorageprince`
- Uploaded sample blob (`test.txt`)
- Tested file access via browser & Storage Explorer

---

## 2️⃣ Authentication Methods & Testing

- ✅ Access Keys tested via Azure Storage Explorer
- ✅ SAS Token tested for limited access
- ✅ RBAC tested via user role (Reader)

---

## 3️⃣ Azure Storage Explorer Connection

- Connected using both:
  - **Access Key**
  - **SAS URI**
- Explored Containers, Blobs, and File Shares

---

## 4️⃣ Shared Access Signature (SAS)

- Created SAS with:
  - **Permissions**: rwdlacupiytfx
  - **Services**: Blob, File, Queue, Table
- Shared SAS URI tested on web

---

## 5️⃣ Stored Access Policy over SAS

- Created container-level policy: `readPolicy`
- SAS linked to the stored policy
- Verified policy-scope access

---

## 6️⃣ Access Tiers: Hot / Cool / Archive

- Uploaded file → changed tier to:
  - 🔥 Hot → 🔄 Cool → 🧊 Archive
- Documented differences:

| Tier     | Cost       | Speed      | Use Case               |
|----------|------------|------------|------------------------|
| Hot      | High       | Fast       | Active data            |
| Cool     | Medium     | Medium     | Infrequent access      |
| Archive  | Lowest     | Very Slow  | Long-term cold storage |

---

## 7️⃣ Lifecycle Policy Testing

- Created policy:
  - Move blobs from Hot → Cool after 7 days
  - Delete after 30 days
- Uploaded blob → waited & tested policy

---

## 8️⃣ Geo Replication (RA-GRS/GZRS)

- Enabled **RA-GRS** on `mystorageprince`
- Primary: Central India
- Secondary (read-only): East US
- Accessed blob via replicated read-only endpoint

---

## 9️⃣ File Share Creation & Mounting

- Created File Share: `myfileshare`
- Uploaded `notes.txt`
- Used connect script:

```powershell
net use Z: \\mystorageprince.file.core.windows.net\myfileshare /u:mystorageprince <your_access_key>
