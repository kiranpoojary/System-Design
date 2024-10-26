# Introduction to Observability

Observability allows engineers and operations personnel to assess how a system is functioning and identify any issues.

The topics covered include logging, monitoring, alerts, anomaly detection, root cause analysis, and incident reporting.

By the end of the chapter, viewers should be able to identify areas for improvement in their organization's observability.

The goal is to achieve a robust and fault-tolerant system through excellent observability capabilities.

## 1. Logging

Logging is a simple way of noting events, similar to using print statements in programming languages like Java or C++. Log lines typically include a timestamp, an event level (INFO, WARN, ERROR), details about the event, and the line number in the code file where the log originated.

Logging helps debugging, allowing engineers to trace and analyze the flow of requests in a system. Examples of log lines and their components, including the masking of sensitive information for privacy and security reasons, are discussed.


## 2. Monitor Metrics

Monitoring involves manually or automatically tracking metrics, which are numerical values representing various aspects of a system's performance. Examples of metrics include the amount of memory used, the number of IO operations, sales made by the system, or the number of visitors on a webpage.

These metrics are tracked over time, presented in graphs or time series, and are monitored by operations teams. The dashboard allows for manual decision-making based on the observed data, such as adjusting the number of load balancers in response to changes in request volume.

For organizations using cloud solutions like AWS, tools like CloudWatch are available for monitoring and alerting.


## 3. Anomaly Detection: Holt-Winters Algorithm

Anomaly detection helps find problems before it's too late. This capability is often offloaded to cloud solution providers.

The goal of anomaly detection is to quickly identify unusual patterns in metrics, such as unexpected spikes or collapses in metrics.

We explain confidence intervals, and note that this method may not adapt well to seasonal metrics.

A more reliable approach involves repeated differentiation of metrics. After differentiating multiple times, anomalies, especially spikes, become apparent and can be flagged as issues.

The Holt-Winters algorithm is capable of detecting anomalies even in metrics with seasonal variations.


## 4. Root Cause Analysis

Root cause analysis involves understanding what went wrong when a system experiences an anomaly, and aims to identify the underlying cause of the issue.

There are two approaches to root cause analysis: manual and automated. The manual approach involves investigating log lines, metrics, and possible causes to build an incident report.

The "Five Whys" technique, a series of iterative questions aimed at getting to the root cause of the problem, is a manual method that provides in-depth insights. But it becomes challenging as you delve deeper into the causes.

Automated approaches focus on quickly identifying the cause of an anomaly. They involve looking at the factors affecting a metric and determining the root factor contributing to the anomaly. Mathematical algorithms such as principal component analysis (PCA) and Spearman coefficient, which can be used for automated root cause analysis.

You can also outsource or using machine learning for root cause analysis. Services like Amazon SageMaker can use algorithms like isolation trees to detect anomalies in metrics.
