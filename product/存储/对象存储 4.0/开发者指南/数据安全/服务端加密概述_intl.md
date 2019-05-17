## Overview

Tencent Cloud COS encrypts your data at the object level before data is written to IDC disks, and automatically decrypts it when you access data. The encryption and decryption operations are completed in servers, and the encryption feature can effectively protect your static data.

>!
> - Server-side encryption only supports Beijing, Shanghai, and Guangzhou.
> - As long as you have access permissions to objects, there is no difference in the way you access encrypted or unencrypted objects.
> - Server-side encryption encrypts only the object data. Any object metadata is not encrypted. Objects protected by the server-side encryption must be accessed with a valid signature and cannot be accessed by anonymous users.

## Use Cases

-  **Private data storage scenarios:** For private data storage, server-side encryption can encrypt the stored data to protect user privacy, and decrypt it automatically when you access it.
-  **Private data transmission scenarios:** For private data transmission, COS supports deploying SSL certificate with HTTPS to implement encryption, and establishing an encryption layer on the transmission linkage layer to ensure that data will not be stolen and tampered during transmission.

## Support for Server-side Encryption

### Supported encryption methods

Tencent Cloud COS supports server-side encryption (SSE-COS) with managed keys. SSE-COS adopts strong multi-factor encryption to ensure each object is encrypted with a unique key. It uses 256-bit Advanced Encryption Standard (AES-256) to encrypt data, and encrypts the key itself with a master key that it regularly rotates.

### Supported APIs

>!When you list objects in a bucket, all objects will be returned in the list, regardless of whether the object is encrypted.

Tencent Cloud COS provides REST API related to server-side encryption. When creating objects, you can request server-side encryption by specifying the x-cos-server-side-encryption header. The x-cos-server-side-encryption header is required when you perform the following upload and copy operations.

The following operations support these request headers:

-  PUT operation: When uploading an object using the PUT API, you can specify these request headers. See [PUT Object](https://cloud.tencent.com/document/product/436/7749).
-  Initiate Multipart Upload: When uploading large objects using the multipart upload API, you can specify these headers in the initiate request. See [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746).
-  POST operation: This operation can use form fields to upload objects. HTTP header parameters are no longer in use. See [POST Object](https://cloud.tencent.com/document/product/436/14690).
-  Copy operation: When you copy an object, you have both a source object and a target object. See [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881).

