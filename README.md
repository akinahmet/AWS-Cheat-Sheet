# Amazon Web Services Cheat Sheet for beginners

## Create Instance
(A simple example for new learners. You can change and improve these settings as you learn.)

- Go to AWS console page
- Click on **EC2**
- Click on **Instances**
- Click on **Launch Instance**
- On `Name and Tags: Write a name` 
- On `Application and OS Images (Amazon Machine Image): Choose an Amazon Machine Image (AMI)`
- On `Instance Type: Choose an Instance Type, (You can choose free tier)`
- On `Key pair (login): You can create a new key pair (You must have a key pair in each region.)`
- On `Network settings: Set the security groups`
- On `Configure Storage, (8 GB is enough for now)`
- Click on **Launch Instance**
- You created an instance 💪

## AWS Server
### Connect to your instance with SSH.
ssh -i <....pem> ubuntu@<Your Public DNS> (When you choose Ubuntu as AMI)
ssh -i <....pem> ec2-user@<Your Public DNS> (When you choose Amazon Linux as AMI)

## AWS IAM (Identity & Access Management)
### What is IAM?
AWS IAM stands for Identity & Access Management and is the primary service that handles authentication and authorization processes within AWS environments.

### Creating IAM user 
Let's pretend that we only have the root account in the first place.
Create IAM user with Administrator access for your daily work
- Log in as a Root User
- Go to AWS console page
- Click on **IAM**
- Click on **Users**
- Click on **Add users**
- On `Set user details: Write a user name`
(You can enter multiple usernames at the same time)
- Select AWS access type
- On `Set permissions: Attach existing policies directly`
(You can copy permissions from existing user or if there is already a group you can choose add user group)
- Choose one or more policies
- Click on **Next Tags** and Add tags (optional)
- Click on **Next Review** 
- Click on **Create User** 
- You successfully created user(s) 
- You should keep Access key ID and Secret access key in a safe place.

### Creating IAM group





```




