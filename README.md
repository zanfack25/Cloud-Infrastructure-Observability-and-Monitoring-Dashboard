# Cloud-Infrastructure-Observability-and-Monitoring-Dashboard
Monitoring &amp; Root Cause Analysis (RCA) Dashboard on AWS, Enterprise Cloud Observability with CloudWatch, CloudTrail &amp; Lambda, Logging and Incident Response Solution



# AWS Cloud Observability & Monitoring Dashboard

## Project Overview

Modern cloud applications require continuous monitoring to ensure **availability, performance, security, and reliability**. Simply deploying workloads is not enough—organizations need complete visibility into infrastructure activity, application performance, network traffic, and user actions.

This project demonstrates the implementation of a centralized **AWS Cloud Observability Platform** that collects logs, monitors system health, visualizes operational metrics, generates alerts, and supports **Root Cause Analysis (RCA)**.

The solution integrates multiple AWS services including **CloudWatch**, **CloudTrail**, **VPC Flow Logs**, **Lambda**, **SNS**, **IAM**, **S3**, and **EC2** to create an end-to-end monitoring and logging ecosystem.

---

# Project Objective

The objective of this project is to build a centralized cloud monitoring solution that enables DevOps and Cloud Operations teams to:

* Monitor Cloud infrastructure health in real time
* Collect and centralize logs from multiple AWS services using AWS CloudWatch Monitoring and Logging Solution
* Detect abnormal system behavior with Cloud Infrastructure Observability Platform
* Enhance Enterprise Cloud Observability with CloudWatch, CloudTrail & Lambda
* Generate automated alerts
* Improve application reliability, Cloud Logging and Incident Response Solution*
* Strengthen security auditing with AWS VPC Flow Logs, Monitoring & Alerting Framework
* Support Root Cause Analysis (RCA) with Dashboard on AWS
* Increase operational visibility across AWS resources

---


---

# Why Cloud Logging & Monitoring Matters

Cloud environments are highly dynamic. New resources are created and terminated automatically, making manual monitoring impossible.

A well-designed observability solution helps organizations:

* Detect infrastructure failures before users are affected
* Monitor application performance continuously
* Identify security incidents
* Track user and API activity
* Reduce Mean Time To Detect (MTTD)
* Reduce Mean Time To Resolve (MTTR)
* Improve service reliability
* Enable proactive operations instead of reactive troubleshooting

Without centralized logging and monitoring, diagnosing production issues becomes significantly more difficult.

---

# Architecture Overview

The monitoring architecture consists of the following components:

# Project Architecture 

<img width="784" height="570" alt="image" src="https://github.com/user-attachments/assets/182e0cc6-16d4-42a0-91f3-1079f13bbd93" />

1. VPC Flow Log will log all the data hitting the VPC (accept & reject)
2. IAM role is required to give permissions to VPC Flow Log to write to cloudwatch
3. All the data of VPC Flow Log will be stored in a S3 Bucket for audit trail
4. An EC2 instance is launched in the same VPC which will allow CPU utilization to be captured
5. Cloudwatch acts as the central log and metrics store.
6. Cloudwatch dashboard will help the user to visualize the data such as VPC Flow Logs,
EC2 CPU utilization and Cloud Trail data among others.
7. SNS will send email notification (alarm) to the admin user if CPU utilization of the EC2
instance goes above 80%
8. CloudTrail will send all the account level management data to Cloudwatch which includes
EC2 instance launch events, account activities etc.
9. IAM role is required to give permissions to Lambda to write to Cloudwatch log groups
10. Lambda function is used to filter out the data given by CloudTrail to identify any EC2
launch action and take necessary actions on it, if required.

---

# AWS Services Used

* Amazon EC2
* Amazon VPC
* VPC Flow Logs
* Amazon CloudWatch
* CloudWatch Dashboard
* CloudWatch Alarms
* Amazon CloudTrail
* AWS Lambda
* Amazon SNS
* Amazon S3
* IAM Roles & Policies

---

# Key Features

## 1. Amazon CloudWatch – Centralized Observability

CloudWatch acts as the heart of the monitoring platform.

### Contribution

* Collects infrastructure metrics
* Stores application logs
* Visualizes system health
* Enables dashboards
* Creates alarms
* Supports operational monitoring

### Metrics Monitored

