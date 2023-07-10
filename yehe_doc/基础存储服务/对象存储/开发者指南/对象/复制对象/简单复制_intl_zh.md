## 适用场景

您可以在对象存储（Cloud Object Storage，COS）中将已存储的对象通过简单的复制操作，创建一个新的对象副本。在单个操作中，您可以复制最大5GB 的对象。当对象超过5GB 时，您必须使用 [分块复制](https://intl.cloud.tencent.com/document/product/436/14118) 接口来实现复制。复制对象有以下功能：

- 创建一个新的对象副本。
- 复制对象并更名，删除原始对象，实现重命名。
- 修改对象的存储类型，在复制时选择相同的源和目标对象键，修改存储类型。
- 在不同的腾讯云 COS 地域复制对象。
- 修改对象的元数据，在复制时选择相同的源和目标对象键，并修改其中的元数据。

复制对象时，默认将继承原对象的元数据，但创建日期将会按新对象的时间计算。

>?
>- 不支持对归档存储类型的对象进行复制粘贴。
>- 开启了多 AZ 配置的存储桶，不支持将多 AZ 存储类型复制为单 AZ 存储类型。
>- 子账号复制对象，需要拥有这三个权限：PutObject、GetObject、GetObjectACL。

## 使用方法

### 使用对象存储控制台

您可以使用对象存储控制台复制对象，详情请参见 [复制对象](https://intl.cloud.tencent.com/document/product/436/33456) 控制台指南文档。

### 使用 REST API

您可以直接使用 REST API 发起复制对象请求，详情请参见 [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) API 文档。

### 使用 SDK

您可以直接调用 SDK 的设置对象复制方法，详情请参见下列各语言 SDK 文档：

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/40494)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/44872)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/40171)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/44064)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/40495)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/44019)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/43865)
- [Node.js SDK ](https://intl.cloud.tencent.com/document/product/436/43874)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/45498)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/46470)
- [小程序 SDK](https://intl.cloud.tencent.com/document/product/436/43885)
