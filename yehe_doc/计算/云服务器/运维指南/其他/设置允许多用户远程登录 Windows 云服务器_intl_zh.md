## 操作场景
本文档以 Windows Server 2016 R2 操作系统云服务器为例，指导您配置多用户远程登录 Windows 云服务器。

<dx-alert infotype="notice" title="">
微软提供的多用户远程登录功能试用期为120天，若未购买多用户登录授权（RDS CALs），则试用期结束后会导致无法通过远程桌面登录云服务器，只能通过 mstsc /admin 命令登录。Windows Server 默认允许2个用户同时登录，可满足多数需求。请您结合实际业务场景进行评估，若有强烈需求需配置多用户远程登录，请参考本文进行操作。
</dx-alert>


## 操作步骤

### 添加远程桌面服务
1. 登录 Windows 云服务器。
2. 在操作系统界面单击 <img src="https://qcloudimg.tencent-cloud.cn/raw/10c0728e4d194732be4eb6c1a95e0a8c.png" style="margin: -5px 0px;"/>，在弹出的界面中选择 <img src="https://qcloudimg.tencent-cloud.cn/raw/8a27d0993c99b2564c33df6bbabec4f7.png" style="margin: -5px 0px;"/>，打开“服务器管理器”。如下图所示：
    ![](https://main.qcloudimg.com/raw/66bb5237846f1dd79e3145bfd82d9257.png)
3. 单击**添加角色和功能**，弹出 “添加角色和功能向导” 窗口。
4. 在“添加角色和功能向导”窗口中，保持默认参数，连续单击三次**下一步**。
5. 在“选择服务器角色”界面，勾选“远程桌面服务”，单击**下一步**。如下图所示：
    ![](https://main.qcloudimg.com/raw/54d329c2667ac5c60ffdc2b74f1fc555.png)
6. 保持默认参数，连续单击两次**下一步**。
7. 在“选择角色服务”界面，勾选**远程桌面会话主机**。如下图所示：
    ![](https://main.qcloudimg.com/raw/8d24fd515bd363dc020257c2843c5562.png)
8. 弹出“添加 远程桌面会话主机 所需的功能”提示框。在提示框中，单击**添加功能**。如下图所示：
    ![](https://main.qcloudimg.com/raw/2a33d896c16b1d98012536cdc3776248.png)
9. 在“选择角色服务”界面，勾选“远程桌面授权”。如下图所示：
    ![](https://main.qcloudimg.com/raw/1c908dc77f50488387a2fdbfda08ba35.png)
10. 弹出 “添加 远程桌面授权 所需的功能” 提示框。在提示框中，单击**添加功能**。如下图所示：
    ![](https://main.qcloudimg.com/raw/d7aa066366b168ac8a7475155d34ea19.png)
11. 单击**下一步**。
12. 勾选“如果需要，自动重新启动目标服务器”，并在弹出的提示框中单击**是**。如下图所示：
    ![](https://main.qcloudimg.com/raw/df280b0a66470be404f114bd17c47d21.png)
13. 单击**安装**，等待远程桌面服务安装完成。


### 申请多用户登录授权许可证
1. 在操作系统界面单击 <img src="https://qcloudimg.tencent-cloud.cn/raw/10c0728e4d194732be4eb6c1a95e0a8c.png" style="margin: -5px 0px;"/>，在弹出的界面中选择 <img src="https://qcloudimg.tencent-cloud.cn/raw/8a27d0993c99b2564c33df6bbabec4f7.png" style="margin: -5px 0px;"/>，打开“服务器管理器”。
2. 在“服务器管理器”窗口中，选择右上角的**工具** > **Remote Desktop Services** > **远程桌面授权管理器**。
3. 在弹出的 “RD 授权管理器”窗口中，右键单击服务器所在行，并选择**激活服务器**。
4. 在弹出的“服务器激活向导”窗口中，单击**下一步**。
5. 在“连接方法”设置中，本文选择 “Web 浏览器”，并单击**下一步**。
您也可以结合实际情况选择其他连接方式。
6. [](id:Step6)在“许可证服务器激活”中，记录产品 ID 并访问 [远程桌面授权网站](https://activate.microsoft.com/)。
7. 在远程桌面授权网站中，选择“启用许可证服务器”，并单击**下一步**。
8. 输入 [步骤6](#Step6) 获取的产品 ID，并根据实际情况填写公司信息后，单击**下一步**。
9. 确认输入信息无误后，单击**下一步**。
10. [](id:Step10)记录许可证服务器 ID，并单击**是**。
11. 输入上一步获取的许可证服务器 ID，并按需选择授信息，填写公司信息后单击**下一步**。
本文授权信息以选择“企业协议”为例。
12. 选择产品类型，并输入数量及许可证授权信息。
<dx-alert infotype="explain" title="">
您可前往 [微软官网](https://www.microsoftstore.com.cn/software/software)，联系客服购买 RDS CALs 授权。
</dx-alert>
13. 确认信息无误后，单击**下一步**。
14. [](id:Step14)获取并记录密钥包 ID。
15. 单击**结束**。


### 激活远程桌面服务许可证服务器
1. 在操作系统界面单击 <img src="https://qcloudimg.tencent-cloud.cn/raw/10c0728e4d194732be4eb6c1a95e0a8c.png" style="margin: -5px 0px;"/>，在弹出的界面中选择 <img src="https://qcloudimg.tencent-cloud.cn/raw/8a27d0993c99b2564c33df6bbabec4f7.png" style="margin: -5px 0px;"/>，打开“服务器管理器”。
2. 在“服务器管理器”窗口中，选择右上角的**工具** > **Remote Desktop Services** > **远程桌面授权管理器**。
3. 在弹出的 “RD 授权管理器”窗口中，右键单击服务器所在行，并选择**激活服务器**。
4. 在弹出的“服务器激活向导”窗口中，单击**下一步**。
5. 在“连接方法”设置中，本文选择 “Web 浏览器”，并单击**下一步**。
您也可以结合实际情况选择其他连接方式。
6. 在“许可证服务器激活”中，输入 [步骤10](#Step10) 获取的许可证服务器 ID，并单击**下一步**。
7. “服务器激活向导”窗口中提示“你已完成服务器激活向导”时，单击**下一步**进入许可证安装步骤。


### 安装 RDS 客户端访问许可证
1. 在“许可证安装向导”页面中，确认许可证服务器信息，并单击**下一步**。
2. 在“获取客户端许可证密钥包”中，输入 [步骤14](#Step14) 获取的许可证服务器 ID，并单击**下一步**。
3. “许可证安装向导”窗口中提示“你已完成许可证安装向导”即表示已成功安装许可证。


### 配置远程桌面会话主机授权服务器
1. 在操作系统界面单击 <img src="https://qcloudimg.tencent-cloud.cn/raw/10c0728e4d194732be4eb6c1a95e0a8c.png" style="margin: -5px 0px;"/>，在弹出的界面中选择 <img src="https://qcloudimg.tencent-cloud.cn/raw/8a27d0993c99b2564c33df6bbabec4f7.png" style="margin: -5px 0px;"/>，打开“服务器管理器”。
2. 在“服务器管理器”窗口中，选择右上角的**工具** > **Remote Desktop Services** > **远程桌面授权诊断程序**。查看当前服务器状态。
3. 在操作系统界面右键单击 <img src="https://qcloudimg.tencent-cloud.cn/raw/10c0728e4d194732be4eb6c1a95e0a8c.png" style="margin: -5px 0px;"/>，在弹出菜单中选择**运行**。
4. 在“运行”窗口中输入 **gpedit.msc**，并按 **Enter** 打开计算机本地组策略。
5. 在左侧导航树中，选择**计算机配置** > **管理模板** > **Windows 组件** > **远程桌面服务** > **远程桌面会话主机** > **授权**，双击打开“使用指定的远程桌面许可服务器”。
6. 在弹出的“使用指定的远程桌面许可证服务器”窗口中，选择“已启用”，并在选项中输入“要使用的许可证服务器”，可输入云服务器公网 IP 或主机名。设置完成后单击**确定**。
7. 双击打开“设置远程桌面授权模式”。
8. 在弹出的“设置远程桌面授权模式”窗口中，选择“已启用”，并指定 RD 会话主机服务器的授权模式为“按用户”。设置完成后单击**确定**。
9. 重启云服务器。

至此您已完成多用户远程登录配置。

## 参考资料
- [License your RDS deployment with client access licenses (CALs)](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/rds-client-access-license)
- [Activate the Remote Desktop Services license server](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/rds-activate-license-server)
- [Install RDS client access licenses on the Remote Desktop license server](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/rds-install-cals)
