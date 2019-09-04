## Use Cases

With lifecycle configuration, certain predefined actions can be automatically performed when a rule is applied to objects. For example:

- Transition: transition objects to STANDARD_IA storage or ARCHIVE storage after a specified time of period.
- Expiration: automatically delete objects after their specified expiration time.

For more information, see [Lifecycle Overview](https://intl.cloud.tencent.com/document/product/436/17028) and [Elements of Lifecycle Configuration](https://intl.cloud.tencent.com/document/product/436/17029).

## Directions

### Via the COS Console

You can configure the lifecycle in the COS Console. For more information, see [Lifecycle Management](https://intl.cloud.tencent.com/document/product/436/14605) in Console Guide.

### Via REST API

You can configure and manage the lifecycle of objects in a bucket through the REST API as described in the following API documentations:

- [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280)
- [GET Buket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278)
- [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284)

### Via the SDK

You can directly call the lifecycle method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/34537#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/35559#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/35162#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for C#](https://intl.cloud.tencent.com/document/product/436/32872#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/35058#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/34108#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/35216#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/35650#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/36120#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/34283#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/35152#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
