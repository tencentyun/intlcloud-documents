## TRTCCloud @ TXLiteAVSDK

腾讯云视频通话功能的主要接口类。

### 创建与销毁

| API | 描述 |
|-----|-----|
| [delegate](https://intl.cloud.tencent.com/document/product/647/35123/35120#delegate) | 设置回调接口 TRTCCloudDelegate。 |
| [delegateQueue](https://intl.cloud.tencent.com/document/product/647/35123/35120#delegatequeue) | 设置驱动 TRTCCloudDelegate 回调的队列。 |
| [sharedInstance](https://intl.cloud.tencent.com/document/product/647/35123/35120#sharedinstance) | 创建 [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35123/35120#trtccloud) 单例。 |
| [destroySharedIntance](https://intl.cloud.tencent.com/document/product/647/35123/35120#destroysharedintance) | 销毁 [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35123/35120#trtccloud) 单例。 |


### 房间相关接口函数

| API | 描述 |
|-----|-----|
| [enterRoom](https://intl.cloud.tencent.com/document/product/647/35123/35120#enterroom) | 进入房间。 |
| [exitRoom](https://intl.cloud.tencent.com/document/product/647/35123/35120#exitroom) | 离开房间。 |
| [switchRole](https://intl.cloud.tencent.com/document/product/647/35123/35120#switchrole) | 切换角色，仅适用于直播场景（TRTCAppSceneLIVE）。 |
| [connectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35123/35120#connectotherroom) | 请求跨房通话（主播 PK）。 |
| [disconnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35123/35120#disconnectotherroom) | 退出跨房通话。 |
| [setDefaultStreamRecvMode](https://intl.cloud.tencent.com/document/product/647/35123/35120#setdefaultstreamrecvmode) | 设置音视频数据接收模式（需要在进房前设置才能生效）。 |


### 视频相关接口函数

| API | 描述 |
|-----|-----|
| [startLocalPreview](https://intl.cloud.tencent.com/document/product/647/35123/35120#startlocalpreview) | 开启本地视频的预览画面 (iOS 版本)。 |
| [startLocalPreview](https://intl.cloud.tencent.com/document/product/647/35123/35120#startlocalpreview2) | 开启本地视频的预览画面 (Mac 版本)。 |
| [stopLocalPreview](https://intl.cloud.tencent.com/document/product/647/35123/35120#stoplocalpreview) | 停止本地视频采集及预览。 |
| [muteLocalVideo](https://intl.cloud.tencent.com/document/product/647/35123/35120#mutelocalvideo) | 是否屏蔽自己的视频画面。 |
| [startRemoteView](https://intl.cloud.tencent.com/document/product/647/35123/35120#startremoteview) | 开始显示远端视频画面。 |
| [stopRemoteView](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopremoteview) | 停止显示远端视频画面。 |
| [stopAllRemoteView](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopallremoteview) | 停止显示所有远端视频画面。 |
| [muteRemoteVideoStream](https://intl.cloud.tencent.com/document/product/647/35123/35120#muteremotevideostream) | 暂停接收指定的远端视频流。 |
| [muteAllRemoteVideoStreams](https://intl.cloud.tencent.com/document/product/647/35123/35120#muteallremotevideostreams) | 停止接收所有远端视频流。 |
| [setVideoEncoderParam](https://intl.cloud.tencent.com/document/product/647/35123/35120#setvideoencoderparam) | 设置视频编码器相关参数。 |
| [setNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35123/35120#setnetworkqosparam) | 设置网络流控相关参数。 |
| [setLocalViewFillMode](https://intl.cloud.tencent.com/document/product/647/35123/35120#setlocalviewfillmode) | 设置本地图像的渲染模式。 |
| [setRemoteViewFillMode](https://intl.cloud.tencent.com/document/product/647/35123/35120#setremoteviewfillmode) | 设置远端图像的渲染模式。 |
| [setLocalViewRotation](https://intl.cloud.tencent.com/document/product/647/35123/35120#setlocalviewrotation) | 设置本地图像的顺时针旋转角度。 |
| [setRemoteViewRotation](https://intl.cloud.tencent.com/document/product/647/35123/35120#setremoteviewrotation) | 设置远端图像的顺时针旋转角度。 |
| [setVideoEncoderRotation](https://intl.cloud.tencent.com/document/product/647/35123/35120#setvideoencoderrotation) | 设置视频编码输出的（也就是远端用户观看到的，以及服务器录制下来的）画面方向。 |
| [setLocalViewMirror](https://intl.cloud.tencent.com/document/product/647/35123/35120#setlocalviewmirror) | 设置本地摄像头预览画面的镜像模式（iOS）。 |
| [setLocalViewMirror](https://intl.cloud.tencent.com/document/product/647/35123/35120#setlocalviewmirror2) | 设置本地摄像头预览画面的镜像模式（Mac）。 |
| [setVideoEncoderMirror](https://intl.cloud.tencent.com/document/product/647/35123/35120#setvideoencodermirror) | 设置编码器输出的画面镜像模式。 |
| [setGSensorMode](https://intl.cloud.tencent.com/document/product/647/35123/35120#setgsensormode) | 设置重力感应的适应模式。 |
| [enableEncSmallVideoStream](https://intl.cloud.tencent.com/document/product/647/35123/35120#enableencsmallvideostream) | 开启大小画面双路编码模式。 |
| [setRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35123/35120#setremotevideostreamtype) | 选定观看指定 uid 的大画面还是小画面。 |
| [setPriorRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35123/35120#setpriorremotevideostreamtype) | 设定观看方优先选择的视频质量。 |


### 音频相关接口函数

| API | 描述 |
|-----|-----|
| [startLocalAudio](https://intl.cloud.tencent.com/document/product/647/35123/35120#startlocalaudio) | 开启本地音频的采集和上行。 |
| [stopLocalAudio](https://intl.cloud.tencent.com/document/product/647/35123/35120#stoplocalaudio) | 关闭本地音频的采集和上行。 |
| [muteLocalAudio](https://intl.cloud.tencent.com/document/product/647/35123/35120#mutelocalaudio) | 静音本地的音频。 |
| [setAudioRoute](https://intl.cloud.tencent.com/document/product/647/35123/35120#setaudioroute) | 设置音频路由。 |
| [muteRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35123/35120#muteremoteaudio) | 静音某一个用户的声音。 |
| [muteAllRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35123/35120#muteallremoteaudio) | 静音所有用户的声音。 |
| [enableAudioVolumeEvaluation](https://intl.cloud.tencent.com/document/product/647/35123/35120#enableaudiovolumeevaluation) | 启用音量大小提示。 |
| [startAudioRecording](https://intl.cloud.tencent.com/document/product/647/35123/35120#startaudiorecording) | 开始录音。 |
| [stopAudioRecording](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopaudiorecording) | 停止录音。 |
| [setSystemVolumeType](https://intl.cloud.tencent.com/document/product/647/35123/35120#setsystemvolumetype) | 设置通话过程中使用的系统音量类型。 |
| [enableAudioEarMonitoring](https://intl.cloud.tencent.com/document/product/647/35123/35120#enableaudioearmonitoring) | 开启耳返。 |


### 摄像头相关接口函数

| API | 描述 |
|-----|-----|
| [switchCamera](https://intl.cloud.tencent.com/document/product/647/35123/35120#switchcamera) | 切换摄像头。 |
| [isCameraZoomSupported](https://intl.cloud.tencent.com/document/product/647/35123/35120#iscamerazoomsupported) | 查询当前摄像头是否支持缩放。 |
| [setZoom](https://intl.cloud.tencent.com/document/product/647/35123/35120#setzoom) | 设置摄像头缩放因子（焦距）。 |
| [isCameraTorchSupported](https://intl.cloud.tencent.com/document/product/647/35123/35120#iscameratorchsupported) | 查询是否支持开关闪光灯（手电筒模式）。 |
| [enbaleTorch](https://intl.cloud.tencent.com/document/product/647/35123/35120#enbaletorch) | 开关闪光灯。 |
| [isCameraFocusPositionInPreviewSupported](https://intl.cloud.tencent.com/document/product/647/35123/35120#iscamerafocuspositioninpreviewsupported) | 查询是否支持设置焦点。 |
| [setFocusPosition](https://intl.cloud.tencent.com/document/product/647/35123/35120#setfocusposition) | 设置摄像头焦点。 |
| [isCameraAutoFocusFaceModeSupported](https://intl.cloud.tencent.com/document/product/647/35123/35120#iscameraautofocusfacemodesupported) | 查询是否支持自动识别人脸位置。 |
| [enableAutoFaceFoucs](https://intl.cloud.tencent.com/document/product/647/35123/35120#enableautofacefoucs) | 自动识别人脸位置。 |
| [getCameraDevicesList](https://intl.cloud.tencent.com/document/product/647/35123/35120#getcameradeviceslist) | 获取摄像头设备列表。 |
| [getCurrentCameraDevice](https://intl.cloud.tencent.com/document/product/647/35123/35120#getcurrentcameradevice) | 获取当前使用的摄像头。 |
| [setCurrentCameraDevice](https://intl.cloud.tencent.com/document/product/647/35123/35120#setcurrentcameradevice) | 设置要使用的摄像头。 |


### 音频设备相关接口函数

| API | 描述 |
|-----|-----|
| [getMicDevicesList](https://intl.cloud.tencent.com/document/product/647/35123/35120#getmicdeviceslist) | 获取麦克风设备列表。 |
| [getCurrentMicDevice](https://intl.cloud.tencent.com/document/product/647/35123/35120#getcurrentmicdevice) | 获取当前的麦克风设备。 |
| [setCurrentMicDevice](https://intl.cloud.tencent.com/document/product/647/35123/35120#setcurrentmicdevice) | 设置要使用的麦克风。 |
| [getCurrentMicDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35123/35120#getcurrentmicdevicevolume) | 获取当前麦克风设备音量。 |
| [setCurrentMicDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35123/35120#setcurrentmicdevicevolume) | 设置麦克风设备的音量。 |
| [getSpeakerDevicesList](https://intl.cloud.tencent.com/document/product/647/35123/35120#getspeakerdeviceslist) | 获取扬声器设备列表。 |
| [getCurrentSpeakerDevice](https://intl.cloud.tencent.com/document/product/647/35123/35120#getcurrentspeakerdevice) | 获取当前的扬声器设备。 |
| [setCurrentSpeakerDevice](https://intl.cloud.tencent.com/document/product/647/35123/35120#setcurrentspeakerdevice) | 设置要使用的扬声器。 |
| [getCurrentSpeakerDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35123/35120#getcurrentspeakerdevicevolume) | 当前扬声器设备音量。 |
| [setCurrentSpeakerDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35123/35120#setcurrentspeakerdevicevolume) | 设置当前扬声器音量。 |


### 美颜滤镜相关接口函数

| API | 描述 |
|-----|-----|
| [getBeautyManager](https://intl.cloud.tencent.com/document/product/647/35123/35120#getbeautymanager) | 获取美颜管理对象。 |
| [setBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35123/35120#setbeautystyle) | 设置美颜、美白以及红润效果级别。 |
| [setFilter](https://intl.cloud.tencent.com/document/product/647/35123/35120#setfilter) | 设置指定素材滤镜特效。 |
| [setFilterConcentration](https://intl.cloud.tencent.com/document/product/647/35123/35120#setfilterconcentration) | 设置滤镜浓度。 |
| [setWatermark](https://intl.cloud.tencent.com/document/product/647/35123/35120#setwatermark) | 添加水印。 |
| [setEyeScaleLevel](https://intl.cloud.tencent.com/document/product/647/35123/35120#seteyescalelevel) | 设置大眼级别（商用企业版有效，其它版本设置此参数无效）。 |
| [setFaceScaleLevel](https://intl.cloud.tencent.com/document/product/647/35123/35120#setfacescalelevel) | 设置瘦脸级别（商用企业版有效，其它版本设置此参数无效）。 |
| [setFaceVLevel](https://intl.cloud.tencent.com/document/product/647/35123/35120#setfacevlevel) | 设置V脸级别（商用企业版有效，其它版本设置此参数无效）。 |
| [setChinLevel](https://intl.cloud.tencent.com/document/product/647/35123/35120#setchinlevel) | 设置下巴拉伸或收缩（商用企业版有效，其它版本设置此参数无效）。 |
| [setFaceShortLevel](https://intl.cloud.tencent.com/document/product/647/35123/35120#setfaceshortlevel) | 设置短脸级别（商用企业版有效，其它版本设置此参数无效）。 |
| [setNoseSlimLevel](https://intl.cloud.tencent.com/document/product/647/35123/35120#setnoseslimlevel) | 设置瘦鼻级别（商用企业版有效，其它版本设置此参数无效）。 |
| [setGreenScreenFile](https://intl.cloud.tencent.com/document/product/647/35123/35120#setgreenscreenfile) | 设置绿幕背景视频（商用企业版有效，其它版本设置此参数无效）。 |
| [selectMotionTmpl](https://intl.cloud.tencent.com/document/product/647/35123/35120#selectmotiontmpl) | 选择使用哪一款 AI 动效挂件（商用企业版有效，其它版本设置此参数无效）。 |
| [setMotionMute](https://intl.cloud.tencent.com/document/product/647/35123/35120#setmotionmute) | 设置动效静音（商用企业版有效，其它版本设置此参数无效）。 |


### 辅流相关接口函数（Mac）

| API | 描述 |
|-----|-----|
| [startRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35123/35120#startremotesubstreamview) | 开始显示远端用户的屏幕分享画面。 |
| [stopRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopremotesubstreamview) | 停止显示远端用户的屏幕分享画面。 |
| [setRemoteSubStreamViewFillMode](https://intl.cloud.tencent.com/document/product/647/35123/35120#setremotesubstreamviewfillmode) | 设置屏幕分享画面的显示模式。 |
| [getScreenCaptureSourcesWithThumbnailSize](https://intl.cloud.tencent.com/document/product/647/35123/35120#getscreencapturesourceswiththumbnailsize) | 枚举可分享的屏幕窗口。 |
| [selectScreenCaptureTarget](https://intl.cloud.tencent.com/document/product/647/35123/35120#selectscreencapturetarget) | 设置屏幕共享参数，该方法在屏幕共享过程中也可以调用。 |
| [startScreenCapture](https://intl.cloud.tencent.com/document/product/647/35123/35120#startscreencapture) | 启动屏幕分享。 |
| [stopScreenCapture](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopscreencapture) | 停止屏幕采集。 |
| [pauseScreenCapture](https://intl.cloud.tencent.com/document/product/647/35123/35120#pausescreencapture) | 暂停屏幕分享。 |
| [resumeScreenCapture](https://intl.cloud.tencent.com/document/product/647/35123/35120#resumescreencapture) | 恢复屏幕分享。 |
| [setSubStreamEncoderParam](https://intl.cloud.tencent.com/document/product/647/35123/35120#setsubstreamencoderparam) | 设置屏幕分享的编码器参数。 |
| [setSubStreamMixVolume](https://intl.cloud.tencent.com/document/product/647/35123/35120#setsubstreammixvolume) | 设置屏幕分享的混音音量大小。 |


### 自定义采集和渲染

| API | 描述 |
|-----|-----|
| [enableCustomVideoCapture](https://intl.cloud.tencent.com/document/product/647/35123/35120#enablecustomvideocapture) | 启用视频自定义采集模式。 |
| [sendCustomVideoData](https://intl.cloud.tencent.com/document/product/647/35123/35120#sendcustomvideodata) | 向 SDK 投送自己采集的视频数据。 |
| [setLocalVideoRenderDelegate](https://intl.cloud.tencent.com/document/product/647/35123/35120#setlocalvideorenderdelegate) | 设置本地视频的自定义渲染回调。 |
| [setRemoteVideoRenderDelegate](https://intl.cloud.tencent.com/document/product/647/35123/35120#setremotevideorenderdelegate) | 设置远端视频的自定义渲染回调。 |
| [enableCustomAudioCapture](https://intl.cloud.tencent.com/document/product/647/35123/35120#enablecustomaudiocapture) | 启用音频自定义采集模式。 |
| [sendCustomAudioData](https://intl.cloud.tencent.com/document/product/647/35123/35120#sendcustomaudiodata) | 向 SDK 投送自己采集的音频数据。 |
| [setAudioFrameDelegate](https://intl.cloud.tencent.com/document/product/647/35123/35120#setaudioframedelegate) | 设置音频数据回调。 |


### 自定义消息发送

| API | 描述 |
|-----|-----|
| [sendCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35123/35120#sendcustomcmdmsg) | 发送自定义消息给房间内所有用户。 |
| [sendSEIMsg](https://intl.cloud.tencent.com/document/product/647/35123/35120#sendseimsg) | 将小数据量的自定义数据嵌入视频帧中。 |


### 背景混音相关接口函数

| API | 描述 |
|-----|-----|
| [playBGM](https://intl.cloud.tencent.com/document/product/647/35123/35120#playbgm) | 启动播放背景音乐。 |
| [stopBGM](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopbgm) | 停止播放背景音乐。 |
| [pauseBGM](https://intl.cloud.tencent.com/document/product/647/35123/35120#pausebgm) | 暂停播放背景音乐。 |
| [resumeBGM](https://intl.cloud.tencent.com/document/product/647/35123/35120#resumebgm) | 继续播放背景音乐。 |
| [getBGMDuration](https://intl.cloud.tencent.com/document/product/647/35123/35120#getbgmduration) | 获取音乐文件总时长，单位毫秒。 |
| [setBGMPosition](https://intl.cloud.tencent.com/document/product/647/35123/35120#setbgmposition) | 设置 BGM 播放进度。 |
| [setMicVolumeOnMixing](https://intl.cloud.tencent.com/document/product/647/35123/35120#setmicvolumeonmixing) | 设置麦克风的音量大小，播放背景音乐混音时使用，用来控制麦克风音量大小。 |
| [setBGMVolume](https://intl.cloud.tencent.com/document/product/647/35123/35120#setbgmvolume) | 设置背景音乐的音量大小，播放背景音乐混音时使用，用来控制背景音音量大小。 |
| [setReverbType](https://intl.cloud.tencent.com/document/product/647/35123/35120#setreverbtype) | 设置混响效果 (目前仅支持 iOS)。 |
| [setVoiceChangerType](https://intl.cloud.tencent.com/document/product/647/35123/35120#setvoicechangertype) | 设置变声类型 (目前仅支持 iOS)。 |

### 音效相关接口函数

| API | 描述 |
|-----|-----|
| [playAudioEffect](https://intl.cloud.tencent.com/document/product/647/35123/35120#playaudioeffect) | 播放音效。 |
| [setAudioEffectVolume](https://intl.cloud.tencent.com/document/product/647/35123/35120#setaudioeffectvolume) | 设置单个音效音量。 |
| [stopAudioEffect](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopaudioeffect) | 停止音效。 |
| [stopAllAudioEffects](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopallaudioeffects) | 停止所有音效。 |
| [setAllAudioEffectsVolume](https://intl.cloud.tencent.com/document/product/647/35123/35120#setallaudioeffectsvolume) | 设置所有音效的音量。 |


### 设备和网络测试

| API | 描述 |
|-----|-----|
| [startSpeedTest](https://intl.cloud.tencent.com/document/product/647/35123/35120#startspeedtest) | 开始进行网络测速（视频通话期间请勿测试，以免影响通话质量）。 |
| [stopSpeedTest](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopspeedtest) | 停止服务器测速。 |
| [startCameraDeviceTestInView](https://intl.cloud.tencent.com/document/product/647/35123/35120#startcameradevicetestinview) | 开始进行摄像头测试。 |
| [stopCameraDeviceTest](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopcameradevicetest) | 结束视频测试预览。 |
| [startMicDeviceTest](https://intl.cloud.tencent.com/document/product/647/35123/35120#startmicdevicetest) | 开始进行麦克风测试。 |
| [stopMicDeviceTest](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopmicdevicetest) | 停止麦克风测试。 |
| [startSpeakerDeviceTest](https://intl.cloud.tencent.com/document/product/647/35123/35120#startspeakerdevicetest) | 开始扬声器测试。 |
| [stopSpeakerDeviceTest](https://intl.cloud.tencent.com/document/product/647/35123/35120#stopspeakerdevicetest) | 停止扬声器测试。 |


### 混流转码以及 CDN 旁路推流

| API | 描述 |
|-----|-----|
| [setMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35123/35120#setmixtranscodingconfig) | 设置云端的混流转码参数。 |
| [startPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35123/35120#startpublishcdnstream) | 旁路转推到指定的推流地址。 |
| [stopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35123/35120#stoppublishcdnstream) | 停止旁路推流。 |


### Log 相关接口函数

| API | 描述 |
|-----|-----|
| [getSDKVersion](https://intl.cloud.tencent.com/document/product/647/35123/35120#getsdkversion) | 获取 SDK 版本信息。 |
| [setLogLevel](https://intl.cloud.tencent.com/document/product/647/35123/35120#setloglevel) | 设置 Log 输出级别。 |
| [setConsoleEnabled](https://intl.cloud.tencent.com/document/product/647/35123/35120#setconsoleenabled) | 启用或禁用控制台日志打印。 |
| [setLogCompressEnabled](https://intl.cloud.tencent.com/document/product/647/35123/35120#setlogcompressenabled) | 启用或禁用 Log 的本地压缩。 |
| [setLogDirPath](https://intl.cloud.tencent.com/document/product/647/35123/35120#setlogdirpath) | 修改日志保存路径。 |
| [setLogDelegate](https://intl.cloud.tencent.com/document/product/647/35123/35120#setlogdelegate) | 设置日志回调。 |
| [showDebugView](https://intl.cloud.tencent.com/document/product/647/35123/35120#showdebugview) | 显示仪表盘。 |
| [setDebugViewMargin](https://intl.cloud.tencent.com/document/product/647/35123/35120#setdebugviewmargin) | 设置仪表盘的边距。 |
| [callExperimentalAPI](https://intl.cloud.tencent.com/document/product/647/35123/35120#callexperimentalapi) | 调用实验性 API 接口。 |


## TRTCCloudDelegate @ TXLiteAVSDK

腾讯云视频通话功能的事件回调接口。

### 错误事件和警告事件

| API | 描述 |
|-----|-----|
| [onError](https://intl.cloud.tencent.com/document/product/647/35123/35121#onerror) | 错误回调：SDK 不可恢复的错误，一定要监听，并分情况给用户适当的界面提示。 |
| [onWarning](https://intl.cloud.tencent.com/document/product/647/35123/35121#onwarning) | 警告回调：用于告知您一些非严重性问题，例如出现了卡顿或者可恢复的解码失败。 |


### 房间事件回调

| API | 描述 |
|-----|-----|
| [onEnterRoom](https://intl.cloud.tencent.com/document/product/647/35123/35121#onenterroom) | 已加入房间的回调。 |
| [onExitRoom](https://intl.cloud.tencent.com/document/product/647/35123/35121#onexitroom) | 离开房间的事件回调。 |
| [onSwitchRole](https://intl.cloud.tencent.com/document/product/647/35123/35121#onswitchrole) | 切换角色的事件回调。 |
| [onConnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35123/35121#onconnectotherroom) | 请求跨房通话（主播 PK）的结果回调。 |
| [onDisconnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35123/35121#ondisconnectotherroom) | 结束跨房通话（主播 PK）的结果回调。 |


### 成员事件回调

| API | 描述 |
|-----|-----|
| [onRemoteUserEnterRoom](https://intl.cloud.tencent.com/document/product/647/35123/35121#onremoteuserenterroom) | 有用户加入当前房间。 |
| [onRemoteUserLeaveRoom](https://intl.cloud.tencent.com/document/product/647/35123/35121#onremoteuserleaveroom) | 有用户离开当前房间。 |
| [onUserVideoAvailable](https://intl.cloud.tencent.com/document/product/647/35123/35121#onuservideoavailable) | 用户是否开启摄像头视频。 |
| [onUserSubStreamAvailable](https://intl.cloud.tencent.com/document/product/647/35123/35121#onusersubstreamavailable) | 用户是否开启屏幕分享。 |
| [onUserAudioAvailable](https://intl.cloud.tencent.com/document/product/647/35123/35121#onuseraudioavailable) | 用户是否开启音频上行。 |
| [onFirstVideoFrame](https://intl.cloud.tencent.com/document/product/647/35123/35121#onfirstvideoframe) | 开始渲染本地或远程用户的首帧画面。 |
| [onFirstAudioFrame](https://intl.cloud.tencent.com/document/product/647/35123/35121#onfirstaudioframe) | 开始播放远程用户的首帧音频（本地声音暂不通知）。 |
| [onSendFirstLocalVideoFrame](https://intl.cloud.tencent.com/document/product/647/35123/35121#onsendfirstlocalvideoframe) | 首帧本地视频数据已经被送出。 |
| [onSendFirstLocalAudioFrame](https://intl.cloud.tencent.com/document/product/647/35123/35121#onsendfirstlocalaudioframe) | 首帧本地音频数据已经被送出。 |
| [onUserEnter](https://intl.cloud.tencent.com/document/product/647/35123/35121#onuserenter) | 废弃接口：有主播加入当前房间。 |
| [onUserExit](https://intl.cloud.tencent.com/document/product/647/35123/35121#onuserexit) | 废弃接口： 有主播离开当前房间。 |


### 统计和质量回调

| API | 描述 |
|-----|-----|
| [onNetworkQuality](https://intl.cloud.tencent.com/document/product/647/35123/35121#onnetworkquality) | 网络质量：该回调每2秒触发一次，统计当前网络的上行和下行质量。 |
| [onStatistics](https://intl.cloud.tencent.com/document/product/647/35123/35121#onstatistics) | 技术指标统计回调。 |


### 服务器事件回调

| API | 描述 |
|-----|-----|
| [onConnectionLost](https://intl.cloud.tencent.com/document/product/647/35123/35121#onconnectionlost) | SDK 跟服务器的连接断开。 |
| [onTryToReconnect](https://intl.cloud.tencent.com/document/product/647/35123/35121#ontrytoreconnect) | SDK 尝试重新连接到服务器。 |
| [onConnectionRecovery](https://intl.cloud.tencent.com/document/product/647/35123/35121#onconnectionrecovery) | SDK 跟服务器的连接恢复。 |


### 硬件设备事件回调

| API | 描述 |
|-----|-----|
| [onCameraDidReady](https://intl.cloud.tencent.com/document/product/647/35123/35121#oncameradidready) | 摄像头准备就绪。 |
| [onMicDidReady](https://intl.cloud.tencent.com/document/product/647/35123/35121#onmicdidready) | 麦克风准备就绪。 |
| [onAudioRouteChanged](https://intl.cloud.tencent.com/document/product/647/35123/35121#onaudioroutechanged) | 音频路由发生变化（仅 iOS），音频路由即声音由哪里输出（扬声器、听筒）。 |
| [onUserVoiceVolume](https://intl.cloud.tencent.com/document/product/647/35123/35121#onuservoicevolume) | 用于提示音量大小的回调,包括每个 userId 的音量和远端总音量。 |
| [onDevice](https://intl.cloud.tencent.com/document/product/647/35123/35121#ondevice) | 本地设备通断回调。 |


### 自定义消息的接收回调

| API | 描述 |
|-----|-----|
| [onRecvCustomCmdMsgUserId](https://intl.cloud.tencent.com/document/product/647/35123/35121#onrecvcustomcmdmsguserid) | 收到自定义消息回调。 |
| [onMissCustomCmdMsgUserId](https://intl.cloud.tencent.com/document/product/647/35123/35121#onmisscustomcmdmsguserid) | 自定义消息丢失回调。 |
| [onRecvSEIMsg](https://intl.cloud.tencent.com/document/product/647/35123/35121#onrecvseimsg) | 收到 SEI 消息的回调。 |


### CDN 旁路转推回调

| API | 描述 |
|-----|-----|
| [onStartPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35123/35121#onstartpublishcdnstream) | 启动旁路推流到 CDN 完成的回调。 |
| [onStopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35123/35121#onstoppublishcdnstream) | 停止旁路推流到 CDN 完成的回调。 |
| [onSetMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35123/35121#onsetmixtranscodingconfig) | 设置云端的混流转码参数的回调，对应于 [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35123/35120#trtccloud) 中的 setMixTranscodingConfig() 接口。 |


### 音效回调

| API | 描述 |
|-----|-----|
| [onAudioEffectFinished](https://intl.cloud.tencent.com/document/product/647/35123/35121#onaudioeffectfinished) | 播放音效结束回调。 |


### 屏幕分享回调

| API | 描述 |
|-----|-----|
| [onScreenCaptureStarted](https://intl.cloud.tencent.com/document/product/647/35123/35121#onscreencapturestarted) | 当屏幕分享开始时，SDK 会通过此回调通知。 |
| [onScreenCapturePaused](https://intl.cloud.tencent.com/document/product/647/35123/35121#onscreencapturepaused) | 当屏幕分享暂停时，SDK 会通过此回调通知。 |
| [onScreenCaptureResumed](https://intl.cloud.tencent.com/document/product/647/35123/35121#onscreencaptureresumed) | 当屏幕分享恢复时，SDK 会通过此回调通知。 |
| [onScreenCaptureStoped](https://intl.cloud.tencent.com/document/product/647/35123/35121#onscreencapturestoped) | 当屏幕分享停止时，SDK 会通过此回调通知。 |

### 自定义视频渲染回调
跳转到 [TRTCVideoRenderDelegate](https://intl.cloud.tencent.com/document/product/647/35123/35121#trtcvideorenderdelegate)

| API | 描述 |
|-----|-----|
| [onRenderVideoFrame](https://intl.cloud.tencent.com/document/product/647/35123/35121#onrendervideoframe) | 自定义视频渲染回调。 |


### 声音数据帧的自定义处理回调
跳转到 [TRTCAudioFrameDelegate](https://intl.cloud.tencent.com/document/product/647/35123/35121#trtcaudioframedelegate)

| API | 描述 |
|-----|-----|
| [onCapturedAudioFrame](https://intl.cloud.tencent.com/document/product/647/35123/35121#oncapturedaudioframe) | 本地麦克风采集到的音频数据回调。 |
| [onPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35123/35121#onplayaudioframe) | 混音前的每一路远程用户的音频数据（例如您要对某一路的语音进行文字转换，必须要使用这里的原始数据，而不是混音之后的数据）。 |
| [onMixedPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35123/35121#onmixedplayaudioframe) | 各路音频数据混合后送入喇叭播放的音频数据。 |


### 日志相关回调
跳转到 [TRTCLogDelegate](https://intl.cloud.tencent.com/document/product/647/35123/35121#trtclogdelegate)

建议在一个比较早初始化的类中设置回调委托对象，如 AppDelegate。

| API | 描述 |
|-----|-----|
| [onLog](https://intl.cloud.tencent.com/document/product/647/35123/35121#onlog) | 有日志打印时的回调。 |


### 音效回调

| API | 描述 |
|-----|-----|
| [onAudioEffectFinished](https://intl.cloud.tencent.com/document/product/647/35123/35121#onaudioeffectfinished) | 播放音效结束回调。 |

## 关键类型定义

| 类型定义 | 描述 |
|-----|-----|
| [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35123#trtcparams) | 进房相关参数。 |
| [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoencparam) | 视频编码参数。 |
| [TRTCNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcnetworkqosparam) | 网络流控相关参数。 |
| [TRTCQualityInfo](https://intl.cloud.tencent.com/document/product/647/35123#trtcqualityinfo) | 视频质量。 |
| [TRTCVolumeInfo](https://intl.cloud.tencent.com/document/product/647/35123#trtcvolumeinfo) | 音量大小。 |
| [TRTCMediaDeviceInfo](https://intl.cloud.tencent.com/document/product/647/35123#trtcmediadeviceinfo) | 媒体设备描述。 |
| [TRTCScreenCaptureSourceInfo](https://intl.cloud.tencent.com/document/product/647/35123#trtcscreencapturesourceinfo) | 屏幕分享目标信息（仅 Mac）。 |
| [TRTCSpeedTestResult](https://intl.cloud.tencent.com/document/product/647/35123#trtcspeedtestresult) | 网络测速结果。 |
| [TRTCVideoFrame](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoframe) | 视频帧信息。 |
| [TRTCAudioFrame](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudioframe) | 音频帧数据。 |
| [TRTCMixUser](https://intl.cloud.tencent.com/document/product/647/35123#trtcmixuser) | 云端混流中每一路子画面的位置信息。 |
| [TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35123#trtctranscodingconfig) | 云端混流（转码）配置。 |
| [TRTCPublishCDNParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcpublishcdnparam) | CDN 旁路推流参数。 |
| [TRTCAudioRecordingParams](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudiorecordingparams) | 录音参数。 |
| [TRTCAudioEffectParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudioeffectparam) | 音效。 |
| [TRTCLocalStatistics](https://intl.cloud.tencent.com/document/product/647/35123#trtclocalstatistics) | 自己本地的音视频统计信息。 |
| [TRTCRemoteStatistics](https://intl.cloud.tencent.com/document/product/647/35123#trtcremotestatistics) | 远端成员的音视频统计信息。 |
| [TRTCStatistics](https://intl.cloud.tencent.com/document/product/647/35123#trtcstatistics) | 统计数据。 |

### 枚举值

| 枚举 | 描述 |
|-----|-----|
| [TRTCVideoResolution](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoresolution) | 视频分辨率。 |
| [TRTCVideoResolutionMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoresolutionmode) | 视频宽高比模式。 |
| [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideostreamtype) | 视频流类型。 |
| [TRTCQuality](https://intl.cloud.tencent.com/document/product/647/35123#trtcquality) | 画质级别。 |
| [TRTCVideoFillMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideofillmode) | 视频画面填充模式。 |
| [TRTCVideoRotation](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideorotation) | 视频画面旋转方向。 |
| [TRTCBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35123#trtcbeautystyle) | 美颜（磨皮）算法。 |
| [TRTCVideoPixelFormat](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideopixelformat) | 视频像素格式。 |
| [TRTCVideoBufferType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideobuffertype) | 视频数据包装格式。 |
| [TRTCLocalVideoMirrorType](https://intl.cloud.tencent.com/document/product/647/35123#trtclocalvideomirrortype) | 本地视频预览镜像类型。 |
| [TRTCAppScene](https://intl.cloud.tencent.com/document/product/647/35123#trtcappscene) | 应用场景。 |
| [TRTCRoleType](https://intl.cloud.tencent.com/document/product/647/35123#trtcroletype) | 角色，仅适用于直播场景（TRTCAppSceneLIVE）。 |
| [TRTCQosControlMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcqoscontrolmode) | 流控模式。 |
| [TRTCVideoQosPreference](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoqospreference) | 画质偏好。 |
| [TRTCAudioSampleRate](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudiosamplerate) | 音频采样率。 |
| [TRTCAudioRoute](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudioroute) | 声音播放模式（音频路由）。 |
| [TRTCReverbType](https://intl.cloud.tencent.com/document/product/647/35123#trtcreverbtype) | 声音混响模式。 |
| [TRTCVoiceChangerType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvoicechangertype) | 变声模式。 |
| [TRTCSystemVolumeType](https://intl.cloud.tencent.com/document/product/647/35123#trtcsystemvolumetype) | 系统音量类型。 |
| [TRTCLogLevel](https://intl.cloud.tencent.com/document/product/647/35123#trtcloglevel) | Log 级别。 |
| [TRTCGSensorMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcgsensormode) | 重力感应开关。 |
| [TRTCMediaDeviceType](https://intl.cloud.tencent.com/document/product/647/35123#trtcmediadevicetype) | 设备类型（仅 Mac）。 |
| [TRTCScreenCaptureSourceType](https://intl.cloud.tencent.com/document/product/647/35123#trtcscreencapturesourcetype) | 屏幕分享目标类型（仅 Mac）。 |
| [TRTCTranscodingConfigMode](https://intl.cloud.tencent.com/document/product/647/35123#trtctranscodingconfigmode) | 混流参数配置模式。 |


