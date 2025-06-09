# On-Demand vs Provisioned Resources

## Why This Matters

Choosing between on-demand and provisioned cloud resources impacts scalability, cost, and efficiency in ML deployments.

## Understanding the Models

### On-Demand Resources

- **Scalability:**  
  Ideal for unpredictable, spiky workloads. Easily scales during high demand periods.
  
- **Pricing:**  
  Pay-per-use model (per hour or per second). No upfront costs or long-term commitment.

### Provisioned (Reserved) Resources

- **Scalability:**  
  Best for consistent, predictable workloads. Less responsive to sudden spikes.

- **Pricing:**  
  Lower hourly rates with 1-year or 3-year reservation commitments.

## Key Differences

| Factor            | On-Demand Resources                          | Provisioned Resources                          |
|-------------------|----------------------------------------------|-------------------------------------------------|
| **Availability**  | Immediate when needed                        | Pre-allocated; must be reserved in advance      |
| **Pricing Model** | Pay-as-you-go (per second/hour)              | Discounted rates for long-term commitments      |
| **Cost Control**  | Flexible, but potentially higher total cost  | Predictable, potentially lower total cost       |
| **Scalability**   | Highly scalable for dynamic workloads        | Limited scalability; fixed resource capacity    |

# Scaling

## What is Auto-Scaling?

Auto-scaling allows cloud systems to automatically adjust the amount of compute resources (e.g., EC2 instances or containers) based on demand metrics like traffic, CPU usage, or memory.  
Main AWS tools: **Amazon EC2 Auto Scaling** and **Amazon ECS Auto Scaling**

### Types of Scaling:

- **Vertical Scaling (Scale Up/Down):** Increase capacity of existing instances (e.g., more CPU/RAM).
- **Horizontal Scaling (Scale Out/In):** Adjust number of instances; distributes traffic via an Elastic Load Balancer.

## Types of Scaling Policies and Their Trade-offs

### 1. Dynamic Scaling (Metric-Based)

- **What it does:** Adjusts resources based on usage metrics (e.g., CPU, memory, request count).
- **Use case:** E-commerce sites, unpredictable data processing loads.
- **✅ Advantages:**
  - Efficient use of resources
  - Scales only when demand rises
- **⚠️ Trade-offs:**
  - May delay response during scaling up/down
  - Misconfigured alarms can cause performance issues

### 2. Scheduled Scaling

- **What it does:** Predefined scaling actions based on known usage schedules (e.g., scale up at 8 AM).
- **Use case:** Batch jobs, business applications with regular traffic patterns.
- **✅ Advantages:**
  - Low operational overhead
  - Optimized for known workloads
- **⚠️ Trade-offs:**
  - Not suitable for unpredictable or bursty traffic

### 3. Target Tracking Scaling

- **What it does:** Maintains a specific metric target (e.g., keep CPU at 50%) using CloudWatch alarms.
- **Use case:** Applications requiring constant performance levels.
- **✅ Advantages:**
  - Keeps resources stable and efficient
- **⚠️ Trade-offs:**
  - Choosing the right target can be tricky
  - Struggles with sudden traffic spikes

### 4. Step Scaling

- **What it does:** Adds/removes resources based on tiered metric thresholds.
  - Example: Add 1 instance at 70% CPU for 10 mins; add another at 85%.
- **Use case:** Flash sales, product launches, expected traffic bursts.
- **✅ Advantages:**
  - Responds incrementally to traffic increases
- **⚠️ Trade-offs:**
  - High thresholds → under-provisioning
  - Low thresholds → over-scaling and extra cost

## Choosing the Right Scaling Policy

| Policy Type         | Best For                              | Weakness                         |
|---------------------|----------------------------------------|----------------------------------|
| Dynamic Scaling     | Unpredictable, variable workloads       | Slow reaction if misconfigured   |
| Scheduled Scaling   | Predictable traffic patterns            | Not adaptive to changes          |
| Target Tracking     | Performance-sensitive steady workloads  | Hard to pick the right target    |
| Step Scaling        | Anticipated high surges or traffic spikes | Complex configuration            |

# Infrastructure as Code (IaC) Options

## What is Infrastructure as Code?

Infrastructure as Code (IaC) is a way to define and manage your AWS infrastructure using machine-readable scripts instead of manually configuring settings in the AWS Management Console.

**Key IaC Tools on AWS:**
- **AWS CloudFormation**
- **AWS Cloud Development Kit (CDK)**

## Benefits of IaC

| Benefit         | Description                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| **Scalability** | Easily replicate environments (dev, test, prod)                             |
| **Reproducibility** | Version-controlled, allowing rollback to previous states                   |
| **Automation**  | Reduces manual setup and human error                                        |
| **Collaboration** | Teams can co-develop infrastructure as code, enabling DevOps/ML Ops flows  |

## AWS CloudFormation

Allows you to describe AWS resources in **YAML** or **JSON** templates.

### Core Concepts:
- **Templates**: Define what infrastructure to create
- **Stacks**: Deployed units created from templates
- **Change Sets**: Preview changes before applying updates to a stack

The `AWS::SageMaker::Model CloudFormation` resource is specifically designed to define an ML model hosted on Amazon SageMaker. It includes configuration details such as:

- Model artifacts - Stored in Amazon S3.

- Inference container - The container image that contains the inference code.

- IAM Role - Permissions to allow SageMaker to access the resources required for hosting.

This resource is the foundation for creating a SageMaker endpoint, as it defines the model that the endpoint will host.
### ✅ Pros and ⚠️ Cons

| Pros                                | Cons                                                |
|-------------------------------------|-----------------------------------------------------|
| Declarative – describe what, not how| Complex ML architectures can get hard to read       |
| Change Sets = safer deployments     | YAML/JSON is less flexible than general-purpose code|
| Auto rollback on failures           | Not ideal for intricate programmatic logic          |

## Sample CloudFormation Template (S3 Bucket)

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: 'Simple CloudFormation template for ML infrastructure'

Resources:
  MLStorageBucket:
    Type: 'AWS::S3::Bucket'
    Properties:
      BucketName: !Sub 'ml-storage-${AWS::AccountId}-${AWS::Region}'
      VersioningConfiguration:
        Status: Enabled
      BucketEncryption:
        ServerSideEncryptionConfiguration:
          - ServerSideEncryptionByDefault:
              SSEAlgorithm: AES256
      Tags:
        - Key: Project
          Value: MLInfrastructure
        - Key: Environment
          Value: Development

Outputs:
  BucketName:
    Description: 'Name of the S3 bucket created for ML storage'
    Value: !Ref MLStorageBucket

  BucketARN:
    Description: 'ARN of the S3 bucket'
    Value: !GetAtt MLStorageBucket.Arn
```

