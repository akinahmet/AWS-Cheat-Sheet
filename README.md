# Amazon Web Services Cheat Sheet for beginners

## Create Instance
- Go to AWS console page
- Click on **EC2**
- Click on **Instances**
- Click on **Launch Instance**
- On `Name and Tags: Write a name (AMI)`, 
- On `Application and OS Images (Amazon Machine Image): Choose an Amazon Machine Image (AMI)
- On `Instance Type: Choose an Instance Type, (You can choose free tier)`
- On `Key pair (login): You can create a new key pair (You must have a key pair in each region.)`
- On `Network settings: Set the security groups`
- On `Configure Storage, (8 GB is enough for now)`
- Click on **Launch Instance**

## AWS Server
### Connect to your instance with SSH.
```
ssh -i {path/to/.pem key file} ubuntu@{Public DNS}
ssh -i {path/to/.pem key file} ec2-user@{Public DNS}
