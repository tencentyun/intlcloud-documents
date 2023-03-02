## Overview

You can set different operation permissions on COS buckets or objects through CAM, so that different teams or users in different companies or departments can better collaborate with each other .

To start with, you need to understand several terms: root account, sub-account (user), and user group. For CAM terms and the detailed description of configurations, please see CAM [Glossary](https://intl.cloud.tencent.com/document/product/598/18564).

#### Root account
A root account is also known as a developer. When you sign up for a Tencent Cloud account, the system creates a root account identity for you to log in to the Tencent Cloud services. Tencent Cloud records your usage and bills you based on the root account.

By default, a root account has full access to the resources in the account. A root account can access billing information, change user passwords, create users and user groups, access other Tencent Cloud service resources, etc. By default, only a root account can access such resources. Any other users can only access them after they are authorized by a root account.

#### Sub-account (user) and user group
- A sub-account is an entity created by the root account. It has an ID and identity credentials, as well as permission to log in to the Tencent Cloud console.
- By default, a sub-account does not own resources. It needs to be authorized by a root account.
 - One root account can create multiple sub-accounts (users).
 - One sub-account can belong to multiple root accounts to assist them in managing their Tencent Cloud resources. However, at any specific time point, one sub-account can only log in under one root account to manage its Tencent Cloud resources.
- A sub-account can switch between developers (root accounts) in the console.
 - When a sub-account logs in to the console, it is under its default root account and has the access permissions granted by the root account.
 - After a sub-account switches from one root account to another, it will only have the access permissions granted by the current root account, but not the permissions granted by the previous one.
- A user group is a collection of multiple users (sub-accounts) with the same functions. You can create different user groups based on your business needs and associate them with appropriate policies to grant them different permissions.

## Directions
You can grant a sub-account permission to access COS in three steps: creating a sub-account, granting permissions to the sub-account, and accessing COS resources with the sub-account.

### Step 1. Create a sub-account
You can create a sub-account in the CAM console and grant it access permissions. The specific operations are shown as below:
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam).
2. Select **User** > **User List** > **Create User** to enter the user creation page.
3. Select **Custom Creation**, set **Access Resources and Receive Messages**, and click **Next**.
4. Enter the user information as required.
 - **User Information**: Set the username (for example, Sub_user) and email address of the sub-account. The email address is needed to receive the email sent by Tencent Cloud to bind the sub-account with his/her Weixin account.
 - **Access Method**: Select **Programming access** and **Tencent Cloud console access**. Other configuration items can be set as needed.
