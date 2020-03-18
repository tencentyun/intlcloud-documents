## 1.1. Video Resolution

Here, only the landscape resolution is defined. If the portrait resolution (e.g., 360 * 640) needs to be used, `Portrait` must be selected for `TRTCVideoResolutionMode`.

| Constant | Description |
|-----|-----|
| TRTC_VIDEO_RESOLUTION_120_120 | \[C] 80 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_160_160 | \[C] 100 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_270_270 | \[C] 200 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_480_480 | \[C] 350 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_160_120 | \[C] 100 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_240_180 | \[C] 150 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_280_210 | \[C] 200 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_320_240 | \[C] 250 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_400_300 | \[C] 300 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_480_360 | \[C] 400 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_640_480 | \[C] 600 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_960_720 | \[C] 1,000 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_160_90 | \[C] 100 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_256_144 | \[C] 150 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_320_180 | \[C] 250 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_480_270 | \[C] 350 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_640_360 | \[C] 550 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_960_540 | \[C] 850 Kbps bitrate is recommended. |
| TRTC_VIDEO_RESOLUTION_1280_720 | \[C] 1,200 Kbps bitrate is recommended. |

## 1.2. Video Aspect Ratio Mode


- Landscape resolution: TRTCVideoResolution_640_360 + TRTCVideoResolutionModeLandscape = 640 * 360
- Portrait resolution: TRTCVideoResolution_640_360 + TRTCVideoResolutionModePortrait = 360 * 640



| Constant | Description |
|-----|-----|
| TRTC_VIDEO_RESOLUTION_MODE_LANDSCAPE | Landscape resolution. |
| TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT | Portrait resolution. |

## 1.3. Video Stream Type

TRTC provides three different audio/video streams, including:
- Primary image: the most used channel, which is generally used to transmit video data from the camera.
- Small image: it is similar to the primary image, but with lower resolution and bitrate.
- Secondary stream image: it is generally used for screen sharing and remote video playback (for example, a teacher plays back a video to students).

>?
>- If the upstream network and performance of the anchor is good, the primary (big) and small images can be sent at the same time.
>- The SDK does not support enabling only the small image, which must be enabled together with the primary image.



| Constant | Description |
|-----|-----|
| TRTC_VIDEO_STREAM_TYPE_BIG | Primary image video stream. |
| TRTC_VIDEO_STREAM_TYPE_SMALL | Small image video stream. |
| TRTC_VIDEO_STREAM_TYPE_SUB | Secondary stream (screen sharing). |

<span id="quality"></span>
## 1.4. Video (or Network) Quality Constant Definition

The TRTC SDK defines six levels of image quality, among which "Excellent" stands for the best quality, and "Down" indicates that the image quality is unavailable.

| Constant | Description |
|-----|-----|
| TRTC_QUALITY_UNKNOWN | Undefined. |
| TRTC_QUALITY_Excellent | Excellent. |
| TRTC_QUALITY_Good | Good. |
| TRTC_QUALITY_Poor | Poor. |
| TRTC_QUALITY_Bad | Bad. |
| TRTC_QUALITY_Vbad | Very bad. |
| TRTC_QUALITY_Down | Unavailable. |

## 1.5. Video Image Fill Mode

If video image's display resolution is different from its original resolution, the fill mode needs to be set as below:
- TRTCVideoFillMode_Fill: the entire screen will be covered by the image, where parts that exceed the screen will be cropped, so the displayed image may be incomplete.
- TRTCVideoFillMode_Fit: the long side of the image will fit the screen, while the short side will be proportionally scaled with unmatched areas being filled with black color blocks, but the displayed image is definitely complete.



| Constant | Description |
|-----|-----|
| TRTC_VIDEO_RENDER_MODE_FILL | The entire screen will be covered by the image, where parts that exceed the screen will be cropped. |
| TRTC_VIDEO_RENDER_MODE_FIT | The long side of the image will fit the screen, while the short side will be proportionally scaled with unmatched areas being filled with black color blocks. |

## 1.6. Video Image Rotation Direction

The TRTC SDK provides rotation angle setting APIs for local and remote images. The following rotation angles are all clockwise.

