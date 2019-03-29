### Policy 
This is a syntactic rule that defines and describes one or more permissions. A root account performs authorization by associating policies with users/user groups. A super administrator or any sub-account which is granted the policy management permission can also create, update and delete policies, or grant permissions for policies.

### Login Credentials 
Username and password for login. By logging in to Tencent Cloud console using the login name and password, you can perform operations allowed by your permissions via the console.

### Multi-Factor Authentication (MFA)
MFA is a security protection built on the login credentials. If you have bound an MFA device in the security information settings, you can choose to enable login and operation protections.

### Access Credentials 
Access credentials refer to the cloud API keys (SecretId and SecretKey), including individual API keys and project keys. In most business scenarios, individual API keys are used to access Tencent Cloud APIs. In some business scenarios, project keys are used to access the Tencent Cloud APIs for some services, such as Cloud Infinite, Face Recognition, and COS.

### Root Account 
A root account represents a developer. When you apply for a Tencent Cloud account, a root account identity is created in the system to be used for logging in to Tencent Cloud services. The consumption of Tencent Cloud resources is calculated and billed with the root account as the primary consumer. A root account has the full access to all the account resources.

### Identity Credentials 
Identity credentials, including login credentials and access credentials, are used to validate the identity of a user. You should ensure the security of the credentials.

### Permission 
Permission is an authorization to allow users to perform certain operations or access certain resources. By default, a root account has the full access to all the resources in the account, and a sub-account does not have access to any resources in the root account.

### User Group 
This refers to a group of users (sub-accounts) who have the same duty. You can create multiple user groups as needed, then associate the user groups with specific policies to assign different permissions.

### Sub-Account (User) 
A sub-account is an entity created by the root account. It has an ID, identity credentials and the permission to log in to Tencent Cloud console. A sub-account does not own any resource by default, and must be authorized by its root account to use the resources. A root account can create multiple sub-accounts (users).

### Role
A role refers to a virtual identity with a group of permissions. It is used to grant permissions to access services and resources and to perform operations in Tencent Cloud to the role entities. These permissions are granted to a role, instead of a user or user group.
For more information, see [Basic Concepts](https://cloud.tencent.com/document/product/598/19421).

### Role Entity
A role entity is the object allowed to have the permissions of the role. You can edit a role entity, and add or delete objects to allow or forbid them to assume the roles to access your Tencent Cloud resources.
For more information, see [Basic Concepts](https://cloud.tencent.com/document/product/598/19421).

### Permission Policies
Permission policies are created in a JSON-formatted permission document, where you can define the operations and resources that various roles have access to. This document is based on the language rules of CAM policies.

### Trust Policies
Trust policies are created in a JSON-formatted permission document, where you can define the objects that can assume the roles and the conditions to be met to assume the roles. This document is based on the language rules of CAM policies.

