
本文档主要介绍如何快速使用 Windows 系统的云服务器实例的相关功能，引导新手快速了解腾讯云云服务器的创建和配置。

<div id="page1"></div>
## 步骤一：准备与选型
### 注册腾讯云账号
新用户需在腾讯云官网进行 [注册](https://intl.cloud.tencent.com/register) ，注册指引可参考 [如何注册腾讯云](/doc/product/378/9603) 。

### 确定云服务器所在地域及可用区
地域选择原则：
 - 靠近用户原则。
请根据您的用户所在地理位置选择云服务器地域。云服务器越靠近访问客户，越能获得较小的访问时延和较高的访问速度。比如：您的用户大部分位于北美洲时，多伦多地域是较好的选择。
 - 内网通信同地域原则。
同地域内，内网互通；不同地域，内网不通。需要多个云服务器内网通信的用户须选择相同云服务器地域。
相同地域下的云服务器可以通过内网相互通信（内网通信，免费）。
不同地域之间的云服务器不能通过内网互相通信（通信需经过公网，收费）。

### 确定云服务器配置方案
您可以在[【更多机型】](https://intl.cloud.tencent.com/document/product/213/7153)中根据实际需要比较各配置方案。当然您也可以在购买云服务器之后，根据您的需求随时进行 [配置升级](/doc/product/213/%E8%B0%83%E6%95%B4CVM%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE#1.-配置升级) 或 [配置降级](/doc/product/213/%E8%B0%83%E6%95%B4CVM%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE#2.-配置降级) 。

### 确定付费方式
腾讯云提供按量付费模式。详见 [计费模式说明](/doc/product/213/2180) 。
若您选择按量付费，则需先完成 [实名认证](https://console.cloud.tencent.com/developer/infomation) 。

<div id="page2"></div>
## 步骤二：创建 Windows 云服务器
本步骤介绍 Windows 云服务器的创建。

 1. 登录腾讯云官网，进入【Products】-【Computer】-【Cloud Virtual Machine】，单击【Experience】按钮，进入 [云服务器购买页面](https://console.cloud.tencent.com/cvm/index) 单击【Create】开始选购。

 2. 选择地域和机型。靠近您客户的地域可降低访问延迟，提高下载速度。

    ![image-20181009174217646](https://main.qcloudimg.com/raw/820aa02738c2d69b70090083e292eb4b.png)

 3. 选择镜像。选择符合需求的 Windows 操作系统。

    ![image-20181010105754025](https://main.qcloudimg.com/raw/ae628bc9aea84e55b0a691bb59de1b4a/image-20181010105754025.png)

 4. 选择储存和公网带宽。若不需要连接到公网，带宽值选 0 。

    ![image-20181009174426285](https://main.qcloudimg.com/raw/5cfedc485adae3943823ed7920f26aad.png)

 5. 设置安全组、账户名和登录方式。

    ![image-20181009174512418](https://main.qcloudimg.com/raw/08f3348cb809b812cd9bde269e21ce41.png)

 6. 确定服务器设置并选择服务器数量。

    ![image-20181009174613350](https://main.qcloudimg.com/raw/05578198df6ea198935c89b56546ecb8.png)

查看站内信请见下一步骤。

<div id="Inter-Page">  </div>
## 步骤三：登录 Windows 云服务器
本部分操作介绍登录 Windows 云服务器的常用方法，不同情况下可以使用不同的登录方式，此处介绍控制台登录，更多登录方式请见 [登录 Windows 实例](/doc/product/213/5435) 。

### 前提条件
登录到云服务器时，需要使用管理员帐号和对应的密码。

 * 管理员账号：对于 Windows 类型的实例，管理员帐号统一为 Administrator
 * 密码：快速配置中，初始密码由系统随机分配。在下一环节（查看站内信及云服务器信息）中，具体查看操作。
   更多内容请参考 [登录密码](/doc/product/213/6093) 。
### 查看站内信及云服务器信息
完成云服务器的购买和创建后，云服务器的实例名称、公网 IP 地址、内网 IP 地址、登录名、初始登录密码等信息都将以 [站内信](https://console.cloud.tencent.com/message) 的方式发送到账户上。

 1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/index) 。登录后即可看到公网 IP 地址、内网 IP 地址等信息。

 2. 单击右上角【站内信】。

 3. 站内信页面即可查看新创建的云服务器，及登录名与密码等信息。如下图黄色高亮区域：

    ![image-20181009175141548](https://main.qcloudimg.com/raw/a52108b18b1ab2313a8b92661e3e4782.png)


### 控制台登录云服务器
  1. 在云服务器列表的操作列，单击【Log In】选择合适的登录方式：
    ![image-20181010111640723](https://main.qcloudimg.com/raw/04e1ff6540b7eeed3a9e27146c7f2f93/image-20181010111640723.png)

  2. 这里以 VNC 登陆为例。点击 Log In Now

  ![image-20181010111900601](https://main.qcloudimg.com/raw/9866809b13da4987f8396e75edce253d/image-20181010111900601.png)

 3. 通过单击左上角发送 Ctrl-Alt-Delete 命令进入系统登录界面：
    ![](https://main.qcloudimg.com/raw/9231fba98927bca92af8d3ad3bc43485/win1.png)

 4. 输入帐号（Administrator）和站内信中的初始密码（或您修改后的密码）即可登录。

>**注意：**
>该终端为独享，即同一时间只有一个用户可以使用控制台登录。

<div id="page4"></div>
## 步骤四：分区与格式化数据盘

这里以 Windows Server 2012 R2 DataCenter 64bit EN 为例进行格式化说明。

### 前提条件

 - 已购买数据盘的用户，需要格式化数据盘才可使用。未购买数据盘的用户可以跳过此步骤。
 - 请确保您已完成步骤三操作，登录到云服务器。

### 格式化数据盘

1. 通过步骤三介绍的方法登录 Windows 云服务器。

2. 单击【Start】-【Server Manager】-【Tools】-【Computer Management】-【Storage】-【Disk Management】。

   ![image-20181010120646197](https://main.qcloudimg.com/raw/f988db357f1daae7b6d2c35a7d20bc68/image-20181010120646197.png)

   ![image-20181010120817988](https://main.qcloudimg.com/raw/5cf806c9fff23e19fbede4a7334c4e37/image-20181010120817988.png)

   ![image-20181010121020945](https://main.qcloudimg.com/raw/4e43326adbcb539af918ef40302b24da/image-20181010121020945.png)

3. 在磁盘1上右键单击，选择【Online】，若已经联机，可跳过该步骤：

   ![image-20181010143149191](https://main.qcloudimg.com/raw/5df2d05297fb9cf617f426369ecd0421/image-20181010143149191.png)

4. 右键单击，选择【Initialize Disk】：

   ![image-20181010143401964](快速入门Windows云服务器_intl_cn.assets/image-20181010143401964.png)


根据分区方式的不同，选择【GPT】或【MBR】，单击【OK】按钮：

> 注意：
> 磁盘大于 2TB 时仅支持 GPT 分区形式。若您不确定磁盘后续扩容是否会超过该值，则建议您选择 GPT 分区；若您确定磁盘大小不会超过该值，则建议您选择 MBR 分区以获得更好的兼容性。*
>
> ![image-20181010143526150](https://main.qcloudimg.com/raw/30d5a469940766d7aa36f6abad63f71c/image-20181010143401964.png)
>

### 磁盘分区（可选）

1. 在未分配的空间处右击，选择【New Simple Volume】：

   ![image-20181010143857453](https://main.qcloudimg.com/raw/d2facf7e459d89501a18bfe339415666/image-20181010143857453.png)

2. 在弹出的“新建简单卷向导”窗口中，单击【Next】：

   ![image-20181010144003766](https://main.qcloudimg.com/raw/21aef4b0d7d4a54b960fd564216fefbe/image-20181010144003766.png)

3. 输入分区所需磁盘大小，单击【Next】：

   ![image-20181010144105132](https://main.qcloudimg.com/raw/b7f9354ff8a28543dbe3777af8f595c0/image-20181010144105132.png)

4. 输入驱动器号，单击【Next】：

   ![image-20181010144206060](快速入门Windows云服务器_intl_cn.assets/image-20181010144206060.png)

5. 选择文件系统，格式化分区，单击【Next】：

   ![image-20181010144307006](https://main.qcloudimg.com/raw/e4d65c61310e9515742143e3648605e5/image-20181010144206060.png)

6. 完成新建简单卷，单击【Finish】：

   ![image-20181010144335711](https://main.qcloudimg.com/raw/04716f7b2dd855513d8767236f43aa37/image-20181010144335711.png)

7. 在【Start】中打开【This PC】，查看新分区：

   ![image-20181010144445290](https://main.qcloudimg.com/raw/ded8b50737ffe1d6d342bf604d9a9474/image-20181010144445290.png)

**至此，您已完成 Windows 系统的云服务器的创建和基础配置。**
