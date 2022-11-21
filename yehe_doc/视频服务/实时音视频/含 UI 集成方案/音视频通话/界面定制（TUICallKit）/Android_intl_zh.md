本文将介绍如何定制 TUICallKit 的用户界面，我们提供了两个方案供您选择：**界面微调方案**和**自实现 UI 方案**。

## 方案一：界面微调方案

通过直接修改我们提供的 UI 源代码，对 TUICallKit 的用户界面进行调整，TUICallKit 的界面源代码位于 [Github](https://github.com/tencentyun/TUICalling) 中的 `Android/tuicallkit` 文件夹下面：

### 替换图标

您可以直接替换 `res\drawable-xxhdpi` 文件夹下的图标，以确保整个 App 中的图标色调风格保持一致，请在替换时保持图标文件的名字不变。

![img](https://qcloudimg.tencent-cloud.cn/image/document/f2c76a093afce40a97a8d1d5ff281fef.png)

### 替换铃声

您可以替换 `res\raw` 文件夹下的三个音频文件来达到替换铃声的目的：

| 文件名            | 用途             |
| ----------------- | ---------------- |
| phone_dialing.mp3 | 发起呼叫时的声音 |
| phone_hangup.mp3  | 被挂断的声音     |
| phone_ringing.mp3 | 接到呼叫时的声音 |

### 替换文案

您可以通过修改 values-zh 和 values-en 中的 `strings.xml` 文件来修改视频通话界面中的字符串内容。

## 方案二：自实现 UI 方案

TUICallKit 的整个通话功能是基于 TUICallEngine 这个无 UI 组件实现的，您可以删掉 tuicallkit 文件夹，完全基于 TUICallEngine 实现一套自己的 UI 界面。

### TUICallEngine

TUICallEngine 是整个通话组件的底层接口，主要提供了1对1音视频通话和群组内通话的发起、接听、拒绝、结束以及设备操作等关键接口。

| API                                                          | 描述                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51006#createinstance) | 创建 TUICallEngine 实例（单例模式）                         |
| [destroyInstance](https://www.tencentcloud.com/document/product/647/51006#destroyinstance) | 销毁 TUICallEngine 实例（单例模式）                         |
| [init](https://www.tencentcloud.com/document/product/647/51006#init) | 完成音视频通话基础能力的鉴权                                |
| [addObserver](https://www.tencentcloud.com/document/product/647/51006#addobserver) | 增加事件回调                                                |
| [removeObserver](https://www.tencentcloud.com/document/product/647/51006#removeobserver) | 移除回调接口                                                |
| [call](https://www.tencentcloud.com/document/product/647/51006#call) | 发起 1v1 通话                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51006#groupcall) | 发起群组通话                                                |
| [accept](https://www.tencentcloud.com/document/product/647/51006#accept) | 接听通话                                                    |
| [reject](https://www.tencentcloud.com/document/product/647/51006#reject) | 拒绝通话                                                    |
| [hangup](https://www.tencentcloud.com/document/product/647/51006#hangup) | 结束通话                                                    |
| [ignore](https://www.tencentcloud.com/document/product/647/51006#ignore) | 忽略通话                                                    |
| [inviteUser](https://www.tencentcloud.com/document/product/647/51006#inviteuser) | 在群组通话中，邀请其他人加入                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51006#joiningroupcall) | 主动加入当前的群组通话中                                    |
| [switchCallMediaType](https://www.tencentcloud.com/document/product/647/51006#switchcallmediatype) | 切换通话媒体类型，比如视频通话切音频通话                    |
| [startRemoteView](https://www.tencentcloud.com/document/product/647/51006#startremoteview) | 开始订阅远端用户视频流                                      |
| [stopRemoteView](https://www.tencentcloud.com/document/product/647/51006#stopremoteview) | 停止订阅远端用户视频流                                      |
| [openCamera](https://www.tencentcloud.com/document/product/647/51006#opencamera) | 开启摄像头                                                  |
| [closeCamera](https://www.tencentcloud.com/document/product/647/51006#closecamera) | 关闭摄像头                                                  |
| [switchCamera](https://www.tencentcloud.com/document/product/647/51006#switchcamera) | 切换前后摄像头                                              |
| [openMicrophone](https://www.tencentcloud.com/document/product/647/51006#openmicrophone) | 打开麦克风                                                  |
| [closeMicrophone](https://www.tencentcloud.com/document/product/647/51006#closemicrophone) | 关闭麦克风                                                  |
| [selectAudioPlaybackDevice](https://www.tencentcloud.com/document/product/647/51006#selectaudioplaybackdevice) | 选择音频播放设备（听筒/扬声器）                             |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51006#setselfinfo) | 设置用户的昵称、头像                                        |
| [enableMultiDeviceAbility](https://www.tencentcloud.com/document/product/647/51006#enablemultideviceability) | 开启/关闭 TUICallEngine 的多设备登录模式 （尊享版套餐支持） |

### TUICallObserver

TUICallObserver 是 TUICallEngine 对应的回调事件类，您可以通过此回调，来监听自己感兴趣的回调事件。

| API                                                          | 描述                         |
| ------------------------------------------------------------ | ---------------------------- |
| [onError](https://www.tencentcloud.com/document/product/647/51007#onerror) | 通话过程中错误回调           |
| [onCallReceived](https://www.tencentcloud.com/document/product/647/51007#oncallreceived) | 通话请求的回调               |
| [onCallCancelled](https://www.tencentcloud.com/document/product/647/51007#oncallcancelled) | 通话取消的回调               |
| [onCallBegin](https://www.tencentcloud.com/document/product/647/51007#oncallbegin) | 通话接通的回调               |
| [onCallEnd](https://www.tencentcloud.com/document/product/647/51007#oncallend) | 通话结束的回调               |
| [onCallMediaTypeChanged](https://www.tencentcloud.com/document/product/647/51007#oncallmediatypechanged) | 通话的媒体类型发生改变的回调 |
| [onUserReject](https://www.tencentcloud.com/document/product/647/51007#onuserreject) | xxxx 用户拒绝通话的回调      |
| [onUserNoResponse](https://www.tencentcloud.com/document/product/647/51007#onusernoresponse) | xxxx 用户不响应的回调        |
| [onUserLineBusy](https://www.tencentcloud.com/document/product/647/51007#onuserlinebusy) | xxxx 用户忙线的回调          |
| [onUserJoin](https://www.tencentcloud.com/document/product/647/51007#onuserjoin) | xxxx 用户加入通话的回调      |
| [onUserLeave](https://www.tencentcloud.com/document/product/647/51007#onuserleave) | xxxx 用户离开通话的回调      |
| [onUserVideoAvailable](https://www.tencentcloud.com/document/product/647/51007#onuservideoavailable) | xxx 用户是否有视频流的回调   |
| [onUserAudioAvailable](https://www.tencentcloud.com/document/product/647/51007#onuseraudioavailable) | xxx 用户是否有音频流的回调   |
| [onUserVoiceVolumeChanged](https://www.tencentcloud.com/document/product/647/51007#onuservoicevolumechanged) | 所有用户音量大小的反馈回调   |
| [onUserNetworkQualityChanged](https://www.tencentcloud.com/document/product/647/51007#onusernetworkqualitychanged) | 所有用户网络质量的反馈回调   |

## 关键类型定义

| API                                 | 描述                                         |
| ----------------------------------- | -------------------------------------------- |
| TUICallDefine.MediaType             | 通话的媒体类型，枚举类型：视频通话、语音通话 |
| TUICallDefine.Role                  | 通话的角色，枚举类型：主叫、被叫             |
| TUICallDefine.Status                | 通话的状态，枚举类型：空闲、待接听、接听中   |
| TUICommonDefine.RoomId              | 音视频房间 ID，支持数字、字符串两种类型      |
| TUICommonDefine.Camera              | 摄像头 ID 参数，枚举类型：前摄、后摄         |
| TUICommonDefine.AudioPlaybackDevice | 声音的播放设备，枚举类型：扬声器、听筒       |
| TUICommonDefine.NetworkQualityInfo  | 当前的网络质量信息                           |