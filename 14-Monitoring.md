# Prometheus & Grafana Monitoring Runbook

## Prometheus Architecture Queries (PromQL)

View cluster node CPU utilization percentage across the last 5 minutes:
```promql
100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
```

Identify container memory consumption usage bounds by namespace exclusions:
```promql
sum(container_memory_working_set_bytes{container!=""}) by (namespace)
```

Monitor incoming cluster HTTP request rate frequencies targeting ingress controllers:
```promql
sum(rate(nginx_ingress_controller_requests[5m])) by (status)
```

Identify pods currently trapped or failing due to non-zero exit codes:
```promql
kube_pod_container_status_terminated_reason{reason="OOMKilled"}
```

## Grafana Command Line Interface (grafana-cli)

List all monitoring plugins currently installed on the active Grafana server host:
```bash
grafana-cli plugins ls
```

Install the official companion piechart panel visualization plugin module:
```bash
grafana-cli plugins install grafana-piechart-panel
```

Force an administrative password override reset execution for the local admin account user:
```bash
grafana-cli admin reset-admin-password NewSecurePassword
```

Restart the background runtime service container manager engine to apply structural modifications:
```bash
systemctl restart grafana-server
```

## Kubernetes Monitoring Inspection Utilities

List active Prometheus service endpoints or metric scrape targets inside the monitoring boundary:
```bash
kubectl get svc,pods -n monitoring
```

Forward your local network interface path directly to expose the Grafana server visualization dashboard:
```bash
kubectl port-forward svc/grafana 3000:80 -n monitoring
```

Forward your local network path directly to inspect target state configurations inside the Prometheus expression engine:
```bash
kubectl port-forward svc/prometheus-k8s 9090:9090 -n monitoring
```
