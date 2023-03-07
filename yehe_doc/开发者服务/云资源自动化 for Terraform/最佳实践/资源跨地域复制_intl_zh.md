本文介绍如何将已有资源导入 Terraform，以及如何通过复制文件的方式创建新资源，完成跨地域复制。

## 已有资源导入到 Terraform

大部分刚接触 Terraform 的用户，可能在云上已经存在资源并期望将他们导入到 Terraform 中管理，Terraform 支持单个资源的导入，但是碰到多资源多实例的导入，则需要借助开源工具实现，以下介绍这两种场景的导入方法。

### 导入单个资源

Terraform 支持 Import 命令导入单个资源，格式 `terraform import [资源类型].[名称] [入参]`。名称可以自定义，入参则是查询资源必要的字符串（一般为 ID ，部分资源是名字或者多字段组合）。以云服务器实例为例，通过查询 [CVM Resource 文档](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs/resources/instance#import) ，可知导入命令为 ：
``` shell
$ terraform import tencentcloud_instance.ins ins-jvu2hiw2 -allow-missing-config
```

其中 `-allow-missing-config` 表示允许本地不需要预先声明 block ，否则需要在文件中预先写一段 `resource [资源类型].[名称] {}` 这样的空块导入完成后，字段**不会**写入 TF 文件中，需要执行 `terraform show` 查看导入的资源代码：
``` hcl
# tencentcloud_instance.ins:
resource "tencentcloud_instance" "ins" {
    allocate_public_ip         = true
    availability_zone          = "ap-guangzhou-3"
    create_time                = "2022-01-01T01:11:11Z"
    id                         = "ins-xxxxxxxx"
    image_id                   = "img-xxxxxxxx"
    instance_charge_type       = "POSTPAID_BY_HOUR"
    instance_name              = "xxxxxxxx"
    instance_status            = "RUNNING"
    instance_type              = "S3.MEDIUM2"
    internet_charge_type       = "TRAFFIC_POSTPAID_BY_HOUR"
    internet_max_bandwidth_out = 1
    key_name                   = "skey-xxxxxxxx"
    private_ip                 = "10.0.1.1"
    project_id                 = 0
    public_ip                  = "1.1.1.1"
    running_flag               = true
    security_groups            = [
        "sg-xxxxxxxx",
    ]
    subnet_id                  = "subnet-xxxxxxxx"
    system_disk_id             = "disk-xxxxxxxx"
    system_disk_size           = 50
    system_disk_type           = "CLOUD_PREMIUM"
    tags                       = {}
    vpc_id                     = "vpc-xxxxxxxx"
}
```

将这段代码填入您的 TF 文件中，还需要去掉只读字段，通过 [Attribute Reference](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs/resources/instance#attributes-reference) 可知，需要去掉 `id`, `create_time`, `public_ip` 后完成导入。
``` hcl
resource "tencentcloud_instance" "ins" {
    allocate_public_ip         = true
    availability_zone          = "ap-guangzhou-3"
#    create_time                = "2022-01-01T01:11:11Z"
#    id                         = "ins-xxxxxxxx"
    image_id                   = "img-xxxxxxxx"
    instance_charge_type       = "POSTPAID_BY_HOUR"
    instance_name              = "xxxxxxxx"
#    instance_status            = "RUNNING"
    instance_type              = "S3.MEDIUM2"
    internet_charge_type       = "TRAFFIC_POSTPAID_BY_HOUR"
    internet_max_bandwidth_out = 1
    key_name                   = "skey-xxxxxxxx"
    private_ip                 = "10.0.1.1"
    project_id                 = 0
#    public_ip                  = "1.1.1.1"
    running_flag               = true
    security_groups            = [
        "sg-xxxxxxxx",
    ]
    subnet_id                  = "subnet-xxxxxxxx"
    system_disk_id             = "disk-xxxxxxxx"
    system_disk_size           = 50
    system_disk_type           = "CLOUD_PREMIUM"
    tags                       = {}
    vpc_id                     = "vpc-xxxxxxxx"
}
```

要获取各个资源的 Import 命令和只读字段，访问 [文档](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs) 中对应的实例中可以查询。如果未填写，则说明该资源暂不支持导入。

### 使用 Terraformer 批量导入

通过上文可以看到使用 Terraform 的导入相当繁琐，仅适合导入少量资源。您可能需要借助 Terraformer 进行批量导入。Terraformer 是一个属于 GoogleCloudPlatform 的命令行工具，可以把账号下大部分云资源标记并导入为 TF 文件。
1. 安装

   ``` shell
   $ brew install terraformer
   ```
2. 执行导入命令，假如我想导入腾讯云广州区下所有的 CVM 和 VPC 资源，那么命令格式如下：

   ``` shell
    terraformer import tencentcloud --resources="vpc,cvm" --regions=ap-guangzhou
   ```

   命令执行完成后，Terraformer 默认将导入的资源文件写入 `./generated` 目录，示例如下：

   ``` txt
   .
   └── tencentcloud
       ├── cvm
       │   └── ap-guangzhou
       │       ├── instance.tf
       │       ├── key_pair.tf
       │       ├── outputs.tf
       │       ├── provider.tf
       │       ├── terraform.tfstate
       │       └── variables.tf
       └── vpc
           └── ap-guangzhou
               ├── outputs.tf
               ├── provider.tf
               ├── terraform.tfstate
               └── vpc.tf
   ```
3. **换源**：TencentCloudProvider 由我们腾讯云维护而非 Terraform 官方，需要在生成的 `provider.tf` 中添加 `source` 字段，值为 `tencentcloudstack/tencentcloud`。

   ``` hcl
   provider "tencentcloud" {
     version = "~> 1.77.11"
   }
   
   terraform {
     required_providers {
       tencentcloud = {
         source  = "tencentcloudstack/tencentcloud" # 添加 source 以指定命名空间
         version = "~> 1.77.11"
       }
     }
   }
   
   ```

   当然，不是所有的腾讯云资源 Terraformer 都支持导入，查看已支持导入的资源参考 [Terraformer 源码](https://github.com/GoogleCloudPlatform/terraformer/tree/master/providers/tencentcloud)。


## 跨地域复制

### 实现原理

一个简单的 Terraform 工作目录结构如下：
``` txt
.
├── .terraform
│   └── providers # 引用到的 Provider
├── .terraform.lock.hcl # Provider 锁版本
├── main.tf             # TF 文件
├── vars.tf             # TF 文件
├── outputs.tf          # TF 文件
└── terraform.tfstate   # 状态文件

```

而本地的工作目录跟腾讯云资源映射结构如下图所示：

![](https://qcloudimg.tencent-cloud.cn/image/document/36fccf5b78ee1b28459dc193475b709d.png)

当用户执行 `terraform apply` 命令且部署完成后。会生成 `terraform.tfstate` 文件。它是一份 JSON 格式的文件，默认存储在本地，或者配置在远端存储桶中（需要配置 [Backend](https://www.terraform.io/language/settings/backends/configuration) ）用来描述 TF 声明的资源和真实云资源的映射关系。如果本地目录或 Backend 中不存在 `terraform.tfstate` ，或者该文件没有写入云资源数据，Terraform 就会认为资源没有被部署，执行 `apply` 会进行资源创建操作。

### 示例：TKE Serverless 集群跨地域复制

只要没有 `tfstate` 映射的资源声明都视为创建。基于这一思路，我们通过复制文件并修改地域的方法，再执行 `apply` 即可完成资源跨地域复制。

假设我们已经通过 Terraform 在广州部署了一套基于 Serverless 集群服务的应用，目录如下：
``` txt
eks-app-guangzhou
├── crds.tf
├── infra.tf
├── main.tf
├── terraform.log
└── terraform.tfstate
```

其中 `main.tf` 指定 Terraform 和 Provider 的元信息。代码如下：
``` hcl
terraform {
  required_providers {
    tencentcloud = {
      source = "tencentcloudstack/tencentcloud"
    }
  }
}

provider "tencentcloud" {
  region = "ap-guangzhou"
}
```

`infra.tf` 指定 TKE Serverless 集群和所需的资源：VPC、子网、安全组、TKE Serverless 集群、负载均衡。代码如下：
``` hcl
# 服务对外放通测试 IP 地址
variable "accept_ip" {
   description = "Use EnvVar: $TF_VAR_accept_ip instead"
}

resource "tencentcloud_vpc" "vpc" {
  name       = "eks-vpc"
  cidr_block = "10.2.0.0/16"
}

resource "tencentcloud_subnet" "sub" {
  vpc_id            = tencentcloud_vpc.vpc.id
  name              = "eks-subnet"
  cidr_block        = "10.2.0.0/20"
  availability_zone = "ap-guangzhou-3"
}

resource "tencentcloud_security_group" "sg" {
  name = "eks-sg"
}

resource "tencentcloud_security_group_lite_rule" "sgr" {
  security_group_id = tencentcloud_security_group.sg.id
  ingress = [
    "ACCEPT#10.2.0.0/16#ALL#ALL",
    "ACCEPT#${var.accept_ip}#ALL#ALL"
  ]
}

resource "tencentcloud_eks_cluster" "foo" {
  cluster_name = "tf-test-eks"
  k8s_version = "1.20.6"
  vpc_id = tencentcloud_vpc.vpc.id
  subnet_ids = [
    tencentcloud_subnet.sub.id,
  ]
  cluster_desc = "test eks cluster created by terraform"
  service_subnet_id = tencentcloud_subnet.sub.id
  enable_vpc_core_dns = true
  need_delete_cbs = true
  public_lb {
    enabled = true
    security_policies = [var.accept_ip]
  }
  internal_lb {
    enabled = true
    subnet_id = tencentcloud_subnet.sub.id
  }
}

resource "tencentcloud_clb_instance" "ingress-lb" {
  address_ip_version           = "ipv4"
  clb_name                     = "example-lb"
  internet_bandwidth_max_out   = 1
  internet_charge_type         = "BANDWIDTH_POSTPAID_BY_HOUR"
  load_balancer_pass_to_target = true
  network_type                 = "OPEN"
  security_groups              = [tencentcloud_security_group.sg.id]
  vpc_id                       = tencentcloud_vpc.vpc.id
}

```

`crds.tf` 指定基于 TKE Serverless 集群的 CRD。代码如下：
``` hcl
locals {
  kubeconfig = yamldecode(tencentcloud_eks_cluster.foo.kube_config)
}

provider "kubernetes" {
  host                   = local.kubeconfig.clusters[0].cluster.server
  cluster_ca_certificate = base64decode(local.kubeconfig.clusters[0].cluster["certificate-authority-data"])
  client_key             = base64decode(local.kubeconfig.users[0].user["client-key-data"])
  client_certificate     = base64decode(local.kubeconfig.users[0].user["client-certificate-data"])
}

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
    #    selfLink = "/apis/networking.k8s.io/v1/namespaces/nginx/ingresses/test-ingress"
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

如果想要将这些资源复制一份到其他地域（以新加坡为例） ，那么可以执行以下步骤：
1. 复制该目录下的所有 .tf 文件到新的目录下，如 `eks-app-singapore`，断开原目录的 `tfstate` 引用：

   ``` shell
   $ mkdir ../eks-app-singapore
   $ cp *.tf ../eks-app-singapore
   $ cd ../eks-app-singapore
   ```
2. 修改 TencentCloud Provider 的地域。代码如下：

   ``` hcl
   provider "tencentcloud" {
     # - replace
     # region = "ap-guangzhou"
     # + to
     region = "ap-singapore"
   }
   ```
3. 在新目录 `eks-app-singapore` 下执行 `terraform init` 和 `terraform plan`。由于没有 `tfstate` 文件， plan 提示即将创建新的资源：

   ``` html
   Plan: 11 to add, 0 to change, 0 to destroy.  
   ───────────────────────────────────────  
   Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
   ```
4. 确认无误后，执行 `terraform apply` 即可配置新目录下的云资源在新地域管理。


### 局限性

不同产品的业务形态和逻辑差异较大，导致跨地域复制也是一个比较繁琐的操作。主要限制如下：

#### 实例规格和库存限制

如云服务器、云硬盘、云数据库等实例的资源，各个可用区的实例规格和库存差异较大，很可能出现当前实例规格在其他区域售罄或者不可用的情况，建议使用动态的实例类型，即查询各个资源的 datasource 查询可用的实例规格而非硬编码在文件中，例如：

在上海四区购买 2 核 2G 的 CVM 实例。代码如下：
``` bash
resource "tencentcloud_instance" "cvm" {
  name              = "my-instance"
  availability_zone = "ap-shanghai-4"
  image_id          = "local.cvm_img_id"
  instance_type     = "S5.MEDIUM2"
}
```

切换到广州地域，替换成 datasource 动态获取。代码如下：
``` hcl
provider "tencentcloud" {
   region = "ap-guangzhou"
}

# 查询广州地域 CVM 有哪些可用区
data "tencentcloud_availability_zones_by_product" "cvm" {
  product = "cvm"
}

# 查询以 Tencent 开头的 CVM 镜像
data "tencentcloud_images" "img" {
  image_name_regex = "Tencent"
}

# 查询指定可用区下 2 核 2G 有哪些实例类型
data "tencentcloud_instance_types" "types" {
  availability_zone = data.tencentcloud_availability_zones_by_product.cvm.zones.0.name
  cpu_core_count = 2
  memory_size = 2
}

locals {
   # 挑选第可用区列表的第一个结果
  cvm_zone = data.tencentcloud_availability_zones_by_product.cvm.zones.0.name
   # 挑选镜像列表的第一个结果
  cvm_img_id = data.tencentcloud_images.img.images.0.image_id
   # 挑选实例类型的第一个结果
  cvm_type = data.tencentcloud_instance_types.types.instance_types.0.instance_type
}

resource "tencentcloud_instance" "cvm" {
  name              = "my-instance"
  availability_zone = local.cvm_zone
  image_id          = local.cvm_img_id
  instance_type     = local.cvm_type
}
```

#### 资源数量限制

有些资源在各个地域有数量限制，如 TKE 集群、私有网络、对象存储桶（总量）等，复制之前请确认好目标区域有充足的存量配额，如有配额提升需求，可以通过 [提交工单](https://console.cloud.tencent.com/workorder/category) 申请。

#### 不需要复制的资源

有些资源本身没有地域属性，例如 CAM 用户/角色和策略、SSL 证书、SSH 密钥等。这些资源在进行整体复制操作时需要过滤掉，避免重复创建。

