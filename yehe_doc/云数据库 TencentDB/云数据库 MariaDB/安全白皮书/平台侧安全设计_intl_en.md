
This document describes platform security features such as isolation, authentication, transfer encryption.

## Isolation
The networks of different regions are fully isolated from each other, and Tencent Cloud services in different regions cannot communicate with each other over the private network by default. In addition, security groups and VPCs are also used for network isolation.
- A **[security group](https://intl.cloud.tencent.com/document/product/213/12452)** is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more Tencent Cloud services.
You can control the access permissions of a TencentDB for MariaDB instance in the following ways:
  - Create multiple security groups and specify different rules for them.  
  - Assign one or multiple security groups to the TencentDB for MariaDB instance and use the security group rules to determine what traffic can access the instance and what resources can be accessed by the instance.  
  - Configure a security group to allow only specified IP addresses to access the TencentDB for MariaDB instance.

- **[VPC](https://intl.cloud.tencent.com/document/product/215/535)**: it is a logically isolated network space defined in Tencent Cloud. Even in the same region, different VPCs cannot communicate with each other over the private network by default.

## Authentication
[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users and user groups. You can manage identities and policies to allow specific users to access your Tencent Cloud resources.

When using CAM, you can associate a policy to a user or user group. The policy can authorize or reject users' use of specified resources to finish specified jobs.

If you use multiple cloud services such as VPC, CVM, and TencentDB that are managed by different users sharing your cloud account key, the following problems may arise:

- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from misoperations due to the lack of user access control.

You can avoid the problems above by allowing different users to manage different services through sub-accounts. By default, a sub-account does not have permissions to use Tencent Cloud services or resources. Therefore, you need to create a policy to grant different permissions to the sub-accounts.

## Transfer Encryption
The TencentDB for MariaDB console supports the HTTPS transfer protocol and standard network access protocols, guaranteeing your access security and meeting your needs for sensitive data encryption and transfer.
