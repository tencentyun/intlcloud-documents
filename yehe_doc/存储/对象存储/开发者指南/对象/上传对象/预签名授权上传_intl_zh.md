## 适用场景

在默认情况下，存储桶和对象都是私有的。如果您希望第三方可以上传对象到存储桶，又不希望对方使用 CAM 账户或临时密钥等方式时，您可以使用预签名 URL 的方式将签名提交给第三方，以供完成临时的上传操作。收到有效预签名 URL 的任何人都可以上传对象。

预签名 URL 时，您可以在签名中设置将对象键包含在签名中，只许可上传为指定的对象键。您也可以在程序中指定预签名 URL 的有效时间，以保证超时后该 URL 不会被未授权方使用。

## 使用方法

### 使用 SDK

您可以直接调用 SDK 的预签名 URL 方法，请参见下列各语言 SDK 文档：

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31516)
-  [C SDK](https://intl.cloud.tencent.com/document/product/436/31520)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31524)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30598)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31528)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31532)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31536)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31540)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/32455)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31544)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31548)
