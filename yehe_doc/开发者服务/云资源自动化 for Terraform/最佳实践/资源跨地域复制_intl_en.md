This document describes how to import an existing resource to Terraform and create a resource through file copying for cross-region replication.

## Importing an Existing Resource to Terraform

Most users new to Terraform may want to import existing cloud resources to Terraform for management. Terraform allows for importing a single resource. To import multiple resources and instances, open-source tools are required. The following describes the import methods in the two scenarios.

### Importing a single resource

You can run the `Import` command in Terraform to import a single resource in the format of `terraform import [Resource type].[Name] [Input parameter]`. The name is custom, and the input parameter is a required string for resource query (which is an ID in most cases and a name or multi-field combination for certain resources). Taking the CVM instance as an example, the import command indicated in [Import](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs/resources/instance#import) is as follows:
``` shell
$ terraform import tencentcloud_instance.ins ins-jvu2hiw2 -allow-missing-config
```

Here, `-allow-missing-config` indicates not to require a pre-declared block locally; otherwise, you need to pre-write a `resource [Resource type].[Name] {}` block in the file. After the import, fields **will not** be written into the .tf file, and you need to run `terraform show` to view the code of the imported resource:
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

Write the code into your .tf file and remove read-only fields (`id`, `create_time`, and `public_ip` as indicated in [Attributes Reference](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs/resources/instance#attributes-reference)) before the import.
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

Get the `Import` command and read-only fields of each resource [here](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs). If they are not found, the resource cannot be imported currently.

### Batch importing resources via Terraformer

The above method applies only when the number of resources is small and will become very troublesome for batch import. In this case, you can use Terraformer, a command line tool of Google Cloud Platform that can tag and import most cloud resources under your account as .tf files.
1. Install.

   ``` shell
   $ brew install terraformer
   ```
2. Run the import command. To import all CVM and VPC resources in Guangzhou region, the command format will be as follows:

   ``` shell
    terraformer import tencentcloud --resources="vpc,cvm" --regions=ap-guangzhou
   ```

   After the command is run, Terraform will write the imported resource files into the `./generated` directory by default as shown below:

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
3. **Change the source**: TencentCloud Provider is maintained by Tencent Cloud but not Terraform. Therefore, you need to add the `source` field to the generated `provider.tf` file, with the value of `tencentcloudstack/tencentcloud`.

   ``` hcl
   provider "tencentcloud" {
     version = "~> 1.77.11"
   }
   
   terraform {
     required_providers {
       tencentcloud = {
         source  = "tencentcloudstack/tencentcloud" # Add `source` to specify the namespace
         version = "~> 1.77.11"
       }
     }
   }
   
   ```

   Not all Tencent Cloud resources can be imported via Terraformer. For more information, see [terraformer/providers/tencentcloud](https://github.com/GoogleCloudPlatform/terraformer/tree/master/providers/tencentcloud).


## Cross-Region Replication

### How it works

Below is a simple Terraform working directory structure:
``` txt
.
├── .terraform
│   └── providers # Referenced providers
├── .terraform.lock.hcl # Provider lock version
├── main.tf             # tf. file
├── vars.tf             # tf. file
├── outputs.tf          # tf. file
└── terraform.tfstate   # State file

```

Local working directories are mapped to Tencent Cloud resources as shown below:

![](https://qcloudimg.tencent-cloud.cn/image/document/36fccf5b78ee1b28459dc193475b709d.png)

After you run the `terraform apply` command and complete the deployment, the `terraform.tfstate` file will be generated. It is a JSON file stored locally by default or configured in a remote bucket (you need to configure the [backend](https://www.terraform.io/language/settings/backends/configuration)) to describe the mapping between resources declared by Terraform and real cloud resources. If `terraform.tfstate` does not exist in the local directory or backend, or no cloud resource data is written into it, Terraform will consider that no resources are deployed and run `apply` for resource creation.

### Sample: Cross-region replication in TKE Serverless clusters

Resource declaration without the `tfstate` mapping is regarded as creation. Therefore, you can copy a file, modify the region, and run `apply` for cross-region replication of resources.

Below is the sample directory of the application deployed in Guangzhou region via Terraform based on the serverless cluster service:
``` txt
eks-app-guangzhou
├── crds.tf
├── infra.tf
├── main.tf
├── terraform.log
└── terraform.tfstate
```

Here, `main.tf` specifies the meta information of Terraform and the provider as follows:
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

`infra.tf` specifies the TKE serverless cluster and required resources: VPC, subnet, security group, TKE serverless cluster, and CLB instance as follows:
``` hcl
# The IP address for the test on the external accessibility of the service
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

`crds.tf` specifies the CRD of the TKE Serverless cluster as follows:
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

Copy these resources to another region (such as Singapore) in the following steps:
1. Copy all the .tf files to a new directory, for example, `eks-app-singapore`, and remove the original directory's reference to `tfstate`:

   ``` shell
   $ mkdir ../eks-app-singapore
   $ cp *.tf ../eks-app-singapore
   $ cd ../eks-app-singapore
   ```
2. Modify the region of the TencentCloud Provider as follows:

   ``` hcl
   provider "tencentcloud" {
     # - replace
     # region = "ap-guangzhou"
     # + to
     region = "ap-singapore"
   }
   ```
3. Run `terraform init` and `terraform plan` in the `eks-app-singapore` directory. As there is no `tfstate` file, `terraform plan` will prompt that resources will be created:

   ``` html
   Plan: 11 to add, 0 to change, 0 to destroy.  
   ───────────────────────────────────────  
   Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
   ```
4. After confirming that everything is OK, run `terraform apply` to configure management of cloud resources in the new directory in the new region.


### Limitations

Products vary greatly by business form and logic, which makes cross-region replication troublesome. Main limitations are described as follows.

#### Instance specification and inventory limits

The specification and inventory limits of different Tencent Cloud resources, such as CVM, CBS, and TencentDB instances, vary greatly by AZ, which means that the specification of the current instance may be sold out or unavailable in another AZ. We recommend you use dynamic instance types, that is, query the `datasource` of each resource to query available instance specifications, instead of hard-coding the data in a file, for example:

Purchase a 2-core 2 GB MEM CVM instance in Shanghai Zone 4 as follows:
``` bash
resource "tencentcloud_instance" "cvm" {
  name              = "my-instance"
  availability_zone = "ap-shanghai-4"
  image_id          = "local.cvm_img_id"
  instance_type     = "S5.MEDIUM2"
}
```

Switch to Guangzhou region and dynamically get the information via `datasource` as follows:
``` hcl
provider "tencentcloud" {
   region = "ap-guangzhou"
}

# Query the AZs in Guangzhou region where CVM instances are available
data "tencentcloud_availability_zones_by_product" "cvm" {
  product = "cvm"
}

# Query CVM images starting with `Tencent`
data "tencentcloud_images" "img" {
  image_name_regex = "Tencent"
}

# Query the 2-core 2 GB MEM instance types in the specified AZ
data "tencentcloud_instance_types" "types" {
  availability_zone = data.tencentcloud_availability_zones_by_product.cvm.zones.0.name
  cpu_core_count = 2
  memory_size = 2
}

locals {
   # Select the first result in the AZ list
  cvm_zone = data.tencentcloud_availability_zones_by_product.cvm.zones.0.name
   # Select the first result in the image list
  cvm_img_id = data.tencentcloud_images.img.images.0.image_id
   # Select the first result in the instance type list
  cvm_type = data.tencentcloud_instance_types.types.instance_types.0.instance_type
}

resource "tencentcloud_instance" "cvm" {
  name              = "my-instance"
  availability_zone = local.cvm_zone
  image_id          = local.cvm_img_id
  instance_type     = local.cvm_type
}
```

#### Resource quantity limit

Certain resources (such as TKE clusters, VPCs, and COS buckets) are subject to quantity limits in each region. Before replication, check whether the existing quota is sufficient in the target region. To increase the quota, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

#### Resources that do not need replication

Certain resources are not region-specific, such as CAM users/roles and policies, SSL certificates, and SSH keys. You need to filter them out during replication to avoid recreation.

