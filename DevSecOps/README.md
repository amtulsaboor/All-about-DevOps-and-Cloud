# DevSecOps for DevOps Engineers

# Introduction

DevSecOps integrates security into:
- development
- CI/CD
- infrastructure
- Kubernetes
- cloud platforms

Security becomes part of:
- automation
- deployment pipelines
- infrastructure provisioning
- monitoring workflows

---

# Why DevSecOps?

Traditional security:
- happens at the end
- slows deployments
- detects vulnerabilities late

DevSecOps solves:
- continuous security
- automated scanning
- faster remediation
- secure infrastructure delivery

---

# DevSecOps Lifecycle

| Phase | Security Activity |
|---|---|
| Plan | threat modeling |
| Develop | secure coding |
| Build | SAST scanning |
| Test | DAST scanning |
| Deploy | container scanning |
| Operate | monitoring |
| Monitor | incident detection |

---

# Core DevSecOps Tools

| Tool | Purpose |
|---|---|
| SonarQube | code quality + SAST |
| Trivy | container scanning |
| OWASP ZAP | DAST testing |
| Snyk | dependency scanning |
| Falco | runtime security |
| Vault | secrets management |

---

# SAST (Static Application Security Testing)

SAST scans source code for:
- vulnerabilities
- insecure coding
- security flaws

Examples:
- hardcoded passwords
- SQL injection
- insecure APIs

---

# SonarQube

SonarQube performs:
- code analysis
- vulnerability scanning
- quality checks

---

# Run SonarQube Container

Purpose:
- starts SonarQube server

Command:

```bash
docker run -d --name sonarqube \
-p 9000:9000 sonarqube:lts-community
```

---

# Verify SonarQube

Purpose:
- checks running containers

Command:

```bash
docker ps
```

---

# Run Sonar Scanner

Purpose:
- scans project source code

Command:

```bash
sonar-scanner
```

---

# DAST (Dynamic Application Security Testing)

DAST scans running applications.

Examples:
- SQL injection
- XSS
- insecure authentication

---

# OWASP ZAP

OWASP ZAP performs:
- web application security testing

---

# Run OWASP ZAP

Purpose:
- starts ZAP security scanner

Command:

```bash
docker run -t owasp/zap2docker-stable zap-baseline.py -t http://TARGET_URL
```

---

# Dependency Scanning

Dependency scanning detects:
- vulnerable packages
- outdated libraries

---

# Snyk Test

Purpose:
- scans dependencies

Command:

```bash
snyk test
```

---

# Container Security

Containers must be scanned for:
- vulnerabilities
- misconfigurations
- insecure packages

---

# Trivy

Trivy scans:
- Docker images
- Kubernetes
- filesystems

---

# Install Trivy

Purpose:
- installs vulnerability scanner

Command:

```bash
sudo apt install trivy -y
```

---

# Scan Docker Image

Purpose:
- identifies vulnerabilities

Command:

```bash
trivy image nginx:latest
```

---

# Scan Filesystem

Purpose:
- scans local files

Command:

```bash
trivy fs .
```

---

# Kubernetes Security

Kubernetes security includes:
- RBAC
- network policies
- pod security
- secrets protection

---

# View Kubernetes Secrets

Purpose:
- displays secrets

Command:

```bash
kubectl get secrets
```

---

# Check RBAC

Purpose:
- verifies permissions

Command:

```bash
kubectl auth can-i create pods
```

---

# Pod Security

Best Practices:
- avoid privileged containers
- use read-only filesystem
- restrict root access

---

# Secrets Management

Secrets should never be stored:
- inside code
- inside Docker images
- inside GitHub repositories

---

# HashiCorp Vault

Vault securely manages:
- passwords
- API keys
- certificates

---

# Start Vault Container

Purpose:
- launches Vault

Command:

```bash
docker run --cap-add=IPC_LOCK -d \
-p 8200:8200 vault
```

---

# CI/CD Security

