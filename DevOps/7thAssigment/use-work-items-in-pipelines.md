# Use Work Items in Pipelines

## Objective

Enable traceability between Azure Boards work items and Azure Pipelines, so every build and release is traceable back to why it happened.

## Steps

### 1. Reference Work Items in Commits

Use the work item ID in the commit message:

```bash
git commit -m "Add login validation (#101)"
