## Introduction

In TRTCCloud, you can adjust the video quality in three ways:
- `TRTCAppScene` parameter in `enterRoom`: used to select your application scenario.
- setVideoEncoderParam: used to set the encoding parameter.
- setNetworkQosParam: used to set the network control policy.
This document describes how to configure these parameters to make the video quality of the TRTC SDK meet your project-specific needs.

## Supported Platforms

| iOS | Android | macOS | Windows | WeChat Mini Program | Web |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003; | &#10003;   | &#10003;  |  &#10003;   |   ×  | &#10003;  |

For detailed directions on how to set video quality for the web, please see [Configuration Guide](https://www.qcloudtrtc.com/trtc-web-sdk/docs/api/tutorial-04-advanced-set-video-profile.html).

## TRTCAppScene

- **VideoCall** 
This corresponds to the scenario where most of the time there are two or more people on video calls, and the optimization for internal encoders and network protocols focuses on smoothness to reduce call latency and lagging.

- **LIVE** 
This corresponds to the scenario where most of the time there is only one person speaking or performing and occasionally multiple people interact with one another through video, and the optimization for internal encoders and network protocols focuses on performance and compatibility to deliver better performance and definition.	


## TRTCVideoEncParam

### Recommended configuration

| Application Scenario | videoResolution |  videoFps | videoBitrate | 
|:-------------:|:-------------:|:-------------:|:-------------:|
| Video call (mobile) | 640x360 | 15 | 550 Kbps |
| Video conferencing (primary image on macOS or Windows) | 1280x720 | 15 | 1,200 Kbps | 
| Video conferencing (primary image on mobile device) | 640x360 | 15 | 900 Kbps|
| Video conferencing (small image) | 320x180 | 15 | 250 Kbps |
| Online education (teacher on macOS or Windows) | 960x540 | 15 | 850 Kbps |
| Online education (teacher on iPad) | 640x360 | 15 | 550 Kbps |
| Online education (student) | 320x180 | 15 | 250 Kbps |

### Detailed explanations of fields

- **(TRTCVideoResolution) videoResolution**
Encoded resolution; for example, 640x360 refers to the width (pixels) x height (pixels) of the encoded video image. In the `TRTCVideoResolution` enum definition, only landscape resolution (i.e., width >= height) is defined. If you want to use portrait resolution, you need to set `resMode` to `Portrait`.
 >!As many hardware codecs only support pixel widths that are divisible by 16, the actual resolution encoded by the SDK is not necessarily exactly the same as configured by the parameter; instead, it will be automatically corrected based on the divisor of 16; for example, the resolution 640x360 may be adapted to 640x368 inside the SDK.

- **(TRTCVideoResolutionMode) resMode**
This determines the landscape or portrait resolution. Because only landscape resolution is defined in `TRTCVideoResolution`, if you want to use portrait resolution such as 360x640, you need to specify `resMode` as `TRTCVideoResolutionModePortrait`. Generally, landscape resolution is used on PCs and Macs, while portrait resolution is used on mobile devices.

- **(int) videoFps**
  Frame rate (FPS), which indicates how many frames are encoded per second. The recommended value is 15 FPS, which can ensure that the video image is smooth enough without reducing the video definition due to too many frames per second.
	
 If you have high requirements for smoothness, you can set the frame rate to 20 or 25 FPS. However, please do not set a value above 25 FPS, because the normal frame rate of movies is only 24 FPS.

- **(int) videoBitrate**
Video bitrate, which indicates how many Kbits of encoded binary data is output by the encoder per second. If you set `videoBitrate` to 800 Kbps, the encoder will generate 800 Kbits of video data per second. If such data is stored as a file, the file size will be 800 Kbits, which is 100 KB or 0.1 MB.

 A higher video bitrate is not always better; instead, it must have a proper mapping relationship with resolution as shown in the table below.
 
### Resolution-Bitrate Reference Table

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

If the network bandwidth is sufficient, both high definition and smoothness can be ensured; however, if the user's network connection is not ideal, should priority be given to definition or smoothness? You can make a choice by specifying the `preference` parameter in `TRTCNetworkQosParam`. 

- **Smoothness preferred (TRTCVideoQosPreferenceSmooth)**
Smoothness is ensured on a weak network, while the video image will have a lot of blurs but can be smooth with no or slight lagging.

- **Definition preferred (TRTCVideoQosPreferenceClear)**
Definition is ensured on a weak network, i.e., the image will be as clear as possible but tend to lag.

### ControlMode

For the `controlMode` parameter, select **TRTCQosControlModeServer**. `TRTCQosControlModeClient` is used for internal debugging by the Tencent Cloud R&D team and should be ignored.

## Common Myths
**1. The higher the resolution, the better?**
Higher resolutions require higher bitrates for support. If the resolution is 1280x720, but the bit rate is specified as 200 Kbps, the video image will have a lot of blurs. You are recommended to set it as described in the **Resolution-Bitrate Reference Table**.

**2. The higher the frame rate, the better?**
Because the image captured by the camera is a complete mapping to all real objects in the exposure phase, it is not that the higher the frame rate, the smoother the video, which is different from the concept of FPS in games. On the contrary, if the frame rate is too high, the quality of each video frame will be lowered, and the exposure time of the camera will be reduced, worsening the image effect.

**3. The higher the bitrate, the better?**
Higher bitrates also require higher resolutions for a match. For a resolution of 320x240, a 1,000 Kbps bitrate would be wasteful. You are recommended to set it as described in the **Resolution-Bitrate Reference Table**.

**4. High resolution and bitrate can be set when connected to a Wi-Fi network?**
It is not that the Wi-Fi network speed is constant. If the device is far from the wireless router or the router channel is occupied, the Wi-Fi network may not be as fast as 4G.
In response to this issue, the TRTC SDK provides a speed test feature, which can perform speed test to determine the network quality based on the score before a video call is established.


