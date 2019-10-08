# 摘要

《腾讯云Terraform应用指南》系列文章旨在帮助腾讯云用户借助Terraform，轻松使用简单模板语言来定义、预览和部署云基础结构，让用户通过IaC，基于腾讯云的OpenAPI一键创建或销毁多路资源。利用Terraform这把利器，帮助用户节约资源开销，提高从部署到运维的自动化生产力。

作为该系列的第一篇文章，本文将介绍使用 Terraform 管理腾讯云资源的必要步骤。

# 一、安装Terraform

---

> `NOTES` 由于Terraform使用的过程中需要对文件进行添加、改写或删除等操作，为了保证安全及部署过程的鲁棒，我们建议开发者避免在本地使用Terraform对腾讯云资源进行管理，转而在腾讯云服务器进行相关操作更为便捷和可靠，实现业务百分百上云，享受腾讯云给您带来的优质体验。

下面是在腾讯云服务器上配置安装Terraform的详细步骤：

## 1、下载Terraform

官方提供了最新版本的Terraform[可用下载](https://www.terraform.io/downloads.html)，用户可以选择适合自己开发环境的下载包。若要安装其它的Terraform版本，请自行更改下载链接。

输入下载及安装命令行

```
    // download terraform
    $ wget https://releases.hashicorp.com/terraform/0.12.5/terraform_0.12.5_linux_amd64.zip
```

![下载Terraform](https://ask.qcloudimg.com/draft/5830525/aizam3xptw.png)

```
    // Install terraform
    $ unzip terraform_0.12.5_linux_amd64.zip
```

![安装Terraform](https://ask.qcloudimg.com/draft/5830525/zaupr4et7n.png)

## 2、配置环境变量

新建目录`downloads`，将安装好的`terraform`文件保存在该目录下

```
    // Move terraform
    $ mkdir downloads
    $ mv terraform downloads/
```

![将Terraform保存在自定义目录下](https://ask.qcloudimg.com/draft/5830525/0ki6ca017p.png)

进入配置文件`~/.profile`添加Terraform的环境变量

```
    $ vim ~/.profile

    // Add terraform PATH
    export PATH="$PATH:~/downloads"
```

![添加环境变量](https://ask.qcloudimg.com/draft/5830525/5f0mjxbbpd.png)

重新加载`~/.profile`文件

```
    $ source ~/.profile
```

查看Terraform当前版本

```
    $ terraform -version
```

![完成环境变量的配置](https://ask.qcloudimg.com/draft/5830525/8l1pkdepa3.png)

 有关如何在 Windows 上设置环境变量的说明，请这点击[这里](https://jingyan.baidu.com/article/9f63fb91d87fb0c8400f0e93.html)。

# 二、使用Terraform管理腾讯云

---

下面是Terraform管理腾讯云资源的具体方法：

## 1、Terraform工作流程

利用Terraform部署腾讯云资源的结构简图

![腾讯云Terraform工作流简图](https://ask.qcloudimg.com/draft/5830525/wa7ridhoqw.png)

① 一次性配置 `provider` 文件以支持Tencent Cloud的OpenAPI

② 使用Terraform配置语法生成 `.tf` 资源文件

③ 使用CLI实现腾讯云资源的管理

Terraform会将整个资源部署情况更新在 `*.tf.state` 文件中，让用户在前端控制台和后端平台都清晰的把控自己的云资源。

## 2、配置腾讯云provider文件

登录腾讯云，在访问管理中选择API秘钥管理

![腾讯云控制台](https://ask.qcloudimg.com/draft/5830525/um2jbqi3mu.png)

新建秘钥，获得Secret\_Id和Secret\_Key

![新建秘钥](https://ask.qcloudimg.com/draft/5830525/84g878sgt3.png)

在新目录下创建 `provider.tf` 文件，填入秘钥和区域信息

```
    $ vim provider.tf
    
    //provider.tf
    provider "tencentcloud" {
        secret_id  = "AKID****************"
        secret_key = "QdcM***************"
        region     = "ap-hongkong"
    }
```

![provider.tf](https://ask.qcloudimg.com/draft/5830525/9mcx0p6pyy.png)

保存该文件，执行 `terraform init` 初始化Terraform。此步骤，Terraform会自动检测 `provider.tf` 文件中的 `provider` 字段，发送请求到Terraform官方GitHub下载最新版本腾讯云资源的模块和插件，初始化成功时当前脚本的版本信息也会显示出来。

```
    // Initialize
    $ terraform init
```

![初始化成功](https://ask.qcloudimg.com/draft/5830525/4r4mv4dkmk.png)

当腾讯云脚本有新的版本发布时，可以通过 `terraform init -upgrade` 指令更新脚本，获取最新的应用。

同时，可以通过 `terraform plan` 预览将要完成的操作，准备好创建资源后，可以通过 `terraform apply` 进行资源部署，更多有关Terraform CLI的信息请点击[这里](https://www.terraform.io/docs/commands/index.html)。

> `NOTES` 将秘钥直接填入到.tf文件中是十分不安全的，在多用户共同管理资源时，不建议把腾讯云API 的秘钥直接写到源代码里，以免一不小心更新到公开的版本中，造成安全风险。

腾讯云提供了另一种更为安全可靠的方式，把秘钥信息放在环境变量中配置

```
    // Configure the secret key in the environment path
    $ export TENCENTCLOUD_SECRET_ID="your_fancy_accessid"
    $ export TENCENTCLOUD_SECRET_KEY="your_fancy_accesskey"
    $ export TENCENTCLOUD_REGION="ap-hongkong"
```

这样在 `provider.tf` 文件中就可以省略掉相关信息

```
    $ vim provider.tf
    
    // provider.tf
    provider "tencentcloud" {}
```

对于秘钥信息的配置，腾讯云会持续更新更加安全可靠的方法，致力于保护腾讯云用户的隐私安全。

## 3、部署腾讯云资源

这里提供一个在私有网络（VPC）下创建腾讯云服务器（CVM）的简单用例

创建服务器实例资源文件

```
    $ vim cvm.tf
    
    // Create a cvm
    resource "tencentcloud_instance" "cvm_test" {
        instance_name = "cvm-test"
        availability_zone = "ap-hongkong-1"
        image_id = "img-pi0ii46r"
        instance_type = "S2.SMALL1"
        system_disk_type = "CLOUD_PREMIUM"
      
        security_groups = [
            "${tencentcloud_security_group.sg_test.id}"
        ]

        vpc_id = "${tencentcloud_vpc.vpc_test.id"
        subnet_id = "${tencentcloud_subnet.subnet_test.id}"
        internet_max_bandwidth_out = 10
        count = 1
    }
```

![cvm.tf](https://ask.qcloudimg.com/draft/5830525/8ucwwo2w44.png)

这里可以看到，该服务器关联的安全组、私有网络和子网后面并没有直接填写具体参数信息，可以通过调用相关资源tf文件中的 `id` 字段内容实现具体的资源分配。本例中调用的就是安全组tf文件： `sg_test` ，私有网络tf文件： `vpc_test` ，路由表tf文件： `route_table.tf`和子网tf文件： `subnet_test` ，具体内容分别如下

创建私有网络资源文件

```
    $ vim vpc.tf
    
    // Create a vpc
    resource "tencentcloud_vpc" "vpc_test" {
        name = "vpc-test"
        cidr_block = "10.0.0.0/16"
    }
```

创建子网资源文件

```
    $ vim subnet.tf
    
    // Create a subnet
    resource "tencentcloud_subnet" "subnet_test" {
        name = "subnet-test"
        cidr_block = "10.0.1.0/24"
        availability_zone = "ap-hongkong-1"
        vpc_id = "${tencentcloud_vpc.vpc_test.id}"
        route_table_id = "${tencentcloud_route_table.rtb_test.id}"
    }
```

创建路由表资源文件

```
    $ vim route_table.tf
     
    // Create a route table
    resource "tencentcloud_route_table" "rtb_test" {
        name = "rtb-test"
        vpc_id = "${tencentcloud_vpc.vpc_test.id}"
    }
```

创建安全组和安全规则资源文件

```
    $ vim security_group.tf
    
    // Create a security group and rule
    resource "tencentcloud_security_group" "sg_test" {
        name = "sg-test"    
    }

    resource "tencentcloud_security_group_rule" "sg_rule_test" {
        security_group_id = "${tencentcloud_security_group.sg_test.id}"
        type = "ingress"
        cidr_ip = "0.0.0.0/0"
        ip_protocol = "tcp"
        port_range = "22,80"
        policy = "accept"
    }
```

执行 `terraform plan` 查看部署计划，一共有6个资源计划创建

![](https://ask.qcloudimg.com/draft/5830525/aqprzkly8a.png)

![terraform plan](https://ask.qcloudimg.com/draft/5830525/249g7iehqw.png)

这里参数前面的`+`代表新添加的资源，当销毁资源时，参数前面对应的符号会变为`-`；更改一些参数需要重新部署资源时，该资源前面的符号为`-/+`；在旧参数和新参数内容之间有`→`符号标识

![资源更改](https://ask.qcloudimg.com/draft/5830525/l8vddue0q5.png)

执行 `terraform apply` 进行资源创建

![询问是否创建资源](https://ask.qcloudimg.com/draft/5830525/i15qb31dq.png)

输入 `yes` ，显示成功创建资源

![创建资源成功](https://ask.qcloudimg.com/draft/5830525/wdspnxq47b.png)

回到控制台，可以看到刚刚部署的资源已经生效

![控制台同步创建操作](https://ask.qcloudimg.com/draft/5830525/7820bqejp0.png)

执行 `terraform destroy` 进行资源销毁

![询问是否销毁资源](https://ask.qcloudimg.com/draft/5830525/9bapbljfr8.png)

输入 `yes` ，显示成功销毁资源

![销毁资源成功](https://ask.qcloudimg.com/draft/5830525/wt6hze2znz.png)

控制台中也同步了销毁操作

![控制台同步销毁操作](https://ask.qcloudimg.com/draft/5830525/jgidthue2l.png)

# 三、写在最后

至此，使用Terraform管理腾讯云的准备工作都已完成，请持续关注腾讯云+社区，生态产品专栏《腾讯云Terraform应用指南》系列，生态产品团队将持续帮助用户快速入门，熟练掌握Terraform应用技巧。

> “Write, Plan, and create Infrastructure as Code" 让每一个腾讯云用户高效、快捷的部署资源。