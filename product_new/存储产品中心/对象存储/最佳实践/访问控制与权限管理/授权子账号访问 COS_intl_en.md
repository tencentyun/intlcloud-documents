## Overview

For resources stored in Tencent Cloud COS, different teams or users need to be granted different access permissions. You can set different operation permissions for buckets and objects through CAM, so such teams and users can collaborate seamlessly.

First, you need to understand a few key concepts: root account, sub-account (user), and user group. For detailed descriptions of the relevant terms and configurations of CAM, see [CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583).

### Root Account
A root account is also known as a developer. When you applies for a Tencent Cloud account, the system will create a root account identity for you to log in to the Tencent Cloud services, which acts as the basis for resource usage and billing.
By default, the root account has full access to the resources under its name and can perform various operations such as accessing billing information, changing user passwords, creating users and user groups, and accessing other Tencent Cloud service resources. By default, such resources can only be accessed by the root account, and any other users can only access them after they are authorized by the root account.

### Sub-account (User) and User Group
- A sub-account is an entity created by the root account, has a definite ID and credentials, and has the permission to log in to the Tencent Cloud Console.
- The sub-account does not own resources by default and must be authorized by the root account.
 - One root account can create multiple sub-accounts (users).
 - One sub-account can belong to multiple root accounts to assist them in managing their respective Tencent Cloud resources, but at any specific time point, one sub-account can only log in to one root account to manage its Tencent Cloud resources.
- The sub-account can switch between developers (root accounts) in the console.
 - When the sub-account logs in to the console, it will be automatically switched to the default root account and have the access permissions granted by the default root account.
 - After switching the developer, the sub-account will have the access permissions granted by the root account switched to, and the access permissions granted by the root account before the switch will become invalid immediately.
- A user group is a collection of multiple users (sub-accounts) with the same functions. You can create different user groups based on your business needs and associate them with appropriate policies to grant them different permissions.

## Directions
You can grant a sub-account access to COS in three steps: **creating a sub-account**, **granting permissions to the sub-account**, and **accessing COS resources by the sub-account**.

### Step 1. Create a sub-account
A sub-account can be created in the CAM Console and granted access permissions in the following steps:
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam).
2. Click **User Management** > **Create User** as shown below.
![](https://main.qcloudimg.com/raw/a115caac7547c2c42f2b42db5b0c1064.png)
2. Click **Custom Create**.
![](https://main.qcloudimg.com/raw/bfaafac2fa40663afacbf16a5bdd97af.png)
3. Enter the user information as required.
 - **Username**: It can contain uppercase and lowercase letters [a-z, A-Z] numbers [0-9], and `@、._[]-:`.
 - **Email**: You need to enter an email address for the sub-user so that it can receive the message for WeChat binding sent by Tencent Cloud.
 - **Access Mode**: Select Programming access and Tencent Cloud Console access.
![](https://main.qcloudimg.com/raw/a35e5d654b74c71753d1233f832d4380.png)
4. Based on the policy options provided by the system, you can configure simple policies, such as granting access permission or read-only permission to the COS bucket list. To configure more complex polices, proceed to [Step 2. Grant permissions to the sub-account](#.E6.AD.A5.E9.AA.A4.E4.BA.8C.EF.BC.9A.E5.AF.B9.E5.AD.90.E8.B4.A6.E5.8F.B7.E6.8E.88.E4.BA.88.E6.9D.83.E9.99.90).
![](https://main.qcloudimg.com/raw/0a04c28edc18d021aea726b31a395758.png)
5. After confirming that the information entered is correct, click **Done** to create the sub-account.
![](https://main.qcloudimg.com/raw/fed32d27a9d6ca98f2f5c12ce690a5c3.png)

<span id="Grant permissions to the sub-account"></span>
### Step 2. Grant permissions to the sub-account
You can grant permissions to the sub-account by configuring policies for the sub-account (user) or user group in CAM.
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam).
2. Click **Policy Management** > **Create Custom Policy** as shown below.
![](https://main.qcloudimg.com/raw/4e43e50ed03836bf77de7883b4c60486.png)
2. Select **Create by Policy Syntax** to enter the creation page.
![](https://main.qcloudimg.com/raw/2b15a7e4f7965df8bf56179e19cd2168.png)
3. Available templates include **blank template** and **preset policy templates** associated with COS. Select a policy template for the sub-account and click **Next**.
![](https://main.qcloudimg.com/raw/f656b0726b7575e3a4f435334ebe446f.png)
4. Enter an easy-to-remember policy name. If you select a **blank template**, you need to enter your policy syntax. For more information, see [Sample Policies](#Sample Policies). You can copy and paste the policy content into the **Edit Policy Content** input box and click **Create a Policy**.
![](https://main.qcloudimg.com/raw/334c6c5d253b7d1e5c44a204439ff703.png)
5. After the creation is completed, associate the policy you just created to the sub-account.
![](https://main.qcloudimg.com/raw/6e9316969ff0e1c00e523438902b2787.png)
6. After you select the sub-account and confirm the authorization, the sub-account can access the COS resources within the scope of the permissions.
![](https://main.qcloudimg.com/raw/defb10e7b31731f6059ed88878b9d506.png)

### Step 3. Access COS resources by the sub-account
COS access (API or SDK) requires the following resources: APPID, SecretId, and SecretKey.
When the sub-account accesses the COS resources, it needs to use the APPID of the root account and the SecretId and SecretKey of its own. You can generate the SecretId and SecretKey for the sub-account in the CAM Console.

1. After the sub-account is logged in to the [CAM Console](https://console.cloud.tencent.com/cam/capi), the corresponding root account (developer account) should be switched to.
![](https://main.qcloudimg.com/raw/04ad2e89ac0c5908e1aaf05a956ebbfd.png)
2. After logging in, click **Create a Key** to create the SecretID and SecretKey for the sub-account. The APPID should be provided by the root account.
![11](https://main.qcloudimg.com/raw/aad60d287e1d43f1d4c2237f72c08874.png)

- The sub-account need to access COS resources via the XML API or the XML API-based SDK.
- When accessing COS resources, the sub-account needs to use the APPID of the root account and the SecretId and SecretKey of its own.

#### Access Example of XML-based SDK for Java
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

#### Access Example of COSCMD Command Line Tool
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
Below are some sample policies for typical scenarios. When configuring a custom policy, you can copy and paste the following sample policies into the **Edit Policy Content** input box and make necessary changes based on your actual configuration. For more policy syntax for common COS scenarios, see the **Business Cases** section in the [CAM product documentation](https://intl.cloud.tencent.com/document/product/598).

### Configuring Read/write Permission for a Sub-account
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
### Configuring Read-only Permission for a Sub-account
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

### Configuring Read/write Permission to a Specific IP Range for a Sub-account
In this example, the sub-account has read/write permission only to the IP ranges `192.168.1.0/24` and `192.168.2.0/24` as shown below:
For more effectiveness conditions, see [Effectiveness Conditions](https://intl.cloud.tencent.com/document/product/598/10608).
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
