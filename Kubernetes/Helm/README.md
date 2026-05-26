# Helm — Kubernetes Package Manager

# Introduction

Helm is a package manager for Kubernetes.

Helm simplifies:
- Kubernetes deployments
- application packaging
- upgrades
- rollback
- templating

Helm is widely used in enterprise Kubernetes environments.

---

# Why Helm is Important

Without Helm:
- managing YAML becomes difficult
- repeated configurations increase
- deployments become harder to maintain

Helm solves this using:
- charts
- templates
- reusable values

---

# Helm Architecture

| Component | Purpose |
|---|---|
| Helm CLI | user interaction |
| Chart | packaged Kubernetes app |
| Repository | chart storage |
| Release | deployed chart instance |
| Values.yaml | configuration values |

---

# What is Helm Chart?

A Helm chart is a packaged Kubernetes application containing:
- deployment YAML
- service YAML
- ingress YAML
- templates
- configuration

---

# Helm Workflow

Developer → Helm Chart → Kubernetes Cluster

---

# Install Helm

# Download Helm

Purpose:
- installs Helm CLI

Command:

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

---

# Verify Helm

Purpose:
- checks installation

Command:

```bash
helm version
```

---

# Add Helm Repository

Purpose:
- adds chart repository

Command:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

---

# Update Repositories

Purpose:
- downloads latest chart metadata

Command:

```bash
helm repo update
```

---

# Search Helm Charts

Purpose:
- find applications

Command:

```bash
helm search repo nginx
```

---

# Install NGINX Using Helm

Purpose:
- deploy application

Command:

```bash
helm install my-nginx bitnami/nginx
```

---

# Verify Deployment

Purpose:
- checks release

Command:

```bash
helm list
```

---

# Verify Pods

Purpose:
- confirms Kubernetes deployment

Command:

```bash
kubectl get pods
```

---

# Helm Chart Structure

Example:

```bash
mychart/
├── Chart.yaml
├── values.yaml
├── charts/
├── templates/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml
```

---

# Create Helm Chart

Purpose:
- generates chart template

Command:

```bash
helm create mychart
```

---

# Chart.yaml

Purpose:
- chart metadata

Example:

```yaml
apiVersion: v2
name: mychart
description: My Kubernetes Application
version: 0.1.0
appVersion: "1.0"
```

---

# values.yaml

Purpose:
- configuration variables

Example:

```yaml
replicaCount: 2

image:
  repository: nginx
  tag: latest

service:
  type: ClusterIP
  port: 80
```

---

# Helm Template Example

deployment.yaml:

```yaml
replicas: {{ .Values.replicaCount }}
```

Helm dynamically injects values from values.yaml.

---

# Install Local Helm Chart

Purpose:
- deploy local chart

Command:

```bash
helm install myapp ./mychart
```

---

# Upgrade Helm Release

Purpose:
- update application

Command:

```bash
helm upgrade myapp ./mychart
```

---

# Rollback Helm Release

Purpose:
- restore previous version

Command:

```bash
helm rollback myapp 1
```

---

# View Release History

Purpose:
- checks deployment revisions

Command:

```bash
helm history myapp
```

---

# Uninstall Helm Release

Purpose:
- removes deployment

Command:

```bash
helm uninstall myapp
```

---

# Helm Dry Run

Purpose:
- previews deployment

Command:

```bash
helm install myapp ./mychart --dry-run
```

---

# Helm Template Rendering

Purpose:
- renders YAML locally

Command:

```bash
helm template myapp ./mychart
```

---

# Helm Namespaces

Install into namespace:

```bash
helm install myapp ./mychart -n dev --create-namespace
```

---

# Helm Dependencies

Purpose:
- manage subcharts

Command:

```bash
helm dependency update
```

---

# Package Helm Chart

Purpose:
- creates distributable package

Command:

```bash
helm package mychart
```

---

# Push Chart to Repository

Purpose:
- share chart

Command:

```bash
helm push mychart-0.1.0.tgz
```

---

# Common Helm Use Cases

- microservices deployment
- Kubernetes platform setup
- monitoring stack installation
- GitOps deployments
- multi-environment management

---

# Install Prometheus Using Helm

Purpose:
- monitoring setup

Commands:

```bash
helm repo add prometheus-community \
https://prometheus-community.github.io/helm-charts
```

```bash
helm repo update
```

```bash
helm install prometheus prometheus-community/prometheus
```

---

# Install Grafana Using Helm

Purpose:
- dashboard visualization

Command:

```bash
helm install grafana grafana/grafana
```

---

# Install ArgoCD Using Helm

Purpose:
- GitOps deployment

Command:

```bash
helm install argocd argo/argo-cd
```

---

# Helm Troubleshooting

---

# Release Failed

Investigation:

```bash
helm status myapp
```

---

# Render YAML for Debugging

Purpose:
- checks template rendering

Command:

```bash
helm template myapp ./mychart
```

---

# Debug Helm Install

Purpose:
- detailed logs

Command:

```bash
helm install myapp ./mychart --debug
```

---

# Check Kubernetes Events

Purpose:
- cluster troubleshooting

Command:

```bash
kubectl get events
```

---

# Pod Failures

Investigation:

```bash
kubectl describe pod POD_NAME
kubectl logs POD_NAME
```

---

# Helm Upgrade Failure

Possible causes:
- invalid values
- immutable fields
- Kubernetes validation failure

Investigation:

```bash
helm history myapp
helm rollback myapp REVISION
```

---

# Production Best Practices

