## Use Cases

With lifecycle configuration, certain predefined actions can be automatically performed when a rule is applied to objects. For example:

- Transition: Transitions objects to the STANDARD_IA, INTELLIGENT_TIERING, ARCHIVE, or DEEP_ARCHIVE storage class after a specified period.
- Expiration: Deletes objects after their specified expiration time.

For more information, see [Lifecycle Overview](https://intl.cloud.tencent.com/document/product/436/17028) and [Lifecycle Configuration Elements](https://intl.cloud.tencent.com/document/product/436/17029).

## Directions

### Using COS console

Configure the lifecycle in the COS console. For more information, see [Lifecycle Management](https://intl.cloud.tencent.com/document/product/436/14605) in Console Guide.

### Using REST API

Configure and manage the lifecycle of objects in a bucket through the REST API as described in the following API documentation:

- [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280)
- [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278)
- [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284)

### Using SDKs

Directly call the lifecycle method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/36197)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/31519#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/12301)
- [SDK for .NET](https://intl.cloud.tencent.com/document/product/436/35269)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31527#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/37855)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/10199)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/35806)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/35860)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/35002)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31547)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/35851)
