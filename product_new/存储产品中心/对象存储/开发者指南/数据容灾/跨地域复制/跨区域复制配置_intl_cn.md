## 适用场景
通过配置跨地域复制规则，用户可以将对象数据从源存储桶复制到另一地域的指定目标存储桶中。跨地域复制功能适用于异地容灾、满足行业合规性要求、数据迁移与备份、降低客户访问延迟、方便不同地域的集群访问数据等场景。

>开启了版本控制后，新上传的对象将会产生多个版本并占用存储空间，因此这些版本的对象同样收取存储费用。

## 使用方法

### 使用对象存储控制台
您可以通过对象存储控制台设置跨地域复制规则，请参见 [设置跨地域复制](https://intl.cloud.tencent.com/document/product/436/19235) 控制台指南文档。

### 使用 REST API
您可以直接使用 REST API 配置和管理存储桶的跨地域复制规则，具体可参考以下 API 文档：
- [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) 
- [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) 
- [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) 

### 使用 SDK
您可以直接调用 SDK 的跨地域复制方法，详情请参见下列各语言 SDK 文档：

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/36196#cross-region-replication)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519#cross-region-replication)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31523#cross-region-replication)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/35272#cross-region-replication)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31527#cross-region-replication)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31531#cross-region-replication)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31535#cross-region-replication)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/35805#cross-region-replication)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/35859)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/34996#cross-region-replication)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547#cross-region-replication)
