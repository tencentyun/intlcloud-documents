To store objects in COS, you first need to create a bucket through the console, tools, APIs, or SDKs.

After creating a bucket, you can upload objects to it and configure other features for it, such as [setting up a static website](https://intl.cloud.tencent.com/document/product/436/14984), [setting bucket tags](https://intl.cloud.tencent.com/document/product/436/30928), and [setting bucket encryption](https://intl.cloud.tencent.com/document/product/436/33455). For more configuration guidelines, please see [Console Overview](https://intl.cloud.tencent.com/document/product/436/11365).


## Use Limits

1. One root account can create up to 200 buckets.
2. Once a bucket is created successfully, its name and region cannot be modified.
3. Bucket names must be unique under the same root account and cannot be changed.
4. A bucket name can contain 1-50 characters. Only lowercase letters (a-z), digits (0-9), and hyphens (-) are allowed.
5. A bucket name cannot start or end with "-".


## Directions

### Using COS Console

You can create a bucket in the COS console. For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

### Using tools

You can use tools such as COSBrowser and COSCMD to create buckets. For more information, please see [Tool Overview](https://intl.cloud.tencent.com/document/product/436/6242).

### Using REST APIs

You can use the REST API directly to initiate a bucket creating request. For more information, please see [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738).

### Using SDKs

You can directly call the bucket creating method in the SDK. For more information, please see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/31463)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/31464)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465)
- [SDK for .NET](https://intl.cloud.tencent.com/document/product/436/30595)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31466)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31467)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31468)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/31469)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471)
- [SDK for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/436/30609)

