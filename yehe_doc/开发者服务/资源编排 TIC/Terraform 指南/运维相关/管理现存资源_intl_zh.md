## 操作场景
若您在使用 Terraform 管理云资源之前，已经通过腾讯云控制台创建了资源，则可参考本文进行操作，将现存资源使用 Terraform 管理。



## 操作步骤
使用 Terraform 接管已经存在的资源，实际上在 Terraform 源文件和状态文件里都反映出该资源的状态即可。本文以使用 Terraform 管理现存 PostgreSQL 告警策略为例。



### 获取资源 ID
1. 登录云监控控制台，选择左侧导航栏中的**告警配置** > **[告警策略](https://console.cloud.tencent.com/monitor/alarm2/policy)**。
2. 找到并记录该策略 ID。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/ab816a00ca37e1c086c2d690ebed2395.png)

### 安装 Terraform
参考 [安装 Terraform](https://intl.cloud.tencent.com/document/product/1043/44197)，完成 Terraform 安装。


### 导入资源文件
1. 进入 Terraform 工作目录，执行以下命令，查看 `main.tf` 内容。
```bash
tencent-cloud cat main.tf
```
返回结果如下所示：
```bash
resource "tencentcloud_monitor_alarm_policy" "policy" {}
```
2. 在文件所在目录下执行以下命令，完成初始化工作。
```bash
terraform init --upgrade
```
返回结果如下所示：
```bash
Initializing the backend...

Initializing provider plugins...
- Finding latest version of tencentcloudstack/tencentcloud...
- Installing tencentcloudstack/tencentcloud v1.60.22...
- Installed tencentcloudstack/tencentcloud v1.60.22 (signed by a HashiCorp partner, key ID 84F69E1C1BECF459)

Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://www.terraform.io/docs/cli/plugins/signing.html

Terraform has made some changes to the provider dependency selections recorded
in the .terraform.lock.hcl file. Review those changes and commit them to your
version control system if they represent changes you intended to make.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```
3. 初始化完成后，执行以下命令，将资源导入状态文件。
```bash
terraform import tencentcloud_monitor_alarm_policy.policy policy-vor9w72r 
```
返回信息如下所示：
```bash
tencentcloud_monitor_alarm_policy.policy: Importing from ID "policy-vor9w72r"...
tencentcloud_monitor_alarm_policy.policy: Import prepared!
  Prepared tencentcloud_monitor_alarm_policy for import
tencentcloud_monitor_alarm_policy.policy: Refreshing state... [id=policy-vor9w72r]

Import successful!

The resources that were imported are shown above. These resources are now in
your Terraform state and will henceforth be managed by Terraform.

```
4. 执行以下命令，查看状态文件。
```bash
cat terraform.tfstate
```
可查看如下所示资源相关信息：
```bash
{
  "version": 4,
  "terraform_version": "1.1.0",
  "serial": 1,
  "lineage": "35791a73-d371-db51-5871-bfee13426217",
  "outputs": {},
  "resources": [
    {
      "mode": "managed",
      "type": "tencentcloud_monitor_alarm_policy",
      "name": "policy",
      "provider": "provider[\"registry.terraform.io/tencentcloudstack/tencentcloud\"]",
      "instances": [
        {
          "schema_version": 0,
          "attributes": {
            "conditions": [
              {
                "is_union_rule": 0,
                "rules": [
                  {
                    "continue_period": 5,
                    "description": "cpu",
                    "filter": [],
                    "is_power_notice": 0,
                    "metric_name": "Cpu",
                    "notice_frequency": 86400,
                    "operator": "gt",
                    "period": 60,
                    "rule_type": "STATIC",
                    "unit": "%",
                    "value": "90"
                  }
                ]
              }
            ],
            "conditon_template_id": null,
            "create_time": null,
            "enable": 1,
            "event_conditions": [
              {
                "continue_period": 0,
                "description": "HASwitch",
                "filter": [],
                "is_power_notice": 0,
                "metric_name": "ha_switch",
                "notice_frequency": 0,
                "operator": "",
                "period": 0,
                "rule_type": "",
                "unit": "",
                "value": ""
              }
            ],
            "id": "policy-vor9w72r",
            "monitor_type": "MT_QCE",
            "namespace": "POSTGRESQL",
            "notice_ids": [
              "notice-l9ziyxw6"
            ],
            "policy_name": "PgSql",
            "project_id": 0,
            "remark": "",
            "trigger_tasks": [],
            "update_time": null
          },
          "sensitive_attributes": [],
          "private": "eyJzY2hlbWFfdmVyc2lvbiI6IjAifQ=="
        }
      ]
    }
  ]
}
```

### 更新源文件
1. 执行以下命令，打印资源信息。
```bash
terraform show
```
返回信息如下所示：
```bash
# tencentcloud_monitor_alarm_policy.policy:
resource "tencentcloud_monitor_alarm_policy" "policy" {
    enable       = 1
    id           = "policy-vor9w72r"
    monitor_type = "MT_QCE"
    namespace    = "POSTGRESQL"
    notice_ids   = [
        "notice-l9ziyxw6",
    ]
    policy_name  = "PgSql"
    project_id   = 0

    conditions {
        is_union_rule = 0

        rules {
            continue_period  = 5
            description      = "cpu"
            is_power_notice  = 0
            metric_name      = "Cpu"
            notice_frequency = 86400
            operator         = "gt"
            period           = 60
            rule_type        = "STATIC"
            unit             = "%"
            value            = "90"
        }
    }

    event_conditions {
        continue_period  = 0
        description      = "HASwitch"
        is_power_notice  = 0
        metric_name      = "ha_switch"
        notice_frequency = 0
        period           = 0
    }
}
```
2. 将资源代码拷贝至 Terraform 源文件 `tencentcloud.tf` 中。需删除其中不可设置的选项，例如 ID。
完成编辑后，`tencentcloud.tf` 文件内容如下所示：
```bash
provider tencentcloud {}
resource "tencentcloud_monitor_alarm_policy" "policy" {
  enable       = 1
#  id           = "policy-vor9w72r"
  monitor_type = "MT_QCE"
  namespace    = "POSTGRESQL"
  notice_ids   = [
    "notice-l9ziyxw6",
  ]
  policy_name  = "PgSql"
  project_id   = 0

  conditions {
    is_union_rule = 0

    rules {
      continue_period  = 5
      description      = "cpu"
      is_power_notice  = 0
      metric_name      = "Cpu"
      notice_frequency = 86400
      operator         = "gt"
      period           = 60
      rule_type        = "STATIC"
      unit             = "%"
      value            = "90"
    }
  }

  event_conditions {
    continue_period  = 0
    description      = "HASwitch"
    is_power_notice  = 0
    metric_name      = "ha_switch"
    notice_frequency = 0
    period           = 0
  }
}
```

### 校验
执行以下命令，使用当前工作目录下的代码和状态文件执行 refresh。
```bash
terraform plan
```
返回信息如下所示，可查看 Terraform 已成功接管。
```bash
tencentcloud_monitor_alarm_policy.policy: Refreshing state... [id=policy-vor9w72r]

No changes. Your infrastructure matches the configuration.

Terraform has compared your real infrastructure against your configuration and found no differences, so no changes are needed.
```
至此，Terraform 已成功接管现存资源。可通过 `destory` 来删除该资源，也可通过修改代码的方式对资源进行修改。例如，修改告警阈值后，执行以下命令进行更新。
```bash
terraform plan
```
返回信息如下所示，可查看修改的 value 会导致 Terraform 提示将会更新这个告警策略。
```bash
tencentcloud_monitor_alarm_policy.policy: Refreshing state... [id=policy-vor9w72r]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  ~ update in-place

Terraform will perform the following actions:

  # tencentcloud_monitor_alarm_policy.policy will be updated in-place
  ~ resource "tencentcloud_monitor_alarm_policy" "policy" {
        id           = "policy-vor9w72r"
        # (6 unchanged attributes hidden)

      ~ conditions {
            # (1 unchanged attribute hidden)

          ~ rules {
              ~ value            = "90" -> "99"
                # (9 unchanged attributes hidden)
            }
        }

        # (1 unchanged block hidden)
    }

Plan: 0 to add, 1 to change, 0 to destroy.
```
