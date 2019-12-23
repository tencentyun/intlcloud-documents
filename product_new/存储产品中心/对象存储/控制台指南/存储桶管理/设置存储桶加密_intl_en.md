## Overview

You can set server-side encryption for a bucket in the COS Console, so that new objects uploaded to the bucket can be encrypted by default. For more information on bucket encryption, please see [Bucket Encryption Overview](https://cloud.tencent.com/document/product/436/40117).

>Currently, the supported bucket encryption method is SSE-COS encryption (i.e., server-side encryption using COS-managed encryption keys). For more information on server-side encryption, please see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).


## Directions
#### Setting encryption when creating a bucket

You can configure bucket encryption when [creating a bucket](https://intl.cloud.tencent.com/document/product/436/13309), as shown below:
![](https://main.qcloudimg.com/raw/b94132db83292e6e868a514a33cfd407.png)



#### Setting encryption for an existing bucket

If you do not set encryption when creating a bucket, you can follow the steps below to set configuration subsequently.

1. On the [Bucket List](https://console.cloud.tencent.com/cos5/bucket) page, click the name of the bucket for which to set encryption to enter the bucket configuration page.
2. Click **Basic Configuration** on the left to enter the basic configuration page of the bucket.
3. Scroll down to **Bucket Encryption**, click **Edit**, and change the current status to "Enabled".
![](https://main.qcloudimg.com/raw/b06f1f0e4e0feebffe3c4bf0d6ce3698.png)
4. Select the specified encryption method and click **Save**.
![](https://main.qcloudimg.com/raw/522b0500044a54c12e8651f59d8d5039.jpg)
