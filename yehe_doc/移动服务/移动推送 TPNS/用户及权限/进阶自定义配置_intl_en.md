## Overview
If you use the TPNS service in Tencent Cloud, and the service is managed by different users sharing your Tencent Cloud account key, the following problems may occur:
- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from misoperations due to the lack of user access control.

You can allow different users to manage different services through sub-accounts to avoid the above problems. By default, a sub-account does not have permission to use a TPNS service or related resources. Therefore, you need to create a policy to grant the required permission to the sub-account.
Tencent Cloud’s [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598) is a web service that helps you manage the access permissions for resources under your Tencent Cloud accounts. With CAM, you can create, manage, or terminate users (groups), and manage identities and policies to allow specific users to access and use specific Tencent Cloud resources.
You can use CAM to associate a user/user group with a policy, which allows/denies the user to use specified resources to perform specified tasks. For CAM policy basics, please see [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/33415). For the use of CAM policies, please see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).

>?If you do not need to manage access permissions to TPNS resources for sub-accounts, you can skip this part. This will not affect your understanding and use of other parts of the documentation.

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

| Parameter | Required | Description |
| ------------ | ---- | ---------------------------------------- |
| version  | Yes | Version number. Currently, only "2.0" is supported. |
|  statement      | Yes    | This element describes the details of one or more permissions. It contains a permission or permission set of other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one statement. An `action` (operation) describes an allowed or denied operation, which can be an API or a feature set (a set of specific APIs prefixed with `permid`). |
| resource | Yes | The specific resource. A resource is described in a six-segment format. Detailed resource definitions vary with the products. For more information about how to specify a resource, please see the documentation of the corresponding product. | Yes   |
| condition | No | The condition for the policy to take effect. A condition consists of the operator, action key, and action value. A condition value may be the time, IP address, etc. Some services allow you to specify additional values in a condition.  | No   |
| effect | Yes | Describes whether the statement result is "allowed" (`allow`) or "explicitly denied" (`deny`). |



