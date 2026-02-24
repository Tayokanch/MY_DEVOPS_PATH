# Block Storage Services on AWS


`Elastic Block Storage (EBS)`
- Block Storage breaks up data into blocks and then stores those blocks as seperate peiece, each within a unqiue identifier
- It can be used as a Traditional File system
- EBS Volumes can be mounted & Booted
- It can be used as an Extral Hard Drive for rources like `EC2`
- It is bootable, which means `operating system` can be installed on it
- They can be used to backup database
- When EBS used with an EC2 Insstance, they must be in the same AZ


## How To Use it

- Create an `Ec2 Instance`
- Create An `EBS `in the same AZ that the Ec2 Instance is created 
- Click on the `EBS` we just create, Click on **Action** and Attach the `EBS Volume` to the `EC2`
- SSH to the EC2 Instance and , run command `lsblk` to list all the block storage attached to it