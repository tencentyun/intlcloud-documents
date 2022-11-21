## TUICallEngine API 简介

TUICallEngine API 是音视频通话组件的**无 UI 接口**，如果 TUICallKit 的交互并不满足您的需求，您可以使用这套接口自己封装交互。

## API 概览

| API                                                          | 描述                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](#createinstance) | 创建 TUICallEngine 实例（单例模式）                         |
| [destroyInstance](#destroyinstance) | 销毁 TUICallEngine 实例（单例模式）                         |
| [init](#init) | 完成音视频通话基础能力的鉴权                                |
| [addObserver](#addobserver) | 增加事件回调                                                |
| [removeObserver](#removeobserver) | 移除回调接口                                                |
| [call](#call) | 发起 1v1 通话                                               |
| [groupCall](#groupcall) | 发起群组通话                                                |
| [accept](#accept) | 接听通话                                                    |
| [reject](#reject) | 拒绝通话                                                    |
| [hangup](#hangup) | 结束通话                                                    |
| [ignore](#ignore) | 忽略通话                                                    |
| [inviteUser](#inviteuser) | 在群组通话中，邀请其他人加入                                |
| [joinInGroupCall](#joiningroupcall) | 主动加入当前的群组通话中                                    |
| [switchCallMediaType](#switchcallmediatype) | 切换通话媒体类型，比如视频通话切音频通话                    |
| [startRemoteView](#startremoteview) | 开始订阅远端用户视频流                                      |
| [stopRemoteView](#stopremoteview) | 停止订阅远端用户视频流                                      |
| [openCamera](#opencamera) | 开启摄像头                                                  |
| [closeCamera](#closecamera) | 关闭摄像头                                                  |
| [switchCamera](#switchcamera) | 切换前后摄像头                                              |
| [openMicrophone](#openmicrophone) | 打开麦克风                                                  |
| [closeMicrophone](#closemicrophone) | 关闭麦克风                                                  |
| [selectAudioPlaybackDevice](#selectaudioplaybackdevice) | 选择音频播放设备（听筒/扬声器）                             |
| [setSelfInfo](#setselfinfo) | 设置用户的昵称、头像                                        |
| [enableMultiDeviceAbility](#enablemultideviceability) | 开启/关闭 TUICallEngine 的多设备登录模式 （尊享版套餐支持） |

## API 详情

### createInstance

创建 TUICallEngine 的单例。

```objectivec
- (TUICallEngine *)createInstance;
```

### destroyInstance

销毁 TUICallEngine 的单例。

```objectivec
- (void)destroyInstance;
```

### init

初始化函数，请在使用所有功能之前先调用该函数，以便完成包含通话服务鉴权在内初始化动作。

```objectivec
- (void)init:(NSString *)sdkAppID userId:(NSString *)userId userSig:(NSString *)userSig succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

参数如下表所示：

| 参数     | 类型               | 含义                                                         |
| -------- | ------------------ | ------------------------------------------------------------ |
| sdkAppID | int                | 您可以在**实时音视频控制台** >[**应用管理**](https://console.tencentcloud.com/trtc/app) > **应用信息**中查看 SDKAppID |
| userId   | String             | 当前用户的 ID，字符串类型，只允许包含英文字母（a-z 和 A-Z）、数字（0-9）、连词符（-）和下划线（_） |
| userSig  | String             | 腾讯云设计的一种安全保护签名，获取方式请参见 [如何计算及使用 UserSig](https://www.tencentcloud.com/document/product/647/35166) |
| callback | TUIDefine.Callback | 初始化回调，`onSuccess`表示初始化成功                        |

### addObserver

添加回调接口，您可以通过这个接听，监听`TUICallObserver`相关的事件回调。

```objectivec
- (void)addObserver:(id<TUICallObserver>)observer;
```

### removeObserver

移除回调接口。

```objectivec
- (void)removeObserver:(id<TUICallObserver>)observer;
```

### call

拨打电话（1v1通话）

```objectivec
- (void)call:(TUIRoomId *)roomId userId:(NSString *)userId callMediaType:(TUICallMediaType)callMediaType params:(TUICallParams *)params succ:(TUICallSucc)succ fail:(TUICallFail)fail
```

参数如下表所示：

| 参数          | 类型             | 含义                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | 此次通话的音视频房间 ID，目前仅支持数字房间号，后续版本会支持字符串房间号 |
| userId        | NSString         | 目标用户的 userId                                            |
| callMediaType | TUICallMediaType | 通话的媒体类型，比如视频通话、语音通话                       |
| params        | TUICallParams    | 通话参数扩展字段，例如：离线推送自定义内容                   |

### groupCall

发起群组通话，注意：使用群组通话前需要创建IM 群组，如果已经创建，请忽略。

```objectivec
- (void)groupCall:(TUIRoomId *)roomId groupId:(NSString *)groupId userIdList:(NSArray <NSString *> *)userIdList callMediaType:(TUICallMediaType)callMediaType params:(TUICallParams *)params succ:(TUICallSucc)succ fail:(TUICallFail)fail
```

| 参数          | 类型             | 含义                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | 此次通话的音视频房间 ID，目前仅支持数字房间号，后续版本会支持字符串房间号 |
| groupId       | NSString         | 此次群组通话的群 ID                                          |
| userIdList    | NSArray          | 目标用户的 userId 列表                                       |
| callMediaType | TUICallMediaType | 通话的媒体类型，比如视频通话、语音通话                       |
| params        | TUICallParams    | 通话参数扩展字段，例如：离线推送自定义内容                   |

### accept

接受当前通话，当您作为被叫收到 `onCallReceived()` 的回调时，可以调用该函数接听来电。

```objectivec
- (void)accept:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### reject

拒绝当前通话，当您作为被叫收到 `onCallReceived()` 的回调时，可以调用该函数拒绝来电。

```objectivec
- (void)reject:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### ignore

忽略当前通话，当您作为被叫收到 `onCallReceived()` 的回调时，可以调用该函数忽略来电，此时主叫会收到`onUserLineBusy`的回调。 备注：如果您的业务中存在直播、会议等场景，在直播/会议中的情况时，也可以调用这个函数来忽略此次来电。

```objectivec
- (void)ignore:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### hangup

挂断当前通话，当您处于通话中，可以调用该函数结束通话。

```objectivec
- (void)hangup:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### inviteUser

邀请用户加入此次群组通话。 使用场景：一个群组通话中的用户主动邀请其他人时使用。

```objectivec
- (void)inviteUser:(NSArray<NSString *> *)userIdList params:(TUICallParams *)params succ:(void(^)(NSArray <NSString *> *userIdList))succ fail:(TUICallFail)fail
```

| 参数       | 类型          | 含义                                       |
| ---------- | ------------- | ------------------------------------------ |
| userIdList | NSArray       | 目标用户的 userId 列表                     |
| params     | TUICallParams | 通话参数扩展字段，例如：离线推送自定义内容 |

### joinInGroupCall

主动加入此次群组通话。 使用场景：群组内用户主动加入此次群组通话使用。

```objectivec
- (void)joinInGroupCall:(TUIRoomId *)roomId groupId:(NSString *)groupId callMediaType:(TUICallMediaType)callMediaType succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

| 参数          | 类型             | 含义                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | 此次通话的音视频房间 ID，目前仅支持数字房间号，后续版本会支持字符串房间号 |
| groupId       | NSString         | 此次群组通话的群 ID                                          |
| callMediaType | TUICallMediaType | 通话的媒体类型，比如视频通话、语音通话                       |

### switchCallMediaType

切换视频通话到语音通话。

```objectivec
- (void)switchCallMediaType:(TUICallMediaType)newType;
```

| 参数          | 类型             | 含义                                   |
| ------------- | ---------------- | -------------------------------------- |
| callMediaType | TUICallMediaType | 通话的媒体类型，比如视频通话、语音通话 |

### startRemoteView

设置显示视频画面的 View 对象

```objectivec
- (void)startRemoteView:(NSString *)userId videoView:(TUIVideoView *)videoView onPlaying:(void(^)(NSString *userId))onPlaying onLoading:(void(^)(NSString *userId))onLoading onError:(void(^)(NSString *userId, int code, NSString *errMsg))onError;
```

| 参数      | 类型         | 含义              |
| --------- | ------------ | ----------------- |
| userId    | NSString     | 目标用户的 userId |
| videoView | TUIVideoView | 待渲染的视图      |

### stopRemoteview

停止订阅远端用户的视频数据。

```objectivec
- (void)stopRemoteView:(NSString *)userId;
```

| 参数   | 类型     | 含义              |
| ------ | -------- | ----------------- |
| userId | NSString | 目标用户的 userId |

### openCamera

开启摄像头。

```objectivec
- (void)openCamera:(TUICallCamera)camera videoView:(TUIVideoView *)videoView succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

| 参数      | 类型          | 含义             |
| --------- | ------------- | ---------------- |
| camera    | TUICallCamera | 前置/后置 摄像头 |
| videoView | TUIVideoView  | 待渲染的视图     |

### closeCamera

关闭摄像头。

```objectivec
- (void)closeCamera;
```

### switchCamera

切换前后摄像头。

```objectivec
- (void)switchCamera:(TUICallCamera)camera;
```

| 参数   | 类型          | 含义             |
| ------ | ------------- | ---------------- |
| camera | TUICallCamera | 前置/后置 摄像头 |

### openMicrophone

打开麦克风。

```objectivec
- (void)openMicrophone:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### closeMicrophone

关闭麦克风。

```objectivec
- (void)closeMicrophone;
```

### selectAudioPlaybackDevice

选择音频播放设备。 目前支持听筒、扬声器，在通话场景中，可以使用这个接口来开启/关闭免提模式。

```objectivec
- (void)selectAudioPlaybackDevice:(TUIAudioPlaybackDevice)device;
```

| 参数   | 类型                   | 含义        |
| ------ | ---------------------- | ----------- |
| device | TUIAudioPlaybackDevice | 听筒/扬声器 |

### setSelfInfo

设置用户昵称、头像。 用户昵称不能超过500字节，用户头像必须是 URL 格式。

```objectivec
- (void)setSelfInfo:(NSString * _Nullable)nickName avatar:(NSString * _Nullable)avatar succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### enableMultiDeviceAbility

开启/关闭 TUICallEngine 的多设备登录模式 （尊享版套餐支持）

```objectivec
- (void)enableMultiDeviceAbility:(BOOL)enable succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```