## TUICallEngine (无 UI 接口)

TUICallEngine API 是音视频通话组件的**无 UI 接口**，您可以使用这套 API 根据您的业务需求自定义封装。

| API                                                          | 描述                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [createInstance](#createinstance)                            | 创建 TUICallEngine 实例（单例模式） |
| [destroyInstance](#destroyinstance)                          | 销毁 TUICallEngine 实例（单例模式） |
| [on](#on) | 监听事件                            |
| [off](#off) | 取消监听事件                        |
| [login](#login) | 登录接口                            |
| [logout](#logout) | 登出接口                            |
| [setSelfInfo](#setselfinfo) | 设置用户昵称和头像                  |
| [call](#call) | C2C邀请通话                         |
| [groupCall](#groupcall) | 群聊邀请通话                        |
| [accept](#accept) | 接听通话                            |
| [reject](#reject) | 拒绝通话                            |
| [hangup](#hangup) | 结束通话                            |
| [switchCallingType](#switchcallingtype) | 音视频通话切换                      |
| [startRemoteView](#startremoteview) | 启动远端画面渲染                    |
| [stopRemoteView](#stopremoteview) | 停止远端画面渲染                    |
| [startLocalView](#startlocalview) | 启动本地画面渲染                    |
| [stopLocalView](#stoplocalview) | 停止本地画面渲染                    |
| [openCamera](#opencamera) | 开启摄像头                          |
| [closeCamara](#closecamara) | 关闭摄像头                          |
| [openMicrophone](#openmicrophone) | 打开麦克风                          |
| [closeMicrophone](#closemicrophone) | 关闭麦克风                          |
| [setMicMute](#setmicmute) | 设备麦克风是否静音                  |
| [setVideoQuality](#setvideoquality) | 设置视频质量                        |
| [getDeviceList](#getdevicelist) | 获取设备列表                        |
| [switchDevice](#switchdevice) | 切换摄像头或麦克风设备              |

## 事件类型定义

TUICallEvent 是 TUICallEngine 对应的回调事件类，您可以通过此回调，来监听自己感兴趣的回调事件。

| EVENT                                                        | 描述                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| [TUICallEvent.ERROR](#error) | SDK 内部发生了错误                                   |
| [TUICallEvent.SDK_READY](#sdk_ready) | SDK 进入 ready 状态时收到该回调                      |
| [TUICallEvent.KICKED_OUT](#kicked_out) | 重复登录，收到该回调说明被踢出房间                   |
| [TUICallEvent.USER_ACCEPT](#user_accept) | 如果有用户接听，那么会收到此回调                     |
| [TUICallEvent.USER_ENTER](#user_enter) | 如果有用户同意进入通话，那么会收到此回调             |
| [TUICallEvent.USER_LEAVE](#user_leave) | 如果有用户同意离开通话，那么会收到此回调             |
| [TUICallEvent.REJECT](#reject) | 用户拒绝通话                                         |
| [TUICallEvent.NO_RESP](#no_resp) | 邀请用户无应答                                       |
| [TUICallEvent.LINE_BUSY](#line_busy) | 邀请方忙线                                           |
| [TUICallEvent.CALLING_TIMEOUT](#calling_timeout) | 作为被邀请方会收到，收到该回调说明本次通话超时未应答 |
| [TUICallEvent.USER_VIDEO_AVAILABLE](#user_video_available) | 远端用户开启/关闭了摄像头, 会收到该回调              |
| [TUICallEvent.USER_AUDIO_AVAILABLE](#user_audio_available) | 远端用户开启/关闭了麦克风, 会收到该回调              |
| [TUICallEvent.USER_VOICE_VOLUME](#user_voice_volume) | 远端用户说话音量调整, 会收到该回调                   |
| [TUICallEvent.GROUP_CALL_INVITEE_LIST_UPDATE](#group_call_invitee_list_update) | 群聊更新邀请列表收到该回调                           |
| [TUICallEvent.INVITED](#invited) | 被邀请进行通话                                       |
| [TUICallEvent.CALLING_CANCEL](#calling_cancel) | 作为被邀请方会收到，收到该回调说明本次通话被取消了   |
| [TUICallEvent.CALLING_END](#calling_end) | 收到该回调说明本次通话结束了                         |
| [TUICallEvent.DEVICED_UPDATED](#deviced_updated) | 设备列表更新收到该回调                               |
| [TUICallEvent.CALL_TYPE_CHANGED](#call_type_changed) | 通话类型切换收到该回调                               |
