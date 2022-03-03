## Modules 发布

Module 是 Terraform 组合多种资源的配置形态，在部分多资源场景下，使用 Module 能够更好地抽象业务，减少配置成本。另外，Github 上的 Modules 可以发布到 [terraform 仓库](https://registry.terraform.io/) 中。本文将介绍创建 Terraform TencentCloud Module 创建和发布方法

## 创建公共 Module

GitHub 新建代码仓库，命名格式为：`terraform-<PROVIDER>-<NAME>`， 如 [terraform-tencentcloud-vpc](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-vpc)

一个基本 Module 包含以下文件：

```
.
├── main.tf # 编写模块资源
├── variables.tf # 声明模块变量
├── outputs.tf # 声明模块输出
├── LICENCE # 声明许可
└── README.md # 自述文件

```

建议添加 example 目录，存放该模块引入和使用示例，参考 https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-vpc/tree/master/examples

## Module 发布

### 上传步骤

* 访问 [registry.terraform.io](https://registry.terraform.io/) 在右上角 Publish 下拉菜单中选择 Module

![](https://qcloudimg.tencent-cloud.cn/raw/3413bcf31b0f1d22517cee72bf535bea.png)

* 点击 Select Repository on GitHub 下拉菜单，可以看到个人账户下有管理权限的 Modules 仓库，选择后点击 PUBLISH MODULE 按钮
![](https://qcloudimg.tencent-cloud.cn/raw/b7dcc4ce6be947cff50762fd8bfc32b7.png)
![](https://qcloudimg.tencent-cloud.cn/raw/cd927fe3533319ac0524b50686f9ed02.png)


* 你的仓库将会在几分钟后自动同步到 terraform registry 中。
![](https://qcloudimg.tencent-cloud.cn/raw/08788ec56f75d1fa1befa64780def469.png)


注：Module 亦可以使用个人 GitHub 仓库发布，仓库名称符合 `terraform-tencentcloud-<NAME>` 的 Modules 也会收录在 tencentcloud 的 Modules 中