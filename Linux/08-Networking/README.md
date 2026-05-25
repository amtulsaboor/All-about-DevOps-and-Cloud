# Linux Networking for DevOps Engineers

# Introduction

Networking is the backbone of:
- Cloud Computing
- Kubernetes
- CI/CD
- Microservices
- Load Balancers
- APIs
- Service Discovery
- Distributed Systems

Without networking knowledge, troubleshooting production systems becomes impossible.

DevOps engineers must understand:
- TCP/IP
- DNS
- Routing
- Firewalls
- Ports
- HTTP/HTTPS
- SSH
- Load Balancers
- Kubernetes Networking
- AWS Networking

---

# OSI Model

| Layer | Purpose |
|---|---|
| 7 | Application |
| 6 | Presentation |
| 5 | Session |
| 4 | Transport |
| 3 | Network |
| 2 | Data Link |
| 1 | Physical |

---

# TCP/IP Model

| Layer | Protocols |
|---|---|
| Application | HTTP, HTTPS, DNS |
| Transport | TCP, UDP |
| Internet | IP |
| Network Access | Ethernet |

---

# Understanding IP Address

Example:

```bash
192.168.1.10
```

IPv4 = 32-bit address

---

# Private IP Ranges

| Range | Purpose |
|---|---|
| 10.0.0.0/8 | Private |
| 172.16.0.0/12 | Private |
| 192.168.0.0/16 | Private |

---

# CIDR Notation

Example:

```bash
192.168.1.0/24
```

/24 means:
- 24 bits network
- 8 bits host

Total IPs:

```bash
256
```

---

# Important Networking Commands

# Check IP Address

```bash
ip addr
```

Old command:

```bash
ifconfig
```

---

# Check Routing Table

```bash
ip route
```

---

# Check Hostname

```bash
hostname
hostnamectl
```

---

# DNS Lookup

```bash
nslookup google.com
```

Modern:

```bash
dig google.com
```

---

# Check Connectivity

```bash
ping google.com
```

---

# Trace Route

```bash
traceroute google.com
```

---

# Check Open Ports

```bash
netstat -tulpn
```

Modern replacement:

```bash
ss -tulpn
```

---

# Check Listening Ports

```bash
ss -lnt
```

---

# Test HTTP Endpoint

```bash
curl http://example.com
```

HTTPS:

```bash
curl -v https://example.com
```

---

# Download Files

```bash
wget URL
```

---

# SSH Connectivity

```bash
ssh ubuntu@server-ip
```

Verbose:

```bash
ssh -v ubuntu@server-ip
```

---

# Secure Copy

```bash
scp file.txt ubuntu@server:/tmp
```

---

# Check DNS Configuration

```bash
cat /etc/resolv.conf
```

---

# Network Interface Details

```bash
ip link
```

---

# ARP Table

```bash
arp -a
```

---

# MAC Address

```bash
ip link show
```

---

# Check Firewall Rules

Ubuntu:

```bash
sudo ufw status
```

RHEL:

```bash
sudo firewall-cmd --list-all
```

iptables:

```bash
sudo iptables -L
```

---

# Packet Capture

Install:

```bash
sudo apt install tcpdump -y
```

Capture traffic:

```bash
sudo tcpdump -i eth0
```

Capture port traffic:

```bash
sudo tcpdump port 80
```

---

# DNS Troubleshooting

Query DNS server:

```bash
dig @8.8.8.8 google.com
```

Reverse lookup:

```bash
dig -x IP
```

---

# Check Established Connections

```bash
ss -ant
```

---

# Monitor Bandwidth

Install:

```bash
sudo apt install iftop -y
```

Run:

```bash
sudo iftop
```

---

# HTTP Headers

```bash
curl -I https://google.com
```

---

# Test TCP Connectivity

```bash
telnet IP PORT
```

or

```bash
nc -zv IP PORT
```

---

# Linux Routing

View routes:

```bash
route -n
```

Modern:

```bash
ip route
```

Add route:

```bash
sudo ip route add
```

---

# DNS Resolution Flow

1. Browser cache
2. OS cache
3. /etc/hosts
4. DNS resolver
5. Recursive DNS server
6. Authoritative DNS

---

# Important Network Files

| File | Purpose |
|---|---|
| /etc/hosts | Static host mapping |
| /etc/resolv.conf | DNS servers |
| /etc/hostname | Hostname |
| /etc/nsswitch.conf | Name resolution |

---

# TCP vs UDP

| TCP | UDP |
|---|---|
| Reliable | Fast |
| Connection oriented | Connectionless |
| Used in HTTP | Used in DNS streaming |

---

# Common Ports

| Port | Service |
|---|---|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 53 | DNS |
| 3306 | MySQL |
| 5432 | PostgreSQL |
| 8080 | Jenkins |
| 6443 | Kubernetes API |

---

# Load Balancers

Types:
- Layer 4
- Layer 7

Examples:
- AWS ALB
- AWS NLB
- Nginx
- HAProxy

---

# Kubernetes Networking

Important Concepts:
- Pod networking
- ClusterIP
- NodePort
- Ingress
- CNI plugins

Common CNI:
- Calico
- Flannel
- Cilium

