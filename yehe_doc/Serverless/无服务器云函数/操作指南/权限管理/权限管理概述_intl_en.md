## Overview

SCF uses [Tencent Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598) to manage permissions. CAM is a permission and access management service that helps you securely manage the access permissions to resources under your Tencent Cloud account. With CAM, you can create, manage and destroy users (groups) and use identity and policy management to control user access to Tencent Cloud resources.

## Permissions Manageable for SCF
You can assign different SCF permissions to sub-accounts or collaborators through your root account. Currently, SCF supports the following permission granularities:

| Service | Policy Syntax | TencentCloud API | Console | Authorization Granularity | Temporary Credentials |
| ---------| ---------| ---------| ---------|---------|---------|
| SCF | ✔ | ✔ | ✔ | Resource level | ✔|

Currently, SCF supports the following TencentCloud APIs:

| API Name | Description | Level |
|---------|---------|---------|
| ListFunctions | Gets the function list under account | Account |
| GetAccountSettings | Gets quota configuration under account | Account |
| CreateFunction | Creates function | Resource |
| DeleteFunction| Deletes specified function | Resource |
| InvokeFunction | Triggers function synchronously or asynchronously | Resource |
| UpdateFunction | Updates function, including configuration and/or code | Resource |
| SetTrigger | Configures trigger for specified function | Resource |
| DeleteTrigger | Deletes trigger for specified function | Resource |
| GetFunction | Gets the configuration information of specified function | Resource |
| ListVersion | Gets the version information of specified function | Resource |
| GetFunctionLogs | Gets the log information of specified function | Resource |

## Role and Authorization
SCF implements the access between services and user resources by using the role capability of CAM. SCF offers **configuration role** and **execution role**. You can use the configuration role to enable SCF to access user resources in the configuration process. You can also use the execution role to enable SCF to apply for temporary authorization for executing the code, so that the code can implement permission and resource access through the role authorization mechanism.
