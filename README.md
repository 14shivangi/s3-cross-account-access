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
