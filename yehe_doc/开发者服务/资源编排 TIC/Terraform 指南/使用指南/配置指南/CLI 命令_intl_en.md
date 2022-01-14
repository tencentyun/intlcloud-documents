This document describes how to apply Terraform code and manage the infrastructure with the Terraform command-line interface (CLI).


## Basic Features

### Viewing command list
Terraform provides diversified command-line operations. You can enter `terraform` on the command line to see the complete list as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/5f54e51ba06d4a64625c2270bd160e82.jpg)
You can use `-help` to view the detailed usage of specific subcommands. For example, you can run the `terraform validate -help` command to view the usage of the `validate` subcommand.

### Switching working directory
The usual way to run Terraform is to first switch to the directory containing the .tf files for your root module (using the cd command), so that Terraform will automatically find those code files and argument files to be executed.

#### Global option -chdir
In some cases, particularly when wrapping Terraform in automation scripts, it can be convenient to run Terraform from a different directory than the root module directory. To allow that, Terraform supports a global option `-chdir=...` which you can include before the name of the subcommand you intend to run:
```
terraform -chdir=environments/production apply
```
The `-chdir` option instructs Terraform to change its working directory to the given directory before running the given subcommand. This means that any files that Terraform would normally read or write in the current working directory will be read or written in the given directory instead.
There are two exceptions where Terraform will use the original working directory even when you specify `-chdir`:
- Settings in the CLI Configuration are not for a specific subcommand and Terraform processes them before acting on the `-chdir` option.
- In case you need to use files from the original working directory as part of your configuration, a reference to `path.cwd` in the configuration will produce the original working directory instead of the overridden working directory. Use `path.root` to get the root module directory.


### Auto-Completion
If `bash` or `zsh` is used, you can get the support for auto-completion with the following command.
```
terraform -install-autocomplete
```
You can run the following command to uninstall auto-completion.
```
terraform -uninstall-autocomplete
```

## Basic Commands

<dx-accordion>
::: terraform init
The `terraform init` command is used to initialize a working directory containing Terraform configuration files. You should run this command first after writing Terraform code or cloning a Terraform project.

