## Overview

You can encrypt the objects stored in buckets in the COS Console to prevent data leakage. For more information about encryption, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145). The following section will guide you through how to encrypt objects.

>
> - COS currently supports SSE-COS and SSE-KMS for encryption.
> - Server-side encryption is currently only available in Beijing, Shanghai, and Guangzhou regions.
> - The experience accessing an encrypted object is the same as that accessing an unencrypted one, provided that you already have access to it.
> - Server-side encryption encrypts only the data but not the metadata of the object. Server-side encrypted objects can only be accessed with a valid signature but not by anonymous users.
> - When you try to list the objects in a bucket, all objects will be listed, no matter whether they are encrypted.

## Steps

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List**.
3. Select the bucket to which to add a bucket policy and enter it.
![](https://main.qcloudimg.com/raw/5d2fdd122fd896764e0f03fc31d7e58b.png)
4. Click **File List** and click **Details** to the right of the object you want to encrypt.
![](https://main.qcloudimg.com/raw/50b6a416a92e185f14267c2dd7357995.png)
5. In the **Server-side Encryption** configuration item, select SSE-COS and click **Save** to encrypt the object.
![](https://main.qcloudimg.com/raw/0199d7c178c6125da84d0203f279484e.png)

