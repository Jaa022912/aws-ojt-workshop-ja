---
title: "Week 9 Worklog"
date: 2026-07-12
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

* Deploy Grafana Dashboards; Use AWS Tags & Resource Groups to manage and authorize resources (ABAC); Centrally manage systems with AWS Systems Manager (Patch Manager, Session Manager) and introduce CloudFormation (IaC).

---

### Tasks to be completed this week:

| Day | Tasks | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| 2 | - Research Grafana and its role in monitoring data visualization <br> - Install Grafana on EC2 and connect with CloudWatch as a data source <br> - Build Dashboards to monitor Metrics (CPU, Memory, Disk, Network) in real time | 13/07/2026 | 13/07/2026 | <https://000029.awsstudygroup.com/vi/> |
| 3 | - Research AWS Tags and AWS Resource Groups <br> - Practice tagging EC2, EBS and creating Resource Groups based on Tags to classify and manage resources centrally by project/environment | 14/07/2026 | 14/07/2026 | <https://000027.awsstudygroup.com/vi/> |
| 4 | - Practice managing EC2 access permissions using IAM combined with Resource Tags (ABAC - Tag-based Access Control) <br> - Create IAM Policies with conditions based on Tags to assign permissions following the Least Privilege principle | 15/07/2026 | 15/07/2026 | <https://000028.awsstudygroup.com/vi/> |
| 5 | - Research AWS Systems Manager (SSM) <br> - Practice configuring Patch Manager to manage and automatically deploy patches to EC2 <br> - Use Run Command to execute remote commands on multiple servers simultaneously without SSH | 16/07/2026 | 16/07/2026 | <https://000031.awsstudygroup.com/vi/> |
| 6 | - Practice connecting securely to Public/Private EC2 via SSM Session Manager (without opening port 22) <br> - Configure Port Forwarding via Session Manager <br> - Research AWS CloudFormation to automatically deploy infrastructure as code (IaC) <br> - Clean up resources | 17/07/2026 | 17/07/2026 | <https://000058.awsstudygroup.com/vi/> |

---

### Week 9 Achievements:

* Know how to install Grafana on EC2, connect CloudWatch, and set up visual charts.
* Understand the importance of Tagging and Resource Groups in Cloud system administration.
* Understand how to assign flexible permissions using Tag-Based Access Control (ABAC) in IAM.
* Master Patch Manager, Run Command, and Session Manager features of Systems Manager for secure server administration.
* Understand the concept of Infrastructure as Code (IaC) and basic CloudFormation template configurations.
