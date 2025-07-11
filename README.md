# AWS-CloudWatch-Alarm-for-EC2-Memory-Utilization-Monitoring-

---

```markdown
# AWS CloudWatch Alarm for EC2 Memory Utilization Monitoring

## 📌 Overview

This project sets up **Amazon CloudWatch Alarms** to monitor **EC2 instance memory utilization**, which is not available by default in AWS. It includes the steps to install a memory metrics script on the EC2 instance and configure CloudWatch alarms to notify when memory usage crosses a defined threshold.

## 🧰 Tools & Services Used

- AWS EC2
- Amazon CloudWatch
- AWS CLI / EC2 User Data
- SNS (Simple Notification Service) [Optional for alerts]
- Bash / Shell scripting

## 📂 Project Structure

```

project-root/
├── cloudwatch-agent-config.json   # CloudWatch Agent config for memory metrics
├── install-memory-metrics.sh      # Script to install & start CloudWatch Agent
└── README.md                      # Project documentation

````

## ⚙️ Setup Instructions

### 1. Pre-requisites
- An EC2 instance (Amazon Linux 2 / Ubuntu recommended)
- IAM role attached to the EC2 with `CloudWatchAgentServerPolicy` permission
- AWS CLI installed and configured

### 2. Install and Configure CloudWatch Agent
- Upload and run the `install-memory-metrics.sh` script on your EC2 instance.
```bash
chmod +x install-memory-metrics.sh
./install-memory-metrics.sh
````

This script:

* Installs the CloudWatch Agent
* Applies the memory monitoring configuration
* Starts the agent to push memory utilization metrics to CloudWatch

### 3. Create CloudWatch Alarm

Create a CloudWatch Alarm for memory utilization:

* Namespace: `CWAgent`
* Metric Name: `mem_used_percent`
* Dimension: `InstanceId`
* Statistic: `Average`
* Threshold: e.g., **> 80% for 2 evaluation periods**

You can create the alarm via AWS Console or CLI.

### 4. (Optional) Configure SNS Notification

* Create an SNS topic.
* Subscribe your email or Lambda to the topic.
* Attach the SNS topic to the alarm for alerts.

## ✅ Example Alarm Configuration (AWS Console)

* Metric: `mem_used_percent`
* Threshold: **80**
* Period: **5 minutes**
* Actions: Send notification to **SNS Topic**

## 📈 Monitoring

Once deployed, you can monitor memory utilization in:

* **CloudWatch → Metrics → CWAgent → EC2 InstanceId → mem\_used\_percent**
* Alarm status and history will appear under **CloudWatch → Alarms**

## 📬 Notifications

Set up **email or SMS alerts** via **SNS topics** to be notified when memory usage exceeds the threshold.

## 📌 Conclusion

This setup enhances EC2 observability by enabling memory metrics monitoring and proactive alerting using Amazon CloudWatch.

---