* EC2 CPU Utilization
* EC2 Status Checks
* Lambda Invocations
* Lambda Errors
* S3 Object Count
* SNS Notifications
* VPC Metrics
* CloudTrail Events

### Business Value

CloudWatch provides a single pane of glass for infrastructure monitoring, allowing operations teams to quickly identify abnormal behavior before it impacts users.

---

# 2. CloudTrail – Security & Audit Logging

CloudTrail records every management API call made within the AWS account.

### Contribution

Tracks:

* EC2 launches
* IAM activity
* Console logins
* Resource modifications
* Account changes
* API requests

### Benefits

* Security auditing
* Compliance
* Change tracking
* Root Cause Analysis
* Incident investigation

Example:

If an EC2 instance is unexpectedly launched, CloudTrail records:

* Who launched it
* When
* Source IP
* IAM user
* API request

This significantly reduces investigation time.

## Step 1: Launch EC2 Instance: 
<img width="1552" height="932" alt="image" src="https://github.com/user-attachments/assets/482cc152-c4aa-4b1f-bdf1-baf9e663e597" />


## Step 2: Create and Atach IAM Role to enable EC2 instance to enable communication with CloudWatch

<img width="1552" height="932" alt="image" src="https://github.com/user-attachments/assets/176216bf-b204-444e-a64f-f69879ba52df" />


## Step 3: set up CloudWatch role

<img width="1426" height="942" alt="image" src="https://github.com/user-attachments/assets/8f322b92-a737-4227-9522-bc89f8aa8985" />


<img width="1426" height="942" alt="image" src="https://github.com/user-attachments/assets/29cbfcab-1696-41a2-8ae1-66f673593df4" />


## Step 4: Configure and Launching Amazon CloudWatch Agent

<img width="1665" height="731" alt="image" src="https://github.com/user-attachments/assets/c787e392-2e22-499a-a91a-06c44da00377" />

## Step 5-Verify that the logs are populated by the agent in AWS CloudWatch

<img width="1552" height="932" alt="image" src="https://github.com/user-attachments/assets/08868d3b-c281-4a41-8308-8622496ca8e9" />

<img width="1552" height="932" alt="image" src="https://github.com/user-attachments/assets/e84b3f8b-ea0b-41a5-80da-1ffe93b3abe5" />


---

# 3. VPC Flow Logs – Network Visibility

VPC Flow Logs capture all accepted and rejected network traffic entering or leaving the VPC.

### Contribution

Provides visibility into:

* Incoming traffic
* Outgoing traffic
* Accepted connections
* Rejected packets
* Suspicious IP addresses
* Network troubleshooting

### Benefits

* Network monitoring
* Security analysis
* Firewall troubleshooting
* Root Cause Analysis

The logs are stored in both:

* CloudWatch Logs
* Amazon S3

allowing real-time monitoring and long-term auditing.

---

# 4. CloudWatch Log Groups

Log Groups centralize logs from multiple AWS services.

### Contribution

Stores logs from:

* VPC Flow Logs
* CloudTrail
* Lambda
* EC2 applications

### Benefits

* Centralized logging
* Log retention policies
* Easier searching
* Historical analysis
* Compliance

A retention policy of six months was configured to optimize storage costs while preserving sufficient historical data.

---

# 5. IAM Roles

IAM Roles enable secure service-to-service communication without embedding credentials.

### Roles Created

**VPC Flow Log Role**

Allows:

* Create Log Groups
* Create Log Streams
* Write Logs

**Lambda Execution Role**

Allows:

* CloudWatch access
* Log creation
* Log writing

### Benefits

* Least privilege access
* Improved security
* Credential-free authentication
* AWS best practices

---

# 6. Amazon SNS – Automated Alerting

Amazon SNS delivers real-time notifications whenever critical thresholds are exceeded.

### Alarm Configured

Condition:

```
EC2 CPU Utilization > 80%
```

Action:

```
Send Email Notification
```

### Benefits

* Immediate alerting
* Faster response
* Reduced downtime
* Improved operational awareness

Instead of manually checking dashboards, administrators receive proactive notifications.

---

# 7. AWS Lambda – Intelligent Log Processing

Lambda automatically processes CloudTrail events.

### Workflow

CloudTrail

↓

CloudWatch Logs

↓

Lambda

↓

Parse Events

↓

Detect "RunInstances"

