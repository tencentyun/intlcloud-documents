## Overview
EdgeOne has been connected to Terraform to allow for quick configuration. This document describes how to use Terraform to configure site acceleration. For more information, see [Tencent Cloud EdgeOne](https://www.tencentcloud.com/document/product/1145/46168).

## Prerequisites
1. You have installed and configured Terraform as instructed in [Installing and Configuring Terraform](https://www.tencentcloud.com/document/product/1145/51433).
2. You have connected to the site through Terraform as instructed in [Creating Site Through Terraform](https://www.tencentcloud.com/document/product/1145/51434).

## Directions
1. Modify the Terraform configuration file and add the resource definitions of site acceleration configuration.
   You can view the parameter definitions of the [site acceleration configuration](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs/resources/teo_zone_setting) on the Terraform Provider documentation page. Below is the `tencent_teo.tf` sample configuration file.

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
  plan_type = "ent"
  tags = {
    "createdBy" = "terraform"
  }
}
resource "tencentcloud_teo_zone_setting" "example" {
  zone_id = tencentcloud_teo_zone.example.id
  # Cache rule configuration
  cache {
    follow_origin {
      switch = "on" # Follow the origin server
    }
  }
  # Cache key configuration
  cache_key {
    full_url_cache = "off" # Do not enable full path cache
    ignore_case    = "on" # Ignore the case
    query_string {
      switch = "on"
      action = "includeCustom" # Only use the specified URL parameter
      value  = ["param0", "param1"]
    }
  }
  # HTTPS acceleration configuration of the domain name
  https {
    ocsp_stapling = "on" # OCSP configuration enabled
    tls_version   = ["TLSv1.2", "TLSv1.3"] # Supported TLS protocol versions
  }
  # Smart compression configuration
  compression {
    switch     = "on"
    algorithms = ["brotli", "gzip"]
  }
  # Region of the client IP during origin-pull
  client_ip_header {
    switch      = "on"
    header_name = "EO-Client-IPCountry"
  }
}
```

2. Run the `terraform plan` command to preview the configuration and verify whether it is correct.
```
PS tf-doc> terraform.exe plan
tencentcloud_teo_zone.example: Refreshing state... [id=zone-2ag9gej58j36]
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
Terraform will perform the following actions:
  # tencentcloud_teo_zone_setting.example will be created
  + resource "tencentcloud_teo_zone_setting" "example" {
      + area    = (known after apply)
      + id      = (known after apply)
      + zone_id = "zone-2ag9gej58j36"
      + cache {
          + cache {
              + cache_time           = (known after apply)
              + ignore_cache_control = (known after apply)
              + switch               = (known after apply)
            }
          + follow_origin {
              + switch = "on"
            }
          + no_cache {
              + switch = (known after apply)
            }
        }
      + cache_key {
          + full_url_cache = "off"
          + ignore_case    = "on"
          + query_string {
              + action = "includeCustom"
              + switch = "on"
              + value  = [
                  + "param0",
                  + "param1",
                ]
            }
        }
      + cache_prefresh {
          + percent = (known after apply)
          + switch  = (known after apply)
        }
      + client_ip_header {
          + header_name = "EO-Client-IPCountry"
          + switch      = "on"
        }
      + compression {
          + algorithms = [
              + "brotli",
              + "gzip",
            ]
          + switch     = "on"
        }
      + force_redirect {
          + redirect_status_code = (known after apply)
          + switch               = (known after apply)
        }
      + https {
          + ocsp_stapling = "on"
          + tls_version   = [
              + "TLSv1.2",
              + "TLSv1.3",
            ]
        }
      + ipv6 {
          + switch = (known after apply)
        }
      + max_age {
          + follow_origin = (known after apply)
          + max_age_time  = (known after apply)
        }
      + offline_cache {
          + switch = (known after apply)
        }
      + origin {
          + backup_origins       = (known after apply)
          + cos_private_access   = (known after apply)
          + origin_pull_protocol = (known after apply)
          + origins              = (known after apply)
        }
      + post_max_size {
          + max_size = (known after apply)
          + switch   = (known after apply)
        }
      + quic {
          + switch = (known after apply)
        }
      + smart_routing {
          + switch = (known after apply)
        }
      + upstream_http2 {
          + switch = (known after apply)
        }
      + web_socket {
          + switch  = (known after apply)
          + timeout = (known after apply)
        }
    }
Plan: 1 to add, 0 to change, 0 to destroy.
─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

3. Run `terraform apply` to create the site acceleration configuration.
   After the `terraform apply` command is executed, Terraform will ask you to confirm the actions to be executed. After confirming that everything is correct, enter `yes`. Then, wait for the command to complete.
```
PS tf-doc> terraform.exe apply                                     
tencentcloud_teo_zone.example: Refreshing state... [id=zone-2ag9gej58j36]
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
Terraform will perform the following actions:
  # tencentcloud_teo_zone_setting.example will be created
  + resource "tencentcloud_teo_zone_setting" "example" {
      + area    = (known after apply)
      + id      = (known after apply)
      + zone_id = "zone-2ag9gej58j36"
      + cache {
          + cache {
              + cache_time           = (known after apply)
              + ignore_cache_control = (known after apply)
              + switch               = (known after apply)
            }
          + follow_origin {
              + switch = "on"
            }
          + no_cache {
              + switch = (known after apply)
            }
        }
      + cache_key {
          + full_url_cache = "off"
          + ignore_case    = "on"
          + query_string {
              + action = "includeCustom"
              + switch = "on"
              + value  = [
                  + "param0",
                  + "param1",
                ]
            }
        }
      + cache_prefresh {
          + percent = (known after apply)
          + switch  = (known after apply)
        }
      + client_ip_header {
          + header_name = "EO-Client-IPCountry"
          + switch      = "on"
        }
      + compression {
          + algorithms = [
              + "brotli",
              + "gzip",
            ]
          + switch     = "on"
        }
      + force_redirect {
          + redirect_status_code = (known after apply)
          + switch               = (known after apply)
        }
      + https {
          + ocsp_stapling = "on"
          + tls_version   = [
              + "TLSv1.2",
              + "TLSv1.3",
            ]
        }
      + ipv6 {
          + switch = (known after apply)
        }
      + max_age {
          + follow_origin = (known after apply)
          + max_age_time  = (known after apply)
        }
      + offline_cache {
          + switch = (known after apply)
        }
      + origin {
          + backup_origins       = (known after apply)
          + cos_private_access   = (known after apply)
          + origin_pull_protocol = (known after apply)
          + origins              = (known after apply)
        }
      + post_max_size {
          + max_size = (known after apply)
          + switch   = (known after apply)
        }
      + quic {
          + switch = (known after apply)
        }
      + smart_routing {
          + switch = (known after apply)
        }
      + upstream_http2 {
          + switch = (known after apply)
        }
      + web_socket {
          + switch  = (known after apply)
          + timeout = (known after apply)
        }
    }
Plan: 1 to add, 0 to change, 0 to destroy.
Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.
  Enter a value: yes
tencentcloud_teo_zone_setting.example: Creating...
tencentcloud_teo_zone_setting.example: Creation complete after 1s [id=zone-2ag9gej58j36]
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

4. Check the command execution result.
   You can run `terraform show` to check whether the site acceleration configuration takes effect or log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) for confirmation.
```
PS tf-doc> terraform state show tencentcloud_teo_zone_setting.example
# tencentcloud_teo_zone_setting.example:
resource "tencentcloud_teo_zone_setting" "example" {
    area    = "overseas"
    id      = "zone-2ag9gej58j36"
    zone_id = "zone-2ag9gej58j36"
    cache {
        follow_origin {
            switch = "on"
        }
        no_cache {
            switch = "off"
        }
    }
    cache_key {
        full_url_cache = "off"
        ignore_case    = "on"
        query_string {
            action = "includeCustom"
            switch = "on"
            value  = [
                "param0",
                "param1",
            ]
        }
    }
    cache_prefresh {
        percent = 90
        switch  = "off"
    }
    client_ip_header {
        header_name = "EO-Client-IPCountry"
        switch      = "on"
    }
    compression {
        algorithms = [
            "brotli",
            "gzip",
        ]
        switch     = "on"
    }
    force_redirect {
        redirect_status_code = 302
        switch               = "off"
    }
    https {
        http2         = "on"
        ocsp_stapling = "on"
        tls_version   = [
            "TLSv1.2",
            "TLSv1.3",
        ]
        hsts {
            include_sub_domains = "off"
            max_age             = 0
            preload             = "off"
            switch              = "off"
        }
    }
    ipv6 {
        switch = "off"
    }
    max_age {
        follow_origin = "on"
        max_age_time  = 600
    }
    offline_cache {
        switch = "on"
    }
    origin {
        backup_origins       = []
        origin_pull_protocol = "follow"
        origins              = []
    }
    post_max_size {
        max_size = 524288000
        switch   = "on"
    }
    quic {
        switch = "off"
    }
    smart_routing {
        switch = "off"
    }
    upstream_http2 {
        switch = "off"
    }
    web_socket {
        switch  = "off"
        timeout = 30
    }
}

```