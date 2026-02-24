# File Storage in AWS

`Amazon Elastic File System (Amazon EFS)`
- This is similar to our computer stores files/folders
- With EFS we can store data on in ahierarchical structure of files and folders just like we do on our computer
- This filesystem can be created, accessed remotely
- file storage can be mounted
- Its not bootable, so we can install OS on it



## How to use it

- Create an `Ec2 Instance`
- Create An `EFS `, Select the Mount Target, Security Group(For Firewall) and Subnet ID
- Go to EC2, install EFS Utils to be able to connect with the EFS by (sudo yum install -y amazon-efs-utils)
- Then mount the EFS volume to the EC2 by running (sudo mount.efs the-efs-instance-id-we-created /foldername)
- **NOTE**: A single `EFS instance` can be mounted on multiple EC2 instance