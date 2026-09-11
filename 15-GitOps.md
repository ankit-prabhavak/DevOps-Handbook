# ArgoCD CLI for GitOps Deployment Automation

## Authentication & Initial Login

Retrieve the auto-generated initial administrative tracking bootstrap password from the cluster secret storage:
```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 --decode
```

Establish secure local browser access paths straight to the cluster control plane API gateway:
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Authenticate your local terminal workstation shell interface session with the target cluster operator framework:
```bash
argocd login 127.0.0.1:8080 --username admin --password MyDecodedSecretPassword --insecure
```

Update the initial standard administrative password track immediately following the first environment configuration setup:
```bash
argocd account update-password --current-password MyDecodedSecretPassword --new-password MyNewComplexPassword
```

## Repository Management

Register a private Git application storage repository source using HTTPS access credential mappings:
```bash
argocd repo add https://github.com --username gituser --password gittoken
```

Register a private Git infrastructure architecture repository safely via an SSH private identity key profile:
```bash
argocd repo add git@github.com:your-org/gitops-infra.git --ssh-private-key-path ~/.ssh/id_rsa
```

List all operational source code repository tracking endpoints currently registered inside the active controller cluster:
```bash
argocd repo list
```

## Application Lifecycle Operations

Declaratively instantiate a new cluster deployment application profile pointing directly to a specific tracking target branch repository path:
```bash
argocd app create ecommerce-prod --repo https://github.com --path deployment/prod --dest-server https://default.svc --dest-namespace production
```

List the current tracking statuses, sync operational pathways, and synchronization health indexes for all managed applications:
```bash
argocd app list
```

Retrieve multi-tier, structural status maps detailing target health, configuration drift, and resources for an active application configuration:
```bash
argocd app get ecommerce-prod
```

## Synchronization & Drift Mitigation

Force an intentional configuration reconciliation sync execution path targeting an app to overwrite cluster anomalies manually:
```bash
argocd app sync ecommerce-prod
```

Configure automated self-healing reconciliation properties to prevent local cluster manual modifications from mutating infrastructure definitions:
```bash
argocd app set ecommerce-prod --sync-policy automated --auto-prune --self-heal
```

View structural text variations showing lines of configuration drift separating live infrastructure states from desired Git commits:
```bash
argocd app diff ecommerce-prod
```

## Troubleshooting & Rolling Reversions

Roll back an application tracking frame down instantly to an explicit historical commit revision path tracking ID step:
```bash
argocd app rollback ecommerce-prod 4
```

Forcefully purge an operational tracking environment profile framework out of the active cluster namespace completely:
```bash
argocd app delete ecommerce-prod
```
