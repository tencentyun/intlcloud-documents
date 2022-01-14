
## Terraform Overview
[Terraform](https://www.terraform.io/) is an open-source resource orchestration tool written in Go and running on the client. It is highly scalable based on the HashiCorp Plugin architecture. Currently, Tencent Cloud implements the TencentCloud Provider based on Terraform plugin to manage Tencent Cloud resources through Terraform. The schematic diagram is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/d8c9eb0619e3bfab3f57dad1474a291c.png)

Based on tencentcloud-sdk-go, [TencentCloud Provider](https://github.com/tencentcloudstack/terraform-provider-tencentcloud) offers more than 183 resources and 158 data sources across over 30 products, covering compute, storage, network, container service, load balancing, middleware, database, and cloud monitoring to meet your basic needs for cloudification.

For a quick start on Terraform, see [TencentCloud Provider](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs) and [Examples](https://github.com/tencentcloudstack/terraform-provider-tencentcloud/tree/master/examples). In addition, certain resources have been and more resources will be supported on [Terraform Module](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest).

## Terraform Strengths

### Multi-Cloud orchestration
Terraform is suitable for multi-cloud solutions where you can deploy similar infrastructures in Tencent Cloud, other cloud providers, or local IDCs. You can manage resources from different cloud providers at the same time using the same tools and similar configuration files.


### Infrastructure and code
You can use the high-level configuration syntax HCL to describe an infrastructure, so that it can be codified and versioned for sharing and reuse as shown in the following example:
```bash
resource "tencentcloud_mysql_instance" "mysql" {
    mem_size          = 16000
    cpu               = 4
    volume_size       = 50
    charge_type       = "PREPAID"
    instance_name     = "testAccMysql"
    engine_version    = "5.5"
    root_password     = "test1234"
    availability_zone = var.availability_zone
    internet_service  = 1
    intranet_port     = 3360
    prepaid_period    = 1

    tags = {
        purpose = "for test"
    }

    parameters = {
        max_connections = "1000"
    }
    count = 1
}
```

### Execution plan
Terraform has a "planning" step to generate an execution plan, which shows the state of Terraform when `apply` is called. This allows you to avoid incidents when the infrastructure is manipulated on Terraform, as shown in the following example:
```bash
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
+ create

Terraform will perform the following actions:

# tencentcloud_ckafka_instance.foo will be created
+ resource "tencentcloud_ckafka_instance" "foo" {
    + band_width         = (known after apply)
    + disk_size          = 500
    + disk_type          = "CLOUD_BASIC"
    + id                 = (known after apply)
    + instance_name      = "tf-test"
    + kafka_version      = "1.1.1"
    + msg_retention_time = 1300
    + partition          = (known after apply)
    + period             = 1
    + public_network     = (known after apply)
    + renew_flag         = 0
    + subnet_id          = "subnet-dvzsb5ro"
    + vpc_id             = "vpc-fvl16x63"
    + zone_id            = 100006

    + config {
        + auto_create_topic_enable   = true
        + default_num_partitions     = 3
        + default_replication_factor = 3
        }

    + dynamic_retention_config {
        + bottom_retention        = (known after apply)
        + disk_quota_percentage   = (known after apply)
        + enable                  = 1
        + step_forward_percentage = (known after apply)
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.
```


### Resource topology
Terraform builds a resource map to create and modify non-dependent resources in parallel. This enhances the efficiency of infrastructure construction on Terraform and helps you gain better insights into infrastructure dependencies with the following command:
```bash
terraform graph | dot -Tsvg > graph.svg
```
A diagram of the generated resources is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/dfa0f17c2481d3ac81b94433af3a64af.png)


### Auto change
You can apply complex change sets to your infrastructure with minimal manual intervention. With the execution plan and resource topology mentioned above, you can get an accurate picture of Terraform dynamics and avoid possible human errors.

### Remote state management
Terraform introduces the concept of backend, a remote state storage mechanism. Currently, Tencent Cloud can manage your tfstate files through COS to avoid storing files locally and causing file losses. In addition, remote storage makes it possible for multiple users to manage Terraform resources concurrently.
