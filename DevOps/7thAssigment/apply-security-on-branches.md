# Apply Security on Branches

## Objective

Apply security settings on the `master` branch such that:
- **Contributors** can only create **pull requests**
- **Contributors cannot directly push or merge** code into the `master` branch
- Only **project administrators** have full control

## Steps

1. Go to Azure DevOps → Repos → Branches.
2. Click on the **ellipsis (...)** next to the `master` branch and select **Branch security**.
3. Under **Security for master branch**, select the group: `Contributors`.
4. Set the following permissions:
   - `Contribute`: **Deny**
   - `Bypass policies when pushing`: **Not set**
   - `Bypass policies when completing pull requests`: **Not set**
   - `Force push (rewrite history, delete branches and tags)`: **Deny**
   - `Edit policies`: **Not set**
   - `Manage permissions`: **Not set**
5. Make sure `Inheritance` is **enabled**.
6. Save changes.

## Outcome

Contributors can still push code to their own branches and raise pull requests to the master branch, but they **cannot directly merge** changes without administrator approval.
