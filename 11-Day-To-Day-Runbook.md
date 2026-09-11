# Daily DevOps Engineering Runbook

## Morning Operations & System Health Checks

Verify AWS CLI identity, current session validation, and target active Account ID:
```bash
aws sts get-caller-identity
```

Print the active Kubernetes cluster context profile before running commands:
```bash
kubectl config current-context
```

Inspect all cluster nodes to guarantee they are healthy and in the Ready state:
```bash
kubectl get nodes
```

Scan all namespaces cluster-wide to quickly identify any crashing or evicted pods:
```bash
kubectl get pods -A | grep -v -E "Running|Completed"
```

Audit the availability states and replica targets of all platform deployments:
```bash
kubectl get deployments -A
```

Check for cluster infrastructure warnings or errors generated over the last hour:
```bash
kubectl get events -A --field-selector type=Warning
```

Stream real-time diagnostic output from critical application backend entry points:
```bash
kubectl logs -f pod-name -n production --tail=100
```

Verify local Docker engine health, runtime container states, and port mappings:
```bash
docker ps
```

Clean up dead containers, dangling images, and system build caches on the host machine:
```bash
docker system prune -f
```

Check the local Git workspace status for uncommitted tracking branch deviations:
```bash
git status
```

Fetch and prune remote tracking references to sync branch listings with Azure Repos:
```bash
git fetch --all --prune
```

---

## Production Deployment Checklist
```text
[01. Pull Latest Code]     ──> Git pull origin main / develop to avoid drift.
[02. Validate Infrastructure] ──> Run terraform validate and lint configurations.
[03. Build Container]      ──> Execute docker build with precise release version tags.
[04. Registry Authentication]──> Authenticate local docker engine with AWS ECR target.
[05. Push Image Assets]    ──> Push the built and tagged container images to ECR.
[06. Update Manifest Track]──> Update image tag values inside Helm charts or YAML files.
[07. Apply Manifests]      ──> Run kubectl apply or trigger an ArgoCD/Azure DevOps release.
[08. Verify Pod Rollout]   ──> Monitor rollout status and observe target replica counts.
[09. Audit Live Logs]      ──> Review live streams for connection drops or startup panics.
[10. E2E App Verification] ──> Test application gateway endpoints with curl validation.
```

### Verification Utilities for Deployments

Check rollout progress and verify that the upgrade completes successfully:
```bash
kubectl rollout status deployment/backend-service -n production
```

Verify the HTTP response code and response headers of the live deployment endpoint:
```bash
curl -I https://company.com
```

---

## High-Priority Incident Response Workflow

### Phase 1: Compute Isolation & Evaluation
*   **Is the pod running?** Identify if pods are caught in `CrashLoopBackOff`, `ImagePullBackOff`, or `Pending` cycles.
*   **Are logs clean?** Check stdout and stderr streams for fatal exceptions, syntax issues, or missing variables.
*   **Is system performance normal?** Isolate CPU throttling or Out-Of-Memory (OOM) tracking parameters.

Identify why a non-running pod failed by checking exit codes and error logs:
```bash
kubectl describe pod pod-name -n production
```

Check if containers were terminated due to out-of-memory constraints (OOMKilled):
```bash
kubectl get pods -n production -o jsonpath='{.items[*].status.containerStatuses[*].lastState.terminated.reason}'
```

### Phase 2: Traffic & Routing Validation
*   **Is the service healthy?** Ensure service endpoints are accurately picking up backing pod labels.
*   **Is ingress configured correctly?** Check if SSL/TLS handshakes succeed and host configurations match target specifications.

Confirm that the service mapping has successfully registered active target pod endpoints:
```bash
kubectl get endpoints backend-service -n production
```

### Phase 3: Infrastructure Dependency Checks
*   **Is the database reachable?** Validate cluster networking, security groups, and storage bounds.
*   **Are credentials valid?** Confirm that configuration entries and passwords have not expired.

Test direct database network connectivity from inside an application shell container:
```bash
kubectl exec it pod-name -n production -- nc -zv database-host.internal 5432
```

### Phase 4: Telemetry & Auditing Change Logs
*   **Any active metric alarms?** Check AWS CloudWatch dashboard statuses or platform alerting channels.
*   **Any recent deployment?** Inspect Git tracking files or pipeline execution histories to trace changes.

Identify the last configuration changes applied to the cluster tracking layout:
```bash
kubectl rollout history deployment/backend-service -n production
```
