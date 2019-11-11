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

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/12159)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/12296)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/12301)
- [SDK for .Net](https://intl.cloud.tencent.com/document/product/436/30594)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/30601)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/11280)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/10199)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/11459)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/8629)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/12266)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/12269)
