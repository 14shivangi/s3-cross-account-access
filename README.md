# 🚀 S3 Cross-Account Access Using Bucket Policies  
A practical demonstration of how to securely share an Amazon S3 bucket with another AWS account using IAM policies and bucket permissions.

---

## 📘 1. Introduction

Amazon S3 is widely used for storage across applications, teams, and organizations.  
Sometimes, you need to **share your S3 bucket with another AWS account**, for example:

- Sharing logs with another team  
- Allowing a partner company to upload/download files  
- Centralizing storage in one account and accessing it from another  

**Cross-account access** makes this possible in a secure and controlled way.

This project explains **how to allow another AWS account to list, download, and upload files** to your bucket using a **Bucket Policy**.

---

## 🎯 2. Why Cross-Account Access Is Needed

Organizations often use multiple AWS accounts for:

- Security separation  
- Billing separation  
- Multi-team collaboration  
- Partner or client access  
- Centralized data storage  

Instead of copying data between buckets or accounts, **S3 cross-account access** allows:

- Direct access  
- Reduced duplication  
- Lower storage cost  
- Better data governance  

---

## 🛠️ 3. How It Works (Concept)

S3 access is controlled by two things:

1. **Bucket Policy** → Controls who can access the bucket  
2. **IAM Policy (optional)** → Controls what the user/role is allowed to do  

In this setup:

- **Account A** owns the bucket: `mybucketforss3`  
- **Account B** is granted permission to list, download, and upload objects  

Access is given by writing a **bucket policy** in Account A.

---

## 📦 4. Bucket Details

| Property | Value |
|---------|--------|
| **Bucket Name** | `mybucketforss3` |
| **Account A** | Bucket owner |
| **Account B** | `123********789` (grantee account) |

---
## 🔍 5. Explanation of the Policy

### **Statement 1 – Object-Level Permissions**
This statement allows **Account B** to interact with the objects stored in the bucket.

**Actions Granted:**
- `s3:GetObject` → Download objects  
- `s3:PutObject` → Upload objects  

**Resource Scope:** 
- `arn:aws:s3:::mybucketforss3/*`

  This means the permissions apply to **all objects inside the bucket**, not the bucket itself.

---

### **Statement 2 – Bucket-Level Permissions**
This statement allows Account B to interact with the bucket **metadata**.

**Action Granted:**
- `s3:ListBucket` → View list of objects inside the bucket  

**Resource Scope:**
- `arn:aws:s3:::mybucketforss3/*`

This gives visibility of the bucket's object keys, but not access to the actual objects unless allowed by Statement 1.

---

## ⚙️ 7. How to Apply This Policy (Step-by-Step)

1. Log in to the **AWS Management Console**.  
2. Navigate to **S3**.  
3. Select the bucket **`mybucketforss3`**.  
4. Go to the **Permissions** tab.  
5. Open the **Bucket Policy Editor**.  
6. Paste the JSON policy provided above.  
7. Click **Save**.

✔️ The cross-account access is now active.

---

## 🧪 8. Testing Access From Account B (AWS CLI)

### **List Bucket Contents**
```bash
aws s3 ls s3://mybucketforss3
```


### **Download an Object**
```bash
aws s3 cp "s3://mybucketforss3/example.jpg" "./"


