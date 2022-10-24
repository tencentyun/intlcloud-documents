We offer three types of media SDK (RT-Cube) licenses: **live stream publishing**, **UGSV**, and **video playback**. For their billing details, see [Billing Overview](https://www.tencentcloud.com/document/product/647/50553). After purchasing a license, you can bind it in the [TRTC console](https://console.tencentcloud.com/trtc/license), the [CSS console](https://console.tencentcloud.com/live/license), or the [VOD console](https://console.tencentcloud.com/vod/license) to activate a new capability or extend the validity of an existing capability. The capabilities different licenses can activate are as follows:

| License | Capabilities            |
| -------------------- | ----------------------- |
| Live stream publishing     | Live stream publishing + Video playback |
| UGSV       | UGSV (Lite/Standard) + Video playback |
| Video playback | Video playback |

>! Starting from v10.1, the live stream publishing license and UGSV license can also activate the video playback capability. This means you can now use the video playback capability of the Player SDK with a live stream publishing license or UGSV license.

**This document uses the live stream publishing license as an example** to show you how to activate a capability using a trial or official license, and how to extend the validity of an existing capability.

[](id:test)
## Trial License

[](id:creat_test)
### Applying for a trial license

You can apply for a trial license (valid for 28 days) for the live stream publishing capability for free.

>? If you apply for a trial license on `2022-10-01 11:34:55`, it will expire 28 days later on `2022-10-28 00:00:00`.


In the console, you can either **create a trial license for a new application** or **activate a new capability for trial for an existing application**.
<dx-tabs>
::: Create a new trial license
1. Log in to the [TRTC console](https://console.tencentcloud.com/trtc), the [CSS console](https://console.tencentcloud.com/live/license), or the [VOD console](https://console.tencentcloud.com/vod/license) and click **Create trial license**.
![](https://qcloudimg.tencent-cloud.cn/raw/4507bd038c2a6e43cf91205383a1904f.png)
2. Enter an app name, a package name, and a bundle ID, select **Live stream publishing** (live stream publishing + video playback), and click **Create**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/af9ee37d5d25af0dc63221ff13cac3d6.png" style="zoom:67%;" />
3. After the trial license is successfully created, you will see the license URL and key, **which you need to pass in when initializing the SDK. Save a copy of the information**.
![](https://qcloudimg.tencent-cloud.cn/raw/67b33614792136bb295b3f47a024291f.png)
:::
::: Activate a new capability for trial for an existing application
Follow the steps below to activate **live stream publishing** (live stream publishing + video playback) for an existing application
1. Select an existing trial license and click **Try more capabilities**.
![](https://qcloudimg.tencent-cloud.cn/raw/026830658f7815b3d43432a501f2327a.png)
2. Select **Live stream publishing** (live stream publishing + video playback), and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/80d4dffff43aa6e299088d4a1b06db72.png)
:::
</dx-tabs>

>? 
>- You can click **Edit** to modify the bundle ID and package name bound to a trial license. After modification, click **Confirm**.
>- You can enter `-` if you don’t have a package name or bundle ID to bind yet.
>- A trial license is valid for 28 days. **You can apply for only one trial license for each capability**. To continue using the capability after a trial license expires, please purchase an [official license](#formal).

[](id:up_test)
### Upgrading to an official license
Follow the steps below to upgrade from a trial license to an official license (valid for one year):
1. Select an existing trial license and click **Upgrade** in the **Live stream publishing** area.
![](https://qcloudimg.tencent-cloud.cn/raw/6daf850b30a29014ab8cbd0f1a3f500f.png)
2. Click **Bind**, select a CSS traffic package or live stream publishing license which you have purchased, and click **Confirm**. If there are no license resources to bind, go to the [Purchase Page](https://buy.tencentcloud.com/license) to buy resources.
<img src="https://qcloudimg.tencent-cloud.cn/raw/087fb89a73fa9cffd80e0da4840783f6.png" alt="image" style="zoom: 50%;" />

[](id:formal)
## Official License
[](id:creat_formal)
### Purchasing an official license
1. Get an official license.
    - [Purchase](https://buy.tencentcloud.com/license) a [live stream publishing license](https://www.tencentcloud.com/document/product/647/50553). A purchased license is valid for one year after you bind it to an application (expires at 00:00:00 the next day).
2. Bind the license. You can either **bind the license to a new application** or **use it to activate live stream publishing for an existing application**.
<dx-tabs>
::: Bind an official license to a new application
1. Go to the [TRTC console](https://console.tencentcloud.com/trtc), the [CSS console](https://console.tencentcloud.com/live/license), or the [VOD console](https://console.tencentcloud.com/vod/license) and click **Create official license**.
![](https://qcloudimg.tencent-cloud.cn/raw/c7689b0f319f616a5e5e3ecf47267b65.png)
2. Enter an app name, a package name, and a bundle ID, select **Live stream publishing** (live stream publishing + video playback), and click **Next**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0ba8765431755c7807787782a157297.png" style="zoom:67%;" />
3. Click **Bind**, select a CSS traffic package or live stream publishing license which you have purchased, and click **Confirm**. If there are no license resources to bind, go to the [Purchase Page](https://buy.tencentcloud.com/license) to buy resources.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7ddb304e3d9e35959c0ba93a4138189a.png" style="zoom: 50%;" />

>? Before clicking **Confirm**, double-check the bundle ID and package name and make sure they are identical to what you submit to app stores. **The information cannot be modified after submission.**

4. After the official license is successfully created, you will see the license URL and key, which you need to pass in when initializing the SDK. Save a copy of the information.
![](https://qcloudimg.tencent-cloud.cn/raw/11fcae56bf1fcad8641ba789bdaaa517.png)
:::
::: Activate the capability for an existing application
1. Select an existing official license to which you want to add the **live stream publishing** capability (live stream publishing + video playback), and click **Activate more capabilities**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e1ab736ce2f80e74214dbca9a47f10fd.png" />
2. Select **Live stream publishing** (live stream publishing + video playback) and click **Next**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/1ff7b009cbce37598521d43df2cdae61.png" style="zoom: 67%;" />
3. Click **Bind**, select a CSS traffic package or live stream publishing license which you have purchased, and click **Confirm**. If there are no license resources to bind, go to the [Purchase Page](https://buy.tencentcloud.com/license) to buy resources.
<img src="https://qcloudimg.tencent-cloud.cn/raw/095e35fc6947c3399ca30d66d019b2f5.png" style="zoom:67%;" />
:::
</dx-tabs>

[](id:update_formal)
### Extend the validity of a capability
You can view the validity of a license bound in the [TRTC console](https://console.tencentcloud.com/trtc), the [CSS console](https://console.tencentcloud.com/live/license), or the [VOD console](https://console.tencentcloud.com/vod/license). You can also subscribe to notifications (**Message Center messages**/**email**/**SMS**) from the media SDKs in [Message Subscription](https://console.cloud.tencent.com/message/subscription). We will send you notifications 30 days, 15 days, seven days, and one day before a license expires. To avoid business interruption, please extend the validity of a capability in a timely manner. If a license has expired, you can follow the steps below to extend the validity of the corresponding capability:
1. Select the target license and click **Update validity** in the **Live stream publishing** area.
![](https://qcloudimg.tencent-cloud.cn/raw/534f5d02cb72a6950ad5d37fb3666c70.png)
2. Click **Bind**, select a CSS traffic package or live stream publishing license which you have purchased, and click **Confirm**. If there are no license resources to bind, go to the [Purchase Page](https://buy.tencentcloud.com/license) to buy resources.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6b1f279e5cd439386147c4f4aa96d852.png" style="zoom:50%;" />
3. Check the new validity period.

>! **You cannot modify the information of an official license.** If you want to use a license resource you purchased for a new application, click **Create official license** to bind it to a new application.