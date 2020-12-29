## 问题描述

Windows 操作系统的本地计算机通过 RDP 协议（如 MSTSC 方式）远程桌面连接登录 Windows 云服务器时，出现如下报错：
你的凭据无法工作，之前用于连接到 `XXX.XXX.XXX.XXX` 的凭据无法工作。请输入新凭据。
![](https://main.qcloudimg.com/raw/47a299873e3df8f1f160c1594fc56644.png)

## 处理步骤
>? 以 Windows Server 2012 操作系统的腾讯云云服务器为例，根据操作系统的版本不同，详细操作步骤略有区别。
> 请按照以下步骤依次排查，并在每一个步骤执行完后重新连接 Windows 云服务器验证问题是否解决，如未生效请继续执行下一步骤。

### 步骤1：修改网络访问策略
1. [使用 VNC 登录 Windows 实例](https://intl.cloud.tencent.com/document/product/213/32496)。
2. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;">，打开 “Windows PowerShell” 窗口。
3. 在 “Windows PowerShell” 窗口中，输入 **gpedit.msc**，按 **Enter**，打开“本地组策略编辑器”。
4. 在左侧导航栏中，依次展开【计算机配置】>【Windows 设置】>【安全设置】>【本地策略】>【安全选项】目录。
5. 找到并打开【安全选项】中的【网络访问：本地帐户的共享和安全模型】。如下图所示：
![](https://main.qcloudimg.com/raw/4ffb48c55d2f4aeedee127d97a4378ee.png)
6. 选择【经典 - 对本地用户进行身份验证，不改变其本来身份】，单击【确定】。如下图所示：
![](https://main.qcloudimg.com/raw/0f460bef7a7e35e1295149bb1f5f0d03.png)
7. 重新连接 Windows 云服务器，验证连接是否成功。
 - 是，任务结束。
 - 否，请执行步骤2：修改凭据分配。

### 步骤2：修改凭据分配
1. 在 “本地组策略编辑器” 的左侧导航栏中，依次展开【计算机配置】>【管理模板】>【系统】>【凭据分配】目录。
2. 找到并打开【凭据分配】中的【允许分配保存的凭据用于仅 NTLM 服务器身份验证】。如下图所示：
![](https://main.qcloudimg.com/raw/7643737fdfa2be299c21f6bc82b0165b.png)
3. 在打开的窗口中，选择【已启用】，并在 “选项” 的【显示】中输入`TERMSRV/*`，单击【确定】。如下图所示：
![](https://main.qcloudimg.com/raw/6a9af6aa4c3c3b3c4d1b9eba53d202b1.png)
4. 单击【确定】。
5. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;">，打开 “Windows PowerShell” 窗口。
6. 在 “Windows PowerShell” 窗口中，输入 **gpupdate /force**，按 **Enter**，更新组策略。如下图所示：
![](https://main.qcloudimg.com/raw/98d0b757e65e3617145c05513ba652dc.png)
7. 重新连接 Windows 云服务器，验证连接是否成功。
 - 是，任务结束。
 - 否，请执行步骤3：设置本地主机的凭据。

### 步骤3：设置本地主机的凭据
1. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > 【控制面板】>【用户帐户】，选择【凭据管理器】下的【管理 Windows 凭据】，进入 Windows 凭据界面。如下图所示：
![](https://main.qcloudimg.com/raw/2726e3d109fdaadd1d90a1f3e692601a.png)
2. 查看 Windows 凭据下是否有当前登录的云服务器凭据。
 - 如果没有，请执行下一步，添加 Windows 凭据。
 - 如果有，请执行步骤四：关闭云服务器密码保护共享。
3. 单击【添加 Windows 凭据】，进入添加 Windows 凭据界面。如下图所示：
![](https://main.qcloudimg.com/raw/87077862379ea7d9e86d5fdc7e0af1da.png)
4. 输入当前登录的云服务器 IP 地址，以及用户名和密码，单击【确定】。
>?
> - 云服务器 IP 地址即为云服务器公网 IP 地址，请参考 [获取公网 IP 地址](https://intl.cloud.tencent.com/document/product/213/17940) 获取。
> - Windows 实例默认用户名为 `Administrator`，密码由您在创建实例时设置。如果您忘记了登录密码，请参考 [重置实例密码](https://intl.cloud.tencent.com/document/product/213/16566) 进行密码重置。
>
5. 重新连接 Windows 云服务器，验证连接是否成功。
 - 是，任务结束。
 - 否，请执行步骤4：关闭云服务器密码保护共享。

### 步骤4：关闭云服务器密码保护共享
1. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > 【控制面板】>【网络和 Internet】>【网络和共享中心】>【更改高级共享设置】，进入高级共享设置界面。如下图所示：
![](https://main.qcloudimg.com/raw/d1cc8fd023642654091d1b152bb67ef1.png)
2. 展开【所有网络】页签，并在【密码保护的共享】下选择【关闭密码保护共享】，单击【保存更改】。
3. 重新连接 Windows 云服务器，验证连接是否成功。
 - 是，任务结束。
 - 否，请 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) 反馈。


