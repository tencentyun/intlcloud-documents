## 1.1 视频分辨率

此处仅定义了横屏分辨率，如需使用竖屏分辨率（例如360 × 640），需要同时指定 TRTCVideoResolutionMode 为 Portrait。

| 常量 | 描述 |
|-----|-----|
| TRTC_VIDEO_RESOLUTION_120_120 | \[C] 建议码率80kbps。 |
| TRTC_VIDEO_RESOLUTION_160_160 | \[C] 建议码率100kbps。 |
| TRTC_VIDEO_RESOLUTION_270_270 | \[C] 建议码率200kbps。 |
| TRTC_VIDEO_RESOLUTION_480_480 | \[C] 建议码率350kbps。 |
| TRTC_VIDEO_RESOLUTION_160_120 | \[C] 建议码率100kbps。 |
| TRTC_VIDEO_RESOLUTION_240_180 | \[C] 建议码率150kbps。 |
| TRTC_VIDEO_RESOLUTION_280_210 | \[C] 建议码率200kbps。 |
| TRTC_VIDEO_RESOLUTION_320_240 | \[C] 建议码率250kbps。 |
| TRTC_VIDEO_RESOLUTION_400_300 | \[C] 建议码率300kbps。 |
| TRTC_VIDEO_RESOLUTION_480_360 | \[C] 建议码率400kbps。 |
| TRTC_VIDEO_RESOLUTION_640_480 | \[C] 建议码率600kbps。 |
| TRTC_VIDEO_RESOLUTION_960_720 | \[C] 建议码率1000kbps。 |
| TRTC_VIDEO_RESOLUTION_160_90 | \[C] 建议码率100kbps。 |
| TRTC_VIDEO_RESOLUTION_256_144 | \[C] 建议码率150kbps。 |
| TRTC_VIDEO_RESOLUTION_320_180 | \[C] 建议码率250kbps。 |
| TRTC_VIDEO_RESOLUTION_480_270 | \[C] 建议码率350kbps。 |
| TRTC_VIDEO_RESOLUTION_640_360 | \[C] 建议码率550kbps。 |
| TRTC_VIDEO_RESOLUTION_960_540 | \[C] 建议码率850kbps。 |
| TRTC_VIDEO_RESOLUTION_1280_720 | \[C] 建议码率1200kbps。 |

## 1.2 视频宽高比模式


- 横屏分辨率：TRTCVideoResolution_640_360 + TRTCVideoResolutionModeLandscape = 640 × 360
- 竖屏分辨率：TRTCVideoResolution_640_360 + TRTCVideoResolutionModePortrait = 360 × 640



| 常量 | 描述 |
|-----|-----|
| TRTC_VIDEO_RESOLUTION_MODE_LANDSCAPE | 横屏分辨率。 |
| TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT | 竖屏分辨率。 |

## 1.3 视频流类型

TRTC 内部有三种不同的音视频流，分别是：
- 主画面：最常用的一条线路，一般用来传输摄像头的视频数据。
- 小画面：跟主画面的内容相同，但是分辨率和码率更低。
- 辅流画面：一般用于屏幕分享，以及远程播片（例如老师放一段视频给学生）。

>?
>- 如果主播的上行网络和性能比较好，则可以同时送出大小两路画面。
>- SDK 不支持单独开启小画面，小画面必须依附于主画面而存在。



| 常量 | 描述 |
|-----|-----|
| TRTC_VIDEO_STREAM_TYPE_BIG | 主画面视频流。 |
| TRTC_VIDEO_STREAM_TYPE_SMALL | 小画面视频流。 |
| TRTC_VIDEO_STREAM_TYPE_SUB | 辅流（屏幕分享）。 |

<span id="quality"></span>
## 1.4 视频（或网络）质量常量定义

TRTC SDK 对画质定义了六种不同的级别，Excellent 代表最好，Down 代表不可用。

| 常量 | 描述 |
|-----|-----|
| TRTC_QUALITY_UNKNOWN | 未定义。 |
| TRTC_QUALITY_Excellent | 最好。 |
| TRTC_QUALITY_Good | 好。 |
| TRTC_QUALITY_Poor | 一般。 |
| TRTC_QUALITY_Bad | 差。 |
| TRTC_QUALITY_Vbad | 很差。 |
| TRTC_QUALITY_Down | 不可用。 |

## 1.5 视频画面填充模式

