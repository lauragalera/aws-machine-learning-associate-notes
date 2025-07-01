- Generative artificial intelligence (generative AI) is a type of AI that can create new content and ideas, including conversations, stories, images, videos, and music. AI technologies attempt to mimic human intelligence in nontraditional computing tasks like image recognition, natural language processing (NLP), and translation. Generative models can analyze animal images to record variables like different ear shapes, eye shapes, tail features, and skin patterns. They can then recreate new animal images that were not in the training set.

-  Store the API tokens in AWS Secrets Manager. Use AWS Key Management Service (KMS) to encrypt the keys and configure automatic rotation of the keys. FALSE! AWS KMS handles encryption key management and rotation but does not manage or rotate API tokens directly. Token rotation requires a custom Lambda function or managed rotation in Secrets Manager.

- Network ACLs operate at the subnet level and support explicit allow and deny rules, making them ideal for blocking traffic from specific IP addresses without affecting other legitimate traffic.

-  Amazon QuickSight provides advanced visualizations and interactive dashboards, making it ideal for both technical and non-technical stakeholders to monitor performance metrics with real-time insights and drill-down capabilities. It can directly connect to CloudWatch as a data source without needing Amazon S3 as an intermediary.

- Implementing Amazon Redshift dynamic data masking policies is the optimal solution because it allows sensitive columns to be obfuscated in real-time during query execution. This ensures that the data analyst can access the necessary columns for customer behavior analysis without exposing PII.

-  The best practice for optimizing data access patterns in DynamoDB for machine learning training data is to use a single table with a composite primary key consisting of route ID and timestamp. This schema design enables efficient, ordered queries by route and time, which aligns with typical access patterns needed to analyze delivery routes over time.

- Detect a model is fair: F1 score and AUC-ROC effectively measure model accuracy and discrimination ability, particularly in imbalanced datasets common in loan approvals. Evaluating true positive rates across demographic groups directly assesses whether the model treats these groups equitably, revealing potential biases in decision-making.

- Model Parameters are learned during training and define the model's behavior on input data.

- Model Hyperparameters are set before training and control aspects of the learning process, such as learning rate and batch size.

- The best strategies to improve the model’s precision and recall involve enhancing data quality and selecting a more powerful algorithm with efficient hyperparameter tuning.

- Powrful trio: CodePipeline for orchastrating workflow stages, CodeBuild for executing data preprocessing and model training, Model Registry for tracking model versions.

- How can you reduce latency while training? 1) Placing all training instances in the same Availability Zone reduces network latency and improves data throughput between instances, enhancing distributed training speed. 2) Storing data in an S3 bucket within the same Region as the training instances minimizes data access latency, ensuring efficient throughput during training.

- SM notebook instance needs permissions to decrypt objects in S3 -> Attaching an IAM role to the notebook instance with s3:GetObject and kms:Decrypt permissions, and including the notebook’s IAM role ARN in the KMS key policy is necessary to authorize the role to use the key for decryption

- a real-time fraud detection system must process suspicious transaction events in real-time with variable workload -> AWS Lambda for event-driven execution

- a recommendation engine requires low-latency predictions and dynamic scaling during peak times -> SageMaker endpoints for low-latency and dynamic scaling

- a demand forecasting model processes historical sales data in nightly batch jobs -> Amazon ECS for batch processing

- Configure EFS with General Purpose performance mode and Bursting Throughput mode to handle the high IOPS and throughput requirements of a SM model during training.

-  AWS Lambda can be invoked after the DataBrew job completes to calculate and send data quality metrics to CloudWatch

- AWS Glue efficiently performs ETL operations on data from Amazon RDS, storing the transformed data in Amazon S3

- The best approach balances predictive accuracy, adaptability to new operating conditions, and computational efficiency within budget constraints. Random Forest models are well-suited for this because they handle diverse data patterns effectively and are less computationally intensive than deep learning models.

- SM security: data encryption at rest and in transit, fine-grained access controls via AWS Identity and Access Management (IAM), network isolation through VPC endpoints, and compliance with healthcare regulations such as HIPAA

- The best choices for optimizing a resource-intensive image processing model with variable demand are AWS Lambda and AWS SageMaker with automatic endpoint scaling.

- Implement Amazon Personalize and utilize Amazon CloudWatch for monitoring alongside simple notification configurations with Amazon SNS for alerts.

- logs from S3 to OpenSearch -> Use Amazon Kinesis Data Firehose to stream logs from S3 to AWS Lambda for processing, then deliver the processed logs to Amazon OpenSearch Service for indexing.

- Amazon API Gateway serves as a secure entry point for real-time data ingestion, Amazon SageMaker hosts and processes the ML model for predictions, and Amazon Cognito manages secure user authentication and fine-grained access control, which are critical for protecting sensitive healthcare data.

- Run SQL queries in Lake Formation -> Athena and Redshift Spectrum

- You are asked with feature selection -> Deep learning models, such as CNNs or RNNs, automatically learn feature representations from raw text, enhancing both performance and automation in feature extraction.

- Online learning enables the model to incrementally update as new user interactions occur, ensuring that recommendations reflect the latest user preferences and seasonal trends without the latency of batch retraining.

- Amazon Comprehend Medical: a natural language processing service that extracts medical information from unstructured text

-  Amazon A2I (Augmented AI): A service that integrates human review into machine learning workflows to improve prediction accuracy by allowing humans to verify or correct model outputs.

-  Amazon SQS is a fully managed message queuing service that can handle large volumes of messages and scale automatically. It decouples components and enables reliable queuing of human review tasks, making it ideal for scaling Amazon A2I workflows.

