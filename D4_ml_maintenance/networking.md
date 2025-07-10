
# 4.4 Networking for Machine Learning on AWS

- [4.4.1 VPCs and Subnets](#441-vpcs-and-subnets)
- [4.4.2 Security Groups and NACLs](#442-security-groups-and-nacls)
- [4.4.3 Internet Access and VPC Endpoints](#443-internet-access-and-vpc-endpoints)
- [4.4.4 Private IPs and Internal Communication](#444-private-ips-and-internal-communication)
- [4.4.5 Secure Communications](#445-secure-communications)

---

## 4.4.1 VPCs and Subnets

### Virtual Private Cloud (VPC)
An AWS VPC creates a private, isolated network for ML infrastructure. Benefits:
- Secure environment for ML systems
- Private communication between resources
- Hybrid cloud support (VPN, Direct Connect, Transit Gateway)

You define:
- IP address range
- Subnets
- Route tables
- Gateways (Internet Gateway, NAT Gateway)

**AZ Proximity:** Locating data and instances in the same Availability Zone (AZ) ensures low-latency, high-speed access—critical for distributed training.

**Endpoint Isolation:** Deploying multiple SageMaker endpoints in a VPC enables strong isolation and centralized security. Use VPC endpoint policies for fine-grained access control. Monitor with CloudWatch.

### Subnets
Subnets segment your VPC for different ML components:
- **Private Subnets:** Databases, training jobs, backend services (no direct internet)
- **Public Subnets:** Endpoints, load balancers (internet-facing)

Access control:
- Security Groups
- Network Access Control Lists (NACLs)

---

## 4.4.2 Security Groups and NACLs

### Security Groups
Virtual firewalls for EC2 and SageMaker resources.
- **Stateful:** Responses to allowed inbound traffic are allowed out
- **Rule-based:** Inbound/outbound rules by IP, protocol, port

**Best Practices:**
- Allow only trusted IPs, VPCs, or security groups
- Regularly review/update rules
- Deny broad internet access by default

**Example:** SageMaker notebook in a private subnet only accepts traffic from VPC resources, not the internet.

### Network Access Control Lists (NACLs)
Stateless, subnet-level security layer.
- Separate inbound/outbound rules
- Useful for broad traffic control

**Best Practices:**
- Use NACLs with security groups
- Restrict unnecessary traffic
- Deny suspicious/unknown IP ranges

---

## 4.4.3 Internet Access and VPC Endpoints

### Internet Gateway (IGW)
- Provides internet access to public subnets
- Must be attached to VPC and linked via route tables

### Private Subnets
- No direct internet access
- Use NAT Gateway/Instance for outbound-only internet (e.g., updates)

### Public Subnets
- Directly exposed to internet
- Typically have public IPs

### VPC Endpoints
- Private access to AWS services (S3, SageMaker, DynamoDB)
- Traffic stays within AWS network

**Best Practice:** Use VPC endpoints to reduce attack surface and data transfer costs

---

## 4.4.4 Private IPs and Internal Communication

### Private IPs
- Assigned to VPC resources (EC2, RDS, SageMaker)
- Keeps internal traffic private

### Internal Load Balancers
- Use private IPs for secure routing between services

### PrivateLink
- Private VPC-to-VPC communication across accounts/regions (no public internet)

---

## 4.4.5 Secure Communications

### SSL/TLS Encryption
- Always encrypt communication with ML endpoints (e.g., SageMaker HTTPS)
- Ensures confidentiality of requests/responses

### VPC Peering
- Private connection between two VPCs (same/different accounts/regions)
- No traffic over public internet