4. Click **Next** and start identity verification.
5. Grant permissions to the sub-account. You can configure simple policies, such as granting the sub-account permission to access the COS bucket list or read-only permission, with the policy options provided. To configure a more complex policy, proceed to [Step 2. Grant permissions to the sub-account](#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E5.AF.B9.E5.AD.90.E8.B4.A6.E5.8F.B7.E6.8E.88.E4.BA.88.E6.9D.83.E9.99.90).
6. Set the user tag optionally and click **Next**.
7. Click **Finish**. In this way, the sub-account is created.


<span id="Grant permissions to the sub-account"></span>
### Step 2. Grant permissions to the sub-account


Create a custom policy or select an existing policy and associate it with the sub-account.

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam).
2. Choose **Policy** > **Create Custom Policy** > **Create by Policy Syntax** to go to the policy creation page.
3. You can select **Blank Template** to customize a permission policy as needed. You can also select a COS-associated **System Template**. Then, click **Next**.
4. Enter an easy-to-remember policy name. If you have selected **Blank Template**, enter the policy syntax. For more information, see [Sample Policies](#Sample policies). You can copy and paste the policy content into the **Policy Content** box and click **Finish**.
5. After you create a policy, associate it with the sub-account.
![](https://main.qcloudimg.com/raw/1495c8b19dfff2aad622b794d8f5bc6a.png)
6. Select the sub-account and click **Confirm** to complete the authorization.
![](https://main.qcloudimg.com/raw/3667de5320e99321a78c5d1c22a49157.png)

### Step 3. Access COS resources using the sub-account

The access methods (programming access and Tencent Cloud console access) mentioned in Step 1 are described as follows:

(1) Programming access

To use the programming access method (for example, using APIs, SDKs, or tools) to access COS resources with a sub-account, you need to obtain the `APPID` of the root account first. Besides, you need to go to the CAM console to generate `SecretId` and `SecretKey` of the sub-account as follows:

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) with the root account.
2. Click **User** > **User List**.
3. Click the name of the sub-account to go to the **User Details** page of the sub-account.
4. Click the **API Key** tab. Then, click **Create Key** to create `SecretId` and `SecretKey` for the sub-account.

After this, you can use this sub-account’s `SecretId` and `SecretKey`, as well as the root account’s `APPID` to access COS resources. 
>!To access COS resources with a sub-account, you need to use XML APIs or SDKs based on XML APIs.


#### Example of access using XML Java SDK

The following parameters need to be set if you use the XML Java SDK:
```
// Initialize the user authentication information
COSCredentials cred = new BasicCOSCredentials("<root account's APPID>", "<sub-account's SecretId>", "<sub-account's SecretKey>");
```

Example:
```
String secretId = System.getenv("secretId");// Sub-account's `SecretId`. Follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
String secretKey = System.getenv("secretKey");// Sub-account's `SecretKey`. Follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

// Initialize the user authentication information
COSCredentials cred = new BasicCOSCredentials("<root account's APPID>", secretId, secretKey);
```

#### Example of access using COSCMD command line tool

The following parameters need to be set if you use COSCMD:
```sh
coscmd config -u <root account's APPID> -a <sub-account's SecretId> -s <sub-account's SecretKey>  -b <root account's bucketname> -r <root account's bucket region>
```
Example:
```sh
coscmd config -u 1250000000 -a AKIDasdfmRxHPa9oLhJp**** -s e8Sdeasdfas2238Vi**** -b examplebucket -r ap-beijing
```


(2) Tencent Cloud console access

After the sub-user is granted permissions, they can enter the root account ID, sub-user name, and sub-user password on the [Sub-user Login](https://www.tencentcloud.com/account/login/subAccount) page to log in to the console. Then, they can click **Cloud Object Storage** in **Products** to access storage resources under the root account.

<span id="Sample policies"></span>
## Sample Policies
The following typical sample policies are provided herein. When configuring a policy, you can refer to the following code, copy and paste it into the **Policy Content** box, and modify it as needed. For more policy syntax for other common COS scenarios, see [Overview](https://intl.cloud.tencent.com/document/product/436/18023) or the business use cases parts of [Cloud Access Management](https://www.tencentcloud.com/document/product/598).

### Sample 1. Granting the sub-account full read/write permissions for COS access

>!This policy grants a large range of permissions to the sub-account. Please configure it with caution.

The policy is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action":[
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

### Sample 2. Granting the sub-account read-only permission
The following policy grants the sub-account read-only permission:
```
{
    "version": "2.0",
    "statement": [
        {
            "action":[
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


### Sample 3. Granting the sub-account write-only permission (excluding deletion)

The policy is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action":[
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload",
                "cos:ListMultipartUploads"
            ],
            "resource": "*"
        }
    ]
}
```


### Sample 4. Granting the sub-account read/write permission for a certain IP range
The following sample grants read/write permission only for the `192.168.1.0/24` and `192.168.2.0/24` IP address ranges:
To enter more conditions, see [Conditions](https://www.tencentcloud.com/document/product/598/10608).
```
{
    "version": "2.0",
    "statement": [
        {
            "action":[
    "cos:*"
            ],
            "resource": "*",
            "effect": "allow",
            "condition":{
                "ip_equal":{
                    "qcs:ip": ["192.168.1.0/24", "192.168.2.0/24"]
                }
            }
        }
    ]
}
```

