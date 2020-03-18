## TRTCCloud @ TXLiteAVSDK

腾讯云视频通话功能的主要接口类。

### 基础方法

| API | 描述 |
|-----|-----|
| [sharedInstance](https://intl.cloud.tencent.com/document/product/647/35126#sharedinstance) | 创建 [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35126#trtccloud) 单例。 |
| [destroySharedInstance](https://intl.cloud.tencent.com/document/product/647/35126#destroysharedinstance) | 销毁 [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35126#trtccloud) 单例。 |
| [setListener](https://intl.cloud.tencent.com/document/product/647/35126#setlistener) | 设置回调接口 TRTCCloudListener，用户获得来自 [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35126#trtccloud) 的各种状态通知。 |
| [setListenerHandler](https://intl.cloud.tencent.com/document/product/647/35126#setlistenerhandler) | 设置驱动 [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/35127#trtccloudlistener) 回调的队列。 |


### 房间相关接口函数

| API | 描述 |
|-----|-----|
| [enterRoom](https://intl.cloud.tencent.com/document/product/647/35126#enterroom) | 进入房间。 |
| [exitRoom](https://intl.cloud.tencent.com/document/product/647/35126#exitroom) | 离开房间。 |
| [switchRole](https://intl.cloud.tencent.com/document/product/647/35126#switchrole) | 切换角色，仅适用于直播场景（TRTCAppSceneLIVE）。 |
| [ConnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35126#connectotherroom) | 请求跨房通话（主播 PK）。 |
| [DisconnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35126#disconnectotherroom) | 退出跨房通话。 |
| [setDefaultStreamRecvMode](https://intl.cloud.tencent.com/document/product/647/35126#setdefaultstreamrecvmode) | 设置音视频数据接收模式（需要在进房前设置才能生效）。 |


### 视频相关接口函数

| API | 描述 |
|-----|-----|
| [startLocalPreview](https://intl.cloud.tencent.com/document/product/647/35126#startlocalpreview) | 开启本地视频的预览画面。 |
| [stopLocalPreview](https://intl.cloud.tencent.com/document/product/647/35126#stoplocalpreview) | 停止本地视频采集及预览。 |
| [muteLocalVideo](https://intl.cloud.tencent.com/document/product/647/35126#mutelocalvideo) | 是否屏蔽自己的视频画面。 |
| [startRemoteView](https://intl.cloud.tencent.com/document/product/647/35126#startremoteview) | 开始显示远端视频画面。 |
| [stopRemoteView](https://intl.cloud.tencent.com/document/product/647/35126#stopremoteview) | 停止显示远端视频画面。 |
| [stopAllRemoteView](https://intl.cloud.tencent.com/document/product/647/35126#stopallremoteview) | 停止显示所有远端视频画面。 |
| [muteRemoteVideoStream](https://intl.cloud.tencent.com/document/product/647/35126#muteremotevideostream) | 暂停接收指定的远端视频流。 |
| [muteAllRemoteVideoStreams](https://intl.cloud.tencent.com/document/product/647/35126#muteallremotevideostreams) | 停止接收所有远端视频流。 |
| [setVideoEncoderParam](https://intl.cloud.tencent.com/document/product/647/35126#setvideoencoderparam) | 设置视频编码器相关参数。 |
| [setNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35126#setnetworkqosparam) | 设置网络流控相关参数。 |
| [setLocalViewFillMode](https://intl.cloud.tencent.com/document/product/647/35126#setlocalviewfillmode) | 设置本地图像的渲染模式。 |
| [setRemoteViewFillMode](https://intl.cloud.tencent.com/document/product/647/35126#setremoteviewfillmode) | 设置远端图像的渲染模式。 |
| [setLocalViewRotation](https://intl.cloud.tencent.com/document/product/647/35126#setlocalviewrotation) | 设置本地图像的顺时针旋转角度。 |
| [setRemoteViewRotation](https://intl.cloud.tencent.com/document/product/647/35126#setremoteviewrotation) | 设置远端图像的顺时针旋转角度。 |
| [setVideoEncoderRotation](https://intl.cloud.tencent.com/document/product/647/35126#setvideoencoderrotation) | 设置视频编码输出的（也就是远端用户观看到的，以及服务器录制下来的）画面方向。 |
| [setLocalViewMirror](https://intl.cloud.tencent.com/document/product/647/35126#setlocalviewmirror) | 设置本地摄像头预览画面的镜像模式。 |
| [setVideoEncoderMirror](https://intl.cloud.tencent.com/document/product/647/35126#setvideoencodermirror) | 设置编码器输出的画面镜像模式。 |
| [setGSensorMode](https://intl.cloud.tencent.com/document/product/647/35126#setgsensormode) | 设置重力感应的适应模式。 |
| [enableEncSmallVideoStream](https://intl.cloud.tencent.com/document/product/647/35126#enableencsmallvideostream) | 开启大小画面双路编码模式。 |
| [setRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35126#setremotevideostreamtype) | 选定观看指定 uid 的大画面还是小画面。 |
| [setPriorRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35126#setpriorremotevideostreamtype) | 设定观看方优先选择的视频质量。 |


### 音频相关接口函数

| API | 描述 |
|-----|-----|
| [startLocalAudio](https://intl.cloud.tencent.com/document/product/647/35126#startlocalaudio) | 开启本地音频的采集和上行。 |
| [stopLocalAudio](https://intl.cloud.tencent.com/document/product/647/35126#stoplocalaudio) | 关闭本地音频的采集和上行。 |
| [muteLocalAudio](https://intl.cloud.tencent.com/document/product/647/35126#mutelocalaudio) | 静音本地的音频。 |
| [setAudioRoute](https://intl.cloud.tencent.com/document/product/647/35126#setaudioroute) | 设置音频路由。 |
| [muteRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35126#muteremoteaudio) | 静音某一个用户的声音。 |
| [muteAllRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35126#muteallremoteaudio) | 静音所有用户的声音。 |
| [enableAudioVolumeEvaluation](https://intl.cloud.tencent.com/document/product/647/35126#enableaudiovolumeevaluation) | 启用音量大小提示。 |
| [startAudioRecording](https://intl.cloud.tencent.com/document/product/647/35126#startaudiorecording) | 开始录音。 |
| [stopAudioRecording](https://intl.cloud.tencent.com/document/product/647/35126#stopaudiorecording) | 停止录音。 |
| [setSystemVolumeType](https://intl.cloud.tencent.com/document/product/647/35126#setsystemvolumetype) | 设置通话过程中使用的系统音量类型。 |
| [enableAudioEarMonitoring](https://intl.cloud.tencent.com/document/product/647/35126#enableaudioearmonitoring) | 开启耳返。 |

### 摄像头相关接口函数

| API | 描述 |
|-----|-----|
| [switchCamera](https://intl.cloud.tencent.com/document/product/647/35126#switchcamera) | 切换摄像头。 |
| [isCameraZoomSupported](https://intl.cloud.tencent.com/document/product/647/35126#iscamerazoomsupported) | 查询当前摄像头是否支持缩放。 |
| [setZoom](https://intl.cloud.tencent.com/document/product/647/35126#setzoom) | 设置摄像头缩放因子（焦距）。 |
| [isCameraTorchSupported](https://intl.cloud.tencent.com/document/product/647/35126#iscameratorchsupported) | 查询是否支持开关闪光灯（手电筒模式）。 |
| [enableTorch](https://intl.cloud.tencent.com/document/product/647/35126#enabletorch) | 开关闪光灯。 |
| [isCameraFocusPositionInPreviewSupported](https://intl.cloud.tencent.com/document/product/647/35126#iscamerafocuspositioninpreviewsupported) | 查询是否支持设置焦点。 |
| [setFocusPosition](https://intl.cloud.tencent.com/document/product/647/35126#setfocusposition) | 设置摄像头焦点。 |
| [isCameraAutoFocusFaceModeSupported](https://intl.cloud.tencent.com/document/product/647/35126#iscameraautofocusfacemodesupported) | 查询是否支持自动识别人脸位置。 |


### 美颜滤镜相关接口函数

| API | 描述 |
|-----|-----|
| [getBeautyManager](https://intl.cloud.tencent.com/document/product/647/35126#getbeautymanager) | 获取美颜管理对象。 |
| [setBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35126#setbeautystyle) | 设置美颜、美白、红润效果级别。 |
| [setFilter](https://intl.cloud.tencent.com/document/product/647/35126#setfilter) | 设置指定素材滤镜特效。 |
| [setFilterConcentration](https://intl.cloud.tencent.com/document/product/647/35126#setfilterconcentration) | 设置滤镜浓度。 |
| [setWatermark](https://intl.cloud.tencent.com/document/product/647/35126#setwatermark) | 添加水印。 |
| [setEyeScaleLevel](https://intl.cloud.tencent.com/document/product/647/35126#seteyescalelevel) | 设置大眼级别（商用企业版有效，其它版本设置此参数无效）。 |
| [setFaceSlimLevel](https://intl.cloud.tencent.com/document/product/647/35126#setfaceslimlevel) | 设置瘦脸级别（商用企业版有效，其它版本设置此参数无效）。 |
| [setFaceVLevel](https://intl.cloud.tencent.com/document/product/647/35126#setfacevlevel) | 设置V脸级别（商用企业版有效，其它版本设置此参数无效）。 |
| [setFaceShortLevel](https://intl.cloud.tencent.com/document/product/647/35126#setfaceshortlevel) | 设置短脸级别（商用企业版有效，其它版本设置此参数无效）。 |
| [setChinLevel](https://intl.cloud.tencent.com/document/product/647/35126#setchinlevel) | 设置下巴拉伸或收缩（商用企业版有效，其它版本设置此参数无效）。 |
| [setNoseSlimLevel](https://intl.cloud.tencent.com/document/product/647/35126#setnoseslimlevel) | 设置瘦鼻级别（商用企业版有效，其它版本设置此参数无效）。 |
| [setGreenScreenFile](https://intl.cloud.tencent.com/document/product/647/35126#setgreenscreenfile) | 设置绿幕背景视频（商用企业版有效，其它版本设置此参数无效）。 |
| [selectMotionTmpl](https://intl.cloud.tencent.com/document/product/647/35126#selectmotiontmpl) | 选择使用哪一款 AI 动效挂件（商用企业版有效，其它版本设置此参数无效）。 |
| [setMotionMute](https://intl.cloud.tencent.com/document/product/647/35126#setmotionmute) | 设置动效静音（商用企业版有效，其它版本设置此参数无效）。 |


### 辅流相关接口函数

| API | 描述 |
|-----|-----|
| [startRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35126#startremotesubstreamview) | 开始显示远端用户的屏幕分享画面。 |
| [stopRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35126#stopremotesubstreamview) | 停止显示远端用户的屏幕分享画面。 |
| [setRemoteSubStreamViewFillMode](https://intl.cloud.tencent.com/document/product/647/35126#setremotesubstreamviewfillmode) | 设置屏幕分享画面的显示模式。 |


### 自定义采集和渲染

| API | 描述 |
|-----|-----|
| [enableCustomVideoCapture](https://intl.cloud.tencent.com/document/product/647/35126#enablecustomvideocapture) | 启用视频自定义采集模式。 |
| [sendCustomVideoData](https://intl.cloud.tencent.com/document/product/647/35126#sendcustomvideodata) | 向 SDK 投送自己采集的视频数据。 |
| [setLocalVideoRenderListener](https://intl.cloud.tencent.com/document/product/647/35126#setlocalvideorenderlistener) | 设置本地视频的自定义渲染回调。 |
| [setRemoteVideoRenderListener](https://intl.cloud.tencent.com/document/product/647/35126#setremotevideorenderlistener) | 设置远端视频的自定义渲染回调。 |
| [enableCustomAudioCapture](https://intl.cloud.tencent.com/document/product/647/35126#enablecustomaudiocapture) | 启用音频自定义采集模式。 |
| [sendCustomAudioData](https://intl.cloud.tencent.com/document/product/647/35126#sendcustomaudiodata) | 向 SDK 投送自己采集的音频数据。 |
| [setAudioFrameListener](https://intl.cloud.tencent.com/document/product/647/35126#setaudioframelistener) | 设置音频数据回调。 |


### 自定义消息发送

| API | 描述 |
|-----|-----|
| [sendCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35126#sendcustomcmdmsg) | 发送自定义消息给房间内所有用户。 |
| [sendSEIMsg](https://intl.cloud.tencent.com/document/product/647/35126#sendseimsg) | 将小数据量的自定义数据嵌入视频帧中。 |


### 背景混音相关接口函数

| API | 描述 |
|-----|-----|
| [playBGM](https://intl.cloud.tencent.com/document/product/647/35126#playbgm) | 启动播放背景音乐。 |
| [stopBGM](https://intl.cloud.tencent.com/document/product/647/35126#stopbgm) | 停止播放背景音乐。 |
| [pauseBGM](https://intl.cloud.tencent.com/document/product/647/35126#pausebgm) | 暂停播放背景音乐。 |
| [resumeBGM](https://intl.cloud.tencent.com/document/product/647/35126#resumebgm) | 继续播放背景音乐。 |
| [getBGMDuration](https://intl.cloud.tencent.com/document/product/647/35126#getbgmduration) | 获取音乐文件总时长，单位毫秒。 |
| [setBGMPosition](https://intl.cloud.tencent.com/document/product/647/35126#setbgmposition) | 设置 BGM 播放进度。 |
| [setMicVolumeOnMixing](https://intl.cloud.tencent.com/document/product/647/35126#setmicvolumeonmixing) | 设置麦克风的音量大小，播放背景音乐混音时使用，用来控制麦克风音量大小。 |
| [setBGMVolume](https://intl.cloud.tencent.com/document/product/647/35126#setbgmvolume) | 设置背景音乐的音量大小，播放背景音乐混音时使用，用来控制背景音音量大小。 |
| [setReverbType](https://intl.cloud.tencent.com/document/product/647/35126#setreverbtype) | 设置混响效果。 |
| [setVoiceChangerType](https://intl.cloud.tencent.com/document/product/647/35126#setvoicechangertype) | 设置变声类型。 |

### 音效相关接口函数

| API | 描述 |
|-----|-----|
| [playAudioEffect](https://intl.cloud.tencent.com/document/product/647/35126#playaudioeffect) | 播放音效。 |
| [setAudioEffectVolume](https://intl.cloud.tencent.com/document/product/647/35126#setaudioeffectvolume) | 设置单个音效音量。 |
| [stopAudioEffect](https://intl.cloud.tencent.com/document/product/647/35126#stopaudioeffect) | 停止音效。 |
| [stopAllAudioEffects](https://intl.cloud.tencent.com/document/product/647/35126#stopallaudioeffects) | 停止所有音效。 |
| [setAllAudioEffectsVolume](https://intl.cloud.tencent.com/document/product/647/35126#setallaudioeffectsvolume) | 设置所有音效的音量。 |


### 网络测试

| API | 描述 |
|-----|-----|
| [startSpeedTest](https://intl.cloud.tencent.com/document/product/647/35126#startspeedtest) | 开始进行网络测速（视频通话期间请勿测试，以免影响通话质量）。 |
| [stopSpeedTest](https://intl.cloud.tencent.com/document/product/647/35126#stopspeedtest) | 停止服务器测速。 |


### 混流转码并发布到 CDN

| API | 描述 |
|-----|-----|
| [setMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35126#setmixtranscodingconfig) | 设置云端的混流转码参数。 |
| [startPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35126#startpublishcdnstream) | 旁路转推到指定的推流地址。 |
| [stopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35126#stoppublishcdnstream) | 停止旁路推流。 |


### Log 相关接口函数

| API | 描述 |
|-----|-----|
| [getSDKVersion](https://intl.cloud.tencent.com/document/product/647/35126#getsdkversion) | 获取 SDK 版本信息。 |
| [setLogLevel](https://intl.cloud.tencent.com/document/product/647/35126#setloglevel) | 设置 Log 输出级别。 |
| [setConsoleEnabled](https://intl.cloud.tencent.com/document/product/647/35126#setconsoleenabled) | 启用或禁用控制台日志打印。 |
| [setLogCompressEnabled](https://intl.cloud.tencent.com/document/product/647/35126#setlogcompressenabled) | 启用或禁用 Log 的本地压缩。 |
| [setLogDirPath](https://intl.cloud.tencent.com/document/product/647/35126#setlogdirpath) | 修改日志保存路径。 |
| [setLogListener](https://intl.cloud.tencent.com/document/product/647/35126#setloglistener) | 设置日志回调。 |
| [showDebugView](https://intl.cloud.tencent.com/document/product/647/35126#showdebugview) | 显示仪表盘。 |
| [setDebugViewMargin](https://intl.cloud.tencent.com/document/product/647/35126#setdebugviewmargin) | 设置仪表盘的边距。 |
| [callExperimentalAPI](https://intl.cloud.tencent.com/document/product/647/35126#callexperimentalapi) | 调用实验性 API 接口。 |


### 播放背景音乐的回调接口

播放背景音乐的回调接口。

| API | 描述 |
|-----|-----|
| [onBGMStart](https://intl.cloud.tencent.com/document/product/647/35126#onbgmstart) | 音乐播放开始的回调通知。 |
| [onBGMProgress](https://intl.cloud.tencent.com/document/product/647/35126#onbgmprogress) | 音乐播放进度的回调通知。 |
| [onBGMComplete](https://intl.cloud.tencent.com/document/product/647/35126#onbgmcomplete) | 音乐播放结束的回调通知。 |

### 其它

| API | 描述 |
|-----|-----|
| [TRTCViewMargin](https://intl.cloud.tencent.com/document/product/647/35126#trtcviewmargin) | 视图边距。 |

## TRTCCloudListener @ TXLiteAVSDK

腾讯云视频通话功能的事件回调接口。

### 错误事件和警告事件

| API | 描述 |
|-----|-----|
| [onError](https://intl.cloud.tencent.com/document/product/647/35127#onerror) | 错误回调：SDK 不可恢复的错误，一定要监听，并分情况给用户适当的界面提示。 |
| [onWarning](https://intl.cloud.tencent.com/document/product/647/35127#onwarning) | 警告回调：用于告知您一些非严重性问题，例如出现卡顿或者可恢复的解码失败。 |


### 房间事件回调

| API | 描述 |
|-----|-----|
| [onEnterRoom](https://intl.cloud.tencent.com/document/product/647/35127#onenterroom) | 已加入房间的回调。 |
| [onExitRoom](https://intl.cloud.tencent.com/document/product/647/35127#onexitroom) | 离开房间的事件回调。 |
| [onSwitchRole](https://intl.cloud.tencent.com/document/product/647/35127#onswitchrole) | 切换角色的事件回调。 |
| [onConnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35127#onconnectotherroom) | 请求跨房通话（主播 PK）的结果回调。 |
| [onDisConnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35127#ondisconnectotherroom) | 结束跨房通话（主播 PK）的结果回调。 |


### 成员事件回调

| API | 描述 |
|-----|-----|
| [onRemoteUserEnterRoom](https://intl.cloud.tencent.com/document/product/647/35127#onremoteuserenterroom) | 有用户加入当前房间。 |
| [onRemoteUserLeaveRoom](https://intl.cloud.tencent.com/document/product/647/35127#onremoteuserleaveroom) | 有用户离开当前房间。 |
| [onUserVideoAvailable](https://intl.cloud.tencent.com/document/product/647/35127#onuservideoavailable) | 用户是否开启摄像头视频。 |
| [onUserSubStreamAvailable](https://intl.cloud.tencent.com/document/product/647/35127#onusersubstreamavailable) | 用户是否开启屏幕分享。 |
| [onUserAudioAvailable](https://intl.cloud.tencent.com/document/product/647/35127#onuseraudioavailable) | 用户是否开启音频上行。 |
| [onFirstVideoFrame](https://intl.cloud.tencent.com/document/product/647/35127#onfirstvideoframe) | 开始渲染本地或远程用户的首帧画面。 |
| [onFirstAudioFrame](https://intl.cloud.tencent.com/document/product/647/35127#onfirstaudioframe) | 开始播放远程用户的首帧音频（本地声音暂不通知）。 |
| [onSendFirstLocalVideoFrame](https://intl.cloud.tencent.com/document/product/647/35127#onsendfirstlocalvideoframe) | 首帧本地视频数据已经被送出。 |
| [onSendFirstLocalAudioFrame](https://intl.cloud.tencent.com/document/product/647/35127#onsendfirstlocalaudioframe) | 首帧本地音频数据已经被送出。 |
| [onUserEnter](https://intl.cloud.tencent.com/document/product/647/35127#onuserenter) | 废弃接口：有主播加入当前房间。 |
| [onUserExit](https://intl.cloud.tencent.com/document/product/647/35127#onuserexit) | 废弃接口： 有主播离开当前房间。 |


### 统计和质量回调

| API | 描述 |
|-----|-----|
| [onNetworkQuality](https://intl.cloud.tencent.com/document/product/647/35127#onnetworkquality) | 网络质量：该回调每2秒触发一次，统计当前网络的上行和下行质量。 |
| [onStatistics](https://intl.cloud.tencent.com/document/product/647/35127#onstatistics) | 技术指标统计回调。 |


### 服务器事件回调

| API | 描述 |
|-----|-----|
| [onConnectionLost](https://intl.cloud.tencent.com/document/product/647/35127#onconnectionlost) | SDK 跟服务器的连接断开。 |
| [onTryToReconnect](https://intl.cloud.tencent.com/document/product/647/35127#ontrytoreconnect) | SDK 尝试重新连接到服务器。 |
| [onConnectionRecovery](https://intl.cloud.tencent.com/document/product/647/35127#onconnectionrecovery) | SDK 跟服务器的连接恢复。 |
| [onSpeedTest](https://intl.cloud.tencent.com/document/product/647/35127#onspeedtest) | 服务器测速的回调，SDK 对多个服务器 IP 做测速，每个 IP 的测速结果通过这个回调通知。 |


### 硬件设备事件回调

| API | 描述 |
|-----|-----|
| [onCameraDidReady](https://intl.cloud.tencent.com/document/product/647/35127#oncameradidready) | 摄像头准备就绪。 |
| [onMicDidReady](https://intl.cloud.tencent.com/document/product/647/35127#onmicdidready) | 麦克风准备就绪。 |
| [onAudioRouteChanged](https://intl.cloud.tencent.com/document/product/647/35127#onaudioroutechanged) | 音频路由发生变化，音频路由即声音由哪里输出（扬声器、听筒）。 |
| [onUserVoiceVolume](https://intl.cloud.tencent.com/document/product/647/35127#onuservoicevolume) | 用于提示音量大小的回调,包括每个 userId 的音量和远端总音量。 |


### 自定义消息的接收回调

| API | 描述 |
|-----|-----|
| [onRecvCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35127#onrecvcustomcmdmsg) | 收到自定义消息回调。 |
| [onMissCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35127#onmisscustomcmdmsg) | 自定义消息丢失回调。 |
| [onRecvSEIMsg](https://intl.cloud.tencent.com/document/product/647/35127#onrecvseimsg) | 收到 SEI 消息的回调。 |


### CDN 旁路转推回调

| API | 描述 |
|-----|-----|
| [onStartPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35127#onstartpublishcdnstream) | 启动旁路推流到 CDN 完成的回调。 |
| [onStopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35127#onstoppublishcdnstream) | 停止旁路推流到 CDN 完成的回调。 |
| [onSetMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35127#onsetmixtranscodingconfig) | 设置云端的混流转码参数的回调，对应于 [TRTCCloud](https://cloud.tencent.com/document/product/647/32264#trtccloud) 中的 setMixTranscodingConfig() 接口。 |

### 音效回调

| API | 描述 |
|-----|-----|
| [onAudioEffectFinished](https://intl.cloud.tencent.com/document/product/647/35127#onaudioeffectfinished) | 播放音效结束回调。 |

### 视频数据帧的自定义渲染回调
跳转到 [TRTCVideoRenderListener](https://intl.cloud.tencent.com/document/product/647/35127#trtcvideorenderlistener)

| API | 描述 |
|-----|-----|
| [onRenderVideoFrame](https://intl.cloud.tencent.com/document/product/647/35127#onrendervideoframe) | 自定义视频渲染回调。 |


### 声音数据帧的自定义处理回调（只读）
跳转到 [TRTCAudioFrameListener](https://intl.cloud.tencent.com/document/product/647/35127#trtcaudioframelistener)

| API | 描述 |
|-----|-----|
| [onCapturedAudioFrame](https://intl.cloud.tencent.com/document/product/647/35127#oncapturedaudioframe) | 本地麦克风采集到的音频数据回调。 |
| [onPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35127#onplayaudioframe) | 混音前的每一路远程用户的音频数据（例如您要对某一路的语音进行文字转换，必须要使用这里的原始数据，而不是混音之后的数据）。 |
| [onMixedPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35127#onmixedplayaudioframe) | 各路音频数据混合后送入喇叭播放的音频数据。 |


### 日志相关回调
跳转到 [TRTCLogListener](https://intl.cloud.tencent.com/document/product/647/35127#trtcloglistener)

建议在一个比较早初始化的类中设置回调对象，如 Application。

| API | 描述 |
|-----|-----|
| [onLog](https://intl.cloud.tencent.com/document/product/647/35127#onlog) | 有日志打印时的回调。 |


## 关键类型定义
| API | 描述 |
|-----|-----|
| [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35129#trtcparams) | 进房参数。 |
| [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcvideoencparam) | 编码参数。 |
| [TRTCNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcnetworkqosparam) | 网络流控相关参数。 |
| [TRTCQuality](https://intl.cloud.tencent.com/document/product/647/35129#trtcquality) | 视频（或网络）质量。 |
| [TRTCTexture](https://intl.cloud.tencent.com/document/product/647/35129#trtctexture) | 视频纹理数据，包含纹理 ID 及 EGL 环境。 |
| [TRTCVideoFrame](https://intl.cloud.tencent.com/document/product/647/35129#trtcvideoframe) | 视频帧信息。 |
| [TRTCAudioFrame](https://intl.cloud.tencent.com/document/product/647/35129#trtcaudioframe) | 音频帧数据。 |
| [TRTCVolumeInfo](https://intl.cloud.tencent.com/document/product/647/35129#trtcvolumeinfo) | 音量大小。 |
| [TRTCSpeedTestResult](https://intl.cloud.tencent.com/document/product/647/35129#trtcspeedtestresult) | 网络测速结果。 |
| [TRTCMixUser](https://intl.cloud.tencent.com/document/product/647/35129#trtcmixuser) | 云端混流中每一路子画面的位置信息。 |
| [TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35129#trtctranscodingconfig) | 云端混流（转码）配置。 |
| [TRTCPublishCDNParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcpublishcdnparam) | 旁路推流参数。 |
| [TRTCAudioRecordingParams](https://intl.cloud.tencent.com/document/product/647/35129#trtcaudiorecordingparams) | 录音参数。 |
| [TRTCAudioEffectParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcaudioeffectparam) | 音效。 |
| [TRTCStatistics](https://intl.cloud.tencent.com/document/product/647/35129#trtcstatistics) | 统计数据。 |
| [TRTCRemoteStatistics](https://intl.cloud.tencent.com/document/product/647/35129#trtcremotestatistics) | 远端成员的音视频统计信息。 |
| [TRTCLocalStatistics](https://intl.cloud.tencent.com/document/product/647/35129#trtclocalstatistics) | 自己本地的音视频统计信息。 |
