## Least-Privilege-Setup-in-AWS-Management-Console

This setup demonstrates how the principle of least privilege is enforced in the AWS Management Console using IAM policies to restrict a developer user to only the permissions required to perform specific tasks, which also serves as a control measure to prevent unauthorized access to resources within an AWS account.


 **Create the target resource (S3 bucket)**
 
- Log into the AWS Management Console as the root user and create a dedicated S3 bucket, leave all default settings with Block Public Access enabled


<img width="1600" height="687" alt="WhatsApp Image 2026-09-28 at 22 32 59" src="https://github.com/user-attachments/assets/74bba7d1-d327-4491-8acc-498812b7d3b4" />




**Create a custom least-privilege IAM policy tailored to the user's development needs using JSON.**

- This policy grants the user read and write access to objects in the dedicated S3 bucket, and to also allow the user to list S3 buckets in the AWS Management Console


<img width="1600" height="695" alt="WhatsApp Image 2026-09-28 at 22 37 31" src="https://github.com/user-attachments/assets/85638c5a-e24a-4c87-8da8-19789a689a7d" />


<img width="1100" height="461" alt="WhatsApp Image 2026-09-28 at 22 39 43" src="https://github.com/user-attachments/assets/33288a4a-e535-417b-b33d-6c9cab770681" />


<img width="1600" height="685" alt="WhatsApp Image 2026-09-28 at 22 42 04" src="https://github.com/user-attachments/assets/68899a82-e848-4968-8e78-9bc2ff95b135" />


**Create the User and Assign Permissions via Groups**

- The user belongs to the Developers group. As a best practice, create the developers group and attach the custom least-privilege policy to the group. Then, create the user and add the user to the group so that they inherit the permissions granted by the group policy, rather than assigning policies directly to individual users

<img width="1600" height="692" alt="WhatsApp Image 2026-09-28 at 22 44 15" src="https://github.com/user-attachments/assets/4291bde5-4403-4139-84a0-789191697aae" />


- Create IAM user, enable AWS Management Console access, and add the user to the developers group


<img width="938" height="373" alt="USER 2 - IAM" src="https://github.com/user-attachments/assets/60daf648-370c-40cd-967b-ea299179ce6f" />



<img width="957" height="368" alt="USER 3 - IAM" src="https://github.com/user-attachments/assets/3065445c-1124-41a1-8384-c58d3698e156" />


 - Copy the user's log in details after the user is created
 
<img width="955" height="368" alt="LOG IN 1 - IAM" src="https://github.com/user-attachments/assets/efae22ee-3bbd-4326-a38d-2979b36017b5" />


<img width="952" height="382" alt="LOG IN 2 - IAM" src="https://github.com/user-attachments/assets/bd7418b7-0c81-4a0c-8959-ee32d0f82b15" />


<img width="956" height="377" alt="LOG IN 3 - IAM" src="https://github.com/user-attachments/assets/a0b1a19d-7325-48fc-9f7c-57bf4b398c15" />


## Test and Verify Least Privilege Access

- Log into the AWS Management Console using Alice login credentials to confirm that only the permitted actions succeed

**On the S3 page, Alice can view all the buckets in the AWS account because the s3:ListAllMyBuckets permission assigned through the user's group**


<img width="955" height="392" alt="TEST 1 - IAM" src="https://github.com/user-attachments/assets/76fec40a-dc6d-4f67-9c6d-92d2bb112d9c" />


**The user can also read from and write to the dedicated developers S3 bucket. The user was able to upload an object successfully because the policy grants the s3:PutObject permission**

<img width="956" height="391" alt="TEST 2 - IAM" src="https://github.com/user-attachments/assets/5dc4637f-b742-4e9f-8251-73f55e9a0b03" />


<img width="947" height="389" alt="TEST 3 - IAM" src="https://github.com/user-attachments/assets/72e27634-db11-4b91-9484-d3d9464627e6" />


## Test unauthorized actions

- Attempt to create a new S3 bucket as the user Alice, the user received an "Access Denied" error because the developer group's policy allows only listing, reading and writing objects in to the dedicated S3 bucket, and AWS denies any action that isn't explicitly allowed


<img width="954" height="152" alt="TEST 4 - IAM" src="https://github.com/user-attachments/assets/112c3439-9615-4752-8d8b-5b1d87dbee8b" />



## Summary

This setup demonstrates the implementation of the principle of least privilege in AWS IAM using a custom JSON policy and an IAM group. A developer user was granted only the permissions required to list S3 buckets and read/write objects in a dedicated S3 bucket. Authorized actions were successfully tested, while unauthorized actions, such as creating a new S3 bucket, were denied. This demonstrates how IAM policies can be used to enforce controlled access to AWS resources and reduce the risk of unauthorized actions








