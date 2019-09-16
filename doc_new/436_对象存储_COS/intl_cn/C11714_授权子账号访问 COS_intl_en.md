## Overview

For resources stored in Tencent Cloud COS, different teams or users may need to be granted different access permissions. In Cloud Access Management (CAM), you can grant different permissions to different groups for them to operate buckets and objects so that different teams and users can work together.

First, let’s take a look at a few key concepts: root account, sub-account (user), and user group. For detailed descriptions of CAM terms and configurations, see [CAM Overview](/doc/product/598/10583).

### Root Account
A root account is also known as a developer. When you sign up for a Tencent Cloud account, the system creates a root account identity for you to log in to the Tencent Cloud services. Tencent Cloud records your usage and bills you based on the root account.
By default, a root account has full access to the resources in the account. A root account can access billing information, change user passwords, create users and user groups, access other Tencent Cloud service resources, etc. By default, only a root account can access such resources. Any other users can only access them after they are authorized by a root account.

### Sub-account (User) and User Group
- A sub-account is an entity created by a root account. It has its ID and credentials, and has the permission to log in to the Tencent Cloud Console.
- By default, a sub-account does not own resources. It needs to be authorized by a root account.
 - One root account can create multiple sub-accounts (users).
 - One sub-account can belong to multiple root accounts to assist them in managing their Tencent Cloud resources. However, at any specific time point, one sub-account can only log in under one root account to manage its Tencent Cloud resources.
- A sub-account can switch between developers (root accounts) in the console.
 - When a sub-account logs in to the console, it is under its default root account and has the access permissions granted by the root account.
 - After a sub-account switches from one root account to another, it will only have the access permissions granted by the current root account, but not the permissions granted by the previous one.
- A user group is a collection of multiple users (sub-accounts) with the same functions. You can create different user groups based on your business needs and associate them with appropriate policies to grant them different permissions.
 
## Directions
You can grant a sub-account access to COS in three steps: **creating a sub-account**, **granting permissions to the sub-account**, and **accessing COS resources with the sub-account**.

### Step 1. Create a sub-account
You can create a sub-account and configure the access permissions you want to grant the account in the CAM Console. Please follow the steps below:
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam).
2. Click **User** > **Create a User** as shown below.
![](https://main.qcloudimg.com/raw/7b1bcd172ca430dd5d022dbd7bc9764c.png)
2. Click **Custom Creation**.
![](https://main.qcloudimg.com/raw/1e3b845388d0f66ca80db92c5ee27c9f.png)
3. Enter the user information as required.
 - **Username**: it can contain uppercase and lowercase letters [a-z, A-Z], numbers [0-9], and `@、._[]-:`.
 - **Email**: you need to enter an email address for the sub-account.
 - ** Access Method**: Select **Programming access ** and **Tencent Cloud Console access**.
![](https://main.qcloudimg.com/raw/ccb56ea4d723988e541b9a93ef5ebd45.png)
4. Configure simple policies with the options provided such as granting permission for the account to access the COS bucket list or granting read-only permissions. To configure more complex polices, proceed to [Step 2. Grant permissions to the sub-account](#.E6.AD.A5.E9.AA.A4.E4.BA.8C.EF.BC.9A.E5.AF.B9.E5.AD.90.E8.B4.A6.E5.8F.B7.E6.8E.88.E4.BA.88.E6.9D.83.E9.99.90).
![](https://main.qcloudimg.com/raw/71f052ed73144bee6bf6fab9be1bca97.png)
5. Click **Finish** to create the sub-account.
![](https://main.qcloudimg.com/raw/ee3bfab6657f15b8e08c05b8786ccc9e.png)

<span id="Grant permissions to the sub-account"></span>
### Step 2. Grant permissions to the sub-account
You can grant permissions to the sub-account by configuring policies for the sub-account (user) or user group in CAM.
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam).
2. Click **Policy** > **Create a Custom Policy** as shown below.
![](https://main.qcloudimg.com/raw/c21ff705edcc38a69629c07c7b327483.png)
2. Select **Create by Policy Syntax** to enter the creation page.
![](https://main.qcloudimg.com/raw/71f06c6317ecab4ddcd8dd1d2b7dc79e.png)
3. Available templates include **a blank template** and **preconfigured policy templates** associated with COS. Select a policy template for the sub-account and click **Next**.
![](https://main.qcloudimg.com/raw/f086c895e1e2408c204cdb0c90cd4021.png)
4. Enter an easy-to-remember policy name. If you select the **blank template**, you need to enter your policy syntax. For more information, see [Sample Policies](#Sample Policies). You can copy and paste the policy content into the **Edit Policy Content** input box and click **Create a Policy**.
![](https://main.qcloudimg.com/raw/880f49ec0df3199c2e301fd86b108580.png)
5. After you create a policy, associate it with the sub-account.
![](https://main.qcloudimg.com/raw/481057a2b826bf038bffa4f49817b380.png)
6. Check the desired sub-account and confirm the authorization. Then the sub-account can access the COS resources within the scope of the permissions.
![](https://main.qcloudimg.com/raw/2a4783ba4976aa7acb89347e75d1236b.png)

### Step 3. Access COS resources using the sub-account
To access COS using APIs or SDKs, you need to have the  APPID, SecretId, and SecretKey.
When you access COS resources with a sub-account, you need to use the APPID of the root account and the SecretId and SecretKey of the sub-account. You can generate a SecretId and a SecretKey for the sub-account in the CAM Console.

1. When logging in to the [CAM Console](https://console.cloud.tencent.com/cam/capi) using a sub-account, you need to switch to the corresponding root account (the developer account).
![](https://main.qcloudimg.com/raw/0470d3941e878fbb6e6ff794a2c9391d.png)
2. After logging in, click **Create a Key** to create a SecretID and a SecretKey for the sub-account. The APPID should be provided by the root account.
![11](https://main.qcloudimg.com/raw/79a7ec6f2a3f083a152b841f679edb76.png)

>!
- To access COS resources with a sub-account, you need to do so using XML APIs or SDKs based on XML API.
- To access COS resources with a sub-account, you need to use the APPID of the root account and the SecretId and SecretKey of the sub-account.

#### Example of access using XML Java SDK
Take the command line in XML Java SDK as an example. You need to enter the following parameters:
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
Below are some sample policies for typical scenarios. When configuring a custom policy, you can copy and paste the following sample policies into the **Edit Policy Content** input box and make necessary changes based on your actual configuration. For more policy syntax for common COS scenarios, see the **Business Cases** section in the [CAM product documentation](/doc/product/598).

### Configuring Read/Write Permission for a Sub-account
Configure Read/Write permission for a sub-account with the following policy:
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

### Configuring Read/Write Permission Only for Sub-accounts Using an IP Address within a Certain IP Range
In the following example, Read/Write Permission is only granted to sub-accounts which use an IP address within the IP range of `192.168.1.0/24` and `192.168.2.0/24`.
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
