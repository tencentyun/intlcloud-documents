[Terraform Tencent Cloud Provider](https://github.com/tencentcloudstack/terraform-provider-tencentcloud) 由腾讯云的 IaC 团队维护，我们欢迎更多的开发者参与进来。

>?
> 本文档适用于 Terraform Tencent Cloud Provider 代码开发人员。


## 贡献

请按照以下步骤确保您的 Contribute 能够顺利进行。当然您可以先对 Provider 的[实现原理](https://www.tencentcloud.com/document/product/1172/52386)做一个大致的了解，同时也可以查看我们的[要求与建议](https://www.tencentcloud.com/document/product/1172/52388)。

### 1. 配置开发环境

在开始开发之前，您需要安装 Terraform 和 Go 拉取代码库，进行程序编译并设置测试。请参阅[开发环境配置](https://www.tencentcloud.com/document/product/1172/52387)。

### 2. 编写代码

根据您贡献代码的类型，从下面的表格中，参阅相应的指引文档。

| 贡献类型 | 描述 |
|---------|---------|
| [Resource and Data Sources](https://www.tencentcloud.com/document/product/1172/52377) | 通过向 Terraform Tencent Cloud Provider 添加新 Resource 和 DataSource 实现，从而支持管理腾讯云产品功能或者查询腾讯云的远程数据 |
| [Bug Fix or Enhancement](https://www.tencentcloud.com/document/product/1172/52378) | 大部分的请求，应该是对已有功能的增强和修复 |
| [Tagging Support](https://www.tencentcloud.com/document/product/1172/52380) | 当前资源需要支持 Tag 标签，需要使用统一的 Tag 服务接口 |
| [Documentation Changes](https://www.tencentcloud.com/document/product/1172/52379) | 文档的新增与变更 |

### 3. 编写测试

我们要求所有的代码贡献，必须有相对应的测试覆盖。请参阅[用例编写](https://www.tencentcloud.com/document/product/1172/52381)。

### 4. 创建拉取请求

当您的贡献准备就绪时，在提供商存储库中创建一个拉取请求。请参阅[发起PR](https://www.tencentcloud.com/document/product/1172/52382)。

### 5. 更新变更日志

开源项目需要维护一个用户友好、可读的 CHANGELOG.md，它允许用户一眼就知道发布是否应该对他们产生任何影响，并评估升级的风险。请参阅[提交变更日志](https://www.tencentcloud.com/document/product/1172/52383)。

## Modules

除了贡献 Provider 源码之外，我们还欢迎提交 Modules。请参与[贡献 Modules](https://www.tencentcloud.com/document/product/1172/52310)。