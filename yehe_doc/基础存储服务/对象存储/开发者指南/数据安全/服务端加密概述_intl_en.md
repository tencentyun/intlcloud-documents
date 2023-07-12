## Overview

Cloud Object Storage (COS) encrypts your data at the object level before data is written to disks and automatically decrypts the data when you access it. Encryption and decryption are completed on servers. Server-side encryption can effectively protect static data.

>!
>- As long as you have access permission on an object, your object accessing experience is the same regardless of whether the object is encrypted.
> - Server-side encryption encrypts only the object data but not its metadata. Server-side encrypted objects can only be accessed with a valid signature and cannot be accessed by anonymous users.
> 

## Use Cases

- **Private data storage:** For private data storage, server-side encryption can encrypt stored data to protect your privacy and automatically decrypt the data when you access it.
- **Private data transfer:** For private data transfer, COS supports deploying SSL certificates with HTTPS to implement encryption. An encryption layer will be established on the transfer linkage layer, ensuring that data will not be stolen or tampered with during transfer.

## Encryption
COS supports multiple server-side encryption methods such as SSE-COS and SSE-C. You can choose the appropriate one to encrypt data stored in COS.

### SSE-COS Encryption

SSE-COS: Server-side encryption with a key managed by COS. In this mode, COS will manage the master key and data, and users can manage and encrypt the data directly through COS. SSE-COS uses a strong AES-256 multi-factor encryption to ensure that each object is encrypted with a unique key, while regularly rotating the master key to encrypt the key itself.

>!
>- When uploading an object using the `POST` operation, you need to provide the same information in the form field instead of the `x-cos-server-side-encryption` header. For more information, see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).
>- SSE-COS encryption is not available for objects uploaded with a pre-signed URL. Instead, you need to use the COS console or HTTP request header to specify server-side encryption.

#### Using COS console
For details on how to use the COS console to perform SSE-COS encryption on objects, see [Setting Object Encryption](https://intl.cloud.tencent.com/document/product/436/30929).

#### Using RESTful APIs

>!
>- When you list objects in a bucket, all objects will be listed, regardless of whether they are encrypted.
>- When uploading an object using the POST operation, provide the same information in the form field instead of the request header. For more information, see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).

When you request the following APIs, you can apply server-side encryption by providing the `x-cos-server-side-encryption` header. For more information, see [Common Request Headers - SSE-COS](https://intl.cloud.tencent.com/document/product/436/7728).

- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)

### SSE-KMS Encryption

SSE-KMS encryption is server-side encryption using a key managed by KMS. KMS is a security management service launched by Tencent Cloud, using a third-party-certified hardware security module (HSM) to generate and protect keys. KMS allows users to easily create and manage keys, meeting their key management needs for multiple applications and services, while satisfying regulatory and compliance requirements.

When using SSE-KMS encryption for the first time, you need to [enable the KMS service](https://intl.cloud.tencent.com/pricing/kms). After the KMS service is enabled, the system will automatically create a default customer master key (CMK) for you. You can also create your own keys through the [KMS console](https://console.cloud.tencent.com/kms2), and define key policies and use methods. KMS allows users to choose their own key material from **KMS** or **external** sources. For more information, see [Create Key](https://intl.cloud.tencent.com/document/product/1030/31971) and [Import External Key](https://intl.cloud.tencent.com/document/product/1030/32795).

>!
>- SSE-KMS only encrypts the object data, not its metadata.
>- Currently, SSE-KMS only supports Beijing, Shanghai, Guangzhou, and Hong Kong (China) regions.
>- Using SSE-KMS encryption will incur an additional cost, which will be charged by KMS. For more information, see [KMS Billing Overview](https://intl.cloud.tencent.com/document/product/1030/31966).
>- Objects encrypted with SSE-KMS can only be accessed with a valid signature but not by anonymous users.

#### Using COS console

For details on how to use the COS console to perform SSE-KMS encryption on objects, see [Setting Object Encryption](https://intl.cloud.tencent.com/document/product/436/30929).

#### Using RESTful APIs

>!
>
>- When you list objects in a bucket, all objects will be listed, regardless of whether they are encrypted.
>- When uploading an object using the POST operation, please provide the same information in the form field instead of the request header. For more information, see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).

When you request the following APIs, you can apply server-side encryption by providing the `x-cos-server-side-encryption` header. For more information, see [Common Request Headers - SSE-KMS](https://intl.cloud.tencent.com/document/product/436/7728).

- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)

#### Details
If you have never used **COS console** for SSE-KMS encryption, and only used **API** for SSE-KMS encryption, you need to create a [CAM role](https://intl.cloud.tencent.com/document/product/598/19420) first:
1. Log in to the CAM Console and go to the [Roles](https://console.cloud.tencent.com/cam/role) page.
2. Click **Create Role** and select **Tencent Cloud Product Service** as the role entity.
3. Select **Cloud Object Storage** as the service supporting the role, and click **Next**. 
4. Search for the **QcloudKMSAccessForCOSRole** role policy and select it, and click **Next**.
![](https://main.qcloudimg.com/raw/b3d8ef7f3c534f33207c47b7fb7725fb.png)
5. Set the role tag keys and values and click **Next**.
6. Enter the specified role name: COS_QcsRole.
7. Click **Done** to complete the process.

### SSE-C Encryption

SSE-C encryption is server-side encryption with a user-defined key. When you upload an object, COS will use the encryption key you provide to apply AES-256 encryption to your data.

>!
>- COS does not store your encryption key. Instead, it stores the HMAC value of the encryption key with random data added, which is used to verify your request to access the object. COS cannot use the HMAC value to derive the value of the encryption key or decrypt the encrypted object. Therefore, if you lose the encryption key, the object cannot be obtained again.
>- When uploading an object using the POST operation, you need to provide the same information in the form field instead of the `x-cos-server-side-encryption-*` header. For more information, see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).
>- SSE-C can only be used via APIs but not the console.

#### Using RESTful APIs

When you request the following APIs, you can apply server-side encryption to PUT and POST requests by providing the `x-cos-server-side-encryption-*` header. For GET and HEAD requests, you need to provide the `x-cos-server-side-encryption-*` header to decrypt the specified object encrypted with SSE-C. For more information, see [Common Request Headers - SSE-C](https://intl.cloud.tencent.com/document/product/436/7728). The following operations support this header:

- [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
- [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745)
- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750)
- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)

