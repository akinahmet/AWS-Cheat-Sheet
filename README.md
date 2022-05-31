# Amazon Web Services Cheat Sheet for beginners

## AWS Elastic Compute Cloud (EC2)

### Create security group
(We will use secutity group in the next steps.)

- Open the Amazon **EC2** console.
- Choose `Security Groups` on the left-hand menu,
- Click the `Create Security Group` tab.
- You will see this:

```text
Security Group Name  : Please write a name
Description         : Please write a description
VPC                 : `Default VPC`
Inbound Rules:
    - Type: SSH----> Source: Anywhere
    - Type: HTTP ---> Source: Anywhere
Outbound Rules: Keep it as it is
Tag:
    - Key   : Name
    - Value : Please write value
```

- Click `Create Security Group` button.


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

### Create Instance with user data
(Almost same as above)
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
- Click on the `Advanced details` at the bottom,
- Go to user data,
- (With apache) Open the file `user_data_for_apache_server.txt` in this repository and copy content,
or
- (With nginx) Open the file `user_data_for_nginx.txt` in this repository and copy content,
- Paste it in user data,
- Click on **Launch Instance**

### Connect to your instance (method1)
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

### Connect to your instance (method2)

(We have already created an instance)
- Go to AWS console page and copy your puplic IP,
- Open your VS Code,
- Click on **Open a remote window** (bottom left),
- Click on **Open ssh configuration file**
- Edit config file

   `TCPKeepAlive` yes

   `ServerAliveInterval` 60

   `Host` You can write your name

   `HostName` Your puplic IP

   `IdentityFile` Your pem file path

   `User` ec2-user  for Amazon linux 

- Save and close
- Again Click on **Open a remote window**
- Click on **connect to host**
- And continue ...

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

### Create a target group
(Assume we create already two instances)

- Go to AWS console page
- Click on **EC2**
- Click on **Target Groups**
- Click on **Create Target Group** 
- Basic configuration.

```text
Choose a target type    : Instances
Target Groups Name      : Please write a name
Protocol                : HTTP
Port                    : 80
VPC                     : Default
Protocol version        : HTTP1
```

- Health checks

```text
Health check protocol   : HTTP
Health check path       : /
```

- Advance Health check settings.

```text
Port                    : Traffic port
Healthy treshold        : 5
Unhealthy treshold      : 2
Timeout                 : 5 seconds
Interval                : 10 seconds
Succes codes            : 200
```

- Tags

```text
Key                     : Name
Value                   : Please write value
```

- Click on 'next'
- Select two instances that is created from Launch Template before and add to them to the target group.

```text
Ports for the selected instances : 80
```
- Click `Include as pending below` button.
- Show that two instances are added to the target group.
- Click `Create target group` button.


###  EC2 Extend Root Volume
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

### Install Nginx Web Server on EC2 Linux 2

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

### Launch Template Versioning

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

## AWS Simple Storage Service (S3)

### What is S3?
Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. 

### Creating a S3 bucket

- Open S3 Service from AWS Management Console.
- Click on **Create bucket**
- Write a bucket name 
   Bucket name must be unique and must not contain spaces or uppercase letters.
- Select a region.
- `Object Ownership` (ACLs enabled - Bucket owner preferred)
- `Block all public access` Checked (KEEP BlOCKED)
- `Versioning`(Disabled)
- `Tagging` (0 Tags)
- `Default encryption`(None)
- `Object-level logging` (Disabled)
-  Click on **Create bucket**
- We created a bucket 

(If you want to create a a new Bucket for Static Website, also do the following steps)

- ...



