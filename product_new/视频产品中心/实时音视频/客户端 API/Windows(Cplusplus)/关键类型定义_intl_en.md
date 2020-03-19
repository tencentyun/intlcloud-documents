## TRTCParams

__Feature__

Room entry parameters.

__Overview__

Only if these parameters are correctly set can the user successfully call `enterRoom` to enter the audio/video room specified by `roomId`.




__Attribute list__

| Attribute | Type | Description | Recommended Value |
|-----|-----|-----|-----|
| sdkAppId | uint32_t | Application ID, which is required. Tencent Cloud generates bills based on `sdkAppId`. | The ID can be obtained on the account information page in the [TRTC Console](https://console.cloud.tencent.com/rav/) after the corresponding application is created. |
| userId | const char * | User ID in UTF-8 format, which is required. It is the `userId` of the local user and acts as the username. | If the ID of a user in your account system is "abc", `userId` can be set to "`abc`". |
| userSig | const char * | User signature, which is required. It is the authentication signature corresponding to the current `userId` and acts as the login password. | For more information on the calculation method, please see [How to Calculate `UserSig`](https://intl.cloud.tencent.com/document/product/647/35123/35166). |
| roomId | uint32_t | Room number, which is required. Users in the same room can see and make video calls to one another. | The parameter value can be customized but must be unique. If the user ID (`userId`) is numeric, the room creator's user ID can be directly used as the `roomId`. |
| role | [TRTCRoleType](https://intl.cloud.tencent.com/document/product/647/35134#trtcroletype) | Role, which applies only to the LVB scenario (`TRTCAppSceneLIVE`) and does not take effect in the video call scenario. | Default value: anchor (`TRTCRoleAnchor`). |
| privateMapKey | const char * | Room signature, which is optional. If you want only users with the specified `userIds` to enter a room, you need to use `privateMapKey` to restrict the permission. | You are recommended to use this parameter only if you have high security requirements. For more information, please see [Restricting Room Entry Permissions](https://intl.cloud.tencent.com/document/product/647/35123/32240). |
| businessInfo | const char * | Business data, which is optional. This field applies only to some advanced features. | This parameter is not recommended. |




## TRTCVideoEncParam

__Feature__

Video encoding parameters.

__Overview__

These settings determine the quality of image viewed by remote users, which is also the image quality of recorded video files in the cloud.




__Attribute list__

| Attribute | Type | Description | Recommended Value | Remarks |
|-----|-----|-----|-----|-----|
| videoResolution | [TRTCVideoResolution](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoresolution) | Video resolution. | - For video calls, it is recommended to select 360 * 640 or lower for resolution and `Portrait` for `resMode`. - For MLVB, it is recommended to select 540 * 960 for resolution and `Portrait` for `resMode`.<br><br>- For Window and macOS, it is recommended to select 640 * 360 or higher for resolution and `Landscape` for `resMode`. | Resolution set in `TRTCVideoResolution` is only in landscape mode by default, e.g., 640 * 360.<br> If resolution in portrait mode is required, please select `Portrait` for `resMode`; for example, 640 * 360 will become 360 * 640 in portrait mode. |
| resMode | [TRTCVideoResolutionMode](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoresolutionmode) | Resolution mode (landscape/portrait). | For MLVB, it is recommended to select `Portrait`. For Window and macOS, it is recommended to select `Landscape`. | If 640 * 360 resolution is selected for `videoResolution` and `Portrait` is selected for `resMode`, then the final output resolution after encoding will be 360 * 640. |
| videoFps | uint32_t | Video capture frame rate. | 15 or 20 fps. If the frame rate is lower than 5 fps, there will be obvious lagging; if lower than 10 fps but higher than 5 fps, there will be slight lagging; if higher than 20 fps, too many resources will be wasted (the frame rate of movies is generally 24 fps). | The front cameras on many Android phones do not support a capture frame rate higher than 15 fps. For some Android phones that focus too much on beautification features, the capture frame rate of the front cameras may be lower than 10 fps. |
| videoBitrate | uint32_t | Video upstreaming bitrate. | For more information on the recommended settings, please see the description in the definition of `TRTCVideoResolution` in the first half of this document. | If the bitrate is too low, the video will have a lot of blurs. |




## TRTCNetworkQosParam

__Feature__

Network bandwidth limit parameters.

__Overview__

Network bandwidth limit parameters. The settings determine the bandwidth limit practices of the SDK in various network conditions (e.g., whether to "ensure definition" or "ensure smoothness" on a weak network).




__Attribute list__

| Attribute | Type | Description | Recommended Value | Remarks |
|-----|-----|-----|-----|-----|
| preference | [TRTCVideoQosPreference](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoqospreference) | Whether to select "ensure definition" or "ensure smoothness" on a weak network. | - | - Smoothness on weak network: on a weak network, the video image will have a lot of blurs but can be smooth with no lagging. <br><br>- Definition on weak network: the image will be as clear as possible on a weak network but tend to have more lagging. |
| controlMode | [TRTCQosControlMode](https://intl.cloud.tencent.com/document/product/647/35134#trtcqoscontrolmode) | On-cloud control. | - Server mode (default): on-cloud control. If there are no special needs, please use this mode directly <br><br>- Client mode: client-based control, which is for internal debugging of the SDK and shall not be used by users. |




## TRTCQualityInfo

__Feature__

Video quality.

__Overview__

This indicates the video call quality, based on which corresponding icons can be displayed on UI to represent the line quality of a `userId`.


__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | const char * | User ID. |
| quality | [TRTCQuality](https://intl.cloud.tencent.com/document/product/647/35134#trtcquality) | Video quality. |




## TRTCVolumeInfo

__Feature__

Volume level.

__Overview__

This indicates the audio volume level, based on which corresponding icons can be displayed on UI to indicate whether a `userId` is speaking.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | const char * | `userId` of the speaking user, which is in UTF-8 format. |
| volume | uint32_t | Volume level of the speaking user. Value range: 0–100. |




## TRTCSpeedTestResult

__Feature__

Network speed test result.

__Overview__

The `startSpeedTest` API of `TRTCCloud` can be used to test the network speed before a user enters a room (this API cannot be called during a call). The speed test result will be returned once every 2–3 seconds, and the test result of one IP address will be returned each time.

__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| ip | const char * | Server IP address. |
| quality | [TRTCQuality](https://intl.cloud.tencent.com/document/product/647/35134#trtcquality) | Network quality, which is tested and calculated based on the internal evaluation algorithm. The smaller the loss and round-trip time (RTT), the higher the network quality score. |
| upLostRate | float | Upstreaming packet loss rate between 0 and 1.0. For example, 0.3 indicates that 3 data packets may be lost in every 10 packets sent to the server. |
| downLostRate | float | Downstreaming packet loss rate between 0 and 1.0. For example, 0.2 indicates that 2 data packets may be lost in every 10 packets received from the server. |
| rtt | int | Delay in milliseconds, which is the round-trip time between the current device and CVM instance. The smaller the value, the better. The normal value range is 10–100 ms. |




## TRTCMixUser

__Feature__

Position information of each channel of subimage in On-Cloud MixTranscoding.

__Overview__

[TRTCMixUser](https://intl.cloud.tencent.com/document/product/647/35134#trtcmixuser) is used to specify the detailed position of the video image of each channel (i.e., each `userId`).




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | const char * | `userId` that engages in mixing. |
| roomId | const char * | `roomId` that engages in mixing. If the stream is from another room, the actual `roomId` needs to be passed in; if the stream is from the current room, `roomId = NULL` needs to be passed in. |
| rect | RECT | Layer position coordinates and dimensions. The top-left corner is the origin (0,0) (absolute pixel value). |
| zOrder | int | Layer number (1–15), which must be unique. |
| pureAudio | bool | Whether it is pure audio. |
| streamType | [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideostreamtype) | Whether the primary image (`TRTCVideoStreamTypeBig`) or screen sharing image (`TRTCVideoStreamTypeSub`) engages in mixing. |




## TRTCTranscodingConfig

__Feature__

On-Cloud MixTranscoding configuration.

__Overview__

This contains the final encoding quality and the positions of images of each channel.




__Attribute list__

| Attribute | Type | Description | Recommended Value |
|-----|-----|-----|-----|
| mode | [TRTCTranscodingConfigMode](https://intl.cloud.tencent.com/document/product/647/35134#trtctranscodingconfigmode) | Transcoding `config` mode. | - |
| appId | uint32_t | Tencent Cloud LVB application ID. | Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| bizId | uint32_t | Tencent Cloud LVB business ID. | Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| videoWidth | uint32_t | Width of video resolution in px after being transcoded. | - |
| videoHeight | uint32_t | Height of video resolution in px after being transcoded. | - |
| videoBitrate | uint32_t | Bitrate of video resolution in Kbps after being transcoded. | - |
| videoFramerate | uint32_t | Frame rate of video resolution in FPS after being transcoded. | 15 |
| videoGOP | uint32_t | GOP interval of video resolution in seconds after being transcoded. | 3 |
| audioSampleRate | uint32_t | Audio sample rate after being transcoded. | 48000 |
| audioBitrate | uint32_t | Audio bitrate in Kbps after being transcoded. | 64 |
| audioChannels | uint32_t | Number of sound channels after being transcoded. | 2 |
| mixUsersArray | [TRTCMixUser](https://intl.cloud.tencent.com/document/product/647/35134#trtcmixuser) * | Position information of each channel of subimage. | - |
| mixUsersArraySize | uint32_t | Size of the `mixUsersArray` array. | - |




## TRTCPublishCDNParam

__Feature__

CDN relayed push parameters.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| appId | uint32_t | Tencent Cloud application ID. Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| bizId | uint32_t | Tencent Cloud LVB business ID. Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| url | const char * | Relayed push URL. |




## TRTCAudioRecordingParams

__Feature__

Audio recording parameters.

__Overview__

Please set the parameters correctly to ensure that the audio recording file can be successfully generated.




__Attribute list__

| Attribute | Type | Description | Remarks |
|-----|-----|-----|-----|
| filePath | const char * | File path, which is the storage path to the audio recording file and is required. The path needs to be specified by the user and must exist and be writable. | The file name and its extension need to be specified in the path, and the extension determines the format of the audio recording file. Currently supported formats are PCM, WAV, and AAC. For example, if the specified path is `path/to/audio.aac`, a file in AAC format will be generated. Please specify a valid path that is readable/writable; otherwise, the audio recording file cannot be generated. |




## TRTCAudioEffectParam

__Feature__

Audio effect.




__Attribute list__

| Attribute | Type | Description | Recommended Value |
|-----|-----|-----|-----|
| effectId | int | Audio effect ID. **Note:** the SDK allows playback of multiple audio effects, so audio effect IDs are needed for identification, through which the audio effects can be controlled, such as starting/stopping and adjusting volume level. | - |
| path | const char * | Path to audio effect. | - |
| loopCount | int | Number of loop playback times. | Value range: 0 or any positive integer. Default value: 0. 0 indicates that the audio effect will be played back once; 1 indicates that the audio effect will be played back twice; and so on. |
| publish | bool | Whether to upstream audio effect. | YES: when the audio effect is played back locally, it will be upstreamed to the cloud and can be heard by remote users; NO: the audio effect will not be upstreamed to the cloud and can only be heard locally. Default value: NO. |
| volume | int | Volume level of audio effect. | Value range: 0–100. Default value: 100. |




## TRTCLocalStatistics

__Feature__

Local audio/video statistics.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| width | uint32_t | Video width. |
| height | uint32_t | Video height. |
| frameRate | uint32_t | Frame rate in fps. |
| videoBitrate | uint32_t | Video sending bitrate in Kbps. |
| audioSampleRate | uint32_t | Audio sample rate in Hz. |
| audioBitrate | uint32_t | Audio sending bitrate in Kbps. |
| streamType | [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideostreamtype) | Stream type (big image &#124; small image &#124; secondary channel image). |



## TRTCRemoteStatistics

__Feature__

Audio/video statistics of a remote user.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | const char * | User ID, which specifies the user whose video stream is to be queried. |
| finalLoss | uint32_t | Total packet loss rate of this line in percent (%)<br>A smaller value is preferred; for example, if the packet loss rate is 0, it means the network conditions are good. The packet loss rate is the total packet loss rate in one turn of upstreaming and downstreaming between the `userId` and server. If `downLoss` is 0% but `finalLoss` is not 0, it indicates that there was an irrecoverable packet loss in upstreaming from the `userId`. |
| width | uint32_t | Video width. |
| height | uint32_t | Video height. |
| frameRate | uint32_t | Receipt frame rate in fps. |
| videoBitrate | uint32_t | Video bitrate in Kbps. |
| audioSampleRate | uint32_t | Audio sample rate in Hz. |
| audioBitrate | uint32_t | Audio bitrate in Kbps. |
| streamType | [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideostreamtype) | Stream type (big image &#124; small image &#124; secondary channel image). |



## TRTCStatistics

__Feature__

Statistics.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| upLoss | uint32_t | Client-to-server upstream packet loss rate in percent (%). The smaller the value, the better. For example, if the packet loss rate is 0, it means the network conditions are good. If the value is 30%, it indicates that 30% of data packets sent to the server by the SDK were lost during upstreaming. |
| downLoss | uint32_t | Server-to-client downstream packet loss rate in percent (%). The smaller the value, the better. For example, if the packet loss rate is 0, it means the network conditions are good. If the value is 30%, it indicates that 30% of data packets sent to the server by the SDK were lost during downstreaming. |
| appCpu | uint32_t | CPU utilization of the current application in percent (%). |
| systemCpu | uint32_t | CPU utilization of the current system in percent (%). |
| rtt | uint32_t | Delay in milliseconds, which is the round-trip time between the SDK and CVM instance. The smaller the value, the better. Generally `rtt` lower than 50 ms is satisfactory, while `rtt` higher than 100 ms will result in long call latency. As data upstreaming and downstreaming share the same network connection, `rtt` is the same for the local user and remote user. |
| receivedBytes | uint32_t | Total number of received bytes (including signals and audios/videos). |
| sentBytes | uint32_t | Total number of sent bytes (including signals and audios/videos). |
| localStatisticsArray | [TRTCLocalStatistics](https://intl.cloud.tencent.com/document/product/647/35134#trtclocalstatistics) * | Local audio/video statistics, which are an array since they may contain statistics of multiple channels, such as primary image, small image, and secondary channel image. |
| localStatisticsArraySize | uint32_t | Size of the `localStatisticsArray` array. |
| remoteStatisticsArray | [TRTCRemoteStatistics](https://intl.cloud.tencent.com/document/product/647/35134#trtcremotestatistics) * | Remote audio/video statistics, which are an array since they may contain statistics of multiple channels, such as primary image, small image, and secondary channel image. |
| remoteStatisticsArraySize | uint32_t | Size of the `remoteStatisticsArray` array. |



## TRTCVideoResolution

__Feature__

Video resolution.

__Overview__

Here, only the landscape resolution is defined. If the portrait resolution (e.g., 360 * 640) needs to be used, `Portrait` must be selected for `TRTCVideoResolutionMode`.

| Enumerated Value | Description |
|-----|-----|
| TRTCVideoResolution_120_120 | [C] 80 Kbps bitrate is recommended. |
| TRTCVideoResolution_160_160 | [C] 100 Kbps bitrate is recommended. |
| TRTCVideoResolution_270_270 | [C] 200 Kbps bitrate is recommended. |
| TRTCVideoResolution_480_480 | [C] 350 Kbps bitrate is recommended. |
| TRTCVideoResolution_160_120 | [C] 100 Kbps bitrate is recommended. |
| TRTCVideoResolution_240_180 | [C] 150 Kbps bitrate is recommended. |
| TRTCVideoResolution_280_210 | [C] 200 Kbps bitrate is recommended. |
| TRTCVideoResolution_320_240 | [C] 250 Kbps bitrate is recommended. |
| TRTCVideoResolution_400_300 | [C] 300 Kbps bitrate is recommended. |
| TRTCVideoResolution_480_360 | [C] 400 Kbps bitrate is recommended. |
| TRTCVideoResolution_640_480 | [C] 600 Kbps bitrate is recommended. |
| TRTCVideoResolution_960_720 | [C] 1,000 Kbps bitrate is recommended. |
| TRTCVideoResolution_160_90 | [C] 150 Kbps bitrate is recommended. |
| TRTCVideoResolution_256_144 | [C] 200 Kbps bitrate is recommended. |
| TRTCVideoResolution_320_180 | [C] 250 Kbps bitrate is recommended. |
| TRTCVideoResolution_480_270 | [C] 350 Kbps bitrate is recommended. |
| TRTCVideoResolution_640_360 | [C] 550 Kbps bitrate is recommended. |
| TRTCVideoResolution_960_540 | [C] 850 Kbps bitrate is recommended. |
| TRTCVideoResolution_1280_720 | [C] Camera capture - 1,200 Kbps bitrate is recommended [S] Screen sharing - recommended bitrate: LD: 400 Kbps; HD: 600 Kbps. |
| TRTCVideoResolution_1920_1080 | [S] Screen sharing - 800 Kbps bitrate is recommended. |


## TRTCVideoResolutionMode

__Feature__

Video resolution mode.

__Overview__

- Landscape resolution: TRTCVideoResolution_640_360 + TRTCVideoResolutionModeLandscape = 640 * 360
- Portrait resolution: TRTCVideoResolution_640_360 + TRTCVideoResolutionModePortrait = 360 * 640.

| Enumerated Value | Description |
|-----|-----|
| TRTCVideoResolutionModeLandscape | Landscape resolution. |
| TRTCVideoResolutionModePortrait | Portrait resolution. |


## TRTCVideoStreamType

__Feature__

Video stream type.

__Overview__

TRTC provides three different audio/video streams, including:
- Primary image: the most used channel, which is generally used to transmit video data from the camera.
- Small image: it is similar to the primary image, but with lower resolution and bitrate.
- Secondary stream image: it is generally used for screen sharing and remote video playback (for example, a teacher plays back a video to students).

>?
>- If the upstream network and performance of the anchor is good, the primary (big) and small images can be sent at the same time.
>- The SDK does not support enabling only the small image, which must be enabled together with the primary image.

| Enumerated Value | Description |
|-----|-----|
| TRTCVideoStreamTypeBig | Primary image video stream. |
| TRTCVideoStreamTypeSmall | Small image video stream. |
| TRTCVideoStreamTypeSub | Secondary stream (screen sharing). |


## TRTCQuality

__Feature__

Image quality.

__Overview__

The TRTC SDK defines six levels of image quality, among which "Excellent" stands for the best quality, and "Down" indicates that the image quality is unavailable.

| Enumerated Value | Description |
|-----|-----|
| TRTCQuality_Unknown | Undefined. |
| TRTCQuality_Excellent | Excellent. |
| TRTCQuality_Good | Good. |
| TRTCQuality_Poor | Poor. |
| TRTCQuality_Bad | Bad. |
| TRTCQuality_Vbad | Very bad. |
| TRTCQuality_Down | Unavailable. |


## TRTCVideoFillMode

__Feature__

Video image fill mode.

__Overview__

If video image's display resolution is different from its original resolution, the fill mode needs to be set as below:
- TRTCVideoFillMode_Fill: the entire screen will be covered by the image, where parts that exceed the screen will be cropped, and the displayed image may be incomplete.
- TRTCVideoFillMode_Fit: the long side of the image will fit the screen, while the short side will be proportionally scaled with unmatched areas being filled with black color blocks, but the displayed image is definitely complete.

| Enumerated Value | Description |
|-----|-----|
| TRTCVideoFillMode_Fill | The entire screen will be covered by the image, where parts that exceed the screen will be cropped. |
| TRTCVideoFillMode_Fit | The long side of the image will fit the screen, while the short side will be proportionally scaled with unmatched areas being filled with black color blocks. |


## TRTCBeautyStyle

__Feature__

Beauty (skin smoothing) filter algorithm.

__Overview__

The TRTC SDK has multiple in-built skin smoothing algorithms. You can select the one most suitable for your product needs.

| Enumerated Value | Description |
|-----|-----|
| TRTCBeautyStyleSmooth | Smooth, which is suitable for shows since it has more obvious effect. |
| TRTCBeautyStyleNature | Natural, which retains more facial details and seems more natural subjectively. |


## TRTCAppScene

__Feature__

Application scenario.

__Overview__

TRTC can be used in various application scenarios such as videoconferencing and live video broadcasting. The TRTC SDK provides different optimized configurations for different scenarios.
- VideoCall: video call, i.e., the scenario where most of the time there are two or more people on video calls, such as 1-to-1 online course, 1-to-N (N < 8) video conference, or a small class.
- LIVE: live video broadcasting (LVB), i.e., the scenario where most of the time there is only one person speaking or performing and occasionally multiple people interact with one another through video, such as co-anchoring in shows.

| Enumerated Value | Description |
|-----|-----|
| TRTCAppSceneVideoCall | Video call scenario, where optimization for internal encoders and network protocols focuses on smoothness to reduce call latency and lagging. |
| TRTCAppSceneLIVE | LVB scenario, where optimization for internal encoders and network protocols focuses on performance and compatibility to deliver better performance and definition. |


## TRTCRoleType

__Feature__

Role, which applies only to the LVB scenario (`TRTCAppSceneLIVE`).

__Overview__

In the LVB scenario, most users are viewers, and only several users are anchors. The differentiation in roles can help TRTC implement better and more specific optimization.

- Anchor: anchor, who can upstream video and audio. Up to 20 anchors are allowed to upstream videos at the same time in one room.
- Audience: viewer, who can only watch the video but cannot upstream video or audio. There is no upper limit for the number of viewers in one room.

| Enumerated Value | Description |
|-----|-----|
| TRTCRoleAnchor | Anchor. |
| TRTCRoleAudience | Viewer. |


## TRTCQosControlMode

__Feature__

Bandwidth limit mode.

__Overview__

The TRTC SDK needs to adjust the internal codecs and network module based on the network conditions in real-time to respond to network changes. To support fast algorithm upgrade, the SDK provides two network bandwidth limit modes:
- ModeServer: on-cloud control, which is the default and recommended mode.
- ModeClient: client-based control, which is for internal debugging of SDK and shall not be used by users.


>?You are recommended to use on-cloud control, so that when the QoS algorithm is upgraded, you do not need to upgrade the SDK to get a better experience.


| Enumerated Value | Description |
|-----|-----|
| TRTCQosControlModeClient | Client-based control (which is for internal debugging of SDK and shall not be used by users). |
| TRTCQosControlModeServer | On-cloud control (default). |


## TRTCVideoQosPreference

__Feature__

Image quality preference.

__Overview__

This specifies whether to "ensure smoothness" or "ensure definition" when the TRTC SDK is used on a weak network:

- Smooth: smoothness is ensured on a weak network, i.e., ensuring the smoothness and sending of the audio, while the video image will have a lot of blurs but can be smooth with no lagging.
- Clear: definition is ensured on a weak network, i.e., the image will be as clear as possible but tend to lag.


| Enumerated Value | Description |
|-----|-----|
| TRTCVideoQosPreferenceSmooth | Ensures smoothness on a weak network. |
| TRTCVideoQosPreferenceClear | Ensures definition on a weak network. |


## TRTCLogLevel

__Feature__

Log level.

| Enumerated Value | Description |
|-----|-----|
| TRTCLogLevelVerbose | Outputs logs at all levels. |
| TRTCLogLevelDebug | Outputs logs at the DEBUG, INFO, WARNING, ERROR, and FATAL levels. |
| TRTCLogLevelInfo | Outputs logs at the INFO, WARNING, ERROR, and FATAL levels. |
| TRTCLogLevelWarn | Outputs logs at the WARNING, ERROR, and FATAL levels. |
| TRTCLogLevelError | Outputs logs at the ERROR and FATAL levels. |
| TRTCLogLevelFatal | Outputs logs at the FATAL level. |
| TRTCLogLevelNone | No SDK logs will be output. |


## TRTCDeviceState

__Feature__

Device operation.

| Enumerated Value | Description |
|-----|-----|
| TRTCDeviceStateAdd | Adds a device. |
| TRTCDeviceStateRemove | Removes a device. |
| TRTCDeviceStateActive | The device has been enabled. |


## TRTCDeviceType

__Feature__

Device type.

| Enumerated Value | Description |
|-----|-----|
| TRTCDeviceTypeUnknow | - |
| TRTCDeviceTypeMic | Mic. |
| TRTCDeviceTypeSpeaker | Speaker. |
| TRTCDeviceTypeCamera | Camera. |


## TRTCWaterMarkSrcType

__Feature__

Watermark image source type.

| Enumerated Value | Description |
|-----|-----|
| TRTCWaterMarkSrcTypeFile | Path to the image file, which can be in BMP, GIF, JPEG, PNG, TIFF, Exif, WMF, or EMF format. |
| TRTCWaterMarkSrcTypeBGRA32 | Memory block in BGRA32 format. |
| TRTCWaterMarkSrcTypeRGBA32 | Memory block in RGBA32 format. |


## TRTCTranscodingConfigMode

__Feature__

MixTranscoding parameter configuration mode.

__Overview__

Currently, only the manual configuration mode is supported, i.e., all parameters of [TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35134#trtctranscodingconfig) need to be set manually.

| Enumerated Value | Description |
|-----|-----|
| TRTCTranscodingConfigMode_Unknown | Undefined. |
| TRTCTranscodingConfigMode_Manual | Manual configuration of MixTranscoding parameters. |


