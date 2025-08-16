![IaC](https://img.shields.io/badge/IaC-Databricks%20Asset%20Bundles-8B5CF6?style=flat-square&logo=terraform&logoColor=white)
![Azure DevOps](https://img.shields.io/badge/CI%2FCD-Azure%20DevOps-2563eb?style=flat-square&logo=azuredevops&logoColor=white)
![DLT](https://img.shields.io/badge/Delta%20Live%20Tables-DLT-059669?style=flat-square)
![Unity Catalog](https://img.shields.io/badge/Unity%20Catalog-Ready-6b7280?style=flat-square)
![Security](https://img.shields.io/badge/Security-Service%20Principal-DC2626?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-111827?style=flat-square&logo=open-source-initiative&logoColor=white)
![Author](https://img.shields.io/badge/Kishore%20Kumar%20Nagisetty-Maintainer-ec4899?style=flat-square&logo=github&logoColor=white)



## 📦 Features

- 🧱 **Declarative IaC**: Jobs & DLT pipelines modelled in YAML under `resources/`.
- 🔁 **Environment Promotion**: Single artifact built once, promoted across **DEV → TEST → PROD**.
- 🔐 **Run-as SPN**: All deployments use Azure AD **Service Principal** (non-interactive & secure).
- ✅ **Validation**: `databricks bundle validate` in build; `bundle deploy` in each environment.
- 🧾 **Unity Catalog Ready**: Catalog & schema injected via variables.
- ⚙️ **Autoscaling Clusters**: Node types and min/max workers parameterised.

---

## 📁 Repository Structure
```bash
.
├── resources
│   ├── jobs
│   │   ├── Absence Data.yaml              # Job: Notebook task → DLT task
│   │   └── Absence Spells Test.yaml
│   └── pipelines
│       ├── Absence Data DLT.yaml          # DLT pipeline config
│       └── Absence Spells Test DLT.yaml
├── templates
│   ├── main.yaml                          # Build → DeployToDev → DeployToTest
│   └── deployment.yaml                    # Generic deploy (param: buildEnv)
├── databricks.yml                         # DAB bundle & targets (env vars injected)
├── fixtures/.gitkeep                      # Example snippet for loading CSV fixtures (docs)
└── README.md

⚙️ How It Works
Build (AzDO)
Install Databricks CLI.
Replace placeholders inside databricks.yml with env values from Variable Groups.
databricks bundle validate -t <ENV> to sanity check.
Publish DatabricksBundle artifact.
Deploy (AzDO)
Download artifact and re-inject env values (DEV/TEST/PROD).
az login with Service Principal.
databricks bundle deploy -t <ENV> to create/update Jobs & DLT Pipelines.
Already have objects in the workspace? Bind once
databricks bundle deployment bind -t <env> <resource-name> <existing-id> --auto-approve

Prerequisites
✅ Azure Databricks workspaces for DEV/TEST/PROD
✅ Azure AD Service Principal with workspace access
✅ Azure DevOps Project + Variable Groups per env:
Dab_DEV_Dbw_Variables, Dab_Test_Dbw_Variables, …
✅ Variables defined (per env):
workspaceUrl, deployEnv, prefixNotebookPath, storageAccount, container, folderPath, existingClusterId, DLTClusterNodeType, DLTMinWorkers, DLTMaxWorkers, DLTSchema, catalog, successEmailDL, failureEmailDL, clientid, clientsecret, tenantid
