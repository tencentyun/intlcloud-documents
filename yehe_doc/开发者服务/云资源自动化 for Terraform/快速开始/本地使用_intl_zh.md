## 安装 Terraform

### 下载安装包

前往 [Terraform 官网](https://www.terraform.io/downloads.html)，使用命令行直接安装 Terraform 或下载二进制安装文件。

### 解压并配置全局路径
- Linux：请参见 [Linux全局路径配置](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix?spm=a2c4g.11186623.0.0.51772e079tx0CM)。

- Windows：请参见 [Windows全局路径配置](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows?spm=a2c4g.11186623.0.0.51772e079tx0CM)。

- MAC：请参见 [Mac全局路径配置](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix)。


### 验证是否安装成功

执行以下命令，查看是否安装成功。
``` html
terraform  -version
```

返回信息如下所示（版本号可能存在差异），则表示安装成功。
``` bash
Terraform v1.3.0
on darwin_amd64

Your version of Terraform is out of date! The latest version
is 1.3.2. You can update by downloading from https://www.terraform.io/downloads.html
```

## 认证和鉴权

### 凭证获取

在首次使用 Terraform 之前，请前往 [云 API 密钥页面](https://console.cloud.tencent.com/cam/capi) 申请安全凭证 SecretId 和 SecretKey。若已有可使用的安全凭证，则跳过该步骤。
1. 登录 [访问管理控制台](https://console.cloud.tencent.com/cam/overview)，在左侧导航栏，选择**访问密钥 > API 密钥管理**。

2. 在 API 密钥管理页面，单击**新建密钥**，即可以创建一对 SecretId/SecretKey。


### 静态凭证鉴权

在用户目录下创建 `provider.tf` 文件，输入如下内容：

`my-secret-id` 及 `my-secret-key` 请替换为 [获取凭证](https://www.tencentcloud.com/document/product/1172/52304) 中的 SecretId 和 SecretKey。

``` tcl
provider "tencentcloud" {
  secret_id = "my-secret-id"
  secret_key = "my-secret-key"
}
```

### 环境变量鉴权

请将如下信息添加至环境变量配置：

`YOUR_SECRET_ID` 及 `YOUR_SECRET_KEY` 请替换为 [获取凭证](https://www.tencentcloud.com/document/product/1172/52304) 中的 SecretId 和 SecretKey。

``` shell
export TENCENTCLOUD_SECRET_ID=YOUR_SECRET_ID
export TENCENTCLOUD_SECRET_KEY=YOUR_SECRET_KEY
```

## 使用 Terraform 创建腾讯云 VPC
1. 创建 provider.tf 文件，指定 provider 配置信息。文件内容如下：

   ``` tcl
   terraform {
     required_providers {
       tencentcloud = {
         source = "tencentcloudstack/tencentcloud"
         # 通过version指定版本
         # version = ">=1.60.18"
       }
     }
   }
   
   provider "tencentcloud" {
     region = "ap-guangzhou"
     # secret_id = "my-secret-id"
     # secret_key = "my-secret-key"
   }
   ```
2. 创建 main.tf 文件，配置腾讯云 Provider 并创建私有网络 VPC。文件内容如下：

   ``` bash
   resource "tencentcloud_vpc" "foo" {
       name         = "ci-temp-test-updated"
       cidr_block   = "10.0.0.0/16"
       dns_servers  = ["119.29.29.29", "8.8.8.8"]
       is_multicast = false
   
       tags = {
           "test" = "test"
       }
   }
   ```
3. 执行以下命令，初始化工作目录并下载插件。

   ``` html
   terraform init
   ```

   返回信息如下所示：
   

   >?
   > 遇到下载失败问题，请参考 [Init 加速](https://www.tencentcloud.com/document/product/1172/52391)。


   ``` bash
   ➜  terraform_workspace terraform init
   
   Initializing the backend...
   
   Initializing provider plugins...
   - Finding latest version of tencentcloudstack/tencentcloud...
   - Installing tencentcloudstack/tencentcloud v1.60.18...
   - Installed tencentcloudstack/tencentcloud v1.60.18 (signed by a HashiCorp partner, key ID 84F69E1C1BECF459)
   
   Partner and community providers are signed by their developers.
   If you'd like to know more about provider signing, you can read about it here:
   https://www.terraform.io/docs/cli/plugins/signing.html
   
   Terraform has created a lock file .terraform.lock.hcl to record the provider
   selections it made above. Include this file in your version control repository
   so that Terraform can guarantee to make the same selections by default when
   you run "terraform init" in the future.
   
   Terraform has been successfully initialized!
   
   You may now begin working with Terraform. Try running "terraform plan" to see
   any changes that are required for your infrastructure. All Terraform commands
   should now work.
   
   If you ever set or change modules or backend configuration for Terraform,
   rerun this command to reinitialize your working directory. If you forget, other
   commands will detect it and remind you to do so if necessary.
   ```
4. 执行以下命令，升级 Provider 版本。

   ``` html
   terraform init -upgrade
   ```

   返回信息如下所示：

   ``` bash
   ➜  terraform_workspace terraform init -upgrade
   
   Initializing the backend...
   
   Initializing provider plugins...
   - Finding tencentcloudstack/tencentcloud versions matching ">= 1.60.18"...
   - Installing tencentcloudstack/tencentcloud v1.60.19...
   - Installed tencentcloudstack/tencentcloud v1.60.19 (signed by a HashiCorp partner, key ID 84F69E1C1BECF459)
   
   Partner and community providers are signed by their developers.
   If you'd like to know more about provider signing, you can read about it here:
   https://www.terraform.io/docs/cli/plugins/signing.html
   
   Terraform has made some changes to the provider dependency selections recorded
   in the .terraform.lock.hcl file. Review those changes and commit them to your
   version control system if they represent changes you intended to make.
   
   Terraform has been successfully initialized!
   
   You may now begin working with Terraform. Try running "terraform plan" to see
   any changes that are required for your infrastructure. All Terraform commands
   should now work.
   
   If you ever set or change modules or backend configuration for Terraform,
   rerun this command to reinitialize your working directory. If you forget, other
   commands will detect it and remind you to do so if necessary.
   ```
5. 执行以下命令，查看执行计划，显示将要创建的资源详情。

   ``` html
   terraform plan
   ```

   返回信息如下所示：

   ``` bash
   ➜  terraform_workspace terraform plan
   
   Terraform used the selected providers to generate the following execution plan. Resource actions are
   indicated with the following symbols:
     + create
   
   Terraform will perform the following actions:
   
     # tencentcloud_vpc.foo will be created
     + resource "tencentcloud_vpc" "foo" {
         + cidr_block             = "10.0.0.0/16"
         + create_time            = (known after apply)
         + default_route_table_id = (known after apply)
         + dns_servers            = [
             + "119.29.29.29",
             + "8.8.8.8",
           ]
         + id                     = (known after apply)
         + is_default             = (known after apply)
         + is_multicast           = false
         + name                   = "ci-temp-test-updated"
         + tags                   = {
             + "test" = "test"
           }
       }
   
   Plan: 1 to add, 0 to change, 0 to destroy.
   
   ─────────────────────────────────────────────────────────────────────────────────────────────────────────────
   
   Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these
   actions if you run "terraform apply" now.
   ```
6. 执行以下命令，创建资源。

   ``` html
   terraform apply
   ```

   根据提示输入 yes 创建资源，返回信息如下所示：

   ``` bash
   ➜  terraform_workspace terraform apply
   
   Terraform used the selected providers to generate the following execution plan. Resource actions are
   indicated with the following symbols:
     + create
   
   Terraform will perform the following actions:
   
     # tencentcloud_vpc.foo will be created
     + resource "tencentcloud_vpc" "foo" {
         + cidr_block             = "10.0.0.0/16"
         + create_time            = (known after apply)
         + default_route_table_id = (known after apply)
         + dns_servers            = [
             + "119.29.29.29",
             + "8.8.8.8",
           ]
         + id                     = (known after apply)
         + is_default             = (known after apply)
         + is_multicast           = false
         + name                   = "ci-temp-test-updated"
         + tags                   = {
             + "test" = "test"
           }
       }
   
   Plan: 1 to add, 0 to change, 0 to destroy.
   
   Do you want to perform these actions?
     Terraform will perform the actions described above.
     Only 'yes' will be accepted to approve.
   
     Enter a value: yes
   
   tencentcloud_vpc.foo: Creating...
   tencentcloud_vpc.foo: Still creating... [10s elapsed]
   tencentcloud_vpc.foo: Creation complete after 13s [id=vpc-07mx4yfd]
   
   Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
   ```

   执行完毕后，您可以在腾讯云控制台查看创建的资源。

7. （可选）更新资源。


   若您将资源配置信息修改为如下所示内容：

   ``` bash
   resource "tencentcloud_vpc" "foo" {
       name         = "ci-temp-test-updated2"
       cidr_block   = "10.0.0.0/16"
       dns_servers  = ["119.29.29.29", "8.8.8.8"]
       is_multicast = false
   
       tags = {
           "test" = "test"
       }
   }
   ```

   请执行 `terraform plan` 命令更新计划。返回信息如下所示：

   ``` bash
   ➜  terraform_workspace terraform plan 
   tencentcloud_vpc.foo: Refreshing state... [id=vpc-jhmdf9q9]
   
   Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
     ~ update in-place
   
   Terraform will perform the following actions:
   
     # tencentcloud_vpc.foo will be updated in-place
     ~ resource "tencentcloud_vpc" "foo" {
           id                     = "vpc-jhmdf9q9"
         ~ name                   = "ci-temp-test-updated" -> "ci-temp-test-updated2"
           tags                   = {
               "test" = "test"
           }
           # (6 unchanged attributes hidden)
       }
   
   Plan: 0 to add, 1 to change, 0 to destroy.
   
   ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   
   Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply"
   now.
   ```

   执行`terraform apply`命令，应用更新的数据创建资源。返回信息如下：

   ``` bash
   ➜  terraform_workspace terraform apply
   tencentcloud_vpc.foo: Refreshing state... [id=vpc-jhmdf9q9]
   
   Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
     ~ update in-place
   
   Terraform will perform the following actions:
   
     # tencentcloud_vpc.foo will be updated in-place
     ~ resource "tencentcloud_vpc" "foo" {
           id                     = "vpc-jhmdf9q9"
         ~ name                   = "ci-temp-test-updated" -> "ci-temp-test-updated2"
           tags                   = {
               "test" = "test"
           }
           # (6 unchanged attributes hidden)
       }
   
   Plan: 0 to add, 1 to change, 0 to destroy.
   
   Do you want to perform these actions?
     Terraform will perform the actions described above.
     Only 'yes' will be accepted to approve.
   
     Enter a value: yes
   
   tencentcloud_vpc.foo: Modifying... [id=vpc-jhmdf9q9]
   tencentcloud_vpc.foo: Modifications complete after 1s [id=vpc-jhmdf9q9]
   
   Apply complete! Resources: 0 added, 1 changed, 0 destroyed.
   ```
8. 您可根据实际需求，执行以下命令销毁资源。

   ``` html
   terraform destroy
   ```

   返回信息如下所示：

   ``` bash
   ➜  terraform_workspace terraform destroy
   tencentcloud_vpc.foo: Refreshing state... [id=vpc-07mx4yfd]
   
   Terraform used the selected providers to generate the following execution plan. Resource actions are
   indicated with the following symbols:
     - destroy
   
   Terraform will perform the following actions:
   
     # tencentcloud_vpc.foo will be destroyed
     - resource "tencentcloud_vpc" "foo" {
         - cidr_block             = "10.0.0.0/16" -> null
         - create_time            = "2021-12-15 16:20:32" -> null
         - default_route_table_id = "rtb-4m1nmo0e" -> null
         - dns_servers            = [
             - "119.29.29.29",
             - "8.8.8.8",
           ] -> null
         - id                     = "vpc-07mx4yfd" -> null
         - is_default             = false -> null
         - is_multicast           = false -> null
         - name                   = "ci-temp-test-updated" -> null
         - tags                   = {
             - "test" = "test"
           } -> null
       }
   
   Plan: 0 to add, 0 to change, 1 to destroy.
   
   Do you really want to destroy all resources?
     Terraform will destroy all your managed infrastructure, as shown above.
     There is no undo. Only 'yes' will be accepted to confirm.
   
     Enter a value: yes
   
   tencentcloud_vpc.foo: Destroying... [id=vpc-07mx4yfd]
   tencentcloud_vpc.foo: Destruction complete after 7s
   
   Destroy complete! Resources: 1 destroyed.
   ```

