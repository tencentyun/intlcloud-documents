
## 简介	
欢迎使用腾讯云命令行工具 TCCLI，TCCLI 是管理腾讯云资源的统一工具。通过腾讯云命令行工具，您可以快速轻松的调用腾讯云 API 来管理您的腾讯云资源。您还可以基于 TCCLI 来做自动化和脚本处理，能够以更多样的方式进行组合和重用。

<dx-alert infotype="explain" title="">
- 本文档介绍新版命令行工具 TCCLI，我们强烈建议您使用 TCCLI，若您仍使用旧版命令行工具，请参见 [旧版命令行工具](https://www.tencentcloud.com/document/product/1013) 介绍和操作指南。
- 您也可以在 Github 中查阅 [tencentcloud-tccli](https://github.com/TencentCloud/tencentcloud-cli)，如果您在使用中有任何问题，可以直接提交 [Github Issues](https://github.com/TencentCloud/tencentcloud-cli/issues/new) 向我们反馈。

</dx-alert>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                推荐使用 API Explorer
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn"><i class="rno-icon-explorer"></i>点击调试</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                您可以通过 API Explorer 工具自动生成 TCCLI 命令，帮助您更方便使用 TCCLI。
            </div>
        </div>
    </div>
</div>

## 产品功能
### 多产品集成

TCCLI 集成了腾讯云所有支持云 API 的产品，可以在命令行下完成对腾讯云产品的配置和管理。包括使用 TCCLI 创建云服务器，操作云服务器，通过 TCCLI 创建云硬盘、查看云硬盘使用情况，通过 TCCLI 创建 VPC 网络、往私有网络中添加资源等等，所有在控制台页面能完成的操作，均能在 TCCLI 上通过执行命令实现。

通过 TCCLI，可以进行无图形页面操作腾讯云资源。

### 多账户支持
TCCLI 支持设置多个账号，可完成账号间快速切换。

### 多平台支持
支持在 Windows、Mac OS、Linux/Unix 等操作系统上安装和使用，满足不同开发者的要求。Linux/Unix 环境下支持命令自动补齐。
在 Windows、MacOS、Linux/Unix 操作系统上安装 Python 环境后，即可通过 pip 命令执行安装 TCCLI。在 Linux 下使用熟练后，切换到 Windows 上同样可以执行相应操作，各个平台对应功能的执行命令均相同，无差异化的指令。

### 多种输出格式
命令行工具支持多种输出格式，可以自由选择 text、JSON、table 等作为输出格式。

- text 是以文本的形式输出，每个返回一行为一条记录，用空格隔开，适合获取资源列表保存成文本或自行转换成表格。
- JSON 是以 JSON 形式返回，适合二次开发编码，通过解析 JSON 返回获取想要的信息。
- table 是以表格形式返回，可视化较好，适合单纯使用命令行工具操作云资源。

## 支持命令行工具的产品
腾讯云 API 3.0 的产品，均支持命令行工具。您可前往 [API 中心](https://www.tencentcloud.com/document/api/213/)进行查看，若产品名称后带有3.0标志，则该产品及其对应 API 均支持命令行工具。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8zH8964_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221222102318.png)