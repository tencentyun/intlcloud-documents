[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users and user groups. You can manage identities and policies to allow specific users to access your Tencent Cloud resources.

## Background
If you have multiple users managing different Tencent Cloud services such as CVM, VPC, and TencentDB, and they all share your Tencent Cloud account access key, you may face the following problems:
- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from misoperations due to the lack of user access control.

## Concepts
**Root account**
When you apply for a Tencent Cloud account, a root account is created by the system which you can use to log in to Tencent Cloud services. A root account is the entity used to bill your usage of Tencent Cloud resources. A root account has full access to all the resources under it by default and can create and authorize sub-accounts. 

**Sub-account**
A sub-account is created by and belongs to the root account. Every sub-account has a definite ID and identity credential.

**Identity credential**
An identity credential includes a **login credential** and an **access certificate**. The former refers to a user’s login name and password. The latter refers to Tencent Cloud API keys (SecretId and SecretKey).

**Resource**
A resource is an object manipulated in Tencent Cloud services, such as a TencentDB for MongoDB instance.

**Permission**
A permission is an authorization that allows or forbids users to perform certain operations. By default, the **root account** has full access to all resources under the account, while a **sub-account** does not have access to any resources under its root account.

**Policy**
A policy is a syntax rule that defines and describes one or more permissions. By default, a sub-account has no access to Tencent Cloud services or resources. To grant a sub-account such access, you need to create a CAM policy.

## References
For more information on access management, see [CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583).

