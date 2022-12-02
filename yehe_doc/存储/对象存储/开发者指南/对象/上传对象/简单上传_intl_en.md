Simple upload refers to uploading objects using the `PUT Object` API. It is suitable for uploading an object smaller than 5 GB in a single request.

To upload an object larger than 5 GB, you can use:

- COS console: You can upload an object up to 512 GB. For more information, see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).
- Multipart upload with APIs or SDKs: You can upload an object up to 48.82 TB (i.e., 50,000 GB). For more information, see [Multipart Upload](https://intl.cloud.tencent.com/document/product/436/14112).
- COSCMD: You can upload an object up to 40 TB. For more information, see [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).

>?When initiating a request, if you want to specify a directory or path, you can use `/`. For example, if you need to upload `picture.png` to the `doc` directory, set the object key to `doc/picture.png`.
>

## Use Cases

Simple upload is suitable for uploading an object smaller than 5 GB.

In a high bandwidth or weak network environment, if your object is relatively large, for example, over 100 MB, we recommend you use [Multipart Upload](https://intl.cloud.tencent.com/document/product/436/14112), even if the object is smaller than 5 GB. This is because multipart upload supports uploading multiple parts concurrently, which gives full play to resources in high bandwidth environments. On the other hand, in weak network environments, the uploaded parts will not be affected by the failed ones. Therefore, failed parts can be re-uploaded with a simple retry, improving the overall upload success rate. For more information about uploading objects with a client in a weak network environment, see [Multipart Upload Resumption in a Weak Network Environment](https://intl.cloud.tencent.com/document/product/436/30932).


## Directions

### Using REST APIs

Use REST APIs to initiate a simple upload request. For more information, see [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749).

### Using SDKs
Directly call the simple upload method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:
- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37674)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31518)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/38062)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31526)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37683)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/43881)


