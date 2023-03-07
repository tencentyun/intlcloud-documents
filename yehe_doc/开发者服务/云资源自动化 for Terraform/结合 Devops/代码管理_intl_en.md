## Concepts

### GitOps

GitOps is a method of continuous delivery proposed by Weaveworks. Its core idea is having a Git version repository that stores declarative infrastructure and applications of application systems. With Git at the center of the delivery workflow, you can submit pull requests and use Git to accelerate and simplify the deployment and Ops of Terraform applications. With such a simple tool like Git, you can focus more on feature creation rather than Ops tasks such as application system installation, configuration, and migration.

### Terraform root module

The root configuration (root module) is the working directory running Terraform CLI.

#### The criteria of a root module:
- **Minimize the number of resources in each root module**


   Avoid configuring too many resources in a root directory and storing too many resources in a directory or state. Every time Terraform is run, all the resources in the specified root directories will be refreshed. If a state contains too many resources, the execution may be slow. In general, a state should contain up to 100 resources (up to a dozen of resources at best).

- **Use different directories for different applications**


   To manage applications and projects separately, put their resources in their own Terraform directories. A service can be a certain application or general service, for example, a shared network. You should nest all the Terraform code of a certain service in a directory (including sub-directories).


## Project Structure

Split the Terraform configuration of the service into two top-level directories: **`modules` directory** containing the actual service configuration; **`environments` directory** containing the root configuration of each environment.
- The `modules` directory contains abstracted and reusable modules.

- The `environments` directory isolates different environments, which allows for using providers for different cloud vendors and configuring different accounts for multi-cloud management (the `prod` directory isolates businesses by `workspace`).


   Below is the recommended project structure. For more information, see the code repositories of [CODING](https://tencentiac.coding.net/p/terraform/d/gitops-terraform/git) and [GitHub](https://github.com/tongyiming/gitops-terraform).

   ``` bash
   .
   ├── README.md
   ├── environments
   │   ├── dev
   │   │   ├── main.tf
   │   │   └── provider.tf
   │   └── prod
   │       ├── cicd
   │       │   └── main.tf
   │       ├── local.tf
   │       ├── main.tf
   │       ├── provider.tf
   │       └── qta
   │           └── main.tf
   └── modules
     ├── network
     │   ├── main.tf
     │   ├── outputs.tf
     │   ├── provider.tf
     │   └── variables.tf
     ├── security_group
     │   ├── main.tf
     │   ├── outputs.tf
     │   ├── provider.tf
     │   └── variables.tf
     └── tke
         ├── main.tf
         ├── outputs.tf
         ├── provider.tf
         └── variables.tf
   ```

## Code Reuse

To reuse code, we recommend you use [Terraform modules](https://developer.hashicorp.com/terraform/language/modules). You can use custom or provided modules, such as [Tencent Cloud modules](https://github.com/terraform-tencentcloud-modules/). The `Modules` directory of the project encapsulates module templates. Resources are categorized, and resources of the same category are managed in the same directory. Target resources are managed in a template so as to connect target and dependent resources, for example, the TKE template and its dependent template of `Network` resources.

## Building a Secure Terraform Update Process

Secure infrastructure relies on a stable and secure Terraform update process.

#### Planning before execution

Always generate a plan first for Terraform executions and save it in the output file. Execute the plan after gaining the approval of the infrastructure owner. Even when you design the prototype for a change locally, you should generate a plan and view the resources to be added, modified, and terminated in an application.

#### Implementing an automated workflow

Execute Terraform via an automated tool to ensure execution context consistency and avoid human errors.

#### Avoiding importing existing resources
- Avoid importing existing resources (through `terraform import`), as this may make it hard to understand the source and configuration of a manually created resource. Instead, create and delete resources in Terraform.

- In cases where deleting old resources would create significant toil, use the `terraform import` command with explicit approval. Resources imported to Terraform can be managed only by Terraform.


#### Avoiding modifying the Terraform state

If you use Terraform to manage the infrastructure and manually update resource attributes in the console, the Terraform execution plan may turn out unexpected. To modify the Terraform state information, run the `terraform state` command.

#### Versioning

Similar to other code forms, infrastructure code can be stored in the versioning system to retain records and allow for easy rollback.

## Environment Isolation

The following isolation methods are supported:

#### Isolation by directory

Group resources by directory and configure root modules in sub-directories for isolation (as adopted in this document).

Note: In `environments`, the `dev` and `prod` directories use different root modules to isolate the infrastructure configurations of different environments.

#### Isolation by branch

Use different branches in different environments and initialize Terraform in the root module of the corresponding branch.

Note: Similar to isolation by directory, isolation by branch adopts root modules to configure certain environments in different branches and deploys modification by merging changes in different branches.

#### Isolation by workspace

Create resources based on different `workspace` configurations in the same root module.

Note: In the `prod` directory, `cicd` and `qta` isolate the configurations of different businesses by `workspace`.