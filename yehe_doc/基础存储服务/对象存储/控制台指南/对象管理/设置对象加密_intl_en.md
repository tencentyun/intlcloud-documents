## Overview

You can encrypt the objects stored in buckets using the COS console to prevent data disclosure. For more information on encryption, see [Server-Side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145). The following shows you how to configure object encryption:

>!
>- This operation does not support configuring encryption for objects in the ARCHIVE storage class. If encryption is required, [restore archived objects](https://intl.cloud.tencent.com/document/product/436/30961) first. After the restoration is complete, change the storage class to STANDARD or STANDARD_IA  before configuring the encryption.
>- As long as you have access permission on an object, the object accessing experience is the same regardless of whether the object is encrypted.
> - Server-side encryption encrypts only the object data but not its metadata. Server-side encrypted objects can only be accessed with a valid signature and cannot be accessed by anonymous users.
> - When you list the objects in a bucket, all objects will be listed, regardless of whether they are encrypted.
> 

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left sidebar.
5. Find the target object and click **Details** in the **Operation** column on the right.
6. Select the encryption mode in the **Server-Side Encryption** column and click **Submit**.
The following two encryption methods are currently supported:
 - SSE-COS: Server-side encryption with a key managed by COS. For more information on SSE-COS encryption, see [SSE-COS Encryption](https://intl.cloud.tencent.com/document/product/436/18145#sse-cos-.E5.8A.A0.E5.AF.86)。
 - SSE-KMS: Server-side encryption with a key managed by Tencent Cloud Key Management System (KMS). You can use the default key or create a key. For more information about keys, see [Creating a Key](https://intl.cloud.tencent.com/document/product/1030/31971). For more information about SSE-KMS, see the **SSE-KMS Encryption** section in [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145#sse-kms-.E5.8A.A0.E5.AF.86).
>?
>- If you use SSE-KMS encryption for the first time, you need to [enable the KMS service](https://intl.cloud.tencent.com/pricing/kms).
>- Currently, SSE-KMS encryption is available only in the Beijing, Shanghai, and Guangzhou regions.
>- To batch encrypt multiple objects, select multiple objects and click **More Actions** > **Modify Encryption Method** at the top.

