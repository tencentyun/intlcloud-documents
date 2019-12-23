## Overview

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598) is a permission and access management service offered by Tencent Cloud, helping you securely manage the access permissions to resources under your Tencent Cloud account. With CAM, you can create, manage and destroy users (groups) and use identity and policy management to control user access to Tencent Cloud resources.

## Permissions Manageable for SCF

SCF supports permission management through CAM. You can assign different permissions to sub-accounts or collaborators through your master account. The permission levels currently supported by SCF are as follows:

| Service | Policy syntax | TencentCloud API | Console | Authorization | Temporary certificate |
| ---------| ---------| ---------| ---------|---------|---------|
| SCF | ✔ | ✔ | ✔ | Resource level | ✔ |

The TencentCloud APIs currently supported by SCF include:

| API name | Description | Level |
|---------|---------|---------|
| ListFunctions | Get the list of functions under the account | Account |
| GetAccountSettings | Get the quota configuration under the account | Account |
| CreateFunction | Create a function | Resource |
| DeleteFunction| Delete the specified function | Resource |
| InvokeFunction | Trigger the function synchronously or asynchronously | Resource |
| UpdateFunction | Update the function, including configuration and/or code | Resource |
| SetTrigger | Configure a trigger for the specified function | Resource |
| DeleteTrigger | Delete the trigger for the specified function | Resource |
| GetFunction | Get the configuration information of the specified function | Resource |
| ListVersion | Get the version information of the specified function | Resource |
| GetFunctionLogs | Get the log information of the specified function | Resource |
>! When configuring the policy syntax, you also need to use the monitor-related APIs to obtain the monitoring information under the account. For the usage, see the sample policy below.

## SCF Policy

### Policy Syntax

SCF's policy syntax follows CAM's [syntax structure](https://intl.cloud.tencent.com/document/product/598/10604) and [resource describing method](https://intl.cloud.tencent.com/document/product/598/10606), which is based on the JSON format, and all resources can be described in the six-segment style as shown in the sample below:
```
qcs: :scf:region:uin/uin—id:function/function-name
```

### Sample Policy
```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"allow", 
              "action":
              [
                "scf:ListFunctions",
                "scf:GetAccountSettings",
                "monitor:*"
              ], 
              "resource":["*"]  
           }, 
          { 
             "effect": "allow",
             "action": 
             [
                "scf:DeleteFunction",
                "scf:CreateFunction",
                "scf:InvokeFunction",
                "scf:UpdateFunction",
                "scf:GetFunctionLogs",
                "scf:SetTrigger",
                "scf:DeleteTrigger",
                "scf:GetFunction",
                "scf:ListVersion"
            ],
            "resource": 
            [
                "qcs::scf:gz:uin/******:function/Test1",
                "qcs::scf:gz:uin/******:function/Test2"
            ]
         }
      ] 
} 
```
- If an action is one that needs to associate with a resource, the resource is defined as `*`, indicating that all resources are associated.
- If an action is one that does not needs to associate with a resource, the resource needs to be defined as `*`.
- This sample allows the sub-account to have the action permissions of certain functions under the master account. The resource in "resource" is described as a function under the master account.

## Role and Authorization

SCF implements the access between services and user resources by using the role capability of CAM. By configuring roles, SCF can access user resources in the configuration process. By using executing roles, SCF can apply temporary role authorization for code execution, so that permission and resource access for code can be realized via role authorization.

For details on roles and authorizations, see [Role and Authorization](https://cloud.tencent.com/document/product/583/32389).
