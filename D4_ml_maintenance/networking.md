# Network Access Controls

Network access controls are essential for securing machine learning (ML) infrastructure. By isolating resources and managing data flow, you can prevent unauthorized access and protect sensitive systems.

## Configuring VPCs, Subnets, and Security Groups

### Virtual Private Cloud (VPC)

An AWS **Virtual Private Cloud (VPC)** lets you create a separate, private network within AWS. You can launch ML infrastructure within this network to protect it from external threats.

**VPC Benefits**:
- Provides a secure, isolated environment for ML systems
- Enables private communication between resources within the VPC
- Supports hybrid cloud integrations (VPN, Direct Connect, AWS Transit Gateway)

You define:
- IP address range
- Subnets
- Route tables
- Gateways (e.g., Internet Gateway, NAT Gateway)

When both the data and the instances are located within the same AZ, the network communication occurs over the high-speed, low-latency infrastructure specific to that AZ, eliminating the additional latency and potential data transfer costs associated with cross-AZ communication. This proximity ensures that the training instances can access the data more quickly and efficiently, which is critical for distributed training where timely synchronization between instances significantly impacts overall performance.

Deploying multiple SageMaker endpoints within a single VPC allows for strong network isolation and centralized security management. Using VPC endpoint policies provides fine-grained access control, while network isolation and encryption enhance security. Amazon CloudWatch enables effective monitoring and alerting, supporting scalability and operational health.

### Subnets

Subnets divide your VPC into smaller segments based on the traffic and security requirements of different ML components.

- **Private Subnets**: Used for resources like databases, training jobs, and backend services that shouldn't have direct internet access.
- **Public Subnets**: Host services that need to communicate with the internet, such as SageMaker endpoints or load balancers.

Access is controlled through:
- **Security Groups**
- **Network Access Control Lists (NACLs)**

### Security Groups

Security groups function as virtual firewalls for Amazon EC2 and SageMaker resources.

**Key Characteristics**:
- **Stateful**: Responses to allowed inbound traffic are automatically allowed back out.
- **Rule-based**: Define inbound and outbound rules based on IP, protocol, and port.

**Best Practices**:
- Allow access only from trusted IPs, VPCs, or other security groups.
- Regularly review and update rules.
- Deny broad internet access by default.

**Example**: A SageMaker notebook in a private subnet may only accept traffic from other VPC resources, with no internet exposure.

### Network Access Control Lists (NACLs)

NACLs offer a stateless, subnet-level layer of security.

- Define separate **inbound** and **outbound** rules.
- Useful for broader traffic control in and out of subnets.

**Best Practices**:
- Use NACLs in conjunction with security groups.
- Restrict unnecessary traffic.
- Apply deny rules for suspicious or unknown IP ranges.

## Controlling Internet Access and Private IPs

Securing ML systems also requires managing internet access and ensuring internal communication happens privately.

### Internet Access

**Internet Gateway (IGW)**:
- Provides internet access to resources in public subnets.
- Must be attached to the VPC and linked via route tables.

**Private Subnets**:
- No direct internet access.
- Use a **NAT Gateway** or **NAT Instance** for outbound-only internet access (e.g., software updates).

**Public Subnets**:
- Directly exposed to the internet.
- Typically include public IP addresses.

**VPC Endpoints**:
- Allow private access to AWS services like S3, SageMaker, and DynamoDB.
- Traffic stays within the AWS network and avoids public exposure.

**Best Practice**:
- Use VPC endpoints to reduce attack surface and data transfer costs.

## Private IPs for Secure Internal Communication

**Private IPs**:
- Assigned to VPC resources (EC2, RDS, SageMaker, etc.)
- Ensure internal traffic remains inside the private network

**Internal Load Balancers**:
- Use private IPs to route traffic securely between internal services

**PrivateLink**:
- Allows private VPC-to-VPC communication across accounts or regions without using the public internet

## Secure Communications

**SSL/TLS Encryption**:
- Always encrypt communication with ML endpoints (e.g., SageMaker HTTPS endpoints)
- Ensures request/response data remains confidential

**VPC Peering**:
- Creates a private connection between two VPCs (same or different accounts/regions)
- No traffic goes over the public internet