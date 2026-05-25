# AWS for DevOps Engineers

# Introduction

Amazon Web Services (AWS) is a cloud computing platform providing:
- compute
- storage
- networking
- security
- databases
- monitoring
- automation services

AWS is widely used for:
- cloud-native applications
- DevOps automation
- Kubernetes infrastructure
- scalable deployments
- enterprise applications

---

# Why AWS?

Before cloud computing:
- expensive physical infrastructure
- difficult scaling
- hardware maintenance
- long provisioning time

AWS solves:
- scalability
- elasticity
- automation
- global infrastructure
- high availability

---

# AWS Global Infrastructure

AWS consists of:

| Component | Purpose |
|---|---|
| Region | geographic area |
| Availability Zone | isolated datacenter |
| Edge Location | CDN endpoint |

---

# AWS Core Services

| Service | Purpose |
|---|---|
| EC2 | virtual servers |
| S3 | object storage |
| IAM | identity management |
| VPC | networking |
| RDS | relational database |
| Route53 | DNS management |
| CloudWatch | monitoring |
| EKS | Kubernetes |
| ECS | container orchestration |
| Lambda | serverless |

---

# Install AWS CLI

# Download AWS CLI

Purpose:
- installs AWS command line tool

Command:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

---

# Install unzip

Purpose:
- extracts AWS CLI archive

Command:

```bash
sudo apt install unzip -y
```

---

# Extract AWS CLI

Purpose:
- extracts installer files

Command:

```bash
unzip awscliv2.zip
```

---

# Install AWS CLI

Purpose:
- installs AWS CLI

Command:

```bash
sudo ./aws/install
```

---

# Verify Installation

Purpose:
- checks AWS CLI version

Command:

```bash
aws --version
```

---

# Configure AWS CLI

Purpose:
- configures AWS credentials

Command:

```bash
aws configure
```

Inputs:
- Access Key
- Secret Key
- Region
- Output format

---

# IAM (Identity and Access Management)

IAM manages:
- users
- groups
- roles
- permissions

---

# List IAM Users

Purpose:
- displays IAM users

Command:

```bash
aws iam list-users
```

---

# Create IAM User

Purpose:
- creates AWS user

Command:

```bash
aws iam create-user --user-name devops-user
```

---

# Attach IAM Policy

Purpose:
- grants permissions

Command:

```bash
aws iam attach-user-policy \
--user-name devops-user \
--policy-arn arn:aws:iam::aws:policy/AdministratorAccess
```

---

# EC2 (Elastic Compute Cloud)

EC2 provides virtual machines.

Common Use Cases:
- Jenkins servers
- application hosting
- Kubernetes nodes

---

# Launch EC2 Instance

Purpose:
- creates virtual machine

Command:

```bash
aws ec2 run-instances \
--image-id ami-xxxxxxxx \
--count 1 \
--instance-type t2.micro \
--key-name my-key
```

---

# List EC2 Instances

Purpose:
- displays EC2 servers

Command:

```bash
aws ec2 describe-instances
```

---

# Stop EC2 Instance

Purpose:
- stops server

Command:

```bash
aws ec2 stop-instances --instance-ids INSTANCE_ID
```

---

# Start EC2 Instance

Purpose:
- starts server

Command:

```bash
aws ec2 start-instances --instance-ids INSTANCE_ID
```

---

# Terminate EC2 Instance

Purpose:
- permanently deletes server

Command:

```bash
aws ec2 terminate-instances --instance-ids INSTANCE_ID
```

---

# Security Groups

Security Groups act as virtual firewalls.

---

# Create Security Group

Purpose:
- creates firewall rules

Command:

```bash
aws ec2 create-security-group \
--group-name devops-sg \
--description "DevOps Security Group"
```

---

# Add Inbound Rule

Purpose:
- allows traffic

Command:

```bash
aws ec2 authorize-security-group-ingress \
--group-id SG_ID \
--protocol tcp \
--port 22 \
--cidr 0.0.0.0/0
```

---

# S3 (Simple Storage Service)

S3 stores objects and files.

Common Uses:
- Terraform backend
- backups
- logs
- artifacts

---

# Create S3 Bucket

Purpose:
- creates storage bucket

Command:

```bash
aws s3 mb s3://my-devops-bucket
```

---

# List Buckets

Purpose:
- displays S3 buckets

Command:

```bash
aws s3 ls
```

---

# Upload File to S3

Purpose:
- uploads files

Command:

```bash
aws s3 cp backup.zip s3://my-devops-bucket
```

---

# Download File from S3

Purpose:
- downloads objects

Command:

```bash
aws s3 cp s3://my-devops-bucket/backup.zip .
```

---

# Delete S3 Bucket

Purpose:
- removes bucket

Command:

```bash
aws s3 rb s3://my-devops-bucket --force
```

---

# VPC (Virtual Private Cloud)

VPC provides isolated networking.

Components:
- subnets
- route tables
- internet gateway
- NAT gateway

---

# Create VPC

