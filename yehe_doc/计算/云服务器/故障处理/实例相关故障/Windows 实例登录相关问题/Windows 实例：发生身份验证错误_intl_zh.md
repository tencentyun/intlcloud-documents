## 问题描述

通过远程桌面连接登录 Windows 实例时，出现以下报错：
- “发生身份验证错误，给函数提供标志无效”。
- “发生身份验证错误。要求的函数不受支持”。

## 问题分析

由于微软于2018年3月发布了一个安全更新，此更新通过更正凭据安全支持提供程序协议（CredSSP），以及在身份验证过程中验证请求的方式，修复 CredSSP 存在的远程执行代码漏洞。客户端和服务器都需要安装此更新，否则可能出现问题描述中的情况。
以下三种情况均会引起远程连接失败：

- 情况一：客户端未修补，服务器安装了安全更新，并且策略配置为 “强制更新的客户端”。
- 情况二：服务器未修补，客户端安装了安全更新，并且策略配置为 “强制更新的客户端”。
- 情况三：服务器未修补，客户端安装了安全更新，并且策略配置为 “缓解”。

## 解决方案



<dx-alert infotype="explain" title="">
若仅对客户端本地进行升级操作，请直接执行 [方案一：安装安全更新（推荐）](#step4)。
</dx-alert>


### 通过 VNC 登录云服务器

1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/index)。
2. 在实例的管理页面，找到目标云服务器实例，单击**登录**。如下图所示：
![云服务器列表页](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. 在弹出的 “标准登录 | Windows 实例” 窗口中，选择 **VNC登录**。
4. 在弹出的登录窗口中，选择左上角的 “发送远程命令”，单击 **Ctrl-Alt-Delete** 进入系统登录界面。如下图所示：
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)
5. 输入登录密码，按 **Enter**，即可登录到 Windows 云服务器。


### 方案一：安装安全更新（推荐）[](id:step4)

安装安全更新，可更新未修补的客户端/服务器端。不同系统对应的更新情况可参见 [CVE-2018-0886 | CredSSP 远程执行代码漏洞](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)。本方案以 Windows Server 2016 为例。
其他操作系统可参考以下操作进入 **Windows 更新**：

- Windows Server 2012：<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;width: 22px;"></img> > **控制面板** > **系统和安全** > **Windows 更新**
- Windows Server 2008：**开始** > **控制面板** > **系统和安全** > **Windows Update**
- Windows10：<img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin:-3px 0px;"></img> > **设置** > **更新和安全**
- Windows 7：<img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin:-3px 0px;width: 28px;"></img> > **控制面板** > **系统和安全** > **Windows Update**


1. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin:-3px 0px;"></img>，选择**设置**。
2. 在打开的 “设置” 窗口中，选择**更新和安全**。
3. 在 “更新和安全” 中，选择 **Windows 更新**，单击**检查更新**。
4. 根据界面提示，单击**开始安装**。
5. 安装完成后，重启实例，完成更新。

### 方案二：修改策略配置

在已安装安全更新的机器中，将**加密 Oracle 修正**策略设置为 “易受攻击” 。本方案以 Windows Server 2016 为例，其操作步骤如下：


<dx-alert infotype="notice" title="">
Windows 10 家庭版操作系统中，若没有组策略编辑器，可通过修改注册表来实现。操作步骤请参见 [方案三：修改注册表](#Plan3)。
</dx-alert>


1. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin:-3px 0px;"></img>，输入 **gpedit.msc**，按 **Enter**，打开 “本地组策略编辑器”。
<dx-alert infotype="explain" title="">
您也可使用 “**Win+R**” 快捷键打开运行界面。
</dx-alert>
2. 在左侧导航树中，选择**计算机配置** > **管理模板** > **系统** > **凭据分配**，双击**加密 Oracle 修正**。
3. 在打开的 “加密 Oracle 修正” 窗口中，选择**已启用**，并将**保护级别**设置为**易受攻击**。
4. 单击**确定**，完成设置。


### 方案三：修改注册表[](id:Plan3)

1. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin:-3px 0px;"></img>，输入 **regedit**，按 **Enter**，打开注册表编辑器。
<dx-alert infotype="explain" title="">
您也可使用 “**Win+R**” 快捷键打开运行界面。
</dx-alert>
2. 在左侧导航树中，依次展开**计算机** > **HKEY_LOCAL_MACHINE** > **SOFTWARE** > **Microsoft** > **Windows** > **CurrentVersion** > **Policies** > **System** > **CredSSP** > **Parameters** 目录。
<dx-alert infotype="explain" title="">
若该目录路径不存在，请手动创建。
</dx-alert>
4. 右键单击 **Parameters**，选择**新建** > **DWORD(32位)值**，并将文件名称命名为 “AllowEncryptionOracle”。
4. 双击新建的 “AllowEncryptionOracle” 文件，将 “数值数据” 设置为 “2”，单击**确定**。
6. 重启实例。

## 相关文档

- [CVE-2018-0886 | CredSSP 远程执行代码漏洞](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)
- [CVE-2018-0886 的 CredSSP 更新](https://support.microsoft.com/zh-cn/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)

