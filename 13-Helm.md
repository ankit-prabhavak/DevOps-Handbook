# Helm CLI for Kubernetes Package Management

## Repository Management

Add a trusted third-party Helm chart registry repository:
```bash
helm repo add bitnami https://bitnami.com
```

Fetch and update the local cache of available charts from all added repositories:
```bash
helm repo update
```

Search all added repositories for a specific application chart matching a keyword:
```bash
helm search repo nginx
```

## Application Releases (Deployments)

Install a chart or upgrade an existing release safely using custom configuration variables:
```bash
helm upgrade --install my-release bitnami/nginx --values values-prod.yaml
```

Install a chart while overriding specific configurations inline via the command line:
```bash
helm install my-db bitnami/postgresql --set auth.database=prod_db,auth.username=admin
```

List all active, failed, or pending Helm chart releases in the current namespace:
```bash
helm list
```

List all chart releases deployed cluster-wide across every single namespace:
```bash
helm list -A
```

Uninstall a release and clean up all of its managed Kubernetes infrastructure footprints:
```bash
helm uninstall my-release
```

## Rollbacks & History Tracking

View the sequential deployment history and revision tracking records of a release:
```bash
helm history my-release
```

Instantly roll back an application deployment to a specific historical revision number:
```bash
helm rollback my-release 2
```

## Chart Development & Quality Control

Scaffold a structured base directory template for engineering a custom Helm chart:
```bash
helm create my-custom-chart
```

Parse and evaluate a chart's syntax issues to ensure it adheres to packaging standards:
```bash
helm lint ./my-custom-chart
```

Render chart templates locally with variables injected to preview the generated YAML manifests:
```bash
helm template my-release ./my-custom-chart --values values.yaml
```
