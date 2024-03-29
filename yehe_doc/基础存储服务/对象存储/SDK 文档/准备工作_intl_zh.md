在使用 SDK 时可能会涉及以下概念和术语，建议您提前了解并准备相关信息：

| 名称             | 描述                                                         |
| :--------------- | :----------------------------------------------------------- |
| APPID            | 开发者访问 COS 服务时拥有的用户维度唯一资源标识，用以标识资源，可在 [API 密钥管理](https://console.cloud.tencent.com/capi) 页面获取 |
| SecretId         | 开发者拥有的项目身份识别 ID，用于身份认证，可在 [API 密钥管理](https://console.cloud.tencent.com/capi) 页面获取 |
| SecretKey        | 开发者拥有的项目身份密钥，可在 [API 密钥管理](https://console.cloud.tencent.com/capi) 页面获取 |
| Bucket           | 存储桶，COS 中用于存储数据的容器。有关存储桶的进一步说明，请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) 文档 |
| BucketName-APPID | 完整的存储桶名称，以 APPID 为后缀，例如 `examplebucket-1250000000` |
| Object           | 对象，COS 中存储的具体文件，是存储的基本实体                 |
| ObjectKey        | 对象键，对象（Object）在存储桶（Bucket）中的唯一标识。有关对象与对象键的进一步说明，请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) 文档 |
| Region           | 地域信息，枚举值可参见 [可用地域](https://intl.cloud.tencent.com/document/product/436/6224) 文档，例如：ap-beijing、ap-hongkong、eu-frankfurt 等 |
| ACL              | 访问控制列表（Access Control List），是指特定 Bucket 或 Object 的访问控制信息列表，请参见 [ACL概述](https://intl.cloud.tencent.com/document/product/436/30583) 文档 |

>? 如果您在使用 XML 版本 SDK 时遇到函数或方法不存在等错误，请先将 XML 版本 SDK 升级到最新版再重试。
>
