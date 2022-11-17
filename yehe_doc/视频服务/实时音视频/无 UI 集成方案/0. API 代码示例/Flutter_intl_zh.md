本文主要介绍如何快速运行腾讯云 TRTC Demo（Flutter）。

>! 目前 Windows/MacOs 端暂不支持屏幕分享及设备选择功能。

## 环境要求
- Flutter 2.0 及以上版本。
- **Android 端开发：**
  - Android Studio 3.5及以上版本。
  - App 要求 Android 4.1及以上版本设备。
- **iOS & macOS 端开发：**
  - Xcode 11.0及以上版本。
  - osx 系统版本要求 10.11 及以上版本
  - 请确保您的项目已设置有效的开发者签名。
- **Windows 开发：**
    - 操作系统：Windows 7 SP1 或更高的版本（基于 x86-64 的 64 位操作系统）。
    - 磁盘空间：除安装 IDE 和一些工具之外还应有至少 1.64 GB 的空间。
    - 安装 [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)。

## 前提条件
您已 [注册腾讯云](https://intl.cloud.tencent.com) 账号。

## 操作步骤

### 步骤 1：创建新的应用

1. 登录实时音视频控制台，选择【[应用管理](https://console.tencentcloud.com/trtc/app)】。
2. 单击【创建应用】输入应用名称，例如 `APIExample`；若您已创建过应用，可以勾选【选择已有应用】，然后单击【下一步】。
   ![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)

### 步骤 2：下载示例代码

1. 选择无 UI 集成后，然后您可以根据自己的业务平台，前往【[Github](https://github.com/LiteAVSDK/TRTC_Flutter/tree/master/TRTC-Simple-Demo)】下载相关 SDK 及配套的 Demo 源码。
2. 下载完成后，单击【下一步】。
   ![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)

### 步骤 3：配置工程

1. 在示例工程跑通阶段，选择【调试阶段】即可，然后记录下您的 SDKAppID、Secret key。
   ![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. 打开下载完成的示例代码，找到并打开`/lib/debug/GenerateTestUserSig.dart`文件，设置`GenerateTestUserSig.dart`文件中的相关参数：
   > - SDKAPPID：默认为 PLACEHOLDER ，请设置为实际的 SDKAppID。
   > - SECRETKEY：默认为 PLACEHOLDER ，请设置为实际的 Secret key。
3. 此时工程配置已经完成，您可以单击【下一步】，

>？
>- 本文提到的生成 UserSig 的方案是在客户端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 TRTC-Simple-Demo 和功能调试**。
>- 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://www.tencentcloud.com/document/product/647/35166)。

### 步骤 4：编译运行

1. 执行`flutter pub get`
2. 编译、运行或调试项目工程。

#### Android 调试：

1. 可以执行`flutter run`
2. 可以使用 Android Studio（3.5 及以上的版本）打开源码工程，单击【运行】即可。

#### iOS 调试：

1. 执行`cd ios`
2. 执行`pod install`
3. 使用 XCode（11.0 及以上的版本）打开源码目录下的 `/ios` 工程，编译并运行 Demo 工程即可。

#### windows 调试：

1. 启用 windows 支持：`flutter config --enable-windows-desktop`
2. 执行`flutter run -d windows`

#### macOS 调试

1. 启用 macOS 支持：`flutter config --enable-macos-desktop`
2. 执行`cd macos`
3. 执行`pod install`
4. 执行`flutter run -d macos`


## 常见问题
### 如何查看 TRTC 日志？
TRTC 的日志默认压缩加密，后缀为 `.xlog`。地址如下：
- **iOS 端**：sandbox 的 `Documents/log`。
- **Android 端**：
	- 6.7及之前的版本：`/sdcard/log/tencent/liteav`。
	- 6.8之后的版本：`/sdcard/Android/data/包名/files/log/tencent/liteav/`。

### iOS 无法显示视频（Android 没问题）？
请确认在您的 info.plist 中，`io.flutter.embedded_views_preview` 是否为 YES。 

### Android Manifest merge failed 编译失败？
请打开 `/example/android/app/src/main/AndroidManifest.xml` 文件。
    
1. 将 `xmlns:tools="http://schemas.android.com/tools"` 加入到 manifest 中。
2. 将 `tools:replace="android:label"` 加入到 application 中。
![Illustration](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

>? 更多常见问题，请参见 [Flutter 相关问题](https://intl.cloud.tencent.com/document/product/647/39242)。