| Constant | Description |
|-----|-----|
| TRTC_VIDEO_ROTATION_0 | No rotation. |
| TRTC_VIDEO_ROTATION_90 | Rotates 90 degree clockwise. |
| TRTC_VIDEO_ROTATION_180 | Rotates 180 degree clockwise. |
| TRTC_VIDEO_ROTATION_270 | Rotates 270 degree clockwise. |

## 1.7. Beauty (Skin Smoothing) Filter Algorithm

The TRTC SDK has multiple in-built skin smoothing algorithms. You can select the one most suitable for your product needs.

| Constant | Description |
|-----|-----|
| TRTC_BEAUTY_STYLE_SMOOTH | Smooth, which is suitable for shows since it has more obvious effect. |
| TRTC_BEAUTY_STYLE_NATURE | Natural, which retains more facial details and seems more natural subjectively. |

<span id="TRTC_VIDEO_PIXEL_FORMAT"></span>
## 1.8. Video Pixel Format

The TRTC SDK provides custom capture and rendering features for video. In the custom capture feature, the following enumerated values can be used to describe the pixel format of the captured video. In the custom rendering feature, the video pixel format of the SDK callback can be specified.

| Constant | Description |
|-----|-----|
| TRTC_VIDEO_PIXEL_FORMAT_UNKNOWN | Unknown. |
| TRTC_VIDEO_PIXEL_FORMAT_I420 | YUV I420 |
| TRTC_VIDEO_PIXEL_FORMAT_Texture_2D | OpenGL 2D texture. |
| TRTC_VIDEO_PIXEL_FORMAT_TEXTURE_EXTERNAL_OES | - |
| TRTC_VIDEO_PIXEL_FORMAT_NV21 | - |

<span id="TRTC_VIDEO_MIRROR_TYPE"></span>
## 1.9. Mirror Type for Local Video Image Preview

The TRTC SDK provides a mirror setting feature for the local preview image. The default mirror type is `AUTO`.

| Constant | Description |
|-----|-----|
| TRTC_VIDEO_MIRROR_TYPE_AUTO | The SDK determines the mirror type: mirrors the front camera's image and does not mirror the rear camera's image. |
| TRTC_VIDEO_MIRROR_TYPE_ENABLE | Mirrors the images of both the front and rear cameras. |
| TRTC_VIDEO_MIRROR_TYPE_DISABLE | Does not mirror the images of both the front and rear cameras. |

<span id="TRTC_VIDEO_BUFFER_TYPE"></span>
## 1.10. Video Data Container Format

In custom capture and rendering features, you need to use the following enumerated values to specify the type of container that is used to contain the video data.

| Constant | Description |
|-----|-----|
| TRTC_VIDEO_BUFFER_TYPE_UNKNOWN | Unknown. |
| TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER | `DirectBuffer`, which carries buffers such as I420 and is used at the Native layer. |
| TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY | `byte[]`, which carries buffers such as I420 and is used at the Java layer. |
| TRTC_VIDEO_BUFFER_TYPE_TEXTURE | Direct operation texture ID, which has the best performance and least image quality loss. |

## 2.1. Application Scenarios

TRTC can be used in various application scenarios such as videoconferencing and live video broadcasting. The TRTC SDK provides different optimized configurations for different scenarios.
- VideoCall: video call, i.e., the scenario where most of the time there are two or more people on video calls, such as 1-to-1 online course, 1-to-N (N < 8) video conference, or a small class.
- LIVE: live video broadcasting (LVB), i.e., the scenario where most of the time there is only one person speaking or performing and occasionally multiple people interact with one another through video, such as co-anchoring in shows.



| Constant | Description |
|-----|-----|
| TRTC_APP_SCENE_VIDEOCALL | Video call scenario, where optimization for internal encoders and network protocols focuses on smoothness to reduce call latency and lagging. |
| TRTC_APP_SCENE_LIVE | LVB scenario, where optimization for internal encoders and network protocols focuses on performance and compatibility to deliver better performance and definition. |

## 2.2. Role for LVB Scenario Only (TRTCAppSceneLIVE)

