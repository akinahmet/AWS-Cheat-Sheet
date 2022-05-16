# Amazon Web Services Cheat Sheet for beginners

## Create Instance
(A simple example for new learners. You can change and improve these settings as you learn.)

- Go to AWS console page
- Click on **EC2**
- Click on **Instances**
- Click on **Launch Instance**
- On `Name and Tags: Write a name`, 
- On `Application and OS Images (Amazon Machine Image): Choose an Amazon Machine Image (AMI)`
- On `Instance Type: Choose an Instance Type, (You can choose free tier)`
- On `Key pair (login): You can create a new key pair (You must have a key pair in each region.)`
- On `Network settings: Set the security groups`
- On `Configure Storage, (8 GB is enough for now)`
- Click on **Launch Instance**
- You created an instance 💪

## AWS Server
### Connect to your instance with SSH.
```
ssh -i <....pem> ubuntu@<Your Public DNS> (When you choose Ubuntu as AMI)
ssh -i <....pem> ec2-user@<Your Public DNS> (When you choose Amazon Linux as AMI)

## AWS IAM (Identity & Access Management)
### What is IAM?
AWS IAM stands for Identity & Access Management and is the primary service that handles authentication and authorization processes within AWS environments.

