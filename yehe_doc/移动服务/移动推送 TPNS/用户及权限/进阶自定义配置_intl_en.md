## Cloud Access Management Overview
If you use the TPNS service in Tencent Cloud, and the service is managed by different users sharing your Tencent Cloud account key, you may face the following problems:
- Your key is shared by multiple users, leading to high risk of compromise.
- You cannot limit the access permissions of other users, which poses a security risk due to potential faulty operations.

You can allow different users to manage different services through sub-accounts so as to avoid the above problems. By default, a sub-account does not have permission to use a TPNS service or related resources. Therefore, you need to create a policy to grant the required permission to the sub-account.
[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/zh/document/product/598) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.
When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, please see [Syntax Logic](https://intl.cloud.tencent.com/zh/document/product/598/10603). For more information on how to use CAM policies, please see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
If you do not need to manage the access permissions to TPNS resources for sub-accounts, you can skip this part. This will not affect your understanding and usage of other parts in the documentation.

## Policy Syntax Description
A CAM policy must authorize or deny the use of one or more TPNS operations. At the same time, it must specify the resources that can be used for the operations (which can be all resources or partial resources for certain operations). For TPNS operations that do not support resource-level authorization, you need to specify the authorized object as all resources.
CAM policy syntax description:
```
{     
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 
```

Parameter description:

| Parameter Name             | Required | Description                                       |
| ------------ | ---- | ---------------------------------------- |
| version   | Yes    | It is the version number. Currently, only "2.0" is allowed. |
|  statement      | Yes    | This element describes the details of one or more permissions. It contains a permission or permission set of other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one statement. An `action` (operation) describes an allowed or denied operation, which can be an API or a feature set (a set of specific APIs prefixed with `permid`). |
| resource  | Yes    |  This element describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify a resource, please see the documentation for the product whose resources you are writing a statement for. |
|condition    | No               | This element describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition. |
|effect    | Yes                | This element describes whether the statement result is an "allow" or "explicit deny".  |



## Creating Policy and Granting Permission
Two types of system-level policies are preset for you to quickly and easily grant permissions. You can go to the console > Access Management > [Policy Management](https://console.cloud.tencent.com/cam/policy), click **Create Custom Policy**, and select "Create by Policy Syntax" as shown below:
![](https://main.qcloudimg.com/raw/6feaa3a4a99112a79f6f61311273e7c6.png)
On the policy editing page, you can search and find two preset policy templates provided by TPNS, which grants the full access and read-only access, respectively (you can view the list of specific permissions during policy creation). You can select a template and edit it or create a blank template.
![](https://main.qcloudimg.com/raw/75082c251b9d0d7a534bfe36d4c8a9b5.png)
After creating a policy, you can find it on the [Policy Management](https://console.cloud.tencent.com/cam/policy) page in the CAM Console and associate it with sub-user to complete permission configuration.
This document describes how to grant TPNS permissions in CAM.

## Authorizable TPNS Resources
Resource-level permission can be used to specify which resources a user can manipulate. The type of resources that can be authorized in TPNS is "application", that is, you can grant resource-level permissions in CAM at the application granularity. The resource description method is as follows:
```
qcs::tpns::uin/1000000000:app/*
```
Here, `*` indicates all resources at the application granularity, which can be replaced with the `Access ID`. You can find the application's `Access ID` in the [Product Management](https://console.cloud.tencent.com/tpns) module in the TPNS Console. For the `uin`, get the account ID on the [Account Info](https://console.cloud.tencent.com/developer) page in the console and replace the `uin` with it (such as `1000000000`, which is a sample Tencent Cloud ID of a root account).

When authorizing multiple resources, separate them with commas.


## Authorizable TPNS Operations
In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with `name/tpns:` should be used for TPNS, such as `name/tpns:CreateProduct`.
To specify multiple operations in a single statement, separate them with commas as shown below:
``` 
"action":["tpns:action1","tpns:action2"]
```
You can also specify multiple operations by using a wildcard. For example, you can specify all operations beginning with "Describe" in name, as shown below:
``` 
"action":["tpns:Describe*"]
```
If you want to specify all operations in TPNS, use a wildcard "*" as shown below:
``` 
"action":["tpns:*"]
```

List of operations that can be authorized:
>!Only operations that support resource-level permissions can be authorized at the application level.

| Name | Description | Resource-Level Permission Supported |
| --- | --- | --- |
| AddChannelInfo | Adds vendor channel |Yes|
| CancelPush | Cancels scheduled push task |Yes|
| CreateApp | Creates application |No|
| CreateAppTrialRequest | Applies for product trial |Yes|
| CreateProduct | Creates product |No|
| DeleteAppInfo | Deletes application |Yes|
| DeleteProductInfo | Deletes product |No|
| DescribeApnsCertInfo | Queries APNS certificate information |Yes|
| DescribeAppAllTags | Queries all tag information |Yes|
| DescribeAppInfo | Queries application information |Yes|
| DescribeAppVipInfo | Queries VIP information |Yes|
| DescribeChannelInfo | Queries vendor channel information |Yes|
| DescribeProductInfo | Queries product information |No|
| DescribeTagTokenNums | Queries the quantity of devices under tag |Yes|
| DownloadPushPackage | Downloads push number package |Yes|
| DescribeAccountByToken | Queries account bound to device |Yes|
| DescribeAccountPushStatInfo | Queries the total number of push messages under account |No|
| DescribeAccountPushStatInfoAllZone | Queries the total number of messages supposed to be sent by all applications in cluster |No|
| DescribeAppSecretInfo | Queries `AppSecret` information |Yes|
| DescribeDeviceStatOverview | Queries the number of accumulated and daily active devices of application |Yes|
| DescribeProductDeviceStatWithRatioOverview | Queries application statistics |Yes|
| DescribePushPackaDescribeoken | Uploads number package to get temporary COS token |Yes|
| DescribePushTaskGroupStatAllChannel | Queries the aggregated data of pushes in all channels |Yes|
| DescribePushTaskStatAllChannel | Queries the data of each push channel |Yes|
| DescribeTagsByToken | Queries tags bound to device |Yes|
| DescribeTokenInfos | Queries `tokenInfo` information |No|
| DescribePushInfos | Queries push list |Yes|
| ModifyAppInfo | Updates application information |Yes|
| ModifyProductInfo | Updates product information |No|
| CreatePush | Creates push |Yes|
| UpdateAppStatus | Updates application status |Yes|
| UploadCert | Uploads iOS certificate |Yes|
| UploadPushPackage | Uploads push number package |Yes|
|DescribePlanPushInfos |  Queries the task list under push plan |Yes|
|DescribePushPlans      | Queries push plan list   | Yes|
|UpdatePushPlan          |Modifies push plan | Yes|
|DeletePushPlan           |Deletes push plan |Yes|
|CreatePushPlan        |Creates push plan |Yes |

## Sample Policy for Operator
Suppose the main responsibility of an operator is to view push records and create pushes, then the operation permissions can be queried according to the list of authorizable operations:
- All query operations.
- Canceling scheduled push task.
- Creating push.
- Uploading push number package.
- Downloading push number package.

Suppose the current root account ID is 1000000000 and the `Access_id` values of authorized applications are 1500000000 and 1500000001, respectively;
The corresponding policy syntax should be as follows:
```
//
{
    "version": "2.0",
    "statement": [
        { 
            "action": [
                "tpns:Describe*",
                "tpns:CancelPush",
                "tpns:DownloadPushPackage",
                "tpns:CreatePush",
                "tpns:UploadPushPackage"
            ],
            "resource": [
                "qcs::tpns::uin/1000000000:app/1500000000","qcs::tpns::uin/1000000000:app/1500000001"
            ],
            "effect": "allow"
        },
        {
            "action": [
                "tpns:Describe*"
            ],
            "resource": [
                "qcs::tpns::uin/1000000000:other/*"
            ],
            "effect": "allow"
        }

     ]
}
```
After creating a policy, you can find it on the [Policy Management](https://console.cloud.tencent.com/cam/policy) page of CAM and associate it with the sub-user to complete permission configuration. It can also be associated with other sub-users.

## Sample Policy for Developer
Suppose the main responsibility of a developer is to access and test and all operation permissions should be granted;
Suppose the current root account ID is 1000000000 and the `Access_id` values of authorized applications are 1500000000 and 1500000001, respectively;
The corresponding policy syntax should be as follows:
```
//
{
    "version": "2.0",
    "statement": [
        { 
            "action": "*",
            "resource": [
                "qcs::tpns::uin/1000000000:app/1500000000","qcs::tpns::uin/1000000000:app/1500000001"
            ],
            "effect": "allow"
        },
        {
            "action": [
                "tpns:Describe*"
            ],
            "resource": [
                "qcs::tpns::uin/1000000000:other/*"
            ],
            "effect": "allow"
        }

     ]
}
```
After creating a policy, you can find it on the [Policy Management](https://console.cloud.tencent.com/cam/policy) page of CAM and associate it with the sub-user to complete permission configuration. It can also be associated with other sub-users.


