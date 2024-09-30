# Highly-Available-AWS-Infrastructure-with-Auto-Scaling-Load-Balancing-and-Aurora-Failover

|-- README.md

|-- architecture-diagram.png

|-- templates
    |-- vpc.yaml  # CloudFormation template for VPC
    |-- ec2-auto-scaling.yaml  # Template for EC2 Auto Scaling
    |-- aurora-cluster.yaml  # Template for Aurora DB cluster

|-- scripts
    |-- deploy-ec2.sh  # Shell script to deploy EC2 instances
    |-- failover-test.sh  # Script to simulate Aurora failover

This project demonstrates how to set up a highly available AWS architecture featuring EC2 Auto Scaling, Application Load Balancer (ALB), Amazon Aurora with automatic failover, and highly available VPC with redundant NAT gateways. The infrastructure is defined using AWS CloudFormation templates and can be easily deployed using AWS CLI or the AWS Management Console.

Project Overview
This project creates a highly available and scalable AWS infrastructure:

Amazon EC2 Auto Scaling: Automatically adjusts the number of EC2 instances to handle load.
Application Load Balancer (ALB): Distributes incoming traffic across multiple EC2 instances in different Availability Zones.
Amazon Aurora: A highly available MySQL-compatible database with read replicas for automatic failover.
Amazon VPC: A highly available Virtual Private Cloud (VPC) setup with public and private subnets across multiple Availability Zones.
Redundant NAT Gateways: Ensures high availability for outbound traffic from private subnets using NAT Gateways in multiple zones.

This architecture spans multiple Availability Zones for both the application layer and the database layer, ensuring high availability and automatic recovery in case of failure.

Spans across multiple Availability Zones.
Redundant NAT gateways for internet access from private subnets.
EC2 Auto Scaling Group

EC2 instances distributed across multiple Availability Zones.
Load balancing through ALB.
Auto Scaling to maintain the right number of instances based on load.
Amazon Aurora Cluster

A MySQL-compatible Aurora DB cluster.
Multi-AZ read replicas for failover and high availability.
Automatic failover mechanism in case the primary instance becomes unavailable.
Deploying the Infrastructure
Follow these steps to deploy the AWS infrastructure:

1. Deploy the VPC
Use the CloudFormation template provided in cloudformation/vpc.yaml to set up the VPC, subnets, and NAT gateways.
bash
Copy code
aws cloudformation create-stack --stack-name my-vpc-stack --template-body file://cloudformation/vpc.yaml --capabilities CAPABILITY_NAMED_IAM
2. Deploy EC2 Auto Scaling and ALB
Deploy the EC2 instances, Auto Scaling Group, and ALB using the cloudformation/ec2-auto-scaling.yaml template.
bash
Copy code
aws cloudformation create-stack --stack-name my-ec2-stack --template-body file://cloudformation/ec2-auto-scaling.yaml --capabilities CAPABILITY_NAMED_IAM
3. Deploy the Aurora Database Cluster
Use the cloudformation/aurora-cluster.yaml template to create a multi-AZ Amazon Aurora DB cluster with automatic failover.
bash
Copy code
aws cloudformation create-stack --stack-name my-aurora-stack --template-body file://cloudformation/aurora-cluster.yaml --capabilities CAPABILITY_NAMED_IAM
4. Deploy EC2 Instances
Optionally, you can deploy EC2 instances and register them with the ALB using the provided shell script.
bash
Copy code
bash scripts/deploy-ec2.sh
Testing and Validation
1. Test Auto Scaling and Load Balancing
Use a load testing tool (like Apache JMeter) to generate traffic and observe EC2 Auto Scaling in action.
Check the ALB dashboard to ensure traffic is evenly distributed across multiple EC2 instances.
2. Simulate Failover for Amazon Aurora
Test the failover mechanism by simulating a failure in the primary Aurora DB instance.
Use the provided script to initiate a failover:
bash
Copy code
bash scripts/failover-test.sh
Verify in the AWS RDS console that a read replica has been promoted to the primary instance.
3. Test NAT Gateway Failover
Disable one of the NAT Gateways and observe if traffic from private subnets is automatically routed through the remaining NAT Gateway.
Clean Up
To avoid unnecessary charges, ensure that you clean up all the resources created:

bash
Copy code
aws cloudformation delete-stack --stack-name my-vpc-stack
aws cloudformation delete-stack --stack-name my-ec2-stack
aws cloudformation delete-stack --stack-name my-aurora-stack
Diagrams
VPC Architecture

Aurora Failover Process
