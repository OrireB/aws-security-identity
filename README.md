# AWS Security and Identity

## 1. IAM User with Restricted Permissions

### A. Create IAM User
### 6. Implement a Security Group for Traffic Control:
   1. Sign in to the AWS Management Console.
   2. 

Go to IAM > Users > Add users.

Enter username: limited-user.

Select Access key - Programmatic access and AWS Management Console access.

Set a custom password (uncheck "Require password reset").

User Details:
Username: limited-user

Permissions: Read-only access to Amazon S3

Steps:
Navigate to IAM > Users > Add user.

Enable AWS Management Console access and programmatic access.

Attach policy: AmazonS3ReadOnlyAccess.

Complete user creation.

## 2. Multi-Factor Authentication (MFA)
- Enabled Virtual MFA
- Tested login and received MFA prompt

## 3. Custom IAM Policy and Role
- Created `EC2StartStopPolicy`
- Policy allows starting/stopping EC2 instances
- Attached to `EC2OperatorRole`

## Screenshots

Here are the key screenshots:

- **Screenshot 1**: RDS instance
  ![RDS instance dashboard showing the status as “Available”]()

---

- **Screenshot 2**: MySQL Connected Successfully
  ![Connected MySQL with database overview]()

---



### 6. Implement a Security Group for Traffic Control:
   - **Step 1**: Create a Security Group.
   - Go to the Security Groups section in the EC2 dashboard.
   - Click on Create Security Group.
     - **Name**: MySecurityGroup-test
     - **Description**: Security group for my test EC2 instances
     - **VPC**: MyVPC-test

   - **Step 2: Add Inbound Rules**
   - Click on Inbound Rules and then click Edit inbound rules.
   - Add rules to allow traffic from the NAT Gateway
     - **Name**: MySecurityGroup-test
     - **Type**: SSH
     - **Protocol**: TCP
     - **Port Range**: 22
     - **Source**: My IP (Enter the NAT Gateway's IP address )
     - **Description**: Allow SSH from NAT Gateway.
   - Click Save rules.

   - **Step 3: Add Outbound Rules**
     - By default, security groups allow all outbound traffic, so you usually don’t need to modify outbound rules unless you have specific needs.

   - **Step 4: Apply the Security Group**
     - Attach this security group to your EC2 instances.

## Architectural Diagram

![Architecture](architecture-diagram.png)

