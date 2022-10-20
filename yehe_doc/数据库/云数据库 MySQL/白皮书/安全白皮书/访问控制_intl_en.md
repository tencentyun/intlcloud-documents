TencentDB for MySQL provides access control capabilities. By defining and verifying user permissions, regulating user access to database resources, and managing database resource permissions, you can ensure that only authorized users can access database objects within the scope of their permissions or at their security levels.

## [Database account management](id:SJKZHGL)
You can create database accounts through the TencentDB for MySQL console or API. You can also grant management permissions at different levels to such accounts. We recommend you authorize accounts based on the principle of least privilege to ensure the data security.

For more information, see [Creating Account](https://intl.cloud.tencent.com/document/product/236/31900).

## [Access management](id:FWGL)
Cloud Access Management (CAM) helps you securely manage and control access permissions to your Tencent Cloud resources. With CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management, which implements permission separation.

For more information, see [CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583).

## [Password complexity](id:MMFZD)
Passwords are the most important means for protecting database security. As more data security regulations are introduced, there are higher requirements for the database password strength. TencentDB for MySQL supports the custom password complexity feature to protect your database security and meet your needs for compliance with applicable regulations.

You can configure the custom password complexity feature in the console to set the password strength for all console and database operations involving a password. This helps protect your passwords and prevent security risks such as password leakage. The feature offers the following configuration items:
- Min Number of Uppercase or Lowercase Letters
- Min Number of Digitals
- Min Number of Symbols
- Min Number of Password Characters

For more information, see [Setting Password Complexity](https://intl.cloud.tencent.com/document/product/236/49197).
