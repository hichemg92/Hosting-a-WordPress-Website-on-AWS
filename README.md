# WordPress Hosting on AWS with High Availability Architecture

## Project Overview

This project demonstrates how to host a WordPress website on AWS, leveraging a high-availability architecture. The deployment utilizes a wide range of AWS services and DevOps practices to ensure reliability, security, and scalability. 

The reference architecture diagram and deployment scripts are available in the [hichemg92/Hosting-a-WordPress-Website-on-AWS](#). This document outlines the key components, setup process, and scripts used in the deployment.

---

## Architecture Highlights

The WordPress website is deployed using the following AWS resources and configurations:

Host_a_WordPress_Website_on_AWS.png

1. **Networking**
   - Configured a **Virtual Private Cloud (VPC)** with public and private subnets across two Availability Zones for fault tolerance.
   - Deployed an **Internet Gateway** for internet connectivity.
   - Implemented **Security Groups** as a network firewall mechanism.
   - Set up **EC2 Instance Connect Endpoint** for secure connections to resources in both public and private subnets.

2. **Compute**
   - Hosted WordPress on **EC2 Instances** within private subnets for enhanced security.
   - Utilized an **Auto Scaling Group** to manage the number of EC2 instances dynamically.
   - Deployed an **Application Load Balancer (ALB)** for distributing traffic across instances in multiple Availability Zones.

3. **Storage**
   - Configured **Amazon EFS** for shared storage to host WordPress files.
   - Used **Amazon RDS** for WordPress database management.

4. **Scalability and Monitoring**
   - Leveraged **Auto Scaling Groups** for elasticity and fault tolerance.
   - Configured **AWS Certificate Manager** for secure communications (HTTPS).
   - Enabled **Amazon SNS** to send notifications about Auto Scaling activities.

5. **Domain and DNS**
   - Registered a domain name and set up DNS records using **Amazon Route 53**.

---

## Deployment Steps

### Prerequisites

- AWS account with required permissions.
- Registered domain name.
- SSH key pair for EC2 instance access.
- Git installed on your local machine.

### Steps to Deploy

#### 1. **Set Up Networking**
   - Create a VPC with public and private subnets across two Availability Zones.
   - Attach an Internet Gateway to the VPC.
   - Configure Security Groups for web servers and database access.

#### 2. **Launch EC2 Instances**
   - Use the provided launch template to configure the EC2 instances with the necessary software and configurations.

#### 3. **Install WordPress**
   - SSH into the EC2 instance and execute the `wordpress-setup.sh` script (provided below).
   - Install Apache, PHP, MySQL, and WordPress files.
   - Configure the WordPress `wp-config.php` file.

#### 4. **Configure Load Balancing and Auto Scaling**
   - Set up an Application Load Balancer with a target group.
   - Associate the target group with an Auto Scaling Group to handle dynamic traffic.

#### 5. **Enable HTTPS**
   - Use AWS Certificate Manager to generate an SSL certificate.
   - Attach the certificate to the Load Balancer.

#### 6. **Set Up Storage**
   - Attach Amazon EFS for shared storage and mount it on all EC2 instances.
   - Configure Amazon RDS for database connectivity.

#### 7. **Set Up Domain and DNS**
   - Use Amazon Route 53 to configure DNS records for your domain, pointing to the Load Balancer.

---

## Key Scripts

### WordPress Setup Script

```bash
# Switch to root user
sudo su
# Update software packages
sudo yum update -y
# Install Apache and PHP
sudo yum install -y httpd php php-mysqlnd php-fpm
sudo systemctl enable httpd
sudo systemctl start httpd
# Install MySQL and configure
sudo wget https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm
sudo dnf install -y mysql80-community-release-el9-1.noarch.rpm
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023
sudo dnf install -y mysql-community-server
sudo systemctl start mysqld
sudo systemctl enable mysqld
# Mount EFS
EFS_DNS_NAME=fs-064e9505819af10a4.efs.us-east-1.amazonaws.com
sudo mkdir -p /var/www/html
sudo mount -t nfs4 -o nfsvers=4.1 "$EFS_DNS_NAME":/ /var/www/html
# Download and configure WordPress
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
sudo cp -r wordpress/* /var/www/html/
sudo chown -R apache:apache /var/www/html
# Restart services
sudo systemctl restart httpd
```

### Auto Scaling Launch Template Script

```bash
#!/bin/bash
sudo yum update -y
sudo yum install -y httpd php php-mysqlnd php-fpm
sudo systemctl enable httpd
sudo systemctl start httpd
EFS_DNS_NAME=fs-02d3268559aa2a318.efs.us-east-1.amazonaws.com
echo "$EFS_DNS_NAME:/ /var/www/html nfs4 defaults 0 0" >> /etc/fstab
mount -a
sudo chown -R apache:apache /var/www/html
sudo systemctl restart httpd
```

---

## Repository Contents

- **Architecture Diagram**: Visual representation of the setup.
- **Deployment Scripts**: Scripts for WordPress installation and Auto Scaling configuration.
- **Documentation**: Detailed steps to replicate the deployment.

---

## Future Enhancements

- Automate deployment using **Terraform** or **CloudFormation**.
- Integrate with **AWS CloudWatch** for advanced monitoring.
- Implement CI/CD pipelines for continuous deployment.

---

## Contact

For any questions or suggestions, feel free to reach out! 

---