Purpose:
- creates private network

Command:

```bash
aws ec2 create-vpc --cidr-block 10.0.0.0/16
```

---

# Create Subnet

Purpose:
- creates subnet inside VPC

Command:

```bash
aws ec2 create-subnet \
--vpc-id VPC_ID \
--cidr-block 10.0.1.0/24
```

---

# Route53

Route53 manages DNS.

---

# List Hosted Zones

Purpose:
- displays DNS zones

Command:

```bash
aws route53 list-hosted-zones
```

---

# CloudWatch

CloudWatch provides:
- monitoring
- logs
- metrics
- alarms

---

# List CloudWatch Metrics

Purpose:
- displays metrics

Command:

```bash
aws cloudwatch list-metrics
```

---

# Create Alarm

Purpose:
- monitors infrastructure

Command:

```bash
aws cloudwatch put-metric-alarm \
--alarm-name HighCPU \
--metric-name CPUUtilization \
--namespace AWS/EC2 \
--statistic Average \
--period 300 \
--threshold 80 \
--comparison-operator GreaterThanThreshold \
--evaluation-periods 2
```

---

# Load Balancer

Load Balancer distributes traffic.

Types:
- Application Load Balancer
- Network Load Balancer

---

# Auto Scaling

Auto Scaling automatically adjusts infrastructure.

Benefits:
- high availability
- cost optimization

---

# EKS (Elastic Kubernetes Service)

EKS provides managed Kubernetes.

Benefits:
- managed control plane
- scalable clusters

---

# Update kubeconfig

Purpose:
- connects kubectl to EKS

Command:

```bash
aws eks update-kubeconfig --region us-east-1 --name my-cluster
```

---

# ECS (Elastic Container Service)

ECS manages containers.

Common Launch Types:
- EC2
- Fargate

---

# Lambda

Lambda runs serverless functions.

Benefits:
- no server management
- pay per execution

---

# CloudFormation

CloudFormation automates infrastructure using templates.

Benefits:
- infrastructure as code
- repeatable deployments

---

# AWS Security Best Practices

- least privilege IAM
- enable MFA
- encrypt S3 buckets
- restrict security groups
- use private subnets
- enable logging
- rotate credentials

---

# AWS Cost Optimization

- use Auto Scaling
- terminate unused resources
- use reserved instances
- use lifecycle policies
- monitor CloudWatch billing alarms

---

# AWS Troubleshooting

# Verify AWS CLI Access

Purpose:
- checks authentication

Command:

```bash
aws sts get-caller-identity
```

---

# Check EC2 Status

Purpose:
- verifies instance health

Command:

```bash
aws ec2 describe-instance-status
```

---

# Check Security Group Rules

Purpose:
- verifies firewall configuration

Command:

```bash
aws ec2 describe-security-groups
```

---

# Verify S3 Access

Purpose:
- checks S3 permissions

Command:

```bash
aws s3 ls
```

---

# Debug IAM Permissions

Purpose:
- identifies access issues

Command:

```bash
aws iam simulate-principal-policy
```

---

# 50 Most Used AWS Commands

| Command | Purpose |
|---|---|
| aws configure | configure CLI |
| aws sts get-caller-identity | verify credentials |
| aws ec2 describe-instances | list EC2 |
| aws ec2 run-instances | launch EC2 |
| aws ec2 stop-instances | stop EC2 |
| aws ec2 start-instances | start EC2 |
| aws ec2 terminate-instances | terminate EC2 |
| aws ec2 describe-security-groups | list security groups |
| aws ec2 create-security-group | create SG |
| aws ec2 authorize-security-group-ingress | add rule |
| aws s3 ls | list buckets |
| aws s3 mb | create bucket |
| aws s3 rb | delete bucket |
| aws s3 cp | upload/download |
| aws iam list-users | list IAM users |
| aws iam create-user | create IAM user |
| aws iam create-role | create IAM role |
| aws iam attach-user-policy | attach policy |
| aws vpc create-vpc | create VPC |
| aws ec2 create-subnet | create subnet |
| aws ec2 create-route-table | route table |
| aws ec2 create-internet-gateway | internet gateway |
| aws route53 list-hosted-zones | DNS zones |
| aws cloudwatch list-metrics | metrics |
| aws cloudwatch put-metric-alarm | create alarm |
| aws logs describe-log-groups | log groups |
| aws eks list-clusters | EKS clusters |
| aws eks update-kubeconfig | configure kubectl |
| aws ecs list-clusters | ECS clusters |
| aws lambda list-functions | Lambda functions |
| aws cloudformation list-stacks | CloudFormation stacks |
| aws autoscaling describe-auto-scaling-groups | ASG details |
| aws elbv2 describe-load-balancers | load balancers |
| aws rds describe-db-instances | RDS databases |
| aws dynamodb list-tables | DynamoDB tables |
| aws ecr describe-repositories | ECR repositories |
| aws acm list-certificates | SSL certificates |
| aws sns list-topics | SNS topics |
| aws sqs list-queues | SQS queues |
| aws cloudtrail describe-trails | CloudTrail |
| aws organizations list-accounts | AWS accounts |
| aws iam list-roles | IAM roles |
| aws ec2 describe-volumes | EBS volumes |
| aws ec2 create-key-pair | SSH key pair |
| aws ec2 describe-vpcs | list VPCs |
| aws ec2 describe-subnets | list subnets |
| aws ec2 describe-route-tables | route tables |
| aws ec2 reboot-instances | reboot EC2 |
| aws s3 sync | synchronize S3 |
| aws configure list | CLI configuration |

