本文档以 Windows Server 2012 操作系统为例，介绍 Windows 云服务器实例因重置密码失败或者不生效的排查方法和解决方案。

## 现象描述

- 重置云服务器密码后，提示“由于系统繁忙，您的实例重置实例密码失败(7617d94c)”。
- 重置云服务器密码后，新密码不生效，登录密码仍为原密码。


## 可能原因
导致重置云服务器密码失败或者不生效的可能原因如下：
- 云服务器中的 `cloudbase-init` 组件损坏、被修改、禁止或者未启动。
- 云服务器上安装了例如360安全卫士或火绒等第三方安全软件，则有可能因第三方安全软件拦截了重置密码组件 `cloudbase-init`，导致重置实例密码失效。


## 故障定位及处理

根据引起密码重置不成功的可能原因，提供以下两种检查方式：

### 检查 cloudbase-init 服务

1. 参考  [使用 VNC 登录 Windows 实例](https://intl.cloud.tencent.com/document/product/213/32496)，登录目标 Windows 实例。
2. 在操作系统界面，右键单击 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"></img>，选择【运行】，并在【运行】中输入 **services.msc**，并按 **Enter**，打开 “服务” 窗口。
3. 检查是否存在 `cloudbase-init` 服务。如下图所示：
![](https://main.qcloudimg.com/raw/2615f5c0e68a31174c16c9a80884455c.png)
 - 是，执行下一步。
 - 否，重新安装 `cloudbase-init` 服务。具体操作请参见 [Windows 操作系统安装 Cloudbase-Init](https://intl.cloud.tencent.com/document/product/213/32364)。
4. 双击打开 `cloudbase-init` 的属性。如下图所示：
![](https://main.qcloudimg.com/raw/10702cb2e359d6de36aec4960771c841.png)
5. 在【常规】页签，检查 `cloudbase-init` 的启动类型是否设置为【自动】。
 - 是，执行下一步。
 - 否，将 `cloudbase-init` 的启动类型设置为【自动】。
6. 切换至【登录】页签，检查 `cloudbase-init` 的登录身份是否选择为【本地系统帐户】。
 - 是，执行下一步。
 - 否，将 `cloudbase-init` 的登录身份设置为【本地系统帐户】。
7. 切换至【常规】页签，单击服务状态的【启动】，手动启动 `cloudbase-init` 服务并观察是否报错。
 - 是，[检查云服务器中安装的安全软件](#CheckSecuritySoftware)。
 - 否，执行下一步。
8. 在操作系统界面，右键单击 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"></img>，选择【运行】，并在【运行】中输入 **regedit**，并按 **Enter**，打开 “注册表编辑器” 窗口。
9. 在左侧的注册表导航中，依次展开【HKEY_LOCAL_MACHINE】>【SOFTWARE】>【Cloudbase Solutions】>【Cloudbase-Init】目录。
10. 找到【ins-xxx】下的全部 “LocalScriptsPlugin” 注册表，并检查 LocalScriptsPlugin 的数值数据是否为2。
![](https://main.qcloudimg.com/raw/75580b56e3a28fb9e0559372eb33ff11.png)
 - 是，执行下一步。
 - 否，将 LocalScriptsPlugin 的数值数据设置为2。
11. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"></img>，选择【这台电脑】，检查设备和驱动器中是否加载了 CD-驱动器。如下图所示：
![](https://main.qcloudimg.com/raw/8755719fb39bb5f841f4c32897545233.png)
 - 是，[检查云服务器中安装的安全软件](#CheckSecuritySoftware)。
 - 否，在设备管理器中启动 CD-ROM 驱动器。

<span id="CheckSecuritySoftware"></span>
### 检查云服务器中安装的安全软件

在已安装的安全软件，选择全盘扫描，检查是否云服务器有漏洞，以及检查 `cloudbase-init` 的核心组件是否被拦截。
- 如检查出云服务器有漏洞，请修复。
- 如检查出核心组件被拦截，请取消拦截。

`cloudbase-init` 组件检查及配置步骤如下：
1. 参考  [使用 VNC 登录 Windows 实例](https://intl.cloud.tencent.com/document/product/213/32496)，登录目标 Windows 实例。
2. 对应实际安装的第三方安全软件，恢复并设置 `cloudbase-init` 组件。


