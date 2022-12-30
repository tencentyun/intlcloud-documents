## 自适应分辨率
本节主要介绍云端应用如何支持自适应分辨率。当业务需要适配不同用户客户端的分辨率时，可以使用自适应分辨率的能力。
### 时序图
![](https://staticintl.cloudcachetci.com/yehe/backend-news/VGvx889_PRELIM__%E5%BA%94%E7%94%A8%E4%BA%91%E6%B8%B2%E6%9F%93_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US.png)

### 步骤说明
1. [](id:step1)业务需要在 [应用管理](https://console.tencentcloud.com/car/application) 中将应用配置为仅捕捉应用窗口模式，具体操作可参考使用[捕捉应用窗口模式](https://www.tencentcloud.com/document/product/1158/50549)。
2. [](id:step2)业务需要将应用设置为无边框模式并开启自适应桌面分辨率。
>!
>- 应用独占全屏不属于无边框模式，应用独占全屏时显示器分辨率是由应用控制的，此时强行修改桌面分辨率可能导致应用崩溃。
>- 区分无边框全屏和独占全屏，无边框全屏应用按 Alt+Tab 切换窗口不会导致显示器闪烁，独占全屏应用切换会有闪烁的现象。

3. [](id:step3)业务客户端调用 [TCGSDK.start()](https://ex.cloud-gaming.myqcloud.com/cloud_gaming_web/docs_en/TCGSDK.html#start) 接口启动云渲染应用，SDK 完成应用连接后会触发回调 [onConnectSuccess()](https://ex.cloud-gaming.myqcloud.com/cloud_gaming_web/docs_en/InitConfig.html#onConnectSuccess)，建议业务客户端在这之后设置分辨率。

4. [](id:step4)业务客户端获取分辨率后，调用 [TCGSDK.setRemoteDesktopResolution()](https://ex.cloud-gaming.myqcloud.com/cloud_gaming_web/docs_en/TCGSDK.html#setRemoteDesktopResolution) 接口设置云端分辨率。
5. 云端收到设置分辨率请求后，修改云端桌面分辨率，云端应用根据分辨率变化自适应修改。
6. 业务客户端可以在回调 [onRemoteScreenResolutionChange()](https://ex.cloud-gaming.myqcloud.com/cloud_gaming_web/docs_en/InitConfig.html#onRemoteScreenResolutionChange) 接口中获取分辨率设置是否生效。