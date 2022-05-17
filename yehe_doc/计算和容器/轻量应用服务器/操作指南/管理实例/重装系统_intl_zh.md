## 操作场景

重装系统相当于重新安装轻量应用服务器的操作系统（或操作系统加预置应用），达到将实例恢复至初始状态或全新安装的目的，是实例遭遇系统故障时的一种重要恢复手段。

<dx-alert infotype="explain" title="">
目前轻量应用服务器已支持敏感操作保护功能，可有效保障账号资源安全。重装系统属于敏感操作，您可前往 [安全设置](https://console.cloud.tencent.com/developer/security) 开启操作保护。
</dx-alert>




## 注意事项
 - **跨平台重装：** 
  - 目前仅支持中国内地区域实例进行跨平台重装，例如 Linux 实例重装为 Windows 实例，Windows 实例重装为 Linux 实例。其中，如 Linux 实例的系统盘小于40GB，则会因不满足 Windows Server 镜像的最小系统盘配置要求而无法跨平台重装。
  - 非中国内地区域实例仅支持同平台重装。
 - **数据备份：** 重装系统后，系统盘中的内容将会清空，重置为新镜像的初始状态。因此，您需要在重装前完成系统盘中重要数据和信息的备份。
 - **实例 IP：** 重装系统后，实例的公网 IP 不会改变。
 - **强制关机：** 重装系统过程中，实例将会自动关机（默认先尝试软关机，如果软关机失败，则会执行强制硬关机）。


## 操作步骤

1. 登录 [轻量应用服务器控制台](https://console.cloud.tencent.com/lighthouse/instance/index)。
2. 在服务器列表中，找到待重装系统的实例。根据实际的操作习惯，选择不同的方式进行重装。
 - 在实例卡片中，选择**更多** > **重装系统**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/dc9015130e76d6e42a8ff42d93658c95.png)
 - 单击实例卡片，进入实例详情页。在**概要**页签中，单击“镜像信息”中的**重装系统**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/ce759d182b030207c73ca36de9f6d102.png)
 - 单击实例卡片，进入实例详情页。在**应用管理**页签中，单击“应用信息”栏的**重装系统**。如下图所示：
<dx-alert infotype="explain" title="">
如轻量应用服务器实例未使用“应用镜像”，则不支持通过此方式重装系统。
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/013f084fab8164bcd95f7a2d2815d47c.png"/>
4. 在“重装系统”页面中，选择重装系统需要使用的镜像（系统镜像、应用镜像、Docker 基础镜像、自定义镜像及共享镜像均可），阅读重装确认事项，勾选“确认已了解以上内容，我确定已备份完成”，单击**确定**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/a14d73a12bec47a63f96e1e5390d8d89.png)

