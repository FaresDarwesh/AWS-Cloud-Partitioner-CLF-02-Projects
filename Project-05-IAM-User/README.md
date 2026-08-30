# Project 5: Creating an IAM User

## Objective
Create an IAM user with limited permissions following the principle of least privilege.

## AWS Services Used
- IAM (Identity and Access Management)

## Steps

### 1. Go to IAM Console
- Services → IAM → Users → Add users

### 2. Set User Details
- User name: `s3-readonly-user`
- Access type: ✅ Programmatic access ✅ AWS Management Console access
- Console password: Custom password
- Require password reset: ❌ Uncheck

### 3. Set Permissions
- Attach existing policies directly
- Search: `AmazonS3ReadOnlyAccess`
- Select it → Next → Create user

### 4. Save Credentials
- Download `.csv` file (contains Access Key ID & Secret Access Key)
- ⚠️ This is the ONLY time you can see the Secret Access Key!

### 5. Test Login
- Use the IAM sign-in URL (found in IAM Dashboard)
- Log in with the new user credentials
- Verify: Can view S3 buckets but CANNOT delete/create

## What I Learned
- Root user vs IAM user
- Principle of Least Privilege
- Programmatic access vs Console access
- Access Keys vs Passwords
- IAM sign-in URL

## Screenshot
![IAM User](screenshots/iam-user.png)

## Next
Project 6: RDS Database 🗄️