如果画面的显示分辨率不等于画面的原始分辨率，就需要您设置画面的填充模式:
- TRTCVideoFillMode_Fill，图像铺满屏幕，超出显示视窗的视频部分将被截掉，所以画面显示可能不完整。
- TRTCVideoFillMode_Fit，图像长边填满屏幕，短边区域会被填充黑色，但画面的内容肯定是完整的。



| 常量 | 描述 |
|-----|-----|
| TRTC_VIDEO_RENDER_MODE_FILL | 图像铺满屏幕，超出显示视窗的视频部分将被截掉。 |
| TRTC_VIDEO_RENDER_MODE_FIT | 图像长边填满屏幕，短边区域会被填充黑色。 |

## 1.6 视频画面旋转方向

TRTC SDK 提供了对本地和远程画面的旋转角度设置 API，如下的旋转角度都是指顺时针方向的。

| 常量 | 描述 |
|-----|-----|
| TRTC_VIDEO_ROTATION_0 | 不旋转。 |
| TRTC_VIDEO_ROTATION_90 | 顺时针旋转90度。 |
| TRTC_VIDEO_ROTATION_180 | 顺时针旋转180度。 |
| TRTC_VIDEO_ROTATION_270 | 顺时针旋转270度。 |

## 1.7 美颜（磨皮）算法

TRTC SDK 内置多种不同的磨皮算法，您可以选择最适合您产品定位的方案。

| 常量 | 描述 |
|-----|-----|
| TRTC_BEAUTY_STYLE_SMOOTH | 光滑，适用于美女秀场，效果比较明显。 |
| TRTC_BEAUTY_STYLE_NATURE | 自然，磨皮算法更多地保留了面部细节，主观感受上会更加自然。 |

<span id="TRTC_VIDEO_PIXEL_FORMAT"></span>
## 1.8 视频像素格式

TRTC SDK 提供针对视频的自定义采集和自定义渲染功能，在自定义采集功能中，您可以用如下枚举值描述您采集的视频像素格式。 在自定义渲染功能中，您可以指定您期望 SDK 回调的视频像素格式。

| 常量 | 描述 |
|-----|-----|
| TRTC_VIDEO_PIXEL_FORMAT_UNKNOWN | 未知。 |
| TRTC_VIDEO_PIXEL_FORMAT_I420 | YUV I420 |
| TRTC_VIDEO_PIXEL_FORMAT_Texture_2D | OpenGL 2D 纹理。 |
| TRTC_VIDEO_PIXEL_FORMAT_TEXTURE_EXTERNAL_OES | - |
| TRTC_VIDEO_PIXEL_FORMAT_NV21 | - |

<span id="TRTC_VIDEO_MIRROR_TYPE"></span>
## 1.9 本地视频画面预览镜像类型

TRTC SDK 提供了对本地预览画面的镜像设置功能，默认是 AUTO 类型。

| 常量 | 描述 |
|-----|-----|
| TRTC_VIDEO_MIRROR_TYPE_AUTO | SDK 决定镜像方式：前置摄像头镜像，后置摄像头不镜像。 |
| TRTC_VIDEO_MIRROR_TYPE_ENABLE | 前置摄像头和后置摄像头都镜像。 |
| TRTC_VIDEO_MIRROR_TYPE_DISABLE | 前置摄像头和后置摄像头都不镜像。 |

<span id="TRTC_VIDEO_BUFFER_TYPE"></span>
## 1.10 视频数据包装格式

在自定义采集和自定义渲染功能，您需要用到如下枚举值来指定您希望以什么类型的容器来包装视频数据。

| 常量 | 描述 |
|-----|-----|
| TRTC_VIDEO_BUFFER_TYPE_UNKNOWN | 未知。 |
| TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER | DirectBuffer，装载 I420 等 buffer，在 native 层使用。 |
| TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY | byte[]，装载 I420 等 buffer，在 Java 层使用。 |
| TRTC_VIDEO_BUFFER_TYPE_TEXTURE | 直接操作纹理 ID，性能最好，画质损失最少。 |

## 2.1 应用场景

TRTC 可用于视频会议和在线直播等多种应用场景，针对不同的应用场景，TRTC SDK 的内部会进行不同的优化配置：
- VideoCall：视频通话场景，即绝大多数时间都是两人或两人以上视频通话的场景，例如1v1的在线课程辅导，1vN (N < 8) 的视频会议或者小班课堂。
- LIVE：在线直播场景，即绝大多数时间都是一人直播，偶尔有多人视频互动的场景，例如美女秀场连麦等场景。



