# Kubernetes CLI (kubectl) for DevOps

## Cluster Architecture & Node Context

List all nodes present in the cluster along with status and roles:
```bash
kubectl get nodes
```

Display detailed information about cluster master components and core system services:
```bash
kubectl cluster-info
```

Show current context info, API server endpoint configuration, and active users:
```bash
kubectl config view
```

Switch your active terminal shell context to a different cluster profile:
```bash
kubectl config use-context production-cluster
```

## Namespaces

List all configuration boundaries and isolated virtual environments in the cluster:
```bash
kubectl get ns
```

Create a new namespace boundary to isolate resources:
```bash
kubectl create namespace dev
```

Dynamically change the active default namespace context for subsequent commands:
```bash
kubectl config set-context --current --namespace=dev
```

## Pod Lifecycle & Inspection

List all working pods located in the current default namespace boundary:
```bash
kubectl get pods
```

List all pods cluster-wide across every single namespace boundary:
```bash
kubectl get pods -A
```

List pods with expanded details including individual pod IP allocations and host node locations:
```bash
kubectl get pods -o wide
```

Stream pod updates live and watch state transitions as they occur inside the cluster:
```bash
kubectl get pods -w
```

Filter and extract specific structural fields using advanced JSONPath querying:
```bash
kubectl get pods -o jsonpath='{.items[*].metadata.name}'
```

## Troubleshooting & Diagnosing Pods

`kubectl logs` configurations:
```bash
kubectl logs pod-name
```
```bash
kubectl logs -f pod-name
```
```bash
kubectl logs pod-name -c application-container
```
```bash
kubectl logs pod-name --previous
```

Display verbose, low-level engine details, environmental states, lifecycle events, and conditions:
```bash
kubectl describe pod pod-name
```

## Internal Execution & Debugging

Open an interactive terminal container inside a running pod using Bash:
```bash
kubectl exec -it pod-name -- bash
```

Target and log in to a specific container within a multi-container pod structure:
```bash
kubectl exec -it pod-name -c application-container -- sh
```

Forward a local network port directly to an application container endpoint for local debugging:
```bash
kubectl port-forward pod-name 8080:80
```

## Deployments & Declarations

List all active state management configurations across the current namespace:
```bash
kubectl get deployment
```

Declaratively create or update cluster resources defined inside a structured YAML file:
```bash
kubectl apply -f deployment.yaml
```

Remove and clean up a managed state footprint from the cluster architecture:
```bash
kubectl delete deployment app
```

Manually adjust horizontal replica limits up or down on the fly:
```bash
kubectl scale deployment app --replicas=5
```

## Release Rollouts & Revision Strategies

Monitor the live integration health and progress state of a triggered release update:
```bash
kubectl rollout status deployment app
```

Trigger an immediate restart of all underlying containers across an entire application layer:
```bash
kubectl rollout restart deployment app
```

View the linear list of past deployment release updates tracked inside the control plane:
```bash
kubectl rollout history deployment app
```

Roll back the active application state instantly to the previous recorded healthy step:
```bash
kubectl rollout undo deployment app
```

Revert the current application back to a specific version number from the recorded history track:
```bash
kubectl rollout undo deployment app --to-revision=2
```

## Networking & Services

List all network routing profiles, virtual IPs, and active services:
```bash
kubectl get svc
```

Inspect routing pathways, configuration bindings, target selectors, and healthy backend pods:
```bash
kubectl describe svc app-service
```

List proxy routing paths and layer-7 ingress rules mapping domain traffic to endpoints:
```bash
kubectl get ingress
```

## Configuration Data & App Properties

List all environment configuration data structures stored in the namespace:
```bash
kubectl get configmap
```

Generate a new decoupled application property payload using a directory file source:
```bash
kubectl create configmap app-config --from-file=config.properties
```

## Secrets Management

List all sensitive configuration entries and credentials:
```bash
kubectl get secrets
```

Create an encrypted string key-value reference securely inside the storage boundary:
```bash
kubectl create secret generic db-secret --from-literal=username=admin --from-literal=password=password
```

Retrieve a secret payload and completely decode its base64 string back into readable plain-text:
```bash
kubectl get secret db-secret -o jsonpath='{.data.password}' | base64 --decode
```

## Cluster Activity & Events

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

## Resource Cleanup

Wipe out all stale or unassigned cluster resources by executing an active manifest removal:
```bash
kubectl delete -f deployment.yaml
```

Delete all resource types matching a single configuration label flag:
```bash
kubectl delete pods,services -l app=old-version
```
