## Use Cases

The copy operation creates a copy of a COS object of up to 5 GB in a single request. To copy an object over 5 GB, use the [multipart copy](https://intl.cloud.tencent.com/document/product/436/14118) API. With the copy operation, you can:

- Create a copy of an object.
- Rename an object by copying it and deleting the original one.
- Modify the storage class of an object. You can select the same object key as both the source and target and modify the storage class.
- Copy objects across different COS regions.
- Modify object metadata. You can select the same object key as both the source and target and modify object metadata.

In the copy operation, the metadata of the source object is inherited by default, while the creation date is subject to the creation date of the target object.

>?
>- Copy and paste is not supported for objects in the ARCHIVE storage class.
>- Objects in MAZ buckets cannot be replicated to an OAZ bucket.
>- A sub-account should be granted the `PutObject`, `GetObject`, and `GetObjectACL` permissions to copy objects.

## How to Use

### Using COS console

Copy objects in the COS console. For more information, see [Copying Objects](https://intl.cloud.tencent.com/document/product/436/33456) in Console Guide.

### Using the REST API

Use REST APIs to initiate an object copy request. For more information, see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### Using SDKs

Directly call the object copy method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/40494)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/44872)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/40171)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/44064)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/40495)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/44019)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/43865)
- [Node.js SDK ](https://intl.cloud.tencent.com/document/product/436/43874)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/45498)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/46470)
- [SDK for Weixin Mini Program](https://intl.cloud.tencent.com/document/product/436/43885)
