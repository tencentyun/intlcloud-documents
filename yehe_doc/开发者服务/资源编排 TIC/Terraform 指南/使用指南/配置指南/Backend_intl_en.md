## Remote State Storage Mechanism
Storing state files locally only may cause the following issues:
 - A `tfstate` file is stored locally in the current working directory by default. If computer damage causes file loss, all the resources corresponding to the `tfstate` file will become unmanageable, leading to a resource leak.
 - A `tfstate` file cannot be shared among group members.


To facilitate the storage and sharing of state files, Terraform introduces the remote state storage mechanism called "backend", an abstract remote storage API. Similar to a provider, backend supports a variety of remote storage services as described in [Available Backends](https://www.terraform.io/language/settings/backends/local). A Terraform backend has two modes:
- **Standard**: supports remote state storage and state lock.
- **Enhanced**: supports remote operations (such as `plan` and `apply` on a remote server) in addition to the standard features.

## Notes
- After the backend configuration is updated, you need to run `terraform init` to verify and configure the backend.
- If no custom backend is configured, Terraform will use the local backend by default. For example, a `tfstate` file is stored in the local directory by default.
- Backend configuration is subject to the following restraints:
 - One configuration file provides only one backend block.
 - Backend blocks cannot reference named values (such as input variables, local variables, or data source attributes).

## Using Backend
The definition of a `backend` block is nested in a top-level Terraform block. This document uses the Tencent Cloud Object Storage (COS) service as an example for configuration. For more information on other storage modes, see [Available Backends](https://www.terraform.io/language/settings/backends/local).
```bash
terraform {
  backend "cos" {
    region = "ap-nanjing"
    bucket = "tfstate-cos-1309190246"
    prefix = "terraform/state"
  }
}
```
If you have the `tfstate-cos-1309190246` bucket in COS, the Terraform state information will be written into the `terraform/state/terraform.tfstate` file as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/fb65de33be4abf481b6d6efd0d67597c.png)

 
