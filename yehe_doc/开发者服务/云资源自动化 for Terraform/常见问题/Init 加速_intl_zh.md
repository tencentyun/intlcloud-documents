## 现象描述

下载或更新 Provider 出现如下报错信息：
``` bash
Initializing the backend...

Initializing provider plugins...
- Finding latest version of tencentcloudstack/tencentcloud...
╷
│ Error: Failed to install provider
│ 
│ Error while installing tencentcloudstack/tencentcloud v1.78.5: could not query provider registry for registry.terraform.io/tencentcloudstack/tencentcloud: failed to retrieve authentication checksums for provider: the request failed after 2 attempts, please try again later: Get
│ "https://github.com/tencentcloudstack/terraform-provider-tencentcloud/releases/download/v1.78.5/terraform-provider-tencentcloud_1.78.5_SHA256SUMS": context deadline exceeded
╵
```

或者下载很慢：
``` bash
Initializing the backend...

Initializing provider plugins...
- Finding latest version of tencentcloudstack/tencentcloud...
╷
│ Error: Failed to query available provider packages
│ 
│ Could not retrieve the list of available versions for provider tencentcloudstack/tencentcloud: could not connect to registry.terraform.io: Failed to request discovery document: Get "https://registry.terraform.io/.well-known/terraform.json": net/http: request canceled while waiting for connection
│ (Client.Timeout exceeded while awaiting headers)
╵
```

## 问题定位

Terraform 的默认镜像源 `registry.terraform.io` 部署在国外，在国内拉取镜像时可能存在网络问题导致拉取速度慢、甚至无法成功拉取。为解决此问题，您可以使用腾讯云提供的 [镜像源](https://www.tencentcloud.com/document/product/1172/52391)。

## 操作步骤

### 创建 Terraform CLI 配置文件

按需创建 `.terraformrc` 或 `terraform.rc` 配置文件，您可以将其与其他配置文件放在一个文件夹内，位置取决于主机操作系统：
- **在 Windows 上**，该文件必须命名 `terraform.rc`，并放置在相关用户的 `%APPDATA%` 目录中。该目录的物理位置取决于您的 Windows 版本和系统配置；可以在 PowerShell 中使用 `$env:APPDATA` 查找其在系统上的位置。

- **在所有其他系统上**，文件必须命名 `.terraformrc`，并直接放在相关用户的根目录中。Terraform CLI  配置文件的位置也可以使用 `TF_CLI_CONFIG_FILE` 环境变量来指定。任何此类文件都应遵循命名模式 `*.tfrc`，详情见 [Terraform 官网指引](https://developer.hashicorp.com/terraform/cli/config/config-file)。


   以 MacOS 为例，创建 `.terraformrc` 文件在用户根目录下，内容如下：

   ``` bash
   provider_installation {
       network_mirror {
           url = "https://mirrors.tencent.com/terraform/"
       }
   }
   ```

### 运行 terraform init

在您保存 Terraform 配置文件的目录下，执行 `terraform init` 命令初始化配置。

此步骤中，Terraform 会自动检测配置文件中的 provider 字段，并下载最新版本的模块和插件。若打印如下信息，则表示初始化成功。
``` shell
Initializing the backend...

Initializing provider plugins...
- Finding latest version of tencentcloudstack/tencentcloud...
- Installing tencentcloudstack/tencentcloud v1.78.5...
- Installed tencentcloudstack/tencentcloud v1.78.5 (verified checksum)

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
│ The current .terraform.lock.hcl file only includes checksums for darwin_amd64, so Terraform running on another platform will fail to install these providers.
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

