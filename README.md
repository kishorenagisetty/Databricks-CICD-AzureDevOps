<!-- 👑 AUTHOR BADGE -->
<p align="center">
  <img src="https://img.shields.io/badge/Made%20by-Kishore%20Kumar%20Nagisetty-ff69b4?style=for-the-badge&logo=crown&logoColor=white" alt="Author Badge"/>
</p>

<h1 align="center">🚀 Databricks CI/CD — Jobs & DLT with Azure DevOps (Asset Bundles)</h1>

<p align="center"><strong>100% automated promotion Dev → Test → Prod using Azure DevOps, Databricks Asset Bundles, Unity Catalog & Service Principals 👑</strong></p>

<p align="center">
  <a href="https://www.linkedin.com/in/kishorekumarnagisetty/">
    <img src="https://img.shields.io/badge/LinkedIn-Kishore%20Nagisetty-0A66C2?style=for-the-badge&logo=linkedin" alt="LinkedIn Badge"/>
  </a>
</p>

<p align="center">
  <a href="https://github.com/kishorenagisetty">
    <img src="https://img.shields.io/badge/GitHub-kishorenagisetty-181717?style=for-the-badge&logo=github" alt="GitHub Badge"/>
  </a>
</p>

# 🚀 Databricks CI/CD — Jobs & DLT with Azure DevOps (Asset Bundles)

A fully automated solution to **define & deploy Databricks Jobs/Workflows and Delta Live Tables (DLT)** as code, with environment promotion **DEV → TEST → PROD** using **Azure DevOps Pipelines** and **Databricks Asset Bundles (DAB)**.

![IaC](https://img.shields.io/badge/IaC-Databricks%20Asset%20Bundles-f59e0b?style=for-the-badge)
![Azure DevOps](https://img.shields.io/badge/CI%2FCD-Azure%20DevOps-2563eb?style=for-the-badge&logo=azuredevops)
![DLT](https://img.shields.io/badge/Delta%20Live%20Tables-DLT-10b981?style=for-the-badge)
![Unity Catalog](https://img.shields.io/badge/Unity%20Catalog-Ready-6b7280?style=for-the-badge)
![Security](https://img.shields.io/badge/Security-Service%20Principal-ef4444?style=for-the-badge)
![License: MIT](https://img.shields.io/badge/License-MIT-111827?style=for-the-badge)

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
