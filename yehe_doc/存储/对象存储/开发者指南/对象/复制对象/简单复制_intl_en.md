## Use Cases

The copy operation creates a copy of an object that is already stored in COS. You can create a copy of your object up to 5 GB in a single operation. To copy an object over 5 GB, you must use the multipart upload API. With the copy operation, you can:

- Create a copy of an object.
- Rename the object by copying it and deleting the original one.
- Modify the storage class of the object. In the copy operation, you can select the same object key as both the source and destination and modify the storage class.
- Copy objects across different COS regions.
- Modify object metadata. In the copy operation, you can select the same object key as both the source and destination and modify object metadata.

In the copy operation, the metadata of the original object is inherited by default, but the creation date is subject to the new object.

>? 
>- Copy and paste is not supported for objects in the archive storage class.
>- For a sub-account to replicate an object, it should have permission to PutObject, GetObject, and GetObjectACL.

## Directions

### Configuring via the COS Console

You can copy an object in the COS Console. For more information, see [Copying Objects](https://intl.cloud.tencent.com/document/product/436/33456) in Console Guide.

### Configuring via REST API

You can use the REST API directly to initiate an object copying request. For more information, see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### Via the SDK

You can directly call the object copying method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/31514)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/31518)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30596)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31526)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31530)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31534)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK ](https://intl.cloud.tencent.com/document/product/436/31710)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31542)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31546)
- [SDK for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/436/32457)
