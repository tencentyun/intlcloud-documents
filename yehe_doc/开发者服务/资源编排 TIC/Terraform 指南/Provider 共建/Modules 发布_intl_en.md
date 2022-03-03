## Overview

Modules are Terraform configurations that allow you to manage a group of resources and can provide better business abstraction and lower costs in some multi-resource scenarios. In addition, you can publish modules on GitHub to the [Terraform registry](https://registry.terraform.io/). This document describes how to create and publish a Terraform TencentCloud module.

## Creating a Public Module

Create a code repository on GitHub and name it in the format of `terraform-<PROVIDER>-<NAME>`, such as [terraform-tencentcloud-vpc](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-vpc).

A basic module contains the following files:

```
.
├── main.tf # Write module resources
├── variables.tf # Declare module variables
├── outputs.tf # Declare module outputs
├── LICENCE # Declare license
└── README.md # Readme

```

You are advised to add the `examples` directory to store the examples for importing and using the module. For more information, [visit](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-vpc/tree/master/examples).

## Publishing a Module

### Directions

* Visit [registry.terraform.io](https://registry.terraform.io/) and select **Publish** > **Module** in the top right.

![](https://qcloudimg.tencent-cloud.cn/raw/3413bcf31b0f1d22517cee72bf535bea.png)

* Click the drop-down arrow for **Select Repository on GitHub** to view the module repositories you are authorized to manage. Then, select a repository and click **PUBLISH MODULE**.
![](https://qcloudimg.tencent-cloud.cn/raw/b7dcc4ce6be947cff50762fd8bfc32b7.png)
![](https://qcloudimg.tencent-cloud.cn/raw/cd927fe3533319ac0524b50686f9ed02.png)


* Your repository will be automatically synchronized to the Terraform registry in a few minutes.
![](https://qcloudimg.tencent-cloud.cn/raw/08788ec56f75d1fa1befa64780def469.png)


Note: You can also publish a module through a personal GitHub repository. The modules whose repositories are named in the format of `terraform-tencentcloud-<NAME>` will also be included in the tencentcloud modules.
