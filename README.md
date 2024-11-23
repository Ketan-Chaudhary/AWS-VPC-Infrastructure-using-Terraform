# Overview

The primary objective of this project is to set up a highly available and scalable web server infrastructure on AWS using Terraform. The infrastructure includes a Virtual Private Cloud (VPC), subnets, security groups, EC2 instances, an Application Load Balancer (ALB), and an S3 bucket for storage. The setup ensures the web servers are accessible, secure, and can handle traffic efficiently.


# VPC Infrastructure

![how-it-works](https://github.com/user-attachments/assets/59602158-0baf-4ccb-a401-3342ab73ddaa)


### This Terraform script (main.tf) provisions the following resources in AWS:

1. **VPC** with a specified CIDR block.
2. **Two Subnets** within the VPC, each in different availability zones.
3. **Internet Gateway** attached to the VPC.
4. **Route Table** associated with the subnets, routing traffic through the Internet Gateway.
5. **Security Group** allowing HTTP and SSH traffic.
6. **S3 Bucket** for storing files.
7. Two **EC2 Instances** within the subnets, using a specified AMI, with user data scripts.
8. **Application Load Balancer** (ALB) spanning both subnets.
9. **Target Group** for the ALB, with health checks.
10. **ALB Listener** for forwarding traffic to the target group.
11. **Output** for the DNS name of the load balancer.

# Components:

## VPC (Virtual Private Cloud):

* A VPC is created with a specified CIDR block to provide an isolated network for resources.

## Subnets:

* Two subnets are provisioned within the VPC, each located in different availability zones (ap-south-1a and ap-south-1b) to ensure high availability.

## Internet Gateway and Route Table:

* An Internet Gateway is attached to the VPC to allow internet access.
* A route table is created and associated with the subnets, directing internet-bound traffic through the Internet Gateway.

## Security Group:

* A security group is configured to allow HTTP (port 80) and SSH (port 22) traffic from any IP address, ensuring web and administrative access.

## S3 Bucket:

* An S3 bucket is created to store files, potentially for hosting static content or backups.

## EC2 Instances:

* Two EC2 instances are launched in the subnets using a specified Amazon Machine Image (AMI).
* User data scripts are executed on these instances at launch to set up the web servers.

## Application Load Balancer (ALB):

An ALB is set up to distribute incoming HTTP traffic across the two EC2 instances.
The ALB spans both subnets to ensure availability even if one availability zone fails.

## Target Group and Listener:

* A target group is created for the ALB with health checks to monitor the web servers' status.
* The ALB listener forwards incoming traffic to the target group, ensuring load balancing.

## Outputs:

* The DNS name of the ALB is outputted, providing a single point of access to the web servers.


# Result

Each EC2 instance is configured with a user data script(userdata.sh & userdata1.sh) that sets up the web server.when we click on the DNS Endpoint from the ALB it will show basic HTML page which is written in user data script.On refreshing the page again and again we can see the load distributed to diffrent instances in the  target group by the ALB.
