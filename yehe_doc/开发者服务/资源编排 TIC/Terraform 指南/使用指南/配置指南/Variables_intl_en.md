
## Input Variable
- Input variables let you customize aspects of Terraform modules without altering the module's own source code. This allows you to share modules across different Terraform configurations, making your module composable and reusable.
- Input variables can be dynamically passed in; for example, you can pass in variables when creating or modifying the infrastructure, replace hard-coded access keys with variables when defining a provider in the code, and let users (infrastructure creators) decide the desired server size.
- You can understand a set of Terraform code as a function, so the input variables can be seen as function input parameters.

### Defining input variable
Input variables are defined using a `variable` block. For example:
```bash
variable "image_id" {
  type = string
}

variable "availability_zone_names" {
  type    = list(string)
  default = ["us-west-1a"]
}

variable "docker_ports" {
  type = list(object({
    internal = number
    external = number
    protocol = string
  }))
  default = [
    {
      internal = 8300
      external = 8300
      protocol = "tcp"
    }
  ]
}
```

The label after the `variable` keyword is a name for the variable, which must be unique among all variables in the same module. You can reference the variable value in the code through `var.<NAME>`.

A `variable` block can be declared with the following optional arguments:
- `default`: specifies the default value of the input variable.
- `type`: specifies that the input variable can only be assigned with a specific value.
- `description`: specifies the description of the input variable.
- `validation`: specifies the validation rules for the input variable.
- `sensitive`: limits Terraform UI output when the variable is used in configuration.
- `nullable`: specifies whether the input variable can be `null` or not.

#### Type
A type is defined in an input variable block by `type`.
- Basic types: `string`, `number`, `bool`.
- Complex types: `list(<TYPE>)`, `set(<TYPE>)`, `map(<TYPE>)`, `object({<ATTR NAME> = <TYPE>, ... })`, `tuple([<TYPE>, ...])`.

#### Description
You can briefly describe the purpose of each variable. For example:
```bash
variable "image_id" {
  type        = string
  description = "The id of the machine image (AMI) to use for the server."
}
```

#### Custom validation rule
Prior to Terraform 0.13.0, only type constraints could be used to ensure that input arguments were of the correct type. Terraform 0.13.0 introduced custom validation rules for input variables. For example:
```bash
variable "image_id" {
  type        = string
  description = "The id of the machine image (AMI) to use for the server."

  validation {
    condition     = length(var.image_id) > 4 && substr(var.image_id, 0, 4) == "ami-"
    error_message = "The image_id value must be a valid AMI id, starting with \"ami-\"."
  }
}
```
The `condition` argument is a bool argument. You can use an expression to determine whether the input variable is valid. When the `condition` is `true`, the input variable is valid; otherwise, it is not. A `condition` expression can reference only the currently defined variable by `var.<VARIABLE NAME>` and must not produce errors. If the failure of an expression is the basis of the validation decision, use the `can` function to detect such errors. For example:
```bash
variable "image_id" {
  type        = string
  description = "The id of the machine image (AMI) to use for the server."

  validation {
    # regex(...) fails if it cannot find a match
    condition     = can(regex("^ami-", var.image_id))
    error_message = "The image_id value must be a valid AMI id, starting with \"ami-\"."
  }
}
```
In the above example, if the input `image_id` does not meet the requirements of the regex, the regex function call will throw an error, which will be captured by the `can` function to output `false`. If the condition expression outputs `false`, Terraform will return the error message defined in `error_message`, which should fully describe the reason for the failure of the input variable validation, along with the valid constraints on the input variable.


### Using input variable
You can access an input variable with `var.<VARIABLE NAME>` only within the module where the variable is declared. For example:
```bash
resource "tencentclould_instance" "example" {
  instance_type = "t2.micro"
  ami           = var.image_id
}
```



### Assigning value to input variable

#### Command line argument
To specify individual variables on the command line, you need to use the `-var` option when running the `terraform plan` and `terraform apply` commands. For example:
```bash
terraform apply -var="image_id=ami-abc123"
terraform apply -var='image_id_list=["ami-abc123","ami-def456"]' -var="instance_type=t2.micro"
terraform apply -var='image_id_map={"us-east-1":"ami-abc123","us-east-2":"ami-def456"}'
```

