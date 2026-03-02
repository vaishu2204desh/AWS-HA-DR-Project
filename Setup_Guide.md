Setup Guide – High Availability & Disaster Recovery on AWS
🏗️ Step 1: Create VPCs in Two Regions
Go to VPC Dashboard.

Create VPC-1 in Region A (e.g., ap-south-1 – Mumbai).

CIDR block: 10.0.0.0/16
Create 2 public subnets in different AZs.
Create VPC-2 in Region B (e.g., us-east-1 – N. Virginia).

CIDR block: 20.0.0.0/16
Create 2 public subnets in different AZs.
⚙️ Step 2: Launch EC2 Instances & Auto Scaling
Go to EC2 Dashboard in Region A.

Create a Launch Template with:

Amazon Linux 2 / Ubuntu AMI

Instance type: t2.micro (for testing)

Security group: allow HTTP (80), HTTPS (443), SSH (22).

User Data (optional for web app):

#!/bin/bash
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "Hello from Region A" > /var/www/html/index.html
Create an Auto Scaling Group (ASG) using this launch template.

Attach ASG to 2 subnets in Region A.
Min size = 2, Desired = 2, Max = 4.
Repeat steps in Region B, but update User Data:

echo "Hello from Region B" > /var/www/html/index.html
🌐 Step 3: Setup Target Group and Load Balancers
In Region A, create an Target Group.

select EC2 instances that you want to target.

In Region A, create an Application Load Balancer (ALB).

Attach ALB to the 2 subnets in different AZs.
Target Group → attach the ASG.
Listener → HTTP (80) forward to Target Group.
Repeat the same steps in Region B.

🌍 Step 4: Configure Route 53 for Failover
Go to Route 53 → Hosted Zones.

Create a new hosted zone (e.g., myhaapp.com).

Add 2 A-records with failover policy:

Record 1 (Primary) → Alias → ALB DNS name (Region A).
Record 2 (Secondary) → Alias → ALB DNS name (Region B).
Set health check for Region A load balancer.
Test DNS:

If Region A is UP → traffic goes to Region A.
If Region A is DOWN → Route 53 sends traffic to Region B.
🔍 Step 5: Testing Disaster Recovery
Stop all EC2 instances in Region A → Route 53 will failover to Region B.
Restart Region A instances → traffic will return to primary region.
📊 Monitoring & Logging
Enable CloudWatch Alarms for CPU, Memory, and Instance Health.
Enable ALB Access Logs to S3.
Setup SNS Alerts for failures.
✅ Final Architecture
2 VPCs across 2 AWS regions.
Auto Scaling Groups with 2 EC2 instances each.
Load Balancer per region.
Route 53 DNS Failover between regions.
