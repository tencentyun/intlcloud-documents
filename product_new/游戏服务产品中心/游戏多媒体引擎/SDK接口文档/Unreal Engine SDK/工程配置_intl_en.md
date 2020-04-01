## Overview
This document describes how to configure a Unreal Engine project for the GME APIs for Unreal Engine.

## SDK Preparations
1. Download the applicable demo and SDK in [Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).
2. In the Unreal Engine project directory, open the `Plugins` folder (create it if it does not exist) and copy the SDK into it as shown below:
![](https://main.qcloudimg.com/raw/751894ab16c5262b7a99370cc7efd52c.png)
3. After importing, compile the plugin in Unreal Engine.
4. After compilation is completed, the following directories will appear in VS2015.
![](https://main.qcloudimg.com/raw/15421a160d0bd69d21f8343cdf3563e5.jpg)
5. Open Unreal Engine again, click **Edit** > **Plugins** to view the GME plugin.
![](https://main.qcloudimg.com/raw/60fb6340f6899e2c8fc6f4693193533e.png)
6. If you are using Unreal Engine v4.21 or higher, you need to add the following code after downloading the GME sample code for Unreal Engine:
```
AUEDemoLevelScriptActor::AUEDemoLevelScriptActor()
{
    PrimaryActorTick.bCanEverTick = true;
}
```

>Tick is disabled by default and must be enabled manually.

## Exporting for Different Platforms
Project configuration is required before you can export executables from Unreal Engine for different platforms:

| OS | Project Configuration           
| ------------- |:-------------:|
| Android |[Android Project Configuration](https://intl.cloud.tencent.com/document/product/607/10783)|
| iOS     	|[iOS Project Configuration](https://intl.cloud.tencent.com/document/product/607/10783)|
| macOS     	|[macOS Project Configuration](https://intl.cloud.tencent.com/document/product/607/10783)|
