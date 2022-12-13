## Overview
EdgeOne has been connected to Terraform to allow for quick configuration. This document describes how to use Terraform to configure the rule engine of the EdgeOne site and differentiate subdomain name configurations.

## Prerequisites
1. You have installed and configured Terraform as instructed in [Installing and Configuring Terraform](https://www.tencentcloud.com/document/product/1145/51433).
2. You have connected to the site through Terraform as instructed in [Creating Site Through Terraform](https://www.tencentcloud.com/document/product/1145/51434).

## Directions
1. Modify the Terraform configuration file by adding the resource definitions of the DNS record and rule engine of the subdomain name.
   You can view the parameter definitions of the [DNS record](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs/resources/teo_dns_record) and [rule engine](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs/resources/teo_rule_engine) on the Terraform Provider documentation page. Below is the `tencent_teo.tf` sample configuration file.

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
# DNS record of the subdomain name
resource "tencentcloud_teo_dns_record" "rule_record" {
  zone_id = tencentcloud_teo_zone.example.id
  type    = "A"
  name    = "rule.example.com"
  content = "<your-backend-ip>"
  mode    = "proxied"
  ttl     = 300
}
# Differentiated configurations of the subdomain name
resource "tencentcloud_teo_rule_engine" "rule_example" {
  zone_id   = tencentcloud_teo_zone.example.id
  rule_name = "example_rule"
  status    = "enable" # Enable the rule
  rules {
    # For `rule.example.com` and requests with the `mp3` or `mp4` file extension
    or {
      and {
        target   = "host"
        operator = "equal"
        values   = [tencentcloud_teo_dns_record.rule_record.name]
      }
      and {
        target   = "extension"
        operator = "equal"
        values   = ["mp4", "mp3"]
      }
    }
    actions {
      # Use the specified `CacheKey`
      normal_action {
        action = "CacheKey"
        # `CacheKey` is case-sensitive
        parameters {
          name   = "Type"
          values = ["IgnoreCase"]
        }
        parameters {
          name   = "Switch"
          values = ["off"]
        }
        # `CacheKey` contains the `User-Agent` header
        parameters {
          name   = "Type"
          Values = ["Header"]
        }
        parameters {
          name   = "Switch"
          values = ["on"]
        }
        parameters {
          name   = "Value"
          values = "User-Agent"
        }
      }
    }
    # Add the specified response header
    actions {
      rewrite_action {
        action = "ResponseHeader"
        parameters {
          action = "add"
          name   = "Added-Header"
          values = ["Added-Value"]
        }
      }
    }
  }
}
```

2. Run the `terraform plan` command to preview the configuration and verify whether it is correct.
```
PS tf-doc> terraform plan
tencentcloud_teo_zone.example: Refreshing state... [id=zone-2ag9gej58j36]
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
Terraform will perform the following actions:
  # tencentcloud_teo_dns_record.rule_record will be created
  + resource "tencentcloud_teo_dns_record" "rule_record" {
      + cname         = (known after apply)
      + content       = "<your-backend-ip>"
      + created_on    = (known after apply)
      + dns_record_id = (known after apply)
      + domain_status = (known after apply)
      + id            = (known after apply)
      + locked        = (known after apply)
      + mode          = "proxied"
      + modified_on   = (known after apply)
      + name          = "rule.example.com"
      + priority      = (known after apply)
      + status        = (known after apply)
      + ttl           = 300
      + type          = "A"
      + zone_id       = "zone-2ag9gej58j36"
    }
  # tencentcloud_teo_rule_engine.rule_example will be created
  + resource "tencentcloud_teo_rule_engine" "rule_example" {
      + id        = (known after apply)
      + rule_id   = (known after apply)
      + rule_name = "example_rule"
      + status    = "enable"
      + zone_id   = "zone-2ag9gej58j36"
      + rules {
          + actions {
              + normal_action {
                  + action = "CacheKey"
                  + parameters {
                      + name   = "Type"
                      + values = [
                          + "IgnoreCase",
                        ]
                    }
                  + parameters {
                      + name   = "Switch"
                      + values = [
                          + "off",
                        ]
                    }
                  + parameters {
                      + name   = "Type"
                      + values = [
                          + "Header",
                        ]
                    }
                  + parameters {
                      + name   = "Switch"
                      + values = [
                          + "on",
                        ]
                    }
                  + parameters {
                      + name   = "Value"
                      + values = [
                          + "User-Agent",
                        ]
                    }
                }
            }
          + actions {
              + rewrite_action {
                  + action = "ResponseHeader"
                  + parameters {
                      + action = "add"
                      + name   = "Added-Header"
                      + values = [
                          + "Added-Value",
                        ]
                    }
                }
            }
          + or {
              + and {
                  + operator = "equal"
                  + target   = "host"
                  + values   = [
                      + "rule.example.com",
                    ]
                }
              + and {
                  + operator = "equal"
                  + target   = "extension"
                  + values   = [
                      + "mp3",
                      + "mp4",
                    ]
                }
            }
        }
    }
Plan: 2 to add, 0 to change, 0 to destroy.
─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

3. Run `terraform apply` to create the DNS record and rule engine of the subdomain name.
   After the `terraform apply` command is executed, Terraform will ask you to confirm the actions to be executed. After confirming that everything is correct, enter `yes`. Then, wait for the command to complete.
```
PS tf-doc> terraform apply
tencentcloud_teo_zone.example: Refreshing state... [id=zone-2ag9gej58j36]
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
Terraform will perform the following actions:
  # tencentcloud_teo_dns_record.rule_record will be created
  + resource "tencentcloud_teo_dns_record" "rule_record" {
      + cname         = (known after apply)
      + content       = "<your-backend-ip>"
      + created_on    = (known after apply)
      + dns_record_id = (known after apply)
      + domain_status = (known after apply)
      + id            = (known after apply)
      + locked        = (known after apply)
      + mode          = "proxied"
      + modified_on   = (known after apply)
      + name          = "rule.example.com"
      + priority      = (known after apply)
      + status        = (known after apply)
      + ttl           = 300
      + type          = "A"
      + zone_id       = "zone-2ag9gej58j36"
    }
  # tencentcloud_teo_rule_engine.rule_example will be created
  + resource "tencentcloud_teo_rule_engine" "rule_example" {
      + id        = (known after apply)
      + rule_id   = (known after apply)
      + rule_name = "example_rule"
      + status    = "enable"
      + zone_id   = "zone-2ag9gej58j36"
      + rules {
          + actions {
              + normal_action {
                  + action = "CacheKey"
                  + parameters {
                      + name   = "Type"
                      + values = [
                          + "IgnoreCase",
                        ]
                    }
                  + parameters {
                      + name   = "Switch"
                      + values = [
                          + "off",
                        ]
                    }
                  + parameters {
                      + name   = "Type"
                      + values = [
                          + "Header",
                        ]
                    }
                  + parameters {
                      + name   = "Switch"
                      + values = [
                          + "on",
                        ]
                    }
                  + parameters {
                      + name   = "Value"
                      + values = [
                          + "User-Agent",
                        ]
                    }
                }
            }
          + actions {
              + rewrite_action {
                  + action = "ResponseHeader"
                  + parameters {
                      + action = "add"
                      + name   = "Added-Header"
                      + values = [
                          + "Added-Value",
                        ]
                    }
                }
            }
          + or {
              + and {
                  + operator = "equal"
                  + target   = "host"
                  + values   = [
                      + "rule.example.com",
                    ]
                }
              + and {
                  + operator = "equal"
                  + target   = "extension"
                  + values   = [
                      + "mp3",
                      + "mp4",
                    ]
                }
            }
        }
    }
Plan: 2 to add, 0 to change, 0 to destroy.
Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.
  Enter a value: yes
tencentcloud_teo_dns_record.rule_record: Creating...
tencentcloud_teo_dns_record.rule_record: Creation complete after 2s [id=zone-2ag9gej58j36#record-2ahmb3w7ssl8]
tencentcloud_teo_rule_engine.rule_example: Creating...
tencentcloud_teo_rule_engine.rule_example: Creation complete after 1s [id=zone-2ag9gej58j36#rule-2ahmb5dhn9qq]
Apply complete! Resources: 2 added, 0 changed, 0 destroyed.
```

4. Check the command execution result.
   You can run `terraform show` to check whether the rule engine configuration takes effect or log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) for confirmation.
```
PS tf-doc> terraform state show tencentcloud_teo_dns_record.rule_record
# tencentcloud_teo_dns_record.rule_record:
resource "tencentcloud_teo_dns_record" "rule_record" {
    content       = "<your-backend-ip>"
    created_on    = "2022-10-20T06:31:38Z"
    dns_record_id = "record-2ahmb3w7ssl8"
    domain_status = [
        "security",
    ]
    id            = "zone-2ag9gej58j36#record-2ahmb3w7ssl8"
    locked        = false
    mode          = "proxied"
    modified_on   = "2022-10-20T06:31:38Z"
    name          = "rule.example.com"
    priority      = 0
    status        = "active"
    ttl           = 300
    type          = "A"
    zone_id       = "zone-2ag9gej58j36"
}
PS tf-doc> terraform state show tencentcloud_teo_rule_engine.rule_example
# tencentcloud_teo_rule_engine.rule_example:
resource "tencentcloud_teo_rule_engine" "rule_example" {
    id        = "zone-2ag9gej58j36#rule-2ahmb5dhn9qq"
    rule_id   = "rule-2ahmb5dhn9qq"
    rule_name = "example_rule"
    status    = "enable"
    zone_id   = "zone-2ag9gej58j36"
    rules {
        actions {
            normal_action {
                action = "CacheKey"
                parameters {
                    name   = "Type"
                    values = [
                        "IgnoreCase",
                    ]
                }
                parameters {
                    name   = "Switch"
                    values = [
                        "off",
                    ]
                }
                parameters {
                    name   = "Type"
                    values = [
                        "Header",
                    ]
                }
                parameters {
                    name   = "Switch"
                    values = [
                        "on",
                    ]
                }
                parameters {
                    name   = "Value"
                    values = [
                        "User-Agent",
                    ]
                }
            }
        }
        actions {
            rewrite_action {
                action = "ResponseHeader"
                parameters {
                    action = "add"
                    name   = "Added-Header"
                    values = [
                        "Added-Value",
                    ]
                }
            }
        }
        or {
            and {
                operator = "equal"
                target   = "host"
                values   = [
                    "rule.example.com",
                ]
            }
            and {
                operator = "equal"
                target   = "extension"
                values   = [
                    "mp3",
                    "mp4",
                ]
            }
        }
    }
}
```