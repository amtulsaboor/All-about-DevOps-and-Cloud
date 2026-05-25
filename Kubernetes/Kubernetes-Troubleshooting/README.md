# Kubernetes Troubleshooting and Production Debugging

# Introduction

Kubernetes troubleshooting is a critical skill for:
- DevOps Engineers
- Site Reliability Engineers
- Platform Engineers
- Cloud Engineers

Production Kubernetes clusters fail because of:
- pod crashes
- networking issues
- DNS failures
- node failures
- ingress issues
- storage failures
- autoscaling issues
- container runtime failures

Strong troubleshooting skills are essential in production environments.

---

# Kubernetes Troubleshooting Workflow

A good Kubernetes engineer:
1. identifies symptoms
2. checks cluster health
3. investigates logs
4. analyzes events
5. identifies root cause
6. applies fix
7. prevents recurrence

---

# Kubernetes Architecture Components

| Component | Purpose |
|---|---|
| API Server | cluster communication |
| Scheduler | assigns pods |
| Controller Manager | maintains desired state |
| kubelet | manages pods on nodes |
| etcd | cluster database |
| CoreDNS | DNS resolution |
| kube-proxy | networking |

---

# Cluster Health Checks

# View Cluster Nodes

Purpose:
- checks node status

Command:

```bash
kubectl get nodes
```

---

# Detailed Node Information

Purpose:
- investigates node issues

Command:

```bash
kubectl describe node NODE_NAME
```

---

# Cluster Events

Purpose:
- identifies failures and warnings

Command:

```bash
kubectl get events -A
```

---

# Kubernetes API Health

Purpose:
- verifies API server

Command:

```bash
kubectl cluster-info
```

---

# Pod Troubleshooting

Pods commonly fail because of:
- application crashes
- image pull failures
- missing secrets
- insufficient resources

---

# View Pods

Purpose:
- checks pod status

Command:

```bash
kubectl get pods -A
```

---

# Describe Pod

Purpose:
- detailed pod investigation

Command:

```bash
kubectl describe pod POD_NAME
```

---

# Pod Logs

Purpose:
- application troubleshooting

Command:

```bash
kubectl logs POD_NAME
```

---

# Previous Container Logs

Purpose:
- investigates restarted containers

Command:

```bash
kubectl logs POD_NAME --previous
```

---

# Enter Running Pod

Purpose:
- interactive debugging

Command:

```bash
kubectl exec -it POD_NAME -- bash
```

---

# CrashLoopBackOff Troubleshooting

CrashLoopBackOff means:
- container repeatedly crashing

---

# Common Causes

- application crash
- missing environment variable
- database connectivity failure
- insufficient memory
- invalid startup command

---

# Investigation Workflow

Commands:

```bash
kubectl describe pod POD_NAME
kubectl logs POD_NAME
kubectl logs POD_NAME --previous
```

---

# ImagePullBackOff Troubleshooting

ImagePullBackOff means:
- Kubernetes cannot pull image

---

# Common Causes

- wrong image name
- invalid tag
- registry authentication issue
- network problem

---

# Verify Image

Purpose:
- checks deployment image

Command:

```bash
kubectl describe pod POD_NAME
```

---

# Kubernetes Networking Troubleshooting

Networking is one of the most difficult Kubernetes areas.

---

# View Services

Purpose:
- checks service configuration

Command:

```bash
kubectl get svc -A
```

---

# Describe Service

Purpose:
- detailed service investigation

Command:

```bash
kubectl describe svc SERVICE_NAME
```

---

# Test Service Connectivity

Purpose:
- verifies internal communication

Command:

```bash
kubectl exec -it POD_NAME -- curl SERVICE_NAME
```

---

# Check Endpoints

Purpose:
- verifies backend pod mapping

Command:

```bash
kubectl get endpoints
```

---

# DNS Troubleshooting

Kubernetes DNS commonly fails because of:
- CoreDNS issues
- network policies
- kube-proxy failures

---

# Verify DNS Resolution

Purpose:
- tests Kubernetes DNS

Command:

```bash
kubectl exec -it POD_NAME -- nslookup kubernetes.default
```

---

# CoreDNS Pods

Purpose:
- verifies DNS services

Command:

```bash
kubectl get pods -n kube-system
```

---

# CoreDNS Logs

Purpose:
- investigates DNS issues

Command:

```bash
kubectl logs -n kube-system COREDNS_POD
```

---

# Ingress Troubleshooting

Ingress issues commonly involve:
- wrong routing
- TLS failures
- ingress controller problems

---

# View Ingress Resources

Purpose:
- checks ingress rules

Command:

```bash
kubectl get ingress -A
```

---

# Describe Ingress

Purpose:
- detailed ingress investigation

Command:

```bash
kubectl describe ingress INGRESS_NAME
```

---

# Verify Ingress Controller

Purpose:
- checks ingress controller health

Command:

```bash
kubectl get pods -n ingress-nginx
```

---

# Storage Troubleshooting

Storage issues cause:
- pod startup failures
- database outages

---

# View Persistent Volumes

