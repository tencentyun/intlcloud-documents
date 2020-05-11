## Overview

[Tencent Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598) is a permission and access management service that helps you securely manage the access permissions to resources under your Tencent Cloud account. With CAM, you can create, manage and destroy users (groups) and use identity and policy management to control user access to Tencent Cloud resources.

## Permissions Manageable for SCF

SCF supports permission management through CAM. You can assign different permissions to sub-accounts or collaborators through your root account. Currently, SCF supports the following permission granularities:

| Service | Policy Syntax | TencentCloud API | Console | Authorization Granularity | Temporary Credential |
| ---------| ---------| ---------| ---------|---------|---------|
| SCF | ✔ | ✔ | ✔ | Resource level | ✔|

Currently, SCF supports the following TencentCloud APIs:

| API Name | Description | Level |
|---------|---------|---------|
| ListFunctions | Gets the function list under account | Account |
| GetAccountSettings | Get quota configuration under account | Account |
| CreateFunction | Creates function | Resource |
| DeleteFunction| Deletes specified function | Resource |
| InvokeFunction | Triggers function synchronously or asynchronously | Resource |
| UpdateFunction | Updates function, including configuration and/or code | Resource |
| SetTrigger | Configures trigger for specified function | Resource |
| DeleteTrigger | Deletes trigger for specified function | Resource |
| GetFunction | Gets the configuration information of specified function | Resource |
| ListVersion | Gets the version information of specified function | Resource |
| GetFunctionLogs | Gets the log information of specified function | Resource |
> When configuring the policy syntax, you also need to use the monitor APIs to get the monitoring information under the account. For the usage, please see the sample policy below.

## SCF Policy

### Policy syntax

SCF's policy syntax follows CAM's [syntax structure](https://intl.cloud.tencent.com/document/product/598/10604) and [resource description method](https://intl.cloud.tencent.com/document/product/598/10606), which is based on the JSON format, and all resources can be described in the six-segment style as shown in the sample below:
```
qcs: :scf:region:uin/uin—id:function/function-name
```

### Sample policy
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
- If the `action` is an operation that needs to be associated with a resource, the resource can be defined as `*`, indicating that all resources are associated.
- If the `action` is an operation that does not need to be associated with a resource, the resource needs to be defined as `*`.
- This sample allows the sub-account to have the operation permissions of certain functions under the root account. The resource in `resource` is described as a function under the root account.

### Specifying condition

The access policy language allows you to specify conditions when granting permissions, such as limiting the user access source or authorization time. The list below contains supported condition operators as well as general condition keys and examples.

<table>
<thead>
<tr>
<th style="width:20%">Condition Operator</th>
<th style="width:15%">Description</th>
<th style="width:15%">Condition Name</th>
<th style="width:50%">Example</th>
</tr>
</thead>
<tbody><tr>
<td>ip_equal</td>
<td>IP is equal to</td>
<td>qcs:ip</td>
<td><code>{"ip_equal":{"qcs:ip ":"10.121.2.0/24"}}</code></td>
</tr>
<tr>
<td>ip_not_equal</td>
<td>IP is not equal to</td>
<td>qcs:ip</td>
<td><code>{"ip_not_equal":{"qcs:ip ":["10.121.1.0/24", "10.121.2.0/24"]}}</code></td>
</tr>
<tr>
<td>date_not_equal</td>
<td>Date is not equal to</td>
<td>qcs:current_time</td>
<td><code>{"date_not_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}}</code></td>
</tr>
<tr>
<td>date_greater_than</td>
<td>Date is later than</td>
<td>qcs:current_time</td>
<td><code>{"date_greater_than":{"qcs:current_time":"2016-06-01T00:01:00Z"}}</code></td>
</tr>
<tr>
<td>date_greater_than_equal</td>
<td>Date is later than or equal to</td>
<td>qcs:current_time</td>
<td><code>{"date_greater_than_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}}</code></td>
</tr>
<tr>
<td>date_less_than</td>
<td>Date is earlier than</td>
<td>qcs:current_time</td>
<td><code>{"date_less_than":{"qcs:current_time":"2016-06-01T 00:01:00Z"}}</code></td>
</tr>
<tr>
<td>date_less_than_equal</td>
<td>Date is earlier than or equal to</td>
<td>qcs:current_time</td>
<td><code>{"date_less_than":{"qcs:current_time":"2016-06-01T 00:01:00Z"}}</code></td>
</tr>
<tr>
<td>date_less_than_equal</td>
<td>Date is earlier than or equal to</td>
<td>qcs:current_time</td>
<td><code>{"date_less_than_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}}</code></td>
</tr>
</tbody></table>

- To allow access only by IPs in the `10.121.2.0/24` IP range, use the following syntax:
```json
"ip_equal":{"qcs:ip ":"10.121.2.0/24"}
```
- To allow access only by IPs `101.226.\*\*\*.185` and `101.226.\*\*\*.186`, use the following syntax:
```json
"ip_equal": {
    "qcs:ip": [
      "101.226.***.185",
      "101.226.***.186"
    ]
}
```

## Role and Authorization

SCF implements the access between services and user resources by using the role capability of CAM. You can use the configuration role to enable a function to access user resources in the configuration process. You can also use the execution role to enable the function to apply for temporary authorization for executing the code, so that the code can implement permission and resource access through the role authorization mechanism.

For more information on roles and authorizations, please see [Role and Authorization](https://intl.cloud.tencent.com/document/product/583/31444).
