
# 🚀 Pushing Code to Azure DevOps Repository (`ProjectX`)

This guide walks you through the exact steps to push your local code to an Azure DevOps Git repository, including resolving common errors.

---

## ✅ Prerequisites

- You have an Azure DevOps organization (e.g., `prince-org`)
- You have created a project (e.g., `ProjectX`)
- You have a repo created at:
  ```
  https://dev.azure.com/prince-org/ProjectX/_git/ProjectX
  ```
- Git is installed on your system.

---

## 🧩 Step-by-Step Git Commands

### 1. Open terminal in your project folder
Example:
```bash
cd "D:/VScode/Advance Projects/DevOpsApp"
```

### 2. Initialize Git (if not already)
```bash
git init
```

### 3. Create a `.gitignore` file
Create a `.gitignore` file with:
```gitignore
node_modules/
.next/
.env
.DS_Store
.vscode/
.idea/
*.log
```

Then run:
```bash
git add .gitignore
git commit -m "Add .gitignore"
```

### 4. Add Azure DevOps as the remote origin
```bash
git remote remove origin   # Optional, if origin already exists
git remote add origin https://prince-org@dev.azure.com/prince-org/ProjectX/_git/ProjectX
```

### 5. Add all files and commit
```bash
git add .
git commit -m "Initial commit"
```

### 6. Set your branch to `master`
```bash
git branch -M master
```

---

## 🛑 If You See Error: "rejected: fetch first"

Run:
```bash
git pull --rebase origin master
```

Then:
```bash
git push -u origin master
```

✅ This will successfully push your code without overwriting existing remote files (like README.md).

---

## 🔐 Authentication Note

If prompted for username and password:
- Username: your Azure email (e.g., princedayma230@gmail.com)
- Password: Use a [Personal Access Token (PAT)](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate)

---

Happy Coding! 🎉
