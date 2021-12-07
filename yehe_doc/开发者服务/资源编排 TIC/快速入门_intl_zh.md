

为了让您快速了解 TIC（Tencent Cloud Infrastructure as Code）产品能力，本文将介绍 TIC 如下几个基本功能：

- [TIC 授权](#tic-.E6.8E.88.E6.9D.83)：授权 TIC 对云资源（CVM、COS、MySQL 等）的编排的权限。
- [新建资源栈](#.E6.96.B0.E5.BB.BA.E8.B5.84.E6.BA.90.E6.A0.88)：编辑资源栈代码，执行 Plan、Apply 操作，创建云资源，构建云基础环境。
- [查看云资源](#.E6.9F.A5.E7.9C.8B.E4.BA.91.E8.B5.84.E6.BA.90)：查看通过 TIC 创建的云资源列表。
- [销毁云资源](#.E9.94.80.E6.AF.81.E4.BA.91.E8.B5.84.E6.BA.90)：释放云资源，回到初始状态。


>!使用 TIC 产品是免费，但通过 TIC 创建的云资源（CVM、MySQL 等）却不是免费的，请您根据实际情况调整配置文件，确保不会产生意料之外的费用。

## TIC 授权

首次使用资源编排 TIC 服务时，需要您显示授权 TIC 编排腾讯云账号下的云资源，否则 TIC 将无法执行腾讯云资源的编排操作。

1. 登录 [TIC 控制台](https://console.cloud.tencent.com/tic)。
2. 在左侧菜单栏中，选择【平台设置】>【API 密钥】，进入 API 密钥管理页面。
3. 单击【TIC 授权】，在弹出的服务授权窗口中，单击【访问管理】，将跳转到访问管理 CAM 页面。
	 ![](https://main.qcloudimg.com/raw/31f1045cfc15d113845afb62444a2c2d.png)
4. 跳转到访问管理 CAM 页面后，单击【同意授权】，即可完成授权。
5. 授权成功，跳回到 TIC 页面，TIC 授权开启成功。
	![](https://main.qcloudimg.com/raw/d11560f5fb0305845f46a87599b8ea8c.png)

## 新建资源栈

<span id="step1"></span>

### 步骤1：模式选择

1. 在左侧菜单栏中，选择【资源编排】>【资源栈】，进入资源栈页面。
2. 单击【新建】，相关配置项如下说明：
 - **Provider**： 默认为 Tencent Cloud（腾讯云），当前仅支持 Tencent Cloud。
 - **地域**：选择资源栈的地域，即该资源栈下的所有的资源都将属于该地域，为了便于测试，选择 Chengdu（成园区），您也可以选择其他园区进行测试。
3. 指定新建资源栈的方式：
   - **URL**：目前仅支持 [腾讯云 COS](https://intl.cloud.tencent.com/document/product/436) 和 Github，并且每次仅支持获取一个文件。
   - **私有模板**：选择私有模板，了解更多模板详情，请参见 [模板管理](https://intl.cloud.tencent.com/document/product/1043/37185)。
   - **公共模板**：选择公共模板，了解更多模板详情，请参见 [模板管理](https://intl.cloud.tencent.com/document/product/1043/37185)。
   - **输入模板内容**：编辑模式，直接编辑基础架构代码，支持多文件编写。
   此处我们选择输入模板内容，从头构建资源栈配置。
![](https://main.qcloudimg.com/raw/b3a59abb630f7665aec21a5b1adc89c1.png)
4. 单击【下一步】，进行步骤2：参数配置。	 

### 步骤2：参数配置

TIC 参数配置兼容 Terraform 的 HCL 语法，关于 HCL 语法细节，请参见 [Terraform Configuration Language](https://www.terraform.io/docs/configuration/index.html)。

1. 创建资源参数配置文件。为了与现网真实运营环境保持一致，我们创建了2台 CVM 云服务器、1个 VPC、1个子网、1个路由表、1个安全组、1个云数据库 MySQL，分别创建了对应的配置文件为：cvm.tf、vpc.tf、subnet.tf、route_table.tf、security_group.tf、mysql.tf，文件的结构如下：
![](https://main.qcloudimg.com/raw/3e67d3e0260f9e582deca2639ba9223f.png)
2. 为了使模板更加通用，我们创建了 variable.tf，定义了默认地域为 ap-chengdu（成都），默认可用区为 ap-chengdu-1（成都一区）两个变量（variable），地域名称要与 [步骤1](#step1) 中选择的地域保持一致：
   ```
   // variable.tf
   variable "default_region" {
     type = string
     default = "ap-chengdu"
   }
   variable "default_az" {
     type = string
     default = "ap-chengdu-1"
   }
   ```
3. variable.tf 定义的变量 ，将在其他 tf 文件被引用，我们举 cvm.tf 为例对语法进行简要的说明，完整 tf 配置文件内容，请下载 [tic-demo-config.zip](https://tic-demo-1259649581.cos.ap-nanjing.myqcloud.com/templates/tic-demo-config.zip)。
   ```
   // Create cvm
   resource "tencentcloud_instance" "cvm_demo" {
     instance_name = "ajaxhe-cvm-demo"
     availability_zone = var.default_az
     image_id = "img-pi0ii46r"
     instance_type = "S2.SMALL1"
     system_disk_type = "CLOUD_PREMIUM"
     allocate_public_ip = true
   
     security_groups = [
       tencentcloud_security_group.sg_demo.id
     ]
   
     vpc_id = tencentcloud_vpc.vpc_demo.id
     subnet_id = tencentcloud_subnet.subnet_demo.id
     count = 2
   
     tags = {
       role = "cgi"
       env = "prod"
     }
   }
   ```
**resource "tencentcloud_instance"**：表示当前创建的云资源是 CVM 云服务器实例，关于云资源的说明，请参见 [资源类型](https://intl.cloud.tencent.com/document/product/1043/37186)。
	- cvm_demo：本地资源名称，用于跨云资源的引用。
	- instance_name：CVM 云服务器实例名称。
	- availability_zone：CVM 云服务器可用区，这里引用了 variable.tf  文件定义的 default_az 变量。
	- image_id：CVM 云服务器镜像ID，img-pi0ii46r 代表 Ubuntu Server 18.04.1 LTS 64位 系统（镜像 ID 可以在腾讯云控制台 [镜像列表](https://console.cloud.tencent.com/cvm/image?rid=16&imageType=PUBLIC_IMAGE) 页中获取）。
	- instance_type：[实例规格](https://intl.cloud.tencent.com/document/product/213/11518)。

 **system_disk_type**：系统盘类型，CLOUD_PREMIUM：表示高性能云硬盘，可参见 [云硬盘类型](https://intl.cloud.tencent.com/document/api/362/16312) 中的 DiskType 说明。
	- allocate_public_ip：是否配置公网访问 IP，true 表示配置公网访问 IP。
	- security_groups：CVM 云服务器绑定的安全组列表，tencentcloud_security_group.sg_demo.id 关联了 security_group.tf 定义的安全组。
	- vpc_id：CVM 云服务关联的私有网络，tencentcloud_vpc.vpc_demo.id 关联了 vpc.tf 中定义的 VPC。
	- count：属于语法保留字段，表示创建2台上述配置的 CVM 云服务器。
	- tags：标签，方便对云服务器进行归类。


### 步骤3：Plan

编写完配置文件后，单击【下一步】，进入【Plan】阶段，Plan 阶段主要完成配置语法校验，以及对即将进行资源变更操作进行预处理。
通过 Plan 执行的结果，可以看到当前配置变更将新建8个云资源，无资源更新（change）、销毁（Destory）操作：
![](https://main.qcloudimg.com/raw/d14df232e44296af17a18892a2354b94.png)


### 步骤4：Apply

Plan 结果符合预期：

1. 单击【下一步】，为新的资源栈补充名称、描述等信息：
![](https://main.qcloudimg.com/raw/20ad3f3a27c3a8dd72b5926881a2687c.png)
2. 单击【确认】，提示进行二次确认：
![](https://main.qcloudimg.com/raw/6176b9089361d770bc73a04c8f7ed826.png)
3. 再次【确认】后，执行 Apply 操作，开始执行云资源创建操作，页面自动跳转到【资源栈】>【事件】页面。APPLY_IN_PROGRESS 表示资源构建中，整个资源构建过程预计需要数分钟时间。
![](https://main.qcloudimg.com/raw/84bb9b982a3beb670ac7d80329cafa64.png)
4. 在【事件】页面，可单击右上角的刷新按钮刷新状态，当状态显示为：APPLY_COMPLETED 时，代表资源构建成功。
![](https://main.qcloudimg.com/raw/496cb13ee5e63a75e01799b77fb6b6f5.png)

## 查看云资源

1. 在 [资源栈](https://console.cloud.tencent.com/tic/stacks) 页面，找到您上述创建的资源栈，在其右侧单击【详情】，进入资源栈详情页面。
2. 单击【资源】，进入云资源管理页面，可以看到通过 TIC 管理的云资源列表：
![](https://main.qcloudimg.com/raw/797368480d77b609b65153ad00692fa5.png)
3. 【资源】页面仅仅展现了云资源最核心的几个字段，如果需要查看资源详情，可以访问云产品控制台，查看资源详情。例如可以在 [云服务器 CVM](https://console.cloud.tencent.com/cvm/instance/index?rid=1) 控制台页面中看到 TIC 创建的2个实例：
![](https://main.qcloudimg.com/raw/06174011acf8858928818770a1ddd1bc.png)


## 销毁云资源

使用 TIC 产品是免费，但通过 TIC 创建的云资源却不全是免费的，为了确保防止资源闲置带来资金开销，若资源仅仅作为体验用途，请尽快执行销毁（Destory） 操作，销毁相关云资源。

1. 进入 [资源栈](https://console.cloud.tencent.com/tic/stacks) 页面，选中需要销毁的资源栈，单击【销毁】。
![](https://main.qcloudimg.com/raw/4a470b03f2f97f861ec5a73665aa6bea.png)
2. 在 TIC 执行实际的资源销毁操作之前，会显示待销毁的资源信息，资源栈一旦被销毁，资源栈中所有的资源将无法恢复。
![](https://main.qcloudimg.com/raw/3c4c448baeb017e3dadae9a87bfe08d5.png)
3. 单击【Destroy】，将再次弹出弹窗进行销毁确认，单击「确认」，TIC 将开始资源销毁操作，销毁过程如图所示：
![](https://main.qcloudimg.com/raw/f1a241eb14f218cf1dd820e1d6c78d66.png)
5. 稍等几分钟，云资源销毁完成：
![](https://main.qcloudimg.com/raw/4ed698e0d87e561c2e09f4a25474502f.png)
6. 单击【完成】，返回到资源栈列表页面，资源栈显示是完成销毁状态：DESTROY_COMPLETED。
![](https://main.qcloudimg.com/raw/9950499ff6dea48d49d090408f2c8009.png)

