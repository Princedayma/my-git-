
# ✅ Azure Policy Assignment - Allowed Locations (Subscription Level)

## 🎯 Objective

Assign a built-in Azure Policy at the **subscription level** to restrict resource creation to specific allowed regions (e.g., `westeurope`).

---

## 🔹 Policy Details

- **Policy Name**: Allowed locations  
- **Policy Definition ID**: `e56962a6-4747-49cd-b67b-bf8b01975c4c`  
- **Scope**: `/subscriptions/b290a724-98ac-4f31-bec6-54bb616b497f`

---

## 🛠️ Command Used

```bash
az policy assignment create \
  --name "allowed-locations-policy" \
  --display-name "Allowed Locations Only" \
  --policy "e56962a6-4747-49cd-b67b-bf8b01975c4c" \
  --params "{ \"listOfAllowedLocations\": { \"value\": [\"westeurope\"] } }" \
  --scope "/subscriptions/b290a724-98ac-4f31-bec6-54bb616b497f"
```

---

## 🔍 Verify the Assignment

List all policy assignments for the subscription:

```bash
az policy assignment list \
  --scope "/subscriptions/b290a724-98ac-4f31-bec6-54bb616b497f" \
  --output table
```

You should see: `allowed-locations-policy` listed.

---

## 🧪 Test the Policy

Try creating a new Azure resource (e.g., Virtual Machine or Storage Account) in any region **other than** `westeurope`.

🛑 It should fail with a policy violation error.

---

## ✅ Output

- ✔️ Policy successfully assigned at the **subscription level**
- ✔️ Resource creation now restricted to **West Europe**
- ✔️ Validated via CLI and Azure Portal

---

## 📌 Notes

- Azure Policy helps ensure governance by enforcing standards across subscriptions.
- Other policies you can try:
  - Require Tags on Resources
  - Restrict VM SKUs
  - Enforce Diagnostic Settings