In the LVB scenario, most users are viewers, and only several users are anchors. The differentiation in roles can help TRTC implement better and more specific optimization.
- Anchor: anchor, who can upstream video and audio. Up to 20 anchors are allowed to upstream videos at the same time in one room.
- Audience: viewer, who can only watch the video but cannot upstream video or audio. There is no upper limit for the number of viewers in one room.

| Constant | Description |
|-----|-----|
| TRTCRoleAnchor | Anchor. |
| TRTCRoleAudience | Viewer. |

## 2.3. Bandwidth Limit Mode

The TRTC SDK needs to adjust the internal codecs and network module based on the network conditions in real-time to respond to network changes. To support fast algorithm upgrade, the SDK provides two network bandwidth limit modes:
- ModeServer: on-cloud control, which is the default and recommended mode.
- ModeClient: client-based control, which is for internal debugging of SDK and shall not be used by users.


>?You are recommended to use on-cloud control, so that when the QoS algorithm is upgraded, you do not need to upgrade the SDK to get a better experience.



| Constant | Description |
|-----|-----|
| VIDEO_QOS_CONTROL_CLIENT | Client-based control (which is for internal debugging of SDK and shall not be used by users). |
| VIDEO_QOS_CONTROL_SERVER | On-cloud control (default). |

## 2.4. Image Quality Preference

This specifies whether to "ensure smoothness" or "ensure definition" when the TRTC SDK is used on a weak network:
- Smooth: smoothness is ensured on a weak network, i.e., ensuring the smoothness and sending of the audio, while the video image will have a lot of blurs but can be smooth with no lagging.
- Clear: definition is ensured on a weak network, i.e., the image will be as clear as possible but tend to lag.



| Constant | Description |
|-----|-----|
| TRTC_VIDEO_QOS_PREFERENCE_SMOOTH | Ensures smoothness on a weak network. |
| TRTC_VIDEO_QOS_PREFERENCE_CLEAR | Ensures definition on a weak network. |

## 3.1. Audio Sample Rate

The audio sample rate is used to measure the audio fidelity. A higher sample rate indicates higher fidelity. If there is music in the application scenario, `TRTCAudioSampleRate48000` will be recommended.

| Constant | Description |
|-----|-----|
| TRTCAudioSampleRate16000 | 16 kHz sample rate. |
| TRTCAudioSampleRate32000 | 32 kHz sample rate. |
| TRTCAudioSampleRate44100 | 44.1 kHz sample rate. |
| TRTCAudioSampleRate48000 | 48 kHz sample rate. |

<span id="TRTC_AUDIO_ROUTE"></span>
## 3.2. Audio Playback Mode (Audio Routing)

Both the video call features in WeChat and Mobile QQ have a hands-free mode during call. This mode is implemented based on audio routing. Generally, a mobile phone has two speakers, and the purpose of setting audio routing is to determine which speaker will be used:
- Speakerphone: speaker at the bottom of a phone, which has high volume and is suitable for playing back music.
- Earpiece: receiver at the top of a phone, which has low volume and is suitable for calls.



| Constant | Description |
|-----|-----|
| TRTC_AUDIO_ROUTE_SPEAKER | Speaker. |
| TRTC_AUDIO_ROUTE_EARPIECE | Receiver. |

## 3.3. Audio Reverb Mode
| Constant | Description |
|-----|-----|
| TRTC_REVERB_TYPE_0 | Disables reverb. |
| TRTC_REVERB_TYPE_1 | KTV |
| TRTC_REVERB_TYPE_2 | Small room. |
| TRTC_REVERB_TYPE_3 | Big hall. |
| TRTC_REVERB_TYPE_4 | Deep. |
| TRTC_REVERB_TYPE_5 | Resonant. |
| TRTC_REVERB_TYPE_6 | Metallic. |
| TRTC_REVERB_TYPE_7 | Husky. |