- You want to test a new model without affecting users -> Shadow deployment.

- AWS Auto Scaling does not directly manage scaling of Amazon Managed Service for Apache Flink applications; scaling is handled within the Flink service itself.

- Amazon Macie uses machine learning to automatically discover, classify, and monitor sensitive data access patterns, making it suitable for detecting security threats related to data

- Automated fragmentation and indexing enhance the accessibility and processability of video data in real-time, which is crucial for effective machine learning pipelines.

- S3 Select enables querying and retrieving only the required subset of data from S3 objects, reducing the amount of data transferred and processed, which speeds up machine learning model training.

- Apache Flink's stateful operations enable tracking unique events or entities over time directly within the stream processing pipeline, which is essential for managing session data or performing windowing operations needed for real-time analytics in machine learning workflows.

-  Using word embeddings improves input feature representation by capturing semantic relationships between words, which helps the model generalize better to unseen documents.

- Including multiple years of historical data, especially covering high-traffic events, allows the model to learn diverse seasonal patterns and improves its ability to detect anomalies during spikes like Black Friday.

-  AWS CDK enables scripting the provisioning of SageMaker training jobs, including selecting instance types that match computational requirements to optimize resource usage and control costs.

- Alerts in slack -> AWS Chatbot is designed to integrate AWS alerts and notifications with communication platforms like Slack, enabling real-time monitoring and interaction within Slack channels.

- Integrating MWAA with AWS CodePipeline enables automated workflows for continuous testing and deployment of ML models, leveraging MWAA's orchestration capabilities alongside CodePipeline's CI/CD features.

- AWS Shield adds a robust layer of protection against DDoS attacks

- AWS Secrets Manager is designed to securely store and manage sensitive information such as database credentials, enabling automatic rotation and secure access, which enhances the security of ML applications.

- You want to add new features -> add the features to the dataset, retrain the model, and compare the performance

- unbalanced dataset -> Applying class weights to penalize misclassification of the minority class helps the model pay more attention to the positive class, improving its sensitivity toward it.

- RL -> In reinforcement learning, an agent learns by associating actions with rewards or penalties. If the agent is moving farther away from the goal instead of closer, the most likely explanation is that it is being incorrectly rewarded for moving in the wrong direction. This means that the reward function may be flawed, reinforcing undesirable behavior and misleading the agent into thinking that moving away is beneficial.

- data parallelism on SM -> In data parallelism, the dataset is divided into chunks, and each chunk is assigned to a different machine (or worker). Each worker trains the same model on its portion of the data, and then SageMaker synchronizes the gradients across all workers to update the model.

- model parallelism -> When a model is too large to fit into a single machine's memory, model parallelism is used to split the model itself across multiple machines or GPUs. Each machine handles a portion of the model, and they communicate during training to share intermediate output

- A labeled dataset and appropriate hyperparameter definitions are required to train a model with a built-in algorithm in SageMaker.

- Defining the compute resources and running a training job through SageMaker’s managed service is a crucial step.

- reduce bias -> Adding more training data can help reduce bias by providing the model with more diverse examples, enabling it to better capture the complexity of the data. Cross-validation helps reduce bias by ensuring that the model is tested on multiple subsets of the data, improving its ability to generalize and capture more diverse patterns.

- SageMaker provides built-in evaluation tools and allows users to plot training metrics using the SageMaker SDK to assess the model’s performance before deployment. This helps users visualize learning progress and adjust as needed.

- Factorization Machines (FMs) are a type of machine learning model designed to capture interactions between variables — especially in sparse datasets

- reduce bias and variance -> cross validation and early stopping

- While CloudWatch can monitor logs, it is not used to store and query logs specifically for Bedrock models.

- For SM automatic tuning, you must specify the performance metric (accuracy, MSE,...) and the training algorithm.

- When you bring your own container, you are responsible for the image creation, container configurations and deployment.

- SageMaker provides pre-built RL toolkits like Intel Coach and Ray RLlib, which allow users to leverage advanced reinforcement learning algorithms for applications like portfolio optimization.

- SageMaker’s integration with the Python SDK allows users to monitor and manage training jobs, view metrics, and adjust parameters directly from their notebooks.

- Setting up AWS Organizations with Single Sign-On (SSO) provides a centralized management system for multiple AWS accounts. SSO allows users to log in with a single set of credentials and access resources across all linked accounts based on their permissions.

- You can associate an action (like stopping an EC2) with a CloudWatch alarm. No need for lambda.

- You are ingesting data with Kinesis Data Firehose but some data fails transformation, then make KDF to send failed records to a separate S3 bucket.

- Running Glue ETL jobs on a minimal number of DPUs is a cost-effective method. It maintains necessary performance for tasks without provisioning unnecessary resources, adhering to the pay-as-you-go model effectively.

- AWS Step Functions is a nice approach for handling long-running tasks, such as external API calls, without exceeding Lambda's timeout limits.

- Glue does not support automatic scaling of DPUs; you need to manually configure the required DPU settings.

- Amazon Business supports plugins, which allow seamless integration with third-party applications like ServiceNow and Zendesk, enabling the AI assistant to interact with these tools for tasks like ticket creation.

- AWS Config Rules with periodic evaluation can be set to periodically check resources for compliance, allowing the organization to automate regular compliance checks. Custom rules with AWS Lambda allow the organization to create specific compliance criteria to trigger alerts for non-compliant resources, enabling automated responses.

- SageMaker Debugger can capture disappearing gradients through debug rules, allowing users to diagnose gradient issues and adjust parameters like the learning rate.