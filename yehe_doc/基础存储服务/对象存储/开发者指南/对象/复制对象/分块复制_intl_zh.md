## 适用场景

当需要复制一个超过5GB的对象时，您需要选择分块复制的方法来实现。使用分块上传的 API 来创建一个新的对象，并使用 Upload Part - Copy 的功能，携带 x-cos-copy-source 头部来指定源对象，流程包括：

1. 初始化一个分块上传的对象。
2. 复制源对象的数据，可指定 x-cos-copy-source-range 头部，每次只可复制最多5GB 数据。
3. 完成分块上传。

>? 使用腾讯云 COS 提供的 SDK 可以轻松完成分块复制的功能。

## 使用方法

### 使用 REST API

您可以直接使用 REST API 发起分块复制请求，请参见以下 API 文档：

- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287)
- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742)
- [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740)

### 使用 SDK

您可以直接调用 SDK 的复制分块方法，请参见下列各语言 SDK 文档：

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37674#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [C SDK](https://www.tencentcloud.com/document/product/436/44872)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [.NET(C#) SDK](https://www.tencentcloud.com/document/product/436/40171)
- [Go SDK](https://www.tencentcloud.com/document/product/436/44064)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37683#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [小程序 SDK](https://www.tencentcloud.com/document/product/436/43885)
