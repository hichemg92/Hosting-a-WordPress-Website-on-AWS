# Hosting a WordPress Website on AWS

This project demonstrates how to host a WordPress website on AWS, utilizing various AWS services and resources to ensure reliability, security, scalability, and high availability. The deployment process, scripts, and architecture reference diagram are available in this [GitHub repository](<insert-your-repo-link>).

## **Project Overview**

This WordPress hosting project employs a robust and scalable infrastructure setup, leveraging AWS best practices. The following AWS resources and services were utilized:

### **AWS Resources and Architecture:**
1. **Virtual Private Cloud (VPC):**  
   Configured with both public and private subnets across two different Availability Zones (AZs) for high availability.
   
2. **Internet Gateway:**  
   Facilitates Internet connectivity for instances in public subnets.

3. **Security Groups:**  
   Act as a network firewall to control inbound and outbound traffic to instances.

4. **Availability Zones:**  
   Utilized two AZs to ensure fault tolerance and enhance system reliability.

5. **Public Subnets:**  
   Host critical infrastructure components, including the NAT Gateway and Application Load Balancer.

6. **EC2 Instance Connect Endpoint:**  
   Ensures secure connectivity to instances within public and private subnets.

7. **Private Subnets:**  
   Hosts web servers (EC2 instances) to enhance security.

8. **NAT Gateway:**  
   Enables instances in private subnets to access the Internet securely.

9. **EC2 Instances:**  
   Used to host the WordPress application.

10. **Application Load Balancer:**  
   Distributes incoming web traffic evenly to EC2 instances in the Auto Scaling Group across multiple AZs.

11. **Auto Scaling Group:**  
   Automatically manages the number of EC2 instances to maintain website availability, scalability, and fault tolerance.

12. **Elastic File System (EFS):**  
   Shared file storage system used to ensure data consistency across multiple instances.

13. **Relational Database Service (RDS):**  
   Hosts the WordPress database to provide scalable and managed database solutions.

14. **Simple Notification Service (SNS):**  
   Configured to send alerts for Auto Scaling Group activities.

15. **Route 53:**  
   Used for domain registration and DNS configuration.

16. **Certificate Manager:**  
   Secured application communications with SSL/TLS certificates.

17. **Version Control (GitHub):**  
   Web files and deployment scripts stored for collaboration and version control.

---

## **Deployment Diagram**
Refer to the architecture diagram in the repository: [Deployment Diagram](<Host_a_WordPress_Website_on_AWS.png>).

---

## **Setup Instructions**
### **Pre-requisites:**
1. An AWS account with the necessary permissions to provision resources.
2. A registered domain name for DNS configuration in Route 53.
3. A GitHub account to clone the repository.

### **Steps:**
1. Clone the repository:  
   ```bash
   git clone <repository-url>
   cd <repository-folder>
   ```
2. Configure AWS CLI with your credentials:  
   ```bash
   aws configure
   ```
3. Deploy the infrastructure using the provided scripts:  
 [Scripts Directory](<Bash-Script-for-aws-launch-template>)

4. Once the infrastructure is provisioned, deploy the WordPress application to the EC2 instances.
5. Configure SSL/TLS certificates via AWS Certificate Manager.
6. Set up DNS records in Route 53 to point your domain to the Load Balancer.
7. Verify the WordPress website is accessible via the domain name.

---

## **Key Features**
- **Scalable Infrastructure:** Automatic scaling of EC2 instances based on traffic.
- **High Availability:** Multi-AZ deployment ensures fault tolerance.
- **Secure Architecture:** Private subnets and Security Groups for enhanced security.
- **Reliable Storage:** EFS for shared file storage and RDS for database hosting.
- **Monitoring and Notifications:** SNS alerts for scaling activities.

---

## **Resources**
- Deployment scripts: [Scripts Directory](<Bash-Script-for-aws-launch-template>)
- Reference diagram: [Architecture Diagram](<Host_a_WordPress_Website_on_AWS.png>)
- AWS Documentation:  
  - [WordPress Hosting Best Practices](https://aws.amazon.com/architecture/wordpress/)
  - [EC2 Documentation](https://docs.aws.amazon.com/ec2/)

---

## **Contributing**
Contributions are welcome! Please fork the repository and submit a pull request with your changes.

---

## **License**
This project is licensed under the [MIT License](<insert-link-to-license>).

--- 

If you'd like to refine any details, let me know!
