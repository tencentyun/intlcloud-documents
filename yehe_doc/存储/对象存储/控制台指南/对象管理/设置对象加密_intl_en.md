### Introduction

You can encrypt the objects stored in buckets on the COS console to prevent data leakage. For more information on encryption, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145). The following information outlines how to configure object encryption:

>!
>- This operation does not support configuring encryption for archived objects. If encryption is needed, please first refer to the information on [restoring an archived object](https://intl.cloud.tencent.com/document/product/436/30961). After the restoration is complete, modify the storage type to standard or low frequency before configuring the encryption.
>- As long as you have access permission for an object, whether the object has been encrypted has no effect on your accessing said object.
> - Server-side encryption encrypts only the object data but not its metadata. Server-side encrypted objects can only be accessed with a valid signature and cannot be accessed by anonymous users.
> - When you list the objects in a bucket, all objects, regardless of encryption, will be listed.

### Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List**.
3. Select the bucket for which you want to add a bucket policy to enter the bucket details page.
![](https://main.qcloudimg.com/raw/5d2fdd122fd896764e0f03fc31d7e58b.png)
4. Click **File List**, locate the object for which you want to configure encryption, and click **Details** in the Actions column on the right.
![](https://main.qcloudimg.com/raw/05c7a0e867badbd56242b93f6425561d.png)
5. Scroll down to find the [Server-Side Encryption] configuration item and select the corresponding encryption method. Currently, the following two encryption methods are supported:
 - SSE-COS: Server-side encryption via key managed by COS. For more information on SSE-COS encryption, see [SSE-COS Encryption](https://intl.cloud.tencent.com/document/product/436/18145)。
 - SSE-KMS: Server-side encryption via key managed by the Tencent Cloud Key Management System (KMS). You can use the default key or create a key. For more information on keys, see [Creating a Key](https://intl.cloud.tencent.com/document/product/1030/31971). For more information on SSE-KMS, see [SSE-KMS Encryption](https://intl.cloud.tencent.com/document/product/436/18145).
![](https://main.qcloudimg.com/raw/48c8b3a3d32170db7172397398c8a883.png)
6. Click **Save**.
7. If you need to configure batch encryption for multiple objects, you can check multiple objects from the file list and then select [Modify Encryption Method] under [More Actions].

>!
>- If you’re using SSE-KMS encryption for the first time, you need to [enable KMS services](https://buy.cloud.tencent.com/kms).
>- Currently, SSE-KMS encryption only supports the Beijing, Shanghai, and Guangzhou regions.
