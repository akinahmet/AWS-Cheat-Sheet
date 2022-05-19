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




