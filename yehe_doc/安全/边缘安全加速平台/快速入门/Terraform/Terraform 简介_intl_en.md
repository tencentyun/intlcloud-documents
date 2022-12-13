## Terraform Overview
[Terraform](https://www.terraform.io/) is an open-source resource orchestration tool written in Go and running on the client. It is highly scalable based on the HashiCorp Plugin architecture. Currently, Tencent Cloud implements the TencentCloud Provider based on Terraform plugin to manage Tencent Cloud resources through Terraform. The schematic diagram is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/69ea96aa85a163700d360676fa01abd8.png)

Based on tencentcloud-sdk-go, [TencentCloud Provider](https://github.com/tencentcloudstack/terraform-provider-tencentcloud) offers more than 183 resources and 158 data sources across over 30 products, covering compute, storage, network, container service, load balancing, middleware, database, and cloud monitoring to meet your basic needs for cloudification.

For a quick start on Terraform, see [tencentcloud_teo_zone](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs/resources/teo_zone) and [terraform-provider-tencentcloud/examples/tencentcloud-teo/](https://github.com/tencentcloudstack/terraform-provider-tencentcloud/tree/master/examples/tencentcloud-teo).


## Terraform Strengths
### Multi-cloud orchestration
Terraform is suitable for multi-cloud solutions where you can deploy similar infrastructures in Tencent Cloud, other cloud providers, or local IDCs. You can manage resources from different cloud providers at the same time using the same tools and similar configuration files.

### Infrastructure and code
You can use the high-level configuration syntax HCL to describe an infrastructure, so that it can be codified and versioned for sharing and reuse as shown in the following example:
```terraform
# Create the `example.com` site with NS access  
resource "tencentcloud_teo_zone" "zone" {
  zone_name      = "example.com"
  # Query available plans by `zone_available_plans`
  plan_type      = "<your-plan-type>"
  type           = "full"
  paused         = false
  cname_speed_up = "enabled"
}

# Create the DNS record of `example.com`
resource "tencentcloud_teo_dns_record" "dns_record" {
  zone_id     = tencentcloud_teo_zone.zone.id
  type        = "A"
  name        = "example.com"
  # Enable the CDN acceleration service
  mode        = "proxied"
  content     = "<your-backend-ip>"
  ttl         = 60
}
```

### Execution plan
Terraform has a "planning" step. It runs the `terraform plan` command to generate an execution plan, which shows the state of Terraform when `apply` is called. This allows you to avoid incidents when the infrastructure is manipulated on Terraform, as shown in the following example:
```
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # tencentcloud_teo_dns_record.dns_record will be created
  + resource "tencentcloud_teo_dns_record" "dns_record" {
      + cname         = (known after apply)
      + content       = "<your-backend-ip>"
      + created_on    = (known after apply)
      + domain_status = (known after apply)
      + id            = (known after apply)
      + locked        = (known after apply)
      + mode          = "proxied"
      + modified_on   = (known after apply)
      + name          = "example.com"
      + priority      = (known after apply)
      + type          = "A"
      + status        = (known after apply)
      + ttl           = 60
      + zone_id       = (known after apply)
    }

  # tencentcloud_teo_zone.zone will be created
  + resource "tencentcloud_teo_zone" "zone" {
      + area                    = (known after apply)
      + cname_speed_up          = "enabled"
      + cname_status            = (known after apply)
      + created_on              = (known after apply)
      + id                      = (known after apply)
      + modified_on             = (known after apply)
      + name                    = "example.com"
      + name_servers            = (known after apply)
      + original_name_servers   = (known after apply)
      + paused                  = false
      + plan_type               = "sta"
      + status                  = (known after apply)
      + type                    = "full"
      + vanity_name_servers_ips = (known after apply)

      + vanity_name_servers {
          + servers = (known after apply)
          + switch  = (known after apply)
        }
    }

Plan: 2 to add, 0 to change, 0 to destroy.

───────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

### Auto change
You can apply complex change sets to your infrastructure with minimal manual intervention. With the execution plan and resource topology mentioned above, you can get an accurate picture of Terraform dynamics and avoid possible human errors.

## Remote State Management
Terraform introduces the concept of backend, a remote state storage mechanism. Currently, Tencent Cloud can manage your tfState files through [COS](https://intl.cloud.tencent.com/document/product/436) to avoid storing files locally and causing file losses. In addition, remote storage makes it possible for multiple users to manage Terraform resources concurrently.

 
