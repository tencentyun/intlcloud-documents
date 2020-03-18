## TRTCParams

__Feature__

Room entry parameters.

__Overview__

Only if these parameters are correctly set can the user successfully call `enterRoom` to enter the audio/video room specified by `roomId`.




__Attribute list__

| Attribute | Type | Description | Recommended Value |
|-----|-----|-----|-----|
| sdkAppId | UInt32 | Application ID, which is required. Tencent Cloud generates bills based on `sdkAppId`. | The ID can be obtained on the account information page in the [TRTC Console](https://console.cloud.tencent.com/rav/) after the corresponding application is created. |
| userId | NSString * | User ID, which is required. It is the `userId` of the local user and acts as the login username. | If the ID of a user in your account system is "abc", `userId` can be set to "`abc`". |
| userSig | NSString * | User signature, which is required. It is the authentication signature corresponding to the current `userId` and acts as the login password. | For more information on the calculation method, please see [How to Calculate `UserSig`](https://intl.cloud.tencent.com/document/product/647/35166). |
| roomId | UInt32 | Room number, which is required. Users in the same room can see and make video calls to one another. | The parameter value can be customized but must be unique. If the user ID (`userId`) is numeric, the room creator's user ID can be directly used as the `roomId`. |
| role | [TRTCRoleType](#trtcroletype) | Role, which applies only to the LVB scenario (`TRTCAppSceneLIVE`) and does not take effect in the video call scenario. | Default value: anchor (`TRTCRoleAnchor`). |
| privateMapKey | NSString * | Room signature, which is optional. If you want only users with the specified `userIds` to enter a room, you need to use `privateMapKey` to restrict the permission. | You are recommended to use this parameter only if you have high security requirements. For more information, please see [Restricting Room Entry Permissions](https://cloud.tencent.com/document/product/647/32240). |
| bussInfo | NSString * | Business data, which is optional. This field applies only to some advanced features. | This parameter is not recommended. |



## TRTCVideoEncParam

__Feature__

Video encoding parameters.

__Overview__

These settings determine the quality of image viewed by remote users, which is also the image quality of recorded video files in the cloud.




__Attribute list__

| Attribute | Type | Description | Recommended Value | Remarks |
|-----|-----|-----|-----|-----|
| videoResolution | [TRTCVideoResolution](#trtcvideoresolution) | Video resolution. | - For video calls, it is recommended to select 360 * 640 or lower for resolution and `Portrait` for `resMode`.<br> <br>- For MLVB, it is recommended to select 540 * 960 for resolution and `Portrait` for `resMode`.<br><br>- For Window and macOS, it is recommended to select 640 * 360 or higher for resolution and `Landscape` for `resMode`. | Resolution set in `TRTCVideoResolution` is only in landscape mode by default, e.g., 640 * 360.<br> If resolution in portrait mode is required, please select `Portrait` for `resMode`; for example, 640 * 360 will become 360 * 640 in portrait mode. |
| resMode | [TRTCVideoResolutionMode](#trtcvideoresolutionmode) | Resolution mode (landscape/portrait). | For MLVB, it is recommended to select `Portrait`. For Window and macOS, it is recommended to select `Landscape`. | If 640 * 360 resolution is selected for `videoResolution` and `Portrait` is selected for `resMode`, then the final output resolution after encoding will be 360 * 640. |
| videoFps | int | Video capture frame rate. | 15 or 20 fps. If the frame rate is lower than 5 fps, there will be obvious lagging; if lower than 10 fps but higher than 5 fps, there will be slight lagging; if higher than 20 fps, too many resources will be wasted (the frame rate of movies is generally 24 fps). | The front cameras on many Android phones do not support a capture frame rate higher than 15 fps. For some Android phones that focus too much on beautification features, the capture frame rate of the front cameras may be lower than 10 fps. |
| videoBitrate | int | Video upstreaming bitrate. | For more information on the recommended settings, please see the description in the definition of [TRTCVideoResolution](#trtcvideoresolution). | If the bitrate is too low, the video will have a lot of blurs. |

## TRTCNetworkQosParam

__Feature__

Network bandwidth limit parameters.

__Overview__

Network bandwidth limit parameters. The settings determine the bandwidth limit practices of the SDK in various network conditions (e.g., whether to "ensure definition" or "ensure smoothness" on a weak network).

__Attribute list__

| Attribute | Type | Description | Recommended Value | Remarks |
|-----|-----|-----|-----|-----|
| preference | [TRTCVideoQosPreference](#trtcvideoqospreference) | Whether to select "ensure definition" or "ensure smoothness" on a weak network. | - | - Smoothness on weak network: on a weak network, the video image will have a lot of blurs but can be smooth with no lagging<br><br>- Definition on weak network: the image will be as clear as possible on a weak network but tend to have more lagging. |
| controlMode | [TRTCQosControlMode](#trtcqoscontrolmode) | Video resolution (on-cloud control - client-based control). | On-cloud control. | - Server mode (default): on-cloud control. If there are no special needs, please use this mode directly <br><br>- Client mode: client-based control, which is for internal debugging of the SDK and shall not be used by users. |



## TRTCQualityInfo

__Feature__

Video quality.

__Overview__

This indicates the video call quality, based on which corresponding icons can be displayed on UI to represent the line quality of a `userId`.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | NSString * | User ID. |
| quality | [TRTCQuality](#trtcquality) | Video quality. |



## TRTCVolumeInfo

__Feature__

Volume level.

__Overview__

This indicates the audio volume level, based on which corresponding icons can be displayed on UI to indicate whether a `userId` is speaking.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | NSString * | `userId` of the speaking user. `nil` indicates the local user. |
| volume | NSUInteger | Volume level of the speaking user. Value range: 0–100. |



## TRTCMediaDeviceInfo

__Feature__

Media device description.

__Overview__

On MacOS, there can be multiple devices of each type. The TRTC SDK for macOS provides a set of functions to manipulate these devices.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| type | [TRTCMediaDeviceType](#trtcmediadevicetype) | Device type. |
| deviceId | NSString * | Device ID. |
| deviceName | NSString * | Device name. |



## TRTCScreenCaptureSourceInfo

__Feature__

Screen sharing target information (only for MacOS).

__Overview__

If you want to add the screen sharing feature to your application, a window selection UI needs to be displayed first generally, so that the user can select the window to be shared. [TRTCScreenCaptureSourceInfo](#trtcscreencapturesourceinfo) is mainly used to define the window ID, type, name, and thumbnail.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| type | [TRTCScreenCaptureSourceType](#trtcscreencapturesourcetype) | Screen sharing type: a specified window or entire screen. |
| sourceId | NSString * | Window ID. |
| sourceName | NSString * | Window name. |
| extInfo | NSDictionary * | Window attribute. |
| thumbnail | NSImage * | Window thumbnail. |
| icon | NSImage * | Window icon. |



## TRTCSpeedTestResult

__Feature__

Network speed test result.

__Overview__

The `startSpeedTest` API of [TRTCCloud](https://cloud.tencent.com/document/product/647/32259#trtccloud) can be used to test the network speed before a user enters a room (this API cannot be called during a call). The speed test result will be returned once every 2–3 seconds, and the test result of one IP address will be returned each time.


__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| ip | NSString * | Server IP address. |
| quality | [TRTCQuality](#trtcquality) |Network quality, which is tested and calculated based on the internal evaluation algorithm. The smaller the loss and round-trip time (RTT), the higher the network quality score. |
| upLostRate | float | Upstreaming packet loss rate between 0 and 1.0. For example, 0.3 indicates that 3 data packets may be lost in every 10 packets sent to the server. |
| downLostRate | float | Downstreaming packet loss rate between 0 and 1.0. For example, 0.2 indicates that 2 data packets may be lost in every 10 packets received from the server. |
| rtt | uint32_t | Delay in milliseconds, which is the round-trip time between the current device and CVM instance. The smaller the value, the better. The normal value range is 10–100 ms. |



## TRTCVideoFrame

__Feature__

Video frame information.

__Overview__

[TRTCVideoFrame](#trtcvideoframe) is used to describe the raw data of a frame of video image, which can be the image before frame encoding or after frame decoding.

__Attribute list__

| Attribute | Type | Description | Recommended Value |
|-----|-----|-----|-----|
| pixelFormat | [TRTCVideoPixelFormat](#trtcvideopixelformat) | Video pixel format. | TRTCVideoPixelFormat_NV12 |
| bufferType | [TRTCVideoBufferType](#trtcvideobuffertype) | Video data structure type. | TRTCVideoBufferType_PixelBuffer |
| pixelBuffer | CVPixelBufferRef | Video data when `bufferType` is `TRTCVideoBufferType_PixelBuffer`. | - |
| data | NSData * | Video data when `bufferType` is `TRTCVideoBufferType_NSData`. | - |
| timestamp | uint64_t | Video frame timestamp in milliseconds. | This parameter can be set to 0 for custom video capture, and in this case, the SDK will automatically set the `timestamp` field. However, please "evenly" set the calling interval of `sendCustomVideoData`. |
| width | uint32_t | Video width. | This parameter can be left empty if custom video capture is enabled. |
| height | uint32_t | Video height. | This parameter can be left empty if custom video capture is enabled. |
| rotation | [TRTCVideoRotation](#trtcvideorotation) | Clockwise rotation angle of video pixels. | - |



## TRTCAudioFrame

__Feature__

Audio frame data.

__Overview__

Audio frame data.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| data | NSData * | Audio data. |
| sampleRate | [TRTCAudioSampleRate](#trtcaudiosamplerate) | Sample rate. |
| channels | int | Number of sound channels. |
| timestamp | uint64_t | Timestamp in milliseconds. |



## TRTCMixUser

__Feature__

Position information of each channel of subimage in On-Cloud MixTranscoding.

__Overview__

[TRTCMixUser](#trtcmixuser) is used to specify the detailed position of the video image of each channel (i.e., each `userId`).




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | NSString * | `userId` that engages in mixing. |
| roomID | NSString * | Room that engages in On-Cloud MixTranscoding. The `nil` value indicates the local room. |
| rect | CGRect | Layer position coordinates and dimensions. The top-left corner is the origin (0,0) (absolute pixel value). |
| zOrder | int | Layer number (1–15), which must be unique. |
| streamType | [TRTCVideoStreamType](#trtcvideostreamtype) | Whether the primary image (`TRTCVideoStreamTypeBig`) or screen sharing image (`TRTCVideoStreamTypeSub`) engages in mixing. |
| pureAudio | BOOL | Whether the pure audio mode is enabled. |



## TRTCTranscodingConfig

__Feature__

On-Cloud MixTranscoding configuration.

__Overview__

This contains the final encoding quality and the positions of images of each channel.

__Attribute list__

| Attribute | Type | Description | Recommended Value |
|-----|-----|-----|-----|
| mode | [TRTCTranscodingConfigMode](#trtctranscodingconfigmode) | Transcoding `config` mode. | - |
| appId | int | Tencent Cloud LVB application ID. | Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| bizId | int | Tencent Cloud LVB business ID. | Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| videoWidth | int | Width of video resolution in px after being transcoded. | - |
| videoHeight | int | Height of video resolution in px after being transcoded. | - |
| videoBitrate | int | Bitrate of video resolution in Kbps after being transcoded. | - |
| videoFramerate | int | Frame rate of video resolution in FPS after being transcoded. | 15 |
| videoGOP | int | GOP interval of video resolution in seconds after being transcoded. | 3 |
| audioSampleRate | int | Audio sample rate after being transcoded. | 48000 |
| audioBitrate | int | Audio bitrate in Kbps after being transcoded. | 64 |
| audioChannels | int | Number of sound channels after being transcoded. | 2 |
| mixUsers | NSArray< [TRTCMixUser](#trtcmixuser) * > * | Position information of each channel of subimage. | - |



## TRTCPublishCDNParam

__Feature__

CDN relayed push parameters.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| appId | int | Tencent Cloud application ID. Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| bizId | int | Tencent Cloud LVB business ID. Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| url | NSString * | Relayed push URL. |



## TRTCAudioRecordingParams

__Feature__

Audio recording parameters.

__Overview__

Please set the parameters correctly to ensure that the audio recording file can be successfully generated.


__Attribute list__

| Attribute | Type | Description | Remarks |
|-----|-----|-----|-----|
| filePath | NSString * | File path, which is the storage path to the audio recording file and is required. The path needs to be specified by the user and must exist and be writable. | The file name and its extension need to be specified in the path, and the extension determines the format of the audio recording file. Currently supported formats are PCM, WAV, and AAC. For example, if the specified path is `path/to/audio.aac`, a file in AAC format will be generated. Please specify a valid path that is readable/writable; otherwise, the audio recording file cannot be generated. |

## TRTCAudioEffectParam

__Feature__

Audio effect.

__Attribute list__

| Attribute | Type | Description | Recommended Value | Remarks |
|-----|-----|-----|-----|-----|
| effectId | int | Audio effect ID. | - | Each audio effect needs to be assigned with a unique ID, through which the audio effect can be manipulated, such as starting/stopping and adjusting volume level. |
| path | NSString * | Absolute path to the audio effect file. | - | - |
| loopCount | int | Number of loop playback times. | Value range: 0 or any positive integer. Default value: 0. 0 indicates that the audio effect will be played back once; 1 indicates that the audio effect will be played back twice; and so on. | - |
| publish | BOOL | Whether to send audio effect to remote users. | YES: when the audio effect is played back locally, it will be upstreamed to the cloud and can be heard by remote users; NO: the audio effect will not be upstreamed to the cloud and can only be heard locally. Default value: NO. | - |
| volume | int | Volume level of audio effect. | Value range: 0–100. Default value: 100. | - |


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
| streamType | [TRTCVideoStreamType](#trtcvideostreamtype) | Stream type (big image &#124; small image &#124; secondary channel image). |



## TRTCRemoteStatistics

__Feature__

Audio/video statistics of a remote user.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | NSString * | User ID, which specifies the user whose video stream is to be queried. |
| finalLoss | uint32_t | Total packet loss rate of this line in percent (%)<br>A smaller value is preferred; for example, if the packet loss rate is 0, it means the network conditions are good. The packet loss rate is the total packet loss rate in one turn of upstreaming and downstreaming between the `userId` and server. If `downLoss` is 0% but `finalLoss` is not 0, it indicates that there was an irrecoverable packet loss in upstreaming from the `userId`. |
| width | uint32_t | Video width. |
| height | uint32_t | Video height. |
| frameRate | uint32_t | Receipt frame rate in fps. |
| videoBitrate | uint32_t | Video bitrate in Kbps. |
| audioSampleRate | uint32_t | Audio sample rate in Hz. |
| audioBitrate | uint32_t | Audio bitrate in Kbps. |
| streamType | [TRTCVideoStreamType](#trtcvideostreamtype) | Stream type (big image &#124; small image &#124; secondary channel image). |



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
| receivedBytes | uint64_t | Total number of received bytes (including signals and audios/videos). |
| sentBytes | uint64_t | Total number of sent bytes (including signals and audios/videos). |
| localStatistics | NSArray< [TRTCLocalStatistics](#trtclocalstatistics) * > * | Local audio/video statistics, which are an array since they may contain statistics of multiple channels, such as big image, small image, and secondary channel image. |
| remoteStatistics | NSArray< [TRTCRemoteStatistics](#trtcremotestatistics) * > * | Remote audio/video statistics, which are an array since they may contain statistics of multiple channels, such as big image, small image, and secondary channel image. |



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
| TRTCVideoResolution_160_90 | [C] 100 Kbps bitrate is recommended. |
| TRTCVideoResolution_256_144 | [C] 150 Kbps bitrate is recommended. |
| TRTCVideoResolution_320_180 | [C] 250 Kbps bitrate is recommended. |
| TRTCVideoResolution_480_270 | [C] 350 Kbps bitrate is recommended. |
| TRTCVideoResolution_640_360 | [C] 550 Kbps bitrate is recommended. |
| TRTCVideoResolution_960_540 | [C] 850 Kbps bitrate is recommended. |
| TRTCVideoResolution_1280_720 | [C] Camera capture - 1,200 Kbps bitrate is recommended [S] Screen sharing - recommended bitrate: LD: 400 Kbps; HD: 600 Kbps. |
| TRTCVideoResolution_1920_1080 | [S] Screen sharing - 800 Kbps bitrate is recommended. |


## TRTCVideoResolutionMode

__Feature__

Video aspect ratio mode.

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
- TRTCVideoFillMode_Fit: the long side of the image will fit the screen, while the short side will be proportionally scaled with unmatched areas being filled with black color blocks. The displayed image is complete.



| Enumerated Value | Description |
|-----|-----|
| TRTCVideoFillMode_Fill | The entire screen will be covered by the image, where parts that exceed the screen will be cropped. |
| TRTCVideoFillMode_Fit | The long side of the image will fit the screen, while the short side will be proportionally scaled with unmatched areas being filled with black color blocks. |


## TRTCVideoRotation

__Feature__

Video image rotation direction.

__Overview__

The TRTC SDK provides rotation angle setting APIs for local and remote images. The following rotation angles are all clockwise.

| Enumerated Value | Description |
|-----|-----|
| TRTCVideoRotation_0 | No rotation. |
| TRTCVideoRotation_90 | Rotates 90 degree clockwise. |
| TRTCVideoRotation_180 | Rotates 180 degree clockwise. |
| TRTCVideoRotation_270 | Rotates 270 degree clockwise. |


## TRTCBeautyStyle

__Feature__

Beauty (skin smoothing) filter algorithm.

__Overview__

The TRTC SDK has multiple in-built skin smoothing algorithms. You can select the one most suitable for your product needs.

| Enumerated Value | Description |
|-----|-----|
| TRTCBeautyStyleSmooth | Smooth, which is suitable for shows since it has more obvious effect. |
| TRTCBeautyStyleNature | Natural, which retains more facial details and seems more natural subjectively. |


## TRTCVideoPixelFormat

__Feature__

Video pixel format.

__Overview__

The TRTC SDK provides custom capture and rendering features for video. In the custom capture feature, the following enumerated values can be used to describe the pixel format of the captured video. In the custom rendering feature, the video pixel format of the SDK callback can be specified.

| Enumerated Value | Description |
|-----|-----|
| TRTCVideoPixelFormat_Unknown | Unknown. |
| TRTCVideoPixelFormat_I420 | YUV420p I420. |
| TRTCVideoPixelFormat_NV12 | YUV420sp NV12. |
| TRTCVideoPixelFormat_32BGRA | BGRA8888. |


## TRTCVideoBufferType

__Feature__

Video data container format.

__Overview__

In custom capture and rendering features, you need to use the following enumerated values to specify the type of container that is used to contain the video data.
- PixelBuffer: it is most efficient when used directly. The iOS system provides various APIs to get or process `PixelBuffer`.
- NSData: it applies only to custom rendering. The SDK performs memory copy from `PixelBuffer` to `NSData`, which has certain performance loss. 



| Enumerated Value | Description |
|-----|-----|
| TRTCVideoBufferType_Unknown | Unknown. |
| TRTCVideoBufferType_PixelBuffer | It is most efficient when used directly. The iOS system provides various APIs to get or process `PixelBuffer`.|
| TRTCVideoBufferType_NSData | It applies only to custom rendering. The SDK performs memory copy from `PixelBuffer` to `NSData`, which has certain performance loss. |


## TRTCLocalVideoMirrorType

__Feature__

Mirror type of local video preview.

__Overview__

The local image supports the following mirror types for iOS:

| Enumerated Value | Description |
|-----|-----|
| TRTCLocalVideoMirrorType_Auto | Mirrors the front camera's image and does not mirror the rear camera's image. |
| TRTCLocalVideoMirrorType_Enable | Mirrors images of both the front and rear cameras. |
| TRTCLocalVideoMirrorType_Disable | Does not mirror the images of both the front and rear cameras. |


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

>?You are recommended to use on-cloud control, so that when upgrading the QoS algorithm, you do not need to upgrade the SDK to get a better experience.


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


## TRTCAudioSampleRate

__Feature__

Audio sample rate.

__Overview__

The audio sample rate is used to measure the audio fidelity. A higher sample rate indicates higher fidelity. If there is music in the application scenario, `TRTCAudioSampleRate48000` will be recommended.

| Enumerated Value | Description |
|-----|-----|
| TRTCAudioSampleRate16000 | 16 kHz sample rate. |
| TRTCAudioSampleRate32000 | 32 kHz sample rate. |
| TRTCAudioSampleRate44100 | 44.1 kHz sample rate. |
| TRTCAudioSampleRate48000 | 48 kHz sample rate. |


## TRTCAudioRoute

__Feature__

Audio playback mode (audio routing).

__Overview__
The hands-free mode of video call features in WeChat and Mobile QQ is implemented based on audio routing. Generally, a mobile phone has two speakers, one is the receiver at the top with low volume, and the other is the stereo speaker at the bottom with high volume. The purpose of setting audio routing is to determine which speaker will be used.
- Speakerphone: speaker at the bottom of a phone, which has high volume and is suitable for playing back music.
- Earpiece: receiver at the top of a phone, which has low volume and is suitable for calls. 



| Enumerated Value | Description |
|-----|-----|
| TRTCAudioModeSpeakerphone | Speaker. |
| TRTCAudioModeEarpiece | Receiver. |


## TRTCReverbType

__Feature__

Audio reverb mode.

__Overview__

This enumerated value applies to reverb mode in the LVB scenario and is mainly used in LVB shows.

| Enumerated Value | Description |
|-----|-----|
| TRTCReverbType_0 | Disables reverb. |
| TRTCReverbType_1 | KTV |
| TRTCReverbType_2 | Small room. |
| TRTCReverbType_3 | Big hall. |
| TRTCReverbType_4 | Deep. |
| TRTCReverbType_5 | Resonant. |
| TRTCReverbType_6 | Metallic. |
| TRTCReverbType_7 | Husky. |


## TRTCVoiceChangerType

__Feature__

Voice changer mode.

__Overview__

This enumerated value applies to voice changer mode in the LVB scenario and is mainly used in LVB shows.

| Enumerated Value | Description |
|-----|-----|
| TRTCVoiceChangerType_0 | Disables the voice changer. |
| TRTCVoiceChangerType_1 | Naughty boy. |
| TRTCVoiceChangerType_2 | Little girl. |
| TRTCVoiceChangerType_3 | Middle-aged man. |
| TRTCVoiceChangerType_4 | Heavy metal. |
| TRTCVoiceChangerType_5 | Being cold. |
| TRTCVoiceChangerType_6 | Non-native speaker. |
| TRTCVoiceChangerType_7 | Furious animal. |
| TRTCVoiceChangerType_8 | Chubby. |
| TRTCVoiceChangerType_9 | Strong electric current. |
| TRTCVoiceChangerType_10 | Robot. |
| TRTCVoiceChangerType_11 | Ethereal voice. |

## TRTCSystemVolumeType

__Feature__

System volume type.

__Overview__

Smartphones usually have two system volume types, i.e., call volume and media volume.
- Call volume: volume type dedicated to the VoIP scenario. It will forcibly enable acoustic echo cancellation (AEC) and has low sound quality, and its volume level cannot be set to 0.
- Media volume: volume type dedicated to music and movie playback through players. It will not enable AEC and can be set to 0 with the volume buttons on the phone. In media volume mode, AEC can be implemented by using the SDK's built-in acoustic algorithm if needed.

Currently, the SDK provides two control modes of system volume types, including:
- TRTCSystemVolumeTypeAuto: "call volume with mic and media volume without mic", i.e., the call volume mode will be used in a call, while the media volume mode will be used when a user only watches the video without speaking.
- TRTCSystemVolumeTypeMedia: the media volume will be used all the time. If a user is on a call, the SDK will use the built-in algorithm for AEC. 

>?Considering the increment in the installation package size, only the SDKs in the TRTC Enterprise and Professional editions contain the acoustic algorithm library. **If `TRTCSystemVolumeTypeMedia` is selected in the TRTC Lite edition, echo issues will occur, so please do so with caution.**


| Enumerated Value | Description |
|-----|-----|
| TRTCSystemVolumeTypeAuto | Default type, in which the SDK automatically selects the appropriate volume type. |
| TRTCSystemVolumeTypeMedia | Only the media volume is used, and the SDK does not use the call volume. |


## TRTCLogLevel

__Feature__

Log level.

__Overview__

Different log levels indicate different levels of details and number of logs. It is recommended to set the log level to `TRTCLogLevelInfo` generally.

| Enumerated Value | Description |
|-----|-----|
| TRTCLogLevelVerbose | Outputs logs at all levels. |
| TRTCLogLevelDebug | Outputs logs at the DEBUG, INFO, WARNING, ERROR, and FATAL levels. |
| TRTCLogLevelInfo | Outputs logs at the INFO, WARNING, ERROR, and FATAL levels. |
| TRTCLogLevelWarn | Outputs logs at the WARNING, ERROR, and FATAL levels. |
| TRTCLogLevelError | Outputs logs at the ERROR and FATAL levels. |
| TRTCLogLevelFatal | Outputs logs at the FATAL level. |
| TRTCLogLevelNone | No SDK logs will be output. |


## TRTCGSensorMode

__Feature__

Switch of the g-sensor.

__Overview__

This configuration item applies only to mobile devices such as iPhones and iPads, and needs to be used together with the current UI layout mode.
- Disable: this value indicates that the video image direction will not be adjusted along with the sensed gravity direction.
- UIAutoLayout: this value indicates that the SDK will not automatically adjust the rotation direction of `LocalVideoView`, which will be adjusted by the system instead. It can be used if the application UI supports gravity sensing.
- UIFixLayout: this value indicates that the SDK will automatically adjust the rotation direction of `LocalVideoView` and can be used if the application UI currently does not support gravity sensing.



| Enumerated Value | Description |
|-----|-----|
| TRTCGSensorMode_Disable | Disables the g-sensor. |
| TRTCGSensorMode_UIAutoLayout | Enables the g-sensor, which can be used if the application UI supports gravity sensing. |
| TRTCGSensorMode_UIFixLayout | Enables the g-sensor, which can be used if the application UI currently does not support gravity sensing. |


## TRTCMediaDeviceType

__Feature__

Device type (only for macOS).

__Overview__

On MacOS, there can be multiple devices of each type. The TRTC SDK for macOS provides a set of functions to manipulate these devices.

| Enumerated Value | Description |
|-----|-----|
| TRTCMediaDeviceTypeUnknown | Undefined. |
| TRTCMediaDeviceTypeAudioInput | Mic. |
| TRTCMediaDeviceTypeAudioOutput | Speaker or receiver. |
| TRTCMediaDeviceTypeVideoCamera | Camera. |
| TRTCMediaDeviceTypeVideoWindow | Window (for screen sharing). |
| TRTCMediaDeviceTypeVideoScreen | Entire screen (for screen sharing). |


## TRTCScreenCaptureSourceType

__Feature__

Screen sharing target type (only for macOS).

__Overview__

This enumerated value is mainly used for the SDK to distinguish between screen sharing targets (a window or the entire screen).

| Enumerated Value | Description |
|-----|-----|
| TRTCScreenCaptureSourceTypeUnknown | Undefined. |
| TRTCScreenCaptureSourceTypeWindow | The screen sharing target is a macOS window. |
| TRTCScreenCaptureSourceTypeScreen | The screen sharing target is the entire desktop of macOS. |


## TRTCTranscodingConfigMode

__Feature__

MixTranscoding parameter configuration mode.

__Overview__

Currently, only the manual configuration mode is supported, i.e., all parameters of [TRTCTranscodingConfig](#trtctranscodingconfig) need to be set manually.

| Enumerated Value | Description |
|-----|-----|
| TRTCTranscodingConfigMode_Unknown | Undefined. |
| TRTCTranscodingConfigMode_Manual | Manual configuration of MixTranscoding parameters. |


