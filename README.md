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

<img width="1600" height="692" alt="WhatsApp Image 2026-09-28 at 22 44 15" src="https://github.com/user-attachments/assets/939b85a0-f8ee-4950-bdef-4611f0ebbbd1" />



<img width="1600" height="709" alt="WhatsApp Image 2026-09-28 at 22 48 19" src="https://github.com/user-attachments/assets/d930322c-250d-41d7-8516-8446469f4851" />


 - Copy the user's log in details after the user is created


<img width="1600" height="692" alt="WhatsApp Image 2026-09-28 at 22 49 49" src="https://github.com/user-attachments/assets/28fd2034-6d8f-4bbb-80ee-29dab7d32689" />


<img width="1600" height="698" alt="WhatsApp Image 2026-09-28 at 22 51 09" src="https://github.com/user-attachments/assets/32e33b29-c136-4a16-a80b-b54a7c94f346" />



<img width="1600" height="692" alt="WhatsApp Image 2026-09-28 at 22 53 42" src="https://github.com/user-attachments/assets/2c48fd38-3c09-42e0-be49-133e228db1b4" />



## Test and Verify Least Privilege Access

- Log into the AWS Management Console using Alice login credentials to confirm that only the permitted actions succeed

**On the S3 page, Alice can view all the buckets in the AWS account because the s3:ListAllMyBuckets permission assigned through the user's group**



<img width="1600" height="651" alt="WhatsApp Image 2026-09-28 at 22 54 52" src="https://github.com/user-attachments/assets/8630ef54-de47-40f7-a36b-9891aeb391d7" />



**The user can also read from and write to the dedicated developers S3 bucket. The user was able to upload an object successfully because the policy grants the s3:PutObject permission**



<img width="1600" height="633" alt="WhatsApp Image 2026-09-28 at 22 56 16" src="https://github.com/user-attachments/assets/b1c8f5e3-50db-44c0-b23b-b82f6a2c6957" />




<img width="1600" height="692" alt="WhatsApp Image 2026-09-28 at 22 57 46" src="https://github.com/user-attachments/assets/9ac392f2-9a7c-4599-9283-9325c2098af9" />


## Test unauthorized actions

- Attempt to create a new S3 bucket as the user Alice, the user received an "Access Denied" error because the developer group's policy allows only listing, reading and writing objects in to the dedicated S3 bucket, and AWS denies any action that isn't explicitly allowed



<img width="1600" height="758" alt="WhatsApp Image 2026-09-28 at 22 59 26" src="https://github.com/user-attachments/assets/8cd08e8d-b263-4397-8476-1ac30333ca86" />



## Summary

This setup demonstrates the implementation of the principle of least privilege in AWS IAM using a custom JSON policy and an IAM group. A developer user was granted only the permissions required to list S3 buckets and read/write objects in a dedicated S3 bucket. Authorized actions were successfully tested, while unauthorized actions, such as creating a new S3 bucket, were denied. This demonstrates how IAM policies can be used to enforce controlled access to AWS resources and reduce the risk of unauthorized actions








