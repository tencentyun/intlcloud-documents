## Overview

**Sub-accounts** do not have the permission to pull the bucket list by default. Therefore, if you log in to the [COS Console](https://console.cloud.tencent.com/cos5) with a sub-account, you cannot access buckets, bucket list, or statistics in Bucket List, as shown below.

**Example of denied access to bucket list:**
![](https://main.qcloudimg.com/raw/f44e5b110fd1f2ed61bb0a936078559f.png)
**Example of denied access to statistics:**
![7](https://main.qcloudimg.com/raw/5261ae1703fb712d0abccdfb89066817.png)

You can allow a **sub-account** to access a bucket by **adding an access path** or access the bucket list by **adding the preset policy QcloudCOSGetServiceAccess (i.e., the permission to obtain the bucket list)** to it.

> This feature is applicable to scenarios where the sub-account is logged in to the console to access the bucket.

## Adding an Access Path

Sub-accounts are not granted the preset policy QcloudCOSGetServiceAccess by default and thus do not have the permission to pull the bucket list. When granted the permissions (e.g., data read or write permissions) to a bucket by the root account, a sub-account can then access this bucket by **adding an access path**.

### Directions

1. Log in to the COS Console with a **sub-account**, enter the [Access Path List](https://console.cloud.tencent.com/cos5/access_path) page, and click **Add Access Path**.
![](https://main.qcloudimg.com/raw/5b43952bfa49f24088801b5ef01b3b3a.png)
2. In the **Add Access Path** pop-up window, select the bucket region and enter the access path, as shown below:
 - **Region**: Select the region of the bucket to be allowed for access.
 - **Access Path**: Enter the name of the bucket to be allowed for access (e.g., examplebucket-1250000000) or the path to an object in the bucket (e.g., `examplebucket-1250000000/exampleobject.txt`).
![](https://main.qcloudimg.com/raw/89e586af646087d1a87df5a19c3dc1a7.png)
3. After confirming that the region and the access path are correct, click **OK** to add the path to the authorized bucket or an object in it.
![](https://main.qcloudimg.com/raw/ef918f066ba2029e2520cc3e998ea946.png)


## Adding a Preset Policy
A sub-account can access the bucket list by **adding the preset policy QcloudCOSGetServiceAccess (i.e., the permission to obtain the bucket list)** to it.

> - The preset policy QcloudCOSFullAccess or QcloudCOSReadOnlyAccess can also grant a sub-account access permission to the bucket list. However, due to the wide coverage of permissions granted by these two policies, **they are not recommended for security reasons**.
> - The collection of statistics in the overview requires the access permission to the bucket list. When the sub-account needs to pull statistics, please make sure that the root account has added the preset policy [QcloudCOSGetServiceAccess](https://console.cloud.tencent.com/cam/policy/detail/2158379&QcloudCOSGetServiceAccess&2) to it; otherwise, the system will prompt that the sub-account has no access permission to the statistics.

### Directions

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) with the root account and click the created sub-account.
![](https://main.qcloudimg.com/raw/af2791b8a841865c05ecdb1ac644a8ec.png)
2. Click **Associate Policies**, search for and add the preset policy [QcloudCOSGetServiceAccess](https://console.cloud.tencent.com/cam/policy/detail/2158379&QcloudCOSGetServiceAccess&2) (i.e., the permission to access the bucket list in COS) in the policy list, and click **OK** to associate the policy.
![](https://main.qcloudimg.com/raw/3aef8fa0c9e95faf67428d38b78aca07.png)
3. You can view the added policies here. When you no longer need a policy, you can unbind it.
![](https://main.qcloudimg.com/raw/175b7a5e3d061a6aa47b7c61300af91b.png)
