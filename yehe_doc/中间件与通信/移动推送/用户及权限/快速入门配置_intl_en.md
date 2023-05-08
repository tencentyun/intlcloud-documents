
This document describes how to create and authorize sub-users. If you have never used Tencent Cloud Access Management (CAM), read this document for more information on the configuration.

Tencent Push Notification Service uses CAM for permission management. You need to authorize applications, create sub-users, and grant application permissions to the sub-users. For detailed directions, see the following sections.

## Creating a Sub-User
1. Go to the [CAM console](https://console.cloud.tencent.com/cam) and click **Create User**.
![](https://qcloudimg.tencent-cloud.cn/raw/f66c0500cc623b161f611bba8b1a0c4c.png)
2. Click **Custom Creation** to enter the **Create Sub-user** page (this example is based on the custom creation method).
![](https://qcloudimg.tencent-cloud.cn/raw/08e0b1bc2080def5772794dd97202a36.png)
3. Configure the login information of the sub-user as instructed and grant the sub-user application permissions in the **User Permissions** step.


## Granting Application Permissions
#### Granting permissions of all applications in a centralized manner
1. Continue with the **User Permissions** page mentioned in the previous step.
![](https://qcloudimg.tencent-cloud.cn/raw/01df52c8be53b93b22675e284849650d.png)
2. Enter **Tencent Push Notification Service** in the search box. In the search results, there are two default preset permissions as listed below:

| Policy Name | Permission Scope |
| --- | --- |
| QcloudTPNSFullAccess | All permissions on all the applications under the root account |
| QcloudTPNSReadOnlyAccess | Data read and push permissions on all applications under the root account |

#### Granting permissions of selected applications

1. Click **Create Custom Policy**.
![](https://qcloudimg.tencent-cloud.cn/raw/6741b778bc804388134b3d97d68fe433.png)
2. On the displayed page, select **Create by Policy Syntax**.
![](https://qcloudimg.tencent-cloud.cn/raw/9f875d430a89c2270aa0cdbf63a3d020.png)
3. Select **Blank Template**.
![](https://qcloudimg.tencent-cloud.cn/raw/3b7d9e84a1a3db6b24506f659b8a77bc.png)
4. Click **Next** to enter the syntax creation page.
![](https://qcloudimg.tencent-cloud.cn/raw/de89a170da2bb02f20f7e2be15ae5a4a.png)
>?
>- Enter an easy-to-remember policy name.
>- Copy the code provided in this document and replace the account ID and Access_ID in it with your own account ID and Access_ID, which can be found on the account information page under the current root account and the Tencent Push Notification Service product management page in the console respectively.
>
Copy the following syntax code:
```
{
    "version": "2.0",
    "statement": [
        { 
            "action":[
                "tpns:Describe*",
                "tpns:CancelPush",
                "tpns:DownloadPushPackage",
                "tpns:CreatePush",
                "tpns:UploadPushPackage"
            ],
            "resource": [
                "qcs::tpns::uin/1000000000:app/1500000000"
            ],
            "effect": "allow"
        },
        {
            "action":[
                "tpns:Describe*"
            ],
            "resource": [
                "qcs::tpns::uin/1000000000:/*"
            ],
            "effect": "allow"
        }

     ]
}
```
Replace parameters in the syntax code as follows:
 - Replace the ID of the root account: enter the [Account Information](https://console.cloud.tencent.com/developer) page under the current root account, copy the account ID, and replace `1000000000` in the syntax above with it.
>?If your current login account is a collaborator or sub-account, you need to get the account ID from the owner of the root account that grants you permissions.
![](https://qcloudimg.tencent-cloud.cn/raw/82f946f2d0dc124a634d6398531d3f89.png)
 - Replace the application `Access_ID`: go to the [Product Management page](https://console.cloud.tencent.com/tpns) in the Tencent Push Notification Service console, copy the `Access_ID` of the application whose permissions you want to grant, and replace `1500000000` in the syntax above with it. If you want to grant permissions of multiple applications, you can change `resource` to:
`"qcs::tpns::uin/1000000000:app/{Application Access_ID 1}"`,`"qcs::tpns::uin/1000000000:app/{Application Access_ID 2}"`
>?Please delete "{" and "}" in actual use. For detailed directions, please see [Advanced Custom Configuration](https://www.tencentcloud.com/document/product/1024/35288).
5. Go back to the user creation page.
![](https://qcloudimg.tencent-cloud.cn/raw/b8806c04fccc0c79d3021c45133f22a7.png)
Search for the created policy by name, select it, click **Next**, and click **Complete**.
6. After the permission configuration, you can select **Sub-User Login** on the login page to verify the account permissions.
