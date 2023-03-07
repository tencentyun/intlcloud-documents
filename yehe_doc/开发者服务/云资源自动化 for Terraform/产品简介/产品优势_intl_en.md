## Infrastructure as code (IaC)

Leverage Terraform HCL declarative syntax to manage your infrastructure resources with code and versioning. This improves the efficiency of automated deployment and O&M while reducing the costs of management and configuration.

## Cloud state management

Terraform introduces the concept of backend, a remote state storage mechanism. Currently, Tencent Cloud can manage your .tfstate files through [COS](https://www.tencentcloud.com/document/product/436) to avoid storing files locally and causing file losses. In addition, remote storage provides a basis for multiple users to manage Terraform resources concurrently.

## Template

Choose from a wealth of Tencent Cloud for [Terraform modules](https://registry.terraform.io/search/modules?q=terraform-tencentcloud-modules). You only need to configure module input parameters, without caring about details like resource definitions, parameters, and syntax in modules. In this way, you can focus more on architecture design and resource relationship integration.

## Existing resource management

Use the compatible [Terraformer](https://github.com/GoogleCloudPlatform/terraformer.git) to quickly import existing Tencent Cloud resources and generate .tf or .tfstate files, which effectively reduces the costs of cloud resource management and migration.