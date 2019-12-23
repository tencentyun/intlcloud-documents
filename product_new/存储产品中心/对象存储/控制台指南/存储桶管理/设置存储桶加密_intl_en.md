## Overview

You can set server-side encryption for a bucket in the COS Console, so that new objects uploaded to the bucket can be encrypted by default. <!--For more information on bucket encryption, please see [Bucket Encryption Overview]().-->

>Currently, the supported bucket encryption method is SSE-COS encryption (i.e., server-side encryption using COS-managed encryption keys). For more information on server-side encryption, please see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).


## Directions
#### Setting encryption when creating a bucket

You can configure bucket encryption when [creating a bucket](https://intl.cloud.tencent.com/document/product/436/13309), as shown below:
![](https://main.qcloudimg.com/raw/cc4f781f6ffa98b3786e52cf84d5c8d4.png)



#### Setting encryption for an existing bucket

If you do not set encryption when creating a bucket, you can follow the steps below to set configuration subsequently.

1. On the [Bucket List](https://console.cloud.tencent.com/cos5/bucket) page, click the name of the bucket for which to set encryption to enter the bucket configuration page.
2. Click **Basic Configuration** on the left to enter the basic configuration page of the bucket.
3. Scroll down to **Bucket Encryption**, click **Edit**, and change the current status to "Enabled".
![](https://main.qcloudimg.com/raw/e2863ba89860f15464870ac198b5335f.png)
4. Select the specified encryption method and click **Save**.
![](https://main.qcloudimg.com/raw/524717e180e357eb74fa8be0b42a51a3.png)
