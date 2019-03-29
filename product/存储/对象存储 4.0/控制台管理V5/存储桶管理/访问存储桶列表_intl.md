## Overview
Sub-accounts or collaborator accounts do not have the permission to pull bucket list data by default. Therefore, if you log in to the [COS Console](https://intl.cloud.tencent.com/login) with a sub-account, you cannot access buckets, bucket list and statistics in Bucket List (as shown below).

A sub-account can access a bucket by **adding an access path** or access buckets and bucket list by **gaining access to the bucket list (adding preset policy QcloudCOSGetServiceAccess)**.

- Example of denied access to bucket list
![](https://main.qcloudimg.com/raw/4798331dcf8325cf4d9030b30713da22.png)

- Example of denied access to statistics
![](https://main.qcloudimg.com/raw/829488230eb63c793708178db4a0ce0a.png)

## Adding an Access Path
Sub-accounts are not granted the preset policy QcloudCOSGetServiceAccess by default, and thus do not have the permission to pull bucket lists. When granted the permission to a bucket by the root account, a sub-account can then access this bucket by adding an access path. The procedure is as follows:

1. Log in to the COS Console with a sub-account, click [**Access Path List**](https://intl.cloud.tencent.com/login) on the navigation pane, and then click the **Add Access Path** button.
![](https://main.qcloudimg.com/raw/31f9c6789558742cda6480d467218b2e.png)

2. In the **Add Access Path** pop-up window, select the region of the bucket and enter the access path.
![](https://main.qcloudimg.com/raw/3ad7c9c3738764da2d76e8c1e194a9e2.png)
>**Notes:**
> 1. Access path can be a bucket, such as bucket1-1250000000.
> 2. Access path can be a path under a bucket, such as bucket1-1250000000/a/.
> 3. Make sure that the access path entered is an authorized one and that the bucket is in the region selected.

3. After confirming that the region and the access path are correct, click **OK** to add the authorized bucket.
![](https://main.qcloudimg.com/raw/b6910c523c8e6ca8f2aae26d7e7e9fad.png)

## Gaining Access to the Bucket List

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) with the root account, and click the created sub-account.
![](https://main.qcloudimg.com/raw/741793a9b2875dbcf73a5aa1d3069a80.png)

2. Click **Associate Policy**, select the preset policy [QcloudCOSGetServiceAccess](https://intl.cloud.tencent.com/login) in the policy list (the permission of the policy is the access to COS bucket list), and click **OK** to complete authorization configuration.
![](https://main.qcloudimg.com/raw/f8e244ba70db795c17d7306ea21efbb8.png)
>**Notes:**
> 1. Sub-accounts can also gain access to bucket lists if granted the preset policy QcloudCOSFullAccess or QcloudCOSReadOnlyAccess by the root account. However, due to the wide scope of permission granted by these two policies, **it is not recommended to use them for security reasons**.
> 2. Access to statistics: Access to statistics depends on the access to bucket lists. When a sub-account needs to pull up statistics, make sure the root account added the preset policy  for the sub-account already. Otherwise you will be notified that you don’t have access to statistics.

