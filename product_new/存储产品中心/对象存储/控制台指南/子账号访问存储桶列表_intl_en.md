## Overview

**Sub-accounts** do not have the permission to pull the bucket list by default. Therefore, if you log in to the [COS Console](https://console.cloud.tencent.com/cos5) with a sub-account, you cannot access buckets, bucket list, or statistics in Bucket List, as shown below.

You can allow a **sub-account** to access a bucket by **adding an access path** or access the bucket list by **adding the preset policy QcloudCOSGetServiceAccess (i.e., the permission to obtain the bucket list)** to it.

>  This feature is applicable to scenarios where the sub-account is logged in to the console to access the bucket.

## Adding an Access Path

Sub-accounts are not granted the preset policy QcloudCOSGetServiceAccess by default and thus do not have the permission to pull the bucket list. When granted the permissions (e.g., data Read or Write permissions) to a bucket by the root account, a sub-account can then access this bucket by **adding an access path**.

### Directions

1. Log in to the COS Console with a **sub-account**, enter the [Access Path List](https://console.cloud.tencent.com/cos5/access_path) page, and click **Add Access Path**.
![](https://main.qcloudimg.com/raw/6fbc8c24673e0e7719d0a4e907c2c15e.png)
2. In the **Add Access Path** pop-up window, select the bucket region and enter the access path, as shown below:
 - **Region**: Select the region of the bucket to be allowed for access.
 - **Access Path**: Enter the name of the bucket to be allowed for access (e.g., examplebucket-1250000000), or the path to an object in the bucket (e.g., `examplebucket-1250000000/exampleobject.txt`).
![](https://main.qcloudimg.com/raw/1fe816fae295dc4a087354d701fcd941.png)
3. After confirming that the region and the access path are correct, click **OK** to add the path to the authorized bucket or an object in it.
![](https://main.qcloudimg.com/raw/1bef930d904b582ad4629603a390b6f6.png)


## Adding a Preset Policy
A sub-account can access the bucket list by **adding the preset policy QcloudCOSGetServiceAccess (i.e., the permission to obtain the bucket list)** to it.

> - The preset policy QcloudCOSFullAccess or QcloudCOSReadOnlyAccess can also grant a sub-account access permission to the bucket list. However, due to the wide coverage of permissions granted by these two policies, **they are not recommended for security reasons**.
> - The collection of statistics in the overview requires the access permission to the bucket list. When the sub-account needs to pull statistics, please make sure that the root account has added the preset policy [QcloudCOSGetServiceAccess](https://console.cloud.tencent.com/cam/policy/detail/2158379&QcloudCOSGetServiceAccess&2) to it; otherwise, the system will prompt that the sub-account has no access permission to the statistics.

### Directions

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) with the root account and click the created sub-account.
![](https://main.qcloudimg.com/raw/3aa2c4bc879036a5d80a6712f70ce5a4.png)
2. Click **Associate Policies**, search for and add the preset policy [QcloudCOSGetServiceAccess](https://console.cloud.tencent.com/cam/policy/detail/2158379&QcloudCOSGetServiceAccess&2) (i.e., the permission to access the bucket list in COS) in the policy list, and click **OK** to associate the policy.
![](https://main.qcloudimg.com/raw/24fe0ed1f9360395dd995a77e9f30449.png)
3. You can view the added policies here. When you no longer need a policy, you can unbind it.
![](https://main.qcloudimg.com/raw/7c3a9b54e0c7fa582ae9c458135a5b16.png)
