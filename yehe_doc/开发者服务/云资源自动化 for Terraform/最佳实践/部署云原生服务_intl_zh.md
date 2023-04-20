本文介绍如何使用 Terraform 创建腾讯云 TKE 标准集群并结合 Terraform Kubernetes Provider 部署一个简单的 Nginx 应用。

## 前置条件
- Terraform >=0.14.0

- 注册 [腾讯云账号](https://www.tencentcloud.com/document/product/378/17985)。

- 获取凭证，在 [API密钥管理](https://console.cloud.tencent.com/cam/capi) 页面中创建并复制 SecretId 和 SecretKey。

- 进入 [容器服务控制台](https://console.cloud.tencent.com/tke2/cluster?rid=1)，按照界面提示为容器服务授权。


## 创建 TKE 相关资源

创建任意空目录，如 `tf-tke-example`。目录创建后，按照以下步骤声明腾讯云资源。

### 配置基础网络

创建 network.tf 文件，配置私有网络 VPC 、子网和安全组。代码如下：
``` hcl
# Networks
variable "vpc_name" {
  default     = "example-vpc"
}

variable "subnet_name" {
  default     = "example-subnet"
}

variable "security_group_name" {
  default     = "example-security-group"
}

variable "network_cidr" {
  default     = "10.0.0.0/16"
}

variable "security_ingress_rules" {
  default = [
    "ACCEPT#10.0.0.0/16#ALL#ALL",
    "ACCEPT#172.16.0.0/22#ALL#ALL",
    "DROP#0.0.0.0/0#ALL#ALL"
  ]
}

resource "tencentcloud_vpc" "vpc" {
  cidr_block = var.network_cidr
  name       = var.vpc_name
  tags       = var.tags
}

resource "tencentcloud_subnet" "subnet" {
  availability_zone = var.available_zone
  cidr_block        = var.network_cidr
  name              = var.subnet_name
  vpc_id            = tencentcloud_vpc.vpc.id
  tags              = var.tags
}

resource "tencentcloud_security_group" "sg" {
  name        = var.security_group_name
  description = "example security groups for kubernetes networks"
  tags        = var.tags
}

resource "tencentcloud_security_group_lite_rule" "sg_rules" {
  security_group_id = tencentcloud_security_group.sg.id
  ingress           = var.security_ingress_rules
  egress = [
    "ACCEPT#0.0.0.0/0#ALL#ALL"
  ]
}
```

### 配置集群

创建 cluster.tf 文件，配置 TKE 集群。代码如下：
``` hcl
# TKE
variable "cluster_name" {
  default     = "example-cluster"
}

variable "cluster_version" {
  default     = "1.22.5"
}

variable "cluster_cidr" {
  default     = "172.16.0.0/22"
}

variable "cluster_os" {
  default     = "tlinux2.2(tkernel3)x86_64"
}

variable "cluster_public_access" {
  default     = true
}

variable "cluster_private_access" {
  default     = true
}

variable "worker_count" {
  default     = 1
}

variable "worker_instance_type" {
  default     = "S5.MEDIUM2"
}

variable "available_zone" {
  default     = "ap-guangzhou-3"
}

variable "tags" {
  default = {
    terraform = "example"
  }
}

resource "random_password" "worker_pwd" {
  length           = 12
  min_numeric      = 1
  min_special      = 1
  min_upper        = 1
  override_special = "!#$%&*()-_=+[]{}<>:?"
}

resource "tencentcloud_kubernetes_cluster" "cluster" {
  cluster_name                    = var.cluster_name
  cluster_version                 = var.cluster_version
  cluster_cidr                    = var.cluster_cidr
  cluster_os                      = var.cluster_os
  cluster_internet                = var.cluster_public_access
  cluster_internet_security_group = var.cluster_public_access ? tencentcloud_security_group.sg.id : null
  cluster_intranet                = var.cluster_private_access
  cluster_intranet_subnet_id      = var.cluster_private_access ? tencentcloud_subnet.subnet.id : null
  vpc_id                          = tencentcloud_vpc.vpc.id

  worker_config {
    availability_zone  = var.available_zone
    count              = var.worker_count
    instance_type      = var.worker_instance_type
    subnet_id          = tencentcloud_subnet.subnet.id
    security_group_ids = [tencentcloud_security_group.sg.id]
    password = random_password.worker_pwd.result
  }

  tags = var.tags
}
```

### 配置 CAM 角色（可选）

容器服务 TKE 需要访问其他资源的权限，需要 `TKE_QCSRole` 角色并授予其预设策略 `TF_QcloudAccessForTKERole`，`TF_QcloudAccessForTKERoleInOpsManagement` 。

>!
> 如果您已经在控制台完成授权（如下图所示），则不需要创建这个文件。 
> ![](https://staticintl.cloudcachetci.com/yehe/backend-news/wYpM119_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220160518.png)



创建 cam.tf 文件，配置 CAM 角色并关联策略。代码如下：
``` hcl
resource "tencentcloud_cam_role" "TKE_QCSRole" {
  name        = "TKE_QCSRole"
  document    = <<EOF
{
  "statement": [
    {
      "action":"name/sts:AssumeRole",
      "effect":"allow",
      "principal":{
        "service":"ccs.qcloud.com"
      }
    }
  ],
  "version":"2.0"
}
EOF
  description = "The TKE service role."
}

data "tencentcloud_cam_policies" "ops_mgr" {
  name = "QcloudAccessForTKERoleInOpsManagement"
}

data "tencentcloud_cam_policies" "qca" {
  name = "QcloudAccessForTKERole"
}

locals {
  ops_policy_id = data.tencentcloud_cam_policies.ops_mgr.policy_list.0.policy_id
  qca_policy_id = data.tencentcloud_cam_policies.qca.policy_list.0.policy_id
}

resource "tencentcloud_cam_role_policy_attachment" "QCS_OpsMgr" {
  role_id   = lookup(tencentcloud_cam_role.TKE_QCSRole, "id")
  policy_id = local.ops_policy_id
}

resource "tencentcloud_cam_role_policy_attachment" "QCS_QCA" {
  role_id   = lookup(tencentcloud_cam_role.TKE_QCSRole, "id")
  policy_id = local.qca_policy_id
}
```

### 封装为 Module（可选）

您可以把这些 .tf 文件组织起来，以 Module 的形式使用可以减少关注内部的实现，或者直接参考现有的 Module [terraform-tencentcloud-tke](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-tke) ，欢迎使用、 提 Issue 和 Pull Request。

## 配置 Kubernetes

通过上文的配置，我们可以创建出一个基本的 TKE 托管集群，接下来介绍如何把 Kubernetes 结合 TKE 部署一个简单的 Nginx 应用。

### 配置 K8s Provider

通过上文编写的 TF 文件，我们可以获取集群的外网访问地址，CA 证书和用户凭证。
以上文 [Modules](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-tke/tree/main/examples/kubernetes) 为例，将集群的主机和凭证填入 Kubernetes Provider 中。代码如下：

``` hcl
terraform {
  required_providers {
    kubernetes = {
      source  = "hashicorp/kubernetes"
      version = ">= 2.0.0"
    }
    tencentcloud = {
      source  = "tencentcloudstack/tencentcloud"
      version = ">=1.77.7"
    }
  }
}

provider "tencentcloud" {
  region = "ap-hongkong"
}

module "tencentcloud_tke" {
  source         = "github.com/terraform-tencentcloud-modules/terraform-tencentcloud-tke"
  available_zone = "ap-hongkong-3" # Available zone must belongs to the region.
}

provider "kubernetes" {
  host                   = module.tencentcloud_tke.cluster_endpoint
  cluster_ca_certificate = module.tencentcloud_tke.cluster_ca_certificate
  client_key             = base64decode(module.tencentcloud_tke.client_key)
  client_certificate     = base64decode(module.tencentcloud_tke.client_certificate)
}
```

### 配置安全组外网访问

我们不推荐完全放通外网访问，默认的安全组仅放通 `10.0.0.0/16` 、`172.16.0.0/22` 网段，如要测试集群的外网访问，您需要额外添加期望放通的规则。  

修改上文的 `module` 块，传入指定的规则。代码如下：
``` hcl
module "tencentcloud_tke" {
  source         = "../../"
  available_zone = var.available_zone # Available zone must belongs to the region.
  create_cam_strategy = false
  security_ingress_rules = [
    "ACCEPT#10.0.0.0/16#ALL#ALL",
    "ACCEPT#172.16.0.0/22#ALL#ALL",
    "ACCEPT#(改成你的 IP 地址，括号去掉)#ALL#ALL",
    "DROP#0.0.0.0/0#ALL#ALL"
  ]
}
```

### 配置 resources

在 Terraform 中，我们可以使用 HCL 替代原来的 yaml 声明 Namespace、Deployment 和 Service。代码如下：
``` hcl
resource "kubernetes_namespace" "test" {
  metadata {
    name = "nginx"
  }
}

resource "kubernetes_deployment" "test" {
  metadata {
    name      = "nginx"
    namespace = kubernetes_namespace.test.metadata.0.name
  }
  spec {
    replicas = 2
    selector {
      match_labels = {
        app = "MyTestApp"
      }
    }
    template {
      metadata {
        labels = {
          app = "MyTestApp"
        }
      }
      spec {
        container {
          image = "nginx"
          name  = "nginx-container"
          port {
            container_port = 80
          }
        }
      }
    }
  }
}

resource "kubernetes_service" "test" {
  metadata {
    name      = "nginx"
    namespace = kubernetes_namespace.test.metadata.0.name
  }
  spec {
    selector = {
      app = kubernetes_deployment.test.spec.0.template.0.metadata.0.labels.app
    }
    type = "NodePort"
    port {
      node_port   = 30201
      port        = 80
      target_port = 80
    }
  }
}
```

### 配置 Ingress

这里介绍如何配置 Ingress 关联负载均衡 (CLB) ，以实现公网访问，我们先创建一个 CLB 实例。代码如下：
``` hcl
locals {
  lb_vpc = module.tencentcloud_tke.vpc_id
  lb_sg  = module.tencentcloud_tke.security_group_id
}

resource "tencentcloud_clb_instance" "ingress-lb" {
  address_ip_version           = "ipv4"
  clb_name                     = "example-lb"
  internet_bandwidth_max_out   = 1
  internet_charge_type         = "BANDWIDTH_POSTPAID_BY_HOUR"
  load_balancer_pass_to_target = true
  network_type                 = "OPEN"
  security_groups              = [local.lb_sg]
  vpc_id                       = local.lb_vpc
}
```

配置 Ingress，指定刚才创建的 CLB ID。代码如下：
``` hcl
resource "kubernetes_ingress_v1" "test" {
  metadata {
    name      = "test-ingress"
    namespace = "nginx"
    annotations = {
      "ingress.cloud.tencent.com/direct-access"     = "false"
      "kubernetes.io/ingress.class"                 = "qcloud"
      "kubernetes.io/ingress.existLbId"             = tencentcloud_clb_instance.ingress-lb.id
      "kubernetes.io/ingress.extensiveParameters"   = "{\"AddressIPVersion\": \"IPV4\"}"
      "kubernetes.io/ingress.http-rules"            = "[{\"path\":\"/\",\"backend\":{\"serviceName\":\"nginx\",\"servicePort\":\"80\"}}]"
      "kubernetes.io/ingress.https-rules"           = "null"
      "kubernetes.io/ingress.qcloud-loadbalance-id" = tencentcloud_clb_instance.ingress-lb.id
      "kubernetes.io/ingress.rule-mix"              = "false"
    }
  }
  spec {
    rule {
      http {
        path {
          backend {
            service {
              name = kubernetes_service.test.metadata.0.name
              port {
                number = 80
              }
            }
          }
          path = "/"
        }
      }
    }
  }
}
```

如果需要获取 CLB 的 IP 地址，可以创建一个 output 变量。代码如下：
``` hcl
output "load_balancer_ip" {
  value       = kubernetes_ingress_v1.test.status.0.load_balancer.0.ingress.0.ip
}
```

## 执行创建

所有 .tf 文件编写好后，按次序执行如下命令：
``` bash
$ terraform init
$ terraform plan
$ terraform apply
```

创建成功后，控制台输出上文的 output 信息：
``` txt
Apply complete! Resources: 16 added, 0 changed, 0 destroyed.

Outputs:

load_balancer_ip = "xxx.xxx.xxx.xxx"
```

## 验证部署

登录腾讯云控制台，访问容器服务 -> example-cluster 集群，可以看到 Nginx 相关的 Pod 已经 Running:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/hBaN946_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_d36efe57-ccb3-407a-befc-0f13f8eaa657.png)

访问 `load_balancer_ip` 显示的地址，页面显示 Welcome To Nginx 则说明应用部署成功！

![](https://qcloudimg.tencent-cloud.cn/image/document/7c8913afd6077d43c4314add7589c53c.png)
