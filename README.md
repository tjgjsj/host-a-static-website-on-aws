# Hosting a Static Website on AWS

This repository contains scripts and configuration files used to deploy a static HTML web application on AWS infrastructure. Below is an overview of the components and configurations utilized in this project:

### Infrastructure Components:
1. **Virtual Private Cloud (VPC)**:
   - Configured with public and private subnets across two availability zones for redundancy and fault tolerance.

2. **Internet Gateway**:
   - Facilitates connectivity between VPC instances and the wider Internet.

3. **Security Groups**:
   - Implemented as a network firewall mechanism to control traffic to EC2 instances.

4. **Availability Zones**:
   - Utilized two availability zones to enhance system reliability.

5. **Subnet Configuration**:
   - Public subnets used for infrastructure components like the NAT Gateway and Application Load Balancer.
   - Web servers (EC2 instances) positioned within private subnets for enhanced security.
   - Instances in private application and data subnets can access the Internet via the NAT Gateway.

6. **EC2 Instance Connect Endpoint**:
   - Implemented for secure connections to assets within both public and private subnets.

7. **Application Load Balancer (ALB)**:
   - Employed to evenly distribute web traffic to an Auto Scaling Group of EC2 instances across multiple Availability Zones.

8. **Auto Scaling Group**:
   - Used to automatically manage EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.

### Deployment Process:
The following script outlines the deployment process for hosting the static website on AWS:

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su
# Update all installed packages to their latest versions
yum update -y
# Install Apache HTTP Server
yum install -y httpd
# Change the current working directory to the Apache web root
cd /var/www/html
# Install Git
yum install git -y
# Clone the project GitHub repository to the current directory
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd
# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

### Additional Configurations:
- **Version Control and Collaboration**:
  - Web files are stored on GitHub for version control and collaboration.

- **Security**:
  - Application communications are secured using a Certificate Manager.
  - Simple Notification Service (SNS) is configured to alert about activities within the Auto Scaling Group.

- **Domain Registration and DNS Setup**:
  - Registered the domain name and set up a DNS record using Route 53.
