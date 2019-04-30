Among companies or teams in a company, different access permissions to Tencent Cloud COS resources should be configured for different teams or personnel. You can use Cloud Access Management (CAM) to set permissions to perform different operations on buckets/objects to various teams or personnel.
This generally takes three steps: creating a sub-account, granting permissions to the sub-account, accessing resources using the sub-account.

First, we need to understand a few key concepts.
## Glossary
For CAM-related terms and configurations, see [CAM Overview](/doc/product/598/10583).
### Root Account
A root account represents a developer. When you apply for a Tencent Cloud account, a root account identity is created in the system to be used for logging in to Tencent Cloud services. The consumption of Tencent Cloud resources is calculated and billed with the root account as the primary consumer.
A root account has the full access to all the resources under it, including accessing the billing information of the account, modifying user password, creating users and user groups, and accessing other could service resources. By default, only the root account has access to the resources, and authorization from the root account is required for any access by any other users.

### Sub-account (user) and user group
- Sub-account is an entity created by the root account. It has an ID and identity credentials and has the permission to log in to Tencent Cloud console.
- A sub-account does not own any resource by default, and must be authorized by its root account to use the resources.
 - A root account can create multiple sub-accounts (users).
 - A sub-account can belong to multiple root accounts to assist different root accounts in managing their own cloud resources. But a sub-account can only log in to a single root account at a time to manage the cloud resources under this root account.
- A sub-account can switch from a root account to another one by switching the developer (the root account) on the console.
 - The sub-account can be automatically switched to the default root account when logging in to the console, and owns the access permissions granted by the root account.
 - After switching the developer, the sub-account owns the access permissions granted by the second root account, and the ones granted by the original root account become invalid immediately.
- A user group refers to a group of users (sub-accounts) who fulfill the same function. You can create multiple user groups as needed, then associate the user groups with specific policies to assign different permissions.

