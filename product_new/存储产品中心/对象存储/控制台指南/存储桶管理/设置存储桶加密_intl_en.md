## Overview

You can set server-side encryption for a bucket in the COS console, so that new objects uploaded to the bucket can be encrypted by default. For more information on bucket encryption, see [Bucket Encryption Overview](https://intl.cloud.tencent.com/document/product/436/33457).

>?Currently, the supported bucket encryption method is SSE-COS encryption (i.e., server-side encryption using COS-managed encryption keys). For more information on server-side encryption, see [Server-Side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).


## Directions

#### Setting encryption when creating a bucket

You can configure bucket encryption when [creating a bucket](https://intl.cloud.tencent.com/document/product/436/13309), as shown below:
![](https://main.qcloudimg.com/raw/3529ae1c392f524209cf899931aa1fef.png)



#### Setting encryption for an existing bucket

If you did not set encryption when creating a bucket, follow the steps below to set it subsequently.

1. On the [Bucket List](https://console.cloud.tencent.com/cos5/bucket) page, click the name of the bucket for which to set encryption to enter the bucket configuration page.
2. Select **Security Management** > **Server-Side Encryption** on the left sidebar, click **Edit**, and toggle **Status** on.
![](https://main.qcloudimg.com/raw/e2863ba89860f15464870ac198b5335f.png)
3. Select the specified encryption method and click **Save**.
![](https://main.qcloudimg.com/raw/524717e180e357eb74fa8be0b42a51a3.png)
