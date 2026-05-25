# Kubernetes for DevOps Engineers

# Introduction

Kubernetes is a container orchestration platform used to automate:
- deployment
- scaling
- networking
- monitoring
- self-healing

Kubernetes manages containerized applications at enterprise scale.

Most modern cloud-native applications use Kubernetes.

---

# Why Kubernetes?

Before Kubernetes:
- manual deployments
- scaling difficulties
- downtime during releases
- infrastructure inconsistency

Kubernetes solves:
- automatic scaling
- self-healing
- service discovery
- rolling updates
- workload orchestration

---

# Kubernetes Architecture

Kubernetes consists of:

# Control Plane Components

| Component | Purpose |
|---|---|
| API Server | Main communication layer |
| Scheduler | Assigns pods to nodes |
| Controller Manager | Maintains desired state |
| etcd | Stores cluster data |

---

# Worker Node Components

| Component | Purpose |
|---|---|
| kubelet | Node agent |
| kube-proxy | Networking |
| Container Runtime | Runs containers |

---

# Kubernetes Cluster Flow

1. User sends request
2. API server receives request
3. etcd stores cluster state
4. Scheduler selects node
5. kubelet creates pod

---

# Install kubectl

Purpose:
- command line tool to manage Kubernetes cluster

Command:

```bash
sudo snap install kubectl --classic
```

---

# Verify kubectl

Purpose:
- checks kubectl installation

Command:

```bash
kubectl version --client
```

---

# Check Cluster Information

Purpose:
- displays cluster details

Command:

```bash
kubectl cluster-info
```

---

# Check Nodes

Purpose:
- displays worker and master nodes

Command:

```bash
kubectl get nodes
```

---

# Pods

Pods are the smallest deployable units in Kubernetes.

A pod can contain:
- one container
- multiple containers

---

# Create Pod YAML

Purpose:
- defines pod configuration

Command:

```bash
vim pod.yml
```

Example:

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
    - name: nginx
      image: nginx
```

---

# Create Pod

Purpose:
- creates pod in cluster

Command:

```bash
kubectl apply -f pod.yml
```

---

# View Pods

Purpose:
- lists running pods

Command:

```bash
kubectl get pods
```

---

# Detailed Pod Information

Purpose:
- displays pod IP, node, events, container details

Command:

```bash
kubectl describe pod nginx-pod
```

---

# Pod Logs

Purpose:
- checks application logs

Command:

```bash
kubectl logs nginx-pod
```

---

# Access Pod Shell

Purpose:
- opens terminal inside pod

Command:

```bash
kubectl exec -it nginx-pod -- bash
```

---

# Delete Pod

Purpose:
- removes pod from cluster

Command:

```bash
kubectl delete pod nginx-pod
```

---

# Deployments

Deployments manage:
- replica scaling
- rolling updates
- self-healing

---

# Create Deployment YAML

Purpose:
- defines deployment configuration

Command:

```bash
vim deployment.yml
```

Example:

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 2

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
      - name: nginx
        image: nginx
```

---

# Create Deployment

Purpose:
- deploys replicated application

Command:

```bash
kubectl apply -f deployment.yml
```

---

# View Deployments

Purpose:
- displays deployments

Command:

```bash
kubectl get deployments
```

---

# Scale Deployment

Purpose:
- increases or decreases pod replicas

Command:

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

---

# Rolling Update

Purpose:
- updates application without downtime