↓

Extract EC2 Details

↓

Log Results

### Benefits

* Event-driven automation
* Real-time processing
* Reduced manual effort
* Foundation for automated remediation

The solution can easily be extended to automatically terminate unauthorized EC2 instances or notify security teams.

---

# 8. Amazon S3 – Long-Term Log Storage

S3 stores VPC Flow Logs for durable, low-cost archival.

### Benefits

* Long-term retention
* Compliance
* Historical investigation
* Cost-effective storage
* Disaster recovery

Keeping logs outside CloudWatch also reduces operational costs for long-term retention.

---

# 9. CloudWatch Dashboard

A centralized dashboard provides operational visibility across the AWS environment.

### Dashboard Widgets

* EC2 CPU Utilization
* Top Rejected IP Addresses
* CloudTrail Events
* SNS Notification Count
* S3 Object Count
* Lambda Metrics

### Benefits

* Single monitoring interface
* Faster troubleshooting
* Infrastructure health overview
* Executive reporting

<img width="1870" height="700" alt="image" src="https://github.com/user-attachments/assets/52f83490-f7dd-41be-b485-8d2b9f15bc19" />




<img width="934" height="385" alt="image" src="https://github.com/user-attachments/assets/7bfb59d6-86d4-4bc1-91a1-a3c87b339417" />



---

# Root Cause Analysis (RCA)

One of the primary objectives of this project is to enable efficient Root Cause Analysis.

Example investigation workflow:

**Issue**

Users report application latency.

↓

CloudWatch Dashboard identifies CPU spikes.

↓

CloudWatch Alarm confirms CPU exceeded 80%.

↓

SNS sends notification.

↓

CloudTrail verifies whether a new EC2 instance was launched.

↓

Lambda extracts EC2 launch details.

↓

VPC Flow Logs reveal abnormal incoming traffic.

↓

Logs stored in S3 provide historical evidence.

↓

Root cause identified and corrective action taken.

This integrated workflow significantly reduces Mean Time to Resolution (MTTR).

---

# Observability Features Implemented

| Capability              | AWS Service            | Purpose                       |
| ----------------------- | ---------------------- | ----------------------------- |
| Metrics Collection      | CloudWatch             | Monitor resource performance  |
| Centralized Logging     | CloudWatch Logs        | Aggregate infrastructure logs |
| API Auditing            | CloudTrail             | Record account activity       |
| Network Visibility      | VPC Flow Logs          | Monitor network traffic       |
| Dashboard Visualization | CloudWatch Dashboard   | Operational insights          |
| Alerting                | SNS + CloudWatch Alarm | Notify administrators         |
| Event Processing        | Lambda                 | Automated log analysis        |
| Long-Term Storage       | S3                     | Log archival                  |
| Secure Access           | IAM Roles              | Least-privilege permissions   |

---

# Security Considerations

This implementation follows several AWS security best practices:

* Least privilege IAM roles
* Service-to-service authentication using IAM Roles
* CloudTrail enabled for auditing
* Centralized log management
* Long-term log retention
* Automated monitoring
* Real-time alerting
* Audit trail preservation in S3

---

# Skills Demonstrated

* AWS Cloud Architecture
* CloudWatch Monitoring
* CloudWatch Dashboards
* CloudWatch Alarms
* CloudTrail Logging
* VPC Flow Logs
* AWS Lambda
* Amazon SNS
* Amazon S3
* IAM Roles & Policies
* Infrastructure Monitoring
* Cloud Observability
* Root Cause Analysis (RCA)
* Security Auditing
* Event-Driven Automation
* DevOps Operations
* Infrastructure Reliability
* Performance Monitoring

---

# Project Outcomes

By implementing this cloud observability solution, the environment gained:

* Centralized monitoring across AWS services
* Real-time infrastructure visibility
* Automated CPU utilization alerts
* Comprehensive audit logging for compliance
* Network traffic analysis through VPC Flow Logs
* Automated processing of CloudTrail events using Lambda
* Long-term log retention in Amazon S3
* Faster incident detection and Root Cause Analysis (RCA)
* Improved reliability, operational efficiency, and security posture

This project demonstrates practical experience in designing and implementing an AWS observability solution aligned with DevOps operational best practices, showcasing the ability to monitor, troubleshoot, and maintain cloud infrastructure at an intermediate level.
