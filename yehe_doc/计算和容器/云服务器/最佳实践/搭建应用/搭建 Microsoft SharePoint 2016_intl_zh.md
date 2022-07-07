## 操作场景
本文档介绍如何在云服务器实例上搭建 Microsoft SharePoint 2016。

## 示例软件版本
本文在示例步骤中使用的云服务器实例硬件规格如下：
- vCPU：4核
- 内存： 8GB

本文在示例步骤中使用如下软件版本：
- 操作系统：Windows Server 2012 R2 数据中心版 64位英文版
- 数据库：SQL Server 2014

## 前提条件
已购买 Windows 云服务器。如果您还未购买云服务器，请参考 [快速配置 Windows 云服务器](https://intl.cloud.tencent.com/document/product/213/10516)。

## 操作步骤

### 步骤1：登录 Windows 实例
[使用 RDP 文件登录 Windows 实例（推荐）](https://intl.cloud.tencent.com/document/product/213/5435)。您也可以根据实际操作习惯，[使用远程桌面连接登录 Windows 实例](https://intl.cloud.tencent.com/document/product/213/32498)。


### 步骤2：添加 AD、DHCP、DNS、IIS 服务[](id:AddAD_DHCP_DNS_IIS)
1. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>，打开服务器管理器。
2. 在左侧导航栏中，选择**本地服务器**，找到 **IE 增强的安全配置**。如下图所示：
![](https://main.qcloudimg.com/raw/c2b0791555bbc910cea70732c75daa0f.png)
3. 关闭 **IE 增强的安全配置**。如下图所示：
![](https://main.qcloudimg.com/raw/6acbf171bc703100401e48e362539b21.png)
4. 在左侧导航栏中，选择**仪表盘**，单击**添加角色和功能**，打开 “添加角色和功能向导” 窗口。
5. 在 “添加角色和功能向导” 窗口中，保持默认配置，连续单击3次**下一步**。
6. 在 “选择服务器角色” 界面，勾选 **Active Directory 域服务**、**DHCP 服务器**、**DNS 服务器**和 **Web 服务器(IIS)**，并在弹出的窗口中单击**添加功能**。如下图所示：
![](https://main.qcloudimg.com/raw/a2bb1c86c9277ca870c629ecf5b0d3f5.png)
7. 单击**下一步**。
8. 在 “选择功能” 界面，勾选“.NET Framework 3.5 功能”，并在弹出的窗口中单击**添加功能**。如下图所示：
![](https://main.qcloudimg.com/raw/bf47abbb95ad42b9d6c720c3bb2c846b.png)
9. 保持默认配置，连续单击6次**下一步**。
10. 确认安装信息，单击**安装**。
11. 待完成安装后，重启云服务器。


### 步骤3：配置 AD 服务
1. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>，打开服务器管理器。
2. 在服务器管理器窗口中，单击 <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img>，选择**将此服务器提升为域控制器**。如下图所示：
![](https://main.qcloudimg.com/raw/1e6aa1d75044898357709909bb969c6f.png)
3. [](id:step14)在打开的 “Active Directory 域服务配置向导” 窗口中，将 “选择部署操作” 设置为**添加新林**，输入根域名，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/017acc0e5939632f3808698f36320fd2.png)
4. [](id:step15)设置目录服务还原模式（DSRM）密码，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/078672b95294790e4985108bd58d8504.png)
5. 保持默认配置，连续单击4次**下一步**。
6. 单击**安装**。

### 步骤4：配置 DHCP 服务
1. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>，打开服务器管理器。
2. 在服务器管理器窗口中，单击 <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img>，选择**完成 DHCP 配置**。如下图所示：
![](https://main.qcloudimg.com/raw/4c65a7990acc647866d73c1b5ba20a6c.png)
3. 在打开的 “DHCP 安装后配置向导” 窗口中，单击**下一步**。
4. 保持默认配置，单击**提交**，完成安装配置。如下图所示：
![](https://main.qcloudimg.com/raw/4162a8fbde1b7af1d8fadacaa61965cf.png)
5. 单击**关闭**，关闭向导窗口。

### 步骤5：安装数据库 SQL Server 2014

1. 在云服务器中打开浏览器，并访问 SQL Server 2014 官网下载 SQL Server 2014 安装包。
<dx-alert infotype="explain" title="">
您也可以通过第三方网站或其他合法渠道获取 SQL Server 2014 安装包。
</dx-alert>
2. 双击打开 “Setup.exe” 文件打开 SQL Server 安装向导，进入安装选项卡界面，单击**全新 SQL Server 独立安装或向现有安装添加功能**。如下图所示：
![](https://main.qcloudimg.com/raw/f2cc33aef5ec2662238ffeca56d08a7d.png)
3. 输入产品密钥，单击**下一步**。
4. 勾选“我接受许可条款”，单击**下一步**。
5. 保持默认配置，单击**下一步**。
6. 完成安装检查，单击**下一步**。
7. 保持默认配置，单击**下一步**。
8. 在 “功能选择” 界面，单击**全选**，选中全部功能，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/92eac7b681dae5937bafa484874ae122.png)
9. 在 “实例配置” 界面，选择**默认实例**，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/2bf1682b927b66224c574435ee35e7af.png)
10. 在 “服务器配置” 界面，配置 SQL Server 数据库引擎服务和 SQL Server Analysis Services 服务的帐号和密码，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/1310d9db077772be6dad6f58a698273e.png)
 - 将 “SQL Server 数据库引擎” 的帐户名设置为 “NT AUTHORITY\NETWORK SERVICE”。
 - 将 “SQL Server Analysis Services” 的帐户名和密码设置为 [步骤2：添加 AD、DHCP、DNS、IIS 服务](#AddAD_DHCP_DNS_IIS) 中 [14](#step14) - [15](#step15) 设置的域账户及密码。
11. 在 “数据库引擎” 界面，单击**添加当前用户**，将当前帐号作为 SQL Server 的管理员帐号，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/90ac80988b45a6b08650d97fd0d08c09.png)
12. 在 “Analysis Services 配置” 界面，单击**添加当前用户**，为当前帐号添加 Analysis Services 的管理员权限，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/5fda4e9b2ac31d8394ab0dfa14847d73.png)
13. 保持默认配置，单击**下一步**。
14. 在 “Distributed Replay 控制器” 界面，单击**添加当前用户**，为当前帐号添加 Distributed Replay 控制器的权限，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/2b67cc38051c51cb88ba7bbb740027b3.png)
15. 保持默认配置，单击**下一步**直至安装完成。


### 步骤6：安装 SharePoint 2016

1. 在云服务器中打开浏览器，并访问 Microsoft SharePoint 2016 官网下载 Microsoft SharePoint 2016 安装包。
2. 打开 Microsoft SharePoint 2016 镜像文件，双击准备工具的可执行文件 `prerequisiteinstaller.exe`，安装 Microsoft SharePoint 2016 准备工具。如下图所示：
![](https://main.qcloudimg.com/raw/1c6c2e0970ea456bbabd4a77ef454a5e.png)
3. 在打开的 Microsoft SharePoint 2016 产品准备工具向导窗口中，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/4b42cde60ca558a7c905c6f8031e3a50.png)
4. 勾选“我接受许可协议的条款”，单击**下一步**。
5. 等待完成安装必备组件，单击**完成**，重启云服务器。如下图所示：
![](https://main.qcloudimg.com/raw/a8c14625c359decb9941511e267ea2a6.png)
6. 打开 Microsoft SharePoint 2016 镜像文件，双击安装文件 `setup.exe`，开始安装 Microsoft SharePoint 2016。如下图所示：
![](https://main.qcloudimg.com/raw/2614739955551657148d9c3a72e566df.png)
7. 输入产品密钥，单击**继续**。
8. 勾选“我接受此协议的条款”，单击**继续**。
9. 选择安装目录（本示例中保持默认设置，您可以根据实际情况选择相应安装目录），单击**立即安装**。如下图所示：
![](https://main.qcloudimg.com/raw/3ea703e1632ec78b3f8f4b961c189208.png)
10. 待安装完成后，勾选“立即运行 SharePoint 产品配置向导”，单击**关闭**。如下图所示：
![](https://main.qcloudimg.com/raw/368fa9a4cdb3b47a77c554db855737e0.png)

### 步骤7：配置 SharePoint 2016

1. 在运行的 SharePoint 产品配置向导中，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/73aa25130b0e24e6784760a28d6d8fe2.png)
2. 在弹出的提示框中，单击**是**，允许在配置过程中重启服务。
3. 选择**创建新的服务器场**，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/b66da626c4883f2f2fb1b75bce6042f6.png)
4. 配置数据库设置和指定数据库访问账户信息，单击**下一步**。如下图所示：
由于 Sharepoint 的数据库在本机，所以填写本机的数据库及帐户。
![](https://main.qcloudimg.com/raw/d1ccac780ddb9fb308b071fe385ad3f6.png)
5. 配置指定服务器场的密码，单击**下一步**。
6. 将 “多服务器场” 设置为**前端**，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/c23051f73ae543002bc9c15d3d2b3387.png)
7. 设置 Sharepoint 管理中心的端口号（本示例以10000端口号为例，您可以根据实际情况设置端口号），单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/c7622761e6eb45b1935fccc851379b29.png)
8. 查看并确认 Sharepoint 配置，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/8d97c6aff42bb8b27fb3e108fa3d16d8.png)
9. 待 Sharepoint 完成配置后，单击**完成**。

