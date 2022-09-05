本文将为您介绍如何快速入门主机安全。


## 操作指南
1.登录 [主机安全控制台](https://console.intl.cloud.tencent.com/cwp) 。
2.单击左侧导航中的**主机列表**。

### 步骤1：安装主机安全客户端
选择左侧菜单中的 **未安装客户端（无防护）**，查看当前暂未安装主机安全客户端的主机。
![](https://qcloudimg.tencent-cloud.cn/raw/3b2fd4103cbb397f7f82ecf0d1a57b71.png)
单击操作列中的 **重新安装**，打开主机安全客户端安装指引，您可根据主机实际情况，选择合适的安装方式进行安装。

### 步骤2：处理客户端上报的安全事件
安装客户端后的主机，即为基础版防护，支持监控并告警异常登录、密码破解，且可在主机安全控制台对事件进行处理。
![](https://qcloudimg.tencent-cloud.cn/raw/87fee85d70ed0df94e7e16937e4a0f67.png)
解锁更多防护功能须升级版本，各版本功能特性请参见 [功能介绍与版本比较](https://intl.cloud.tencent.com/document/product/296/2222) 。


### 步骤3：故障排除
若主机遭遇入侵，可根据入侵类问题排查指南进行问题排查，恢复网站或系统的正常运行，请参见 [Linux 入侵类问题排查思路](https://intl.cloud.tencent.com/document/product/296/34230) 或 [Windows 入侵类问题排查思路](https://intl.cloud.tencent.com/document/product/296/34231)。

### 步骤4：卸载主机安全客户端
若您不再需要主机安全防护，可将其卸载，卸载方式如下：
- 控制台卸载
在 [主机列表](https://intl.cloud.tencent.com/document/product/296/49372) 的操作列中，单击**卸载**即可，确定卸载后10分钟左右同步最新状态。
- 系统卸载
  - Windows系统：依照路径 C:\Program Files\QCloud\YunJing\uninst.exe ，找到 uninst.exe 文件，双击即可卸载。
  - Linux系统：输入命令：if [ -w '/usr' ]; then /usr/local/qcloud/YunJing/uninst.sh ; else /var/lib/qcloud/YunJing/uninst.sh ; fi 即可卸载。
