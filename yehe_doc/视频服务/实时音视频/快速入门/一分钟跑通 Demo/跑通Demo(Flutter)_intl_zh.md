本文主要介绍如何快速运行腾讯云 TRTC Demo（Flutter）。

## 环境要求
- Flutter 1.12 及以上版本。
- Android 端开发：
  -  Android Studio 3.5及以上版本。
  -  App 要求 Android 4.1及以上版本设备。
- iOS 端开发：
  - Xcode 11.0及以上版本。
  - 请确保您的项目已设置有效的开发者签名。

## 前提条件

您已 [注册腾讯云](https://intl.cloud.tencent.com/document/product/378/17985) 账号，并完成 [实名认证](https://intl.cloud.tencent.com/document/product/378/3629)，未进行实名认证的用户无法购买中国大陆的实时音视频实例。

## 操作步骤

<span id="step1"></span> 
### 步骤1：创建新的应用
1. 登录实时音视频控制台，选择【开发辅助】>【[快速跑通Demo](https://console.cloud.tencent.com/trtc/quickstart)】。
2. 单击【立即开始】，输入应用名称，例如 `TestTRTC`，单击【创建应用】。

<span id="step2"></span> 
### 步骤2：下载 SDK 和 Demo 源码
1. 单击【[Github](https://github.com/c1avie/trtc_demo)】跳转至 Github，下载相关 SDK 及配套的 Demo 源码。
2. 下载完成后，返回实时音视频控制台，单击【我已下载，下一步】，可以查看 SDKAppID 和密钥信息。


<span id="step3"></span> 
### 步骤3：配置 Demo 工程文件
1. 解压 [步骤2](#step2) 中下载的源码包。
2. 找到并打开 `/lib/debug/GenerateTestUserSig.dart` 文件。
3. 设置 `GenerateTestUserSig.java` 文件中的相关参数：
  -  SDKAPPID：默认为 PLACEHOLDER ，请设置为实际的 SDKAppID。
	 SECRETKEY：默认为 PLACEHOLDER ，请设置为实际的密钥信息。
  -  返回实时音视频控制台，单击【粘贴完成，下一步】。
  -  单击【关闭指引，进入控制台管理应用】。

>!
>- 本文提到的生成 UserSig 的方案是在客户端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 Demo 和功能调试**。
>- 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/647/35166)。

### 步骤4：编译运行
1. 执行 `flutter pub get`。
2. 编译运行调试：

#### Android端
1. 执行 `flutter run`。
2. 使用 Android Studio（3.5及以上的版本）打开源码工程。
3. 单击【运行】即可。

#### iOS端
1. 使用 XCode（11.0及以上的版本）打开源码目录下的 `/ios工程`。
2. 编译并运行 Demo 工程即可。



## 常见问题

- [两台手机同时运行 Demo，为什么看不到彼此的画面？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que1)
- [防火墙有什么限制？](hhttps://intl.cloud.tencent.com/zh/document/product/647/39242#que2)
- [iOS 打包运行 Crash？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que3)
- [iOS 无法显示视频（Android 正常）？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que4)
- [更新 SDK 版本后，iOS CocoaPods 运行报错？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que5)
- [Android Manifest merge failed 编译失败？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que6)
- [因为没有签名，真机调试报错?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que7)
- [对插件内的 swift 文件做了增删后，build 时查找不到对应文件？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que8)
- [Run 报错“Info.plit, error: No value at that key path or invalid key path: NSBonjourServices”？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que9)
- [Pod install 报错？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que10)
- [Run 的时候 iOS 版本依赖报错？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que11)