| 常量 | 描述 |
|-----|-----|
| TRTC_APP_SCENE_VIDEOCALL | 视频通话场景，内部编码器和网络协议优化侧重流畅性，降低通话延迟和卡顿率。 |
| TRTC_APP_SCENE_LIVE | 在线直播场景，内部编码器和网络协议优化侧重性能和兼容性，性能和清晰度表现更佳。 |

## 2.2 角色，仅适用于直播场景（TRTCAppSceneLIVE）

在直播场景中，多数用户只是观众，只有个别用户是主播，这种角色区分可以有利于 TRTC 进行更好的定向优化。
- Anchor：主播，可以上行视频和音频，一个房间里最多支持20个主播同时上行音视频。
- Audience：观众，只能观看，不能上行视频和音频，一个房间里的观众人数没有上限。

| 常量 | 描述 |
|-----|-----|
| TRTCRoleAnchor | 主播。 |
| TRTCRoleAudience | 观众。 |

## 2.3 流控模式

TRTC SDK 内部需要时刻根据网络情况调整内部的编解码器和网络模块，以便能够对网络的变化做出反应。 为了支持快速算法升级，SDK 内部设置了两种不同的流控模式：
- ModeServer：云端控制，默认模式，推荐选择。
- ModeClient：本地控制，用于 SDK 开发内部调试，客户请勿使用。


>?推荐您使用云端控制，这样每当我们升级 Qos 算法时，您无需升级 SDK 即可体验更好的效果。



| 常量 | 描述 |
|-----|-----|
| VIDEO_QOS_CONTROL_CLIENT | 客户端控制（用于 SDK 开发内部调试，客户请勿使用）。 |
| VIDEO_QOS_CONTROL_SERVER | 云端控制 （默认）。 |

## 2.4 画质偏好

指当 TRTC SDK 在遇到弱网络环境时，您是希望“保清晰”还是“保流畅”：
- Smooth：弱网下保流畅，在遭遇弱网环境时首先确保声音的流畅和优先发送，画面会变得模糊且会有较多马赛克，但可以保持流畅不卡顿。
- Clear：弱网下保清晰，在遭遇弱网环境时，画面会尽可能保持清晰，但可能会更容易出现卡顿。



| 常量 | 描述 |
|-----|-----|
| TRTC_VIDEO_QOS_PREFERENCE_SMOOTH | 弱网下保流畅。 |
| TRTC_VIDEO_QOS_PREFERENCE_CLEAR | 弱网下保清晰。 |

## 3.1 音频采样率

音频采样率用来衡量声音的保真程度，采样率越高保真程度越好，如果您的应用场景有音乐的存在，推荐使用 TRTCAudioSampleRate48000。

| 常量 | 描述 |
|-----|-----|
| TRTCAudioSampleRate16000 | 16k采样率。 |
| TRTCAudioSampleRate32000 | 32采样率。 |
| TRTCAudioSampleRate44100 | 44.1k采样率。 |
| TRTCAudioSampleRate48000 | 48k采样率。 |

<span id="TRTC_AUDIO_ROUTE"></span>
## 3.2 声音播放模式（音频路由）

微信和手机 QQ 里的视频通话功能，都有一个免提模式，开启后就不用把手机贴在耳朵上，这个功能就是基于音频路由实现的。 一般手机都有两个扬声器，设置音频路由的作用就是要决定声音从哪个扬声器播放出来：
- Speakerphone：扬声器，位于手机底部，声音偏大，适合外放音乐。
- Earpiece：听筒，位于手机顶部，声音偏小，适合通话。



| 常量 | 描述 |
|-----|-----|
| TRTC_AUDIO_ROUTE_SPEAKER | 扬声器。 |
| TRTC_AUDIO_ROUTE_EARPIECE | 听筒。 |

## 3.3 声音混响模式
| 常量 | 描述 |
|-----|-----|
| TRTC_REVERB_TYPE_0 | 关闭混响。 |
| TRTC_REVERB_TYPE_1 | KTV |
| TRTC_REVERB_TYPE_2 | 小房间。 |
| TRTC_REVERB_TYPE_3 | 大会堂。 |
| TRTC_REVERB_TYPE_4 | 低沉。 |
| TRTC_REVERB_TYPE_5 | 洪亮。 |
| TRTC_REVERB_TYPE_6 | 金属声。 |
| TRTC_REVERB_TYPE_7 | 磁性。 |