- **Usage**
`terraform init [options]`
This command initializes the current directory in a series of steps. It is always safe to run multiple times and will not delete configuration files or state information even if an error is reported.
- **General options**
 - `-input=true`: whether to ask for input in case no input variable value is obtained.
 - `-lock=false`: whether to lock a state file at runtime.
 - `-lock-timeout=\`: timeout period for trying to get a state file lock. The default value is 0, indicating that an error will be reported as soon as the lock is found to have been held by another process.
 - `-no-color`: disables color codes in the command output.
 - `-upgrade`: whether to upgrade module code and plugins.
- **Source module copying**
By default, the `terraform init` command assumes that the working directory already contains a configuration and will attempt to initialize that configuration. You can also run `terraform init` in an empty working directory with the `-from-module=MODULE-SOURCE` option, in which case the specified module will be copied into the current directory before any other initialization steps are run. This special mode of operation supports two use cases:
 - Checking out the specified code version and initializing the working directory for it if the version control system corresponds to the source.
 - Copying the sample code into a local directory to write new code accordingly if the module source points to an example project.
For regular running operations, we recommend you check out the code from the version control system separately using the version control system's tool.
- **Backend initialization**
During initialization, the root module code will be parsed to find the backend configuration, and the backend storage will be initialized with the given configuration settings.
Re-running `init` with an already-initialized backend will update the working directory to use the new backend settings. The `init` command may prompt you for confirmation of state migration based on the changes. You can use the following options as needed:
 - `-force-copy`: skips the prompt to confirm the migration state directly.
 - `-reconfigure`: makes `init` ignore any existing configuration to prevent any state migration.
 - `-backend=false`: skips the backend configuration.
 Note that some initialization steps require an already initialized backend, and we recommend you use this option only after the backend has been initialized.
 - `-backend-config`: dynamically specifies the backend configuration.
- **Child module initialization**
The `init` command will search for `module` blocks and get the module code with the `source` argument. You can use the following options as needed:
 - `-upgrade`: upgrades all modules to the latest code version. By default, re-running the `init` command after module installation will continue to install the modules added after the last `init` execution, but will not modify the already installed modules.
 - `-get=false`: skips child module installation steps.
 Note that other initialization steps require a complete module tree, and we recommend you use this option only after the module has been successfully installed.
- **Plugin installation**
The options are described as follows:
 - `-upgrade`: upgrades all previously installed plugins to the latest version in line with the version constraint. This option is invalid for manually installed plugins.
 - `-get-plugins=false`: skips plugin installation. Terraform will use plugins already installed in the current working directory or the plugin cache path. If these plugins are not sufficient to meet the requirements, `init` will fail.
 - `-plugin-dir=PATH`: skips plugin installation and loads plugins only from a specified directory. This option will skip plugins in the user plugin directory and all the current working directories. To restore the default behavior after this option is used, re-run `init` with the `-plugin-dir=""` options.
 - `-verify-plugins=false`: (not recommended) skips signature verification after plugin downloading (Terraform does not verify signatures of manually installed plugins). Official plugins are signed by HashiCorp and verified by Terraform.


:::
::: terraform plan
The `terraform plan` command is used to create a change plan. Terraform will first run a refresh (this behavior can also be disabled explicitly):
 - If changes are detected, you can decide which change to be executed in order to migrate the existing state to the desired state as described by the code. You can also use the optional `-out` option to save the change plan in a file for execution later using the `terraform apply` command.
 - If no change is detected, you will be prompted that there is no change to be executed.

This command makes it easy to review all the details of a state migration without actually changing the existing resources and state files. For example, you can run `terraform plan` before committing the code to the version control system to confirm that the changes behave as expected.
 
- **Usage**
`terraform plan [options]`
By default, the plan command does not require options. It runs a refresh using the code and state files in the current working directory.
- **General options**:
 - `-compact-warnings`: displays alarms only with a message summary if Terraform generates only alarm information but no error information.
 - `-destroy`: generates a plan to terminate all resources.
 - `-detailed-exitcode`: details the meanings of the code returned upon command exit:
   - 0 = successful empty plan (no change)
   - 1 = error
   - 2 = successful non-empty plan (with changes)
 - `-input=true`: whether to ask you to specify the input variable value in case no value is obtained.
 - `-lock=true`: similar to that of the `apply` command.
 - `-lock-timeout=0s`: similar to that of the `apply` command.
 - `-no-color`: disables color output.
 - `-out=path`: saves the change plan to a file in the specified path for execution using `terraform apply`.
 - `-parallelism-n`: limits the maximum parallelism of the Terraform traversing graph, with a default value of 10.
 - `-refresh=true`: executes a refresh before calculating changes.
 - `-state=path`: location of a state file, with a default value of `"terraform.tfstate"`. This option is invalid if remote backend is enabled.
 - `-target=resource`: address of the target resource. This option can be declared repeatedly to perform partial updates to the infrastructure.
 - `-var 'foo=bar'`: similar to that of the `apply` command.
 - `-var-file=foo`: similar to that of the `apply` command.
- **Partial update**
Using the `-target` option allows Terraform to focus on a subset of resources, which can be marked with a resource address as described below:
 - If a resource can be located at a given address, only the resource will be marked. If the resource uses the `count` argument without a given access subscript, all instances of the resource will be marked.
 - If a module is located at a given address, all resources in the module and its embedded module resources will be marked.
<dx-alert infotype="explain" title="">
Particular special scenarios, such as recovery from a previous error or bypassing certain Terraform design constraints, require the capability to mark partial resources and calculate update plans. The `-target` option is not recommended for routine operations, as it can cause undetectable configuration drift and make it impossible to deduce the current actual state from the code.
</dx-alert>
- **Security alarm**
Change plan files saved (using the `-out` option) may contain sensitive information. We strongly recommend you encrypt the files by yourself for movement or save as Terraform does not encrypt them. Terraform is expected to launch new features to enhance the security of plan files.


:::
::: terraform apply
As the most important command in Terraform, `terraform apply` is used to generate and (optionally) run an execution plan so that the infrastructure resource state matches the code description.

- **Usage**
`terraform apply [options] [dir-or-plan]`
By default, the `apply` command scans the current directory for code files and performs changes accordingly. Other code file directories can also be specified through options.
When designing an automation pipeline, you can also explicitly divide the process into two steps: creating an execution plan and running the plan with the `apply` command. If no change plan file is explicitly specified, `terraform apply` will automatically create a change plan and ask you whether to approve the execution. If the created plan does not contain any changes, `terraform apply` will exit immediately without prompting you for input.

- **General options**
 - `-backup-path`: path to save a backup file, with a default value of the `-state-out` option plus the `".backup"` suffix. You can set it to "-" to disable backup (not recommended).
 - `-compact-warnings`: displays alarms only with a message summary if Terraform generates only alarm information but no error information.
 - `-lock=true`: whether to lock a state file first before execution.
 - `-lock-timeout=0s`: interval to attempt to get a state lock again.
 - `-input=true`: whether to prompt you for input in case no input variable value is obtained.
 - `-auto-approve`: skips interactive confirmation and runs changes directly.
 - `-no-color`: disables color output.
 - `-parallelism=n`: limits the maximum parallelism of the Terraform traversing graph, with a default value of 10.
 - `-refresh=true`: whether to query the current state of the recorded infrastructure object to refresh the state file first before specifying and running a change plan. This option is invalid if the command line specifies the change plan file to be executed.
 - `-state=path`: path to save a state file, with a default value of `"terraform.tfstate"`. This option is invalid if a remote backend is used. It does not affect other commands; for example, the state file it sets will not be found when `init` is executed. If you want all commands to use the same location-specific state file, use a local backend.
 - `-state-out=path`: path to write an updated state file, with a default value of `-state`. This option is invalid if a remote backend is used.
 - `-target=resource`: specifies to update target resources by specifying resource addresses.
 - `-var 'foo=bar'`: sets the value of a set of input variables. This option can be set repeatedly to pass in multiple input variable values.
 - `-var-file=foo`: specifies an input variable file.


:::
::: terraform destroy
The `terraform destroy` command can be used to terminate and repossess all the Terraform-managed infrastructure resources.

#### **Usage**
`terraform destroy [options]`
Before Terraform-managed resources are terminated, you will be asked for confirmation on an interactive UI. This command can accept all options of the `apply` command, but cannot specify a plan file.
 - If the `-auto-approve` option is `true`, resources will be terminated without your confirmation.
 - If a resource is specified with the `-target` option, the resource will be terminated along with all the resources that depend on it.

<dx-alert infotype="explain" title="">
All the operations to be performed by `terraform destroy` can be previewed at any time by running the `terraform plan -destroy` command.
</dx-alert>


:::
::: terraform graph
The `terraform graph` command is used to generate a visual graph of the infrastructure of the code description or the execution plan. Its output is in DOT format and can be converted to an image using GraphViz.

- **Usage**
`terraform graph [options] [DIR]`
This command generates a visual dependency graph of Terraform resources as described by the code lock in the DIR path (the current working directory is used if the default DIR option is used).
- **General options**
 - `-type`: specifies the type of diagram to be output. Terraform creates different graphs for different operations. The default type of the code file is `"plan"`, and that of the change plan file is `"apply"`.
 - `-draw-cycles`: highlights the rings in the graph with colored edges to help analyze ring errors in the code (Terraform prohibits ring dependencies).
 - `-type=plan`: generates different types of diagrams, including `plan`, `plan-destroy`, `apply`, `validate`, `input`, and `refresh`.
- **Image file creation**
The `terraform graph` command outputs data in DOT format, which can be converted to an image file with the following command on GraphViz:
```
terraform graph | dot -Tsvg > graph.svg
```
If Graphviz is not installed, you can install it with the following command:
 - CentOS: `yum install graphviz`
 - Windows: `choco install graphviz`
 - macOS: `brew install graphviz`
The output image is similar to the one as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/dfa0f17c2481d3ac81b94433af3a64af.png)

:::
::: terraform show
The `terraform show` command prints readable output from a state file or change plan file, which can be used to check the change plan to ensure that all operations are as expected, or to review the current state file.

<dx-alert infotype="notice" title="">
Machine-Readable JSON data can be output by adding the `-json` option, but all the data marked as `sensitive` will be output in plaintext.
</dx-alert>

-  **Usage**
`terraform show [options] [path]`
- **General options**
 - `path`: specifies a state file or change plan file. If no path is given, the state file corresponding to the current working directory will be used.
 - `-no-color`: similar to that of the `apply` command.
 - `-json`: outputs in JSON format.
- **Output in JSON Format**
The state information can be printed in JSON format using the `terraform show -json` command. If a change plan file is specified, `terraform show -json` will record the change plan, configuration, and current state in JSON format.

:::
::: terraform import
The `terraform import` command is used to import an existing resource object into Terraform.

If there exists a set of running infrastructure resources that are not built or managed using Terraform and corresponding Terraform code has been written for them, you can use `terraform import` to "import" the resource objects into the Terraform state file.

- **Usage**
`terraform import [options] ADDRESS ID`
`terraform import` finds the corresponding resource based on its resource ID (subject to the type of the imported resource object) and imports its information to the resource corresponding to `ADDRESS` in the state file. `ADDRESS` must be in the valid resource address format as described in the resource address. `terraform import` can import resources into not only root modules but also child modules.
<dx-alert infotype="notice" title="">
Each resource object in Terraform corresponds to only one actual infrastructure object. You need to avoid importing the same object to two and more addresses, which can lead to unpredictable behaviors in Terraform.
</dx-alert>
- **General options**
 - `-backup=path`: address of the generated state backup file, with a default value of the `-state-out` path plus the `".backup"` suffix. You can set it to "-" to disable backup (not recommended).
 - `-config=path`: path to the folder containing the Terraform code with the import target. The default path is the current working directory.
 - `-input=true`: whether to allow prompting for the input of provider configuration information.
 - `-lock=true`: whether to lock a state file with backend support.
 - `-lock-timeout=0s`: interval to attempt to get a state lock again.
 - `-no-color`: disables color output.
 - `-parallelism=n`: limits the maximum parallelism of the Terraform traversing graph, with a default value of 10.
 - `-state=path`: address of the state file to be read. The default address is the configured backend storage address or the `"terraform.tfstate"` file.
 - `-state-out=path`: specifies the path to save a modified state file. By default, the source state file is overwritten. This option can be used to create a state file while avoiding corrupting the existing one.
 - `-var 'foo=bar'`: sets the input variable value on the command line.
 - `-var-file=foo`: similar to that of the `apply` command.
- **Provider configuration**
Terraform will try to read the configuration information of the provider corresponding to the resource to be imported. If no relevant provider configuration is found, Terraform will ask you to input relevant access credentials. You can either input credentials or configure them through environment variables.
The only restriction to read provider configuration in Terraform is that the configuration cannot rely on the input of "non-input variables", such as data sources.
If you need to import Tencent Cloud resources, Terraform will use the `secret_id` and `secret_key` input variables to configure TencentCloud Provider. The configuration files are as follows:
```
variable "secret_id" {}
variable "secret_key" {}

provider "tencentcloud" {
      secret_id = var.secret_id
      secret_key = var.secret_key
    }
```
Upon the completion of configuration, you can import resources by running a command similar to the following:
```
terraform import tencentcloud_instance.foo ins-2s6ewubw
```


:::
</dx-accordion>






