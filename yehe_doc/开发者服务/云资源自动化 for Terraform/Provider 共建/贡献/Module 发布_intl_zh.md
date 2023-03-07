## 操作场景

Module 是 Terraform 组合多种资源的配置形态。在部分多资源场景下，使用 Module 能够更好地抽象业务，减少配置成本。您可将 Github 中的 Modules 发布到 [terraform 仓库](https://registry.terraform.io/)。本文介绍如何创建及发布 Terraform TencentCloud Module。

## 操作步骤

### 创建公共 Module

在 GitHub 中新建代码仓库。
- 命名格式为 `terraform-<PROVIDER>-<NAME>`，例如 [terraform-tencentcloud-vpc](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-vpc)。

- 一个基本的 Module 需包含以下文件：

   ``` bash
   .
   ├── main.tf # 编写模块资源
   ├── variables.tf # 声明模块变量
   ├── outputs.tf # 声明模块输出
   ├── LICENCE # 声明许可
   └── README.md # 自述文件
   ```

   >?
   > 建议添加 example 目录，存放该模块引入和使用示例。您可参考 [examples](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-vpc/tree/master/examples) 进行添加。

### 发布 Module
1. 登录 [registry.terraform.io ](https://registry.terraform.io/)，选择页面右上角的 **Publish**，并在下拉列表中单击 **Module**。如下图所示：![](https://qcloudimg.tencent-cloud.cn/image/document/98796ead2fca3f29e837b42c88f054dd.png)

2. 在页面中展开 “Select Repository on GitHub” 下拉列表，可在列表中查看个人账户下有管理权限的 Modules 仓库，选择需发布的 Module。如下图所示：


   ![](https://qcloudimg.tencent-cloud.cn/image/document/e4f81682690e3b037a7f89dc4c81df74.png)


   >!
   > Module 可以使用个人 GitHub 仓库发布。若仓库名称符合 `terraform-tencentcloud-<NAME>`，则该 Modules 也会收录在 tencentcloud 的 Modules 中。

3. 勾选 “ I agree to the Terms of Use.”后，单击 **PUBLISH MODULE**。

4. 该仓库将会在几分钟后，自动同步到 terraform registry 中。如下图所示：![](https://qcloudimg.tencent-cloud.cn/image/document/4d28ea3da90c2eb1ccb775ea11f7fd41.png)


### 添加仓库合并检查（可选）

若您的 Module 涉及多人协作，则可以借助 GitHub Action 对请求合并的代码做初步检查。

本文以 [terraform-tencentcloud-vpc](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-vpc) 为例，在仓库根目录下新建 `.github/workflow` 目录，创建 `pull-request.yml` 文件。示例代码如下：
``` yaml
name: MR_CHECK

on:
  pull_request:
    branches: [ master ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: hashicorp/setup-terraform@v1
      - name: Module Files Checking
        run: |
          files=(
            LICENSE
            main.tf
            version.tf
            variables.tf
            outputs.tf
            README.md
          )

          test -d examples || echo "[WARN] Missing ./examples in modules directory, we strongly recommend you to provide example usage of this module."

          for i in ${files[@]} ; do
            fileCount=$(find ./ -name $i | wc -l)
            if [[ $fileCount -gt 0 ]]; then
              echo "[INFO] File: $i exist."
            else
              echo "[ERROR] Missing $i, a recommend module should include these files:\n ${files[@]}"
              exit -1
            fi
          done
      - name: Terraform Validate
        run: |
          terraform init
          terraform validate

      - name: Terraform Format Check
        run: |
          terraform fmt -diff -check -recursive

```

说明如下：
- `Module Files Checking`：检查该目录下是否包含上文中需要的文件。

- `Terraform Validate`：进行 Module 参数检查。

- `Terraform Format Check`：校验 Module 中的 tf 代码格式。 
