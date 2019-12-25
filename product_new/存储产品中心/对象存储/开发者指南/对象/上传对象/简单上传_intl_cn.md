## 适用场景

该操作适用于在单个请求中，上传一个不超过5GB的对象。

>
>1. 若您要上传的对象大于5GB，您必须使用 [分块上传](https://intl.cloud.tencent.com/document/product/436/14112) 方式。
>2. 在高宽带或弱网络环境中，若您要上传的对象较大，如超过100MB（即便小于5GB），我们建议您优先使用 [分块上传](https://intl.cloud.tencent.com/document/product/436/14112) 的方式。因为分块上传可以并行传输多个分块：在高宽带环境中，可以有效利用资源；在弱网络环境中，单一分块上传失败不会影响其他已上传的分块，通过简单的重试即可重传失败分块，从而提高整体的上传成功率。有关移动端在弱网络环境的上传，可参见 [弱网分块续传实践](https://intl.cloud.tencent.com/document/product/436/30932)。



## 使用方法

### 使用对象存储控制台
您可以使用对象存储控制台上传对象，详情请参见 [上传对象](https://intl.cloud.tencent.com/document/product/436/13321) 控制台指南文档。

### 使用 REST API

您可以直接使用 REST API 发起简单上传对象请求，详情请参见 [PUT Object](https://cloud.tencent.com/document/product/436/7749) API 文档。

### 使用 SDK
您可以直接调用 SDK 的简单上传对象方法，详情请参见下列各语言 SDK 文档：
- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31514)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31518)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30596)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31526)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31530)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546)