Purpose:
- checks storage resources

Command:

```bash
kubectl get pv
```

---

# View Persistent Volume Claims

Purpose:
- verifies storage claims

Command:

```bash
kubectl get pvc
```

---

# Describe PVC

Purpose:
- storage issue investigation

Command:

```bash
kubectl describe pvc PVC_NAME
```

---

# Resource Troubleshooting

---

# Node Resource Usage

Purpose:
- identifies overloaded nodes

Command:

```bash
kubectl top nodes
```

---

# Pod Resource Usage

Purpose:
- identifies heavy workloads

Command:

```bash
kubectl top pods
```

---

# Autoscaling Troubleshooting

---

# View HPA

Purpose:
- checks autoscaler status

Command:

```bash
kubectl get hpa
```

---

# Describe HPA

Purpose:
- investigates scaling issues

Command:

```bash
kubectl describe hpa HPA_NAME
```

---

# etcd Troubleshooting

etcd stores:
- Kubernetes cluster state

etcd issues can break entire cluster.

---

# etcd Health Check

Purpose:
- verifies etcd health

Command:

```bash
etcdctl endpoint health
```

---

# View etcd Members

Purpose:
- checks cluster members

Command:

```bash
etcdctl member list
```

---

# Kubernetes Node Troubleshooting

Node failures commonly involve:
- kubelet failure
- disk exhaustion
- container runtime issue

---

# Check kubelet Status

Purpose:
- verifies node agent

Command:

```bash
systemctl status kubelet
```

---

# kubelet Logs

Purpose:
- investigates node issues

Command:

```bash
journalctl -u kubelet
```

---

# Container Runtime Status

Purpose:
- verifies container runtime

Command:

```bash
systemctl status containerd
```

---

# Production Incident Workflow

# Step 1 — Identify Symptoms

Examples:
- pods crashing
- ingress unavailable
- application downtime

---

# Step 2 — Verify Cluster Health

Commands:

```bash
kubectl get nodes
kubectl get pods -A
```

---

# Step 3 — Investigate Events

Command:

```bash
kubectl get events -A
```

---

# Step 4 — Check Logs

Commands:

```bash
kubectl logs
journalctl -u kubelet
```

---

# Step 5 — Verify Networking

Commands:

```bash
kubectl get svc
kubectl get endpoints
```

---

# Step 6 — Verify Resources

Commands:

```bash
kubectl top nodes
kubectl top pods
```

---

# Step 7 — Identify Root Cause

Examples:
- memory exhaustion
- DNS failure
- image pull issue
- storage issue

---

# Step 8 — Apply Fix

Examples:
- restart deployment
- scale nodes
- update secrets
- rollback deployment

---

# Step 9 — Prevent Recurrence

Examples:
- monitoring
- alerting
- autoscaling
- better resource limits

---

# 100 Most Used Kubernetes Troubleshooting Commands

| Command | Purpose |
|---|---|
| kubectl get pods | list pods |
| kubectl get pods -A | all namespaces |
| kubectl describe pod | pod details |
| kubectl logs | pod logs |
| kubectl logs --previous | previous logs |
| kubectl exec -it | pod shell |
| kubectl get nodes | node status |
| kubectl describe node | node details |
| kubectl top nodes | node metrics |
| kubectl top pods | pod metrics |
| kubectl get svc | services |
| kubectl describe svc | service details |
| kubectl get ingress | ingress resources |
| kubectl describe ingress | ingress details |
| kubectl get endpoints | service endpoints |
| kubectl get events | cluster events |
| kubectl get pv | persistent volumes |
| kubectl get pvc | persistent claims |
| kubectl describe pvc | PVC details |
| kubectl get hpa | autoscalers |
| kubectl describe hpa | HPA details |
| kubectl get deployments | deployments |
| kubectl rollout status | rollout health |
| kubectl rollout undo | rollback |
| kubectl delete pod | restart pod |
| kubectl scale deployment | scale workload |
| kubectl apply -f | apply manifest |
| kubectl delete -f | delete manifest |
| kubectl edit deployment | edit deployment |
| kubectl cordon node | mark unschedulable |
| kubectl drain node | evacuate workloads |
| kubectl uncordon node | enable scheduling |
| kubectl cluster-info | cluster details |
| kubectl api-resources | API resources |
| kubectl api-versions | API versions |
| kubectl auth can-i | RBAC test |
| kubectl get secrets | secrets |
| kubectl describe secret | secret details |
| kubectl get configmap | configmaps |
| kubectl describe configmap | config details |
| kubectl get namespaces | namespaces |
| kubectl describe namespace | namespace details |
| kubectl get daemonsets | daemonsets |
| kubectl get statefulsets | statefulsets |
| kubectl get jobs | jobs |
| kubectl get cronjobs | cron jobs |
| kubectl cp | copy files |
| kubectl port-forward | local forwarding |
| helm list | Helm releases |
| helm history | release history |
| helm rollback | rollback release |
| helm upgrade | upgrade release |
| docker ps | containers |
| docker logs | container logs |
| crictl ps | container runtime |
| crictl logs | runtime logs |
| systemctl status kubelet | kubelet status |
| journalctl -u kubelet | kubelet logs |
| systemctl status containerd | runtime status |
| journalctl -u containerd | runtime logs |
| etcdctl endpoint health | etcd health |
| etcdctl member list | etcd members |
| curl | API testing |
| ping | connectivity |
| dig | DNS lookup |
| nslookup | DNS resolution |
| traceroute | route tracing |
| tcpdump | packet capture |
| ss -tulpn | listening ports |
| netstat -tulpn | port details |
| top | CPU usage |
| htop | process monitoring |
| free -h | memory usage |
| vmstat | memory stats |
| iostat | disk I/O |
| df -h | disk usage |
| du -sh | directory size |
| lsof | open files |
| ps -ef | process list |
| pstree | process tree |
| grep | log search |
| awk | text processing |
| sed | stream editing |
| vim | edit configs |
| cat | view files |
| less | paginated view |
| tail -f | follow logs |
| find | locate files |
| tar -xvf | extract files |
| ssh | remote access |
| scp | secure copy |
| rsync | file sync |
| uptime | system load |
| whoami | current user |
| id | user details |
| chmod | permissions |
| chown | ownership |
| env | environment variables |
| export | export variable |
| history | command history |
| crontab -l | cron jobs |
| mount | mounted disks |
| lsblk | block devices |
| fdisk -l | partitions |
| uname -a | kernel details |

