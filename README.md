# AWS-How-To

A guide on how to do the fundamental actions within AWS

## EC2
- [how to create an ec2][create-ec2]
- [how to ssh into your ec2][ssh-ec2]

## Elastic Beanstalk

## Lambda

[ssh-ec2]:#how-to-ssh-into-your-ec2
[create-ec2]:#how-create-an-ec2
[home]:#aws-how-to

### How to create an EC2

1. Log into management console and go to
    - Services > compute > ec2
    - The search bar and type in ec2
2. Click the "Launce instance" button
3. In the Instance Wizard Form 
    - Add the name of the instance and possibly add tags
    - In Application and OS Images. Pick the AMI that you want to use for the OS ( or just leave it by default)
    - In instance type. Choose the instance type that you believe your app needs
    - In key pair(login). Create a key pair, if you think you're going to need to SSH into it
    - In network settings. Choose what type of VPC, security group, or security group name you want to assign to it
    - Choose the type of Block Storage you want to assign to your instance



