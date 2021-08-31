Tencent Cloud TRTC supports screen sharing where the screen sharing image uses an independent channel of audio/video stream in parallel to the camera image. It also supports audio/video sync. Generally, the channel of the camera image is called the "primary channel (or primary image)", and the channel of screen sharing is called the "secondary channel (**substream**)". This document describes how to use the screen sharing feature of the TRTC SDK for Windows.

## Supported Platforms

| iOS | Android | macOS | Windows | Electron | WeChat Mini Program | Chrome Browser |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003;  |  &#10003;  |   &#10003; |   &#10003; | &#10003;  | ×    |  &#10003; |

## Getting Sharing Target
You can enumerate the list of sharable windows by using `getScreenCaptureSources`, and the list will be returned through the output parameter `sourceInfoList`.
> The desktop screen in Windows is also a window called the desktop window. When there are two displays, each display has its own desktop window. Therefore, the window list returned by `getScreenCaptureSources` will also include the desktop windows.

Each `sourceInfo` in `sourceInfoList` can be a sharing target and is described by the following fields:

| Field | Type | Description |
|:-------:|:--------:| :---------------:|
| type |TRTCScreenCaptureSourceType| Capture source type, which can be specified as window or screen |
| sourceId | HWND| Capture source ID. <br>For a window, this field indicates a window handle; <br>for a screen, this field indicates a screen ID |
| sourceName| string | Window name. For screens, Screen0, Screen1, and so on will be returned |
| thumbWidth| int32 | Window thumbnail width | 
| thumbHeight| int32 | Window thumbnail height |
| thumbBGRA| buffer | Window thumbnail binary buffer |
| iconWidth | int32 | Window icon width |
| iconHeight| int32 | Window icon height |
| iconBGRA | buffer | Window icon binary buffer |

Based on the information above, you can implement a simple list page to list the sharable targets for users to choose from.

## Selecting Sharing Target
TRTC SDK supports three sharing modes, which can be specified with `selectScreenCaptureTarget`.

- **Full screen sharing**:
This shares the entire screen and supports multi-display screen splitting. Specifically, you need to specify a `source` parameter of `TRTCScreenCaptureSourceTypeScreen` type in `sourceInfoList` and set `captureRect` to { 0, 0, 0, 0 }.

- **Specified area sharing**:
This shares a certain area of the screen, and you need to define the coordinates of the area. Specifically, you need to specify a `source` parameter of `TRTCScreenCaptureSourceTypeScreen` type in `sourceInfoList` and set `captureRect` to a non-null value, such as { 100, 100, 300, 300 }.

- **Specified window sharing**:
This shares a specified target window, and you need to select the window to be shared. Specifically, you need to specify a `source` parameter of `TRTCScreenCaptureSourceTypeWindow` type in `sourceInfoList` and set `captureRect` to { 0, 0, 0, 0 }.


> Two additional parameters:
> - The `captureMouse` parameter is used to specify whether to capture the cursor.
> - The `highlightWindow` parameter is used to specify whether to highlight the currently shared window and whether to highlight a covered window to remind the user to move the covering window away. This UI effect is implemented internally by the SDK.


## Starting Screen Sharing

 - After selecting the sharing target, you can start screen sharing by using the `startScreenCapture` API.
 - During the sharing process, you can change the sharing target by calling `selectScreenCaptureTarget`.
 - The difference between `pauseScreenCapture` and `stopScreenCapture` is that the former will stop the capture of the screen content and display the image captured at the moment of pausing. Therefore, remote users will see a still image of the last frame until the sharing is resumed.
 
```C++
    /**
    * \brief 7.5 **Screen Sharing**   Start screen sharing
    * \param: rendHwnd - the HWND that sustains the preview image
    */
    void startScreenCapture(HWND rendHwnd);

    /**
    * \brief 7.6 **Screen Sharing**   Pause screen sharing
    */
    void pauseScreenCapture();

    /**
    * \brief 7.7 **Screen Sharing**   Resume screen sharing
    */
    void resumeScreenCapture();

    /**
    * \brief 7.8 **Screen Sharing**   Close screen sharing
    */
    void stopScreenCapture();
```

## Setting Image Quality
You can set the screen sharing image quality by using the `setSubStreamEncoderParam` API, which includes resolution, bitrate, and frame rate. The following recommended values are provided for your reference:

| Definition | Resolution | Frame Rate | Bitrate | 
|:-------------:|:---------:|:---------:| :---------: | 
| HD+ | 1920x1080 | 10 | 800 Kbps |
| HD | 1280x720 | 10 | 600 Kbps |
| SD | 960x720 | 10 | 400 Kbps |

## Viewing Shared Screen
When a user in a room starts screen sharing, other users in the room will get a notification through `onUserSubStreamAvailable` in `TRTCCloudCallback`.
Users who want to view the shared screen can start rendering the secondary stream image of the remote user through `startRemoteSubStreamView`.

```C++
// Sample code: viewing screen sharing image
void CTRTCCloudSDK::onUserSubStreamAvailable(const char * userId, bool available)
{
	    LINFO(L"onUserSubStreamAvailable userId[%s] available[%d]\n", UTF82Wide(userId).c_str(), available);
	   if (available)  {
	         startRemoteSubStreamView(userId, hWnd);
	   } else {
	         stopRemoteSubStreamView(userId);
	   }
}
```

## FAQs
 **Can there be more than one channel of screen sharing in the same room at the same time?**
Currently, there can be only one channel of screen sharing in a TRTC room.

 **When window sharing (SourceTypeWindow) is specified, will the resolution of the video stream change as the window size changes?**
By default, the SDK will automatically adjust the encoding parameter according to the shared window size.
If you want a fixed resolution, you need to call the `setSubStreamEncoderParam` API to set the encoding parameter for screen sharing or specify the corresponding encoding parameter when calling `startScreenCapture`.




