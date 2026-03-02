This project demonstrates a highly available and disaster recovery architecture deployed on AWS. The infrastructure is designed to minimize downtime and ensure business continuity in case of failures
---
![image](https://github.com/username/repo-name/assets/xxxxx)


# 📌 AWS High Availability & Disaster Recovery (HA/DR) Project

## 🚀 Project Overview

This project demonstrates a highly available and disaster recovery architecture built on AWS. The infrastructure is designed to ensure minimum downtime, automatic failover, and business continuity during failures.

The application is deployed across multiple Availability Zones with load balancing and auto scaling enabled. Database reliability is achieved using Multi-AZ deployment and automated backups.

---

## 🏗️ Architecture Components

* VPC with Public and Private Subnets
* EC2 Instances (Multi-AZ)
* Application Load Balancer
* Auto Scaling Group
* Route 53 (DNS & Health Checks)
* CloudWatch (Monitoring & Alarms)

---

## 🔹 High Availability Features

* Deployment across multiple Availability Zones
* Application Load Balancer distributing traffic
* Auto Scaling for dynamic scaling
* Health checks for instance monitoring

---

## 🔹 Disaster Recovery Strategy

* Manual failover testing
* Infrastructure can be recreated using IaC (if Terraform/CloudFormation used)

---

## 🔍 Failover Testing

* Stopped one EC2 instance manually
* Verified traffic automatically shifted to healthy instance

---

## 📊 Monitoring & Logging

* CloudWatch metrics and alarms
* CPU utilization monitoring
* Load Balancer health checks
* Log tracking for troubleshooting

---

## 🎯 Key Outcomes

* Achieved zero downtime during instance failure
* Ensured database availability using Multi-AZ
* Improved fault tolerance and system reliability
* Designed scalable and production-ready cloud architecture

---

## 📚 Tools & Services Used

* AWS EC2
* AWS Auto Scaling
* AWS Application Load Balancer
* AWS Route 53
* AWS CloudWatch

---

## 📌 Conclusion

This project demonstrates the implementation of High Availability and Disaster Recovery best practices on AWS, ensuring system resilience, scalability, and reliability.

