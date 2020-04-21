## Overview

For resources stored in Tencent Cloud COS, different teams or users may need to be granted different access permissions. In Cloud Access Management (CAM), you can grant different permissions to different groups for them to manipulate buckets and objects, so that they can work together.

First, you need to understand a few key concepts: root account, sub-account (user), and user group. For detailed descriptions of the relevant terms and configurations of CAM, please see [CAM Glossary](https://intl.cloud.tencent.com/document/product/598/18564).

#### Root account
A root account is also known as a developer. When you sign up for a Tencent Cloud account, the system creates a root account identity for you to log in to the Tencent Cloud services. Tencent Cloud records your usage and bills you based on the root account.
By default, a root account has full access to the resources in the account. A root account can access billing information, change user passwords, create users and user groups, access other Tencent Cloud service resources, etc. By default, only a root account can access such resources. Any other users can only access them after they are authorized by a root account.

#### Sub-account (user) and user group
- A sub-account is an entity created by a root account. It has its ID and credentials and has the permission to log in to the Tencent Cloud Console.
- By default, a sub-account does not own resources. It needs to be authorized by a root account.
 - One root account can create multiple sub-accounts (users).
 - One sub-account can belong to multiple root accounts to assist them in managing their Tencent Cloud resources. However, at any specific time point, one sub-account can only log in under one root account to manage its Tencent Cloud resources.
- A sub-account can switch between developers (root accounts) in the console.
 - When a sub-account logs in to the console, it is under its default root account and has the access permissions granted by the root account.
 - After a sub-account switches from one root account to another, it will only have the access permissions granted by the current root account, but not the permissions granted by the previous one.
- A user group is a collection of multiple users (sub-accounts) with the same functions. You can create different user groups based on your business needs and associate them with appropriate policies to grant them different permissions.

## Directions
You can grant a sub-account access to COS in three steps: creating a sub-account, granting permissions to the sub-account, and accessing COS resources with the sub-account.

### Step 1. Create a sub-account
You can create a sub-account and configure the access permissions you want to grant in the CAM Console. Please follow the steps below:
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam).
2. Select **User** > **User List** > **Create User** to enter the user creation page.
3. Click **Custom Creation**, select the **Access resources and receive messages** type, and click **Next**.
4. Enter the user information as required.
 - **Username**: enter the name of the sub-user, such as `Sub_user`.
 - **Email**: enter an email address for the sub-user.
 - **Access Method**: select **Programming access** and **Tencent Cloud Console access**.
4. After entering the user information, click **Next** to perform authentication.
5. After the authentication is completed, grant permissions to the sub-user. Configure simple policies with the options provided such as granting permission for the account to access the COS bucket list or granting read-only permissions. To configure more complex polices, proceed to [Step 2. Grant permissions to the sub-account](#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E5.AF.B9.E5.AD.90.E8.B4.A6.E5.8F.B7.E6.8E.88.E4.BA.88.E6.9D.83.E9.99.90).
6. Click **Complete** to create the sub-account.


<span id="Grant permissions to the sub-account"></span>
### Step 2. Grant permissions to the sub-account
You can grant permissions to the sub-account by configuring policies for the sub-account (user) or user group in CAM.
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam).
2. Select **Policies** > **Create Custom Policy** > **Create by Policy Syntax** to enter the policy creation page.
3. Available templates include **a blank template** and **preconfigured policy templates** associated with COS. Select a policy template for the sub-account and click **Next**.
![](https://main.qcloudimg.com/raw/f656b0726b7575e3a4f435334ebe446f.png)
4. Enter an easy-to-remember policy name. If you select the **blank template**, you need to enter your policy syntax. For more information, please see [Sample Policies](#Sample Policies). You can copy and paste the policy content into the **Edit Policy Content** input box and click **Create Policy**.
![](https://main.qcloudimg.com/raw/334c6c5d253b7d1e5c44a204439ff703.png)
5. After you create a policy, associate it with the sub-account.
![](https://main.qcloudimg.com/raw/6e9316969ff0e1c00e523438902b2787.png)
6. Check the desired sub-account and confirm the authorization. Then, the sub-account can access the COS resources within the scope of the permissions.
![](https://main.qcloudimg.com/raw/defb10e7b31731f6059ed88878b9d506.png)

### Step 3. Access COS resources using the sub-account
To access COS using APIs or SDKs, you need to have the `APPID`, `SecretId`, and `SecretKey`.
When you access COS resources with a sub-account, you need to use the `APPID` of the root account and the `SecretId` and `SecretKey` of the sub-account. You can generate a `SecretId` and a `SecretKey` for the sub-account in the CAM Console.

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/capi) with your root account.
2. Select **User List** to enter the user list page.
3. Click the username of the sub-account to enter the sub-account details page.
4. Click **API Key** and click **Create Key** to create `SecretId` and `SecretKey` for the sub-account.


Now you can access the resources in COS using the `SecretId` and `SecretKey` of the sub-account and the `APPID` of the root account. 

>
>- To access COS resources with a sub-account, you need to do so using XML APIs or SDKs based on XML API.
>- To access COS resources with a sub-account, you need to use the `APPID` of the root account and the `SecretId` and `SecretKey` of the sub-account.

#### Example of access using the XML-based SDK for Java
Take the command line in the XML-based SDK for Java as an example. You need to enter the following parameters:
```
// 1. Initialize identity information
COSCredentials cred = new BasicCOSCredentials("<root account's APPID>", "<sub-account's SecretId>", "<sub-account's SecretKey>");
```

Below is an example:
```
// 1. Initialize identity information
COSCredentials cred = new BasicCOSCredentials("1250000000", "AKIDasdfmRxHPa9oLhJp", "e8Sdeasdfas2238Vi");
```

#### Example of access using COSCMD command line tool
Take the COSCMD `config` command line as an example. You need to enter the following parameters:
```sh
coscmd config -u <root account's APPID> -a <sub-account's SecretId> -s <sub-account's SecretKey>  -b <root account's bucketname> -r <root account's bucket region>
```
Below is an example:
```sh
coscmd config -u 1250000000 -a AKIDasdfmRxHPa9oLhJp -s e8Sdeasdfas2238Vi -b examplebucket -r ap-beijing
```


<span id="sample policies"></span>
## Sample Policies
Below are some sample policies for typical scenarios. When configuring a custom policy, you can copy and paste the following sample policies into the **Edit Policy Content** input box and make necessary changes based on your actual configuration. For more policy syntax for common COS scenarios, please see the **Business Cases** section in the [CAM product documentation](https://intl.cloud.tencent.com/document/product/598/11083).

### Configuring read/write permission for a sub-account
Configure read/write permission for a sub-account with the following policy:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cos:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        }
    ]
}
```
### Configuring read-only permission for a sub-account
Configure read-only permission for a sub-account with the following policy:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cos:List*",
                "name/cos:Get*",
                "name/cos:Head*",
                "name/cos:OptionsObject"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        }
    ]
}
```

### Configuring read/write permission to a specific IP range for a sub-account
In the following example, read/write permission is only granted to sub-accounts that use an IP address within the IP range of `192.168.1.0/24` and `192.168.2.0/24`.
For more conditions, please see [Condition](https://intl.cloud.tencent.com/document/product/598/10608).
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
    "cos:*"
            ],
            "resource": "*",
            "effect": "allow",
            "condition": {
                "ip_equal": {
                    "qcs:ip": ["192.168.1.0/24", "192.168.2.0/24"]
                }
            }
        }
    ]
}
```
