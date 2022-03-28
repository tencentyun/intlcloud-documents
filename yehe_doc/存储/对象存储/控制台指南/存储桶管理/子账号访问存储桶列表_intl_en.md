## Overview

**Sub-accounts** have no permissions to pull a bucket list by default. Therefore, if you log in to the [COS console](https://console.cloud.tencent.com/cos5) with a sub-account, you cannot access overview data, bucket list, or any other administration items that require permissions.

**Sub-accounts** can access a bucket list using the following two methods:
- **Adding an access path**: this method applies to scenarios where a sub-account has permissions to operate on objects but no permissions to access a bucket list. The access path can be a **Bucket** or a **Path under the bucket**. Please make sure the added path is authorized.
- **Adding a preset policy**: you can add a preset policy QcloudCOSGetServiceAccess with your root account for a sub-account to access a bucket list. This method also allows you to check the statistics overview in the console.

>This feature is applicable to scenarios where a sub-account accesses a bucket list using the console.



## Adding an Access Path

Sub-accounts are not granted the preset policy QcloudCOSGetServiceAccess by default and thus do not have the permission to pull the bucket list. When granted the permissions (e.g., Read or Write) to a bucket by the root account, a sub-account can then access this bucket by **adding an access path**.

#### Prerequisites
The sub-account has been granted user permissions on a bucket by the root account. For more information, see [Set Access Permission](https://intl.cloud.tencent.com/document/product/436/13315).

#### Directions

1. Log in to the COS console with a **sub-account**, enter the [Access Path List](https://console.cloud.tencent.com/cos5/access_path) page, and click **Add Access Path**.
![](https://main.qcloudimg.com/raw/6fbc8c24673e0e7719d0a4e907c2c15e.png)
2. In the **Add Access Path** pop-up window, select the bucket region and enter the access path, as shown below:
 - **Region**: select the region of the bucket to be allowed for access.
 - **Access Path**: enter the name of the bucket to be allowed for access (e.g., examplebucket-1250000000) or the path to an object in the bucket (e.g., `examplebucket-1250000000/exampleobject.txt`).
![](https://main.qcloudimg.com/raw/1fe816fae295dc4a087354d701fcd941.png)
3. After confirming that the region and the access path are correct, click **OK** to add the path to the authorized bucket or an object in it.
![](https://main.qcloudimg.com/raw/1bef930d904b582ad4629603a390b6f6.png)
4. Click **Objects** on the right, and you can see the object(s) to which the sub-account has been granted access.


## Adding a Preset Policy
A sub-account can access the bucket list by **adding the preset policy QcloudCOSGetServiceAccess (i.e., the permission to obtain the bucket list)** to it.

>
> - The preset policy QcloudCOSFullAccess or QcloudCOSReadOnlyAccess can also grant a sub-account access permission to the bucket list. However, due to the wide coverage of permissions granted by these two policies, **they are not recommended for security reasons**.
> - The collection of statistics in the overview requires the access permission to the bucket list. When the sub-account needs to pull statistics, please make sure that the root account has added the preset policy [QcloudCOSGetServiceAccess](https://console.cloud.tencent.com/cam/policy/detail/2158379&QcloudCOSGetServiceAccess&2) to it; otherwise, the system will prompt that the sub-account has no access permission to the statistics.



1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) with the root account to enter the user list page.
2. Locate the sub-account to which you want to add a policy, and click **Grant Permission** on the right to enter the Associate Policies page.
![](https://main.qcloudimg.com/raw/bd701b29b255102c37ca17ca5974099a.png)
3. Search for and add the preset policy [QcloudCOSGetServiceAccess](https://console.cloud.tencent.com/cam/policy/detail/2158379&QcloudCOSGetServiceAccess&2) (i.e., the permission to access the bucket list in COS) in the policy list. No search result will be displayed if the policy has been added.
![](https://main.qcloudimg.com/raw/24fe0ed1f9360395dd995a77e9f30449.png)
4. Click **OK**.
5. Click the sub-account name to enter its details page where you view the added policies. When you no longer need a policy, you can unbind it.
![](https://main.qcloudimg.com/raw/7c3a9b54e0c7fa582ae9c458135a5b16.png)
>Now, you have successfully added a preset policy for the sub-account through the root account. Log in to the COS console with the sub-account, and you can check the bucket list and statistics overview.
