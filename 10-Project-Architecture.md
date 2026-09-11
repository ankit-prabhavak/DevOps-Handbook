# Full Stack EKS Production Architecture Guide

## Enterprise Request Flow Architecture
```text
[Internet User]
       │
       ▼
  [Route 53] ──(Global DNS Resolution)
       │
       ▼
[AWS Load Balancer] ──(ALB / NLB Provisioned by AWS Load Balancer Controller)
       │
       ▼
[Ingress Controller] ──(Layer-7 Reverse Proxy & Path-Based Routing e.g., NGINX Ingress)
       │
       ▼
[Frontend Service] ──(ClusterIP Internal Network Abstraction Layer)
       │
       ▼
 [Frontend Pods] ──(React / Angular / Vue Client-Side Container Application)
       │
       ▼
[Backend Service] ──(ClusterIP Internal Network Abstraction Layer)
       │
       ▼
  [Backend Pods] ──(Node.js / Python / Java API Server Application)
       │
       ▼
   [Database] ──(StatefulSet Database Instance or Managed Amazon RDS Endpoint)
       │
       ▼
[Persistent Volume] ──(AWS EBS / EFS Block Storage Infrastructure Layer)
```

---

## Architecture Supporting Components
*   **Secret**: Encrypted parameters managing database strings, API access tokens, and TLS keys.
*   **ConfigMap**: Externalised environment configuration profiles decoupling properties from runtime engine code.
*   **Horizontal Pod Autoscaler (HPA)**: Automatic compute pod scalability reacting dynamically to real-time metric thresholds.
*   **Persistent Volume Claim (PVC)**: Decoupled cluster storage request layer binding physical cloud disks to application pods.
*   **CloudWatch**: Central tracking platform collecting container logs, engine events, and platform health infrastructure metrics.
*   **SNS**: Cloud messaging notification system broadcasting deployment alarms and infrastructure warnings instantly to engineering channels.

---

## Core Kubernetes Resource Definitions & Verification Commands

### Namespace
Logical runtime boundary isolating multi-tenant architectures, environments, and team access profiles within a shared cluster plane.

List all operational namespace isolation boundaries in the active cluster context:
```bash
kubectl get namespaces
```

### Secret
Secure storage mechanism decoupling passwords, certificates, credentials, and API access tokens safely away from the configuration source control.

View all secrets in the namespace and extract their base64 string values:
```bash
kubectl get secrets
```

### ConfigMap
Key-value pairing database mounting external files, environment settings, and application flags into container file systems non-disruptively.

View configuration profiles and inspect environment configurations loaded into the context:
```bash
kubectl get configmaps
```

### Deployment
Declarative controller tracking replications, running application configurations, self-healing pod lifecycles, and rolling update strategies.

Verify the health, updated instances, and ready status of application deployments:
```bash
kubectl get deployments
```

### Service
Persistent internal load balancing network layer establishing static cluster IP addresses and DNS records across ephemeral pod groups.

List all service endpoints, cluster IP definitions, and active target ports:
```bash
kubectl get services
```

### Ingress
Layer-7 routing configurations implementing domain definitions, SSL/TLS termination, and path mappings to target internal cluster services.

Verify public endpoints, routing annotations, and active ingress rules:
```bash
kubectl get ingress
```

### Persistent Volume Claim (PVC)
Storage lifecycle request matching physical data blocks dynamically to stateful applications to prevent data loss upon pod terminations.

Inspect the active binding status and allocation capacities of persistent storage configurations:
```bash
kubectl get pvc
```

### Horizontal Pod Autoscaler (HPA)
Dynamic cluster metric monitor adjusting pod deployment scaling limits up or down depending on target CPU and memory consumption.

Monitor current scaling target metrics, limits, and calculated replica counts:
```bash
kubectl get hpa
```

### CronJob
Automated orchestrator scheduling cron time expressions to execute point-in-time worker actions, maintenance routines, and database backups.

List all scheduled execution jobs, active historical runs, and next launch targets:
```bash
kubectl get cronjobs
```