## 3.4 变声类型
| 常量 | 描述 |
|-----|-----|
| TRTC_VOICE_CHANGER_TYPE_0 | 关闭变声。 |
| TRTC_VOICE_CHANGER_TYPE_1 | 熊孩子。 |
| TRTC_VOICE_CHANGER_TYPE_2 | 萝莉。 |
| TRTC_VOICE_CHANGER_TYPE_3 | 大叔。 |
| TRTC_VOICE_CHANGER_TYPE_4 | 重金属。 |
| TRTC_VOICE_CHANGER_TYPE_5 | 感冒。 |
| TRTC_VOICE_CHANGER_TYPE_6 | 外国人。 |
| TRTC_VOICE_CHANGER_TYPE_7 | 困兽。 |
| TRTC_VOICE_CHANGER_TYPE_8 | 死肥仔。 |
| TRTC_VOICE_CHANGER_TYPE_9 | 强电流。 |
| TRTC_VOICE_CHANGER_TYPE_10 | 重机械。 |
| TRTC_VOICE_CHANGER_TYPE_11 | 空灵。 |

## 3.5 音频帧的格式
| 常量 | 描述 |
|-----|-----|
| TRTC_AUDIO_FRAME_FORMAT_PCM | PCM |


<span id="TRTCSystemVolumeType"></span>
## 3.6 系统音量类型

智能手机一般具备两种系统音量类型，即通话音量类型和媒体音量类型。
- 通话音量：手机专门为 VOIP 场景设计的音量类型，会强制开启回声抵消（AEC），音质较差，同时音量无法调成0。
- 媒体音量：手机专门为播放器音乐和电影而设计的音量类型，不会开启 AEC，通过调节手机的音量调节键可以将音量调成0。 在媒体音量模式下，如果需要开启 AEC (回声抵消)，需要 SDK 用自带的声学算法来处理。

SDK 目前提供了两种系统音量类型的控制模式，分别为：
- TRTCSystemVolumeTypeAuto：“麦上通话，麦下媒体”，即在进行连麦时使用通话音量模式，仅作为观众观看不进行连麦时使用媒体音量。
- TRTCSystemVolumeTypeMedia：全程使用媒体音量，如果进入通话模式，SDK 会使用自带的声学算法来进行回声抵消。


| 常量 | 描述 |
|-----|-----|
| TRTCSystemVolumeTypeAuto | 默认类型，SDK 会自动选择合适的音量类型。 |
| TRTCSystemVolumeTypeMedia | 仅使用媒体音量，SDK 不再使用通话音量。 |

## 4.1 界面调试 Log
| 常量 | 描述 |
|-----|-----|
| TRTC_DEBUG_VIEW_LEVEL_GONE | 界面不显示 Log。 |
| TRTC_DEBUG_VIEW_LEVEL_STATUS | 界面上半部分显示状态 Log。 |
| TRTC_DEBUG_VIEW_LEVEL_ALL | 界面上半部分显示状态 Log，下半部分显示关键事件。 |

## 4.2 Log 级别

不同的日志等级定义了不同的详实程度和日志数量，推荐一般情况下将日志等级设置为：TRTC_LOG_LEVEL_INFO。

| 常量 | 描述 |
|-----|-----|
| TRTC_LOG_LEVEL_VERBOSE | 输出所有级别的 Log。 |
| TRTC_LOG_LEVEL_DEBUG | 输出 DEBUG，INFO，WARNING，ERROR 和 FATAL 级别的 Log。 |
| TRTC_LOG_LEVEL_INFO | 输出 INFO，WARNING，ERROR 和 FATAL 级别的 Log。 |
| TRTC_LOG_LEVEL_WARN | 输出 WARNING，ERROR 和 FATAL 级别的 Log。 |
| TRTC_LOG_LEVEL_ERROR | 只输出 ERROR 和 FATAL 级别的 Log。 |
| TRTC_LOG_LEVEL_FATAL | 只输出 FATAL 级别的 Log。 |
| TRTC_LOG_LEVEL_NULL | 不输出任何 SDK Log。 |

## 4.3 重力感应开关

此配置适用于 Phone 和 Pad 等移动设备，并且需要配合您当前 UI 的布局模式一起使用
- Disable，如果您不希望视频画面跟随重力感应方向而调整。
- UIAutoLayout，SDK 不会自动调整 LocalVideoView 的旋转方向，而是交给系统进行处理，这需要您的 App 界面已经针对重力感应做了适配工作。
- UIFixLayout，SDK 自动调整 LocalVideoView 的旋转方向，适用于您的 App 界面没有做重力感应适配的情况下。



