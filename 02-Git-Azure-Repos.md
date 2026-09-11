# Git and Azure Repos for DevOps

## Repository Initialisation & Cloning

Clone a repository using its HTTPS or SSH URL:
```bash
git clone repo-url
```

Initialize a new local Git repository in the current directory:
```bash
git init
```

## Branch Management

List all local branches (current branch is highlighted with an asterisk):
```bash
git branch
```

List both local and remote-tracking branches:
```bash
git branch -a
```

Create and immediately switch to a new feature branch:
```bash
git checkout -b feature/login
```

Switch to an existing branch (e.g., develop):
```bash
git checkout develop
```

Safely delete a local branch that has already been merged:
```bash
git branch -d feature/login
```

Force delete a local branch regardless of its merge status:
```bash
git branch -D feature/login
```

## Synchronising with Azure Repos (Remote)

Fetch updates and merge the latest remote changes into your current branch:
```bash
git pull
```

Download latest objects and references from the remote without merging them:
```bash
git fetch --all --prune
```

Push your local commits to the remote repository and set the upstream branch:
```bash
git push -u origin feature/login
```

Push subsequent changes after the upstream branch has already been set:
```bash
git push
```

View configured remote repository URLs:
```bash
git remote -v
```

## Inspecting the Repository Status

Show modified, staged, and untracked files in the working directory:
```bash
git status
```

View the commit history formatted as a clean, single line per commit:
```bash
git log --oneline
```

View the commit history displaying a visual text-based graph of branches:
```bash
git log --oneline --graph --all
```

Show changes between the working directory and the index (staged files):
```bash
git diff
```

Show changes that have been staged for the next commit:
```bash
git diff --staged
```

## Staging & Committing Changes

Stage all modified and new files for the next commit:
```bash
git add .
```

Stage a specific file instead of all changes:
```bash
git add src/app.js
```

Record your staged changes to the repository history with a descriptive message:
```bash
git commit -m "feat: added login feature with validation"
```

Modify the message of the very last local commit:
```bash
git commit --amend -m "feat: updated login feature documentation"
```

## Undoing Changes & Troubleshooting

Discard local changes in a specific file and revert it to the last commit:
```bash
git checkout -- src/app.js
```

Save modified, tracked files to a temporary workspace storage to clean the directory:
```bash
git stash
```

Restore the most recently saved stashed changes back to your working directory:
```bash
git stash pop
```

Unstage a file while keeping its modifications in your working directory:
```bash
git reset HEAD src/app.js
```

Move the current branch tip backward to a specific commit, preserving your working directory changes:
```bash
git reset --soft HEAD~1
```

Forcefully discard all local modifications and commits back to a specific commit (destructive):
```bash
git reset --hard HEAD~1
```

## Azure CLI (az devops) Automation

Install the Azure DevOps extension for the Azure CLI:
```bash
az extension add --name azure-devops
```

Log in to your Azure account via the browser:
```bash
az login
```

Configure default organization and project to avoid passing them in every command:
```bash
az devops configure --defaults organization=https://azure.com project=YourProject
```

List all repositories within the configured project:
```bash
az repo list --output table
```

Create a new Git repository in Azure Repos:
```bash
az repo create --name MyNewRepo
```

Create a new Pull Request to merge feature/login into develop:
```bash
az repo pr create --source-branch feature/login --target-branch develop --title "feat: login implementation" --description "Resolves task 402"
```

List active Pull Requests for the current repository:
```bash
az repo pr list --status active --output table
```

View details and status of a specific Pull Request:
```bash
az repo pr show --id 123
```

Complete and merge an approved Pull Request:
```bash
az repo pr update --id 123 --status completed
```

Abandon and close a Pull Request without merging:
```bash
az repo pr update --id 123 --status abandoned
```

Add a reviewer to an active Pull Request:
```bash
az repo pr reviewer add --id 123 --reviewers engineer@company.com
```

---

## Azure Repos Workflow & Branching Strategy

### Pull Request Flow
```text
[Feature Branch] ──> [Publish to Azure Repos] ──> [Create Pull Request (PR)] ──> [Code Review & Policies Passed] ──> [Merge into Develop/Main]
```

### GitFlow Branch Structure
*   `main` / `master` : Production-ready code only. Tagged with release versions (e.g., v1.0.0).
*   `develop` : Integration branch for features. Main target for daily development.
*   `feature/*` : Isolated branches for new features or user stories. Branched from `develop`.
*   `release/*` : Preparation branches for production releases (bug fixes, documentation). Branched from `develop`.
*   `hotfix/*` : Urgent fixes for production critical bugs. Branched directly from `main` and merged back to both `main` and `develop`.
