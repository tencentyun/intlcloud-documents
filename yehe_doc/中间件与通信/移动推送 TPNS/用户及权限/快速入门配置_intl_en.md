
This document describes how to create and authorize sub-users. If you have never used Tencent Cloud Access Management (CAM), please read this document for more information on the configuration.

TPNS uses CAM for permission management. You need to authorize applications, create sub-users, and grant application permissions to the sub-users. For detailed directions, please see the following sections.

## Creating a Sub-User
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) and click **Create User**.
![](https://main.qcloudimg.com/raw/5748b2815c001fda0e9c53b4150cabe0.png)
2. The following describes the custom creation method. Click **Custom Create** to enter the **Create Sub-user** page.
![](https://main.qcloudimg.com/raw/2eaf4e9b04c38cd73fdc542040ff40d4.png)
3. Configure the login information of the sub-user as instructed and grant the sub-user application permissions on the **Setting User Permission** page.


## Granting Application Permissions
#### Granting permissions of all applications in a centralized manner
1. Continue from the last step in the previous section as shown below:
![](https://main.qcloudimg.com/raw/99b2092998ca4fe0388f8f675991fcb0.png)
2. Enter "TPNS" in the search box. In the search results, there are two default preset permissions as listed below:

| Policy Name | Permission Scope |
| --- | --- |
| QcloudTPNSFullAccess | Grants all permissions of all applications under the root account |
| QcloudTPNSReadOnlyAccess | Grants read and push permissions of all applications under the root account |

#### Granting permissions of selected applications

1. Click **Create Custom Policy**.
![](https://main.qcloudimg.com/raw/d1cd0a4933398923aa109dfc34e67128.png)
2. On the displayed page, select **Create by Policy Syntax** as shown below.
![](https://main.qcloudimg.com/raw/0bf98c5b3c21003369dbd7a745bc885e.png)
3. Select **Blank Template**.
![](https://main.qcloudimg.com/raw/a39dd84e81eb01cfb17f2b47152b0461.png)
4. Click **Next** to enter the syntax creation page as shown below.
![](https://main.qcloudimg.com/raw/07d666185cd1d54b27f1e6a6aaf40142.png)
Copy the following syntax code:
```
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
                "qcs::tpns::uin/1000000000:app/1500000000"
            ],
            "effect": "allow"
        },
        {
            "action": [
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
- Replace the ID of the root account: enter the [Account Info](https://console.cloud.tencent.com/developer) page under the current root account, copy the account ID, and replace `1000000000` in the syntax above with it.
>?If your current login account is a collaborator or sub-account, you need to get the account ID from the owner of the root account that grants you permissions.

![](https://main.qcloudimg.com/raw/dabad6214ed659ea1a218b5e87ce4108.png)
- Replace the application `Access_ID`: log in to the [TPNS console](https://console.cloud.tencent.com/tpns), copy the `Access_ID` of the application whose permissions you want to grant, and replace `1500000000` in the syntax above with it. If you want to grant permissions of multiple applications, you can change `resource` to:
`"qcs::tpns::uin/1000000000:app/{application Access_ID1}"`,`"qcs::tpns::uin/1000000000:app/{application Access_ID2}"`

>?Please delete "{" and "}" in actual use. For detailed directions, please see [Advanced Custom Configuration](https://intl.cloud.tencent.com/document/product/1024/35288).

5. Return to the user creation page.
![](https://main.qcloudimg.com/raw/b85068f6796a0c762ec2fa22411fd24b.png)
Search for the created policy by name, select it, click **Next**, and click **Complete**.
6. After the permission configuration, you can select **Sub-User Login** on the login page to verify the account permissions.
![](https://main.qcloudimg.com/raw/eeb29bbdfdcb602e9a2ddab2b848f68b.png)
