## CAM Overview
Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage and control access permissions, resources, and use permissions of your Tencent Cloud account. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

Serverless SSR supports **resource-level authorization**. You can use policy syntax to grant sub-accounts permissions to manage individual resources. For more information, please see [Authorization Scheme Examples](#examples).

## Authorizable Resource Types
Serverless SSR supports resource-level authorization. You can grant a specified sub-account the API permission of a specified resource. APIs supporting resource-level authorization include:

| API Name | Description | Six-Segment Example of Resource |
|---------|---------|---------|
| SaveInstance | Saves the instance information of component | `qcs::sls:${Region}:uin/:appname/${AppName}/stagename/${StageName}` |
| GetInstance | Gets the instance information of component |`qcs::sls:${Region}:uin/:appname/${AppName}/stagename/${StageName}` |
| ListInstances | Gets the instance list information of component | `qcs::sls:${Region}:uin/:appname/${AppName}/stagename/${StageName}`|
| RunComponent | Runs component instance |`qcs::sls:${Region}:uin/:appname/${AppName}/stagename/${StageName}` |
| RunFinishComponent | Finishes running component instance | `qcs::sls:${Region}:uin/:appname/${AppName}/stagename/${StageName}`|

<span id="examples"></span>

## Authorization Scheme Examples
### Six-Segment resource description
| Parameter | Required | Description |
|---------|---------|---------|
| qcs | Yes | Tencent Cloud service abbreviation, which indicates a resource of Tencent Cloud. |
| project_id | Yes | Project information description, which is only used to enable compatibility with legacy CAM logic. |
| service_type |  Yes  | Product abbreviation, which is `sls` for Serverless Framework. |
| region | Yes | Region information, such as `bj`. For more information, please see [Region List](https://intl.cloud.tencent.com/document/product/213/6091). |
| account | No | Root account of resource owner, such as `uin/164256472`. If it is empty, it indicates the root account of the CAM user who creates the policy. |
| resource | Yes | Detailed resource information of each product, which is `qcs::sls:${Region}:uin/:appname/${AppName}/stagename/${StageName}` for Serverless Framework |

### Sample
You can log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) as a root account to configure and manage the permissions of Serverless Framework. Currently, Serverless Framework provides two preset policies for **full access permission** and **read-only access permission**:

#### Full access permission
- Grant a sub-account full access to Serverless Framework (SLS).
- Policy name: QcloudSLSFullAccess

```json
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "sls:*"
      ],
      "resource": "*",
      "effect": "allow"
    }
  ]
}
```

#### Read-only access permission
- Grant a sub-account read-only access to Serverless SSR (SLS).
- Policy name: QcloudSLSReadOnlyAccess

```json
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "sls:Get*",
        "sls:List*"
      ],
      "resource": "*",
      "effect": "allow"
    }
  ]
}
```

## Sub-account Resource Management
- The sub-account can access and manage the resources authorized to it by the root account.
- If the sub-account has the permission to create resources and pay bills, it can purchase resources by itself in the normal process, and the root account will be charged.


