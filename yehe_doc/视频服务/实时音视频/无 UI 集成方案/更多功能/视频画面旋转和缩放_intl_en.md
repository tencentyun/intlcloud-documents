## Overview

Mobile live streaming uses mainly the portrait mode, but TRTC supports both the landscape and portrait modes, making it necessary to implement different page orientation logics. This document introduces you to the following:
- How to implement the portrait mode, for example, for video calls like those on WeChat
- How to implement the landscape mode, for example, for group communication applications such as Zoom
- How to customize settings for the rotation and rendering mode of the local image and remote images.

![](https://main.qcloudimg.com/raw/1b4452db22edfe88646cd35888794d44.jpg)

## Supported Platforms

| iOS | Android | macOS | Windows |Electron| Web|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003;  |  &#10003; |  &#10003; |  &#10003;  |&#10003;  |  × |


## Portrait Mode
To deliver an experience similar to that of WeChat video calls, you need to do two things.

[](id:step1)
### 1. Set the orientation of your app to portrait.
<dx-tabs>
::: iOS
Set the page orientation in Xcode > **General** > **Deployment Info** > **Device Orientation**.
![](https://main.qcloudimg.com/raw/f7d62ed0954fd44f80d3983a0e6fb52d.png)

Alternatively, use the `supportedInterfaceOrientationsForWindow` method in `Appdelegate`.

<dx-codeblock>
::: ObjectiveC ObjectiveC
- (UIInterfaceOrientationMask)application:(UIApplication *)application 
    supportedInterfaceOrientationsForWindow:(UIWindow *)window 
{

    return  UIInterfaceOrientationMaskPortrait ;

}
:::
</dx-codeblock>
>? This [CSDN article](https://blog.csdn.net/DreamcoffeeZS/article/details/79037207) offers a detailed guide on page orientation and adaptation on iOS for developers.
:::
::: Android
Set the `screenOrientation` attribute of the activity element to `portrait`:
<dx-codeblock>
::: xml 
<activity android:name=".trtc.TRTCMainActivity"  android:launchMode="singleTask" android:windowSoftInputMode="adjustPan"
          android:screenOrientation="portrait" />
:::
</dx-codeblock>
:::
</dx-tabs>

[](id:step2)
### 2. Set the orientation of the SDK to portrait.
When you use the `setVideoEncoderParam` API of `TRTCCloud` to set video encoding parameters, set `resMode` to `TRTCVideoResolutionModePortrait`.
Below is the sample code:[](id:example_code)
<dx-codeblock>
::: iOS ObjectiveC
TRTCVideoEncParam* encParam = [TRTCVideoEncParam new];
encParam.videoResolution = TRTCVideoResolution_640_360;
encParam.videoBitrate = 600;
encParam.videoFps = 15;
encParam.resMode = TRTCVideoResolutionModePortrait; // Set the resolution mode to portrait.

[trtc setVideoEncoderParam: encParam];
:::
::: Android java
TRTCCloudDef.TRTCVideoEncParam encParam = new TRTCCloudDef.TRTCVideoEncParam();
encParam.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_640_360;
encParam.videoBitrate = 600;
encParam.videoFps = 15;
encParam.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT; //Set the resolution mode to portrait.
trtc.setVideoEncoderParam(encParam);
:::
</dx-codeblock>

## Landscape Mode
The steps to implement the landscape mode for your app are similar to the steps of implementing the portrait mode, except that different values are used for the parameters in step 1 and step 2.
In particular, regarding the value of `resMode` in `TRTCVideoEncParam` in [step 2](#step2),
- on iOS, set it to `TRTCVideoResolutionModeLandscape`.
- on Android, set it to `TRTC_VIDEO_RESOLUTION_MODE_LANDSCAPE`.

## Custom Settings

The TRTC SDK provides different APIs for the setting of the rotation and rendering mode of the local image and remote images.

| API | Description | Remarks |
|---------|---------| ----- |
| setLocalViewRotation | Set the clockwise rotation of the local image preview | Rotate 90, 180, or 270 degrees clockwise |
| setLocalViewFillMode | Set the rendering mode of the local image preview | Crop the image or fill the blank space with black bars |
| setRemoteViewRotation | Set the clockwise rotation of remote video images | Rotate 90, 180, or 270 degrees clockwise |
| setRemoteViewFillMode | Set the rendering mode of remote video images | Crop the image or fill the blank space with black bars |
| setVideoEncoderRotation | Set the clockwise rotation of encoded images | Rotate 90, 180, or 270 degrees clockwise |

![](https://main.qcloudimg.com/raw/f965d6d603f95862d73525469637b437.jpg)


## GSensorMode
For adaptation during video recording and CDN live streaming, the TRTC SDK provides a simple gravity-sensing adaptation feature, which you can enable using the `setGSensorMode` API of `TRTCCloud`.

The feature supports adaptive rotation by 0, 90, 180, and 270 degrees. When a user's phone is turned, for example, 180 degrees, it ensures that the image seen by remote users remains the same. Because this feature is implemented through encoder-based rotation adjustment, adaptive rotation is also possible for recorded videos and videos played via HTML5 players.

>! Another way to achieve adaptive rotation is by embedding the gravity direction of a video in the information of each video frame, and adjusting the rotation at the player end according to the information. This scheme requires additional transcoding resources to orient recorded videos and is therefore not recommended.