#### Argument file
When you set a large number of variables, we recommend you specify their values in the variable argument file (suffixed with `.tfvars` or `.tfvars.json`) and specify the file on the command line with `-var-file`. For example:
```bash
terraform apply -var-file="testing.tfvars"
```
Argument definition files use the same basic syntax as Terraform language files but contain only variable name assignments. For example:
```bash
image_id = "ami-abc123"
availability_zone_names = [
  "us-east-1a",
  "us-west-1c",
]
```
Terraform automatically loads a number of variable definition files:
- Files named `terraform.tfvars` or `terraform.tfvars.json`.
- Files suffixed with `.auto.tfvars` or `.auto.tfvars.json`.
- `.json` files need to be defined with the JSON syntax. For example:
```bash
{
  "image_id": "ami-abc123",
  "availability_zone_names": ["us-west-1a", "us-west-1c"]
}
```


#### Environment variable
You can specify input variables by defining environment variables prefixed with `TF_VAR_`. For example:
```bash
export TF_VAR_image_id=ami-abc123
export TF_VAR_availability_zone_names='["us-west-1b","us-west-1d"]'
```


### Input variable priority
- You may assign the same variable more than once when using multiple assignment methods at the same time. Terraform overwrites the old value with the new one and loads variable values in the following order:
  1. Environment variables
 2. `terraform.tfvars` files (if any)
 3. `terraform.tfvars.json` files (if any)
 4. All `.auto.tfvars` or `.auto.tfvars.json` files in alphabetical order
 5. Input variables passed in through the `-var` or `-var-file` command line argument, in the order defined in such argument
- If you have tried multiple assignment methods in vain, Terraform will try to use the default value. For variables without a default value defined, Terraform will ask you to input a value on an interactive UI. Some Terraform commands will report errors if they are executed with the `-input=false` argument that disables value passing on the interactive UI.

## Output Variable
Output variables make information of the infrastructure available for the command line and other Terraform configurations. An output value is similar to a returned value in traditional programming languages.


### Use cases
- Child modules can use output variables to pass their resource attributes to modules.
- Root modules can use output variables to print certain values in the CLI output after `terraform apply` is executed.
- When the remote state is used, other configurations can access the root module output through the `terraform_remote_state` data source.


### Defining output variable
Output variables are declared using an `output` block. For example:
```bash
output "instance_ip_addr" {
  value = tencentclould_instance.server.private_ip
}
```

#### Optional argument
- **description**
Specifies descriptive information of the output value. For example:
```
output "instance_ip_addr" {
  value       = tencentclould_instance.server.private_ip
  description = "The private IP address of the main server instance."
}
```
- **sensitive**
Hides the value of the output variable on the CLI when the `terraform plan` and `terraform apply` commands are being executed.
- **depends_on**
Terraform parses various data and resources defined by the code and their dependencies. For example, if the `image_id` argument used to create a virtual machine is queried by `data`, then the virtual machine instance depends on this image's `data`. Terraform creates `data` first and then the virtual machine `resource` after the query result is obtained.
In general, the order for creating `data` and `resource` is automatically calculated by Terraform and does not need to be explicitly specified by the code writer. However, sometimes there are dependencies that cannot be derived through code analysis, in which case the dependencies can be explicitly declared in the code through `depends_on`. For example:
```
output "instance_ip_addr" {
  value       = tencentclould_instance.server.private_ip
  description = "The private IP address of the main server instance."

  depends_on = [
    # Security group rule must be created before this IP address could
    # actually be used, otherwise the services will be unreachable.
    tencentclould_security_group_rule.local_access,
  ]
}
```

## Local Variable
If you need to use a complex expression to calculate a value and use it repeatedly, you can assign the complex expression a local value and then reference it repeatedly. If you see the input variable as the function input and output value as the returned value of the function, the local value is equivalent to a local variable defined in the function.
 

### Local variable definition
Local variables are declared using a `locals` block. For example:
```
locals {
  service_name = "forum"
  owner        = "Community Team"
}
```
Additionally, local variables include not only literal constants but also other variables of the module (variables, resource attributes, or other local values) in order to convert or combine them. For example:
```
locals {
  # Ids for multiple sets of EC2 instances, merged together
  instance_ids = concat(tencentclould_instance.blue.*.id, tencentclould_instance.green.*.id)
}

locals {
  # Common tags to be assigned to all resources
  common_tags = {
    Service = local.service_name
    Owner   = local.owner
  }
}
```

### Using local variable
Local variables are referenced through the `local.<NAME>` expression. For example:
```
resource "tencentclould_instance" "example" {
  # ...

  tags = local.common_tags
}
```
