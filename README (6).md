<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Endpoints

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-endpoints)

**Author:** anifalaje clinton  
**Email:** clintonanif@gmail.com

---

## VPC Endpoints

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-networks-endpoints_09bcaa8a)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is an AWS service that lets you provision a logically isolated portion of the AWS cloud to launch resourcesin a virtual network you define. it is useful because it helps you give structure, manage different resources and keep it secure.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to establish private, secure access to an S3 bucket. This involved creating a VPC endpoint and configuring the route table to direct

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how immediately the S3 console showed 'denied access' warnings after applying the bucket policy, and realizing that it blocked all access not coming through the VPC endpoint.


### This project took me...

This project took me 1hr

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will create a VPC, launch an EC2 instance, and set up an S3 bucket because these are the foundations of today's project.


### Step 2 - Connect to EC2 instance

In this step, I will connect to my EC2 instance and access S3 via the public internet because I want to see how it works without VPC endpoints.

### Step 3 - Set up access keys

In this step, I will set up access keys because my EC2 instance needs credentials to access my AWS services.


### Step 4 - Interact with S3 bucket

In this step, I will head back to my EC2 instance and get it to access my S3 bucket because I want to use the access keys I just created to interact with AWS services from the instance.

---

## Architecture set up

I started my project by launching a VPC, an EC2 instance, and an S3 bucket.

I also set up...I also set up an S3 bucket and uploaded two files into it.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

In this step, I configured the Access Key ID, the AWS Secret Access Key, the Default region name, and the Default output format to set up my EC2 instance to interact with my AWS environment.

Access keys are like keys that let you access and manage AWS services securely. They are part of a credential.

Secret access keys are like the password that pairs with your access key ID (your username). You need both to access AWS services. It's crucial to keep them confidential, as anyone with access to your secret access key can access your AWS account.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use an IAM role with the necessary permissions attached to your EC2 instance. This allows the instance to inherit permissions securely.

---

## Connecting to my S3 bucket

The command I ran was aws s3 ls. This command is used to list the S3 buckets in your account.

The terminal responded with a list of your S3 buckets, including the admin-vpc-project1-anif bucket. This indicated that the access keys I set up were correctly configured and allowed the EC2 instance to access AWS S3 services.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket

I also tested the command aws s3 ls s3://admin-vpc-project1-anif, which returned a list of the objects inside my specified S3 bucket.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-networks-endpoints_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command sudo touch /tmp/admin.txt. This command creates an empty file named admin.txt in the /tmp directory of my EC2 instance.

The second command I ran was aws s3 cp /tmp/admin.txt s3://admin-vpc-project1-anif. This command will copy the admin.txt file from the EC2 instance's /tmp directory to your specified S3 bucket.

The third command I ran was aws s3 ls s3://admin-vpc-project1-anif, which validated that the admin.txt file was successfully uploaded to my S3 bucket by listing its contents.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step, I will set up a way for my VPC and S3 to communicate directly because the current connection is through the public internet, which is not the most secure way to communicate.

### Step 6 - Bucket policies

In this step, we're validating your VPC endpoint by making your S3 bucket accessible only through the endpoint. If your EC2 instance can still access S3, the endpoint is providing direct, private access.

### Step 7 - Update route tables

In this step, I will test the VPC endpoint setup to see if my EC2 instance can still access the S3 bucket. This is to verify the endpoint connection works after the new bucket policy and troubleshoot any connectivity issues.

### Step 8 - Validate endpoint conection

In this step, I will test the VPC endpoint setup again and restrict my VPC's access to the AWS environment. This is to check the endpoint connection one last time and ensure it's working perfectly, while also exploring endpoint policy configurations.

---

## Setting up a Gateway

I set up an S3 Gateway, which is a type of endpoint used mainly for Amazon S3 and DynamoDB. Gateways work by  adding a route to your VPC route table that directs traffic bound for S3 or DynamoDB to go straight for the Gateway instead of the internet.

### What are endpoints?

An endpoint is a service in AWS that allows your VPC to connect privately to other AWS services like S3 without traffic going over the public internet. This ensures your data stays within the AWS network for enhanced security.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is a type of IAM policy designed for setting access permissions to an S3 bucket. Using bucket policies, you get to decide who can access the bucket and what actions they can perform with it.

My bucket policy denies all actions on your S3 bucket and its objects to everyone, unless access originates from your defined VPC endpoint. This ensures only traffic from your VPC endpoint can access your S3 bucket.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies

Right after saving my bucket policy, my S3 bucket page showed 'denied access' warnings. This was because the policy blocked all actions unless access came from your VPC endpoint. Other sources, like the AWS Management Console, were blocked.

I also had to update my route table because without a route directing traffic bound for S3 to the VPC endpoint, my EC2 instance would try to access the S3 bucket via the public internet instead of the secure endpoint.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

To update my route table, I went to the VPC console, selected Endpoints, chose my endpoint, and then its Route tables. I managed these, selected my public route table, and modified it to associate the endpoint with it.

After updating my public subnet's route table, my terminal could return: WOOOHOOOO! We're back. This indicates a successful connection to your S3 bucket through the VPC endpoint.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy is a configuration that allows you to control access to AWS services through your VPC endpoint. It's a tool for granting granular permissions, such as read-only access to an S3 bucket, or for quickly blocking all access if needed.

I updated my endpoint's policy by changing "Effect": "Allow" to "Effect": "Deny". The effect was immediate: running aws s3 ls in my EC2 instance resulted in denied access, confirming the endpoint policy successfully blocked S3 bucket access.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-networks-endpoints_3e1e79a3)

---

---
