You can delete a bucket using the console, APIs, tools, or SDKs.

>!A bucket cannot be recovered once deleted.

## Restrictions

- Only empty buckets can be deleted. If there are still objects or incomplete multipart uploads in a bucket, its deletion will fail. Make sure that there are no objects in the bucket before deleting it. For more information, see [Emptying a Bucket](https://intl.cloud.tencent.com/document/product/436/30926).
- Before deleting a bucket, make sure that the current identity has been granted the permission to delete it and that the correct `Bucket` and `Region` parameters are passed in.


## Directions

### Using COS console

Delete a bucket in the COS console. For more information, see [Deleting a Bucket](https://intl.cloud.tencent.com/document/product/436/30361) in Console Guide.

### Using tools

Use tools such as COSBrowser and COSCMD to delete a bucket. For more information, see [Tool Overview](https://intl.cloud.tencent.com/document/product/436/6242).

### Using REST APIs

Use the REST API to initiate a bucket deleting request. For more information, see [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) in API documentation.

### Using SDKs

Directly call the bucket deleting method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/31463)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/31464)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465)
- [SDK for .NET](https://intl.cloud.tencent.com/document/product/436/30595)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31466)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31467)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31468)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31477)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/31469)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471)
- [SDK for Mini Program](https://www.tencentcloud.com/document/product/436/31472)

