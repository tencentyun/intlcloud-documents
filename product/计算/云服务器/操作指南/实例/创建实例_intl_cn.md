## 前提条件
在创建 CVM 实例前，您需要完成以下工作：

- [注册腾讯云账号](https://intl.cloud.tencent.com/document/product/213/6090)，并完成[实名认证](https://cloud.tencent.com/document/product/378/3629)。
- 如果要创建网络类型为私有网络（VPC）的 CVM 实例，需要在目标地域[创建一个VPC](https://intl.cloud.tencent.com/document/product/215/8113)，并且在 VPC 下的目标可用区[创建一个子网](https://intl.cloud.tencent.com/document/product/215/8114)。
- 如果不使用系统自动创建的默认安全组，需要在目标地域[创建一个安全组](https://intl.cloud.tencent.com/document/product/213/18197#creating-a-security-group)并添加能满足您业务需求的安全组规则。
- 如果创建Linux实例时需要绑定SSH密钥对，需要在目标项目下[创建一个SSH密钥](https://intl.cloud.tencent.com/document/product/213/16691#creating-an-ssh-key)。
- 如果需要创建一个自定义镜像的 CVM 实例，需要[创建自定义镜像](https://intl.cloud.tencent.com/document/product/213/4942)或者[导入镜像](https://intl.cloud.tencent.com/document/product/213/4945)。



## 操作步骤
1) 登录[腾讯云官网](https://intl.cloud.tencent.com)，选择**Product** -> **Compute** -> **Cloud Virtual Machine**，单击 **Get Started** 按钮，进入云服务器购买页面。

2) 选择地域和可用区。

- 购买云服务时建议选择最靠近您客户的地域，可降低访问时延、提高访问速度。
- 当您需要多台云服务器时推荐分别选择不同可用区以达到容灾效果。
- 更多关于可选择地域和可用区介绍，请参考[地域和可用区](https://intl.cloud.tencent.com/document/product/213/6091)。

3) 选择系列、机型和配置。

- 腾讯云目前提供了系列1、系列2和系列3这三种不同的实例系列，为获得最佳性能，我们建议您在新建实例时使用最新一代类实例类型。更多关于系列的介绍，请参考[实例类型介绍](https://intl.cloud.tencent.com/document/product/213/11518#S)。
- 腾讯云目前提供了标准型、高 IO 型、内存型、计算型、GPU 计算型、FPGA 型、大数据型以及网络增强型的实例。更多关于机型的介绍，请参考[实例类型介绍](https://intl.cloud.tencent.com/document/product/213/11518#M)。
- 腾讯云目前提供了丰富的实例配置，不同机型对应的实例配置不同，更多关于实例配置的介绍，请参考[实例规格介绍](https://intl.cloud.tencent.com/document/product/213/11518)。

4) 选择镜像。

- 根据不同来源，腾讯云提供镜像类型有：公共镜像、自定义镜像、共享镜像。更多关于镜像类型的介绍，请参考[镜像类型介绍](https://intl.cloud.tencent.com/document/product/213/4941)。

5) 选择系统盘和数据盘。

- 系统盘：必选项，用于安装操作系统。您可以选择系统盘所用的云盘类型和容量。地域不同会影响可供选择的云盘类型。系统盘默认容量为50 GB。
- 数据盘：可选项。您可以选择在创建实例后再添加数据盘，也可以在购买时添加数据盘，并选择数据盘的云盘类型和容量。您可以创建空数据盘，也可以使用数据盘快照创建数据盘。
- 更多关于云硬盘的介绍，请参考[云硬盘分类](https://intl.cloud.tencent.com/document/product/213/4952)。

7) 选取带宽大小


- 如果需要为实例分配一个公网IP地址，需要设置一个大于0 Mbps的值。
- 使用流量是指服务器使用过程中产生的流量大小，网络费用仅取决于云服务器的出流量。为了防止突然爆发的流量产生较高的费用，可选择设置一个带宽上限，带宽上限对于网络单价完全无影响。

8) 用作公网网关
- 公网网关是开启了转发功能的云主机，在没有外网 IP 但需要进行Internet访问的云服务器可通过位于不同子网的公网网关来访问 Internet。公网网关主机将对公网流量进行源地址转换，所有云服务器访问外网的流量经过公网网关后，IP 都被转换为公网网关主机的 IP 地址。


9) 设置所属项目和选择安全组
- 如果您自己没有创建安全组，可选择【新建安全组】；如果已有安全组，请选择【已有安全组】。同时可以预览安全组规则，关于安全组规则的介绍，请参考[安全组](https://intl.cloud.tencent.com/document/product/213/12452)。


10) 设置主机名及登录方式。

- 主机名：您可以选择在购买时主机命名方式为【立即命名】并填入有语义的名字，但限制在 60 个字符以内。也可以选择【创建后命名】，则创建后的云服务器名字为“未命名”。该名字仅为在控制台显示的名字，并非云服务器的hostname。
- 登录方式：对于镜像选择了 Linux 类型的云服务器，登录方式可选【设置密码】、【立即关联密钥】以及【自动生成密码】。对于镜像选择了 Windows 类型的云服务器，登录方式可选【设置密码】以及【自动生成密码】。



11) 选择安装安全加固和云监控组件。

- 安全加固：免费开通DDoS防护、WAF和云镜主机防护，更多介绍，请参考[主机安全](https://intl.cloud.tencent.com/document/product/296/2221)。
- 云监控：免费开通云产品监控，安装组件获取主机监控指标并以监控图标形式展示，且支持设置自定义告警阈值等。更多介绍，请参考[云监控概述](https://intl.cloud.tencent.com/document/product/248)。

12) 确认设置并启动

- 选取您所需的子机数量，点击 **Enable** 启动您的云服务器。
- 云服务器创建好后用户将会收到站内信，内容包括实例名称、公网 IP 地址、内网 IP 地址、登录名、初始登录密码（选择自动生成密码情况下）等信息，您可以使用这些信息登录和管理实例。
