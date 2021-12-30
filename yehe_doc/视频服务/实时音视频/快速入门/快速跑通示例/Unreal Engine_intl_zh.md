本文主要介绍如何快速运行腾讯云 TRTC Demo（Unreal Engine）。

>! 目前 支持Windows、MacOs、ios、Android。

## 环境要求
- 建议Unreal Engine 4.27.1 及以上版本。
- **Android 端开发：**
  - Android Studio版本4.0及以上版本。
  - Visual Studio 2017 15.6版或更高。
  - 只支持真机调试
- **iOS & macOS 端开发：**
  - Xcode 11.0及以上版本。
  - osx 系统版本要求 10.11 及以上版本
  - 请确保您的项目已设置有效的开发者签名。
- **Windows 开发：**
    - 操作系统：Windows 7 SP1 或更高的版本（基于 x86-64 的 64 位操作系统）。
    - 磁盘空间：除安装 IDE 和一些工具之外还应有至少 1.64 GB 的空间。
    - 安装 [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)。

## 前提条件
您已 [注册腾讯云](https://intl.cloud.tencent.com) 账号，并完成实名认证。

## 操作步骤
[](id:step1)
### 步骤1：创建新的应用
1. 登录实时音视频控制台，选择【开发辅助】>【[快速跑通Demo](https://console.cloud.tencent.com/trtc/quickstart)】。
2. 单击【新建应用】输入应用名称，例如 `TestTRTC`；若您已创建应用可单击【选择已有应用】。
3. 根据实际业务需求添加或编辑标签，单击【创建】。
![](https://qcloudimg.tencent-cloud.cn/raw/f5fbbe70b7139531600e763846051a54.png)

>?
>- 应用名称只能包含数字、中英文字符和下划线，长度不能超过15个字符。
>- 标签用于标识和组织您在腾讯云的各种资源。例如：企业可能有多个业务部门，每个部门有1个或多个 TRTC 应用，这时，企业可以通过给 TRTC 应用添加标签来标记部门信息。标签并非必选项，您可根据实际业务需求添加或编辑。

[](id:step2)
### 步骤2：下载 SDK 和 Demo 源码
1. 根据实际业务需求下载 SDK 及配套的 [Demo 源码](https://github.com/tencentyun/TRTCUnrealEngine)（有疑问可[在此处](https://github.com/tencentyun/TRTCUnrealEngine/issues)提issue单）。
2. 下载完成后，单击【已下载，下一步】。

[](id:step3)
### 步骤3：配置 Demo 工程文件
1. 进入修改配置页，根据您下载的源码包，选择相应的开发环境。
2. 找到并打开 `/TRTC_Demo/Source/debug/include/DebugDefs.h` 文件。
3. 设置 `DebugDefs.h` 文件中的相关参数：
<ul><li/>SDKAPPID：默认为 0 ，请设置为实际的 SDKAppID。
	<li/>SECRETKEY：默认为 "" ，请设置为实际的密钥信息。</ul>
	<img src="https://imgcache.qq.com/operation/dianshi/other/UE4.6a419c2e7f7085671529d3694cb99458527c2970.png"/>
4. 粘贴完成后，单击【已复制粘贴，下一步】即创建成功。
5. 编译完成后，单击【回到控制台概览】即可。

>?
>- 本文提到的生成 UserSig 的方案是在客户端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 Demo 和功能调试**。
>- 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/647/35166#Server)。

[](id:step4)
### 步骤4：编译打包运行
1. 双击打开 `/TRTC_Demo/TRTC_Demo.uproject`。
2. 编译运行调试：
<dx-tabs>
::: macOS\s端
1. File -> Package Project -> Mac
2. 配置权限。右击上一步编译出的 xxx.app 文件 - 选择 "显示包内容" 
![](https://qcloudimg.tencent-cloud.cn/raw/3eb106ee3307c206dff5314a43920132.png)
3. 进入 "Contents->Info.plist"
4. 选择 "Information Property List" 然后添加以下两个权限:
```
<key>NSCameraUsageDescription</key>
<string>授权摄像头权限才能正常视频通话</string>
<key>NSMicrophoneUsageDescription</key>
<string>授权麦克风权限才能正常语音通话</string>
```
5. 如果你现在在UE4的editor运行的话，需要找到 **UE4Editor.app** 文件并且按照上面步骤添加权限。
:::
::: Windows\s端
1. File->Package Project->Windows->Windows(64-bit)
![](https://imgcache.qq.com/operation/dianshi/other/win.ba79ccce59ae58718e6c35c16cdef55531456a70.png)
:::
::: iOS\s端
1. 在 iOS 上也需要以下权限：
```
Privacy - Camera Usage Description
Privacy - Microphone Usage Description
```
为了将上述权限添加到 info.plist 里，你可以在 **Edit->Project Settings->Platforms: iOS** 中，将 
```
<key>NSCameraUsageDescription</key>
<string>授权摄像头权限才能正常视频通话</string>
<key>NSMicrophoneUsageDescription</key>
<string>授权麦克风权限才能正常语音通话</string>
```
添加到 Additional Plist Data 里。
2. 最后打包项目。File -> Package Project -> iOS
:::
::: Android\s端
1.开发调试：详见 [Android快速入门](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/GettingStarted/)
2.打包项目：详见 [打包Android项目](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/)
:::
</dx-tabs>
## Demo运行
Demo 里面提供了一对一视频通话的实现，可以测试和作为调用参考，API 文档参见 [C++ 全平台 API](https://intl.cloud.tencent.com/document/product/647/35131)。
>? UI 可能会有部分调整更新，请以最新版为准。

![](https://qcloudimg.tencent-cloud.cn/raw/e81338b3f3cf22c73744bcfbcf8955d2.png)

## TRTC全平台 C++ API文档
[中文文档](https://liteav.sdk.qcloud.com/doc/api/zh-cn/md_introduction_trtc_zh_Cplusplus_Brief.html)

[英文文档](https://liteav.sdk.qcloud.com/doc/api/en/md_introduction_trtc_en_Cplusplus_Brief.html)

## 常见问题
### 如何查看 TRTC 日志？
TRTC 的日志默认压缩加密，后缀为 `.xlog`。地址如下：
- **iOS 端**：sandbox 的 `Documents/log`。
- **Android 端**：
	- 6.7及之前的版本：`/sdcard/log/tencent/liteav`。
	- 6.8之后的版本：`/sdcard/Android/data/包名/files/log/tencent/liteav/`。

### macos UE4 editor闪退
请确认在您的**UE4Editor.app** info.plist 中设置了音视频权限
```
<key>NSCameraUsageDescription</key>
<string>授权摄像头权限才能正常视频通话</string>
<key>NSMicrophoneUsageDescription</key>
<string>授权麦克风权限才能正常语音通话</string>
```

### 安卓“Attempt to construct staged filesystem reference from absolute path"”报错
关闭UE4项目，打开cmd
>adb shell
>cd sdcard
>ls (you should see the UE4Game directory listed)
>rm -r UE4Game
重新编译项目
