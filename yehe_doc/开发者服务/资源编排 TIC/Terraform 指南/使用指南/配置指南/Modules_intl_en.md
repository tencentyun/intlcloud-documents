
A module is a folder containing a set of Terraform code, which is an abstraction and encapsulation of multiple resources.


## Calling Module
Modules are referenced in Terraform code using a `module` block, which contains the `module` keyword, `module` name, and `module` body (the part within the `{}`) as shown below:
```bash
module "servers" {
  source = "./app-cluster"

  servers = 5
}
```
A `module` can be called using the following arguments:
- `source`: specifies the source of the referenced module.
- `version`: specifies the version number of the referenced module.
- `meta-arguments`: is a feature supported since Terraform 0.13. Similar to `resource` and `data`, it can be used to manipulate the behaviors of `module`.


## Argument Description

### Source


The `source` argument tells Terraform where to find the source code for the desired child module. Terraform uses this during the module installation step of `terraform init` to download the source code to a directory on local disk so that it can be used by other Terraform commands.

The module can be installed from the following source types:
- Local paths
- Terraform Registry
- GitHub
- Bitbucket
- Generic Git, Mercurial repositories
- HTTP URLs
- S3 buckets
- GCS buckets
- Modules in Package Sub-directories

This document describes installation from local path, Terraform Registry, and GitHub.

#### Local path
Local paths can use child modules from the same project. Unlike other resources, local paths do not require the download of relevant code. For example:
```bash
module "consul" {
  source = "./consul"
}
```

#### Terraform Registry
Terraform Registry is currently the module repository solution recommended by Terraform. It uses Terraform's custom protocol and supports version management and module use. [Terraform Registry](https://registry.terraform.io/) hosts and indexes a large number of public modules, allowing quick search for a variety of official and community-supplied quality modules.

Modules in Terraform Registry can be referenced with source addresses in the format of `<NAMESPACE>/<NAME>/<PROVIDER>`. You can get the exact source address in the module description. For example:
```bash
module "consul" {
  source = "hashicorp/consul/xxx"
  version = "0.1.0"
}
```
For modules hosted in other repositories, you can add `<HOSTNAME>/` to the source address header to specify the server name of the private repository. For example:
```bash
module "consul" {
  source = "app.terraform.io/example-corp/k8s-cluster/azurerm"
  version = "1.1.0"
}
```

#### GitHub
If Terraform reads a source argument value prefixed with `github.com`, it will automatically recognize it as a GitHub source. For example, you can clone a repository using the HTTPS protocol:
```bash
module "consul" {
  source = "github.com/hashicorp/example"
}
```
To use the SSH protocol, use the following address:
```bash
module "consul" {
  source = "git@github.com:hashicorp/example.git"
}
```

<dx-alert infotype="explain" title="">
The GitHub source is handled in the same way as generic Git repositories, as both of them get Git credentials and reference specific versions through the `ref` argument in the same way. If you want to access private repositories, you need to configure additional Git credentials.
</dx-alert>


### Version
When a registry is used as a module source, you can use the `version` meta-argument to constrain the version of the module used. For example:
```bash
module "consul" {
  source  = "hashicorp/consul/xxx"
  version = "0.0.5"

  servers = 3
}
```
The format of the `version` meta-argument is in line with the provider version constraint. In this case, Terraform will use the latest version of the module instance that has been installed. If no compliant version is currently installed, the latest compliant version will be downloaded.

The `version` meta-argument can only be used with the registry to support public or private module repositories. Other types of module sources, such as local path, do not necessarily support versioning.
