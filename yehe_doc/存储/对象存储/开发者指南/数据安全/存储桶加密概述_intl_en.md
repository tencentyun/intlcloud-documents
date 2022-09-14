## Overview

By setting bucket encryption, you can encrypt all new objects uploaded to a bucket with the specified encryption method by default.

Currently, SSE-COS encryption is supported, i.e., server-side encryption that uses COS to manage keys.

For more information on server-side encryption, see [Server-Side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

## Directions

#### Using the COS console

You can set bucket encryption in the COS console as instructed in [Setting Bucket Encryption](https://intl.cloud.tencent.com/document/product/436/33455).

#### Using RESTful APIs
You can configure bucket encryption by using the following APIs:

- [PUT Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33459) 
- [GET Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33460) 
- [DELETE Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33461) 

## Notes

#### Uploading object to encrypted bucket

For buckets requiring encryption, note the following:

- Configuring encryption for a bucket will not lead to encryption operations on objects that already exist in it.
- After encryption is configured for a bucket, for objects uploaded to the bucket:
  - If your PUT request does not contain encryption information, the uploaded objects will be encrypted based on the encryption configuration of the bucket.
  - If your PUT request contains encryption information, the uploaded objects will be encrypted based on the contained encryption information.
- After encryption is configured for a bucket, for inventory reports delivered to the bucket:
  - If encryption is not configured for the inventory, the delivered reports will be encrypted based on the encryption configuration of the bucket.
  - If encryption is configured for the inventory, the delivered reports will be encrypted based on the encryption configuration of the inventory.
- After encryption is configured for a bucket, the data retrieved from the origin to the bucket will be encrypted based on the encryption configuration of the bucket by default.

#### Encrypting a bucket that has a cross-region replication rule configured

For the destination bucket that has a cross-region replication rule configured, if you configure encryption for it, note the following:

- If the objects in the source bucket are not encrypted, the object copies in the destination bucket will be encrypted by default.
- If the objects in the source bucket are encrypted, the object copies in the destination bucket will inherit the encryption from the source bucket, and the bucket encryption settings will not be applied.


