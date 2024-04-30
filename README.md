# AWS Load Balancer Project - DevOps

## Overview
The objective of this project is to develop a robust understanding of **EC2 instances** and **Application Load Balancers (ALB)**. The goal is to create a highly available and high-performance traffic handling solution. Additionally, there is a plan to route traffic based on specific query strings, which could be used for a subscription service where users are directed to certain EC2 instances only if they possess a special premium key or query string. This project utilizes automation through the use of AMI images to configure cloned EC2 instances. With the integration of automation, the utilization of managed services, and the implementation of high availability and high-performance strategies using load balancers, this project provides substantial practice with DevOps methodologies.

## AWS Services Utilized

- **Amazon Simple Storage Service (S3):** Used for storing the `index.html` file for EC2 instances. This setup allows for easy retrieval of the file using `wget`, simplifying file transfer compared to traditional methods like SCP or FTP.
- **AWS EC2:** Hosts the `index.html` file and includes hard-coded information such as the instance's IP address and unique ID. This setup is crucial for understanding the behavior and configuration of the Load Balancer and Auto Scaling group.
- **AWS AMI:** Automates the installation of required software on initial EC2 instances. This allows for the replication of the instance setup without manual configuration.
- **AWS IAM:** Ensures best security practices by adhering to the principle of least privilege for accessing AWS services.

## Other Services Utilized

- **Apache:** Installed within the EC2 instance to serve the `index.html` file.

## Project Steps

### 1. Setting Up a Simple Storage Bucket (S3)
I started by creating an S3 bucket and configuring it for static web hosting. This setup later facilitated the easy transfer of the `index.html` file from the S3 bucket to the EC2 instance using the internet, insetad of using putty, winscp or scp methods that Im familar with.

<img src="https://i.imgur.com/MkL0eQv.png" height="80%" width="80%" alt="Code commit permissions"/>
<br />
<img src="https://i.imgur.com/O41m82w.png" height="80%" width="80%" alt="Code commit permissions"/>
<br />

### 2. Setting Up the Initial EC2 Instance
I then launched an EC2 instance and configured Apache to host the `index.html` file. This made the web content accessible via the instance's IP address.

<img src="https://i.imgur.com/kNMcgA0.png" height="80%" width="80%" alt="Code commit permissions"/>
<br />

### 3. Creating an Image of My Initial EC2 Instance (AWS AMI)
After manually installing necessary software like Apache on the original EC2 instance, I created an AMI of this instance to automate the setup process for future instances. This step significantly reduces setup time for additional instances needed for traffic management testing.

<img src="https://i.imgur.com/MTl52gi.png" height="80%" width="80%" alt="Code commit permissions"/>
<br />

### 4. Load Balancer Target Groups
With four instances ready for testing, I split them into two different target groups assigned to different availability zones (one in us-east-1 and the other in us-east-2). This configuration is intended to support health checks by the load balancer, allowing traffic redirection to available zones for enhanced availability.

<img src="https://i.imgur.com/ebpEozU.png" height="80%" width="80%" alt="Code commit permissions"/>
<br />
<img src="https://i.imgur.com/hMmERjZ.png" height="80%" width="80%" alt="Code commit permissions"/>
<br />

### 5. Application Load Balancer
Given that my project primarily involves HTTP traffic and does not require ultra-low latency, I chose the Application Load Balancer over a Network Load Balancer. I set up the ALB to manage traffic across the four instances. Initially, traffic between EC2 instances 1 and 2 is routed randomly, suitable for the low traffic conditions expected. For instances 3 and 4 in target group two, the ALB is configured to check for a specific query string in the request header. This setup enables directing users with the special premium key in the query string to these instances, laying the groundwork for a potential subscription service model.

## Video Demo of the finished project with the application load balancer working
[ALB Project](https://youtu.be/8PYNc-4RGvY)
