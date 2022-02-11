
TDSQL-C implements access control through database account management, password management, access management, security group, and other means to ensure data security.

### Database Account Management
You can create database accounts in the [TDSQL-C](https://console.cloud.tencent.com/cynosdb) console. You can also grant management permissions at different levels to such accounts. You are recommended to authorize accounts based on the principle of least privilege so as to ensure the data security.

### Password Management
TDSQL-C allows you to reset the database account password in the console. The password can contain 8–64 characters in at least two of the following character types: letters, digits, and special symbols `_+-&=!@#$%^*()`.
The password resetting feature has been connected to [CAM](https://intl.cloud.tencent.com/document/product/598/10583); therefore, we recommend you exercise tighter control over the permissions of the password resetting API or sensitive TDSQL-C resources by granting such permissions only to appropriate personnel on an as-needed basis. For data security, we recommend you regularly reset the password at least once every three months.

### Cloud Access Management
[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/1098/40640) helps you securely manage and control access permissions to your Tencent Cloud resources. With CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management, which implements permission separation.

### Security Groups
[Security group](https://intl.cloud.tencent.com/document/product/213/12452) mainly helps you implement network access control for your TDSQL-C instances. It serves as a stateful virtual firewall with filtering feature for configuring network access control for one or more instances. It is an important network security isolation tool provided by Tencent Cloud.

Instances with the same network security isolation requirements in one region can be put into the same security group, which is a logical group. Instances in a security group are matched based on rules. Modifying security group rules does not require restarting the TDSQL-C instances, and the changes will take effect immediately.
