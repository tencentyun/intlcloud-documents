## Security Isolation
The networks of different regions are fully isolated from each other, and Tencent Cloud services in different regions cannot communicate with each other over the private network by default. In addition, security groups and VPCs are also used for network isolation.
- **[Security group](https://intl.cloud.tencent.com/document/product/213/12452)**: it is a stateful virtual firewall capable of packet filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more Tencent Cloud services.
You can control the access permissions of a TDSQL for MySQL instance in the following ways:
  - Create multiple security groups and specify different rules for them.  
  - Assign one or multiple security groups to the TDSQL for MySQL instance and use the security group rules to determine what traffic can access the instance and what resources can be accessed by the instance.  
  - Configure a security group to allow only specified IP addresses to access the TDSQL for MySQL instance.

- **[VPC](https://intl.cloud.tencent.com/document/product/215/535)**: it is a logically isolated network space defined in Tencent Cloud. Even in the same region, different VPCs cannot communicate with each other over the private network by default.

## Authentication
[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks.

If you use multiple Tencent Cloud services such as CVM, VPC, and TencentDB that are managed by different users sharing your Tencent Cloud account key, you may face the following problems:

- Your key is shared by multiple users, leading to high risk of compromise.
- You cannot limit the access permissions of other users, which poses a security risk due to potential faulty operations.

You can allow different users to manage different services through sub-accounts so as to avoid the above problems. By default, a sub-account does not have permission to use a Tencent Cloud service or related resources. Therefore, you need to create a policy to grant the required permission to the sub-account.

## Transfer Encryption
The TDSQL for MySQL Console supports the HTTPS transfer protocol and standard network access protocols, guaranteeing your access security and meeting your needs for sensitive data encryption and transfer.
