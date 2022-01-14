
Terraform relies on provider plugins to interact with cloud providers, SaaS providers, and other APIs. Terraform configurations must declare which providers they require so that Terraform can install and use them. Additionally, some providers require configuration before they can be used. This document describes how to configure provider plugins.


## Searching for Provider
Go to the [Providers](https://registry.terraform.io/browse/providers) page, search, and enter the [TencentCloud Provider](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest) page to view the user guide as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9bb034daa2cfde36c489232369db308a.png)

## Downloading Provider
Run the following command to download the latest plugin version from Terraform's official repository by default.
```bash
terraform init
```
If you need to use a legacy version, you can specify the version information with the `version` argument as shown below:
```bash
terraform {
  required_providers {
    tencentcloud = {
      source = "tencentcloudstack/tencentcloud"
      # Specify the version by `version`
      version = "1.60.18"
    }
  }
}
```

## Provider Declaration
```
provider "tencentcloud" {
  region = "ap-guangzhou"
  secret_id = "my-secret-id"
  secret_key = "my-secret-key"
}
```