## 3.4. Voice Charger Type
| Constant | Description |
|-----|-----|
| TRTC_VOICE_CHANGER_TYPE_0 | Disables the voice changer. |
| TRTC_VOICE_CHANGER_TYPE_1 | Naughty boy. |
| TRTC_VOICE_CHANGER_TYPE_2 | Little girl. |
| TRTC_VOICE_CHANGER_TYPE_3 | Middle-aged man. |
| TRTC_VOICE_CHANGER_TYPE_4 | Heavy metal. |
| TRTC_VOICE_CHANGER_TYPE_5 | Being cold. |
| TRTC_VOICE_CHANGER_TYPE_6 | Non-native speaker. |
| TRTC_VOICE_CHANGER_TYPE_7 | Furious animal. |
| TRTC_VOICE_CHANGER_TYPE_8 | Chubby. |
| TRTC_VOICE_CHANGER_TYPE_9 | Strong electric current. |
| TRTC_VOICE_CHANGER_TYPE_10 | Robot. |
| TRTC_VOICE_CHANGER_TYPE_11 | Ethereal voice. |

## 3.5. Audio Frame Format
| Constant | Description |
|-----|-----|
| TRTC_AUDIO_FRAME_FORMAT_PCM | PCM |


<span id="TRTCSystemVolumeType"></span>
## 3.6. System Volume Type

Smartphones usually have two system volume types, i.e., call volume and media volume.
- Call volume: volume type dedicated to the VoIP scenario. It will forcibly enable acoustic echo cancellation (AEC) and has low sound quality, and its volume level cannot be set to 0.
- Media volume: volume type dedicated to music and movie playback through players. It will not enable AEC and can be set to 0 with the volume buttons on the phone. In media volume mode, AEC can be implemented by using the SDK's built-in acoustic algorithm if needed.

Currently, the SDK provides two control modes of system volume types, including:
- TRTCSystemVolumeTypeAuto: "call volume with mic and media volume without mic", i.e., the call volume mode will be used in a call, while the media volume mode will be used when a user only watches the video without speaking.
- TRTCSystemVolumeTypeMedia: the media volume will be used all the time. If a user is on a call, the SDK will use the built-in algorithm for AEC.


| Constant | Description |
|-----|-----|
| TRTCSystemVolumeTypeAuto | Default type, in which the SDK automatically selects the appropriate volume type. |
| TRTCSystemVolumeTypeMedia | Only the media volume is used, and the SDK does not use the call volume. |

## 4.1. UI Debugging Log
| Constant | Description |
|-----|-----|
| TRTC_DEBUG_VIEW_LEVEL_GONE | The UI does not display logs. |
| TRTC_DEBUG_VIEW_LEVEL_STATUS | The upper part of the UI displays the status logs. |
| TRTC_DEBUG_VIEW_LEVEL_ALL | The upper part of the UI displays the status logs, and the lower part displays the key events. |

## 4.2. Log Level

Different log levels indicate different levels of details and number of logs. It is recommended to set the log level to `TRTC_LOG_LEVEL_INFO` generally.

| Constant | Description |
|-----|-----|
| TRTC_LOG_LEVEL_VERBOSE | Outputs logs at all levels. |
| TRTC_LOG_LEVEL_DEBUG | Outputs logs at the DEBUG, INFO, WARNING, ERROR, and FATAL levels. |
| TRTC_LOG_LEVEL_INFO | Outputs logs at the INFO, WARNING, ERROR, and FATAL levels. |
| TRTC_LOG_LEVEL_WARN | Outputs logs at the WARNING, ERROR, and FATAL levels. |
| TRTC_LOG_LEVEL_ERROR | Outputs logs at the ERROR and FATAL levels. |
| TRTC_LOG_LEVEL_FATAL | Outputs logs at the FATAL level. |
| TRTC_LOG_LEVEL_NULL | No SDK logs will be output. |

## 4.3. G-sensor Switch

This configuration item applies to mobile devices such as phones and tablets, and needs to be used together with the current UI layout mode
- Disable: you can select this value if you do not want the video image direction to be adjusted along with the sensed gravity direction.
- UIAutoLayout: the SDK will not automatically adjust the rotation direction of `LocalVideoView`, which will be adjusted by the system instead. It can be used only if the application UI supports gravity sensing.
- UIFixLayout: the SDK will automatically adjust the rotation direction of `LocalVideoView` and can be used if the application UI currently does not support gravity sensing.



