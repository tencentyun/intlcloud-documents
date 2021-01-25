[](id:que1)
###  移动端（Andriod/iOS）支持哪几种系统音量模式？
支持2种系统音量类型，即通话音量类型和媒体音量类型：
- 通话音量，手机专门为通话场景设计的音量类型，使用手机自带的回声抵消功能，音质相比媒体音量类型较差， 无法通过音量按键将音量调成零，但是支持蓝牙耳机上的麦克风。
- 媒体音量，手机专门为音乐场景设计的音量类型，音质相比于通话音量类型要好，通过通过音量按键可以将音量调成零。 使用媒体音量类型时，如果要开启回声抵消（AEC）功能，SDK 会开启内置的声学处理算法对声音进行二次处理。 在媒体音量模式下，蓝牙耳机无法使用自带的麦克风采集声音，只能使用手机上的麦克风进行声音采集。

[](id:que2)
###  移动端 SDK 推流怎么设置1080p分辨率？
1080P在 TX_Enum_Type_VideoResolution 定义是114，直接设置分辨率传枚举值即可。

[](id:que4)
###  TRTC 移动端怎么实现录屏（屏幕分享）？	
- **Android 端**：Version 7.2 及以上版本支持手机录屏，具体实践方法请参见 [实时屏幕分享（Android）](https://intl.cloud.tencent.com/document/product/647/37337)。
- **iOS 端**：Version 7.2 及以上版本支持 App 内录屏；Version 7.6 及以上版本支持手机录屏和 App 内录屏。具体实践方法请参见 [实时屏幕分享（iOS）](https://intl.cloud.tencent.com/document/product/647/37338)。



[](id:que5)
###  TRTC Android 端能不能支持64位的 arm64-v8a 架构？
TRTC 6.3 版本开始已提供 arm64-v8a 架构 ABI 支持。


[](id:que7)
###  在 iOS 端是否支持 Swift 集成？
支持，直接按照支持集成三方库的流程集成 SDK 即可，还可以参考 [跑通Demo(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086)。


[](id:que9)
###  TRTC SDK 是否支持 iOS 后台运行？
支持，您只需选中当前工程项目，在 **Capabilities** 下的设置  **Background Modes** 为 **ON**，并勾选 **Audio，AirPlay and Picture in Picture**即可实现后台运行，详情如下图所示：
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

[](id:que10)
### iOS 端是否可以监听远端离开房间？
可以使用 [onRemoteUserLeaveRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28) 来监听用户离开房间事件，且该接口仅在 VideoCall 的所有用户和 LIVE 模式下的主播离开房间时会触发回调，观众离开房间不会有回调。 

[](id:que11)
### 手机锁屏状态，视频如何拨通？
实现离线接听等功能，详情请参见 [实现离线接听](https://intl.cloud.tencent.com/document/product/647/36068)。

[](id:que12)
### 是否支持 Android 和 Web 端互通？
支持。使用相同的 [SDKAppID](https://console.cloud.tencent.com/trtc/app)，并进入同一个房间进行通话。详情请参见下列文档链接配置 Demo：
- [跑通 Demo（Android）](https://intl.cloud.tencent.com/document/product/647/35084)
- [跑通 Demo（桌面浏览器）](https://intl.cloud.tencent.com/document/product/647/35607)

[](id:que13)
### 主播和粉丝在直播过程中连麦，是否双方都可以主动发起连麦？
双方都可以主动发起，观众和主播发起逻辑一致，具体操作请参见  [跑通直播模式(Android)](https://intl.cloud.tencent.com/document/product/647/35108) 。

[](id:que14)
### 同一个页面中，是否可以创建 N 个 TRTC 对象，通过 N 个 UserID，分别登录到 N 个房间？
可以。[Version 7.6 版本](https://intl.cloud.tencent.com/document/product/647/34615) 开始支持一个用户进入多个房间了。

[](id:que15_flutter)
### 两台手机同时运行 Demo，为什么看不到彼此的画面？
请确保两台手机在运行 Demo 时使用的是不同的 UserID，TRTC 不支持同一个 UserID （除非 SDKAppID 不同）在两个终端同时使用。

[](id:que16_flutter)
### 防火墙有什么限制？
由于 SDK 使用 UDP 协议进行音视频传输，所以在对 UDP 有拦截的办公网络下无法使用。如遇到类似问题，请参见 [应对公司防火墙限制](https://intl.cloud.tencent.com/document/product/647/35164) 排查并解决。

[](id:que17_flutter)
### iOS 打包运行 Crash？
请排查是否 iOS14 以上的 debug 模式问题，具体请参见 [官方说明](https://flutter.cn/docs/development/ios-14#launching-debug-flutter-without-a-host-computer)。

[](id:que18_flutter)
### iOS 无法显示视频（Android 正常）？
请确认在您项目的 `info.plist` 中 `io.flutter.embedded_views_preview` 值为 YES。

[](id:que19_flutter)
### 更新 SDK 版本后，iOS CocoaPods 运行报错？
1. 删除 iOS 目录下 `Podfile.lock` 文件。
2. 执行 `pod repo update`。
3. 执行 `pod install`。
4. 重新运行。

[](id:que20_flutter)
### Android Manifest merge failed 编译失败？
1. 请打开 `/example/android/app/src/main/AndroidManifest.xml` 文件。
2. 将 `xmlns:tools="http://schemas.android.com/tools"` 加入到 manifest 中。
3. 将 `tools:replace="android:label"` 加入到 application 中。

![img](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

[](id:que21_flutter)
### 因为没有签名，真机调试报错?
若报错信息如下图所示：
![](https://main.qcloudimg.com/raw/809ae94061575b4e670f3a80ac9f3781.png)
1. 您需购买苹果证书，并进行配置、签名操作后，即可在真机上调试。
2. 证书购买成功后，在 `target > signing & capabilities` 中进行配置。

[](id:que22_flutter)
### 对插件内的 swift 文件做了增删后，build 时查找不到对应文件？
在主工程目录的 `/ios` 文件路径下 `pod install` 即可。

[](id:que23_flutter)
### Run 报错“Info.plit, error: No value at that key path or invalid key path: NSBonjourServices”？
执行 `flutter clean` 后，重新运行即可。

[](id:que24_flutter)
### Pod install 报错？
若报错信息如下图所示：
![](https://main.qcloudimg.com/raw/73db67cfc9e6b934fed947b63c6d2120.png)
报错信息里面提示 pod install 的时候没有 `generated.xconfig` 文件，因此运行报错，您根据提示**需要执行 flutter pub get** 解决。
>? 该问题是 flutter 编译后的问题，新项目或者执行了 `flutter clean` 后，都不存在这个问题。

[](id:que25_flutter)
### Run 的时候 iOS 版本依赖报错？
若报错信息如下图所示：
![](https://main.qcloudimg.com/raw/9102b3394560ca9df2f70549baabe3ff.png)
可能是 pods 的 target 版本无法满足所依赖的插件，因此造成报错。因此您需修改报错 pods 中的 target 到对应的版本。












