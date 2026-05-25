# GitHub Actions for DevOps Engineers

# Introduction

GitHub Actions is a CI/CD and automation platform built into GitHub.

GitHub Actions automates:
- builds
- testing
- deployments
- security scans
- release workflows
- infrastructure provisioning

GitHub Actions integrates with:
- Docker
- Kubernetes
- AWS
- Terraform
- Ansible
- SonarQube

---

# Why GitHub Actions?

Before GitHub Actions:
- separate CI/CD platforms
- difficult integrations
- complex webhook management

GitHub Actions solves:
- native GitHub integration
- event-driven automation
- scalable CI/CD
- reusable workflows

---

# GitHub Actions Architecture

GitHub Actions consists of:

| Component | Purpose |
|---|---|
| Workflow | automation pipeline |
| Runner | executes jobs |
| Job | group of steps |
| Step | individual task |
| Action | reusable automation unit |

---

# Workflow Lifecycle

1. Developer pushes code
2. GitHub event triggers workflow
3. Runner starts
4. Jobs execute
5. Deployment occurs
6. Results stored in GitHub

---

# GitHub Actions Directory

GitHub workflows are stored in:

```bash
.github/workflows/
```

---

# Create Workflow Directory

Purpose:
- stores workflow YAML files

Command:

```bash
mkdir -p .github/workflows
```

---

# Create Workflow File

Purpose:
- defines automation pipeline

Command:

```bash
vim .github/workflows/main.yml
```

---

# Basic Workflow Example

```yaml
name: CI Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Print Message
        run: echo "Hello DevOps"
```

---

# Workflow Triggers

GitHub Actions can trigger on:
- push
- pull_request
- release
- workflow_dispatch
- schedule

---

# Manual Workflow Trigger

Purpose:
- manually starts workflow

Example:

```yaml
on:
  workflow_dispatch:
```

---

# Scheduled Workflow

Purpose:
- executes workflow automatically

Example:

```yaml
on:
  schedule:
    - cron: "0 2 * * *"
```

---

# Jobs

Jobs run independently inside workflows.

Example:

```yaml
jobs:
  build:
  test:
  deploy:
```

---

# Steps

Steps execute commands sequentially.

Example:

```yaml
steps:
  - name: Install Packages
    run: npm install
```

---

# GitHub Hosted Runners

GitHub provides managed runners.

Examples:
- ubuntu-latest
- windows-latest
- macos-latest

---

# Self-Hosted Runners

Self-hosted runners run on:
- EC2
- Kubernetes
- on-prem servers

Benefits:
- custom environment
- better performance
- private networking

---

# Docker Integration

GitHub Actions can:
- build Docker images
- push images
- run containers

---

# Docker Build Example

```yaml
- name: Build Docker Image
  run: docker build -t app .
```

---

# Docker Push Example

```yaml
- name: Push Docker Image
  run: docker push username/app:latest
```

---

# Kubernetes Deployment

GitHub Actions can deploy:
- Kubernetes manifests
- Helm charts

---

# Kubernetes Deployment Example

```yaml
- name: Deploy to Kubernetes
  run: kubectl apply -f deployment.yml
```

---

# Terraform Integration

GitHub Actions commonly automates:
- terraform init
- terraform plan
- terraform apply

---

# Terraform Workflow Example

```yaml
- name: Terraform Init
  run: terraform init
```

---

# GitHub Secrets

Secrets securely store:
- passwords
- API keys
- tokens

Location:
- Repository Settings → Secrets

---

# Access Secret Example

```yaml
env:
  AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
```

---

# Environment Variables

Environment variables simplify workflows.

Example:

```yaml
env:
  APP_NAME: devops-app
```

---

# Matrix Strategy

Matrix runs jobs across multiple environments.

Example:

```yaml
strategy:
  matrix:
    node-version: [16, 18]
```

---

# Workflow Artifacts

Artifacts store:
- build outputs
- reports
- binaries

---

# Upload Artifact Example

```yaml
- name: Upload Artifact
  uses: actions/upload-artifact@v4
```

---

# Download Artifact Example

```yaml
- name: Download Artifact
  uses: actions/download-artifact@v4
```

---

# Reusable Workflows

Reusable workflows improve:
- standardization
- maintainability

---

# Workflow Caching

Caching improves pipeline performance.

Common caches:
- npm
- Maven
- Gradle
- Docker layers

---

# GitHub Actions Security Best Practices

- use secrets
- restrict permissions
- pin action versions
- avoid plain text credentials
- use OIDC authentication

---

# GitHub Actions Troubleshooting

# View Workflow Logs

Purpose:
- debug pipeline failures

Location:
- GitHub Actions tab

---

# Enable Debug Logs

Purpose:
- detailed troubleshooting

Secret:

```text
ACTIONS_STEP_DEBUG=true
```

---

# Verify Runner Status

Purpose:
- checks runner health

Location:
- Settings → Actions → Runners

---

# Validate YAML Syntax

Purpose:
- detects YAML issues

Command:

```bash
yamllint .github/workflows/main.yml
```

---

# Test Docker Build

Purpose:
- validates image build

Command:

```bash
docker build -t app .
```

---

# 50 Most Used GitHub Actions Commands

