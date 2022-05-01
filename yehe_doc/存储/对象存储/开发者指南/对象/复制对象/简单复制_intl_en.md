## Overview

The copy operation creates a copy of a COS object of up to 5 GB in a single request. To copy an object over 5 GB, use the multipart upload API. With the copy operation, you can:

- Create a copy of an object.
- Rename an object by copying it and deleting the original one.
- Modify the storage class of an object. You can select the same object key as both the source and target and modify the storage class.
- Copy objects across different COS regions.
- Modify object metadata. You can select the same object key as both the source and target and modify object metadata.

In the copy operation, the metadata of the source object is inherited by default, while the creation date is subject to the replica’s creation date.

>?
>- Copy and paste are not supported for objects in the ARCHIVE storage class.
>- A sub-account should be granted the `PutObject`, `GetObject`, and `GetObjectACL` permissions to copy objects.

## Directions

### Using COS console

Copy objects in the COS console. For more information, see [Copying Objects](https://intl.cloud.tencent.com/document/product/436/33456) in Console Guide.

### Using REST APIs

Use REST APIs to initiate an object copy request. For more information, see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### Using SDKs

Directly call the object copy method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

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
