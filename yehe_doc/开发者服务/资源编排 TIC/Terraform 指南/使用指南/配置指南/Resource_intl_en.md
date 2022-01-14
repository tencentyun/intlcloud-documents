Resources are the most important element in the Terraform language. A resource is defined using a `resource` block, which describes one or more infrastructure objects, such as VPC and VM.

## Resource Syntax
A resource is defined using a `resource` block, which contains the `resource` keyword, resource type, resource name, and resource block body as shown below:
```
    resource "tencentcloud_vpc" "foo" {
        name         = "ci-temp-test-updated"
        cidr_block   = "10.0.0.0/16"
        dns_servers  = ["119.29.29.29", "8.8.8.8"]
        is_multicast = false

        tags = {
            "test" = "test"
        }
    }
```

## Resource Reference
A resource attribute is referenced in the syntax format of `<RESOURCE TYPE>.<NAME>.<ATTRIBUTE>` as shown below:
```
tencentcloud_vpc.foo.resource # ci-temp-test-updated
```
