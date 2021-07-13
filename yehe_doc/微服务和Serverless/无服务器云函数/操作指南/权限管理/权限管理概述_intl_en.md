## Overview

SCF uses [Tencent Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598) to manage permissions. CAM is a permission and access management service that helps you securely manage the access permissions to resources under your Tencent Cloud account. With CAM, you can create, manage and destroy users and user groups and use identity and policy management to control user access to Tencent Cloud resources.

## Manageable Permissions for SCF
You can assign different SCF permissions to sub-accounts or collaborators through your root account. Currently, SCF supports the following permission granularities:

| Service | Policy Syntax | TencentCloud API | Console | Authorization Granularity | Temporary Credentials |
| ---------| ---------| ---------| ---------|---------|---------|
| SCF | ✔ | ✔ | ✔ | Resource level | ✔|

Currently, SCF supports the following TencentCloud APIs:

| API Name | Description | Level |
|---------|---------|---------|
| ListFunctions | Gets the function list under the account | Account |
| GetAccountSettings | Gets the quota configuration under the account | Account |
| CreateFunction | Creates a function | Resource |
| DeleteFunction| Deletes a specified function | Resource |
| InvokeFunction | Triggers a function synchronously or asynchronously | Resource |
| UpdateFunction | Updates a function, including its configuration and/or code | Resource |
| SetTrigger | Configures a trigger for a specified function | Resource |
| DeleteTrigger | Deletes a trigger for a specified function | Resource |
| GetFunction | Gets the configuration information of a specified function | Resource |
| ListVersion | Gets the version information of a specified function | Resource |
| GetFunctionLogs | Gets the log information of a specified function | Resource |

## Roles and Authorization
SCF implements the access between services and user resources by using the role capability of CAM. SCF offers the **configuration role** and the **execution role**. You can use the configuration role to enable SCF to access user resources in the configuration process. You can also use the execution role to enable SCF to apply for the temporary authorization for executing the code, so that the code can implement permission and resource access through the role authorization mechanism.
