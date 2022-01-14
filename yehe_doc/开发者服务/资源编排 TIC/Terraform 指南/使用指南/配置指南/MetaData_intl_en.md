`Metadata` is a built-in meta-argument supported by Terraform and can be used in provider, resource, data, and module blocks. It mainly includes:
- `depends_on`: explicitly declares dependencies.
- `count`: creates multiple resource instances.
- `for_each`: iterates a collection to create a corresponding resource instance for each element in the collection.
- `provider`: specifies a non-default provider instance.
- `lifecycle`: customizes the lifecycle behavior of a resource.
- `dynamic`: builds repeatable nested blocks.

### depends_on
`depends_on` explicitly declares implicit dependencies between resources that cannot be automatically deducted by Terraform. This is useful only if there is a dependency but no data reference between resources. For example:
```bash
variable "availability_zone" {
  default = "ap-guangzhou-6"
}

resource "tencentcloud_vpc" "vpc" {
  name       = "guagua_vpc_instance_test"
  cidr_block = "10.0.0.0/16"
}

resource "tencentcloud_subnet" "subnet" {
  depends_on = [tencentcloud_vpc.vpc]
  availability_zone = var.availability_zone
  name              = "guagua_vpc_subnet_test"
  vpc_id            = tencentcloud_vpc.vpc.id
  cidr_block        = "10.0.20.0/28"
  is_multicast      = false
}
```

### count
The `count` argument can be any natural number. Terraform creates `count` resource instances, each corresponding to a separate infrastructure object that is created, updated, or terminated separately during Terraform code execution. For example:
```bash
resource "tencentcloud_instance" "foo" {
  availability_zone = var.availability_zone
  instance_name     = "terraform-testing"
  image_id          = "img-ix05e4px"
  ...
  count                      = 3
  tags = {
    Name = "Server ${count.index}"
  }
  ...
```
- **count.index**: represents the count subscript index (starting from 0) corresponding to the current object
- **Access to object with multiple resource instances**: `.`


### for_each
`for_each` is a new feature introduced in Terraform 0.12.6. A `resource` block does not allow both `count` and `for_each` to be declared. The `for_each` argument can be a map or a set(string). Terraform creates a separate infrastructure resource object for each element in the collection; just like with `count`, each infrastructure resource object is created, modified, or terminated separately during Terraform code execution. For example:
- **map**
```bash
resource "tencentcloud_cfs_access_group" "foo" {
  for_each = {
      test1_access_group = "test1"
      test2_access_group = "test2"
  }
  name        = each.key
  description = each.value
}
```
- **set(string)**
```bash
resource "tencentcloud_eip" "foo" {
  for_each = toset(["awesome_gateway_ip1", "awesome_gateway_ip2"])
  name = "awesome_gateway_ip"
}

```

### provider
If multiple instances of the same type of provider are declared, you can specify a `provider` argument to select a provider instance to be used when creating a resource. If no `provider` argument is specified, Terraform will use the one corresponding to the first word in the resource type name by default. For example:
```bash
provider "tencentcloud" {
  region = "ap-guangzhou"
  # secret_id = "my-secret-id"
  # secret_key = "my-secret-key"
}

provider "tencentcloud" {
  alias  = "tencentcloud-beijing"
  region = "ap-beijing"
  # secret_id = "my-secret-id"
  # secret_key = "my-secret-key"
}

resource "tencentcloud_vpc" "foo" {
    name         = "ci-temp-test-updated"
    cidr_block   = "10.0.0.0/16"
    dns_servers  = ["119.29.29.29", "8.8.8.8"]
    is_multicast = false

    tags = {
        "test" = "test"
    }
    provider     = tencentcloud.tencentcloud-beijing
}
```

### lifecycle
Each resource instance goes through creation, update, and termination, while the `lifecycle` block can specify a different behavior. Terraform supports the following types of `lifecycle` blocks:
<dx-accordion>
::: create_before_destroy
By default, when Terraform needs to modify a resource that cannot be directly upgraded due to server-side API limitations, it will delete the existing resource object and replace it with one created using new configuration arguments. The `create_before_destroy` argument can modify this behavior so that Terraform creates a new object and terminates the old one only after it has been successfully replaced. For example:
```bash
lifecycle {
  create_before_destroy = true
}
```
Many infrastructure resources need to have a unique name or ID attribute, and this constraint applies to both the old and new objects when they coexist. Some resource types have special arguments that can add a random prefix to each object name to prevent conflicts, which is not adopted by Terraform by default. You need to resolve this type of constraint for each resource type before using `create_before_destroy`.


