## Overview

COS encrypts your data at the object level before it is written to IDC disks and automatically decrypts the data when you access it. Encryption and decryption are completed on servers. Server-side encryption can effectively protect static data.

>
>- As long as you have access permission to objects, user experience is the same accessing encrypted and non-encrypted objects.
>- Server-side encryption only encrypts object data but not its metadata. Server-side encrypted objects can only be accessed with a valid signature, not by anonymous users.

## Use Cases

- **Private data storage:** For private data storage, server-side encryption can encrypt stored data to protect your privacy and automatically decrypt the data when you access it.
- **Private data transfer:** For private data transfer, COS supports deploying SSL certificates with HTTPS to implement encryption. An encryption layer will be established on the transfer linkage layer, ensuring that data will not be stolen or tampered with during transfer.

## Encryption
COS supports multiple server-side encryption methods such as SSE-COS and SSE-C. You can choose the appropriate one to encrypt data stored in COS.

### SSE-COS Encryption

SSE-COS: Server-side encryption with a key managed by COS. In this mode, COS will manage the master key and data, and users can manage and encrypt the data directly through COS. SSE-COS uses a strong AES-256 multi-factor encryption to ensure that each object is encrypted with a unique key, while regularly rotating the master key to encrypt the key itself.

>
>- When uploading an object using the `POST` operation, you need to provide the same information in the form field. instead of providing the `x-cos-server-side-encryption-*` header. For more information, see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).
>- SSE-COS encryption is not available for objects uploaded with a pre-signed URL. Instead, you need to use COS Console or HTTP request header to specify server–side encryption.

#### Using the COS Console
You can refer to [Setting Object Encryption](https://intl.cloud.tencent.com/document/product/436/30929) to learn how to encrypt objects in the console.

#### Using REST API

>
>- When you list objects in a bucket, all objects will be listed, no matter whether they are encrypted.
>- When uploading an object using the POST operation, please provide the same information in the form field, instead of providing the request header. For more information, see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).

When you request the following APIs, you can apply server-side encryption by providing the `x-cos-server-side-encryption` header. For more information, see [Common Request Headers - SSE-COS](https://intl.cloud.tencent.com/document/product/436/7728#sse-cos).

- [PUT Object](https://cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746)
- [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881)
- [POST Object](https://cloud.tencent.com/document/product/436/14690)

### SSE-COS Encryption

SSE-KMS encryption is server-side encryption using a key managed by KMS. KMS is a security management service launched by Tencent Cloud, using a third-party-certified hardware security module (HSM) to generate and protect keys. KMS allows users to easily create and manage keys, meeting their key management needs for multiple applications and services, while satisfying regulatory and compliance requirements.

When using SSE-KMS encryption for the first time, you need to [enable KMS service](https://buy.cloud.tencent.com/kms). After KMS service is enabled, the system will automatically create a default customer master key (CMK) for you. You can also create your own keys through [KMS Console](https://console.cloud.tencent.com/kms2), define key policies and use methods, KMS allows users to choose their own key material from **KMS** or **external** sources, see [Create Key](https://cloud.tencent.com/document/product/573/8875) and [Import External Key](https://cloud.tencent.com/document/product/573/38494).

>
>- SSE-KMS only encrypts the object data, not its metadata.
>- Currently, SSE-KMS only supports Beijing, Shanghai, and Guangzhou regions.
>-Using SSE-KMS encryption will incur additional cost, which will be charged by KMS, please see [KMS Billing Overview](https://cloud.tencent.com/document/product/573/34388) for details.

#### Using the COS Console

You can refer to [Setting Object Encryption](https://intl.cloud.tencent.com/document/product/436/30929) to learn how to encrypt objects in the console.

#### Using REST API

>
>
>- When you list objects in a bucket, all objects will be listed, no matter whether they are encrypted.
>- When uploading an object using the POST operation, please provide the same information in the form field, instead of providing the request header. For more information, see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).

When you request the following APIs, you can apply server-side encryption by providing the `x-cos-server-side-encryption` header. For more information, see [Common Request Headers - SSE-COS](https://intl.cloud.tencent.com/document/product/436/7728#sse-cos).

- [PUT Object](https://cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746)
- [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881)
- [POST Object](https://cloud.tencent.com/document/product/436/14690)

#### Notes
If you have never used **COS console** for SSE-KMS encryption, and only used **API** for SSE-KMS encryption, you need to create [CAM Role](https://intl.cloud.tencent.com/document/product/598/19420) first. The specific creation steps are as follows:
1. Log into the CAM Console and go to the [Roles](https://console.cloud.tencent.com/cam/role) page.
2. Click [Create Role] and select the role entity as [Tencent Cloud Product Service].
3. Select services supporting roles as [Object Storage], and then click [Next].
![](https://main.qcloudimg.com/raw/0c45c4dff7d73614a3656bbccf4cc112.png)
4. Configure the role policy, find and select [QcloudKMSCreaterFullAccess], and then click [Next].
![](https://main.qcloudimg.com/raw/b3d8ef7f3c534f33207c47b7fb7725fb.png)
5. Enter the specified role name: COS_QcsRole.
![](https://main.qcloudimg.com/raw/830a4d4f36a0307a0bee92b6fd6dd24a.png)
6. Click [Done] to complete the creation.

### SSE-C Encryption

SSE-C encryption is server-side encryption with a user-defined key. When you upload an object, COS will use the encryption key you provide to apply AES-256 encryption to your data.

>
>- COS does not store your encryption key. Instead, it stores the HMAC value of the encryption key with random data added, which is used to verify your request to access the object. COS cannot use the HMAC value to derive the value of the encryption key or decrypt the encrypted object. Therefore, if you lose the encryption key, the object cannot be obtained again.
>- When uploading an object using the `POST` operation, you need to provide the same information in the form field, instead of providing the `x-cos-server-side-encryption-*` header. For more information, see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).
>- SSE-C can only be used via APIs but not the console.

#### Using REST API

When you request the following APIs, you can apply server-side encryption to `PUT` and `POST` requests by providing the `x-cos-server-side-encryption-*` header. For `GET` and `HEAD` requests, you need to provide the `x-cos-server-side-encryption-*` header to decrypt the specified object encrypted with SSE-C. For more information, see [Common Request Headers - SSE-C](https://intl.cloud.tencent.com/document/product/436/7728#sse-c). The following operations support this header:

- [GET Object](https://cloud.tencent.com/document/product/436/7753)
- [HEAD Object](https://cloud.tencent.com/document/product/436/7745)
- [PUT Object](https://cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746)
- [Upload Part](https://cloud.tencent.com/document/product/436/7750)
- [POST Object](https://cloud.tencent.com/document/product/436/14690)
- [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881)