CI/CD pipelines should implement:
- image scanning
- dependency scanning
- secret detection
- approval workflows

---

# GitHub Secret Scan

Purpose:
- checks repository secrets

Command:

```bash
git secrets --scan
```

---

# Infrastructure Security

Infrastructure security includes:
- IAM permissions
- security groups
- encryption
- audit logging

---

# AWS IAM Best Practices

- least privilege
- MFA enabled
- role-based access
- avoid root usage

---

# Runtime Security

Runtime security monitors:
- suspicious activity
- container escape attempts
- abnormal behavior

---

# Falco

Falco detects:
- Kubernetes threats
- runtime attacks

---

# Install Falco

Purpose:
- installs runtime security monitoring

Command:

```bash
helm install falco falcosecurity/falco
```

---

# Security Monitoring

Security monitoring includes:
- SIEM
- logs
- alerts
- anomaly detection

---

# DevSecOps Best Practices

- shift security left
- automate scanning
- scan containers
- implement RBAC
- encrypt secrets
- rotate credentials
- monitor continuously

---

# DevSecOps Troubleshooting

# Verify Docker Security Scan

Purpose:
- validates Trivy scanning

Command:

```bash
trivy image nginx:latest
```

---

# Verify Kubernetes Security

Purpose:
- checks cluster permissions

Command:

```bash
kubectl auth can-i --list
```

---

# Verify SonarQube

Purpose:
- checks service health

Command:

```bash
docker logs sonarqube
```

---

# Verify Vault

Purpose:
- checks Vault status

Command:

```bash
vault status
```

---

# Verify Falco

Purpose:
- checks runtime monitoring

Command:

```bash
kubectl logs -n falco daemonset/falco
```

---

# 50 Most Used DevSecOps Commands

| Command | Purpose |
|---|---|
| trivy image | scan image |
| trivy fs | scan filesystem |
| sonar-scanner | code analysis |
| snyk test | dependency scan |
| kubectl get secrets | Kubernetes secrets |
| kubectl auth can-i | RBAC check |
| docker scan | container scan |
| docker ps | running containers |
| docker logs | container logs |
| docker exec | container shell |
| git secrets --scan | secret detection |
| helm install | deploy security tools |
| helm upgrade | update charts |
| kubectl get pods | cluster resources |
| kubectl describe pod | pod details |
| kubectl logs | pod logs |
| kubectl get networkpolicy | network policies |
| kubectl get rolebindings | RBAC bindings |
| kubectl get clusterroles | cluster roles |
| kubectl top pods | resource monitoring |
| openssl genrsa | generate private key |
| openssl req | generate CSR |
| ssh-keygen | generate SSH key |
| chmod 600 | secure file permissions |
| chown | ownership management |
| ufw status | firewall status |
| iptables -L | firewall rules |
| netstat -tulpn | network ports |
| ss -tulpn | listening ports |
| nmap | network scanning |
| curl -I | HTTP headers |
| wget | download tools |
| vim | edit security configs |
| cat | view files |
| grep | search logs |
| awk | text processing |
| sed | stream editing |
| journalctl | system logs |
| systemctl status | service health |
| ps -ef | running processes |
| top | system monitoring |
| htop | interactive monitoring |
| free -h | memory usage |
| df -h | disk usage |
| whoami | current user |
| id | user details |
| sudo -l | sudo permissions |
| aws iam list-users | IAM users |
| aws cloudtrail describe-trails | audit logging |
| terraform validate | validate IaC |

---

# Real World Production Scenarios

# Scenario 1 — Critical Vulnerability in Docker Image

Symptoms:
- production image contains CVEs

Investigation:

```bash
trivy image my-app:latest
```

Fix:
- upgrade vulnerable packages
- rebuild image

---

# Scenario 2 — Kubernetes Privilege Escalation

Symptoms:
- pod running as root

Investigation:

```bash
kubectl describe pod POD_NAME
```

Fix:
- restrict security context
- disable privileged mode

---

