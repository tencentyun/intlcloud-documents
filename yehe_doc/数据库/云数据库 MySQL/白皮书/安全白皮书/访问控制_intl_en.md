TencentDB for MySQL implements access control through database account management, access management, security group, and other means to ensure MySQL data security.

### Database Account Management
You can [create database accounts](https://intl.cloud.tencent.com/document/product/236/31900) in the TencentDB for MySQL Console or through APIs. You can also grant management permissions at different levels to such accounts. You are recommended to authorize accounts based on the principle of least privilege so as to ensure the data security.

### Cloud Access Management
[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) helps you securely manage and control access permissions to your Tencent Cloud resources. With CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management, which implements permission separation.

### Security Group
[Security group](https://intl.cloud.tencent.com/document/product/236/14470) mainly helps you implement network access control for your TencentDB for MySQL instances. A security group is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances.

Instances with the same network security isolation requirements in the same region can be put into the same logical security group. Instances in a security group are matched based on rules. Modifying security group rules does not require restarting the TencentDB for MySQL instances, and the changes will take effect immediately.


