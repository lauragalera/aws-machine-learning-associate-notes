# Understanding Drift in ML Models

## 1. Data Drift
- **Definition**: Changes in the distribution of input features over time.
- **Cause**: External factors or evolving trends.
- **Impact**: Model predictions become less accurate.

### Types of Data Drift
- **Covariate Shift**: Feature distribution changes, but feature-label relationship remains.
- **Prior Probability Shift**: Class distribution changes, but features still relate the same way to the target.

## 2. Concept Drift
- **Definition**: The relationship between input features and the target variable changes.
- **Impact**: More critical than data drift as the model’s logic becomes outdated.

### Types of Concept Drift
- **Sudden Drift**: Immediate change (e.g., legal or market disruptions).
- **Incremental Drift**: Gradual shift in data relationships.
- **Recurring Drift**: Seasonal or cyclic reappearance of patterns.

## 4. Detecting and Addressing Drift
- **Monitor Metrics**: Accuracy, precision, F1 score, etc.
- **Retrain Regularly**: Use updated data to improve model performance.
- **Anomaly Detection**: Spot large deviations in input or predictions.

### Tools
- **Amazon SageMaker Clarify**: Detects data and concept drift, explains predictions.
- **Amazon CloudWatch**: Monitors metrics over time.

# Techniques for Monitoring Data Quality and Model Performance

## 1. Amazon SageMaker Model Monitor

Amazon SageMaker Model Monitor is a service that continuously monitors the quality of machine learning models in production and helps detect data drift, model quality issues, and anomalies. It ensures that models perform as expected and alerts users to issues that might require human intervention.

A managed service to monitor deployed models in real-time.

### Key Features
- **Data Quality Monitoring**: Detects feature distribution drift.
- **Model Performance Monitoring**: Tracks prediction accuracy and other metrics.
- **Automated Alerts**: Flags performance or data issues.
- **Reporting**: Summarizes performance degradation over time.

## 3. Best Practices
1. **Define Key Metrics**: Set performance and distribution benchmarks.
2. **Use Automated Monitoring**: Reduce manual effort with Model Monitor.
3. **Periodic Evaluation**: Test model regularly on fresh data.
4. **Retrain When Needed**: Update the model with new data.
5. **Set Alerts**: Automatically notify stakeholders of issues.