## Creating Policy and Granting Permissions
Two types of system-level policies are preset for you to quickly grant permissions. You can go to the console > Cloud Access Management > [Policies](https://console.cloud.tencent.com/cam/policy), click **Create Custom Policy**, and select **Create by Policy Syntax**, as shown below:
![](https://main.qcloudimg.com/raw/6feaa3a4a99112a79f6f61311273e7c6.png)
On the **Create by Policy Syntax** page, you can search and find two preset policy templates, which grants full access and read-only access, respectively (you can view the list of specific permissions during policy creation). You can select a template and edit it or create a blank template.
![](https://main.qcloudimg.com/raw/75082c251b9d0d7a534bfe36d4c8a9b5.png)
After creating a policy, you can find it on the [Policies](https://console.cloud.tencent.com/cam/policy) page in the CAM console and associate it with a sub-user to complete the permission configuration.
This document describes how to perform CAM authorization in TPNS.
## Authorizable TPNS Resources
Resource-level permission can be used to specify which resources a user can manipulate. The type of resources that can be authorized in TPNS is "app", that is, you can grant resource-level permissions in CAM at the app granularity. The resource description method is as follows:
```
qcs::tpns::uin/1000000000:app/*
```
Here, `*` indicates all resources at the app granularity, which can be replaced with the `Access ID`. You can find the app's `Access ID` in the [Product Management](https://console.cloud.tencent.com/tpns) module in the TPNS Console. For the `uin`, get the account ID on the [Account Info](https://console.cloud.tencent.com/developer) page in the console and replace the `uin` with it (such as `1000000000`, which is a sample Tencent Cloud ID of a root account).

When authorizing multiple resources, separate them with commas.


## TPNS Operations That Can Be Authorized
In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with`name/tpns:` should be used for TPNS, such as `name/tpns:CreateProduct`.
To specify multiple operations in a single statement, separate them with commas as shown below:
``` 
"action":["tpns:action1","tpns:action2"]
```
You can also specify multiple operations using a wildcard. For example, you can specify all operations whose names begin with "Describe" as shown below:
``` 
"action":["tpns:Describe*"]
```
To specify all TPNS operations, use an asterisk (*) as follows:
``` 
"action"：["tpns:*"]
```

The following table describes the list of authorizable operations:

>!Only operations that support resource-level permissions can be authorized at the app level.

| Operation | Description | Resource-Level Permission Supported |
| --- | --- | --- |
| AddChannelInfo | Adds vendor-specific channel |Yes|
| CancelPush | Cancels scheduled push task |Yes|
| CreateApp | Creates app |No|
| CreateAppTrialRequest | Applies for product trial |Yes|
| CreateProduct | Creates product |No|
| DeleteAppInfo | Deletes app |Yes|
| DeleteProductInfo | Deletes product |No|
| DescribeApnsCertInfo | Queries APNS certificate information |Yes|
| DescribeAppAllTags | Queries all tag information |Yes|
| DescribeAppInfo | Queries app information |Yes|
| DescribeAppVipInfo | Queries VIP information |Yes|
| DescribeChannelInfo | Queries vendor-specific channel information |Yes|
| DescribeProductInfo | Queries product information |No|
| DescribeTagTokenNums | Queries the number of devices under the tag |Yes|
| DownloadPushPackage | Downloads push number package |Yes|
| DescribeAccountByToken | Queries account bound to device |Yes|
| DescribeAccountPushStatInfo | Queries the total number of push messages under account |No|
| DescribeAccountPushStatInfoAllZone | Queries the total number of messages supposed to be sent by all apps in cluster |No|
| DescribeAppSecretInfo | Queries `AppSecret` information |Yes|
| DescribeDeviceStatOverview | Queries the number of accumulated and daily active devices of app |Yes|
| DescribeProductDeviceStatWithRatioOverview | Queries app statistics |Yes|
| DescribePushPackaDescribeoken | Uploads number package to get temporary COS token |Yes|
| DescribePushTaskGroupStatAllChannel | Queries the aggregated data of pushes in all channels |Yes|
| DescribePushTaskStatAllChannel | Queries the data of each push channel |Yes|
| DescribeTagsByToken | Queries tags bound to device |Yes|
| DescribeTokenInfos | Queries `tokenInfo` information |No|
| DescribePushInfos | Queries push list |Yes|
| ModifyAppInfo | Updates app information |Yes|
| ModifyProductInfo | Updates product information |No|
| CreatePush | Creates push |Yes|
| UpdateAppStatus | Updates app status |Yes|
| UploadCert | Uploads iOS certificate |Yes|
| UploadPushPackage | Uploads push number package |Yes|
| DescribePlanPushInfos | Queries the task list under the push plan | Yes |
| DescribePushPlans | Queries the list information about the push plan | Yes |
| UpdatePushPlan | Modifies a push plan | Yes |
| DeletePushPlan | Deletes a push plan | Yes |
| CreatePushPlan | Creates a push plan | Yes |

## Sample Policy for Operations Personnel
Suppose that the main responsibilities of the operations personnel are to view push records and create pushes. Then, the operation permissions can be queried according to the list of authorizable operations above:
- All query operations
- Canceling scheduled push tasks
- Creating pushes
-  Uploading push number packages
-  Downloading push number packages

Assume that the root account ID is `1000000000`, and the `Access_id` values of the authorized applications are `1500000000` and `1500000001`, respectively.
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
The created policy can be found at [Policies](https://console.cloud.tencent.com/cam/policy) in the CAM console. You can associate it with the sub-user to complete the permission configuration. Note that the policy can also be associated with other sub-users.

## Sample Policy for Developers
Suppose that the main responsibilities of developers are to access and test. Then, all operation permissions should be granted.
Assume that the root account ID is `1000000000`, and the `Access_id` values of the authorized applications are `1500000000` and `1500000001`, respectively.
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
The created policy can be found at [Policies](https://console.cloud.tencent.com/cam/policy) in the CAM console. You can associate it with the sub-user to complete the permission configuration. Note that the policy can also be associated with other sub-users.


