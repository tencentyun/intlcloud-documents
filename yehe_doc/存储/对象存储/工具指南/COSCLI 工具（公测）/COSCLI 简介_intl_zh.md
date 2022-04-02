
COSCLI 是腾讯云对象存储（Cloud Object Storage，COS）提供的客户端命令行工具。通过 COSCLI 工具，您可以通过简单的命令行指令对您 COS 中的对象（Object）实现批量上传、下载、删除等操作。

COSCLI 使用 Go 编写，基于 Cobra 框架，支持配置多个存储桶和跨桶操作。您可以通过 `./coscli [command] --help` 来查看 COSCLI 的使用方法。


## 功能列表

- [生成与修改配置文件 -  config](https://intl.cloud.tencent.com/document/product/436/43251)
- [创建存储桶 - mb](https://intl.cloud.tencent.com/document/product/436/43252)
- [删除存储桶 - rb](https://intl.cloud.tencent.com/document/product/436/43253)
- [存储桶标签 - bucket-tagging](https://intl.cloud.tencent.com/document/product/436/46272)
- [查询存储桶或文件列表 - ls](https://intl.cloud.tencent.com/document/product/436/43254)
- [获取不同类型文件的统计信息   - du](https://intl.cloud.tencent.com/document/product/436/43255)
- [上传下载或拷贝文件 - cp](https://intl.cloud.tencent.com/document/product/436/43256)
- [同步上传下载或拷贝文件 - sync](https://intl.cloud.tencent.com/document/product/436/43257)
- [删除文件 - rm](https://intl.cloud.tencent.com/document/product/436/43258)
- [获取文件哈希值 -   hash](https://intl.cloud.tencent.com/document/product/436/43259)
- [列出分块上传中产生的碎片   - lsparts](https://intl.cloud.tencent.com/document/product/436/43260)
- [清理碎片 -   abort](https://intl.cloud.tencent.com/document/product/436/43261)
- [取回归档文件 -   restore](https://intl.cloud.tencent.com/document/product/436/43262)
- [获取预签名 URL -   signurl](https://intl.cloud.tencent.com/document/product/436/43263)






