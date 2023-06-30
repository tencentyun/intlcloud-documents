## 操作场景

在 Windows Server 操作系统上，需要配置高性能电源管理，才能支持实例软关机，否则云服务器控制台只能通过硬关机的方式关闭实例。本文档以 Windows Server 2012 操作系统为例，介绍配置电源管理的方法。

## 操作说明

修改电源管理不需要重启计算机。

## 操作步骤

1. [使用 RDP 文件登录 Windows 实例（推荐）](https://intl.cloud.tencent.com/document/product/213/5435)。您也可以根据实际操作习惯，[使用远程桌面连接登录 Windows 实例](https://intl.cloud.tencent.com/document/product/213/32498)。
2. 通过 Windows 实例内的 IE 浏览器访问腾讯云内网，并下载腾讯云电源修改和配置工具。
下载地址为：`http://mirrors.tencentyun.com/install/windows/power-set-win.bat`
例如，将腾讯云电源修改和配置工具（power-set-win.bat）下载至 C: 盘。
3. 使用管理员命令行工具（CMD）打开 power-set-win.bat。如下图所示：
![](https://main.qcloudimg.com/raw/22f81122e1188fc83ed4b1100a7469bc.png)
4. 执行以下命令，查看当前电源管理方案。
```
powercfg -L
```
返回如下结果：
 ![](https://main.qcloudimg.com/raw/54ceb4faddc8745b30556621268ac318.png)

4. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> >**控制面板**>**系统和安全**>**电源选项**，打开电源选项窗口。
5. 在电源选项窗口中，单击**更改计划设置**。如下图所示：
![](https://main.qcloudimg.com/raw/54183c1f9d914789b986781b8a4da6ec.png)
6. 在打开的 “编辑计划设置” 窗口中，修改显示器和硬盘的空闲关闭时间。如下图所示：
 ![](https://main.qcloudimg.com/raw/f0b7f447d90fe50ef829a10dab0029c6.png)

