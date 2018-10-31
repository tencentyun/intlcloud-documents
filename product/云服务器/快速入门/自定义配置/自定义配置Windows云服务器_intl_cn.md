本文档介绍 Windows 云服务器的自定义配置方法。
不同于快速配置，自定义配置选项齐全，您可根据需求选择合适的配置。

<div id="page1"></div>
## 前提条件

 1. 开始自定义配置前，您需完成[【快速入门 Windows 云服务器】](https://cloud.tencent.com/document/product/213/2764#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E5.87.86.E5.A4.87.E4.B8.8E.E9.80.89.E5.9E.8B)文档中的步骤一。
 2. 登录腾讯云官网，选择【云产品】-【计算与网络】-【云服务器】，单击【立即选购】按钮，进入 [云服务器购买页面](https://buy.cloud.tencent.com/buy/cvm) 。
 3. 单击【自定义配置】，进入自定义配置界面。

<div id="page2"></div>
## 选择地域与机型
![image-20181010153405408](https://main.qcloudimg.com/raw/a71d4168ae6bd2b762badd4689c0aba7.png)
 1. 按量进行付费（无法购买按量付费云服务器的用户请先进行 [实名认证](https://console.cloud.tencent.com/developer/infomation) ）。

 2. 选择地域和可用区。当您需要多台云服务器时，选择不同可用区可实现容灾效果。

 3. 选择机型和配置。
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;根据底层硬件的不同，腾讯云目前提供了 **系列 1** 和 **系列 2** （下文也称为 **上一代实例** 和 **当前一代实例** ）两种不同的实例系列，不同的实例系列提供如下实例类型：

- 上一代实例类型：标准型S1，高IO型I1，内存型M1
- 当前一代实例类型：[标准型S2](https://cloud.tencent.com/doc/product/213/7154)，[高IO型I2](https://cloud.tencent.com/doc/product/213/7155)，[内存型M2](https://cloud.tencent.com/doc/product/213/7156)，[计算型C2](https://cloud.tencent.com/doc/product/213/7157)，[GPU型G2](https://cloud.tencent.com/document/product/560)，[FPGA型FX2](https://cloud.tencent.com/document/product/565) 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;为获得最佳性能，我们建议您在新建实例时使用当前一代实例类型。实例类型详细说明，请参见 [实例类型概述](https://cloud.tencent.com/document/product/213/7153) 。

>注意：
>不同的地域与可用区下的系列、机型会有所不同。

单击【下一步：选择镜像】按钮，进入选择镜像页面。

<div id="page3"></div>
## 选择镜像
![image-20181010105754025](https://main.qcloudimg.com/raw/ae628bc9aea84e55b0a691bb59de1b4a/image-20181010105754025.png)
 1. 选择镜像提供方。
腾讯云提供公共镜像、自定义镜像、共享镜像、服务市场，您可参考 [镜像类型](https://cloud.tencent.com/document/product/213/4941) 文档进行选择。
对于刚开始使用腾讯云的用户，推荐选择公共镜像，其中包含了正版 Windows 操作系统，后续运行环境自行搭建。

 2. 选择操作系统：选择 Windows。

 3. 选择系统版本。
-  适合于运行 Windows 下开发的程序，如 .NET。 
-  支持 SQL Server 和其他更多数据库（需自行安装）。 

单击【下一步：选择存储与网络】按钮，进入选择存储与网络页面。

<div id="page4"></div>
## 选择存储与网络
![image-20181009174426285](https://main.qcloudimg.com/raw/5cfedc485adae3943823ed7920f26aad.png)
 1. 选择硬盘类型和数据盘大小。

  腾讯云提供云硬盘、本地硬盘、SSD云硬盘三种种类型。（均默认 50GB 系统盘，系统盘大小任选）
- 云硬盘：采用一盘三备的分布式存储方式，数据可靠性高
- SSD云硬盘：SD 云盘基于全 NVMe SSD 存储介质，利用腾讯云 CBS 三副本分布式存储技术，提供低时延、高随机 IOPS、高吞吐量的 I/O 能力及数据安全性 高达 99.9999999% 的高性能存储。满足对 IO 性能有较高要求的使用场景。
- 本地硬盘：处在云服务器所在的物理机上的存储设备，可以获得较低的时延，但存在单点丢失风险。具体对比可以参考 [产品分类](https://cloud.tencent.com/document/product/362/2353#.E5.90.84.E7.A7.8D.E5.9D.97.E5.AD.98.E5.82.A8.E8.AE.BE.E5.A4.87.E7.9A.84.E5.AF.B9.E6.AF.94) 。

 2. 选择网络类型。
腾讯云提供基础网络或私有网络两种可选。
- 基础网络：适合新手用户，同一用户的云服务器内网互通。
- 私有网络：适合更高阶的用户，不同私有网络间逻辑隔离。

	>**注意：**
	> Windows 云服务器无法作为 [公网网关](http://cloud.tencent.com/doc/product/215/%E7%BD%91%E5%85%B3#1.-公网网关) 使用，需要公网网关的用户请参考 [Linux 云服务器快速入门](https://cloud.tencent.com/document/product/213/10133?!preview=&lang=cn)。

 3. 选择公网带宽。
腾讯云提供  按带宽计费  或  按使用流量计费  两种可选。
- 按带宽计费：选择固定带宽，超过本带宽时将丢包。适合网络波动较小的场景。
- 按使用流量计费：按实际使用流量收费。可限制峰值带宽避免意外流量带来的费用，当瞬时带宽超过该值时将丢包。适合网络波动较大的场景。

  4. 选择服务器数量。


单击【下一步：设置信息】按钮，进入设置信息页面。

<div id="page5"></div>
## 设置信息
![image-20181009174512418](https://main.qcloudimg.com/raw/08f3348cb809b812cd9bde269e21ce41.png)
 1. 命名主机：您可选择创建后命名，也可立即命名。

 2. 登录信息设置：您可设置密码，也可自动生成。设置的密码可在创建后修改，自动生成的密码将会以站内信方式发送。

 3. 选择安全组（**确保登录端口 3389 开放**，更多信息见 [安全组](http://cloud.tencent.com/doc/product/213/%E5%AE%89%E5%85%A8%E7%BB%84)） 。

单击【Enable】按钮，即可进入 [控制台](https://console.cloud.tencent.com/cvm) 查收您的云服务器。

云服务器创建好后将会收到站内信，内容包括实例名称、公网 IP 地址、内网 IP 地址、登录名、初始登录密码等信息。您可以使用这些信息登录和管理实例，也请尽快更改您的 Windows 登录密码保障主机安全性。

单击 [这里](https://cloud.tencent.com/document/product/213/2764#.E6.AD.A5.E9.AA.A4.E4.B8.89.EF.BC.9A.E7.99.BB.E5.BD.95-windows-.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8) ，继续 Windows 云服务器的登录、格式化与分区数据盘等后续配置。