| Constant | Description |
|-----|-----|
| TRTC_GSENSOR_MODE_DISABLE | Disables the g-sensor. |
| TRTC_GSENSOR_MODE_UIAUTOLAYOUT | Enables the g-sensor, which can be used if the application UI supports gravity sensing. |
| TRTC_GSENSOR_MODE_UIFIXLAYOUT | Enables the g-sensor, which can be used if the application UI currently does not support gravity sensing. |

## 4.4. MixTranscoding Parameter Configuration Mode

Currently, only the manual configuration mode is supported, i.e., all parameters of `TRTC_TranscodingConfigMode_Manual` need to be set manually.

| Constant | Description |
|-----|-----|
| TRTC_TranscodingConfigMode_Unknown | Undefined. |
| TRTC_TranscodingConfigMode_Manual | Manual configuration of MixTranscoding parameters. All parameters of `TRTCTranscodingConfig` need to be specified. |


## TRTCParams

__Feature__

Room entry parameters.

__Overview__

As the room entry parameters in the TRTC SDK, only if these parameters are correctly set can the user successfully enter the audio/video room specified by `roomId`.




__Attribute list__

| Attribute | Type | Description | Recommended Value |
|-----|-----|-----|-----|
| sdkAppId | int | Application ID, which is required. Tencent Cloud generates bills based on `sdkAppId`. | - |
| userId | String | User ID, which is required. It is the `userId` of the local user and acts as the username. | - |
| userSig | String | User signature, which is required. It is the authentication signature corresponding to the current `userId` and acts as the login password. | - |
| roomId | int | Room number, which is required. After the room number is specified, users (`userIds`) in the same room can see one another and make video calls. | - |
| role | int | Role, which applies only to the LVB scenario (`TRTCAppSceneLIVE`) and does not take effect in the video call scenario. | Default value: anchor (`TRTCRoleAnchor`). |
| privateMapKey | String | Room signature, which is optional. If you want users with only specified `userIds` to enter a room (`roomId`), you need to use `privateMapKey` to restrict the permission. | - |
| businessInfo | String | Business data, which is optional. This field applies only to some uncommon advanced features. | - |




## TRTCVideoEncParam

__Feature__

Encoding parameters.

__Overview__

Parameters related to video encoder. These settings determine the quality of image viewed by remote users, which is also the image quality of recorded video files in the cloud.




__Attribute list__

| Attribute | Type | Description | Recommended Value | Remarks |
|-----|-----|-----|-----|-----|
| videoResolution | int | Video resolution. | - For video calls, it is recommended to select 360 * 640 or lower for resolution and `Portrait` for `resMode`. - For MLVB, it is recommended to select 540 * 960 for resolution and `Portrait` for `resMode`.<br><br>- For Window and macOS, it is recommended to select 640 * 360 or higher for resolution and `Landscape` for `resMode`. | Resolution set in `TRTCVideoResolution` is only in landscape mode by default, e.g., 640 * 360.<br> If resolution in portrait mode is required, please select `Portrait` for `resMode`; for example, 640 * 360 will become 360 * 640 in portrait mode. |
| videoResolutionMode | int | Resolution mode (landscape/portrait). | For MLVB, it is recommended to select `Portrait`. For Window and macOS, it is recommended to select `Landscape`. | If 640 * 360 resolution is selected for `videoResolution` and `Portrait` is selected for `resMode`, then the final output resolution after encoding will be 360 * 640. |
| videoFps | int | Video capture frame rate. | 15 or 20 fps. If the frame rate is lower than 5 fps, there will be obvious lagging; if lower than 10 fps but higher than 5 fps, there will be slight lagging; if higher than 20 fps, too many resources will be wasted (the frame rate of movies is generally 24 fps). | The front cameras on many Android phones do not support a capture frame rate higher than 15 fps. For some Android phones that focus too much on beautification features, the capture frame rate of the front cameras may be lower than 10 fps. |
| videoBitrate | int | Video upstreaming bitrate. | For more information on the recommended settings, please see the description in the definition of `TRTCVideoResolution` in the first half of this document. | If the bitrate is too low, the video will have a lot of blurs. |



## TRTCNetworkQosParam

__Feature__

