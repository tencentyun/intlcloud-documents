This document describes how to use Terraform to create a Tencent Cloud TKE general cluster and use the Kubernetes provider for Terraform to deploy a simple Nginx application.

## Prerequisites
- Terraform is on v0.14.0 or later.

- Register at [Tencent Cloud](https://www.tencentcloud.com/document/product/378/17985).

- Get the credentials. Create and copy `SecretId` and `SecretKey` on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page.

- Authorize TKE as prompted in the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1).


## Creating TKE Resources

Create an empty directory, for example, `tf-tke-example`. Then, declare Tencent Cloud resources in the following steps.

### Configuring the classic network

Create the `network.tf` file and configure the VPC, subnet, and security group as follows:
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

### Configuring the cluster

Create the `cluster.tf` file and configure the TKE cluster as follows:
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

### (Optional) Configuring the CAM role

TKE requires the access to other resources. You need to create the `TKE_QCSRole` role and the `TF_QcloudAccessForTKERole` and `TF_QcloudAccessForTKERoleInOpsManagement` preset policies.

>!
> You don't need to create the file if you have completed the authorization in the console as shown below: 
> ![](https://staticintl.cloudcachetci.com/yehe/backend-news/wYpM119_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220160518.png)



Create the `cam.tf` file, configure the CAM role, and associate the policy as follows:
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

### (Optional) Encapsulating into a module

You can encapsulate these .tf files into a module so that you can focus less on the internal implementation. Or you can directly refer to the existing module [terraform-tencentcloud-tke](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-tke). You can submit issues and pull requests.

## Configuring Kubernetes

The above configurations are enough to create a basic TKE managed cluster. The following describes how to use Kubernetes and TKE to deploy a simple Nginx application.

### Configuring the K8s provider

Get the public network address, CA certificate, and user credentials of the cluster from the above .tf files.
Taking the above [module](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-tke/tree/main/examples/kubernetes) as an example, enter the server and credentials of the cluster in the Kubernetes provider as follows:

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
  region     = "ap-hongkong"
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

### Configuring the public network access of the security group

We recommend you not open all public IP ranges. By default, the security group opens only `10.0.0.0/16` and `172.16.0.0/22`. To test the public network access of the cluster, add rules to open the target IP range.  

Modify the above `module` block by passing in the specified rule as follows:
``` hcl
module "tencentcloud_tke" {
  source         = "../../"
  available_zone = var.available_zone # Available zone must belongs to the region.
  create_cam_strategy = false
  security_ingress_rules = [
    "ACCEPT#10.0.0.0/16#ALL#ALL",
    "ACCEPT#172.16.0.0/22#ALL#ALL",
    "ACCEPT#(Your IP address without the parentheses `()`)#ALL#ALL",
    "DROP#0.0.0.0/0#ALL#ALL"
  ]
}
```

### Configuring resources

In Terraform, declare the namespace, Deployment, and Service via HCL instead of YAML as follows:
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

### Configuring an Ingress

The following describes how to configure an Ingress to associate a CLB instance to implement public network access. First, create a CLB instance as follows:
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

Configure the Ingress and specify the ID of the created CLB instance as follows:
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

To get the CLB IP, create the `output` variable as follows:
``` hcl
output "load_balancer_ip" {
  value       = kubernetes_ingress_v1.test.status.0.load_balancer.0.ingress.0.ip
}
```

## Executing Creation

Run the following commands in sequence after writing all the .tf files:
``` bash
$ terraform init
$ terraform plan
$ terraform apply
```

After the successful creation, the console will output the above `output` information:
``` txt
Apply complete! Resources: 16 added, 0 changed, 0 destroyed.

Outputs:

load_balancer_ip = "xxx.xxx.xxx.xxx"
```

## Verifying Deployment

Log in to the Tencent Cloud console and go to TKE > **example-cluster**. You can see that Nginx Pods are **Running**:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/hBaN946_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_d36efe57-ccb3-407a-befc-0f13f8eaa657.png)

Access the address of `load_balancer_ip`. If the page displays "Welcome to nginx!", the application is deployed successfully.

![](https://qcloudimg.tencent-cloud.cn/image/document/7c8913afd6077d43c4314add7589c53c.png)
