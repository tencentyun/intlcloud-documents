本文介绍如何使用 TCCLI 查看产品接口的帮助信息。

## 操作步骤

### 查看帮助信息
- 执行以下命令，查看支持的产品。您也可以在 [API中心](https://www.tencentcloud.com/document/api) 的文档中查看。
```bash
tccli help
```
- 以云服务器 CVM 为例，执行以下命令，查看 CVM 支持的接口。
```bash
tccli cvm help
```
- 以云硬盘 CBS 中的 DescribeDisks 接口为例，执行以下命令，查看接口支持的参数。具体的参数说明和 API 的相关信息可以在腾讯云官网查看对应的 API 文档。
```bash
tccli cbs DescribeDisks help
```

### 查看详细帮助信息
TCCLI 默认显示简化版帮助信息，如需查看详细信息，可以使用 `--detail` 选项。
- 执行以下命令，查看支持的产品的详细信息。
```bash
tccli help --detail
```
- 以云服务器 CVM 为例，执行以下命令，查看 CVM 支持的接口的详细信息。
```bash
tccli cvm help --detail
```
- 以 CBS 中的 DescribeDisks 接口为例，执行以下命令，查看接口的入参、出参的详细信息及使用示例。
```bash
tccli cbs DescribeDisks help --detail
```
