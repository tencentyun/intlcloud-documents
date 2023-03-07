## 基础设施即代码

完全兼容 Terraform HCL 声明式语法对基础设施云资源进行代码化描述和版本化的管理，提升自动化部署和运维效率，降低管理和配置成本。

## 云端状态管理

Terraform 引入了远程状态存储机制 Backend，目前腾讯云可通过 [对象存储 COS](https://www.tencentcloud.com/document/product/436) 来管理用户的 tfstate 文件，避免将文件保存在本地，造成丢失。同时，远程存储使多人同时对 Terraform 资源进行管理提供基础。

## 提供模板

提供丰富的腾讯云 [Terraform Modules](https://registry.terraform.io/search/modules?q=terraform-tencentcloud-modules)，开发者只需关心 Module 输入参数，无需关心 Module 中资源的定义、参数、语法等细节问题，抽出更多精力投入到架构设计和资源关系整合上。

## 存量资源管理

兼容 [Terraformer](https://github.com/GoogleCloudPlatform/terraformer.git) 逆向工具，支持对存量腾讯云资源的一键导入，快速生成 tf 和 tfstate 文件，有效降低云资源管理与迁移成本。