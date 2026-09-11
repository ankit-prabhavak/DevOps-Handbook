# Production Troubleshooting Runbook for DevOps

## Pod CrashLoopBackOff & Application Crashes

Inspect pod conditions, lifecycles, exit codes, and recent lifecycle error events:
```bash
kubectl describe pod pod-name
```

Retrieve standard output logs from the current crashing container instance:
```bash
kubectl logs pod-name
```

Fetch application logs from a previous, terminated container instance to locate the panic root cause:
```bash
kubectl logs pod-name --previous
```

Retrieve logs from a specific named container inside a multi-container pod structure:
```bash
kubectl logs pod-name -c container-name
```

## Network Inaccessibility & Routing Failures

List all operational network routing endpoints, target selectors, and virtual cluster IPs:
```bash
kubectl get svc
```

Verify Layer-7 HTTP/HTTPS ingress rules, host mappings, and upstream service bindings:
```bash
kubectl get ingress
```

Inspect detailed ingress annotations, target backends, and controller errors:
```bash
kubectl describe ingress ingress-name
```

Check if internal endpoints exist and match target pod selector criteria correctly:
```bash
kubectl get endpoints service-name
```

Debug live DNS resolution issues natively from a diagnostic network pod:
```bash
kubectl exec -i -t dns-utils -- nslookup service-name.namespace.svc.cluster.local
```

## Kubernetes Node Performance & Allocation Issues

Check cluster-wide node availability, orchestrator version health, and current system states:
```bash
kubectl get nodes
```

Inspect specific node resource capacities, conditions (DiskPressure, MemoryPressure), and system events:
```bash
kubectl describe node node-name
```

List all pods running on a specific node along with their operational limits:
```bash
kubectl get pods -A --field-selector spec.nodeName=node-name -o wide
```

## High CPU & Memory Resource Constraints

Monitor host-level real-time process execution, thread usage, and active system resource consumer loads:
```bash
top
```

Display calculated live CPU and memory metrics consumed across all active pods:
```bash
kubectl top pod
```

Display calculated live CPU and memory metrics consumed across all compute cluster nodes:
```bash
kubectl top node
```

Profile real-time resource allocations for containers inside a specific namespace boundary:
```bash
kubectl top pod -n production --containers
```

## Disk Exhaustion & Persistent Storage Full

Report file system disk space usage and availability across all mounted storage devices:
```bash
df -h
```

Summarize individual storage footprints recursively for all directories inside the working folder:
```bash
du -sh *
```

Sort and identify the top 10 largest individual file payloads inside a directory block:
```bash
find . -type f -exec du -h {} + | sort -rh | head -n 10
```

Inspect persistent volume claim consumption metrics inside the cluster ecosystem:
```bash
kubectl get pvc,pv
```

## Container Initialization Failures & Engine Errors

Extract the operational execution output logs directly from a localized standalone container:
```bash
docker logs container-id
```

Extract complete, low-level structural configuration and status payloads from the engine runtime:
```bash
docker inspect container-id
```

Check structural file system modifications made inside the container's writable storage layer:
```bash
docker diff container-id
```

Query host system kernel diagnostic buffers to uncover underlying out-of-memory (OOM) kills:
```bash
dmesg -T | grep -i -E "oom|kill"
```

## Cluster Event Auditing & Diagnostics

View and list system events sorted sequentially by creation timestamp to isolate errors:
```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

Isolate and filter events explicitly to display runtime structural errors or warnings:
```bash
kubectl get events --field-selector type=Warning
```

Watch the live cluster namespace event log stream in real-time as incidents occur:
```bash
kubectl get events -w --namespace=production
```
