<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Encrypt Data with AWS KMS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-kms)

**Author:** anifalaje clinton  
**Email:** clintonanif@gmail.com

---

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-security-kms_w0x1y2z3)

---

## Introducing Today's Project!

In this project, I will demonstrate how to protect a database using encryption with AWS KMS. The goal is to learn how to create encryption keys with AWS KMS, encrypt a DynamoDB database with a KMS key, add and retrieve data to test your encryption, observe how AWS stops unauthorized access to your data, and give a user encryption access.

### Tools and concepts

Services I used include AWS KMS, DynamoDB, and IAM. Key concepts I learnt include encryption, ciphertext, encryption keys, key management systems, compliance, AWS managed keys vs. customer managed keys (CMKs), symmetric encryption vs. asymmetric encryption (including public and private keys), key usage, key administrators, key users, cross-account access policies, key policies, data at rest, data in transit, data in use, and transparent data encryption. I also learned how to create and manage encryption keys, encrypt a DynamoDB table, add data to an encrypted table, use a test user to validate encryption, and give a test user encryption access.

### Project reflection

This project took me approximately 2 hours.

I chose to do this project today because its part of series of project i am working on. Something that would make learning with NextWork even better is how easy they make learning feel.

---

## Encryption and KMS

Encryption is a process that uses algorithms to convert data into a secure format called ciphertext. Only authorized users can decrypt and restore the data to its original, readable state. Otherwise, it looks like a scrambled piece of text like bihtueg34509ua!

Companies and developers do this to secure user data, transactions, files, and more. Many apps, websites, and devices use encryption behind the scenes to protect information.

Encryption keys are like digital codes that tell the encryption algorithm exactly how to transform plain text into ciphertext. For example, a key could tell the algorithm to swap out certain parts of the data or shuffle the order of data to break up patterns. Encryption keys themselves look like ciphertext that only the algorithm can understand, like A7F3E5C4B1D2.

AWS KMS is a secure vault for your encryption keys. You use KMS to create, manage, and use encryption keys that protect the data in your AWS resources.

Key management systems are important because they help you manage all your encryption keys, including what data they encrypt and who has access, all in one place. Your keys are safe in a KMS, so you don't have to worry about losing them or someone stealing them. You can also use a KMS to create new keys needed for encryption or decryption. Additionally, a KMS provides logs on every time a key was used, which helps companies and developers meet compliance requirements for data security.

Encryption keys are broadly categorized as symmetric and asymmetric. I set up a symmetric key because symmetric encryption uses a single encryption key to both lock (encrypt) and unlock (decrypt) your data. These keys are generally faster and more efficient for encrypting large amounts of data, which is why we're using one for our DynamoDB table.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-security-kms_a2b3c4d5)

---

## Encrypting Data

My encryption key will safeguard data in DynamoDB, which is one of AWS's database services. DynamoDB stands out as a fast and flexible way to store your data, making it a great choice for applications that need quick access to large volumes of data, such as games.

The different encryption options in DynamoDB include:

1. Owned by Amazon DynamoDB: Amazon DynamoDB fully manages the key, so you have no access or visibility to the key.

2. AWS managed key: AWS Key Management Service (KMS) manages the key. You can see the key and its usage, but management is done by AWS.

3. Stored in your account, and owned and managed by you: This is a customer managed key (CMK). You create and manage the key in KMS, giving you full control.

Their differences are based on the level of control you have over the encryption key and its management. Owned by Amazon DynamoDB offers the least control, while customer managed keys offer the most.

I selected Stored in your account, and owned and managed by you because it is the most secure option and provides full control over the encryption key, which is what we are using in this project.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-security-kms_q8r9s0t1)

---

## Data Visibility

Rather than controlling who has access to the key, KMS manages user permissions by defining who can perform specific actions like encryption or decryption through a key policy attached directly to the KMS key, and through IAM policies. This means that while many users might be able to see that a KMS key exists, only those with the correct permissions can actually use it for cryptographic operations.

Despite encrypting my DynamoDB table, I could still see the table's items because I, as an authorized user, have permissions to use the encryption key in KMS. DynamoDB is designed to decrypt the data on my behalf. DynamoDB uses transparent data encryption, which means it retrieves the encrypted data, decrypts it with the key, and then shows me the decrypted format instantly when requested by an authorized user or application.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-security-kms_c0d1e2f3)

---

## Denying Access

I configured a new IAM user to test the KMS encryption by attempting to access an encrypted DynamoDB table. The permission policies I granted this user are AmazonDynamoDBFullAccess but not access to the KMS key.

After accessing the DynamoDB table as the test user, I encountered an error message indicating that access is denied because the new IAM user does not have permission to decrypt the data. This confirmed that the encryption is working as expected and unauthorized users cannot access the data.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-security-kms_w0x1y2z3)

---

## EXTRA: Granting Access

To let my test user use the encryption key, I modified the KMS key's policy as the administrator. My key's policy was updated to grant the test user the necessary permissions to decrypt data.

Using the test user, I retried accessing the encrypted DynamoDB table. I observed that I could now view the items in the table, which confirmed that the test user had been granted the necessary permissions to decrypt the data.

You would use encryption primarily to protect the confidentiality of data itself, ensuring that even if unauthorized individuals gain access to the data, they cannot read or understand it because it's scrambled (ciphertext). This is crucial for data at rest (like your DynamoDB table) and in transit.

On the other hand, access control tools like IAM policies and KMS key policies are used to manage who can perform what actions on specific resources. They define permissions, determining which users or roles are authorized to interact with your AWS services, including using KMS keys for cryptographic operations or accessing DynamoDB tables.

They complement each other: encryption protects the data's content, while access control protects the data's container and the tools used to encrypt/decrypt it. For example, in this project, your DynamoDB table is encrypted, but IAM and KMS key policies dictate which users can actually perform the decryption to view the data.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-security-kms_feffb2fb8)

---

---