Command:

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:latest
```

---

# Rollback Deployment

Purpose:
- restores previous version

Command:

```bash
kubectl rollout undo deployment nginx-deployment
```

---

# Services

Services expose applications.

Types:
- ClusterIP
- NodePort
- LoadBalancer

---

# Create Service

Purpose:
- exposes deployment internally or externally

Command:

```bash
kubectl expose deployment nginx-deployment --port=80 --type=NodePort
```

---

# View Services

Purpose:
- displays services

Command:

```bash
kubectl get svc
```

---

# Namespaces

Namespaces isolate resources.

---

# Create Namespace

Purpose:
- creates isolated environment

Command:

```bash
kubectl create namespace dev
```

---

# View Namespaces

Purpose:
- lists namespaces

Command:

```bash
kubectl get ns
```

---

# ConfigMaps

ConfigMaps store configuration data.

---

# Create ConfigMap

Purpose:
- stores environment configuration

Command:

```bash
kubectl create configmap app-config --from-literal=ENV=prod
```

---

# Secrets

Secrets store sensitive data.

---

# Create Secret

Purpose:
- securely stores passwords and keys

Command:

```bash
kubectl create secret generic db-secret --from-literal=password=admin123
```

---

# Persistent Volumes

Persistent Volumes provide durable storage.

---

# View Persistent Volumes

Purpose:
- displays cluster storage volumes

Command:

```bash
kubectl get pv
```

---

# View Persistent Volume Claims

Purpose:
- displays requested storage

Command:

```bash
kubectl get pvc
```

---

# Ingress

Ingress manages external traffic routing.

---

# View Ingress

Purpose:
- displays ingress resources

Command:

```bash
kubectl get ingress
```

---

# RBAC

RBAC controls permissions.

---

# View Roles

Purpose:
- displays RBAC roles

Command:

```bash
kubectl get roles
```

---

# Helm

Helm is Kubernetes package manager.

---

# Install Helm

Purpose:
- installs Helm package manager

Command:

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

---

# Add Helm Repo

Purpose:
- adds chart repository

Command:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

---

# Install Helm Chart

Purpose:
- deploys packaged applications

Command:

```bash
helm install nginx bitnami/nginx
```

---

# Monitoring

Common tools:
- Prometheus
- Grafana
- Metrics Server

---

# Check Cluster Events

Purpose:
- shows cluster issues and failures

Command:

```bash
kubectl get events
```

---

# Check Resource Usage

Purpose:
- displays CPU and memory usage

Command:

```bash
kubectl top pods
```

---

# Kubernetes Networking

Kubernetes networking includes:
- pod networking
- services
- ingress
- DNS
- CNI plugins

Common CNIs:
- Calico
- Flannel
- Cilium

---

# Kubernetes Security Best Practices

- use RBAC
- restrict privileged containers
- scan images
- use network policies
- use secrets properly
- avoid running as root

---

# Troubleshooting Kubernetes

# Check Pod Status

Purpose:
- identifies failed pods

Command:

```bash
kubectl get pods
```

---

# Describe Pod

Purpose:
- investigates pod failures

Command:

```bash
kubectl describe pod POD_NAME
```

---

# View Logs

Purpose:
- checks application logs

Command:

```bash
kubectl logs POD_NAME
```

---

# Check Node Status

Purpose:
- identifies unhealthy nodes

Command:

```bash
kubectl get nodes
```

---

# Debug Networking

Purpose:
- checks service communication

Command:

```bash
kubectl exec -it POD_NAME -- curl service-name
```

---

# 50 Most Used Kubernetes Commands

| Command | Purpose |
|---|---|
| kubectl get pods | list pods |
| kubectl get nodes | list nodes |
| kubectl get svc | list services |
| kubectl get deployments | list deployments |
| kubectl describe pod | detailed pod info |
| kubectl logs | view pod logs |
| kubectl exec | access pod shell |
| kubectl apply -f | create resources |
| kubectl delete -f | delete resources |
| kubectl delete pod | delete pod |
| kubectl scale deployment | scale replicas |
| kubectl rollout status | rollout progress |
| kubectl rollout undo | rollback deployment |
| kubectl top pods | resource usage |
| kubectl top nodes | node usage |
| kubectl get events | cluster events |
| kubectl get ingress | list ingress |
| kubectl get pvc | list PVC |
| kubectl get pv | list PV |
| kubectl create namespace | create namespace |
| kubectl get ns | list namespaces |
| kubectl config view | kubeconfig |
| kubectl config use-context | switch cluster |
| kubectl cordon | mark node unschedulable |
| kubectl drain | safely remove workloads |
| kubectl uncordon | enable node |
| kubectl taint | apply taints |
| kubectl label | apply labels |
| kubectl annotate | apply annotations |
| kubectl explain | explain resources |
| kubectl api-resources | API resources |
| kubectl cluster-info | cluster details |
| kubectl get componentstatus | control plane health |
| kubectl cp | copy files |
| kubectl port-forward | local port access |
| kubectl auth can-i | permission check |
| kubectl edit | edit resource |
| kubectl replace | replace resource |
| kubectl patch | patch resource |
| kubectl diff | compare changes |
| kubectl wait | wait for resource |
| kubectl get all | list all resources |
| kubectl logs -f | follow logs |
| kubectl exec -it | interactive shell |
| kubectl get endpoints | service endpoints |
| kubectl rollout restart | restart deployment |
| helm install | install chart |
| helm list | list charts |
| helm upgrade | upgrade release |
| helm uninstall | remove release |

---

# Real World Production Scenarios

# Scenario 1 — Pod in CrashLoopBackOff

Symptoms:
- pod repeatedly restarting

Investigation:

```bash
kubectl describe pod POD_NAME
kubectl logs POD_NAME
```

Possible Causes:
- application crash
- wrong environment variable
- database connectivity issue

---

# Scenario 2 — Pod Pending State

Investigation:

```bash
kubectl describe pod POD_NAME
```

Possible Causes:
- insufficient resources
- PVC issue
- node selector mismatch

---

# Scenario 3 — Node NotReady

Investigation:

```bash
kubectl get nodes
journalctl -u kubelet
```

Possible Causes:
- disk pressure
- memory pressure
- kubelet failure

---

# Scenario 4 — Service Not Reachable

Investigation:

```bash
kubectl get svc
kubectl get endpoints
```

Possible Causes:
- selector mismatch
- networking issue
- pod unhealthy

---

# Scenario 5 — ImagePullBackOff

Investigation:

```bash
kubectl describe pod POD_NAME
```

Possible Causes:
- wrong image name
- registry authentication failure
- network issue

---

# Production Troubleshooting Workflow

# Step 1 — Check Pods

```bash
kubectl get pods -A
```

---

# Step 2 — Describe Problem Resource

```bash
kubectl describe pod POD_NAME
```

---

# Step 3 — Check Logs

```bash
kubectl logs POD_NAME
```

---

# Step 4 — Check Events

```bash
kubectl get events
```

---

# Step 5 — Check Nodes

```bash
kubectl get nodes
```

---

# Step 6 — Check Resource Usage

```bash
kubectl top nodes
```

---

# Kubernetes Best Practices

- use namespaces
- use resource limits
- enable monitoring
- implement RBAC
- use readiness probes
- use liveness probes
- avoid latest image tag
- use Helm charts

---

# 50 Kubernetes Interview Questions

## Beginner

1. What is Kubernetes?
2. What is a pod?
3. What is deployment?
4. What is service?
5. Difference between pod and container?
6. What is namespace?
7. What is ConfigMap?
8. What is Secret?
9. What is kubectl?
10. What is ingress?

---

## Intermediate

11. Difference between Deployment and StatefulSet?
12. What is kubelet?
13. What is kube-proxy?
14. What is etcd?
15. Difference between ClusterIP and NodePort?
16. What is rolling update?
17. What is ReplicaSet?
18. What is taint and toleration?
19. Explain liveness and readiness probes.
20. What is Helm?

---

## Advanced

21. Explain Kubernetes architecture.
22. What are CNI plugins?
23. How Kubernetes networking works?
24. Explain Kubernetes scheduler.
25. What is admission controller?
26. Explain RBAC.
27. What is service mesh?
28. Explain Kubernetes operators.
29. What is CSI?
30. Explain container runtime interface.

---

## Production Based

31. Pod in CrashLoopBackOff troubleshooting.
32. Kubernetes node NotReady investigation.
33. Service unreachable debugging.
34. High memory usage in cluster.
35. Kubernetes deployment rollback.
36. Ingress routing failure.
37. Persistent volume issue debugging.
38. Image pull failure handling.
39. Kubernetes upgrade strategy.
40. Securing production cluster.

---

## Scenario Based

41. Entire namespace stuck terminating.
42. Pods cannot communicate.
43. Cluster API server down.
44. Node under memory pressure.
45. Deployment rollout failed.
46. PVC stuck pending.
47. DNS resolution failing inside pods.
48. Kubernetes cluster extremely slow.
49. Pod scheduled on wrong node.
50. Explain your Kubernetes troubleshooting process.

---

# Summary

Kubernetes is the foundation of modern cloud-native infrastructure.

Strong Kubernetes skills are essential for:
- DevOps
- SRE
- Cloud Engineering
- microservices
- CI/CD
- scalable deployments
- production operations

Senior DevOps engineers spend significant time:
- managing clusters
- debugging workloads
- optimizing deployments
- securing infrastructure
- automating operations