---

# Real World Production Scenarios

# Scenario 1 — EC2 Server Not Reachable

Investigation:
- verify security groups
- verify subnet routing
- verify instance status

Commands:

```bash
aws ec2 describe-instance-status
```

```bash
aws ec2 describe-security-groups
```

---

# Scenario 2 — S3 Access Denied

Possible Causes:
- IAM permissions
- bucket policy
- encryption restrictions

Investigation:

```bash
aws iam simulate-principal-policy
```

---

# Scenario 3 — High AWS Bill

Investigation:
- unused EC2
- unattached EBS volumes
- large S3 storage

Commands:

```bash
aws ce get-cost-and-usage
```

---

# Scenario 4 — EKS Cluster Not Accessible

Investigation:
- kubeconfig issue
- IAM role issue
- API endpoint issue

Fix:

```bash
aws eks update-kubeconfig
```

---

# Scenario 5 — Auto Scaling Not Working

Investigation:
- CloudWatch alarms
- launch template
- scaling policy

---

# Production Troubleshooting Workflow

# Step 1 — Verify Authentication

```bash
aws sts get-caller-identity
```

---

# Step 2 — Verify Resource State

```bash
aws ec2 describe-instances
```

---

# Step 3 — Verify Networking

```bash
aws ec2 describe-security-groups
```

---

# Step 4 — Verify Monitoring

```bash
aws cloudwatch list-metrics
```

---

# Step 5 — Verify Logs

```bash
aws logs describe-log-groups
```

---

# Step 6 — Verify Permissions

```bash
aws iam list-users
```

---

# Enterprise AWS Workflow

1. Terraform provisions AWS infrastructure
2. Jenkins triggers deployments
3. Docker images stored in ECR
4. Kubernetes workloads deployed to EKS
5. CloudWatch monitors infrastructure
6. Auto Scaling handles traffic spikes

---

# AWS Best Practices

- use least privilege IAM
- enable CloudTrail
- use multi-AZ deployments
- encrypt sensitive data
- implement monitoring
- automate backups
- use infrastructure as code

---

# 50 AWS Interview Questions

## Beginner

1. What is AWS?
2. What is EC2?
3. What is S3?
4. What is IAM?
5. What is VPC?
6. What is Route53?
7. What is CloudWatch?
8. What is Auto Scaling?
9. What is Load Balancer?
10. What is EKS?

---

## Intermediate

11. Difference between Security Group and NACL?
12. Difference between ECS and EKS?
13. What is IAM role?
14. Explain S3 storage classes.
15. What is CloudFormation?
16. Explain Auto Scaling workflow.
17. Difference between public and private subnet?
18. Explain EBS vs EFS.
19. What is NAT Gateway?
20. What is CloudTrail?

---

## Advanced

21. Explain AWS global infrastructure.
22. How EKS internally works?
23. Explain VPC routing.
24. What is Transit Gateway?
25. Explain IAM policy evaluation.
26. What is AWS Organizations?
27. Explain Lambda architecture.
28. What is AWS Control Tower?
29. Explain cross-account access.
30. What is AWS Well-Architected Framework?

---

## Production Based

31. EC2 unreachable troubleshooting.
32. S3 access denied debugging.
33. EKS cluster issue investigation.
34. High AWS bill optimization.
35. Auto Scaling failure debugging.
36. IAM permission troubleshooting.
37. Multi-region disaster recovery strategy.
38. Secure AWS infrastructure design.
39. CloudWatch monitoring setup.
40. Route53 DNS issue troubleshooting.

---

## Scenario Based

41. Entire VPC lost internet connectivity.
42. Application inaccessible behind ALB.
43. EC2 CPU extremely high.
44. Kubernetes pods failing in EKS.
45. IAM user accidentally deleted.
46. RDS database storage full.
47. CloudFormation stack stuck.
48. Auto Scaling launching unhealthy instances.
49. AWS region outage handling.
50. Explain your end-to-end AWS DevOps architecture.

---

# Summary

AWS is the most widely used cloud platform in DevOps and Cloud Engineering.

Strong AWS skills are essential for:
- cloud infrastructure
- Kubernetes deployments
- CI/CD pipelines
- scalable applications
- enterprise cloud operations

Senior DevOps engineers spend significant time:
- managing cloud infrastructure
- optimizing cloud costs
- debugging production issues
- automating deployments
- securing cloud environments