:::
::: prevent_destroy
The `prevent_destroy` argument is a safety measure. As long as it is set to `true`, Terraform will refuse to run any change plan that might terminate the infrastructure resource. It prevents accidental deletion of a critical resource, such as erroneous execution of `terraform destroy` or accidental modification of an argument of a resource that makes Terraform decide to delete a resource instance and create a new one.
Declaring `prevent_destroy = true` inside a `resource` block will prevent `terraform destroy` from being executed. For example:
```bash
lifecycle {
  prevent_destroy = true
}
```
The `prevent_destroy` argument should be used with caution. Note that this measure does not prevent Terraform from deleting relevant resources after a `resource` block is deleted, as the corresponding `prevent_destroy = true` statement has also been deleted.

:::
::: ignore_changes
By default, when Terraform detects any discrepancy between the configuration described by the code and a real infrastructure object, it will calculate a change plan to update the infrastructure object to match the state described by the code. In some very rare cases, the actual infrastructure object is modified by a process outside of Terraform, and Terraform will continually try to modify the object to bridge the discrepancy with the code. In such cases, you can instruct Terraform to ignore changes to certain attributes by setting `ignore_changes`. The value of `ignore_changes` defines a set of attribute names that need to be created according to the values defined by the code but do not need to be updated according to value changes. For example:
```bash
resource "tencentcloud_instance" "foo" {
...
lifecycle {
  ignore_changes = [
    # Ignore changes to tags, e.g. because a management agent
    # updates these based on some ruleset managed elsewhere.
    tags,
  ]
}
```
:::
</dx-accordion>
 

### dynamic
In a top-level block such as `resource`, you usually can only perform one-to-one assignments in a form like `name = expression`. This assignment form is generally available, except when some resource types contain repeatable nested blocks. For example:
```bash
resource "tencentcloud_tcr_instance" "foo" {
  name                  = "example"
  instance_type		    = "basic"
  open_public_operation = true
  security_policy {
    cidr_block = "10.0.0.1/24"
  }
  security_policy {
    cidr_block = "192.168.1.1/24"
  }
}

```
In this case, you can use the `dynamic` block to dynamically build repeatable nested blocks similar to `security_policy`. For example:
```bash
resource "tencentcloud_tcr_instance" "foo" {
  name                  = "example"
  instance_type         = "basic"
  open_public_operation = true
  dynamic "security_policy" {
    for_each = toset(["10.0.0.1/24", "192.168.1.1/24"])
    content {
      cidr_block = security_policy.value
    }
  }
}
```

`dynamic` can be used in `resource`, `data`, `provider`, and `provisioner` blocks. Similar to a `for` expression, it produces nested blocks that iterate a complex type of data and generate a corresponding nested block for each element. In the above example:

- The label of `dynamic`, i.e. `"security_policy"`, determines the type of nested blocks to be generated.
- The `for_each` argument provides the complex type values to be iterated.
- The `iterator` argument (optional) sets the name of a temporary variable that represents the current iteration element. If `iterator` is not set, the temporary variable name will default to the label of the `dynamic` block, i.e. `security_policy`.
- The `labels` argument (optional) is an ordered list of block labels to generate a set of nested blocks in sequence. Temporary `iterator` variables can be used in expressions with the `labels` argument.
- The nested `content` block defines the body of the nested block to be generated. Temporary `iterator` variables can be used inside the `content` block.

`for_each` argument:
- As the `for_each` argument can be a collection or a structured type, you can use `for` or expanded expressions to convert the type of an existing collection.
- The value of `for_each` must be a non-empty map or set. If you need to declare a collection of resource instances based on nested data structures or combinations of elements in multiple data structures, you can use Terraform expressions and functions to generate appropriate values.

The `iterator` variable (setting in the above example) has the following attributes:
- key: if the iteration container is a map, then `key` is the key of the current element. If it is a list, then `key` is the subscript number of the current element in the list. In the case of a set produced by a `for_each` expression, `key` and `value` are equal, and `key` should not be used.
- value: value of the current element. A `dynamic` block can only generate nested block arguments within the current block definition. It is impossible to generate meta-arguments such as `lifecycle` and `provisioner`. Terraform must ensure the successful calculation of values for these meta-arguments.



