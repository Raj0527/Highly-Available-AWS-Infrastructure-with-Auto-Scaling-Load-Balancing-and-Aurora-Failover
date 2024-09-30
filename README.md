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