| Command | Purpose |
|---|---|
| git push | trigger workflow |
| git pull | fetch changes |
| git clone | clone repository |
| docker build | build image |
| docker push | push image |
| docker login | registry login |
| kubectl apply -f | deploy Kubernetes |
| kubectl get pods | verify deployment |
| terraform init | initialize Terraform |
| terraform plan | preview infrastructure |
| terraform apply | apply infrastructure |
| npm install | install packages |
| npm test | execute tests |
| mvn clean package | Maven build |
| gradle build | Gradle build |
| pytest | Python testing |
| sonar-scanner | code analysis |
| trivy image | security scan |
| aws configure | configure AWS |
| aws eks update-kubeconfig | connect EKS |
| helm install | install Helm chart |
| helm upgrade | upgrade release |
| ssh | remote access |
| scp | file transfer |
| rsync | sync files |
| curl | API requests |
| wget | download files |
| tar -czvf | archive files |
| unzip | extract archives |
| vim | edit workflow |
| cat | view files |
| ls | list files |
| pwd | current directory |
| chmod +x | executable permission |
| systemctl status | service status |
| journalctl -u | logs |
| env | environment variables |
| export | export variables |
| printenv | display variables |
| kubectl logs | pod logs |
| kubectl describe | resource details |
| docker logs | container logs |
| docker ps | running containers |
| terraform validate | validate Terraform |
| ansible-playbook | execute automation |
| yamllint | validate YAML |
| jq | process JSON |
| grep | search logs |
| awk | text processing |
| sed | stream editing |

---

# Real World Production Scenarios

# Scenario 1 — Workflow Failing

Symptoms:
- red workflow status

Investigation:
- inspect logs
- verify secrets
- validate syntax

---

# Scenario 2 — Docker Push Failure

Possible Causes:
- authentication issue
- incorrect tag
- registry unavailable

Fix:
- verify docker login
- verify token permissions

---

# Scenario 3 — Kubernetes Deployment Failure

Investigation:

```bash
kubectl get pods
kubectl describe pod POD_NAME
```

Possible Causes:
- image pull failure
- YAML syntax issue
- insufficient resources

---

# Scenario 4 — Self Hosted Runner Offline

Investigation:
- runner service stopped
- network issue
- disk full

Check:

```bash
systemctl status actions.runner
```

---

# Scenario 5 — Secrets Not Accessible

Possible Causes:
- incorrect secret name
- workflow permissions
- repository restrictions

---

# Production Troubleshooting Workflow

# Step 1 — Verify Workflow Logs

Location:
- GitHub Actions tab

---

# Step 2 — Validate YAML

```bash
yamllint .github/workflows/main.yml
```

---

# Step 3 — Verify Secrets

Location:
- Repository Settings → Secrets

---

# Step 4 — Test Commands Locally

```bash
docker build -t app .
```

---

# Step 5 — Verify Deployment

```bash
kubectl get pods
```

---

# Step 6 — Verify Cloud Infrastructure

Example AWS:

```bash
aws ec2 describe-instances
```

---

# Enterprise GitHub Actions Workflow

1. Developer pushes code
2. Workflow triggered automatically
3. Build starts
4. Unit tests run
5. SonarQube scan executes
6. Docker image built
7. Image pushed to registry
8. Kubernetes deployment updated

---

# GitHub Actions Best Practices

- modularize workflows
- use reusable workflows
- implement caching
- secure secrets
- minimize permissions
- use branch protection
- implement approvals
- monitor workflow execution

---

# 50 GitHub Actions Interview Questions

## Beginner

1. What is GitHub Actions?
2. What is workflow?
3. What is runner?
4. What is job?
5. What is step?
6. What is action?
7. What is workflow_dispatch?
8. What are GitHub hosted runners?
9. What is YAML?
10. What is reusable workflow?

---

## Intermediate

11. Difference between job and step?
12. Explain GitHub Actions architecture.
13. What is matrix strategy?
14. Explain workflow triggers.
15. What are self-hosted runners?
16. Explain workflow caching.
17. What are artifacts?
18. Explain GitHub secrets.
19. How GitHub Actions integrates with Docker?
20. How GitHub Actions integrates with Kubernetes?

---

## Advanced

21. Explain GitHub Actions execution flow.
22. What is OIDC authentication?
23. Explain reusable workflow architecture.
24. How GitHub Actions handles concurrency?
25. Explain runner lifecycle.
26. What are composite actions?
27. Explain workflow permissions.
28. What is dependency graph in workflows?
29. How to optimize workflow performance?
30. Explain GitHub Actions security model.

---

## Production Based

31. Workflow failure troubleshooting.
32. Docker push issue investigation.
33. Self-hosted runner offline debugging.
34. Kubernetes deployment failure handling.
35. Secret management best practices.
36. GitHub Actions scalability strategy.
37. CI/CD rollback workflow.
38. Workflow performance optimization.
39. Production deployment approval strategy.
40. Secure CI/CD pipeline implementation.

---

## Scenario Based

41. Workflow stuck in queued state.
42. GitHub runner consuming high CPU.
43. Workflow passing locally but failing in GitHub.
44. Kubernetes deployment partially updated.
45. Docker image corrupted after build.
46. Workflow triggered multiple times unexpectedly.
47. Secret accidentally exposed in logs.
48. Self-hosted runner disk full.
49. Workflow timeout issue.
50. Explain your end-to-end GitHub Actions CI/CD pipeline.

---

# Summary

GitHub Actions is one of the most important modern CI/CD platforms.

Strong GitHub Actions skills are essential for:
- CI/CD automation
- cloud-native deployments
- Kubernetes automation
- DevOps workflows
- scalable automation pipelines

Senior DevOps engineers spend significant time:
- designing workflows
- automating deployments
- debugging CI/CD pipelines
- securing automation
- optimizing developer workflows
