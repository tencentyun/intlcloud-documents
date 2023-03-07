腾讯云 Cloud Shell 是一款帮助您运维的免费产品，预装了 Terraform 相关组件，并配置好腾讯云临时凭证（credentials）。因此您可直接在 Cloud Shell 中运行 Terraform 命令。参考以下操作，可以在 Cloud Shell 中快速创建 [腾讯云 VPC](https://www.tencentcloud.com/products/vpc) 资源。

## 访问 Cloud Shell

登录 [腾讯云控制台](https://console.cloud.tencent.com/)，选择页面上方的工具 > CloudShell，即可启动 CloudShell。

## 编写 main.tf 文件

您可以使用 vim 命令编写 main.tf 文件。
``` atom
terraform {
  required_providers {
    tencentcloud = {
      source = "tencentcloudstack/tencentcloud"
    }
  }
}

provider "tencentcloud" {
  region = "ap-guangzhou"
}

resource "tencentcloud_vpc" "test-vpc" {
  name         = "demo-vpc"
  cidr_block   = "10.0.10.0/24"
  dns_servers  = ["119.29.29.29", "8.8.8.8"]
  is_multicast = false
  tags         = {
    "createdBy" = "terraform",
  }
}
```

## 初始化 Provider

命令行执行 `terraform init --upgrade` 命令，下载最新版本腾讯云 Provider 插件。
``` bash
[cloudshell@TencentCloudshell ~/data/vpc]$ terraform init --upgrade

Initializing the backend...

Initializing provider plugins...
- Finding latest version of tencentcloudstack/tencentcloud...
- Installing tencentcloudstack/tencentcloud v1.78.9...
- Installed tencentcloudstack/tencentcloud v1.78.9 (verified checksum)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

╷
│ Warning: Incomplete lock file information for providers
│ 
│ Due to your customized provider installation methods, Terraform was forced to calculate lock file checksums locally for the following providers:
│   - tencentcloudstack/tencentcloud
│ 
│ The current .terraform.lock.hcl file only includes checksums for linux_amd64, so Terraform running on another platform will fail to install these providers.
│ 
│ To calculate additional checksums for another platform, run:
│   terraform providers lock -platform=linux_amd64
│ (where linux_amd64 is the platform to generate)
╵

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

## 运行 terraform plan

命令行执行 `terraform plan` 命令，生成执行计划。
``` bash
[cloudshell@TencentCloudshell ~/data/vpc]$ terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # tencentcloud_vpc.test-vpc will be created
  + resource "tencentcloud_vpc" "test-vpc" {
      + assistant_cidrs        = (known after apply)
      + cidr_block             = "10.0.10.0/24"
      + create_time            = (known after apply)
      + default_route_table_id = (known after apply)
      + dns_servers            = [
          + "119.29.29.29",
          + "8.8.8.8",
        ]
      + docker_assistant_cidrs = (known after apply)
      + id                     = (known after apply)
      + is_default             = (known after apply)
      + is_multicast           = false
      + name                   = "tf-ci-test-vpc"
      + tags                   = {
          + "createdBy" = "terraform"
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.

───────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

## 运行 terraform apply

命令行执行 `terraform apply --auto-approve ` 命令，创建资源。
``` bash
[cloudshell@TencentCloudshell ~/data/vpc]$ terraform apply --auto-approve

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # tencentcloud_vpc.test-vpc will be created
  + resource "tencentcloud_vpc" "test-vpc" {
      + assistant_cidrs        = (known after apply)
      + cidr_block             = "10.0.10.0/24"
      + create_time            = (known after apply)
      + default_route_table_id = (known after apply)
      + dns_servers            = [
          + "119.29.29.29",
          + "8.8.8.8",
        ]
      + docker_assistant_cidrs = (known after apply)
      + id                     = (known after apply)
      + is_default             = (known after apply)
      + is_multicast           = false
      + name                   = "tf-ci-test-vpc"
      + tags                   = {
          + "createdBy" = "terraform"
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.
tencentcloud_vpc.test-vpc: Creating...
tencentcloud_vpc.test-vpc: Creation complete after 4s [id=vpc-5jr1hibn]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

## 控制台查看

登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)，查看已创建的实例。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/fNJv122_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221221165427.png)

## 运行 terraform destroy

命令行执行 `terraform destroy --auto-approve ` 命令，销毁资源。
``` bash
[cloudshell@TencentCloudshell ~/data/vpc]$ terraform destroy --auto-approve
tencentcloud_vpc.test-vpc: Refreshing state... [id=vpc-5jr1hibn]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # tencentcloud_vpc.test-vpc will be destroyed
  - resource "tencentcloud_vpc" "test-vpc" {
      - assistant_cidrs        = [] -> null
      - cidr_block             = "10.0.10.0/24" -> null
      - create_time            = "2022-11-10 16:16:36" -> null
      - default_route_table_id = "rtb-0oiqq8mc" -> null
      - dns_servers            = [
          - "119.29.29.29",
          - "8.8.8.8",
        ] -> null
      - docker_assistant_cidrs = [] -> null
      - id                     = "vpc-5jr1hibn" -> null
      - is_default             = false -> null
      - is_multicast           = false -> null
      - name                   = "tf-ci-test-vpc" -> null
      - tags                   = {
          - "createdBy" = "terraform"
        } -> null
    }

Plan: 0 to add, 0 to change, 1 to destroy.
tencentcloud_vpc.test-vpc: Destroying... [id=vpc-5jr1hibn]
tencentcloud_vpc.test-vpc: Destruction complete after 4s

Destroy complete! Resources: 1 destroyed.
```

