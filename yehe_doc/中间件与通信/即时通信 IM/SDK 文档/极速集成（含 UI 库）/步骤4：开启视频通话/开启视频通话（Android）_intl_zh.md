TUIKit 组件在 4.8.50 版本之后基于 [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) 实现了单聊和群组的视频通话和语音通话功能， 并且实现了 iOS 和 Android 平台的互通。需要注意的是不同的版本在集成方式上有一定的区别：
>! 
>- **4.8.50 ~ 5.1.60 版本**的TUIKit 组件默认集成了音视频通话 UI 组件和 [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) 音视频库，默认支持音视频通话相关功能。
>- **5.4.666** 及之后的版本 TUIKit 组件默认不再集成音视频通话 UI 组件和 [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) 音视频库，音视频相关逻辑都移到了 TUIKitLive 组件里面。
>- **TUIKit-Live 和 TUIKit 版本要一致，否则音视频通话功能会出现异常，无法正常使用。**


[](id:Step1)
## 步骤1：开通音视频服务
1. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) ，单击目标应用卡片，进入应用的基础配置页面。
2. 单击【开通腾讯实时音视频服务】区域的【立即开通】。
3. 在弹出的开通实时音视频 TRTC 服务对话框中，单击【确认】。
 系统将为您在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 创建一个与当前 IM 应用相同 SDKAppID 的实时音视频应用，二者帐号与鉴权可复用。

[](id:Step2)
## 步骤2：配置工程文件
建议使用源码集成 TUIKit 和 TUIKit-Live，以便于您修改源码满足自身的业务需求。

```
implementation project(':tuikit')
implementation project(':tuikit-live')
```

[](id:Step3)
## 步骤3：初始化 TUIKit 
初始化 TUIKit 需要传入 [步骤1](#Step1) 生成的 SDKAppID。
```
TUIKitConfigs configs = TUIKit.getConfigs();
TUIKit.init(this, SDKAPPID, configs);
```

[](id:Step4)
## 步骤4：登录 TUIKit
登录 IM 需要通过 TUIKit 提供的 `login` 接口，其中 UserSig 生成的具体操作请参见 [如何计算 UserSig](https://intl.cloud.tencent.com/document/product/647/35166)。
```
TUIKit.login(userID, userSig, new IUIKitCallBack() {
	@Override
	public void onSuccess(Object data) {
		// 登录成功
	}
	
	@Override
	public void onError(String module, final int code, final String desc) {
		// 登录失败
	}
});
```

[](id:Step5)
## 步骤5：发起视频或语音通话
当用户点击聊天界面的视频通话或则语音通话时，TUIKit 会自动展示通话邀请 UI，并给对方发起通话邀请请求。

## 步骤6：接受视频或语音通话


- 当用户**在线并且应用在前台时**收到通话邀请时，TUIKit 会自动展示通话接收 UI，用户可以选择同意或则拒绝通话。
- 当用户**离线**收到通话邀请时，如需唤起 App 通话，就要使用到离线推送能力，离线推送的实现请参考 [步骤7](#Step7)。

## 步骤7：离线推送[](id:Step7)
实现音视频通话的离线推送能力，请参考以下几个步骤：
1. 配置 App 的 [离线推送](https://intl.cloud.tencent.com/document/product/1047/39156)。
2. 升级 TUIKit 到4.9.1以上版本。
3. 通过 TUIKit 发起通话邀请的时候，默认会生成一条离线推送消息，消息生成的具体逻辑请参考 [TRTCCallingImpl.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUICalling/tuicalling/src/main/java/com/tencent/liteav/trtccalling/model/impl/TRTCCallingImpl.java) 类里面的 `sendOnlineMessageWithOfflinePushInfo` 方法。
4. 接收通话的一方，在收到离线推送的消息时，请参考 [OfflineMessageDispatcher.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/OfflineMessageDispatcher.java) 类里面 `redirect` 方法唤起通话界面。

## 常见问题
### 1. 若已分别创建实时音视频 SDKAppID 和即时通信 SDKAppID，现需要同时集成 IM SDK 和 TRTC SDK，需要注意什么?
若已分别创建实时音视频 SDKAppID 和即时通信 SDKAppID，即 SDKAppID 不一致场景，则二者帐号与鉴权不可复用，您需要生成实时音视频 SDKAppID 对应的 UserSig 进行鉴权。生成 UserSig 的具体操作请参见 [如何计算 UserSig](https://intl.cloud.tencent.com/document/product/647/35166)。
获取实时音视频的 SDKAppID 和 UserSig 后，您需要替换 `TRTCAVCallImpl` 源码中对应的值：
```
 private void enterTRTCRoom() {
	 ...
	 TRTCCloudDef.TRTCParams TRTCParams = new TRTCCloudDef.TRTCParams(mSdkAppId, mCurUserId, mCurUserSig, mCurRoomID, "", "");
	 ...
 }
```

### 2. 通话邀请的超时时间默认是多久？怎么修改默认超时时间？
通话邀请的默认超时时间是30s，您可以修改 `TRTCAVCallImpl` 里的 `TIME_OUT_COUNT` 字段来自定义超时时间。

### 3. 在邀请超时时间内，被邀请者如果离线再上线，能否收到邀请？
- 如果是单聊通话邀请，被邀请者离线再上线可以收到通话邀请。
- 如果是群聊通话邀请，被邀请者离线再上线不能收到通话邀请。

