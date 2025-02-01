# AWS-How-To

A guide on how to do the fundamental actions within AWS management console

## EC2
- [how to create an ec2][create-ec2]
- [how to ssh into your ec2][ssh-ec2]

## Elastic Beanstalk

## Lambda

## IAM

## S3
- [s3 permissions and bucket policies][s3-perm]

[home]:#aws-how-to
[s3-perm]:#s3-permissions-and-bucket-policies
[ssh-ec2]:#how-to-ssh-into-your-ec2
[create-ec2]:#how-create-an-ec2

### s3 permissions and bucket policies

<details>
<summary>
View Content
</summary>

1. go to iam
2. click users
3. create a new user
    - add name
    - provide access to the management console
    - make him an iam user
    - then create the user
4. go to s3 and create a bucket
5. after creating the bucket, click inside of it and go to properties
6. copy the bucket arn number
7. paste the arn inside this code block at the `Resource` property that
has the `my-example-bucket`

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets",
                "s3:GetBucketLocation"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::my-example-bucket/*"
            ]
        }
    ]
}
```
8. copy the example code above and go to newly created user account
9. In the permissions tab, click add permissions, and create inline policy
10. In the json tab, paste in the example code and click review policy
11. click create policy
12. login as the new user and go to s3 
(you should be able to see the buckets because the permissions allow it )
13. go to newly created bucket, and choose the properties tab
(verify that you don't have permissions to do anything)
14. go to the object tab and upload an image

</details>

[go back :house:][home]



### How to create an EC2
<details>
<summary>
View Content
</summary>

1. Log into management console and go to
    - Services > compute > ec2
    - The search bar and type in ec2
2. Click the "Launce instance" button
3. In the Instance Wizard Form 
    - Add the name of the instance and possibly add tags
    - [In Application and OS Images][ami-os]. Pick the AMI that you want to use for the OS ( or just leave it by default)
    - [In instance type][instance-type]. Choose the instance type that you believe your app needs
    - [In key pair(login)][key-pair]. Create a key pair, if you think you're going to need to SSH into it
    - [In network settings][net-settings]. Choose what type of VPC, security group, or security group name you want to assign to it
    - [In Configure storage][config-stor]. Choose the type of Block Storage you want to assign to your instance
    - [In advanaced details][adva-deta].You can do a lot of stuff. The User data section allows you add code that will be ran once the instance starts up

    [ami-os]:#more-on-application-and-os-images
    [instance-type]:#more-on-instance-type
    [key-pair]:#more-on-key-pair
    [net-settings]:#more-on-network-settings
    [config-stor]:#more-on-configure-storage
    [adva-deta]:#more-on-advanced-details

    #### More on Application and OS images

    #### More on Instance type

    #### More on Key Pair

    #### More on Network settings

    #### More on Configure storage

    #### More on Advanced details

</details>

[go back :house:][home]
