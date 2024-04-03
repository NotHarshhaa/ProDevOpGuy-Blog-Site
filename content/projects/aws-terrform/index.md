---
title: "Deploy Two-Tier AWS ☁️ Infrastructure with Terraform 🛠️"
summary: Terraform project for deploying a Two-Tier architecture on AWS!
date: 2024-04-03
weight: 1
aliases: ["/aws-terraform"]
tags: ["AWS", "Cloud", "EKS", "Terraform"]
author: ["H A R S H H A A"]
cover:
  image: images/aws-terraform.png
  hiddenInList: true
  UseHugoToc: true
---

[![LinkedIn](https://img.shields.io/badge/Connect%20with%20me%20on-LinkedIn-blue.svg)](https://www.linkedin.com/in/harshhaa-vardhan-reddy/)
[![GitHub](https://img.shields.io/github/stars/NotHarshhaa.svg?style=social)](https://github.com/NotHarshhaa)
[![AWS](https://img.shields.io/badge/AWS-%F0%9F%9B%A1-orange)](https://aws.amazon.com)
[![Terraform](https://img.shields.io/badge/Terraform-%E2%9C%A8-lightgrey)](https://www.terraform.io)

![](https://miro.medium.com/v2/resize:fit:736/1*O1wPuZ_R1dDBCqGvMLIwkw.gif)

## **Introduction**

In the world of cloud computing, infrastructure as code (IaC) plays a pivotal role in automating the deployment and management of resources. This blog post provides a step-by-step guide on creating a Two-Tier architecture on AWS using Terraform. We’ll explore the essential services involved, ensuring high availability, security, and scalability for hosting a static website.

Also, we are adopting a modular approach with enhanced security measures. The infrastructure is organized into dedicated modules, ensuring a scalable, maintainable, and secure deployment.

## **Directory Overview**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705733395583/e6cbad1b-3cc8-4f6f-8031-2350f84b7892.png)

## **Directory Overview**

* **DevOps Project-11:**
    
* [`backend.tf`](https://www.linkedin.com/in/aman-devops/): Configuration for Terraform backend, specifying where to store the Terraform state.
    
* [`main.tf`](https://www.linkedin.com/in/aman-devops/): Main Terraform configuration orchestrating the deployment.
    
* [`variables.tf`](https://www.linkedin.com/in/aman-devops/): Definition of variables used in the main Terraform configuration.
    
* `variables.tfvars`: Input values for the defined variables.
    
* **modules:**
    
* **alb-tg:**
    
* [`gather.tf`](https://www.linkedin.com/in/aman-devops/): Terraform script to gather information about the Application Load Balancer (ALB) and Target Group (TG).
    
* [`main.tf`](https://www.linkedin.com/in/aman-devops/): Main Terraform configuration for ALB and TG.
    
* [`variables.tf`](https://www.linkedin.com/in/aman-devops/): Definition of variables used in the ALB and TG module.
    
* **aws-autoscaling:**
    
* [`deploy.sh`](https://www.linkedin.com/in/aman-devops/): Shell script for deploying the Auto Scaling Group.
    
* [`gather.tf`](https://www.linkedin.com/in/aman-devops/): Terraform script to gather information about the Auto Scaling Group.
    
* [`main.tf`](https://www.linkedin.com/in/aman-devops/): Main Terraform configuration for the Auto Scaling Group.
    
* [`variable.tf`](https://www.linkedin.com/in/aman-devops/): Definition of variables used in the Auto Scaling Group module.
    
* **aws-iam:**
    
* [`iam-instance-profile.tf`](https://www.linkedin.com/in/aman-devops/): Terraform configuration for IAM instance profile.
    
* `iam-policy.json`: JSON file containing the IAM policy.
    
* [`iam-policy.tf`](https://www.linkedin.com/in/aman-devops/): Terraform configuration for IAM policy.
    
* `iam-role.json`: JSON file containing the IAM role.
    
* [`iam-role.tf`](https://www.linkedin.com/in/aman-devops/): Terraform configuration for IAM role.
    
* [`variables.tf`](https://www.linkedin.com/in/aman-devops/): Definition of variables used in the IAM module.
    
* **aws-rds:**
    
* [`gather.tf`](https://www.linkedin.com/in/aman-devops/): Terraform script to gather information about the RDS cluster.
    
* [`main.tf`](https://www.linkedin.com/in/aman-devops/): Main Terraform configuration for the RDS cluster.
    
* [`variables.tf`](https://www.linkedin.com/in/aman-devops/): Definition of variables used in the RDS module.
    
* **aws-vpc:**
    
* [`main.tf`](https://www.linkedin.com/in/aman-devops/): Main Terraform configuration for the Virtual Private Cloud (VPC) and other Networking Services like Public/Private Subnet, ElasticIP, etc.
    
* [`variables.tf`](https://www.linkedin.com/in/aman-devops/): Definition of variables used in the VPC module.
    
* **aws-waf-cdn-acm-route53:**
    
* [`acm.tf`](https://www.linkedin.com/in/aman-devops/): Terraform configuration for ACM (Amazon Certificate Manager).
    
* [`cdn.tf`](https://www.linkedin.com/in/aman-devops/): Terraform configuration for CDN (Content Delivery Network).
    
* [`gather.tf`](https://www.linkedin.com/in/aman-devops/): Terraform script to gather information about WAF, CDN, ACM, and Route 53.
    
* [`route53.tf`](https://www.linkedin.com/in/aman-devops/): Terraform configuration for Route 53.
    
* [`variables.tf`](https://www.linkedin.com/in/aman-devops/): Definition of variables used in the WAF, CDN, ACM, and Route 53 modules.
    
* [`waf.tf`](https://www.linkedin.com/in/aman-devops/): Terraform configuration for AWS WAF (Web Application Firewall).
    
* **security-group:**
    
* [`gather.tf`](https://www.linkedin.com/in/aman-devops/): Terraform script to gather information about security groups.
    
* [`main.tf`](https://www.linkedin.com/in/aman-devops/): Main Terraform configuration for security groups.
    
* [`variable.tf`](https://www.linkedin.com/in/aman-devops/): Definition of variables used in the security group module.
    

This modular approach enhances the project’s maintainability, making it easier to manage and scale as your infrastructure requirements evolve. Each module focuses on a specific aspect of the infrastructure, promoting reusability and clarity in configuration.

## **Pre-requisites**

Before diving into the infrastructure creation, make sure you have the following:

* An AWS Account
    
* Terraform installed on your local machine
    
* AWS Access and Secret Access keys configured
    
* Domain Name Configured manually and add the Name Servers to your Domain Provider
    

## **Step-by-Step Guide**

To get started, clone the repository using the following command:

```bash
git clone https://github.com/NotHarshhaa/DevOps-Projects
```

Navigate to the project folder:

```bash
cd DevOps-Projects/DevOps Project-11
```

# **Planning and Deployment**

Execute the following Terraform commands to plan and deploy the infrastructure:

```bash
terraform plan -var-file=variables.tfvars
```

![](https://miro.medium.com/v2/resize:fit:736/0*akgutqcuOytwyeFr)

```bash
terraform apply -var-file=variables.tfvars --auto-approve
```

![](https://miro.medium.com/v2/resize:fit:736/0*GwqWrmyNzsdrOfF5)

Once the deployment is complete, you can inspect the created services using the provided snippets for each service.

## **VPC & Other Networking related Services**

**VPC**

![](https://miro.medium.com/v2/resize:fit:736/0*bTcoJoGjlg6ama3c)

**Public and Private Subnets**

![](https://miro.medium.com/v2/resize:fit:736/0*2VWNj0x3QI9FcHwm)

**Public and Private Route tables**

![](https://miro.medium.com/v2/resize:fit:736/0*p9tDNlLzWHy9X4Y2)

**Internet Gateway**

![](https://miro.medium.com/v2/resize:fit:736/0*6ETHLCPnh6ScG03w)

**Elastic IP addresses**

![](https://miro.medium.com/v2/resize:fit:736/0*gR3KFl_WY8e5ddzP)

**NAT Gateways**

![](https://miro.medium.com/v2/resize:fit:736/0*Ge6MwFoqlok3UBq4)

**Security Groups**

![](https://miro.medium.com/v2/resize:fit:736/0*Molv2WHfNmwfRmuJ)

## **EC2 & AutoScaling Group**

**Launch template**

![](https://miro.medium.com/v2/resize:fit:736/0*Q2Sd8xEyiah7Djdb)

**AutoScaling Group**

![](https://miro.medium.com/v2/resize:fit:736/0*C618R7r4U4-kmX3B)

## **Target Group & Load Balancer**

**Target Group**

![](https://miro.medium.com/v2/resize:fit:736/0*EsEEVf7ApGKkQTFe)

**Load balancer**

![](https://miro.medium.com/v2/resize:fit:736/0*QTCPt2j7Gd5OpURt)

## **Database**

**Subnet Group for RDS**

![](https://miro.medium.com/v2/resize:fit:736/0*rLHsMTvRh_sw4-rm)

**RDS Cluster**

![](https://miro.medium.com/v2/resize:fit:736/0*jKUP9f-xQhkbRy3M)

## **After Core Service, Deploy Service on Server**

**Route53**

![](https://miro.medium.com/v2/resize:fit:736/0*W0-Fvu87ANSGoUj4)

**AWS Certificate Manager**

![](https://miro.medium.com/v2/resize:fit:736/0*HdzXL7d29RUWzZ2z)

**AWS Web Application Firewall**

![](https://miro.medium.com/v2/resize:fit:736/0*N4z4VUhf2th8e36d)

**CloudFront**

![](https://miro.medium.com/v2/resize:fit:736/0*AQ3ZkMLau34YUSt2)

**IAM Role**

![](https://miro.medium.com/v2/resize:fit:736/0*94hZ3hfPQZ2AsRi2)

**IAM Policy**

![](https://miro.medium.com/v2/resize:fit:736/0*ch9SQWcsk39ILv0J)

**IAM instance profile**

![](https://miro.medium.com/v2/resize:fit:736/0*pRXh28MOhC4rEJcy)

## **TF State file and State lock**

Backend- TF State file stored on S3

![](https://miro.medium.com/v2/resize:fit:736/0*r5Rl9HOFrpnMdf88)

**TF State lock file**

![](https://miro.medium.com/v2/resize:fit:736/0*ylscrtYceyI1Sgna)

Once the deployment is completed, you can enter your domain name in the browser to validate whether your servers are perfectly running or not.

As you can see in the below snippet, the Application is running

![](https://miro.medium.com/v2/resize:fit:736/0*yDhfH8HxGO1EK4AW)

## **Clean-up**

When you’re done exploring the Two-Tier architecture and want to avoid incurring unnecessary costs, follow these steps to clean up the resources:

Run the following command to initiate the destruction of the infrastructure.

```bash
terraform destroy -var-file=variables.tfvars --auto-approve
```

![](https://miro.medium.com/v2/resize:fit:736/1*FiUFrihAMmQz7LO0BNJvfQ.png)

Delete the Repository (Optional):

* If you cloned the Git repository for this project and no longer need it, you can delete it locally.
    

```bash
rm -rf DevOps-Projects
```

This step is optional and depends on whether you plan to reuse the repository for future exploration.

By following these clean-up steps, you ensure that AWS resources are properly decommissioned, and you won’t incur unnecessary charges. Always exercise caution when performing destructive actions like `terraform destroy` to avoid unintended consequences.

## **Conclusion**

In this comprehensive guide, we embarked on a journey to deploy a Two-Tier architecture on AWS using Terraform. Embracing a modular approach with enhanced security measures, our infrastructure is organized into dedicated modules, offering scalability, maintainability, and robust security.

Happy coding!

🚀 **Follow for more DevOps content, tips and tricks, and Hands-On Project Implementation.**

## Support 💖

* Help spread the word about ProDevOpsGuy by sharing it on social media and recommending it to your friends. 🗣️
* You can also sponsor 🏅 on [Github Sponsors](https://github.com/sponsors/NotHarshhaa)
