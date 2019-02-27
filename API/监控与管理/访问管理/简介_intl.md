## Cloud Access Management
Thank you for choosing Cloud Access Management (CAM). You can use and manage the access to the resources under your Tencent Cloud account by calling the APIs described in this document. Please make sure you have a thorough understanding of CAM before using these APIs.

### 1. Terms
The common terms involved in this document are as follows:

| Term | Full Name | Description |
| ------------ | ------------ | ------------ |
| Role | Role | A virtual account with a set of permissions. It is used to grant access to Tencent Cloud resources under your account. |
| STS | Security Token Service | Provides credentials with custom validity period and access permissions. |

### 2. Getting started with APIs

You can use CAM APIs to manage the access to resources under your Tencent Cloud account. The following describes the application scenarios of APIs in this document.
- Role-related APIs allow you to create a virtual sub-account (role), specify the accounts allowed to assume the role, and grant the role a set of permissions to access resources under your account.
- The API "AssumeRole" is used to get temporary credentials for the role that can be assumed by the user.
- The API "GetFederationToken" is used to issue credentials with custom period of validity and access permissions to a user with federated identity (a user managed by your local account system).

## Role-related APIs
A role in CAM is a virtual sub-account, for which you can grant a set of permissions and specify the users allowed to assume the role. A role can be associated with more than one account, and any user allowed to assume the role can be assigned the role. In addition, a role does not have long-term credentials (passwords or API keys) a standard account has, and CAM dynamically creates temporary credentials for a user who applies for a role. You can use and manage the roles by calling the APIs described in this document.

### 1. Terms
The common terms involved in this document are as follows:

| Term | Full Name | Description |
| ------------ | ------------ | ------------ |
| policyDocument | policyDocument | Used to grant the specified user the permission to apply for this role. |
| description | description | Description of the role. |

### 2. Getting started with APIs

You can manage roles by calling role-related APIs. The following describes the application scenarios of APIs in this document.
- The API "CreateRole" is used to create a virtual sub-account (role), and specify the accounts allowed to assume the role.
- The API "AttachRolePolicy" is used to grant the specified role a set of permissions to access resources under your account.
- The API "DetachRolePolicy" is used to unbind a policy from a role.
- The API "GetRole" is used to obtain the details of a role.
- The API "DescribeRoleList" is used to get a list of the roles under your account.
- The API "UpdateAssumeRolePolicy" is used to modify the trust policy of the specified role.
- The API "UpdateRoleDescription" is used to modify the description of a role.
- The API "DeleteRole" is used to delete a role.

## STS-related APIs
Tencent Cloud Security Token Service (STS) is a cloud service that allows Tencent Cloud accounts (or CAM users) to manage short-term access permissions. With STS, you can issue credentials with custom validity period and access permissions to other users so that they can directly call Tencent cloud service APIs with STS temporary credentials.

### 1. Terms
The common terms involved in this document are as follows:

| Term | Full Name | Description |
| ------------ | ------------ | ------------ |
| policy | policy | The policy granted when you apply for temporary credentials for a user with federated identity. |
| durationSeconds | durationSeconds | The validity period set for the temporary credentials you applied for. |
| credentials | credentials | The credentials obtained via STS. |

### 2. Getting started with APIs

The STS APIs allow you to apply for temporary credentials with custom period of validity and access permissions.
- The API "GetFederationToken" is used to issue credentials with custom period of validity and access permissions to a user with federated identity (a user managed by your local account system).
- The API "AssumeRole" is used to get temporary credentials for the role that can be assumed by the user.

