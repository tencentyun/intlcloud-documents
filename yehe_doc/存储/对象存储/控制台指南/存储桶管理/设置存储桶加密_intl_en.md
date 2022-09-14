## Overview

You can set server-side encryption for a bucket in the COS console, so that new objects uploaded to the bucket can be encrypted by default. For more information on bucket encryption, see [Bucket Encryption Overview](https://intl.cloud.tencent.com/document/product/436/33457).

>? Currently, the supported bucket encryption method is SSE-COS encryption (i.e., server-side encryption using COS-managed encryption keys). For more information on server-side encryption, see [Server-Side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).
>


## Directions

#### Setting encryption during bucket creation

You can configure bucket encryption when [creating a bucket](https://intl.cloud.tencent.com/document/product/436/13309).
![](https://main.qcloudimg.com/raw/cc4f781f6ffa98b3786e52cf84d5c8d4.png)


#### Setting encryption for existing bucket

If you did not set encryption when creating a bucket, follow the steps below to set it subsequently.

1. On the [Bucket List](https://console.cloud.tencent.com/cos5/bucket) page, click the name of the target bucket to enter the bucket configuration page.
2. Click **Security Management > Server-Side Encryption** on the left sidebar.
3. In the **Server-Server-Side Encryption** configuration item, toggle the feature on.
![](https://main.qcloudimg.com/raw/e2863ba89860f15464870ac198b5335f.png)
4. Select the specified encryption method and click **Save**.
![](https://main.qcloudimg.com/raw/524717e180e357eb74fa8be0b42a51a3.png)

