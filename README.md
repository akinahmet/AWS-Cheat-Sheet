# Amazon Web Services Cheat Sheet for beginners

## Create Instance
- Go to AWS console page
- Click on **Instances**
- Click on **Launch Instance**
- On `Step 1: Choose an Amazon Machine Image (AMI)`, click on **AWS Marketplace**
- Search for **Deep Learning**
- Choose **AWS Deep Learning AMI**
- On `Step 2: Choose an Instance Type`, choose **p2.xlarge**
- On `Step 6: Configure Security Group`, Add following inbound rules:
    - Custom TCP	TCP	8888	0.0.0.0/0	| For jupyter notebook
    - Custom TCP	TCP	8080	0.0.0.0/0 | For tensorboard

## AWS Server
### Connect to your instance with SSH.
```
ssh -i {path/to/.pem key file} ubuntu@{Public DNS}
ssh -i {path/to/.pem key file} ec2-user@{Public DNS}