- use values.yaml
- version Helm charts
- use namespaces
- implement RBAC
- avoid hardcoded values
- use secrets management
- validate templates before deployment

---

# Helm vs Kustomize

| Helm | Kustomize |
|---|---|
| templating engine | YAML overlays |
| package manager | customization tool |
| reusable charts | native Kubernetes |
| supports repositories | simpler approach |

---

# Real World Helm Workflow

Developer → GitHub → Jenkins → Docker → Helm Chart → Kubernetes → Monitoring

---

# 100 Most Used Helm Commands

| Command | Purpose |
|---|---|
| helm version | verify Helm |
| helm repo add | add repository |
| helm repo update | update repositories |
| helm search repo | search charts |
| helm install | install chart |
| helm upgrade | upgrade release |
| helm rollback | rollback release |
| helm uninstall | remove release |
| helm list | list releases |
| helm history | release history |
| helm status | release status |
| helm template | render YAML |
| helm package | package chart |
| helm dependency update | update dependencies |
| helm create | create chart |
| helm lint | validate chart |
| helm get values | release values |
| helm get manifest | deployed manifests |
| helm pull | download chart |
| helm show values | chart values |
| kubectl get pods | pod status |
| kubectl get svc | services |
| kubectl get ingress | ingress |
| kubectl describe pod | pod details |
| kubectl logs | pod logs |
| kubectl get events | cluster events |
| kubectl top nodes | node metrics |
| kubectl top pods | pod metrics |
| kubectl rollout status | rollout status |
| kubectl rollout undo | rollback |
| kubectl scale deployment | scale workload |
| kubectl exec -it | shell access |
| kubectl apply -f | deploy manifests |
| kubectl delete -f | remove manifests |
| docker build | build image |
| docker push | push image |
| docker pull | pull image |
| docker ps | running containers |
| docker logs | container logs |
| docker exec | shell access |
| docker inspect | inspect container |
| git clone | clone repo |
| git pull | latest changes |
| git push | upload changes |
| git status | repository status |
| git diff | changes |
| git log | history |
| terraform init | initialize Terraform |
| terraform plan | preview infrastructure |
| terraform apply | deploy infrastructure |
| ansible-playbook | automation |
| aws eks list-clusters | EKS clusters |
| aws ec2 describe-instances | EC2 details |
| aws s3 ls | S3 buckets |
| systemctl status docker | Docker health |
| systemctl restart docker | restart Docker |
| journalctl -u kubelet | kubelet logs |
| top | CPU monitoring |
| htop | process monitoring |
| free -h | memory usage |
| vmstat | memory stats |
| iostat | disk I/O |
| df -h | disk usage |
| du -sh | directory size |
| ps -ef | process list |
| ss -tulpn | open ports |
| netstat -tulpn | network ports |
| ping | connectivity |
| curl | API testing |
| dig | DNS lookup |
| traceroute | network tracing |
| grep | search logs |
| awk | text processing |
| sed | stream editing |
| vim | edit files |
| cat | display files |
| less | paginated view |
| tail -f | follow logs |
| find | locate files |
| tar -xvf | extract archives |
| chmod | permissions |
| chown | ownership |
| env | environment variables |
| export | export variables |
| history | command history |
| crontab -l | cron jobs |
| uptime | system load |
| uname -a | kernel details |
| mount | mounted disks |
| lsblk | block devices |
| fdisk -l | partitions |
| kubectl get namespaces | namespaces |
| kubectl api-resources | API resources |
| kubectl cluster-info | cluster info |
| kubectl config view | kubeconfig |
| kubectl auth can-i | RBAC check |
| helm install --dry-run | preview install |
| helm install --debug | debug install |
| helm show chart | chart info |
| helm repo list | repositories |
| helm search hub | search Helm hub |
| helm env | Helm environment |
| helm plugin list | plugins |
| helm completion bash | shell completion |

---

# 50 Helm Interview Questions with Answers

# 1. What is Helm?

Answer:

Helm is a package manager for Kubernetes used to manage Kubernetes applications using charts.

---

# 2. What is Helm Chart?

Answer:

A Helm chart is a packaged Kubernetes application containing templates and configuration files.

---

# 3. What is values.yaml?

Answer:

values.yaml stores configurable values used by Helm templates.

---

# 4. What is Helm Release?

Answer:

A release is a deployed instance of a Helm chart.

---

# 5. Difference between Helm and kubectl?

Answer:

kubectl:
- directly manages Kubernetes resources

Helm:
- package manager
- simplifies deployments
- supports versioning and rollback

---

# 6. What is Helm rollback?

Answer:

Rollback restores previous application version.

Command:

```bash
helm rollback myapp 1
```

---

# 7. What is Helm templating?

Answer:

Helm templates dynamically generate Kubernetes YAML using variables.

---

# 8. Explain Helm lifecycle.

Answer:

Chart creation → install → upgrade → rollback → uninstall

---

# 9. What are Helm repositories?

Answer:

Repositories store Helm charts for distribution.

---

# 10. How do you troubleshoot Helm deployment failures?

Answer:

Check:
- Helm status
- rendered templates
- Kubernetes events
- pod logs

Commands:

```bash
helm status myapp
helm template myapp ./mychart
kubectl logs POD_NAME
```

---

# Summary

Helm is a critical Kubernetes ecosystem tool used heavily in:
- enterprise Kubernetes
- GitOps workflows
- production deployments
- CI/CD automation

Strong Helm knowledge is essential for:
- DevOps Engineers
- Kubernetes Engineers
- Platform Engineers
- SREs
- Cloud Engineers
