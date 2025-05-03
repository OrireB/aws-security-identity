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

### C. Testing IAM User Access
- **Action**: Attempted to create a new S3 bucket using the AWS Management Console
- **Outcome**: Access denied, as expected due to the `AmazonS3ReadOnlyAccess` policy.
- **Error Message**: `An error occurred (AccessDenied) when calling the CreateBucket operation: Access Denied`

### Expected Results:
   - User can view S3 buckets
   - User cannot modify S3 resources 

## 2. Set-up Multi-Factor Authentication (MFA) for IAM User
   1. Go to **IAM** > **Users** > **AfinaTic-M4ACE** > **Security credentials.**
   2. Under **Multi-factor authentication (MFA)**, click **Assign MFA device.**
   3. Choose **Virtual MFA device,** then use the **Google Authenticator.**
   4. Scan QR code and enter two consecutive codes.
   5. Save configuration.

### Testing MFA Setup
- **Action**: Logged in as `AfinaTic-M4ACE` using the AWS Management Console.
- **Outcome**: Prompted for MFA code using the **Google Authenticator.**, successfully logged in after entering the code.
- **Screenshot**: ![MFA Login]([screenshots/mfa-login-prompt.png](https://raw.githubusercontent.com/OrireB/aws-security-identity/5d93100ea28d60e0d74bffa2c72aad6d09566aaf/Testing%20MFA%20Setup.png))

## 3. Create Custom Policy and Attach to IAM Role
### A. Create Custom IAM Policy
   1. Go to **IAM** > **Policies** > **Create policy.**
   2. Choose JSON, paste:
   3. **Name:** `EC2StartStopDescribePolicy`
     - Policy allows starting/stopping EC2 instances

**JSON**

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeInstances",
        "ec2:StartInstances",
        "ec2:StopInstances"
      ],
      "Resource": "*"
    }
  ]
}

### B. Create and Attach IAM Role
   1. Go to **IAM** > **Roles** > **Create role.**
   2. Select **AWS service** > **EC2** (use case: allow EC2 to call AWS services).
   3. Attach your custom policy.
   4. **Name the role:** `EC2ControlRole`.

## Screenshots

Here are the key screenshots:

- **Screenshot 1**: IAM user creation
  ![IAM user creation](https://raw.githubusercontent.com/OrireB/aws-security-identity/7b248e5a11ac022deb0e8802373a2a1cf85a54ef/IAM%20user%20creation-AfinaTicM4ACE.png)

---

- **Screenshot 2**: Failed attempted access 
  ![CDenied access when trying to perform restricted actions](https://raw.githubusercontent.com/OrireB/aws-security-identity/7b248e5a11ac022deb0e8802373a2a1cf85a54ef/Failed%20attempted%20access.png)

---

- **Screenshot 3**: MFA setup confirmation
  ![MFA setup confirmation](https://raw.githubusercontent.com/OrireB/aws-security-identity/7b248e5a11ac022deb0e8802373a2a1cf85a54ef/MFA%20setup%20confirmation.png)

---

- **Screenshot 4**: Custom policy creation
  ![Custom policy creation](https://raw.githubusercontent.com/OrireB/aws-security-identity/7b248e5a11ac022deb0e8802373a2a1cf85a54ef/Custom%20policy%20creation.png)

---

- **Screenshot 5**: Role creation with attached policy.
  ![Role creation with attached policy.](https://raw.githubusercontent.com/OrireB/aws-security-identity/7b248e5a11ac022deb0e8802373a2a1cf85a54ef/Role%20creation%20with%20attached%20policy..png)

## Architectural Diagram

![Architecture](architecture-diagram.png)

