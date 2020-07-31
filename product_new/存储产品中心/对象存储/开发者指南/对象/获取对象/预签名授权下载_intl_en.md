## Use Cases

All buckets and objects are private by default. If you want any third party to be able to download an object without using CAM account or temporary keys, provide the third parties with signatures via pre-signed URLs for download operations. Anyone who receives a valid pre-signed URL can download an object.

When creating a pre-signed URL, you can include object keys in your signature to specify the objects allowed for download. Besides, the validity period of pre-signed URLs can be provided in SDKs to ensure that expired URLs will not be used by any unauthorized party.

## Directions

### Via the SDK

You can call the pre-signed URL method in the SDK directly. For more information, see the SDK documentations for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/31463)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31520)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465)
- [SDK for .NET](https://intl.cloud.tencent.com/document/product/436/30595)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31466)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31467)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31468)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31477)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/8629)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471)
- [Mini Program SDK](https://intl.cloud.tencent.com/document/product/436/31711)
