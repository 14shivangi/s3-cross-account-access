# s3-cross-account-access
Allow another AWS account to list, download and pull files from your S3 bucket using IAM policies and CLI.

1. S3 Bucket Policy for Cross-Account Access
-This document provides details about an AWS S3 bucket policy that enables cross-account access, allowing another AWS account to list, read, and write to a specific S3 bucket named 'mybucketforss3'.


2. Bucket Information
-	Bucket Name: mybucketforss3
-	Owner Account (Account A): The account where the bucket exists
-	Grantee Account (Account B): 123********789


3. Purpose of the Policy
This policy allows another AWS account (Account B) to:
1.	List the contents of the bucket (s3:ListBucket)
2.	Download objects from the bucket (s3:GetObject)
3.	Upload objects to the bucket (s3:PutObject)


4.	Full Policy JSON
   <img width="1920" height="956" alt="Image" src="https://github.com/user-attachments/assets/9bdc9649-46f2-402f-8c58-f8aa46626ef2" />


5.	Explanation of Policy Sections

Statement 1: AllowAccountBReadWriteAccess
-	Effect: Allow
-	Principal: arn:aws:iam::123******789:root
-	Actions: s3:GetObject, s3:PutObject (for objects)
-	Resource: arn:aws:s3:::mybucketforss3/*

Statement 2: AllowAccountBListBucket
-	Effect: Allow
-	Principal: arn:aws:iam::123*****789:root
-	Action: s3:ListBucket (for bucket)
  

6.	How to Apply This Policy
   
1.	Open the AWS Management Console.
2.	Go to S3 and select 'mybucketforss3'.
3.	Click the 'Permissions' tab.
4.	Open the 'Bucket Policy' editor.
5.	Paste the policy and save.


7.Testing the Access (From Account B)
-	List Bucket:
aws s3 ls s3://mybucketforss3

-	Download Object:
aws s3 cp "s3://mybucketforss3/example.jpg" "./"

-	Upload Object:
aws s3 cp "./newfile.txt" "s3://mybucketforss3/newfile.txt"


 
Statement 1: AllowAccountBReadWriteAccess
-	Effect: Allow
-	Principal: arn:aws:iam::123*****789:root
-	Actions: s3:GetObject, s3:PutObject (for objects)
-	Resource: arn:aws:s3:::mybucketforss3/*

Statement 2: AllowAccountBListBucket
-	Effect: Allow
-	Principal: arn:aws:iam::123*****789:root
-	Action: s3:ListBucket (for bucket)
-	Resource: arn:aws:s3:::mybucketforss3


~How to Apply This Policy
-Open the AWS Management Console.
-Go to S3 and select 'mybucketforss3'.
-Click the 'Permissions' tab.
-Open the 'Bucket Policy' editor.
-Paste the policy and save.


Testing the Access (From Account B)
-	List Bucket:
aws s3 ls s3://mybucketforss3

-	Download Object:
aws s3 cp "s3://mybucketforss3/example.jpg" "./"

-	Upload Object:
aws s3 cp "./newfile.txt" "s3://mybucketforss3/newfile.txt"


S3 Cross-Account Access Guide
This guide explains how to allow another AWS account to list, download, and upload files to your Amazon S3 bucket using IAM policies and the AWS CLI.
Bucket Information
Property	Value
Bucket Name	mybucketforss3
Owner Account (Account A)	Account where the bucket exists
Grantee Account (Account B)	123********789
Purpose
This S3 bucket policy allows Account B to:
- List the contents of the bucket (s3:ListBucket)
- Download objects (s3:GetObject)
- Upload objects (s3:PutObject)
Full Bucket Policy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowAccountBReadWriteAccess",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::123********789:root"
            },
            "Action": [
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource": "arn:aws:s3:::mybucketforss3/*"
        },
        {
            "Sid": "AllowAccountBListBucket",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::123********789:root"
            },
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::mybucketforss3"
        }
    ]
}
Explanation of Policy
Statement 1: AllowAccountBReadWriteAccess
- Effect: Allow
- Principal: Account B root user
- Actions: s3:GetObject, s3:PutObject (object-level access)
- Resource: arn:aws:s3:::mybucketforss3/*
Statement 2: AllowAccountBListBucket
- Effect: Allow
- Principal: Account B root user
- Action: s3:ListBucket (bucket-level access)
- Resource: arn:aws:s3:::mybucketforss3
How to Apply This Policy
1. Open AWS Management Console.
2. Navigate to S3 and select the bucket 'mybucketforss3'.
3. Go to the Permissions tab.
4. Open Bucket Policy editor.
5. Paste the above JSON policy and Save.
Testing Access (From Account B)
List Bucket:
aws s3 ls s3://mybucketforss3
Download Object:
aws s3 cp "s3://mybucketforss3/example.jpg" "./"
Upload Object:
aws s3 cp "./newfile.txt" "s3://mybucketforss3/newfile.txt"
Notes
- Ensure AWS CLI is configured in Account B with the correct credentials.
- This policy applies only to the specified bucket 'mybucketforss3'.
- Access is granted to the root user of Account B (can be scoped to specific IAM roles/users if needed).
