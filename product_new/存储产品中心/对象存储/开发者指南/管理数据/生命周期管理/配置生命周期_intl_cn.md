## 适用场景

利用生命周期设置，可以让符合规则的对象在指定的条件下自动执行一些操作。例如：

- 转换存储类型：将创建的对象在指定时间后转换为低频存储类型 STANDARD_IA 或者归档存储类型 ARCHIVE。
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

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31515)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31523)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30597)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31527)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31531)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31535)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31539)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/32454)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31543)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547)
