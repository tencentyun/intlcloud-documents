## Adaptive Resolution
This document describes how to support adaptive resolution for cloud applications. This feature can be used to adapt to different client resolutions. 
### Flowchart
![](https://staticintl.cloudcachetci.com/yehe/backend-news/sinj239_PRELIM__%E5%BA%94%E7%94%A8%E4%BA%91%E6%B8%B2%E6%9F%93_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US%20%281%29.png)

### Directions
1. [](id:step1) Set the application to window capturing mode in [Application management](https://console.tencentcloud.com/car/application). For more information, see [Using Window Capturing Mode](https://www.tencentcloud.com/document/product/1158/50549).
2. [](id:step2) Set the application to borderless windowed mode and enable adaptive resolution.
>!
>- An application is not in the borderless windowed mode when displayed in the fullscreen mode. A fullscreen application has full control over the monitor resolution. In this case, a crash may occur when the monitor resolution is modified.
>- To differentiate between borderless windowed mode and fullscreen mode, you can press **Alt+Tab**. Borderless windowed applications do not cause the monitor to flicker when the window is switched, while fullscreen applications do the opposite.

3. [](id:step3) Call the [TCGSDK.start()](https://ex.cloud-gaming.myqcloud.com/cloud_gaming_web/docs_en/TCGSDK.html#start) API to start the CAR SDK, and [onConnectSuccess()](https://ex.cloud-gaming.myqcloud.com/cloud_gaming_web/docs_en/InitConfig.html#onConnectSuccess) callback will be triggered when the application connection is completed. We recommend waiting until that is complete before setting the resolution on the client. 

4. [](id:step4) After the client resolution is queried, call the [TCGSDK.setRemoteDesktopResolution()](https://ex.cloud-gaming.myqcloud.com/cloud_gaming_web/docs_en/TCGSDK.html#setRemoteDesktopResolution) API to set the cloud resolution.
5. The cloud resolution is modified, and applications will automatically adapt to the changes in the resolution.
6. Call the [onRemoteScreenResolutionChange()](https://ex.cloud-gaming.myqcloud.com/cloud_gaming_web/docs_en/InitConfig.html#onRemoteScreenResolutionChange) API to check whether the settings take effect.