| 常量 | 描述 |
|-----|-----|
| TRTC_GSENSOR_MODE_DISABLE | 关闭重力感应。 |
| TRTC_GSENSOR_MODE_UIAUTOLAYOUT | 开启重力感应，需要您的 App 界面已经针对重力感应做了适配工作。 |
| TRTC_GSENSOR_MODE_UIFIXLAYOUT | 开启重力感应，适用于您的 App 界面没有做重力感应适配的情况下。 |

## 4.4 混流参数配置模式

目前暂仅支持手动配置这一种模式，即需要指定 TRTC_TranscodingConfigMode_Manual 的全部参数。

| 常量 | 描述 |
|-----|-----|
| TRTC_TranscodingConfigMode_Unknown | 未定义。 |
| TRTC_TranscodingConfigMode_Manual | 手动配置混流混流参数，需要指定 TRTCTranscodingConfig 的全部参数。 |


## TRTCParams

__功能__

进房参数。

__介绍__

作为 TRTC SDK 的进房参数，只有该参数填写正确，才能顺利进入 roomId 所指定的音视频房间。




__属性列表__

| 属性 | 类型 | 字段含义 | 推荐取值 |
|-----|-----|-----|-----|
| sdkAppId | int | 应用标识 [必填] 腾讯云基于 sdkAppId 完成计费统计。 | - |
| userId | String | 用户标识 [必填] 当前用户的 userId，相当于用户名。 | - |
| userSig | String | 用户签名 [必填] 当前 userId 对应的验证签名，相当于登录密码。 | - |
| roomId | int | 房间号码 [必填] 指定房间号，在同一个房间里的用户（userId）可以彼此看到对方并进行视频通话。 | - |
| role | int | 直播场景下的角色，仅适用于直播场景（TRTCAppSceneLIVE），视频通话场景下指定无效。 | 默认值：主播（TRTCRoleAnchor）。 |
| privateMapKey | String | 房间签名 [非必选] 如果您希望某个房间（roomId）只让特定的某些用户（userId）才能进入，就需要使用 privateMapKey 进行权限保护。 | - |
| businessInfo | String | 业务数据 [非必选] 某些非常用的高级特性才需要用到此字段。 | - |




## TRTCVideoEncParam

__功能__

编码参数。

__介绍__

视频编码器相关参数，该设置决定了远端用户看到的画面质量（同时也是云端录制出的视频文件的画面质量）。




__属性列表__

| 属性 | 类型 | 字段含义 | 推荐取值 | 特别说明 |
|-----|-----|-----|-----|-----|
| videoResolution | int | 视频分辨率。 | - 视频通话建议选择360 × 640及以下分辨率，resMode 选择 Portrait。- 手机直播建议选择540 × 960，resMode 选择 Portrait。<br><br>- Window 和 iMac 建议选择640 × 360及以上分辨率，resMode 选择 Landscape。 | TRTCVideoResolution 默认只有横屏模式的分辨率，例如640 × 360。<br> 如需使用竖屏分辨率，请指定 resMode 为 Portrait，例如640 × 360结合 Portrait 则为360 × 640。 |
| videoResolutionMode | int | 分辨率模式（横屏分辨率 - 竖屏分辨率）。 | 手机直播建议选择 Portrait，Window 和 Mac 建议选择 Landscape。 | 如果 videoResolution 指定分辨率640 × 360，resMode 指定模式为 Portrait，则最终编码出的分辨率为360 × 640。 |
| videoFps | int | 视频采集帧率。 | 15fps或20fps，5fps以下，卡顿感明显。10fps以下，会有轻微卡顿感。20fps以上，则过于浪费（电影的帧率为24fps）。 | 很多 Android 手机的前置摄像头并不支持15fps以上的采集帧率，部分过于突出美颜功能的 Android 手机前置摄像头的采集帧率可能低于10fps。 |
| videoBitrate | int | 视频上行码率。 | 推荐设置请参考本文件前半部分 TRTCVideoResolution 定义处的注释说明。 | 码率太低会导致视频中有很多的马赛克。 |



## TRTCNetworkQosParam

__功能__

网络流控相关参数。

__介绍__

该设置决定 SDK 在各种网络环境下的调控方向（例如弱网下选择“保清晰”或“保流畅”）。




__属性列表__

