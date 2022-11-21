>? **新版本（1.1.0.103）涉及 TUICallEngine 接口变更：**
>- 如果您在开发过程中，因为 maven latest 更新机制导致的 Android 构建报错 ，可以使用如下两种方式解决：
	  - 升级 TUICallKit 到最新版本。
	  - 修改 tuicallkit/build.gradle 的 tuicallengine 依赖为 1.0 的固定版本：`com.tencent.liteav.tuikit:tuicallengine:1.0.0.53`。
>- 如果您在开发过程中，因为 执行 pod update 导致 iOS 构建报错，可以使用如下两种方式解决：
	  - 升级 TUICallKit 到最新版本。
	  - Podfile 文件中添加 `pod 'TUICallEngine', '1.0.0.53'`。

### Version 1.1.0.103  @ 2022.09.30
- Android&iOS：优化群组通话过程中，邀请群成员加入功能。
- Android&iOS：优化通话流程，避免通话接听前产生录制、审核等费用。
- Android&iOS：支持自定义音视频通话的离线推送消息。
- Android&iOS：部分 **TUICallEngine** 接口参数变更，详见 [call()](https://www.tencentcloud.com/document/product/647/51006#call)、[groupCall()](https://www.tencentcloud.com/document/product/647/51006#groupcall)、[inviteUser()](https://www.tencentcloud.com/document/product/647/51006#inviteuser)、以及回调接口[onCallReceived()](https://www.tencentcloud.com/document/product/647/51007#oncallreceived)。
- Android&iOS：修复群组通话过程中，偶现的少量回调异常问题。
- Android&iOS：修复重复登录以及UserSig过期造成的状态异常问题。
- iOS：修复 TUCallKit Objective-C 和 Swift 混合编译时，`init`接口报错的问题。
- Android：修复Kotlin集成悬浮窗功能时编译报错问题。

### Version 1.0.0.53   @ 2022.08.15

#### 全新发布： 
- Android&iOS：支持1v1 音视频通话、群组音视频通话。
- Android&iOS：支持主流厂商的离线唤醒。
- Android&iOS：支持自定义头像、自定义昵称。
- Android&iOS：支持通话过程中开启悬浮窗。
- Android&iOS：支持设置自定义铃音。
- Android&iOS：支持多平台登录状态下的来电服务。