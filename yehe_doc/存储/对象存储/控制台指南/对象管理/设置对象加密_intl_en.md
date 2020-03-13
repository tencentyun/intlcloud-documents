## Overview

You can encrypt the objects stored in buckets on COS console to prevent data leakage. For more information on encryption, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145). The following shows you how to configure object encryption:

>
>- This operation does not support configuring encryption for objects of archive type. If encryption is needed, [restoring archived objects](https://intl.cloud.tencent.com/document/product/436/30961) first. After the restoration is complete, modify the storage type to standard or low frequency before configuring the encryption.
>- As long as you have access permissions to objects, the way you access encrypted and non-encrypted objects has no difference.
>- Server encryption only encrypts object data, not its metadata. Objects using server encryption can only be accessed with a valid signature, not by anonymous users.
>- When you list the objects in a bucket, all objects will be listed, no matter whether they are encrypted.

## Steps

1. Log into the [COS Console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List**.
3. Select the bucket to which a bucket policy will be added to enter the details page.
![](https://main.qcloudimg.com/raw/5d2fdd122fd896764e0f03fc31d7e58b.png)
4. In **File List**, click **Details** to the right of the object you want to encrypt.
![](https://main.qcloudimg.com/raw/05c7a0e867badbd56242b93f6425561d.png)
5. Scroll down to find the [Server-Side Encryption] configuration item and select the corresponding encryption method. Currently, two encryption methods are supported:
 - SSE-COS: Server-side encryption with a key managed by COS. For more information on SSE-COS encryption, see [SSE-COS Encryption](https://intl.cloud.tencent.com/document/product/436/18145)。
 - SSE-KMS: Server-side encryption with a key managed by Tencent Cloud Key Management System (KMS). You can use the default key or create a key. For more information on keys, see [Create KMS Key](https://cloud.tencent.com/document/product/573/875). For more information on SSE-KMS, see [SSE-KMS Encryption](https://intl.cloud.tencent.com/document/product/436/18145).
![](https://main.qcloudimg.com/raw/48c8b3a3d32170db7172397398c8a883.png)
5. Click **Save**.
7. If you need to configure encryption for multiple objects in batches, you can check multiple objects, and then select [Modify Encryption Method] under [More Actions].

>
>- If you use SSE-KMS encryption for the first time, you need to [enable KMS service](https://buy.cloud.tencent.com/kms).
>- Currently, SSE-KMS encryption only supports Beijing, Shanghai, and Guangzhou regions.
