## Introduction

Different from the portrait mode of mobile live broadcasting, TRTC needs to consider both landscape and portrait modes; therefore, there will be a lot of landscape/portrait mode processing logic to deal with. This document describes:
- How to implement portrait mode; for example, WeChat video call is a typical example of portrait mode.
- How to implement landscape mode; for example, multi-person video conferencing applications (e.g., XYLink) often adopt landscape mode.
- How to customize the rotation direction and fill mode of local and remote video images.


## Platforms Supported

| iOS | Android | macOS | Windows | WeChat Mini Program | Chrome Browser |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|     ✔  |    ✔    |    ✔    |    ✔     |   ✖     |   ✖     |


## Portrait Mode
If you want to achieve a user experience similar to WeChat video call, you need to do two things:

**1. Configure the UI of the application to be in portrait mode**
For iOS, set directly in Xcode's **General** > **Deployment Info** > **Device Orientation**:
![](https://main.qcloudimg.com/raw/f7d62ed0954fd44f80d3983a0e6fb52d.png)

You can also achieve this by implementing the `supportedInterfaceOrientationsForWindow` method in `Appdelegate`:
``` ObjectiveC
- (UIInterfaceOrientationMask)application:(UIApplication *)application 
    supportedInterfaceOrientationsForWindow:(UIWindow *)window 
{

    return  UIInterfaceOrientationMaskPortrait ;

}
```

> For some development ideas about screen orientation on iOS, please see Landscape/Portrait Screen Rotation and Its Basic Adaptation Method on iOS on CSDN.

On the Android platform, you can configure the UI to be in portrait mode by specifying the `screenOrientation` attribute of the activity as `portrait`:
```xml
<activity android:name=".trtc.TRTCMainActivity"  android:launchMode="singleTask" android:windowSoftInputMode="adjustPan"
          android:screenOrientation="portrait" />
```

**2. Configure the SDK to use portrait resolution**
When using the `setVideoEncoderParam` API of TRTCCloud to set video encoding parameters, simply specify `resMode` as `TRTCVideoResolutionModePortrait`.

Taking iOS as an example, the sample code is as follows:
``` ObjectiveC
TRTCVideoEncParam* encParam = [TRTCVideoEncParam new];
encParam.videoResolution = TRTCVideoResolution_640_360;
encParam.videoBitrate = 600;
encParam.videoFps = 15;
encParam.resMode = TRTCVideoResolutionModePortrait; // Set the resolution mode to portrait mode

[trtc setVideoEncoderParam: encParam];
```

## Landscape Mode

If you want the application to be in landscape mode, then you need to do something similar to setting portrait mode and just modify the parameters in the first and second steps accordingly.

Specifically, in the second step, you need to specify `resMode` in `TRTCVideoEncParam` as `TRTCVideoResolutionModeLandscape` (for Android: `TRTC_VIDEO_RESOLUTION_MODE_LANDSCAPE`).

## Custom Controls

The TRTC SDK provides a lot of API functions to control the rotation direction and fill mode of local and remote video images:

| API Function | Purpose | Remarks |  
|---------|---------| ----- |
| setLocalViewRotation | Clockwise rotation angle of local preview image | Valid values: 90 degrees, 180 degrees, 270 degrees | 
| setLocalViewFillMode | Fill mode of local preview image | Valid values: crop, fill with black bars |
| setRemoteViewRotation | Clockwise rotation angle of remote video image | Valid values: 90 degrees, 180 degrees, 270 degrees |
| setRemoteViewFillMode | Fill mode of remote video image | Valid values: crop, fill with black bars |
| setVideoEncoderRotation | Clockwise rotation angle of the video image output by the encoder | Currently, only 180-degree rotation is supported, i.e., upside down |



## GSensorMode
Considering that screen rotation involves various adaptation factors of recording and CDN relayed live streaming, the TRTC SDK only provides a simple adaption feature based on gravity sensing, which can be enabled through the `setGSensorMode` API of TRTCCloud.

This feature currently only supports 180-degree upside-down adaptive rotation, that is, when the user's phone is turned upside down by 180 degrees, the screen orientation presented to the viewer will still remain the same (90-degree or 270-degree adaptive rotation is not supported yet). This adaptation is implemented based on the direction adjustment of the encoder, so the recorded video as well as the video image displayed in WeChat Mini Program and HTML5 webpage can also maintain the original orientation.

> ! Another implementation scheme of gravity sensing-based adaption is to carry the gravity direction of the current video in each video frame, and then adaptively adjust the rendering direction on the viewer's device. However, this scheme requires the introduction of additional transcoding resources in order to achieve the orientation of the recorded video as expected; therefore, it is not recommended.




