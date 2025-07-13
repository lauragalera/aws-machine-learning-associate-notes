
# 4.2 Monitoring Drift in ML Models


- [4.2.1 Data Drift](#421-data-drift)
  - [Types of Data Drift](#types-of-data-drift)
- [4.2.2 Concept Drift](#422-concept-drift)
  - [Types of Concept Drift](#types-of-concept-drift)
- [4.2.3 Detecting and Addressing Drift](#423-detecting-and-addressing-drift)
  - [Tools for Drift Detection](#tools-for-drift-detection)
- [4.2.4 Monitoring Data Quality & Model Performance](#424-monitoring-data-quality--model-performance)
  - [SageMaker Model Monitor](#sagemaker-model-monitor)
  - [Best Practices](#best-practices)

---

## 4.2.1 Data Drift

**Definition:** Changes in the distribution of input features over time.
**Cause:** External factors or evolving trends.
**Impact:** Model predictions become less accurate.

### Types of Data Drift
- **Covariate Shift:** Feature distribution changes, but feature-label relationship remains.
- **Prior Probability Shift:** Class distribution changes, but features still relate the same way to the target.
---
## 4.2.2 Concept Drift

**Definition:** The relationship between input features and the target variable changes.
**Impact:** More critical than data drift as the model’s logic becomes outdated.

### Types of Concept Drift
- **Sudden Drift:** Immediate change (e.g., legal or market disruptions).
- **Incremental Drift:** Gradual shift in data relationships.
- **Recurring Drift:** Seasonal or cyclic reappearance of patterns.
---
## 4.2.3 Detecting and Addressing Drift

- **Monitor Metrics:** Accuracy, precision, F1 score, etc.
- **Retrain Regularly:** Use updated data to improve model performance.
- **Anomaly Detection:** Spot large deviations in input or predictions.

### Tools for Drift Detection
- **Amazon SageMaker Clarify:** Detects data and concept drift, explains predictions.
- **Amazon CloudWatch:** Monitors metrics over time.
---
## 4.2.4 Monitoring Data Quality & Model Performance

### SageMaker Model Monitor
Amazon SageMaker Model Monitor is a managed service that continuously monitors the quality of machine learning models in production. It detects data drift, model quality issues, and anomalies, ensuring models perform as expected and alerting users to issues that might require intervention.

- Automatically detects data drift and anomalies in model inputs/outputs
- Enables automated retraining workflows to maintain accuracy and reliability
- Requires baseline statistics from training data, data capture, and comparison of predictions to actual outcomes

#### Key Features
- **Data Quality Monitoring:** Detects feature distribution drift
- **Model Performance Monitoring:** Tracks prediction accuracy and other metrics
- **Automated Alerts:** Flags performance or data issues
- **Reporting:** Summarizes performance degradation over time

### Best Practices
1. **Define Key Metrics:** Set performance and distribution benchmarks
2. **Use Automated Monitoring:** Reduce manual effort with Model Monitor
3. **Periodic Evaluation:** Test model regularly on fresh data
4. **Retrain When Needed:** Update the model with new data
5. **Set Alerts:** Automatically notify stakeholders of issues