# Scenario 3 — Secrets Exposed in GitHub

Symptoms:
- AWS keys committed

Investigation:

```bash
git secrets --scan
```

Fix:
- rotate credentials
- remove secrets from history

---

# Scenario 4 — SonarQube Scan Failure

Possible Causes:
- scanner authentication issue
- project configuration error

Check:

```bash
docker logs sonarqube
```

---

# Scenario 5 — Runtime Security Alert

Symptoms:
- suspicious shell execution inside container

Investigation:
- Falco alert triggered

Fix:
- isolate container
- analyze logs

---

# Production Troubleshooting Workflow

# Step 1 — Verify Security Scanner

```bash
trivy image nginx:latest
```

---

# Step 2 — Verify Kubernetes Permissions

```bash
kubectl auth can-i --list
```

---

# Step 3 — Verify Runtime Monitoring

```bash
kubectl logs -n falco daemonset/falco
```

---

# Step 4 — Verify Secrets Exposure

```bash
git secrets --scan
```

---

# Step 5 — Verify IAM Security

```bash
aws iam list-users
```

---

# Step 6 — Verify CI/CD Security

Review:
- GitHub Actions
- Jenkins logs
- pipeline scans

---

# Enterprise DevSecOps Workflow

1. Developer pushes code
2. SonarQube performs SAST
3. Dependency scanning executes
4. Docker image built
5. Trivy scans image
6. Kubernetes deployment validated
7. Runtime security enabled with Falco
8. Monitoring and alerting active

---

# DevSecOps Best Practices

- implement least privilege
- automate vulnerability scanning
- scan every container image
- secure Kubernetes clusters
- use secret management
- monitor runtime threats
- implement zero trust principles

---

# 50 DevSecOps Interview Questions

## Beginner

1. What is DevSecOps?
2. What is SAST?
3. What is DAST?
4. What is vulnerability scanning?
5. What is Trivy?
6. What is SonarQube?
7. What is OWASP?
8. What is RBAC?
9. What is secret management?
10. What is container security?

---

## Intermediate

11. Difference between SAST and DAST?
12. Explain DevSecOps lifecycle.
13. What is dependency scanning?
14. Explain Kubernetes security.
15. What is runtime security?
16. Explain RBAC in Kubernetes.
17. What is image scanning?
18. Explain IAM best practices.
19. What is network policy?
20. Explain Vault architecture.

---

## Advanced

21. Explain zero trust architecture.
22. What is supply chain security?
23. Explain Kubernetes admission controllers.
24. What is Falco internally?
25. Explain container escape attacks.
26. What is policy as code?
27. Explain cloud security posture management.
28. What is SBOM?
29. Explain CI/CD security architecture.
30. What is runtime threat detection?

---

## Production Based

31. Vulnerable Docker image remediation.
32. Kubernetes privilege escalation handling.
33. IAM misconfiguration troubleshooting.
34. Secret leakage incident response.
35. Security scan performance optimization.
36. Runtime attack investigation.
37. Secure multi-cloud architecture.
38. Security monitoring strategy.
39. CI/CD security implementation.
40. Kubernetes hardening strategy.

---

## Scenario Based

41. AWS keys leaked publicly.
42. Kubernetes pod compromised.
43. Docker image contains critical CVEs.
44. CI/CD pipeline bypass attack.
45. Falco detecting suspicious activity.
46. SonarQube scan suddenly failing.
47. Secret accidentally committed to GitHub.
48. Production cluster exposed publicly.
49. Container running as privileged root.
50. Explain your end-to-end DevSecOps pipeline.

---

# Summary

DevSecOps is a critical part of modern DevOps engineering.

Strong DevSecOps skills are essential for:
- securing CI/CD pipelines
- protecting cloud infrastructure
- securing Kubernetes clusters
- preventing vulnerabilities
- responding to security incidents

Senior DevOps engineers spend significant time:
- automating security
- scanning infrastructure
- securing pipelines
- hardening Kubernetes
- responding to incidents
