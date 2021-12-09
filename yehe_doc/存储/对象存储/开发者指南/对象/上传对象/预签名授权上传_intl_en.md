## Use Cases

All buckets and objects are private by default. If you want any third party to be able to upload an object to your bucket, but you don't want them to use CAM accounts or temporary keys, signatures can be provided by pre-signed URLs for temporary upload operations. Anyone who receives a valid pre-signed URL can upload an object.

When creating a pre-signed URL, you can include an object key in your signature so that the object can only be uploaded to the specified object key. Besides, the validity period of pre-signed URLs can be provided in SDKs to ensure that expired URLs will not be used by any unauthorized party.

>?
> - You are advised to use a temporary key to generate a pre-signed URL for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 

## Directions

### Using SDKs

You can call the pre-signed URL method in the SDK directly. For more information, please see the SDK documentation for the corresponding programming language below:

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37680)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31520)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31524)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/38068)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31528)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37690)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31536)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31540)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/32455)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31544)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31548)
- [Mini Program SDK](https://intl.cloud.tencent.com/document/product/436/31711)


