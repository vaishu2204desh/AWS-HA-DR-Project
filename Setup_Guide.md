📘 Setup Guide – High Availability & Disaster Recovery on AWS

🏗️ Step 1: Create VPCs in Two Regions
🔹 Region A – Primary (e.g., Asia Pacific – Mumbai)

Use: Amazon Web Services Region ap-south-1

Create VPC

CIDR block: 10.0.0.0/16

Create 2 Public Subnets in different Availability Zones

Attach Internet Gateway

Update Route Table to allow internet access

🔹 Region B – Secondary / DR (e.g., singapor)

Region: us-east-1

Create VPC

CIDR block: 20.0.0.0/16

Create 2 Public Subnets in different Availability Zones

Attach Internet Gateway

Configure Route Table

⚙️ Step 2: Launch EC2 Instances & Auto Scaling

Go to EC2 Dashboard in Region A

🔹 Create Launch Template

AMI: Amazon Linux 2 / Ubuntu

Instance Type: t2.micro

Security Group:

Allow HTTP (80)

Allow HTTPS (443)

Allow SSH (22)

🔹 User Data Script (Region A)
#!/bin/bash
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "Hello from Region A" > /var/www/html/index.html
🔹 Create Auto Scaling Group (ASG)

Attach to 2 public subnets

Minimum: 2

Desired: 2

Maximum: 4

🔹 Repeat in Region B

Change user data:

echo "Hello from Region B" > /var/www/html/index.html
🌐 Step 3: Setup Target Group & Load Balancer
In Region A:

Create Target Group

Register EC2 instances

Create Application Load Balancer (ALB)

Attach ALB to 2 public subnets

Configure Listener:

HTTP (80) → Forward to Target Group

Attach ASG to Target Group

Repeat the same steps in Region B.

🌍 Step 4: Configure DNS Failover using Route 53

Use: Amazon Route 53

Go to Route 53 → Hosted Zones

Create Hosted Zone (example: myhaapp.com)

Create 2 A Records with Failover Policy

🔹 Primary Record

Alias → ALB DNS (Region A)

Set Health Check

🔹 Secondary Record

Alias → ALB DNS (Region B)

✅ Behavior

If Region A is UP → Traffic goes to Region A

If Region A is DOWN → Traffic automatically shifts to Region B

🔍 Step 5: Testing Disaster Recovery

Stop all EC2 instances in Region A

Route 53 detects health check failure

Traffic redirects to Region B

Restart Region A → Traffic returns to Primary

📊 Monitoring & Logging

Use: Amazon CloudWatch

Enable CloudWatch Alarms:

CPU Utilization

Instance Health

Enable ALB Access Logs → Store in S3

Configure SNS Alerts for failure notifications

✅ Final Architecture Summary

2 VPCs across 2 AWS Regions

Auto Scaling Groups in both regions

Application Load Balancer per region

Route 53 DNS Failover configuration

CloudWatch Monitoring & Alerts

Disaster Recovery tested successfully