| 属性 | 类型 | 字段含义 | 推荐取值 | 特别说明 |
|-----|-----|-----|-----|-----|
| preference | int | 弱网下是“保清晰”还是“保流畅”。 | - | - 弱网下保流畅：在遭遇弱网环境时，画面会变得模糊，且出现较多马赛克，但可以保持流畅不卡顿<br><br>- 弱网下保清晰：在遭遇弱网环境时，画面会尽可能保持清晰，但可能容易出现卡顿。 |
| controlMode | int | 视频分辨率（云端控制 - 客户端控制）。 | 云端控制。 | - Server 模式（默认）：云端控制模式，若没有特殊原因，请直接使用该模式<br><br>- Client 模式：客户端控制模式，用于 SDK 开发内部调试，客户请勿使用。 |



## TRTCQuality

__功能__

视频（或网络）质量。




__属性列表__

| 属性 | 类型 | 字段含义 |
|-----|-----|-----|
| userId | String | 用户 ID。 |
| quality | int | 网络质量，定义参见 [视频（或网络）质量常量定义](#quality)。 |



## TRTCTexture

__功能__

视频纹理数据，包含纹理 ID 及 EGL 环境。




__属性列表__

| 属性 | 类型 | 字段含义 |
|-----|-----|-----|
| textureId | int | 视频纹理 ID。 |
| eglContext10 | javax.microedition.khronos.egl.EGLContext | 使用 (javax.microedition.khronos.egl.*) 定义的 OpenGL 接口。 |
| eglContext14 | android.opengl.EGLContext | 使用 (android.opengl.*) 定义的 OpenGL 接口。 |



## TRTCVideoFrame

__功能__

视频帧信息。

__介绍__

TRTCVideoFrame 用来描述一帧视频画面的裸数据，它或者是一帧编码前的画面，或者是一帧解码后的画面。




__属性列表__

| 属性 | 类型 | 字段含义 | 推荐取值 |
|-----|-----|-----|-----|
| pixelFormat | int | 视频像素格式，定义参见 [视频像素格式](#TRTC_VIDEO_PIXEL_FORMAT)。 | 自定义采集：TRTC_VIDEO_PIXEL_FORMAT_Texture_2D 或 TRTC_VIDEO_PIXEL_FORMAT_NV21；自定义渲染：TRTC_VIDEO_PIXEL_FORMAT_I420。 |
| bufferType | int | 视频数据包装格式，定义参见  [视频数据包装格式](#TRTC_VIDEO_BUFFER_TYPE)。 | 自定义采集：TRTC_VIDEO_BUFFER_TYPE_TEXTURE；自定义渲染：TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER 或 TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY。 |
| texture | [TRTCTexture](https://intl.cloud.tencent.com/document/product/647/32266#trtctexture) | bufferType 为 TRTC_VIDEO_PIXEL_FORMAT_Texture_2D 时的视频数据。 | - |
| data | byte[] | bufferType 为 TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY 时的视频数据。 | - |
| buffer | ByteBuffer | bufferType 为 TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER 时的视频数据，主要在 native 层使用。 | - |
| width | int | 视频宽度。 | 请严格填写传入视频数据的宽度。 |
| height | int | 视频高度。 | 请严格填写传入视频数据的高度。 |
| timestamp | long | 视频帧的时间戳，单位毫秒。 | 自定义视频采集时可以填0，这样 SDK 会自定填充 timestamp 字段，但请“均匀”地控制 sendCustomVideoData 的调用间隔。 |
| rotation | int | 视频像素的顺时针旋转角度。 | 自定义视频采集时不需要填写。 |



## TRTCAudioFrame

__功能__

音频帧数据。




__属性列表__

| 属性 | 类型 | 字段含义 |
|-----|-----|-----|
| data | byte[] | 音频数据。 |
| sampleRate | int | 采样率。 |
| channel | int | 声道数。 |
| timestamp | long | 时间戳。 |



## TRTCVolumeInfo

__功能__

音量大小。

__介绍__

表示语音音量的评估大小，通过这个数值，您可以在 UI 界面上用图标表征 userId 是否有在说话。




__属性列表__

| 属性 | 类型 | 字段含义 |
|-----|-----|-----|
| userId | String | 说话者的 userId, 空则为自己。 |
| volume | int | 说话者的音量, 取值范围0 - 100。 |



## TRTCSpeedTestResult

__功能__

网络测速结果。

__介绍__

您可以在用户进入房间前通过 [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/32264#trtccloud) 的 startSpeedTest 接口进行测速 （注意：请不要在通话中调用）， 测速结果会每2 - 3秒钟返回一次，每次返回一个 IP 地址的测试结果。

__属性列表__

| 属性 | 类型 | 字段含义 |
|-----|-----|-----|
| ip | String | 服务器 IP 地址。 |
| quality | int | 网络质量，内部通过评估算法测算出的网络质量，loss 越低，rtt 越小，得分便越高。 |
| upLostRate | float | 上行丢包率，范围是0 - 1.0，例如，0.3表示每向服务器发送10个数据包可能会在中途丢失3个。 |
| downLostRate | float | 下行丢包率，范围是0 - 1.0，例如，0.2表示每从服务器收取10个数据包可能会在中途丢失2个。 |
| rtt | int | 延迟（毫秒），指当前设备到腾讯云服务器的一次网络往返时间，该值越小越好，正常数值范围是10ms - 100ms。 |



## TRTCMixUser

__功能__

云端混流中每一路子画面的位置信息。

__介绍__

TRTCMixUser 用于指定每一路（即每一个 userId）视频画面的具体摆放位置。




__属性列表__

| 属性 | 类型 | 字段含义 |
|-----|-----|-----|
| userId | String | 参与混流的 userId。 |
| roomId | String | 参与混流的 userId 所在roomId，null表示当前房间。 |
| x | int | 图层位置 x 坐标（绝对像素值）。 |
| y | int | 图层位置 y 坐标（绝对像素值）。 |
| width | int | 图层位置宽度（绝对像素值）。 |
| height | int | 图层位置高度（绝对像素值）。 |
| zOrder | int | 图层层次（1 - 15）不可重复。 |
| streamType | int | 参与混合的是主路画面（TRTC_VIDEO_STREAM_TYPE_BIG，默认）还是屏幕分享（TRTC_VIDEO_STREAM_TYPE_SUB）画面。 |
| pureAudio | boolean | 参与混合的是否纯音频流。 |




## TRTCTranscodingConfig

__功能__

云端混流（转码）配置。

__介绍__

包括最终编码质量和各路画面的摆放位置。




__属性列表__

| 属性 | 类型 | 字段含义 | 推荐取值 |
|-----|-----|-----|-----|
| appId | int | 腾讯云直播 AppID。 | 请在 [实时音视频控制台](https://console.cloud.tencent.com/rav) 选择已经创建的应用，单击【帐号信息】后，在“直播信息”中获取。 |
| bizId | int | 腾讯云直播 bizid。 | 请在 [实时音视频控制台](https://console.cloud.tencent.com/rav) 选择已经创建的应用，单击【帐号信息】后，在“直播信息”中获取。 |
| mode | int | 转码config模式。 | - |
| videoWidth | int | 最终转码后的视频分辨率的宽度（px）。 | - |
| videoHeight | int | 最终转码后的视频分辨率的高度（px）。 | - |
| videoBitrate | int | 最终转码后的视频分辨率的码率（kbps）。 | - |
| videoFramerate | int | 最终转码后的视频分辨率的帧率（FPS）。 | 15 |
| videoGOP | int | 最终转码后的视频分辨率的关键帧间隔（也称为 GOP），单位秒。 | 3 |
| audioSampleRate | int | 最终转码后的音频采样率。 | 48000 |
| audioBitrate | int | 最终转码后的音频码率，单位：kbps。 | 64 |
| audioChannels | int | 最终转码后的音频声道数。 | 2 |
| mixUsers | ArrayList[TRTCMixUser](https://intl.cloud.tencent.com/document/product/647/32266#trtcmixuser) | 每一路子画面的位置信息。 | - |



## TRTCPublishCDNParam

__功能__

旁路推流参数。




__属性列表__

| 属性 | 类型 | 字段含义 |
|-----|-----|-----|
| appId | int | 腾讯云 AppID，请在 [实时音视频控制台](https://console.cloud.tencent.com/rav) 选择已经创建的应用，单击【帐号信息】后，在“直播信息”中获取。 |
| bizId | int | 腾讯云直播 bizid，请在 [实时音视频控制台](https://console.cloud.tencent.com/rav) 选择已经创建的应用，单击【帐号信息】后，在“直播信息”中获取。 |
| url | String | 旁路转推的 URL。 |



## TRTCAudioRecordingParams

__功能__

录音参数。

__介绍__

请正确填写参数，确保录音文件顺利生成。




__属性列表__

| 属性 | 类型 | 字段含义 | 特别说明 |
|-----|-----|-----|-----|
| filePath | String | 文件路径（必填），录音的文件地址，由用户自行指定，请确保 App 里指定的目录存在且可写。 | 该路径需精确到文件名及格式后缀，格式后缀决定录制文件的格式，目前支持的格式有 PCM、WAV 和 AAC。 例如，指定路径为 path/to/audio.aac，则会生成一个 AAC 格式的文件。 请指定一个有读写权限的合法路径，否则录音文件无法生成。 |


## TRTCAudioEffectParam

__功能__

音效。


__属性列表__

| 属性 | 类型 | 字段含义 | 特别说明 |
|-----|-----|-----|-----|
| effectId | int | 音效 ID 每个音效均需要指定唯一的 ID。您可以通过此 ID 控制指定音效的开始、停止、音量等行为。 | - |
| path | String | 音效文件的绝对路径。 | - |
| loopCount | int | 音效循环播放的次数。 | 取值范围为0 - 任意正整数，默认值：0。0表示播放音效一次；1表示播放音效两次；以此类推。 |
| publish | boolean | 是否将音效传到远端。 | YES：音效在本地播放的同时，会上行至云端，因此远端用户也能听到该音效；NO：音效不会上行至云端，因此只能在本地听到该音效。默认值：NO。 |
| volume | int | 音效的音量大小。 | 取值范围为0 - 100；默认值：100。 |


## TRTCStatistics

__功能__

统计数据。




__属性列表__

| 属性 | 类型 | 字段含义 |
|-----|-----|-----|
| appCpu | int | 当前 App 的 CPU 使用率（％）。 |
| systemCpu | int | 当前系统的 CPU 使用率（％）。 |
| rtt | int | 延迟（毫秒）：代表 SDK 跟服务器一来一回之间所消耗的时间，这个值越小越好 一般低于50ms的 rtt 是比较理想的情况，而高于100ms的 rtt 会引入较大的通话延时 由于数据上下行共享一条网络连接，所以 local 和 remote 的 rtt 相同。 |
| upLoss | int | C -> S 上行丢包率（％）， 该值越小越好，例如，丢包率为0表示网络很好， 丢包率为30%则意味着 SDK 向服务器发送的数据包中会有30%丢失在上行传输中。 |
| downLoss | int | S -> C 下行丢包率（％）， 该值越小越好，例如，丢包率为0表示网络很好，丢包率为30%则意味着 SDK 向服务器发送的数据包中会有30%丢失在下行传输中。 |
| sendBytes | long | 发送字节总数，注意是字节数（bytes），不是比特数（bits）。 |
| receiveBytes | long | 接收字节总数，注意是字节数（bytes），不是比特数（bits）。 |
| localArray | ArrayList[TRTCLocalStatistics](https://intl.cloud.tencent.com/document/product/647/32266#trtclocalstatistics) | 自己本地的音视频统计信息，由于可能有大画面、小画面以及辅路画面等多路的情况，所以是一个数组。 |
| remoteArray | ArrayList[TRTCRemoteStatistics](https://intl.cloud.tencent.com/document/product/647/32266#trtcremotestatistics) | 远端成员的音视频统计信息，由于可能有大画面、小画面以及辅路画面等多路的情况，所以是一个数组。 |


## TRTCRemoteStatistics

__功能__

远端成员的音视频统计信息。




__属性列表__

| 属性 | 类型 | 字段含义 |
|-----|-----|-----|
| userId | String | 用户 ID，指定是哪个用户的视频流。 |
| finalLoss | int | 该线路的总丢包率（％），这个值越小越好，例如，丢包率为0表示网络很好。丢包率是该线路的 userId 从上行到服务器再到下行的总丢包率。如果 downLoss 为 0%, 但是 finalLoss 不为 0，说明该 userId 在上行就出现了无法恢复的丢包。 |
| width | int | 视频宽度。 |
| height | int | 视频高度。 |
| frameRate | int | 接收帧率（fps）。 |
| videoBitrate | int | 视频码率（Kbps）。 |
| audioSampleRate | int | 音频采样率（Hz）。 |
| audioBitrate | int | 音频码率（Kbps）。 |
| streamType | int | 流类型（大画面 &#124; 小画面 &#124; 辅路画面）。 |



## TRTCLocalStatistics

__功能__

自己本地的音视频统计信息。




__属性列表__

| 属性 | 类型 | 字段含义 |
|-----|-----|-----|
| width | int | 视频宽度。 |
| height | int | 视频高度。 |
| frameRate | int | 帧率（fps）。 |
| videoBitrate | int | 视频发送码率（Kbps）。 |
| audioSampleRate | int | 音频采样率（Hz）。 |
| audioBitrate | int | 音频发送码率（Kbps）。 |
| streamType | int | 流类型（大画面 &#124; 小画面 &#124; 辅路画面）。 |