---

# Real World Production Scenarios

# Scenario 1 — Pods Stuck in Pending

Possible Causes:
- insufficient resources
- node taints
- PVC unavailable

Investigation:

```bash
kubectl describe pod POD_NAME
```

---

# Scenario 2 — CrashLoopBackOff

Investigation:

```bash
kubectl logs POD_NAME
kubectl logs POD_NAME --previous
```

---

# Scenario 3 — Kubernetes DNS Failure

Symptoms:
- services unreachable

Investigation:

```bash
kubectl exec -it POD_NAME -- nslookup kubernetes.default
```

---

# Scenario 4 — Ingress Not Working

Investigation:

```bash
kubectl describe ingress INGRESS_NAME
kubectl get pods -n ingress-nginx
```

---

# Scenario 5 — Node NotReady

Investigation:

```bash
systemctl status kubelet
journalctl -u kubelet
```

---

# Scenario 6 — High CPU Usage in Cluster

Investigation:

```bash
kubectl top nodes
kubectl top pods
```

---

# Root Cause Analysis (RCA)

A good Kubernetes RCA includes:
- incident timeline
- affected workloads
- root cause
- resolution
- prevention strategy

---

# Kubernetes Troubleshooting Best Practices

- implement monitoring
- use centralized logging
- define resource limits
- implement autoscaling
- secure clusters
- test disaster recovery
- backup etcd

---

# 50 Kubernetes Troubleshooting Interview Questions

## Beginner

1. What is CrashLoopBackOff?
2. What is ImagePullBackOff?
3. What is Kubernetes DNS?
4. What is CoreDNS?
5. What is kubelet?
6. What is etcd?
7. What is ingress?
8. What is service discovery?
9. What is HPA?
10. What is persistent volume?

---

## Intermediate

11. Explain Kubernetes pod lifecycle.
12. Difference between Deployment and StatefulSet?
13. Explain Kubernetes networking.
14. What causes pod restarts?
15. Explain kube-proxy.
16. What is node pressure?
17. Explain Kubernetes events.
18. What is taint and toleration?
19. Explain ingress controller.
20. What is resource quota?

---

## Advanced

21. Explain etcd internals.
22. What is CNI?
23. Explain Kubernetes scheduler.
24. What is container runtime interface?
25. Explain kubelet architecture.
26. What is service mesh?
27. Explain admission controllers.
28. What is Kubernetes API aggregation?
29. Explain cluster autoscaler.
30. What is pod eviction?

---

## Production Based

31. Pod CrashLoopBackOff investigation.
32. Kubernetes DNS outage handling.
33. Ingress production debugging.
34. etcd failure investigation.
35. Kubernetes node NotReady troubleshooting.
36. High CPU cluster debugging.
37. PVC mount failure handling.
38. Image pull failure investigation.
39. Kubernetes networking troubleshooting.
40. Production outage response workflow.

---

## Scenario Based

41. Entire cluster inaccessible.
42. Pods stuck in Pending.
43. Node disk full.
44. Ingress returning 502 errors.
45. DNS resolution failing across cluster.
46. HPA not scaling pods.
47. Kubernetes API extremely slow.
48. Worker nodes disconnected.
49. etcd corruption scenario.
50. Explain your Kubernetes production debugging workflow.

---

# Summary

Kubernetes troubleshooting is one of the most critical modern DevOps skills.

Strong Kubernetes debugging skills are essential for:
- cloud-native operations
- production reliability
- incident response
- platform engineering
- SRE workflows

Senior DevOps engineers spend significant time:
- debugging clusters
- investigating outages
- analyzing logs
- optimizing workloads
- improving cluster reliability
