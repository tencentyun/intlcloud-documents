This document describes how to set the image quality for a video call or live streaming session. You can set the properties according to your requirements for video quality and smoothness to deliver better user experience.
Video properties include resolution, frame rate, and bitrate.

## Overview
In the Electron SDK, you can adjust the image quality in the following ways:
- `TRTCAppScene` parameter in [enterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom): Used to select the scenario.
- [setVideoEncoderParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam): Used to set the encoding parameter.
- [setNetworkQosParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setNetworkQosParam): Used to specify the QoS control policy.

This document describes how to configure these parameters to make the video quality of the TRTC SDK meet your project-specific needs.
You can also refer to [Electron API Example: video-quality](https://github.com/tencentyun/TRTCSDK/blob/master/Electron/TRTC-API-Example/assets/code/advanced/video-quality/index.js).

## TRTCAppScene

- **VideoCall:** This scenario is most suitable when there are two or more people on a video call. The internal encoders and network protocols are optimized for video smoothness to reduce call latency and stuttering.
- **LIVE:** This scenario is most suitable when there is only one person speaking or performing for an online audience, and occasionally multiple people interact with one another through video. The internal encoders and network protocols are optimized for performance and compatibility to deliver better performance and video clarity.	


## TRTCVideoEncParam

### Recommended configuration

| Application Scenario | videoResolution |  videoFps | videoBitrate | 
|:-------------:|:-------------:|:-------------:|:-------------:|
| Video conferencing (primary image on macOS or Windows) | 1280 x 720 | 15 | 1,200 Kbps | 
| Online education (teacher on macOS or Windows) | 960 x 540 | 15 | 850 Kbps |

### Detailed description of fields

- **(TRTCVideoResolution) videoResolution**
Encoded resolution (for example, 640 x 360) refers to the width (pixels) x height (pixels) of the encoded video image. In the `TRTCVideoResolution` enum definition, only landscape resolution (i.e., width >= height) is defined. If you want to use portrait resolution, you need to set `resMode` to `Portrait`.
>! Because many hardware codecs only support pixel widths that are divisible by 16, the actual resolution encoded by the SDK may not be exactly the same as configured by the parameter; instead, it will be automatically corrected based on a multiple of 16. For example, the resolution 640 x 360 may be adapted to 640 x 368 inside the SDK.

- **(TRTCVideoResolutionMode) resMode**
Whether to use landscape or portrait resolutions. Because only landscape resolutions are defined in `TRTCVideoResolution`, if you want to a use portrait resolution such as 360 x 640, you need to specify `resMode` as `TRTCVideoResolutionModePortrait`. Generally, landscape resolutions are used on PCs and Macs, while portrait resolutions are used on mobile devices.

- **(int) videoFps**
  Frame rate (FPS), which indicates how many frames are encoded per second. The recommended value is 15 fps, which can ensure that the video image is smooth enough without reducing the video quality due to too many frames per second.
	
 If you have high requirements for smoothness, you can set the frame rate to 20 or 25 fps. However, do not set a value above 25 fps, because the normal frame rate of movies is only 24 fps.

- **(int) videoBitrate**
Video bitrate, which indicates how many Kbits of encoded binary data is output by the encoder per second. If you set `videoBitrate` to 800 Kbps, the encoder will generate 800 Kbits of video data per second. If the data is stored as a file, the file size will be 800 Kbits, which is 100 KB or 0.1 MB.

 A higher video bitrate is not always better; instead, it should be chosen appropriately based on the resolution as shown in the table below.
 
### Resolution-bitrate reference table

| Resolution Definition | Aspect Ratio | Recommended Bitrate | High-end Configuration |
|:-------------:|:-------------:|:-------------:|:-------------:|
| TRTCVideoResolution_120_120 | 1:1 |   80 Kbps | 120 Kbps|
| TRTCVideoResolution_160_160 | 1:1 | 100 Kbps | 150 Kbps|
| TRTCVideoResolution_270_270 | 1:1 | 200 Kbps | 300 Kbps|
| TRTCVideoResolution_480_480 | 1:1 | 350 Kbps | 525 Kbps|
| TRTCVideoResolution_160_120 | 4:3 | 100 Kbps | 150 Kbps|
| TRTCVideoResolution_240_180 | 4:3 | 150 Kbps | 225 Kbps|
| TRTCVideoResolution_280_210 | 4:3 | 200 Kbps | 300 Kbps|
| TRTCVideoResolution_320_240 | 4:3 | 250 Kbps | 375 Kbps|
| TRTCVideoResolution_400_300 | 4:3 | 300 Kbps | 450 Kbps|
| TRTCVideoResolution_480_360 | 4:3 | 400 Kbps | 600 Kbps|
| TRTCVideoResolution_640_480 | 4:3 | 600 Kbps | 900 Kbps|
| TRTCVideoResolution_960_720 | 4:3 | 1,000 Kbps | 1,500 Kbps|
| TRTCVideoResolution_160_90   | 16:9 | 150 Kbps | 250 Kbps|
| TRTCVideoResolution_256_144 | 16:9 | 200 Kbps | 300 Kbps|
| TRTCVideoResolution_320_180 | 16:9 | 250 Kbps | 400 Kbps|
| TRTCVideoResolution_480_270 | 16:9 | 350 Kbps | 550 Kbps|
| TRTCVideoResolution_640_360 | 16:9 | 550 Kbps | 900 Kbps|
| TRTCVideoResolution_960_540 | 16:9 | 850 Kbps | 1,300 Kbps|
| TRTCVideoResolution_1280_720 | 16:9 | 1,200 Kbps | 1,800 Kbps|

## TRTCNetworkQosParam
### QosPreference

If the network bandwidth is sufficient, both high definition and smoothness can be ensured. However, if the user's network connection is not ideal, you can choose whether to give priority to video quality or smoothness by specifying the `preference` parameter in `TRTCNetworkQosParam`. 

- **Smoothness preferred (TRTCVideoQosPreferenceSmooth)**
Smoothness is ensured on a weak network. The video image may be blurry, but it can be viewed smoothly with little or no stuttering.

- **Quality preferred (TRTCVideoQosPreferenceClear)**
Video quality is ensured on a weak network. The image will be as clear as possible but will tend to stutter.

### ControlMode

For the `controlMode` parameter, select **TRTCQosControlModeServer**. `TRTCQosControlModeClient` is used for internal debugging by the Tencent Cloud R&D team and should be ignored.

## Common Misconceptions
#### 1. Higher resolution is always better
A higher resolution also requires a higher bitrate. If the resolution is 1280 x 720, but the bitrate is specified as 200 Kbps, the video will be very blurry. We recommend you set parameters by referring to the [Resolution and Bitrate Reference Table](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolution).

#### 2. Higher frame rate is always better
Because the image captured by the camera is the result of physical light exposure, setting a higher frame rate does not always result in a smoother video. On the contrary, if the frame rate is too high, the quality of each video frame will be lowered because the exposure time is reduced.

#### 3. Higher bitrate is always better
A higher bitrate also requires a higher resolution. However, for a resolution of 320 x 240, a bitrate of 1000 Kbps is a waste. We recommend you set parameters by referring to the [Resolution and Bitrate Reference Table](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolution).

#### 4. High resolution and bitrate can always be set on a Wi-Fi network
Wi-Fi network speed is generally not constant. If the device is far from the wireless router or the router channel is occupied, the Wi-Fi network may not be as fast as 4G.
The TRTC SDK provides a speed test feature, which can perform speed testing before a video call to determine the network quality based on a score.

