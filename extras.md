
# AWS ML Exam Extras

## Generative AI
- Creates new content: conversations, stories, images, videos, music
- Mimics human intelligence in image recognition, NLP, translation
- Analyzes training data patterns to recreate **new content** not in original training set

## AWS ML Services

### SageMaker Core
- Managed ML service for training, hosting, deploying models
- Built-in algorithms require labeled dataset + hyperparameter definitions
- Automatic model tuning requires performance metric + training algorithm
- Python SDK integration for monitoring jobs, viewing metrics, adjusting parameters

### SageMaker Endpoints & Deployment
- **Real-time predictions**: Low-latency with dynamic scaling during peak times
- **Automatic scaling**: Handles variable demand efficiently
- **Shadow deployment**: Test new models without affecting users
- **Batch processing**: Use Amazon ECS for scheduled batch jobs

## Data Storage & Processing

### S3 Optimization
- **S3 Select**: Query only required data subset for faster training
- **Regional placement**: Same region as training instances minimizes latency
- **KMS encryption**: SM notebook needs s3:GetObject + kms:Decrypt permissions

### DynamoDB for ML
- Use single table with composite primary key (route ID + timestamp)
- Enables efficient ordered queries by route and time
- Optimal schema for ML training data access patterns

### Data Lakes & ETL
- **Lake Formation + Athena**: Run SQL queries on data lakes
- **Lake Formation + Redshift Spectrum**: Run SQL queries on data lakes
- **AWS Glue**: ETL operations from RDS to S3
- **Glue DPUs**: Run on minimal DPUs for cost-effectiveness (no automatic scaling)

## Real-time & Streaming Processing

### Kinesis & Streaming
- **Kinesis Data Firehose**: Stream logs from S3 → Lambda → OpenSearch
- **Failed records**: Send to separate S3 bucket for failed transformations
- **Apache Flink**: Stateful operations for tracking unique events over time

### Lambda Functions
- Event-driven execution for real-time fraud detection
- Handles variable workload processing
- Use Step Functions for long-running tasks (avoid Lambda timeout limits)

## Model Training Optimization

### Performance Improvements
- **Same AZ**: All training instances in same Availability Zone reduces network latency
- **Data parallelism**: Dataset divided into chunks, each worker trains same model on portion
- **Model parallelism**: Split large models across multiple machines when too big for single machine
- **EFS configuration**: General Purpose + Bursting Throughput mode for high IOPS

### Training Strategies
- **Feature selection**: Deep learning models (CNNs/RNNs) automatically learn features from raw text
- **Unbalanced datasets**: Apply class weights to penalize misclassification of minority class
- **Reduce bias**: Add more training data + cross-validation
- **Adding features**: Add to dataset → retrain → compare performance
- **Cross-validation + early** stopping reduce bias and variance

## Specialized AWS Services

### AI/ML Specific Services
- **Amazon Comprehend Medical**: Extract medical information from unstructured text
- **Amazon A2I (Augmented AI)**: Human review integration in ML workflows
- **Amazon SQS**: Scale A2I workflows with reliable message queuing
- **Amazon Personalize**: Recommendation systems with CloudWatch monitoring
- **Amazon Macie**: ML-based sensitive data discovery and classification
- **Amazon Business**: Supports plugins for third-party integration (ServiceNow, Zendesk)

### Monitoring & Alerting
- **CloudWatch**: Monitor training metrics and logs (not for storing/querying Bedrock model logs)
- **AWS Chatbot**: Integrate alerts with Slack
- **CloudWatch Alarms**: Can directly trigger actions (like stopping EC2) without Lambda
- **SageMaker Debugger**: Capture gradient issues and diagnose training problems

## Security & Access Management

### Key Management
- **AWS Secrets Manager**: Store API tokens, database credentials with automatic rotation
- **AWS KMS**: Encryption key management (doesn't directly rotate API tokens - requires custom Lambda or managed rotation)
- **IAM roles**: Fine-grained access control for ML resources

### Network Security
- **Network ACLs**: Subnet-level explicit allow/deny rules for blocking specific IPs
- **VPC endpoints**: Network isolation for ML services
- **AWS Shield**: DDoS protection

## Deployment & CI/CD

### Pipeline Management
- **CodePipeline**: Orchestrate workflow stages
- **CodeBuild**: Execute data preprocessing and model training
- **Model Registry**: Track model versions
- **MWAA + CodePipeline**: Automated workflows for continuous ML deployment

### Infrastructure as Code
- **AWS CDK**: Script SageMaker training job provisioning
- **AWS Organizations + SSO**: Centralized multi-account management
- **AWS Config Rules**: Automated compliance checking with Lambda

## Cost & Resource Optimization

### Compute Optimization
- **Variable demand**: AWS Lambda + SageMaker automatic endpoint scaling
- **Batch processing**: Amazon ECS for scheduled jobs
- **Resource matching**: Use AWS CDK to select optimal instance types

### Data Processing
- **QuickSight**: Direct CloudWatch connection for dashboards (no S3 intermediary needed)
- **Redshift dynamic data masking**: Real-time PII obfuscation during queries
- **DataBrew**: Use Lambda for post-job data quality metrics to CloudWatch
- **Video processing**: Automated fragmentation and indexing for ML pipelines

## Advanced ML Concepts

### Reinforcement Learning
- **SageMaker RL toolkits**: Intel Coach and Ray RLlib for portfolio optimization
- **Reward function issues**: Incorrect rewards can cause agent to move away from goal
- **Online learning**: Incremental updates for recommendations without batch retraining

### Specialized Models
- **Factorization Machines**: Capture variable interactions in sparse datasets
- **Word embeddings**: Improve input representation by capturing semantic relationships
- **Random Forest**: Good balance of accuracy, adaptability, and computational efficiency
- **CNNs/RNNs**: Automatically learn feature representations from raw text

### Model Serving Architecture
- **API Gateway**: Secure entry point for real-time data ingestion
- **Amazon Cognito**: User authentication and access control

## Key Patterns & Best Practices

### Training Data
- **Multi-year historical data**: Include high-traffic events for better anomaly detection
- **Diverse examples**: More training data reduces bias
- **Feature engineering**: Deep learning automates feature extraction from raw text

### Model Evaluation
- **SageMaker evaluation tools**: Built-in performance assessment before deployment
- **Training metrics**: Plot using SageMaker SDK to visualize learning progress
- **Performance comparison**: Always compare when adding new features

### Container Management
- **Bring your own container**: You handle image creation, configuration, deployment
- **Pre-built containers**: SageMaker manages infrastructure
- **Custom containers**: Full control over environment and dependencies