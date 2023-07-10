To store objects in COS, you first need to create a bucket using the console, tools, APIs, or SDKs.

After creating a bucket, you can upload objects to it and configure other features for it, such as [setting up a static website](https://intl.cloud.tencent.com/document/product/436/14984), [setting bucket tags](https://intl.cloud.tencent.com/document/product/436/30928), and [setting bucket encryption](https://intl.cloud.tencent.com/document/product/436/33455). For more configuration instructions, see [Console Overview](https://intl.cloud.tencent.com/document/product/436/11365).


## Restrictions

1. One root account can create up to 200 buckets.
2. Once a bucket is created successfully, its name and region cannot be modified.
3. Bucket names under the same root account must be unique and cannot be changed.
4. A bucket name can contain letters, digits, and hyphens (-). The number of characters a bucket name is allowed to contain is limited by the length of the **[region abbreviation](https://intl.cloud.tencent.com/document/product/436/6224)** and **APPID**. The combined domain name can be up to 60 characters. For example, the domain name `123456789012345678901-1250000000.cos.ap-beijing.myqcloud.com` contains 60 characters.
5. A bucket name cannot start or end with "-".


## Directions

### Using COS console

Create a bucket in the COS console. For more information, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

### Using tools

Use tools such as COSBrowser and COSCMD to create a bucket. For more information, see [Tool Overview](https://intl.cloud.tencent.com/document/product/436/6242).

### Using REST APIs

Use the REST API to initiate a bucket creating request. For more information, see [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738).

### Using SDKs

Directly call the bucket creating method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31463)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31464)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30595)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31467)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31469)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471)
- [SDK for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/436/30609)

