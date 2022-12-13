## Overview
EdgeOne has been connected to Terraform to allow for quick configuration. This document describes how to use Terraform to quickly add an EdgeOne site.

## Prerequisites
You have installed and configured Terraform as instructed in [Installing and Configuring Terraform](https://www.tencentcloud.com/document/product/1145/51433).

## Directions
1. Define the site resources managed through Terraform.
   You need to write a Terraform configuration file and save it with the `.tf` extension. You can view the parameter definitions of [EdgeOne site resources](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs/resources/teo_zone) on the Terraform Provider documentation page.
	 Below is the `tencent_teo.tf` sample configuration file:
```terraform
terraform {
  required_providers {
    tencentcloud = {
      source  = "tencentcloudstack/tencentcloud"
      version = ">= 1.78.5"
    }
  }
}
provider "tencentcloud" {
  secret_id  = "<your-secret-id>"
  secret_key = "<your-secret-key>"
  region     = "ap-guangzhou"
}
resource "tencentcloud_teo_zone" "example" {
  zone_name = "example.com"
  plan_type = "<your-plan-type>"
  tags = {
    "createdBy" = "terraform"
  }
}
```

2. In the directory of the Terraform configuration file, run the `terraform init` command to initialize the configuration.
   In this step, Terraform will automatically check the `provider` field in the configuration file and download the latest module and plugin.
   If the following message is printed, the initialization is successful.
```
Initializing the backend...
Initializing provider plugins...
- Finding tencentcloudstack/tencentcloud versions matching ">= 1.78.5"...
- Installing tencentcloudstack/tencentcloud v1.78.5...
- Installed tencentcloudstack/tencentcloud v1.78.5 (signed by a HashiCorp partner, key ID 84F69E1C1BECF459)
Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://www.terraform.io/docs/cli/plugins/signing.html
Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.
Terraform has been successfully initialized!
```

3. Run the `terraform plan` command to preview the configuration and verify whether it is correct.
```
PS tf-doc> terraform.exe plan
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
Terraform will perform the following actions:
  # tencentcloud_teo_zone.example will be created
  + resource "tencentcloud_teo_zone" "example" {
      + area                    = (known after apply)
      + cname_speed_up          = (known after apply)
      + cname_status            = (known after apply)
      + created_on              = (known after apply)
      + id                      = (known after apply)
      + modified_on             = (known after apply)
      + name_servers            = (known after apply)
      + original_name_servers   = (known after apply)
      + paused                  = (known after apply)
      + plan_type               = "ent"
      + resources               = (known after apply)
      + status                  = (known after apply)
      + tags                    = {
          + "createdBy" = "terraform"
        }
      + type                    = (known after apply)
      + vanity_name_servers_ips = (known after apply)
      + zone_id                 = (known after apply)
      + zone_name               = "example.com"
    }
Plan: 1 to add, 0 to change, 0 to destroy.
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

4. Run `terraform apply` to add an EdgeOne node.
   After the `terraform apply` command is executed, Terraform will ask you to confirm the actions to be executed. After confirming that everything is correct, enter `yes`. Then, wait for the command to complete.
```
PS tf-doc> terraform apply
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
Terraform will perform the following actions:
  # tencentcloud_teo_zone.example will be created
  + resource "tencentcloud_teo_zone" "example" {
      + area                    = (known after apply)
      + cname_speed_up          = (known after apply)
      + cname_status            = (known after apply)
      + created_on              = (known after apply)
      + id                      = (known after apply)
      + modified_on             = (known after apply)
      + name_servers            = (known after apply)
      + original_name_servers   = (known after apply)
      + paused                  = (known after apply)
      + plan_type               = "ent"
      + resources               = (known after apply)
      + status                  = (known after apply)
      + tags                    = {
          + "createdBy" = "terraform"
        }
      + type                    = (known after apply)
      + vanity_name_servers_ips = (known after apply)
      + zone_id                 = (known after apply)
      + zone_name               = "example.com"
    }
Plan: 1 to add, 0 to change, 0 to destroy.
Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.
  Enter a value: yes
tencentcloud_teo_zone.example: Creating...
tencentcloud_teo_zone.example: Creation complete after 6s [id=zone-2ag9gej58j36]
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

5. Modify the DNS configuration of the connected site.
   To make the site effective, you need to modify the NS server of the site if you use NS access or to add a TXT record for site verification if you use CNAME access. For more information, see [Connection Method](https://intl.cloud.tencent.com/document/product/1145/45967).
6. Verify whether the site has taken effect.
   Wait a few minutes after step 5 and refresh the resource status through `terraform refresh`. Then, run `terraform show` to check whether the site has taken effect.
   If NS access is used, the value of the `status` field should be `active` after the site takes effect. If CNAME access is used, the value of the `cname_status` field should be `finished` after the site takes effect.

```
PS tf-doc> terraform refresh
tencentcloud_teo_zone.example: Refreshing state... [id=zone-2ag9gej58j36]
PS tf-doc> terraform show   
# tencentcloud_teo_zone.example:
resource "tencentcloud_teo_zone" "example" {
    area                    = "overseas"
    cname_speed_up          = "enabled"
    cname_status            = "pending"
...
    original_name_servers   = []
    paused                  = false
    plan_type               = "ent"
    status                  = "active"
    tags                    = {
        "createdBy" = "terraform"
    }
    type                    = "full"
    vanity_name_servers_ips = []
    zone_id                 = "zone-2ag9gej58j36"
    zone_name               = "example.com"
}
```

## Notes
1. When creating a site, you can query available plans through the data source [tencentcloud_teo_zone_available_plans](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs/data-sources/teo_zone_available_plans).
2. You can configure Terraform with [environment variables](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs#environment-variables) to avoid writing the TencentCloud API key to the Terraform configuration file.