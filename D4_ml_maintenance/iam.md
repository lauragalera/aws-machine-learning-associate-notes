

# 4.3 IAM for Machine Learning on AWS

**Identity and Access Management (IAM) is critical for securing AWS resources and enabling compliant ML workflows.**

- [4.3.1 Overview: IAM Roles, Policies, and Groups](#431-overview-iam-roles-policies-and-groups)
- [4.3.2 Granting Access for ML Workloads](#432-granting-access-for-ml-workloads)
  - [Centralized S3 Access for SageMaker](#centralized-s3-access-for-sagemaker)
- [4.3.3 IAM Policies: Types & Best Practices](#433-iam-policies-types--best-practices)
  - [Types of Policies](#types-of-policies)
  - [Least Privilege Principle](#least-privilege-principle)
- [4.3.4 IAM Groups: Role-Based Access Control (RBAC)](#434-iam-groups-role-based-access-control-rbac)
  - [Benefits of IAM Groups](#benefits-of-iam-groups)
  - [Example Groups](#example-groups)
  - [How to Create an IAM Group](#how-to-create-an-iam-group)
---
## 4.3.1 Overview: IAM Roles, Policies, and Groups

- **IAM Role:** Entity with defined permissions, assumed by users, AWS services (EC2, Lambda, SageMaker), or federated identities. Enables secure, temporary access to AWS resources.
- **IAM Policy:** JSON document that defines permissions (allow/deny) for users, groups, or roles.
- **IAM Group:** Collection of users managed together for streamlined access control.

---

## 4.3.2 Granting Access for ML Workloads

### Centralized S3 Access for SageMaker
To centralize S3 access for SageMaker notebook instances:
1. Create a single IAM role with required S3 permissions
2. Attach this role to all SageMaker notebook instances for the data science team
3. Benefits:
   - Consistent permissions for all team members
   - Simplified management (no duplicate roles)
   - Scalable as new instances are created

---

## 4.3.3 IAM Policies: Types & Best Practices

### Types of Policies
- **AWS Managed Policies:** Pre-built by AWS for common use cases (e.g., `AmazonS3ReadOnlyAccess`, `AmazonSageMakerFullAccess`)
- **Customer Managed Policies:** Custom policies for specific security needs
- **Inline Policies:** Embedded directly in a user, group, or role for unique permissions

### Least Privilege Principle
- Grant only minimum permissions needed
- Audit and update policies regularly

---

## 4.3.4 IAM Groups: Role-Based Access Control (RBAC)

IAM groups simplify permission management for multiple users. Attaching a policy to a group gives all members those permissions.

### Benefits of IAM Groups
- Efficient administration: Assign policies to a group, not each user
- Scalability: Onboard new users by adding them to a group
- RBAC: Define groups by role (e.g., engineers, admins, analysts)

### Example Groups
- **ML_Engineers:** Full SageMaker access, read-only S3
- **ML_Admins:** Full admin privileges
- **Analysts:** Read-only access to logs, metrics, and data

### How to Create an IAM Group
1. Open AWS IAM Console
2. Go to **Groups** > **Create New Group**
3. Name the group (e.g., `SageMaker-Users`)
4. Attach relevant policies (e.g., `AmazonSageMakerFullAccess`, `AmazonS3ReadOnlyAccess`)
5. Add users to the group



