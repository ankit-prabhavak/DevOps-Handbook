# Terraform CLI for Infrastructure as Code (IaC)

## Workflow Initialization

Initialize a new or existing Terraform working directory by downloading providers and modules:
```bash
terraform init
```

Upgrade all installed providers and modules to the latest allowed versions:
```bash
terraform init -upgrade
```

## Validation & Code Quality

Check whether the configuration files are syntactically valid and internally consistent:
```bash
terraform validate
```

Automatically rewrite Terraform configuration files to follow canonical formatting standards:
```bash
terraform fmt
```

Check if the configuration files are formatted correctly without rewriting them:
```bash
terraform fmt -check
```

## Planning & Execution Previews

Create an execution plan to preview the changes Terraform will make to your infrastructure:
```bash
terraform plan
```

Generate and save an execution plan to an external file to guarantee the exact same plan runs later:
```bash
terraform plan -out=tfplan
```

Generate a plan focused exclusively on showing what would happen if the infrastructure were destroyed:
```bash
terraform plan -destroy
```

## Applying Infrastructure Changes

Create or update infrastructure according to the configuration files (requires manual approval):
```bash
terraform apply
```

Apply a previously saved and verified execution plan file instantly without prompting for confirmation:
```bash
terraform apply tfplan
```

Apply configuration modifications automatically without asking for user confirmation (use with caution):
```bash
terraform apply -auto-approve
```

Update specific resource targets selectively without affecting the rest of the infrastructure tree:
```bash
terraform apply -target=aws_instance.web_server
```

## Destroying Infrastructure

Delete all infrastructure resources managed by the current Terraform configuration:
```bash
terraform destroy
```

Forcefully delete all managed infrastructure without waiting for a confirmation prompt:
```bash
terraform destroy -auto-approve
```

## State Management & Inspection

Provide human-readable output from a state file or an execution plan file:
```bash
terraform show
```

List all infrastructure resources currently tracked inside the active state file:
```bash
terraform state list
```

Show detailed internal metadata attributes for a specific resource tracked in the state file:
```bash
terraform state show aws_instance.web_server
```

Remove a resource completely from the state file without deleting the actual cloud asset:
```bash
terraform state rm aws_instance.web_server
```

Import an existing real-world cloud infrastructure asset into your local Terraform state file:
```bash
terraform import aws_instance.web_server i-0123456789abcdef0
```

## Output & Workspace Utilities

Extract and view the value of root-level output variables configured in the deployment:
```bash
terraform output
```

Extract the value of a specific named output variable in a clean format for scripting:
```bash
terraform output -json db_connection_string
```

List all operational isolation workspaces configured within the state directory:
```bash
terraform workspace list
```

Switch the active context to a different isolated environment workspace:
```bash
terraform workspace select production
```
```text
[Write/Edit .tf Files] ──> [terraform init] ──> [terraform validate] ──> [terraform plan] ──> [terraform apply]
```
