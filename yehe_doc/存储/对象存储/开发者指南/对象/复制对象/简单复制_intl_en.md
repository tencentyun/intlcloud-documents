## Overview

The replication operation creates a replica of a COS object of up to 5 GB in a single request. To replicate an object over 5 GB, you need to use the multipart upload API. With the replication operation, you can:

- Create a replica of an object.
- Rename an object by replicating it and deleting the original one.
- Modify the storage class of an object. You can select the same object key as both the source and destination and modify the storage class.
- Replicate objects across different COS regions.
- Modify object metadata. You can select the same object key as both the source and destination and modify object metadata.

In the replication operation, the metadata of the source object is inherited by default, while the creation date is subject to the replica’s creation date.

>?
>- Copy and paste are not supported for objects in the ARCHIVE storage class.
>- A sub-account should be granted with `PutObject`, `GetObject`, and `GetObjectACL` permissions to replicate objects.

## Usage

### Using COS console

You can replicate objects in the COS console. For more information, please see [Copying Objects](https://intl.cloud.tencent.com/document/product/436/33456) in Console Guide.

### Using RESTful APIs

You can directly use RESTful APIs to initiate an object replication request. For more information, please see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### Using SDKs

You can directly call the object replication method in the SDK. For more information, please see the SDK documentation for the corresponding programming language below:

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37674)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31518)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/38062)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31526)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37683)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK ](https://intl.cloud.tencent.com/document/product/436/31710)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546)
- [SDK for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/436/32457)
