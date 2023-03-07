## 基本概念

### GitOps

GitOps 是 Weaveworks 提出的一种持续交付方式，它的核心思想是将应用系统的声明性基础架构和应用程序存放在 Git 版本库中。将 Git 作为交付流水线的核心，每个开发人员都可以提交拉取请求（Pull Request）并使用 Git 来加速和简化 Terraform 的应用程序部署和运维任务。通过使用像 Git 这样的简单工具，开发人员可以更高效地将注意力集中在创建新功能而不是运维相关任务上（例如，应用系统安装、配置、迁移等）。

### Terraform 根模块

根配置（根模块）是您在其中运行 Terraform CLI 的工作目录。

#### 根模块标准：
- **最大限度地减少每个根模块中的资源数量**


   请防止单个根配置过大，同时还要防止同一目录和状态下存储的资源过多。每次运行 Terraform 时，特定根配置中的所有资源都会刷新。如果单个状态中包含的资源过多，则可能会导致执行缓慢。一般规则：在单个状态下，不要添加超过 100 个资源（最好不要超过十几个）。

- **为每个应用使用单独的目录**


   如需相互独立地管理应用和项目，请将每个应用和项目的资源放在其各自的 Terraform 目录中。服务可能表示特定应用或通用服务，例如共享网络。将特定服务的所有 Terraform 代码嵌套在一个目录（包括子目录）下。


## 项目结构

将服务的 Terraform 配置拆分为两个顶级目录：包含服务的实际配置的 **modules 目录**和包含每个环境的根配置的 **environments 目录**。
- modules 目录中为抽象出来的可复用模块。

- environments 目录用于隔离不同环境，用户可以在不同环境中使用不同的云厂商或配置不同的账号以实现多云管理（prod 目录中还通过 workspace 进行业务层面的隔离）。


   以下是推荐的项目结构，详细内容可以参考 [Coding](https://tencentiac.coding.net/p/terraform/d/gitops-terraform/git)、[Github](https://github.com/tongyiming/gitops-terraform) 代码仓库。

   ``` bash
   .
   ├── README.md
   ├── environments
   │   ├── dev
   │   │   ├── main.tf
   │   │   └── provider.tf
   │   └── prod
   │       ├── cicd
   │       │   └── main.tf
   │       ├── local.tf
   │       ├── main.tf
   │       ├── provider.tf
   │       └── qta
   │           └── main.tf
   └── modules
     ├── network
     │   ├── main.tf
     │   ├── outputs.tf
     │   ├── provider.tf
     │   └── variables.tf
     ├── security_group
     │   ├── main.tf
     │   ├── outputs.tf
     │   ├── provider.tf
     │   └── variables.tf
     └── tke
         ├── main.tf
         ├── outputs.tf
         ├── provider.tf
         └── variables.tf
   ```

## 代码复用

若您希望代码复用，建议您使用[ Terraform Module](https://developer.hashicorp.com/terraform/language/modules)。您可以选择使用自定义或使用供应商提供的 Module，例如 [腾讯云官方 Module](https://github.com/terraform-tencentcloud-modules/)。在该项目 Modules 目录中的已封装 Module 模板，通过对资源进行分类，将每一类资源用一个目录管理。然后在一个模板中管理目标资源，完成目标资源和依赖资源的串联，例如 TKE 模板中依赖 Network 资源模板。

## 构建安全的 Terraform 更新流程

确保基础架构的安全性取决于是否有一个稳定安全的应用 Terraform 更新的流程。

#### 先规划再执行

始终先为 Terraform 执行生成计划。将计划保存到输出文件中。获得基础架构所有者的批准后，执行计划。即使开发者在本地对更改进行原型设计，也应该生成计划并查看应用添加、修改和销毁的资源。

#### 实现自动化流水线

为了确保一致的执行上下文，通过自动化工具执行 Terraform。避免人为因素的影响。

#### 避免导入现有资源
- 请尽可能避免导入现有资源（使用 terraform import），因为这样做可能会很难完全了解手动创建的资源的来源和配置。应通过 Terraform 创建新资源并删除旧资源。

- 如果删除旧资源会带来大量重复劳动，请使用 terraform import 命令并明确批准。将资源导入 Terraform 后，只能使用 Terraform 对其进行管理。


#### 不要手动修改 Terraform 状态

若您在使用 Terraform 管理基础设施时又手动在控制台更新资源属性，则会导致 Terraform 执行计划时出现意外结果。如果您需要修改 Terraform 状态信息，请使用命令 `terraform state`。

#### 版本控制

与其他形式的代码类似，您可以将基础架构代码存储在版本控制系统中以保留历史记录并允许轻松回滚。

## 环境隔离

支持的隔离方式如下：

#### 目录隔离

通过不同目录进行分组，在子目录中分别配置跟模块实现隔离（本文示例使用该方式）。

使用说明：environments 中的 dev 和 prod 目录使用不同的根模块隔离不同环境的基础设施配置信息。

#### branch 隔离

不同环境使用不同分支，在对应分支的根模块下初始化 terraform 即可。

使用说明：与目录隔离类似。不同环境使用不同的分支，直接在不同分支中使用根模块配置特定环境信息，通过合并不同分支的更改来部署修改。

#### workspace 隔离

相同根模块下通过配置不同 workspace 来分别创建资源。

使用说明：prod 目录中的 cicd 和 qta 使用 workspace 隔离不同业务的配置信息。