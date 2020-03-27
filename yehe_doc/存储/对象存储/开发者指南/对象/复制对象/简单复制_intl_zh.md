## 适用场景

您可以在 COS 中将已存储的对象通过简单的复制操作，创建一个新的对象副本。在单个操作中，您可以复制最大5GB的对象。当对象超过5GB时，您必须使用分块上传的接口来实现复制。复制对象有以下功能：

- 创建一个新的对象副本。
- 复制对象并更名，删除原始对象，实现重命名。
- 修改对象的存储类型，在复制时选择相同的源和目标对象键，修改存储类型。
- 在不同的腾讯云 COS 地域复制对象。
- 修改对象的元数据，在复制时选择相同的源和目标对象键，并修改其中的元数据。

复制对象时，默认将继承原对象的元数据，但创建日期将会按新对象的时间计算。

>
>- 不支持对归档存储类型的对象进行复制粘贴。
>- 标准存储（多 AZ）类型目前仅支持复制为标准存储（多 AZ）类型，不支持复制为标准存储、低频和归档存储类型。

## 使用方法

### 使用对象存储控制台

您可以使用对象存储控制台复制对象，详情请参见 [复制对象](https://intl.cloud.tencent.com/document/product/436/33456) 控制台指南文档。

### 使用 REST API

您可以直接使用 REST API 发起复制对象请求，详情请参见 [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) API 文档。

### 使用 SDK

您可以直接调用 SDK 的设置对象复制方法，详情请参见下列各语言 SDK 文档：

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31514)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31518)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30596)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31526)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31530)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK ](https://intl.cloud.tencent.com/document/product/436/31710)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546)
- [小程序 SDK](https://intl.cloud.tencent.com/document/product/436/32457)
