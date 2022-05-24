# Amazon Web Services Cheat Sheet for beginners

## AWS EC2

### Create Instance
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

### Use Cloudformation to create an EC2 instance
- Go to AWS console page
- Create a template on your local machine. Click [here](https://docs.aws.amazon.com/quicksight/latest/APIReference/API_CreateTemplate.html) for more details of template creating.
- At AWS Consol Click on **services** and search for Cloudformation.
- You are at Cloudformation main dashboard 
- Click on **Create Stack**
- Select "Template is ready" (assuming we created a template above)
- Select "Upload a template file" and upload your template
(If you have already a template in AWS S3 you can choose Amazon S3 URL)
- Click on **Next** and enter a Stack name
- Choose the instance type, and existing key from your account.
- Click on **Next**
- Tags are optional, you may or may not add tags in this step
- Now you don't need to set 'Configure stack options'
- Review and click **Create Stack** 


## AWS Server

### Connect to your instance from your VS Code
(We have already created an instance)
- Go to AWS console page
- Click on **EC2**
- Click on **Instances**
- Select previously created instance
- Click on **Connect**
- Find 'Connect to your instance using its Public DNS'
- Copy this link
- Go to your VS Code
- Open a Terminal in the directory
- Open terminal in the directory where the your key is
- Paste the link
- Write 'yes'
- And we connected from our computer to our EC2💪

## AWS EC2 Volumes

###  Extend Root Volume
(We have already created an Amazon Linux 2 instance with default ebs volume and ssh)
- Go to AWS console page
- Click on **EC2**
- Click on **Instances**
- Connect your Instance
- List block devices (lsblk)

```bash
   lsblk
```
- Verify the file system in use for each volume

```bash
   df -h
```

- Check file system of the root volume's partition.

```bash
   sudo file -s /dev/xvda1
```

- Go to Volumes, select instance's root volume and modify it (increase capacity 8 GB >> 12 GB)

```bash
   sudo file -s /dev/xvda1
```

-  Extend partition 1 on the modified volume and occupy all newly avaiable space.

```bash
   sudo growpart /dev/xvda 1
```

- Resize the xfs file system on the extended partition to cover all available space.

```bash
   sudo xfs_growfs /dev/xvda1
```

- List block devices (lsblk) and file system disk space usage (df) of the instance again. Partition and file system should be extended.

```bash
   lsblk
```
```bash
   df -h
```

## Install Nginx Web Server on EC2 Linux 2

(We have already created an Amazon Linux 2 instance)
- Connect to your instance with SSH.
```bash
   ssh -i [Your Key pair] ec2-user@[Your EC2 IP / DNS name]
```

- Update the installed packages and package cache on your instance.
```bash
   sudo yum update -y
```

- Install the Nginx Web Server.
```bash
   sudo amazon-linux-extras install nginx1
```

- Install the Nginx Web Server.
```bash
   sudo amazon-linux-extras install nginx1
```

- Start the Nginx Web Server.
```bash
   sudo systemctl start nginx
```

- Check from browser with public IP/DNS


## Creating an Instance with Launch Template and Versioning

### Creating Launch Templates

- Open the Amazon EC2 console
```bash
   https://console.aws.amazon.com/ec2/.
```

- On the navigation pane, under `INSTANCES`, choose `Launch Templates`.

- Click on `Create launch template`.

- Enter a name and provide a description for the initial version of the launch template.


Name                         : MyFirstTemplate
Template version description : Origin


- `Autoscaling Guidance` (Keep it as default)


- `Template Tags` (Keep it as is)


- `Source Template` (Keep it as is)


- `Amazon machine image` (AMI)


Choose Amazon Linux 2 AMI (HVM)

- `Instance Type`


Choose t2.micro


- `Key pair`


Please select your key pair (pem key) that is created before


- `Security groups`

Create a Security Group (SSH 22, HTTP 80 ----> anywhere(0.0.0.0/0))


- `Storage (volumes)`


we keep it as is  (Volume 1 (AMI Root) (8 GiB, EBS, General purpose SSD (gp2)))


- `Resource tags`


Key             : Name
Value           : Webserver-Origin
Resource type   : Instance


- `Network interfaces` (Keep it as is)


- `Advance details` (Keep it as is)

-  Click on `Create Launch Template`

- Select `MyFirstTemplate` ---> `Actions` ---> `Launch Instance from Template`

-  Enter number of instance as `1`.

- Keep the rest of settings as is and click the `Launch instance from template` at the bottom.

- Go to EC2 Instance menu and show the created instance.

### Launch Template Version 2

- Go to `Launch Template` menu on the left hand pane

- Select template named `MyFirstTemplate` ---> `Actions` ---> `Modify template (Create New Version)`

- `Template version description`

You can write version and description


- `Key pair`

Select your .pem file name


- `Resource tags`


Key             : Name
Value           : Webserver-V2
Resource type   : Instance


- Go to `Advance Details` on the bottom and add the script given below into the `user data` field.


#!/bin/bash

yum update -y
amazon-linux-extras install nginx1
systemctl enable nginx
systemctl start nginx


- Go to `Launch Template` Menu and click on `MyFirstTemplate`.

- You can see new version on the `Versions` tab.


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

- Log in as a IAM User (we already created IAM user above)
- Go to AWS console page
- Click on **IAM**
- Click on **User groups**
- Click on **Create group**
- On `Name the group: Write a group name`
Add users to the group - Optional (You can now add users to the group or later)
- On Attach permissions policies - Optional (You can choose one or more policies, you can make it later)
- Click on **Create Group** 
- You successfully created a group
- If we didn't add above, we can add users now
- Click on **IAM**
- Click on **User groups**
- Click on the group name you created earlier
- Click on **Add users**
- Choose user(s)
- Click on **Add users**





```




