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
- [configure replication and lifecycle][s3-rep]
- [s3 event notifications][s3-evt-not]
- [s3 presigned urls][s3-pre-url]

[home]:#aws-how-to
[s3-perm]:#s3-permissions-and-bucket-policies
[ssh-ec2]:#how-to-ssh-into-your-ec2
[create-ec2]:#how-create-an-ec2
[s3-rep]:#configure-replication-and-lifecycle
[s3-evt-not]:#s3-event-notifications
[s3-pre-url]:#s3-presigned-urls

### s3 presigned urls

<details>
<summary>
View Content
</summary>

- create a bucket
- upload a file
- try to acccess the file
- open a new tab to go cloudshell
- type in this command to create a pre-signed url

```

```

</details>

[go back :house:][home]


### s3 event notifications

<details>
<summary>
View Content
</summary>

- create a bucket
- go to sns and create a new topic
    - click create a subscription
    - choose the protocol as email
    - in the endpoint field, add in the email address you want to send the notification to
    - if email address is new, go to your email account and confirm the 
    subscription that you will get from aws
    -
- go back to your bucket and go to properties
    - scroll down and click create event notification
- create the name, and choose, all object create events, option 
    - scroll down, and choose sns topic as the destination
    - pick the topic you just recently created
    - attempt to save ( you will not because you have not configured an sns policy to your bucket)
- open a new tab to go back to your sns topic
- choose access policy and click edit (top right)
- click on the dropdown of access policy and enter in this code
    - obviously change the arn numbers for the bucket and sns, and the sourceAccount as well
    - save the changes

```
{
 "Version": "2012-10-17",
 "Id": "AllowS3Publish",
 "Statement": [
  {
   "Sid": "S3EventNotification",
   "Effect": "Allow",
   "Principal": {
     "Service": "s3.amazonaws.com"  
   },
   "Action": [
    "SNS:Publish"
   ],
   "Resource": "arn:aws:sns:us-east-2:387990400161:myEmail",
   "Condition": {
      "ArnLike": { "aws:SourceArn": "arn:aws:s3:::evt-notification-21125" },
      "StringEquals": { "aws:SourceAccount": "387990400161" }
   }
  }
 ]
}
```
- go back to your bucket event notification page and attempt to save again (you should be able to save now)
- go to your bucket and upload a file
- after uploading a file, go to your email account and verify that sns sent an email verifying that an upload has been made

</details>

[go back :house:][home]

### configure replication and lifecycle

<details>
<summary>
View Content
</summary>

- first we need to setup  two s3 buckets in order to configure same-region replication
- go to s3 and create a source bucket in us-east-1
    - enable bucket versioning
- create another bucket(destination)
    - enable bucket versioning
- go to iam in order create a role that would be used for replication
    1. choose the option custom trust policy
    2. paste this code in the editor 
```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"s3.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```  
  3. click next 2x, and name the role SRR-S3, then create the role
- select the role


</details>

[go back :house:][home]


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
has the `my-example-bucket`. Make sure you keep the `/*` after the bucket name

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
12. login as the new user and go to s3 (in a separate browser)
(you should be able to see the buckets because the permissions allow it )
13. go to newly created bucket, and choose the properties tab
(verify that you don't have permissions to do anything)
14. go to the object tab and upload an image
15. now try to download the file that you created, then attempt to delete
(verify that you cannot delete the file because of permissions)
16. In your admin account. go to your current buckets permmissions tab and edit the bucket policy to paste this content inside( obviously, change the user arn and bucket name) 
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowDeleteObject",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::123456789012:user/my-example-user"
            },
            "Action": [
                "s3:DeleteObject"
            ],
            "Resource": [
                "arn:aws:s3:::my-example-bucket/*"
            ]
        }
    ]
}
```
17. after you saved it, go back to the other user account and attempt to delete the bucket object again (it should work now)
18. in the admin account, go back to iam and edit the user's permission policies. in the json editor  paste this bracket of code at the bottom (obviously changing the names)
```
    {
        "Sid": "DenyDeleteObject",
        "Effect": "Deny",
        "Action": "s3:DeleteObject",
        "Resource": [
            "arn:aws:s3:::my-example-bucket/*"
        ]
    }
```
19. go back to created user account, and try to upload another image. then try to delete that object (of course you could not delete it because you added the deny rule)


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
