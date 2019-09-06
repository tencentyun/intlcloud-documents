## Overview

COS encrypts your data at the object level before it is written to IDC disks and automatically decrypts it when you access it. The encryption and decryption operations are completed on servers. Server-side encryption can effectively protect your static data.

> - Server-side encryption is currently only available in Beijing, Shanghai, and Guangzhou regions.
> - As long as you have access permission to objects, there is no difference in the way you access encrypted or unencrypted objects.
> - Server-side encryption encrypts only the object data. No object metadata is encrypted. Objects protected by server-side encryption must be accessed with a valid signature and cannot be accessed by anonymous users.

## Use Cases

- **Private data storage:** For private data storage, server-side encryption can encrypt the stored data to protect your privacy and decrypt it automatically when you access it.
- **Private data transfer:** For private data transfer, COS supports deploying SSL certificates with HTTPS to implement encryption. The establishment of an encryption layer on the transfer linkage layer ensures that data will not be stolen or tampered with during transfer.

## Encryption
COS supports multiple server-side encryption methods such as SSE-COS and SSE-C. You can choose the most appropriate one to encrypt your data stored in COS.

### SSE-COS Encryption

SSE-COS: Server-side encryption with a key managed by COS. In this mode, COS is responsible for managing the master key and data, and your data can be managed and encrypted directly through COS. SSE-COS uses AES-256 multi-factor strong encryption to ensure that each object is encrypted with a unique key, while regularly rotating the master key to encrypt the key itself.

>- When uploading an object using the `POST` operation, you need to provide the same information in the form field instead of the `x-cos-server-side-encryption` header. For more information, see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).
>- SSE-COS encryption is not available for objects uploaded with a pre-signed URL. Instead, server-side encryption can be specified only in the COS Console or through the HTTP request header.

#### Via the COS Console
You can refer to [Setting Object Encryption](https://intl.cloud.tencent.com/document/product/436/30929) to learn how to encrypt objects in the console.

#### Via REST API

>- When you try to list the objects in a bucket, all objects will be listed, no matter whether they are encrypted.
>- When uploading an object using the POST operation, please provide the same information in the form field instead of the request header. For more information, see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).

When you request the following APIs, you can apply the server-side encryption by providing the `x-cos-server-side-encryption` header. For more information, see [Common Request Headers - SSE-COS](https://intl.cloud.tencent.com/document/product/436/7728#sse-cos). The following operations support this header:

- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)

### SSE-C Encryption

SSE-C: Server-side encryption with a user-defined key. When you upload an object, COS will use the encryption key you provide to apply AES-256 encryption to your data.

>- COS does not store your encryption key; instead, it stores the HMAC value of the encryption key with random data added, which is used to verify your request to access the object. COS cannot use the HMAC value to derive the value of the encryption key or decrypt the encrypted object. Therefore, if you lose the encryption key, the object cannot be decrypted again.
>- When uploading an object using the `POST` operation, you need to provide the same information in the form field instead of the `x-cos-server-side-encryption-*` header. For more information, see [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).
>- SSE-C can only be used via APIs but not the console.

#### Via REST API

When you request the following APIs, you can apply server-side encryption to `PUT` and `POST` requests by providing the `x-cos-server-side-encryption-*` header. For `GET` and `HEAD` requests, you need to provide the `x-cos-server-side-encryption-*` header to decrypt the specified object encrypted with SSE-C. For more information, see [Common Request Headers - SSE-C](https://intl.cloud.tencent.com/document/product/436/7728#sse-c). The following operations support this header:

- [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
- [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745)
- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750)
- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
