# Azure AD RBAC and Policy Assignment Report

## 📘 Project Title: Role-Based Access Control and Policy Enforcement in Azure

### 👤 Prepared By: Prince Dayma  
### 📅 Date: July 13, 2025

---

## 🔧 Objective
To create and configure an Azure project named `ProjectX-RG` by:
- Creating user groups
- Inviting external users
- Assigning RBAC roles
- Enforcing resource deployment policies

---

## 📁 1. Resource Group Created
- **Name:** `ProjectX-RG`
- **Region:** East US

---

## 👥 2. Azure AD Groups Created
| Group Name | Description               | Membership Type | Role Assigned | Scope       |
|------------|---------------------------|------------------|----------------|--------------|
| Admin      | Admin Group               | Assigned         | Owner          | ProjectX-RG  |
| Developer  | Development Team          | Assigned         | Contributor    | ProjectX-RG  |
| Tester     | QA Testing Team           | Assigned         | Reader         | ProjectX-RG  |

---

## 👤 3. Guest User Invitation
- **Email:** princedayma230@gmail.com
- **Status:** Pending → Accepted
- **Object ID:** `61ba84aa-0b33-4a21-9d9b-fc1c716afda2`
- **Group Assigned:** `Tester`

---

## 🔐 4. RBAC Role Assignments

### ✅ Current Role Assignments (Shown in IAM):
| Name         | Type  | Role       | Scope              | Condition   |
|--------------|--------|------------|---------------------|-------------|
| Admin        | Group | Owner      | ProjectX-RG         | View/Edit   |
| Prince Dayma | User  | Owner      | Subscription (Inherited) | None |
| Developer    | Group | Contributor| ProjectX-RG         | None        |
| Tester       | Group | Reader     | ProjectX-RG         | None        |

---

## 🛡️ 5. Azure Policy Assignment

### 📌 Policy Details:
- **Name:** `Allowed-Locations-Only-EastUS`
- **Definition:** Allowed locations
- **Scope:** `ProjectX-RG`
- **Parameter:**
  - `listOfAllowedLocations`: `["eastus"]`
- **Policy Enforcement:** Enabled

---

## ✅ Final Status: COMPLETED

All role-based access control configurations and the Azure Policy were successfully assigned and verified.

You can now monitor compliance and activity under **Azure Policy** and **Access Control (IAM)**.

---

_This report is generated for documentation and submission purposes._