## Sub-account Permission Configuration
### Step 1: Create a sub-account
You can create a sub-account in the CAM Console, and grant it the access permissions. The specific operations are shown as below:
1. Log in to the [Cloud Access Management Console](https://console.cloud.tencent.com/cam), click **User Management** on the left navigation bar, and then click **Create User** on the page.
 ![](//mc.qcloudimg.com/static/img/5d9194888617f10bfde81afa01c69e0b/image.png)
 
2. Enter the user information as required.
 ![](//mc.qcloudimg.com/static/img/97dbdb848557f0195f90e1a78561eb37/image.png)
>!"Login account" can be the account for logging in to Tencent Cloud. You can add any of the following three types of accounts as the sub-account:
 - Email: Enter the email registered with Tencent Cloud or its account ID.
 - WeChat Official Account: Enter its Tencent Cloud account ID.
 - QQ number: Enter a QQ number or its account ID.

3. According to the policy options provided by the system, you can configure simple policies, such as read and write access, or read-only access to COS. To configure more complicated policies, see [Step 2: Grant permissions to sub-accounts](#对子账号授予权限).
![](//mc.qcloudimg.com/static/img/8c3be83e576d892c99b90190d5f5c0b2/image.png)

<span id="Grant permissions to sub-accounts"></span>
### Step 2: Grant permissions to sub-accounts
To grant permissions to sub-accounts, you can configure policies for sub-accounts (users) or user groups through CAM.
1. Log in to the [Cloud Access Management Console](https://console.cloud.tencent.com/cam), click **Policy Management** on the left navigation bar, select the **Custom Policy** tab, and then click **Create Custom Policy**.
![](//mc.qcloudimg.com/static/img/c1edfdc87bc078d8bc8f0fb052313d28/image.png)
2. Select **Create by Policy Syntax** to enter the creation page.
![](//mc.qcloudimg.com/static/img/94801671fcdff7b80dc973d9ee0e1165/image.png)
3. Blank template and existing COS templates are available to choose from based on your actual needs.
![](//mc.qcloudimg.com/static/img/8ee0f66634765849bb90a1a2d60806a5/image.png)
4. Edit the policy. For policies in common COS scenarios, see business use cases in the [CAM product documentation](/doc/product/598). You can copy and paste the policy content into the **Edit Policy Content** input box.
![](//mc.qcloudimg.com/static/img/2a5ce2ce4863f1a537dc74d45284ee5d/image.png)
5. After the policy is created, you can associate it to sub-accounts.
![](//mc.qcloudimg.com/static/img/3517b05ee79c818883d1ecf96dbbad89/image.png)
After being granted the permissions, the sub-accounts can access COS resources within the scope of their permissions.
![](//mc.qcloudimg.com/static/img/606cdbcdccb90cf65dbc8826bc7d92da/image.png)
 

This document also describes several typical scenarios with the following policy examples. For more information, see [Policy Examples](#策略示例):
- In COS, how to set the read and write access for sub-accounts?
- In COS, how to set the read-only access for sub-accounts?
- In COS, how to set the read/write access for an IP address range?

### Step 3: Access the COS resources of the root account using a sub-account
The following resources are needed to access COS via API or SDK: APPID, SecretId, and SecretKey.
When you access COS resources using a sub-account, the root account's APPID, and the sub-account's SecretId and SecretKey are required. You can create the SecretId and SecretKey on the CAM Console.
1. When logging in to the [Cloud Access Management Console](https://console.cloud.tencent.com/cam/capi) using a sub-account, you need to select the corresponding root account (the developer account).
![](//mc.qcloudimg.com/static/img/7f109890f04a9f57f3b8c924b3788e2d/image.png)
2. After login, click **Create Key** to create the SecretId and SecretKey of the sub-account. APPID should be provided by the root account.
![](//mc.qcloudimg.com/static/img/294e294ef54662dedf57af975b7bea75/image.png)


>!
- You need to access COS resources using a sub-account via XML API or SDK based on XML API.
- When you access COS resources using a sub-account, the root account's APPID, and the sub-account's SecretId and SecretKey are required.

#### Example of access via XML-based Java SDK
Taking the XML-based Java SDK command line as an example, you need to enter the following parameters:
```
// 1. Initialize user authentication information
COSCredentials cred = new BasicCOSCredentials("<Primary account's APPID>", "<Sub-account's SecretId>", "<Sub-account's SecretKey>");
```

Example:
```
// 1. Initialize user authentication information
COSCredentials cred = new BasicCOSCredentials("1250000011", "AKIDasdfmRxHPa9oLhJp9wqwraCdtzvfPasdfaqW", "e8Sdeasdfas2238ViAXjpkU6XloeN2Wpxue");
```

#### Example of access via COSCMD command line tool
Taking the COSCMD `config` command line as an example, you need to enter the following parameters:
```
coscmd config -u <Primary account's APPID> -a <Sub-account's SecretId> -s <Sub-account's SecretKey>  -b <Primary account's bucketname> -r <Primary account's bucketname region>
```
Example:
```
coscmd config -u 1250000011 -a AKIDasdfmRxHPa9oLhJp9wqwraCdtzvfPasdfaqW -s e8Sdeasdfas2238ViAXjpkU6XloeN2Wpxue -b bucket1 -r ap-beijing
```
<span id="Policy Examples"></span>
## Policy Examples
When configuring a custom policy, you can copy and paste the following reference policy into the [Edit Policy Content] input box and modify it based on the actual settings.

### Set the read and write access for sub-accounts
The following policy configures the read and write access for sub-accounts:
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
### Set the read-only access for sub-accounts
The following policy configures the read-only access for sub-accounts:
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
### Set the read/write access for an IP address range
The following policy configures the read/write access to the addresses within two IP address ranges: `192.168.1.0/24` and `192.168.2.0/24`:
For more information on how to specify conditions under which a policy should take effect, see [Conditions for Taking Effect](/doc/product/598/10608).
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

