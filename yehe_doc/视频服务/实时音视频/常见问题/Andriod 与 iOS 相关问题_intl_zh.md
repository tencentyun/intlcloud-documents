<span id="que1"></span>
###  移动端（Andriod/iOS）支持哪几种系统音量模式？
支持2种系统音量类型，即通话音量类型和媒体音量类型：
- 通话音量，手机专门为通话场景设计的音量类型，使用手机自带的回声抵消功能，音质相比媒体音量类型较差， 无法通过音量按键将音量调成零，但是支持蓝牙耳机上的麦克风。
- 媒体音量，手机专门为音乐场景设计的音量类型，音质相比于通话音量类型要好，通过通过音量按键可以将音量调成零。 使用媒体音量类型时，如果要开启回声抵消（AEC）功能，SDK 会开启内置的声学处理算法对声音进行二次处理。 在媒体音量模式下，蓝牙耳机无法使用自带的麦克风采集声音，只能使用手机上的麦克风进行声音采集。

<span id="que2"></span>
###  移动端 SDK 推流怎么设置1080p分辨率？
1080P在 TX_Enum_Type_VideoResolution 定义是114，直接设置分辨率传枚举值即可。

<span id="que4"></span>
###  TRTC 移动端怎么实现录屏（屏幕分享）？	
从7.2版本开始，Android 端支持手机录屏，iOS 端支持 App 内录屏，可以直接参考 [官方 Demo](https://github.com/tencentyun/TRTCSDK) 源码。

<span id="que5"></span>
###  TRTC Android 端能不能支持64位的 arm64-v8a 架构？
TRTC 6.3 版本开始已提供 arm64-v8a 架构 ABI 支持。

<span id="que7"></span>
###  在 iOS 端是否支持 Swift 集成？
支持，直接按照支持集成三方库的流程集成 SDK 即可，还可以参考 [跑通Demo(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086)。

<span id="que9"></span>
###  TRTC SDK 是否支持 iOS 后台运行？
支持，您只需选中当前工程项目，在 **Capabilities** 下的设置  **Background Modes** 为 **ON**，并勾选 **Audio，AirPlay and Picture in Picture**即可实现后台运行，详情如下图所示：
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

<span id="que10"></span>
### iOS 端是否可以监听远端离开房间？
可以使用 [onRemoteUserLeaveRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28) 来监听用户离开房间事件，且该接口仅在 VideoCall 的所有用户和 LIVE 模式下的主播离开房间时会触发回调，观众离开房间不会有回调。 

<span id="que11"></span>
### 手机锁屏状态，视频如何拨通？
实现离线接听等功能，详情请参见 [实现离线接听](https://intl.cloud.tencent.com/document/product/647/36068)。

<span id="que12"></span>
### 是否支持 Android 和 Web 端互通？
支持。使用相同的 [SDKAppID](https://console.cloud.tencent.com/trtc/app)，并进入同一个房间进行通话。详情请参见下列文档链接配置 Demo：
- [跑通 Demo（Android）](https://intl.cloud.tencent.com/document/product/647/35084)
- [跑通 Demo（桌面浏览器）](https://intl.cloud.tencent.com/document/product/647/35607)

<span id="que13"></span>
### 主播和粉丝在直播过程中连麦，是否双方都可以主动发起连麦？
双方都可以主动发起，观众和主播发起逻辑一致，具体操作请参见  [跑通直播模式(Android)](https://intl.cloud.tencent.com/document/product/647/35108) 。

<span id="que14"></span>
### 多人视频会议中，移动端和 Web 端是否可以进入同一房间？
可以。需保证 [SDKAppID](https://console.cloud.tencent.com/trtc/app) 和房间号一致，且用户 ID 不一致。

<span id="que15"></span>
### 同一个页面中，是否可以创建 N 个 TRTC 对象，通过 N 个 UserID，分别登录到N个房间？
可以。[Version 7.6 版本](https://intl.cloud.tencent.com/document/product/647/34615) 开始支持一个用户进入多个房间了。