---

# AWS Networking Concepts

- VPC
- Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- NACLs

---

# SSL/TLS Troubleshooting

Check certificate:

```bash
openssl s_client -connect google.com:443
```

---

# Network Performance Analysis

Check latency:

```bash
ping
```

Check packet loss:

```bash
mtr google.com
```

---

# 50 Most Used Networking Commands

```bash
ping
traceroute
tracepath
dig
nslookup
host
curl
wget
ssh
scp
sftp
telnet
nc
netstat
ss
ip addr
ip route
ip link
route
arp
hostname
hostnamectl
tcpdump
iftop
nload
vnstat
wireshark
ethtool
mtr
lsof -i
fuser
iptables
ufw
firewall-cmd
nmcli
resolvectl
journalctl
systemctl restart NetworkManager
curl -I
curl -v
openssl s_client
tcpdump port 443
tcpdump host IP
ip neigh
dig +short
ss -s
ss -antp
```

---

# Real World Production Scenarios

# Scenario 1 — Website Not Accessible

Symptoms:
- timeout
- connection refused

Troubleshooting:

```bash
ping
curl
ss -tulpn
systemctl status nginx
```

Possible Causes:
- nginx down
- firewall block
- DNS issue
- security group issue

---

# Scenario 2 — Kubernetes Pod Cannot Reach Internet

Investigation:

```bash
kubectl exec -it pod -- sh
ping google.com
nslookup google.com
```

Root Causes:
- CNI issue
- DNS issue
- NetworkPolicy block

---

# Scenario 3 — Jenkins Cannot Clone GitHub Repo

Investigation:

```bash
ssh -v git@github.com
curl github.com
dig github.com
```

Root Causes:
- DNS issue
- SSH key issue
- firewall block

---

# Scenario 4 — High Network Latency

Commands:

```bash
mtr google.com
tcpdump
iftop
```

Possible Causes:
- packet drops
- congestion
- overloaded NIC

---

# Scenario 5 — SSL Certificate Expired

Check:

```bash
openssl s_client -connect domain.com:443
```

Fix:
- renew cert
- restart ingress/nginx

---

# Production Troubleshooting Workflow

# Step 1 — Verify Connectivity

```bash
ping
curl
```

---

# Step 2 — Verify DNS

```bash
dig
nslookup
```

---

# Step 3 — Verify Port

```bash
ss -tulpn
nc -zv
```

---

# Step 4 — Verify Service

```bash
systemctl status nginx
```

---

# Step 5 — Verify Firewall

```bash
iptables -L
ufw status
```

---

# Step 6 — Packet Capture

```bash
tcpdump
```

---

# Security Best Practices

- disable unused ports
- use firewalls
- restrict SSH access
- enforce HTTPS
- rotate certificates
- use VPNs
- use private subnets
- disable root SSH login

---

# Performance Best Practices

- use CDN
- enable compression
- optimize DNS
- tune TCP parameters
- use load balancers
- minimize latency

---

# 50 Linux Networking Interview Questions

## Beginner

1. What is IP address?
2. Difference between public and private IP?
3. What is DNS?
4. What is a port?
5. What is ping?
6. Difference between TCP and UDP?
7. What is subnetting?
8. What is CIDR?
9. What is gateway?
10. What is MAC address?

---

## Intermediate

11. What happens when you open google.com?
12. What is routing?
13. What is NAT?
14. Difference between Layer 4 and Layer 7 load balancer?
15. What is ARP?
16. What is MTU?
17. What is packet loss?
18. What is latency?
19. Difference between stateful and stateless firewall?
20. What is DNS propagation?

---

## Advanced

21. Explain TCP three-way handshake.
22. Explain SSL/TLS handshake.
23. What is SYN flood attack?
24. What are Kubernetes CNI plugins?
25. How kube-proxy works?
26. Difference between ClusterIP and NodePort?
27. What is ingress controller?
28. How AWS security groups work?
29. Difference between NACL and Security Group?
30. Explain VPC networking.

---

## Production Based

31. Website not accessible. How will you troubleshoot?
32. DNS resolution failing in Kubernetes.
33. SSL certificate expired incident.
34. Jenkins cannot connect to GitHub.
35. Kubernetes pod cannot reach database.
36. Load balancer returning 502 error.
37. High latency troubleshooting.
38. Connection refused debugging.
39. SSH timeout troubleshooting.
40. Packet drop investigation.

---

## Scenario Based

41. Production API suddenly slow.
42. DNS outage in Kubernetes cluster.
43. Nginx not listening on port 80.
44. EC2 instance unreachable.
45. Docker container networking broken.
46. VPN users cannot connect.
47. HTTPS website failing.
48. Application cannot resolve DNS.
49. Kubernetes ingress not routing traffic.
50. Explain how you troubleshoot a full networking outage.

---

# Summary

Linux networking knowledge is foundational for:
- DevOps
- Kubernetes
- AWS
- Cloud Engineering
- SRE
- Distributed Systems

Senior DevOps engineers spend a huge amount of time debugging:
- DNS
- ports
- load balancers
- routing
- firewalls
- SSL
- Kubernetes networking
- cloud connectivity
