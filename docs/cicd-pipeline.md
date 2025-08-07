# CI/CD Pipeline

```mermaid
flowchart TD
  Dev[Developer Commits Code]
  PR[Pull Request Created]
  CI[GitHub Actions CI]
  BuildAPI[Build API (.NET or Node)]
  BuildUI[Build UI (Next.js)]
  LintTest[Run Linters & Unit Tests]
  DeployDev[Deploy to Dev Env via IaC]
  ManualApproval[Manual Approval for QA/Prod]
  DeployQA[Deploy to QA]
  DeployProd[Deploy to Prod]

  Dev --> PR --> CI
  CI --> BuildAPI
  CI --> BuildUI
  CI --> LintTest
  LintTest --> DeployDev
  DeployDev --> ManualApproval
  ManualApproval --> DeployQA --> DeployProd
```