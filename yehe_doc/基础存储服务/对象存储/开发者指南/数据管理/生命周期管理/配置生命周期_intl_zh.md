## 适用场景

利用生命周期设置，可以让符合规则的对象在指定的条件下自动执行一些操作。例如：

- 转换存储类型：将创建的对象在指定时间后转换为低频存储类型（STANDARD_IA）、智能分层存储（INTELLIGENT_TIERING）、归档存储类型（ARCHIVE）和深度归档存储类型（DEEP_ARCHIVE）。
- 过期删除：设置对象的过期时间，使对象到期后被自动删除。

详情请参见 [生命周期概述](https://intl.cloud.tencent.com/document/product/436/17028) 文档和 [生命周期配置元素](https://intl.cloud.tencent.com/document/product/436/17029) 文档。

## 使用方法

### 使用对象存储控制台

您可以使用对象存储控制台配置生命周期，详情请参见 [设置生命周期](https://intl.cloud.tencent.com/document/product/436/14605) 控制台指南文档。

### 使用 REST API

您可以直接使用 REST API 配置和管理存储桶中对象的生命周期，详情请参见以下 API 文档：

- [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280)
- [GET Buket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278)
- [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284)

### 使用 SDK

您可以直接调用 SDK 的生命周期方法，详情请参见下列各语言 SDK 文档：

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/36197)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/12301)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/35269)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/39152)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37855)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/10199)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/35806)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/35860)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/35002)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547)
