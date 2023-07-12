将文件存放到对象存储（Cloud Object Storage，COS）时，您需要先创建一个存储桶用于存放对象，您可以通过控制台、工具、API 或 SDK 的方式来创建存储桶。

创建存储桶后，您可将对象上传至该存储桶，此外还可以为存储桶配置其他功能，例如 [设置静态网站](https://intl.cloud.tencent.com/document/product/436/14984)、[设置存储桶标签](https://intl.cloud.tencent.com/document/product/436/30928) 、[设置存储桶加密](https://intl.cloud.tencent.com/document/product/436/33455) 等，更多配置指引请参见 [控制台概述](https://intl.cloud.tencent.com/document/product/436/11365)。


## 限制说明

1. 同个主账号下仅允许创建最多200个存储桶。
2. 存储桶一旦创建成功，存储桶名称和所属地域不能修改。
3. 同一主账号下所有存储桶名称唯一且不支持重命名。
4. 存储桶名称仅支持小写英文字母和数字，即[a-z，0-9]、中划线“-”及其组合。存储桶名称的最大允许字符受到 **[地域简称](https://intl.cloud.tencent.com/document/product/436/6224)** 和 **APPID** 的字符数影响，组成的完整请求域名字符数总计最多60个字符。例如请求域名`123456789012345678901-1250000000.cos.ap-beijing.myqcloud.com`总和为60个字符。
5. 存储桶命名不能以“-”开头或结尾。


## 使用方法

### 使用对象存储控制台

您可以使用对象存储控制台创建存储桶，详情请参见 [创建存储桶](https://intl.cloud.tencent.com/document/product/436/13309) 控制台文档。

### 使用工具

您可以使用工具创建存储桶，例如 COSBrowser 工具、COSCMD 工具等，详情请参见 [工具概览](https://intl.cloud.tencent.com/document/product/436/6242)。

### 使用 REST API

您可以直接使用 REST API 发起创建存储桶请求，详情请参见 [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) API 文档。

### 使用 SDK

您可以直接调用 SDK 的创建存储桶方法，详情请参见下列各语言 SDK 文档：

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31463)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31464)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30595)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31467)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31469)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471)
- [小程序 SDK](https://intl.cloud.tencent.com/document/product/436/30609)

