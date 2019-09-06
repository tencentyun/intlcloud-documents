## Use Cases

All buckets and objects are private by default. If you want a third party to be able to upload an object to your bucket but don't want them to use CAM account or temporary keys, signatures can be provided by pre-signed URLs for temporary upload operations. Anyone who receives a valid pre-signed URL can upload an object.

When creating a pre-signed URL, you can include an object key in your signature so that the object can only be uploaded to the specified object key. Besides, the validity period of pre-signed URLs can be provided in SDKs to ensure that expired URLs will not be used by any unauthorized party.

## Directions

### Via the SDK

You can call the pre-signed URL method in the SDK directly. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/31463)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/35560)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465)
- [SDK for C#](https://intl.cloud.tencent.com/document/product/436/30595)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31466)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31467)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31468)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31477)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/31469)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471)
