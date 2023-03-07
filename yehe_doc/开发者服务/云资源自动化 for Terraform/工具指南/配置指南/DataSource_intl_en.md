Data sources allow Terraform to use information defined outside of Terraform, defined by another separate Terraform configuration, or modified by functions.

## Using a data source

A data source is accessed via a special kind of resource known as a data resource, declared using a `data` block as shown below:
``` bash
data "tencentcloud_availability_zones" "my_favourite_zone" {
  name = "ap-guangzhou-3"
}
```

## Referencing a data source

The syntax for referencing data from a data source is `data.<TYPE>.<NAME>.<ATTRIBUTE>` as shown below:
``` bash
resource "tencentcloud_subnet" "app" {
  ...
  availability_zone = data.tencentcloud_availability_zones.default.zones.0.name
  ...
}
```

