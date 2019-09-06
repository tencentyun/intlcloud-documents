## Use Cases
Buckets can be deleted via the console, APIs, or SDKs.

> Only empty buckets can be deleted. If there are still objects in a bucket, its deletion will fail. Make sure that there are no objects in the bucket before deleting it.

Before deleting a bucket, make sure that the current identity has been granted the permission to delete it and that the correct Bucket and Region parameters are passed in.

## Directions

### Via the COS Console

You can delete a bucket in the COS Console. For more information, see [Deleting a Bucket](https://intl.cloud.tencent.com/document/product/436/30361) in Console Guide.

### Via REST API

You can use the REST API directly to initiate a bucket deleting request. For more information, see [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) in API documentataion.

### Via the SDK

You can directly call the bucket deleting method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/31463#.E5.88.9B.E5.BB.BA.E5.AD.98.E5.82.A8.E6.A1.B6)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/31464#.E5.88.9B.E5.BB.BA.E5.AD.98.E5.82.A8.E6.A1.B6)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465#.E5.88.9B.E5.BB.BA.E5.AD.98.E5.82.A8.E6.A1.B6)
- [SDK for C#](https://intl.cloud.tencent.com/document/product/436/30595#.E5.88.9B.E5.BB.BA.E5.AD.98.E5.82.A8.E6.A1.B6)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31466#.E5.88.9B.E5.BB.BA.E5.AD.98.E5.82.A8.E6.A1.B6)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31467#.E5.88.9B.E5.BB.BA.E5.AD.98.E5.82.A8.E6.A1.B6)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31468#.E5.88.9B.E5.BB.BA.E5.AD.98.E5.82.A8.E6.A1.B6)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31477#.E5.88.A0.E9.99.A4.E5.AD.98.E5.82.A8.E6.A1.B6)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/31469#.E5.88.9B.E5.BB.BA.E5.AD.98.E5.82.A8.E6.A1.B6)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470#.E5.88.9B.E5.BB.BA.E5.AD.98.E5.82.A8.E6.A1.B6)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471#.E5.88.9B.E5.BB.BA.E5.AD.98.E5.82.A8.E6.A1.B6)

