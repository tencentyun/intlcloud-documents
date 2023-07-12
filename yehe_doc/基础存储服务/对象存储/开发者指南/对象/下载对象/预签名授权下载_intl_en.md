## Overview

All buckets and objects are private by default. If you want any third party to be able to download an object without using CAM account or temporary keys, provide the third parties with signatures via pre-signed URLs for download operations. Anyone who receives a valid pre-signed URL can download an object.

When creating a pre-signed URL, you can include object keys in your signature to specify the objects allowed for download. Besides, the validity period of pre-signed URLs can be provided in SDKs to ensure that expired URLs will not be used by any unauthorized party.

>!
> - Accessing a CDN domain needs to follow the authentication process of CDN, in which case COS signatures cannot be used. Therefore, pre-signed URLs do not support the use of CDN domains.
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key only to uploads and downloads to avoid risks. In addition, the validity period of the generated URL must be set to the shortest period required to complete the current upload or download operation. This is because the request will be interrupted when the validity period of the specified pre-signed URL expires. In addition, the checkpoint restart is not supported, and therefore the failed request needs to be re-executed after a new URL is applied for.
> 


## Directions

### Using SDKs

Call the pre-signed URL method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37680)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31520)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31524)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/38068)
- [Flutter SDK](https://www.tencentcloud.com/document/product/436/54513)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31528)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37690)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31536)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31540)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/32455)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31544)
- [Python SDK](https://www.tencentcloud.com/document/product/436/31548)
- [React Native SDK](https://www.tencentcloud.com/document/product/436/54312)
- [Mini Program SDK](https://intl.cloud.tencent.com/document/product/436/31711)
