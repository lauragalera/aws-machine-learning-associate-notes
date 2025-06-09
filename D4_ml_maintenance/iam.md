# IAM Roles, Policies, and Groups for AWS Access

Strong identity and access management is essential for AWS resource security and compliance within a machine learning environment.

## Configuring IAM Roles and Policies to Grant Appropriate Access to AWS Services

### IAM Roles Function

- An **IAM role** is an entity with a defined set of permissions to make AWS service requests.
- Roles are assumed by entities such as IAM users (within same or different AWS accounts), AWS services (e.g., EC2, Lambda, SageMaker), or federated users (via web identity or SAML federation).
- Example: An Amazon SageMaker notebook instance assumes an IAM role that grants it read access to an S3 bucket, without needing long-term access keys.

The correct way to centralize access to Amazon S3 buckets for SageMaker notebook instances is to:

- Create a single IAM role with the required S3 access permissions.

- Attach this role to all SageMaker notebook instances used by the data science team.

- IAM roles are specifically designed to grant AWS service resources (like SageMaker notebook instances) secure, temporary access to other AWS services. This ensures:

- Consistent permissions across all team members.

- Simplified management of access policies without duplicating roles.

- Scalability as new SageMaker notebook instances are created.

### IAM Policies

- An **IAM policy** is a JSON document defining permissions (allow or deny) for a user, group, or role.

### Types of Policies

- **AWS Managed Policies:** Pre-created by AWS for common scenarios (e.g., `AmazonS3ReadOnlyAccess`, `AmazonSageMakerFullAccess`).
- **Customer Managed Policies:** Custom policies created by users for specific security needs.
- **Inline Policies:** Embedded directly into a single user, group, or role, often for unique permissions.

### Least Privilege Principle

- Grant only the minimum permissions required for tasks.
- Regularly audit and update policies to remove unnecessary permissions.

## Creating IAM Groups for ML Access Management

### IAM Groups

IAM groups allow you to manage permissions for multiple users collectively. When you attach a policy to a group, all users in that group inherit those permissions.

### Benefits

- **Efficient Administration**: Assign policies to a group instead of each user
- **Scalability**: Easily onboard new users by adding them to a group
- **Role-Based Access Control (RBAC)**: Define groups based on roles

### Example RBAC Grouping

- **ML_Engineers**: Full SageMaker access, read-only S3 access
- **ML_Admins**: Full administrative privileges
- **Analysts**: Read-only access to logs, metrics, and data

### Steps to Create an IAM Group

1. Open the AWS IAM Console
2. Navigate to **Groups**, select **Create New Group**
3. Assign a name, e.g., `SageMaker-Users`
4. Attach relevant policies (e.g., `AmazonSageMakerFullAccess`, `AmazonS3ReadOnlyAccess`)
5. Add users to the group



