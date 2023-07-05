## 现象描述
适用 Windows 远程连接 Window 实例时出现如下图所示的提示：
![](https://main.qcloudimg.com/raw/8c79cadc3e14c9c4e0cbb5303b79f74a.png)

远程桌面由于以下原因之一无法连接到远程计算机：
1）未启用对服务器的远程访问
2）远程计算机已关闭
3）在网络上远程计算机不可用

确保打开远程计算机、连接到网络并且启用远程访问。


## 可能原因

导致出现以上提示的原因包括（不限于以下情况，请根据实际情况进行分析）：
- 实例处于非正常运行状态
- 无公网 IP 或公网带宽为0
- 实例绑定的安全组未放通远程登录端口（默认为3389）
- 远程桌面服务未启动
- 远程桌面设置问题
- Windows 防火墙设置问题

## 排查步骤


### 检查实例是否处于运行状态
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/index)。
2. 在实例的管理页面，查看实例是否处于“运行中”。如下图所示：
![CVM列表页](https://main.qcloudimg.com/raw/03cf75228bc468d2e436f876f229ebc9.png)
 - 是，请 [检查服务器是否设置公网 IP](#step01)。
 - 否，请启动该 Windows 实例。


### 检查服务器是否设置公网 IP[](id:step01)
在云服务器控制台检查服务器是否设置公网 IP。如下图所示：
![无公网IP](https://main.qcloudimg.com/raw/58c75d68372069652ec09ab93cfdbdc0.png)

 - 是，请 [检查是否购买公网带宽](#step02)。
 - 否，请 [申请弹性公网 IP 并进行绑定](https://intl.cloud.tencent.com/document/product/213/16586)。


###  检查是否购买公网带宽[](id:step02)
检查公网带宽是否为0Mb（最少1Mbps）。
 - 是，请参考 [调整网络](https://intl.cloud.tencent.com/document/product/213/15517)，建议将带宽调整到5Mbps或以上。
![](https://main.qcloudimg.com/raw/29b771d9de5d1ecdadb872c0378a31c7.png)
 - 否，请 [检查实例远程登录端口（3389）是否放通](#step03)。


### 检查实例远程登录端口（3389）是否放通[](id:step03)
1. 在云服务器控制台的实例管理页面，单击需要登录的实例 ID/实例名，进入该实例详情页面。
2. 在**安全组**页签下，检查实例的安全组是否放通远程登录接口（默认远程桌面端口：3389）。如下图所示：
![安全组](https://main.qcloudimg.com/raw/28b5f0a038dd354346745bd97f724350.png)
 - 是，请 [检查远程桌面服务](#step04)。
 - 否，请编辑对应的安全组规则，进行放通。操作方法请参考 [添加安全组规则](https://intl.cloud.tencent.com/document/product/213/34272)。

### 检查远程桌面服务[](id:step04)
1. [使用 VNC 登录实例](https://intl.cloud.tencent.com/document/product/213/32496)，检查 Windows 实例远程桌面服务是否开启。
<dx-alert infotype="explain" title="">
 以下操作以 Windows Server 2016 操作系统的实例为例。
</dx-alert>
2. 右键单击 <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;">，在弹出的菜单中选择**系统**。
3. 在打开的“系统”窗口中，选择**高级系统设置**。
4. 在打开的“系统属性”窗口中，选择**远程**页签，检查是否勾选“允许远程连接到此计算机”。
 - 是，请执行 [步骤5](#step04_5)。
 - 否，请勾选并单击**确定**。
5. [](id:step04_5) 右键单击 <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;">，在弹出的菜单中选择**计算机管理**。
6. 在打开的“计算机管理”窗口左侧菜单栏中，选择**服务和应用程序** > **服务**。
7. 在右侧的服务列表中，检查 **Remote Desktop Services** 是否启动。
 - 是，请执行 [步骤8](#step04_8)。
 - 否，请启动服务。
8. [](id:step04_8) 右键单击 <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;">，在弹出的菜单中选择**运行**。
9. 在弹出的“运行”窗口中，输入 **msconfig** 并单击**确定**。
10. 在打开的“系统配置”窗口中，检查是否勾选**正常启动**。
 - 是，请 [检查 Windows 实例的系统设置](#step05)。
 - 否，请勾选并单击**确定**。


### 检查 Windows 实例的系统设置[](id:step05)
1. [使用 VNC 登录实例](https://intl.cloud.tencent.com/document/product/213/32496)，排查 Windows 实例的系统设置。
<dx-alert infotype="explain" title="">
以下操作以 Windows Server 2012 操作系统的实例为例。
</dx-alert>
2. 右键单击 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px;"></img>，在弹出的菜单中选择**运行**。
3. 在弹出的“运行”中输入 **services.msc**，并按 **Enter**，打开 “服务” 窗口。
4. 双击打开 “Remote Desktop Services” 的属性，检查远程桌面服务是否已启动。如下图所示：
![Remote Desktop Service](https://main.qcloudimg.com/raw/6c781636c69eacae76a08b88f9e32b99.png)
 - 是，请执行 [步骤5](#step05_5)。
 - 否，请将 “启动类型” 设置为 “自动”，“服务状态” 设置为 “正在运行”（即单击**启动**，启动服务）。
5. [](id:step05_5)右键单击 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px;"></img>，在弹出的菜单中选择**运行**。
6. 在弹出的“运行”窗口中输入 **sysdm.cpl**，按 **Enter**，打开 “系统属性” 窗口。
7. 在 “远程” 页签中，检查远程桌面是否设置为 “允许远程连接到此计算机(L)”。如下图所示：
![远程设置](https://main.qcloudimg.com/raw/cbf2b2797bd48777008753f389574674.png)
 - 是，请执行 [步骤8](#step05_8)。
 - 否，请将远程桌面设置为 “允许远程连接到此计算机(L)”。
8. [](id:step05_8)单击 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px;"></img>，选择**控制面板**，打开控制面板。
9. 在“控制面板”中，选择**系统与安全** > **Windows 防火墙**，打开 “Windows 防火墙”。
10. 在 “Windows 防火墙”中，检查 Windows 防火墙状态。如下图所示：
![Windows 防火墙状态](https://main.qcloudimg.com/raw/e74937594a03c141e6e5ac753f025d91.png)
 - 为 “启用” 状态，请执行 [步骤11](#step05_11)。
 - 为 “关闭” 状态，请通过 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 反馈。
11. [](id:step05_11)在 “Windows 防火墙”中，单击**允许应用或能通过 Windows 防火墙**，打开 “允许的应用” 窗口。
12. 在“允许的应用”窗口中，检查“允许的应用和功能(A)”是否勾选“远程桌面”。如下图所示：
![勾选远程桌面](https://main.qcloudimg.com/raw/dfed8792ce1dd8b32bee4aaa02ef6bbf.png)
 - 是，请执行 [步骤13](#step05_13)。
 - 否，请勾选 “远程桌面”，放通“远程桌面”。
13. [](id:step05_13)在 “Windows 防火墙” 中，单击**启用或关闭 Windows 防火墙**，打开“自定义设置”窗口。
14. 在“自定义设置”窗口中，将“专用网络设置”和“公用网络设置”设置为“关闭 Windows 防火墙(不推荐)”。如下图所示：
![关闭](https://main.qcloudimg.com/raw/5d5f8c4d7b783bc1018e03368ae400bc.png)

若执行以上操作后仍无法通过远程桌面连接到 Windows 实例，请通过 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 反馈。



