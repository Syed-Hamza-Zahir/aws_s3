# AWS_s3

## AWS Comnand Line Interface (AWSCLI)

Install dependencies:
```sudo apt-get install python-pip -y
sudo apt-get install python3-pip
sudo apt install pip3
alias python=python3
sudo pip3 install awscli
aws configure
```

- Insert access key 
- Insert secret access key 
- Insert Region : eu-west-1
- Insert : json

`aws s3 ls`

# Create a bucket

make a bucket:
`aws s3 mb s3://eng114-syed-bucket --region eu-west-1`

Note: It does not accetpt any special characters

Copy file to bucket:
`aws s3 cp test.text s3://eng114-syed-bucket/`

Copy file from bucket:
`aws s3 cp s3://eng114-syed-bucket/test.text test.text`

Delete file from bucket:
`aws s3 rm s3://eng114-syed-bucket/test.text`

Delete bucket:
`aws s3 rb s3://eng114-syed-bucket`

# Activity

***Exercise:***
- **Launch new EC2 ubuntu instance :**
- **Next:** 
- **Research the documentation on AWS/Python for python  ```boto3``` package to create and manage AWS S3 resources and complete all the following tasks**

***DOD:***
- Setting up awscli and python Env with required dependencies
-   S3 authentication setup - with aws configure on EC2
-  Create S3 bucket using python-boto3
-  Upload data/file to S3 bucket using python-boto3 
-  Retrieve content/file from S3 using python-boto3
-  Delete Content from S3 using python-boto3
-  Delete the bucket using python-boto3.**

```
#!/usr/bin/env python3

import boto3
import botocore

# Creating a S3 client
s3 = boto3.client('s3')
s3 = boto3.resource('s3')

# Creating a bucket in AWS S3
# s3.create_bucket(
  #      Bucket='eng114-syed-test-bucket',
  #      CreateBucketConfiguration={'LocationConstraint': 'eu-west-1'})


for bucket in s3.buckets.all():
    print(bucket.name)

# Upload file
s3.upload_file(
        Filename = 'test0.txt',
        Bucket = 'eng114-syed-bucket',
        Key = 'test0.txt'
)

#Download file + custom error message
try:
   s3.Bucket('eng114-syed-test-bucket').download_file('n/a.txt', 'n/a.txt')
except botocore.exceptions.ClientError as e:
        if e.response['Error']['Code'] == "404":
                print("The object does not exist.")
        else:
                raise

# Delete file
        s3.delete_object(
                Bucket='eng114-syed-test-bucket',
                Key='test0.txt'
        )

# Delete Bucket
        s3.delete_bucket(
        Bucket='eng114-syed-test-bucket')

```
# Alert & Monitoring
We can monitor all sorts of metrics:
- error logs
- budgeting
- uptime - access time - response time
- security breaches
- system test/health
- instance's health
- CPU utilisation %
- Memory utilisation %


## AWS Monitoring

Three monitoring services in AWS
- Cloudwatch - Monitor AWS service
- SNS - Simple notification
- SQS - Simple queue service
-
We will be working with SNS 
CloudWatch enables you to monitor your complete stack (applications, infrastructure, and services) and use alarms, logs, and events data to take automated actions and reduce mean time to resolution (MTTR). This frees up important resources and allows you to focus on building applications and business value.

# Create SNS notifications on AWS
To receive email notifications, you will need to create an alarm in Cloudwatch and subscribe to it using your email.
(for a specific instance click Actions on instance page,

