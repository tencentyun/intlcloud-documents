## 操作场景
如果您遗忘了密码，您可以在控制台上重新设置实例的登录密码。以下文档介绍了如何在云服务器管理控制台上修改实例登录密码。

<dx-alert infotype="notice" title="">

- 处于“已关机”状态的实例，可直接执行重置密码操作。
- 处于“运行中”状态的实例，通过控制台重置实例密码过程中会关闭实例。为了避免数据丢失，请提前规划好操作时间，建议在业务低谷时操作，将影响降到最低。
</dx-alert>


## 操作步骤
<dx-tabs>
::: 重置单台实例密码
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/index)。
2. 在实例的管理页面，根据实际使用的视图模式进行操作：
   - **列表视图**：选择需重置密码云服务器所在行右侧的**更多** > **密码/密钥** > **重置密码**。如下图所示：
   ![](https://qcloudimg.tencent-cloud.cn/raw/9317997308e40e06dcacc64cac24dd41.png)
   - **页签视图**：在需重置密码云服务器页面中，单击**重置密码**。如下图所示：
   ![](https://qcloudimg.tencent-cloud.cn/raw/032ecb8f3544bb17892decba6c955d8a.png)
3. 在“设置密码”步骤中，选择“用户名”的类型，填写需要重置密码的用户名，以及对应的“新密码”和“确认密码”，单击**下一步**。如下图所示：
<dx-alert infotype="notice" title="">
其中“用户名”类型默认为“系统默认”，并使用对应操作系统的默认用户名（Windows 系统默认用户名为 `Administrator`、Ubuntu 系统默认用户名为 `ubuntu`、其他版本 Linux 系统默认为 `root`）。如您需指定其他用户名，请选择“指定用户名”并输入对应用户名称。
</dx-alert>
<img src="https://main.qcloudimg.com/raw/420c83619601563c1c3c0c64c0bf533d.png"/>
4. 在“关机提示”步骤中，根据实例状态的不同，重置密码操作会有一定差别，具体如下：
 - 如果需要重置密码的实例为 “**运行中**” 状态，则勾选 “同意强制关机”，单击**重置密码**，完成重置。如下图所示：
![](https://main.qcloudimg.com/raw/ff478b4ab58289137c47356e00ad4c9a.png)
 - 如果需要重置密码的实例为 “**已关机**” 状态，则单击**重置密码**，完成重置。如下图所示：
![](https://main.qcloudimg.com/raw/950198759de0f3f937df8c6dc4b2a72d.png)   

:::
::: 重置多台实例密码

1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/index)。
2. 在实例的管理页面，勾选需要重置密码的云服务器，单击上方的**重置密码**。如下图所示：
![](https://main.qcloudimg.com/raw/38b9be9d0b1b6890f9b07852e91c8bd3.png)
3. 在“设置密码”步骤中，选择 “用户名” 的类型，填写需要重置密码的用户名，以及对应的“新密码”和“确认密码”，单击**下一步**。如下图所示：
<dx-alert infotype="notice" title="">
其中“用户名”类型默认为“系统默认”，并使用对应操作系统的默认用户名（Windows 系统默认用户名为 `Administrator`、Ubuntu 系统默认用户名为 `ubuntu`、其他版本 Linux 系统默认为 `root`）。如您需指定其他用户名，请选择“指定用户名”并输入对应用户名称。
</dx-alert>
![](https://main.qcloudimg.com/raw/1abf9af8eb892191acc3998bb5845dea.png)
4. 在“关机提示”步骤中，根据实例状态的不同，重置密码操作会有一定差别，具体如下：
 - 如果需要重置密码的实例为 “**运行中**” 状态，则勾选 “同意强制关机”，单击**重置密码**，完成重置。如下图所示：
![](https://main.qcloudimg.com/raw/ff478b4ab58289137c47356e00ad4c9a.png)
 - 如果需要重置密码的实例为 “**已关机**” 状态，则单击**重置密码**，完成重置。如下图所示：
![](https://main.qcloudimg.com/raw/950198759de0f3f937df8c6dc4b2a72d.png)    

:::
</dx-tabs>

## 相关问题
若您遇到重置 Windows 实例密码失败问题时，可参考 [Windows 实例：重置密码无效](https://intl.cloud.tencent.com/document/product/213/35720) 进行问题排查及解决。
