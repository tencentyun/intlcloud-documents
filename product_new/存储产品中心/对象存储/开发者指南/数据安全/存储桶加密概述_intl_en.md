## Overview

Once a bucket is configured for encryption, all objects uploaded to the bucket thereafter will be encrypted by default with the specified encryption method.

Currently supported encryption methods include:

- SSE-COS encryption: server-side encryption using COS-managed encryption keys

For more information on server-side encryption, please see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

## Directions

#### Via the COS Console

You can set bucket encryption in the COS Console. For more information, please see [Setting Bucket Encryption](https://cloud.tencent.com/document/product/436/40116) in Console Guide.

#### Via REST API
You can configure bucket encryption using the following APIs:

- [PUT Bucket encryption](https://cloud.tencent.com/document/product/436/40136) 
- [GET Bucket encryption](https://cloud.tencent.com/document/product/436/40137) 
- [DELETE Bucket encryption](https://cloud.tencent.com/document/product/436/40138) 

## Notes

#### Uploading objects to an encrypted bucket

For buckets requiring encryption, note the following:

- Configuring encryption for a bucket will not lead to encryption operations on objects that already exist in it.
- After encryption is configured for a bucket, for objects uploaded to the bucket:
  - If your PUT request does not contain encryption information, the uploaded objects will be encrypted with the encryption configuration of the bucket.
  - If your PUT request contains encryption information, the uploaded objects will be encrypted with the contained encryption information.
- After encryption is configured for a bucket, for inventory reports delivered to the bucket:
  - If encryption is not configured for the inventory, the delivered reports will be encrypted with the encryption configuration of the bucket.
  - If encryption is configured for the inventory, the delivered reports will be encrypted with the encryption configuration of the inventory.
- After encryption is configured for the bucket, the data pulled back to the bucket will be encrypted with the encryption configuration of the bucket by default.

#### Encrypting buckets that have cross-region replication rules configured

For the destination bucket that has a cross-region replication rule configured, if you configure encryption for it, note the following:

- If the objects in the source bucket are not encrypted, the object copies in the destination bucket will be encrypted by default.
- If the objects in the source bucket are encrypted, the object copies in the destination bucket will inherit the encryption from the source bucket, and the bucket encryption settings will not be honored.

