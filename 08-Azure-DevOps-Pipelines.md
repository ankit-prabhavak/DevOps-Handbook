# Azure DevOps & Pipelines for DevOps Engineers

## Core Platform Components
*   **Azure Repos**: Private Git repositories providing code hosting, version control, and Pull Request workflows.
*   **Azure Boards**: Agile planning and project management tracking using Kanban boards, backlogs, and sprints.
*   **Azure Pipelines**: Cloud-hosted multi-platform CI/CD automation engine supporting both YAML configurations and classic GUIs.
*   **Azure Artifacts**: Universal package management store for hosting and sharing NPM, NuGet, Maven, Python, and universal feeds.
*   **Azure Test Plans**: Manual, exploratory, and continuous cloud-based software testing toolset.

---

## Standard Cloud-Native CI/CD Flow
```text
[Developer Write Code] ──> [Commit & PR to Repo] ──> [Build & Lint Application] ──> [Run Unit & Integration Tests] ──> [Docker Build Container] ──> [Push Image to Registry (ACR/ECR)] ──> [Deploy to Environment (AKS/EKS/Web App)]
```

---

## Modular Multi-Stage Pipeline Blueprint
```yaml
trigger:
  batch: true
  branches:
    include:
    - main
    - develop

pool:
  vmImage: 'ubuntu-latest'

variables:
  - name: buildConfiguration
    value: 'Release'
  - name: dockerRegistryServiceConnection
    value: 'azure-acr-service-connection'
  - name: imageRepository
    value: 'myapp'

stages:
- stage: BuildAndTest
  displayName: 'Build and Test Stage'
  jobs:
  - job: CompileCode
    displayName: 'Compile and Unit Test'
    steps:
    - script: echo "Starting source compilation on \$(buildConfiguration) mode..."
      displayName: 'Initialize Compilation'

    - script: |
        echo "Running application test suites..."
        npm run test -- --watch=false
      displayName: 'Execute Automated Tests'

- stage: BakeAndPushImage
  displayName: 'Containerization Stage'
  dependsOn: BuildAndTest
  condition: succeeded()
  jobs:
  - job: DockerBuild
    displayName: 'Docker Build and Push'
    steps:
    - task: Docker@2
      displayName: 'Build and Push Docker Image to Registry'
      inputs:
        command: 'buildAndPush'
        containerRegistry: '\$(dockerRegistryServiceConnection)'
        repository: '\$(imageRepository)'
        dockerfile: '\$(Build.SourcesDirectory)/Dockerfile'
        tags: |
          \$(Build.BuildId)
          latest
```

---

## Architecture Blueprint Concepts
*   **Trigger**: Event condition constraints (code commits, pull requests, scheduled crons) telling a pipeline exactly when to execute.
*   **Agent Pool**: Orchestrated machine host groups (Microsoft-hosted in the cloud or self-hosted in private networks) running the build steps.
*   **Stage**: Cohesive group of isolation structures (Build, Test, Staging, Production) marking logical release phases.
*   **Job**: Array of targeted instruction boundaries assigned to a single agent runner machine executing sequentially.
*   **Step**: Atomic building blocks representing scripts, tasks, or manual custom terminal commands wrapped in code.
*   **Variables**: Key-value data injection points allowing engineers to pass configuration flags into build layers.
*   **Artifacts**: Extracted structural output files (binaries, ZIPs, compiled code packs) passed across stages or stored for references.
*   **Environments**: Collections of targets (Kubernetes clusters, Virtual Machines) where specific application steps can be deployed.
*   **Approvals**: Deployment gates enforcing strict manual structural sign-offs before a stage is allowed to run in high-security environments.

---

## Azure CLI & DevOps Workspace Control

Log in securely to your active Azure Cloud subscription via browser integration:
```bash
az login
```

List all Azure Cloud account subscriptions attached to your identity:
```bash
az account list --output table
```

Display full metadata parameters for the currently active Azure subscription profile:
```bash
az account show
```

Set a specific target subscription context for subsequent operations:
```bash
az account set --subscription "My-Production-Subscription"
```

Add the proprietary DevOps management extension pack directly to the Azure CLI engine:
```bash
az extension add --name azure-devops
```

Configure standard default properties to minimize parameter redundancy across CLI targets:
```bash
az devops configure --defaults organization=https://azure.com project=MyProject
```

Trigger an immediate run execution sequence on a specific target pipeline blueprint ID:
```bash
az pipelines run --id 42 --output table
```

Monitor the operational execution runtime status details of a targeted running pipeline build execution:
```bash
az pipelines build show --id 1024 --output table
```
