---
title: "Blog 2"
date: 2026-06-06
weight: 2
chapter: false
pre: "<b>3.2.</b>"
---

# AWS Shield Advanced Attack Flow Logs for DDoS Attack Monitoring

## Introduction

While learning about AWS security services, I came across a blog introducing a new feature of **AWS Shield Advanced** called **Attack Flow Logs**. What caught my attention was not only its ability to detect and mitigate Distributed Denial-of-Service (DDoS) attacks, but also how it provides detailed visibility into network traffic throughout the attack lifecycle.

Previously, I thought DDoS protection was mainly about identifying and blocking malicious traffic as quickly as possible. However, after reading this article, I realized that collecting traffic data during an attack is just as important. These records help security teams investigate incidents, assess the impact of attacks, and improve their defense strategies for future threats.

---

## What is AWS Shield Advanced?

**AWS Shield Advanced** is AWS's managed DDoS protection service designed to protect AWS resources from sophisticated Layer 3 (Network) and Layer 4 (Transport) attacks.

It supports protection for several AWS resources, including:

- Amazon CloudFront
- Elastic Load Balancing (ELB)
- Amazon Route 53
- AWS Global Accelerator
- Elastic IP (EIP)

Besides automatically detecting and mitigating DDoS attacks, AWS Shield Advanced also provides several monitoring and forensic capabilities that help organizations analyze attacks after they occur.

---

## What are Attack Flow Logs?

**Attack Flow Logs** is a feature that records metadata about network traffic during a DDoS attack.

Instead of providing only high-level statistics, Attack Flow Logs capture detailed information about traffic flows, enabling security teams to perform deeper investigations and post-incident analysis.

The logs can be exported to:

- Amazon S3
- Amazon CloudWatch Logs
- Amazon Data Firehose

This makes it easy to integrate attack data with existing monitoring and analytics platforms.

---

## What Information Is Recorded?

Attack Flow Logs include a variety of useful metadata fields, including:

- Shield Protection ARN
- Log generation timestamp
- Source and destination IP addresses
- Source and destination ports
- Network protocol
- Packet count
- Byte count
- Aggregation window start and end time
- Action taken by AWS Shield
- AWS Edge Location
- Sampling rate
- TCP flags
- Source country

The figure below illustrates some of the metadata fields available in AWS Shield Advanced Attack Flow Logs.

![Attack Flow Log Fields](attack-flow-logs-fields.jpg)

*Figure 1. Metadata fields recorded by AWS Shield Advanced Attack Flow Logs.*

These fields help administrators better understand the origin, characteristics, and scale of a DDoS attack instead of relying only on high-level dashboards or summary statistics.

---

## Benefits of Attack Flow Logs

### Analyze Attack Traffic

Attack Flow Logs provide detailed information about the characteristics and volume of attack traffic instead of only showing aggregated metrics.

### Identify Attack Sources

Using source IP addresses and geographic information, security teams can determine where suspicious traffic originates, making investigations more effective.

### Verify Mitigation Actions

The **Action** field allows administrators to understand how AWS Shield processed and mitigated individual traffic flows during an attack.

### Integrate with Analytics Tools

The collected logs can be analyzed using services such as:

- Amazon Athena
- CloudWatch Logs Insights
- Amazon OpenSearch Service
- SIEM platforms such as Splunk

This allows organizations to leverage their existing analytics and security infrastructure without building a separate logging solution.

---

## What I Learned

After reading this article, I realized that defending against DDoS attacks is not only about detecting and blocking malicious traffic.

Having detailed visibility into attack traffic is equally important because it helps organizations:

- Measure the scale of an attack.
- Identify the origin of suspicious traffic.
- Understand how AWS Shield mitigated the attack.
- Support post-incident investigations.
- Improve future security operations and response strategies.

In my opinion, this is what makes Attack Flow Logs significantly more valuable than simply viewing dashboards or summary metrics.

---

## Conclusion

AWS Shield Advanced Attack Flow Logs improve visibility into DDoS attacks by recording detailed traffic metadata throughout an attack and exporting that information to multiple AWS services for further analysis.

From my perspective, this is a valuable feature because it makes incident investigation, traffic analysis, and security monitoring on AWS much more comprehensive and effective.

For organizations already using AWS Shield Advanced, enabling Attack Flow Logs is a practical way to strengthen DDoS monitoring, forensic analysis, and overall security operations.

---

# References

## Original AWS Blog

**Gain visibility into DDoS attacks with flow logs in AWS Shield Advanced**

https://aws.amazon.com/blogs/security/gain-visibility-into-ddos-attacks-with-flow-logs-in-aws-shield-advanced/

---

## AWS Shield Advanced Documentation

https://docs.aws.amazon.com/waf/latest/developerguide/ddos-overview.html

---

## AWS Shield Advanced Attack Flow Logs Documentation

https://docs.aws.amazon.com/waf/latest/developerguide/shield-advanced-logging.html

## Related Articles

- **Facebook:** [AWS Shield Advanced Attack Flow Log for DDoS Attack Monitoring](https://www.facebook.com/groups/660548818043427/user/100010448557887)
---

# Related AWS Services

- AWS Shield Advanced
- Amazon CloudWatch Logs
- Amazon S3
- Amazon Data Firehose
- Amazon Athena
- Amazon OpenSearch Service

---

# Sources

1. AWS Security Blog. *Gain visibility into DDoS attacks with flow logs in AWS Shield Advanced.*

2. AWS Documentation. *AWS Shield Advanced Developer Guide.*

3. AWS Documentation. *AWS Shield Advanced Attack Flow Logs.*