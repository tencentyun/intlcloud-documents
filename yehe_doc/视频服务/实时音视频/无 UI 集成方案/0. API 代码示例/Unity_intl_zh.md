这个示例项目演示了如何在 Unity 中快速集成 TRTC SDK，实现在游戏中的音视频通话。

在这个示例项目中包含了以下功能：
- 加入通话和离开通话。
- 自定义视频渲染。
- 设备管理、音乐特效和人声特效。

>?
>- 具体 API 功能参数说明，请参见 [Unity API 概览](https://intl.cloud.tencent.com/document/product/647/40139)。
>- Unity 建议版本： 2020.2.1f1c1。
>- 目前支持 Android、iOS、Windows、Mac(Mac 还在内测中)平台。
>- 需要包含 `Android Build Support`、`iOS Build Support`、`Winodows Build Support` 和 `MacOs Build Support` 模块。
>- 其中 iOS 端开发还需要：
   - Xcode 11.0及以上版本。
   - 请确保您的项目已设置有效的开发者签名。

## 操作步骤

### 步骤 1：创建新的应用

1. 登录实时音视频控制台，选择【[应用管理](https://console.tencentcloud.com/trtc/app)】。
2. 单击【创建应用】输入应用名称，例如 `APIExample`；若您已创建过应用，可以勾选【选择已有应用】，然后单击【下一步】。
   ![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)

### 步骤 2：下载示例代码

1. 选择无 UI 集成后，然后您可以根据自己的业务平台，前往【[Github](https://github.com/LiteAVSDK/TRTC_Unity/tree/main/TRTC-Simple-Demo)】下载相关 SDK 及配套的 Demo 源码。
2. 下载完成后，单击【下一步】。
   ![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)

### 步骤 3：配置工程

1. 在示例工程跑通阶段，选择【调试阶段】即可，然后记录下您的 SDKAppID、Secret key。
   ![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. 打开下载完成的示例代码，找到并打开`TRTC-Simple-Demo/Assets/TRTCSDK/Demo/Tools/GenerateTestUserSig.cs`文件，设置`GenerateTestUserSig.cs`文件中的相关参数：
  - SDKAPPID：默认为 PLACEHOLDER ，请设置为实际的 SDKAppID。
  - SECRETKEY：默认为 PLACEHOLDER ，请设置为实际的 Secret key。
3. 此时工程配置已经完成，您可以单击【下一步】，

>?
>- 本文提到的生成 UserSig 的方案是在客户端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 TRTC-Simple-Demo 和功能调试**。
>- 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://www.tencentcloud.com/document/product/647/35166)。

### 步骤 4：编译运行

#### Android 平台

1. 配置 Unity Editor，单击【File】>【Build Setting】，切换至 Android。
![](https://main.qcloudimg.com/raw/4464eb891829e3505a59c8ec00cc2414.png)
2. 连接 Android 真机，单击【Build And Run】，Demo 就能跑起来。
3. 接口测试，需要先点击调用 enterRoom ，然后自行测试其他相关，数据展示窗口显示点击调用成功，另外一个窗口显示回调信息。

#### iOS 平台

1. 打开`TRTC 构建配置工具`（可在 Unity 编辑器顶部导航栏找到）
2. 点击`构建&配置 IOS`，等待项目生成完成
   ![](https://qcloudimg.tencent-cloud.cn/raw/d7aa3153469c10b2dfe35db31bebbbf2.png)
3. 使用 xcode 打开生成好的 Unity-iPhone.xcodeproj 项目
4. 下载[TRTC 底层 sdk](https://comm.qq.com/trtc/TRTC_9.7.0.11440_iOS.zip)，单击 General，选择 Frameworks,Libraries,and Embedded Content，单击底下的“+”号图标依次添加所需要动态库 FFmpeg.xcframework、SoundTouch.xcframework，选择 Embed & Sign。
   ![](https://imgcache.qq.com/operation/dianshi/other/unity.ca7b6e717bf7b34e4f08a7e688ff59bf49d92217.png)
5. 连接 iOS 真机进行调试

#### Windows 平台

1. 配置 Unity Editor，单击【File】>【Build Setting】，切换至 `PC, Mac & Linux Standalone`，Target Platform 选择 Windows。
   ![](https://main.qcloudimg.com/raw/580764f661c06cf71c4952727c409c5e.png)
2. 单击【 Build And Run】，Demo 就能跑起来。

#### macOS 平台

1. 配置 Unity Editor，单击【File】>【Build Setting】，切换至 `PC, Mac & Linux Standalone`，Target Platform 选择 macOS。
   ![](https://main.qcloudimg.com/raw/6f3f9c21aa9eeadd7a4e3be377b2a6b3.png)
2. 单击【 Build And Run】，Demo 就能跑起来。
3. 使用 Unity Editor 模拟器运行，先要安装 `Device Simulator Package`。
4. 单击【Window】>【General】>【Device Simulator】
   ![](https://main.qcloudimg.com/raw/79f707b89553528956a888f48b4d4d6d.png)

[](id:demo)
## Demo示例
Demo 里面包含了已上线的大部分 API，可以测试和作为调用参考，API 文档参见 [SDK API（Unity）](https://intl.cloud.tencent.com/zh/document/product/647/40139)。
>? UI 可能会有部分调整更新，请以最新版为准。

## 目录结构
```
├─Assets
├── Editor                        // Unity 编辑器脚本
│   ├── BuildScript.cs            // Unity 编辑器build菜单
│   ├── IosPostProcess.cs         // Unity 编辑器构建ios应用脚本
├── Plugins
│   ├── Android                   
│   │   ├── AndroidManifest.xml   //Android应用配置文件
├── StreamingAssets               // Unity Demo 音视频流文件
├── TRTCSDK
    ├── Demo                      // Unity 示例 Demo
    ├── SDK                       // TRTC Unity SDK
        ├── Implement             // TRTC Unity SDK 实现
        ├── Include               // TRTC Unity SDK 头文件
        └── Plugins               // TRTC Unity SDK 不同平台底层实现
            
```