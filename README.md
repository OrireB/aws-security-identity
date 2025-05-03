# AWS Security and Identity

## 1. IAM User with Restricted Permissions

### A. Create IAM User
   1. Sign in to the AWS Management Console.
   2. Go to IAM > Users > Add users.
   3. Enter username: **AfinaTic-M4ACE**
   4. Axxess Type: Check the box - **Provide user access to the AWS Management Console - optional.**
   5. Check the box- **I want to create an IAM user**
   6. Set a custom password **(Check "Require password reset").**

### B. Assign Permissions
   1. Choose **Attach policies directly.**
   2. Select only **AmazonS3ReadOnlyAccess** or create a custom policy.
   3. Click Next > Create user.
**This gives the user limited read-only access to S3.**

### C. Test Access
   1. Log in with the newly created IAM user credentials at the AWS sign-in link.
   2. Attempt to create and delete a bucket.

### Actions Tested:
   - **Allowed:** Listing S3 buckets.
   - **Denied:** Creating or deleting S3 buckets.

### Expected Results:
   - User can view S3 buckets
   - User cannot modify S3 resources 

## 2. Set-up Multi-Factor Authentication (MFA) for IAM User
   1. Go to **IAM** > **Users** > **AfinaTic-M4ACE** > **Security credentials.**
   2. Under **Multi-factor authentication (MFA)**, click **Assign MFA device.**
   3. Choose **Virtual MFA device,** then use an app like **Google Authenticator.**
   4. Scan QR code and enter two consecutive codes.
   5. Save configuration.

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

