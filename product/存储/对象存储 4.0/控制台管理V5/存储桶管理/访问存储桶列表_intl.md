## Overview
Sub-accounts or collaborator accounts do not have the permission to pull bucket list data by default. Therefore, if you log in to the [COS Console](https://console.cloud.tencent.com/cos5) with a sub-account, you cannot access buckets, bucket list and statistics in Bucket List (as shown below).

A sub-account can access a bucket by **adding an access path** or access buckets and bucket list by **gaining access to the bucket list (adding preset policy QcloudCOSGetServiceAccess)**.

- Example of denied access to bucket list
![](https://main.qcloudimg.com/raw/a6ccdd6c2929e106811ea7b9743dbb20.png)

- Example of denied access to statistics
![](https://main.qcloudimg.com/raw/6b067cc708d48d7322ed12a4ad63d86c.png)

## Adding an Access Path
Sub-accounts are not granted the preset policy QcloudCOSGetServiceAccess by default, and thus do not have the permission to pull bucket lists. When granted the permission to a bucket by the root account, a sub-account can then access this bucket by adding an access path. The procedure is as follows:

1. Log in to the COS Console with a sub-account, click [**Access Path List**](https://console.cloud.tencent.com/cos5/access_path) on the navigation pane, and then click the **Add Access Path** button.
![](https://main.qcloudimg.com/raw/ee5c67c4144d98b0a2528be09b0a9f39.png)

2. In the **Add Access Path** pop-up window, select the region of the bucket and enter the access path.
![](https://main.qcloudimg.com/raw/12f559f9bdd69ebad4379a58db5e0065.png)
>**Notes:**
> 1. Access path can be a bucket, such as bucket1-1250000000.
> 2. Access path can be a path under a bucket, such as bucket1-1250000000/a/.
> 3. Make sure that the access path entered is an authorized one and that the bucket is in the region selected.

3. After confirming that the region and the access path are correct, click **OK** to add the authorized bucket.
![](https://main.qcloudimg.com/raw/34b812cf9b6146da99206c93c4e2b1a9.png)

## Gaining Access to the Bucket List

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) with the root account, and click the created sub-account.
![](https://main.qcloudimg.com/raw/e0c74c136565592bd9f903551f949303.png)

2. Click **Associate Policy**, select the preset policy [QcloudCOSGetServiceAccess](https://console.cloud.tencent.com/cam/policy/detail/2158379&QcloudCOSGetServiceAccess&2) in the policy list (the permission of the policy is the access to COS bucket list), and click **OK** to complete authorization configuration.
![](https://main.qcloudimg.com/raw/5f1f8666a35f1c175c45ba54024ffe1d.png)
>**Notes:**
> 1. Sub-accounts can also gain access to bucket lists if granted the preset policy QcloudCOSFullAccess or QcloudCOSReadOnlyAccess by the root account. However, due to the wide scope of permission granted by these two policies, **it is not recommended to use them for security reasons**.
> 2. Access to statistics: Access to statistics depends on the access to bucket lists. When a sub-account needs to pull up statistics, make sure the root account added the preset policy  for the sub-account already. Otherwise you will be notified that you don’t have access to statistics.