Network bandwidth limit parameters.

__Overview__

The settings determine the bandwidth limit practices of the SDK in various network conditions (e.g., whether to "ensure definition" or "ensure smoothness" on a weak network).




__Attribute list__

| Attribute | Type | Description | Recommended Value | Remarks |
|-----|-----|-----|-----|-----|
| preference | int | Whether to select "ensure definition" or "ensure smoothness" on a weak network. | - | - Smoothness on weak network: on a weak network, the video image will have a lot of blurs but can be smooth with no lagging<br><br>- Definition on weak network: the image will be as clear as possible on a weak network but tend to have more lagging. |
| controlMode | int | Video resolution (on-cloud control - client-based control). | On-cloud control. | - Server mode (default): on-cloud control. If there are no special needs, please use this mode directly <br><br>- Client mode: client-based control, which is for internal debugging of the SDK and shall not be used by users. |



## TRTCQuality

__Feature__

Video (or network) quality.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | String | User ID. |
| quality | int | Network quality. For more information on the definition, please see [Video (or Network) Quality Constant Definition](#quality). |



## TRTCTexture

__Feature__

Video texture data, including texture ID and EGL environment.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| textureId | int | Video texture ID. |
| eglContext10 | javax.microedition.khronos.egl.EGLContext | OpenGL API defined by `(javax.microedition.khronos.egl.*)`. |
| eglContext14 | android.opengl.EGLContext | OpenGL API defined by `(android.opengl.*)`. |



## TRTCVideoFrame

__Feature__

Video frame information.

__Overview__

`TRTCVideoFrame` is used to describe the raw data of a frame of video image, which is either the image before frame encoding or after frame decoding.




__Attribute list__

| Attribute | Type | Description | Recommended Value |
|-----|-----|-----|-----|
| pixelFormat | int | Video pixel format. For more information on the definition, please see [Video Pixel Format](#TRTC_VIDEO_PIXEL_FORMAT). | Custom capture: TRTC_VIDEO_PIXEL_FORMAT_Texture_2D or TRTC_VIDEO_PIXEL_FORMAT_NV21; Custom rendering: TRTC_VIDEO_PIXEL_FORMAT_I420. |
| bufferType | int | Video data container format. For more information on the definition, please see [Video Data Container Format](#TRTC_VIDEO_BUFFER_TYPE). | Custom capture: TRTC_VIDEO_BUFFER_TYPE_TEXTURE; Custom rendering: TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER or TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY. |
| texture | [TRTCTexture](https://cloud.tencent.com/document/product/647/32266#trtctexture) | Video data when `bufferType` is `TRTC_VIDEO_PIXEL_FORMAT_Texture_2D`. | - |
| data | byte[] | Video data when `bufferType` is `TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY`. | - |
| buffer | ByteBuffer | Video data when `bufferType` is `TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER`, which is mainly used at the Native layer. | - |
| width | int | Video width. | Please strictly enter the width of the video data passed in. |
| height | int | Video height. | Please strictly enter the height of the video data passed in. |
| timestamp | long | Video frame timestamp in milliseconds. | This parameter can be set to 0 for custom video capture, and the SDK will automatically set the `timestamp` field. However, please "evenly" set the calling interval of `sendCustomVideoData`. |
| rotation | int | Clockwise rotation angle of video pixel. | This parameter can be left empty if custom video capture is enabled. |



## TRTCAudioFrame

__Feature__

Audio frame data.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| data | byte [] | Audio data. |
| sampleRate | int | Sample rate. |
| channel | int | Number of sound channels. |
| timestamp | long | Timestamp. |



## TRTCVolumeInfo

__Feature__

Volume level.

__Overview__

This indicates the audio volume level, based on which corresponding icons can be displayed on UI to indicate whether a `userId` is speaking.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | String | `userId` of the speaking user. An empty value indicates the local user. |
| volume | int | Volume level of the speaking user. Value range: 0–100. |



## TRTCSpeedTestResult

__Feature__

Network speed test result.

__Overview__

The `startSpeedTest` API of [TRTCCloud](https://cloud.tencent.com/document/product/647/32264#trtccloud) can be used to test the network speed before a user enters a room (this API cannot be called during a call). The speed test result will be returned once every 2–3 seconds, and the test result of one IP address will be returned each time.

__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| ip | String | Server IP address. |
| quality | int | Network quality, which is tested and calculated based on the internal evaluation algorithm. The smaller the loss and round-trip time (RTT), the higher the network quality score. |
| upLostRate | float | Upstreaming packet loss rate between 0 and 1.0. For example, 0.3 indicates that 3 data packets may be lost in every 10 packets sent to the server. |
| downLostRate | float | Downstreaming packet loss rate between 0 and 1.0. For example, 0.2 indicates that 2 data packets may be lost in every 10 packets received from the server. |
| rtt | int | Delay in milliseconds, which is the round-trip time between the current device and CVM instance. The smaller the value, the better. The normal value range is 10–100 ms. |



## TRTCMixUser

__Feature__

Position information of each channel of subimage in On-Cloud MixTranscoding.

__Overview__

`TRTCMixUser` is used to specify the detailed position of the video image of each channel (i.e., each `userId`).




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | String | `userId` that engages in mixing. |
| roomId | String | `roomId` of the `userId` that engages in mixing. The `null` value indicates the current room. |
| x | int | X coordinate of the layer position (absolute pixel value). |
| y | int | Y coordinate of the layer position (absolute pixel value). |
| width | int | Width of the layer position (absolute pixel value). |
| height | int | Height of the layer position (absolute pixel value). |
| zOrder | int | Layer number (1–15), which must be unique. |
| streamType | int | Whether the primary image (`TRTC_VIDEO_STREAM_TYPE_BIG`, which is default) or screen sharing image (`TRTC_VIDEO_STREAM_TYPE_SUB`) engages in mixing. |
| pureAudio | boolean | Whether the stream engages in mixing is pure audio stream. |




## TRTCTranscodingConfig

__Feature__

On-Cloud MixTranscoding configuration.

__Overview__

This contains the final encoding quality and the positions of images of each channel.




__Attribute list__

| Attribute | Type | Description | Recommended Value |
|-----|-----|-----|-----|
| appId | int | Tencent Cloud LVB application ID. | Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| bizId | int | Tencent Cloud LVB business ID. | Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| mode | int | Transcoding `config` mode. | - |
| videoWidth | int | Width of video resolution in px after being transcoded. | - |
| videoHeight | int | Height of video resolution in px after being transcoded. | - |
| videoBitrate | int | Bitrate of video resolution in Kbps after being transcoded. | - |
| videoFramerate | int | Frame rate of video resolution in FPS after being transcoded. | 15 |
| videoGOP | int | GOP interval of video resolution in seconds after being transcoded. | 3 |
| audioSampleRate | int | Audio sample rate after being transcoded. | 48000 |
| audioBitrate | int | Audio bitrate in Kbps after being transcoded. | 64 |
| audioChannels | int | Number of sound channels after being transcoded. | 2 |
| mixUsers | ArrayList[TRTCMixUser](https://cloud.tencent.com/document/product/647/32266#trtcmixuser) | Position information of each channel of subimage. | - |



## TRTCPublishCDNParam

__Feature__

Relayed push parameters.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| appId | int | Tencent Cloud application ID. Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| bizId | int | Tencent Cloud LVB business ID. Please select a created application in the [TRTC Console](https://console.cloud.tencent.com/rav), click **Account Info**, and get the ID in "LVB Info". |
| url | String | Relayed push URL. |



## TRTCAudioRecordingParams

__Feature__

Audio recording parameters.

__Overview__

Please set the parameters correctly to ensure that the audio recording file can be successfully generated.




__Attribute list__

| Attribute | Type | Description | Remarks |
|-----|-----|-----|-----|
| filePath | String |File path, which is the path to the audio recording file and is required. The path needs to be specified by the user and must exist in the application and be writable. | The file name and its extension need to be specified in the path, and the extension determines the format of the audio recording file. Currently supported formats are PCM, WAV, and AAC. For example, if the specified path is `path/to/audio.aac`, a file in AAC format will be generated. Please specify a valid path that is readable/writable; otherwise, the audio recording file cannot be generated. |


## TRTCAudioEffectParam

__Feature__

Audio effect.


__Attribute list__

| Attribute | Type | Description | Remarks |
|-----|-----|-----|-----|
| effectId | int | Audio effect ID. Each audio effect needs to be assigned with a unique ID, through which the audio effect can be manipulated, such as starting/stopping and adjusting volume level. | - |
| path | String | Absolute path to the audio effect file. | - |
| loopCount | int | Number of loop playback times of audio effect. | Value range: 0 or any positive integer. Default value: 0. 0 indicates that the audio effect will be played back once; 1 indicates that the audio effect will be played back twice; and so on. |
| publish | boolean | Whether to send audio effect to remote users. | YES: when the audio effect is played back locally, it will be upstreamed to the cloud and can be heard by remote users; NO: the audio effect will not be upstreamed to the cloud and can only be heard locally. Default value: NO. |
| volume | int | Volume level of audio effect. | Value range: 0–100. Default value: 100. |


## TRTCStatistics

__Feature__

Statistics.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| appCpu | int | CPU utilization of the current application in percent (%). |
| systemCpu | int | CPU utilization of the current system in percent (%). |
| rtt | int | Delay in milliseconds, which is the round-trip time between the SDK and server. The smaller the value, the better. Generally `rtt` lower than 50 ms is satisfactory, while `rtt` higher than 100 ms will result in long call latency. As data upstreaming and downstreaming share the same network connection, `rtt` is the same for the local user and remote user. |
| upLoss | int | Client-to-server upstream packet loss rate in percent (%). The smaller the value, the better. For example, if the packet loss rate is 0, it means the network conditions are good. If the value is 30%, it indicates that 30% of data packets sent to the server by the SDK were lost during upstreaming. |
| downLoss | int | Server-to-client downstream packet loss rate in percent (%). The smaller the value, the better. For example, if the packet loss rate is 0, it means the network conditions are good. If the value is 30%, it indicates that 30% of data packets sent to the server by the SDK were lost during downstreaming. |
| sendBytes | long | Total number of bytes sent. Note that this is the number of bytes but not bits. |
| receiveBytes | long | Total number of bytes received. Note that this is the number of bytes but not bits. |
| localArray | ArrayList[TRTCLocalStatistics](https://cloud.tencent.com/document/product/647/32266#trtclocalstatistics) | Local audio/video statistics, which are an array since they may contain statistics of multiple channels, such as big image, small image, and secondary channel image. |
| remoteArray | ArrayList[TRTCRemoteStatistics](https://cloud.tencent.com/document/product/647/32266#trtcremotestatistics) | Remote audio/video statistics, which are an array since they may contain statistics of multiple channels, such as big image, small image, and secondary channel image. |


## TRTCRemoteStatistics

__Feature__

Audio/video statistics of a remote user.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| userId | String | User ID, which specifies the user whose video stream is to be queried. |
| finalLoss | int | Total packet loss rate of this line in percent (%). A smaller value is preferred; for example, if the packet loss rate is 0, it means the network conditions are good. The packet loss rate is the total packet loss rate in one turn of upstreaming and downstreaming between the `userId` and server. If `downLoss` is 0% but `finalLoss` is not 0, it indicates that there was an irrecoverable packet loss in upstreaming from the `userId`. |
| width | int | Video width. |
| height | int | Video height. |
| frameRate | int | Receipt frame rate in fps. |
| videoBitrate | int | Video bitrate in Kbps. |
| audioSampleRate | int | Audio sample rate in Hz. |
| audioBitrate | int | Audio bitrate in Kbps. |
| streamType | int | Stream type (big image &#124; small image &#124; secondary channel image). |



## TRTCLocalStatistics

__Feature__

Local audio/video statistics.




__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| width | int | Video width. |
| height | int | Video height. |
| frameRate | int | Frame rate in fps. |
| videoBitrate | int | Video sending bitrate in Kbps. |
| audioSampleRate | int | Audio sample rate in Hz. |
| audioBitrate | int | Audio sending bitrate in Kbps. |
| streamType | int | Stream type (big image &#124; small image &#124; secondary channel image). |



