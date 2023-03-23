当您在某些情况下需要删除存储桶时，您可以通过控制台、工具、API 或 SDK 的方式来删除存储桶。

>!删除存储桶后，将无法恢复，请谨慎操作。

## 限制说明

- 目前仅支持删除数据已被清空的存储桶，如果存储桶中仍有对象或文件碎片，将会删除失败。请在执行删除存储桶前确保存储桶内已清空对象。前往了解如何 [清空存储桶](https://intl.cloud.tencent.com/document/product/436/30926)。
- 当删除存储桶时，您需要确保操作的身份已被授权该操作，并确认传入了正确的存储桶名称（Bucket）和地域（Region）参数。


## 使用方法

### 使用对象存储控制台

您可以使用对象存储控制台删除存储桶，详情请参见 [删除存储桶](https://intl.cloud.tencent.com/document/product/436/30361) 控制台指南文档。

### 使用工具

您可以使用工具删除存储桶，例如 COSBrowser 工具、COSCMD 工具等，详情请参见 [工具概览](https://intl.cloud.tencent.com/document/product/436/6242)。

### 使用 REST API

您可以直接使用 REST API 发起删除存储桶请求，详情请参见 [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) API 文档。

### 使用 SDK

您可以直接调用 SDK 的删除存储桶方法，详情请参见下列各语言 SDK 文档：

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31463)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31464)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30595)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31467)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31477)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31469)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471)
- [小程序 SDK](https://www.tencentcloud.com/document/product/436/31472)

