Tencent Cloud TRTC service supports a screen sharing feature in which the screen sharing image uses an independent single-channel audio/video stream and is viewed as a split screen with the camera’s image. It also supports audio-video synchronization. We generally call the channel with the camera image the “main channel (or primary image)” and the channel with the screen sharing the “auxiliary channel (**substream**)”. This document mainly describes how to use TRTC SDK to provide a screen sharing feature on the Windows platform.

## Supported Platforms

| iOS | Android | Mac OS | Windows | WeChat Mini Program | Chrome browser|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|     ✖  |    ✖    |    ✔   |    ✔    |    ✖     |   ✔     |

## Capturing the Sharing Target
You can make a list of sharable windows by using `getScreenCaptureSources`, with the list being returned through the output parameter sourceInfoList.
> The desktop screen in Windows is a window called the desktop window. When there are two screens, each screen has its corresponding desktop window. Therefore, the window list returned by getScreenCaptureSources will also contain the desktop window.

Each sourceInfo in the sourceInfoList can be a sharing target and is described using the following fields.

| Field | Type | Description|
|:-------:|:--------:| :---------------:|
| Type |TRTCScreenCaptureSourceType| Capture source type: specify type as window or screen|
| SourceId | HWND| Capture source ID: for a window, this field indicates window handle;<br>for a screen, this field indicates screen ID |
| SourceName| String | Window name, if screen then returns Screen0 Screen1... |
| ThumbWidth| Int32 | Window thumb width | 
| ThumbHeight| Int32 | Window thumb height |
| ThumbBGRA| Buffer | Window thumbnail binary buffer |
| IconWidth | Int32 | Window icon width |
| IconHeight| Int32 | Window icon height |
| IconBGRA | Buffer | Window icon binary buffer |

Based on this information, you can make a simple list page to list the sharable targets for users to choose from.

## Selecting sharing targets
TRTC SDK supports three sharing modes, which you can specify using `selectScreenCaptureTarget`.

- **Full screen sharing**:
This shares the entire screen window, and multi-screen split screen is supported. You will need to specify the source parameter of one type in the sourceInfoList as `TRTCScreenCaptureSourceTypeScreen` and set its captureRect as { 0, 0, 0, 0 }.

- **Specific region sharing**:
This shares a certain region of the screen. The user needs to define the coordinates of the region’s location. You will need to specify the source parameter of one type in the sourceInfoList as `TRTCScreenCaptureSourceTypeScreen` and set its captureRect as non-null, such as { 100, 100, 300, 300 }.

- **Specific window sharing**:
This shares the contents of a target window. The user needs to select which window is to be shared. You will need to specify the source parameter of one type in the sourceInfoList as `TRTCScreenCaptureSourceTypeWindow` and set its captureRect as { 0, 0, 0, 0 }.


> Two additional parameters:
> - The captureMouse parameter is used to specify whether or not to capture the cursor.
> - The highlight window parameter is used to specify whether or not to highlight the window being shared and to remind the user to remove the mask when the captured image is masked. This UI effect is achieved in SDK.


## Starting Screen Sharing

 - After selecting the sharing target, you can start screen sharing by using the `startScreenCapture` API.
 - In the sharing process, you can always switch the sharing target by calling `selectScreenCaptureTarget`.
 - The difference between `pauseScreenCapture` and `stopScreenCapture` is that pause will stop the capture of the screen contents and stay on the pause image displayed at the moment of pausing. Therefore, the remote end will see a still image of the last frame until it is resumed.
 
```C++
    /**
    * \brief 7.5 **Screen Sharing** Activate screen sharing
    * \param: rendHwnd - the HWND that identifies the preview window
    */
    void startScreenCapture(HWND rendHwnd);

    /**
    * \brief 7.6 **Screen Sharing** Pause screen sharing
    */
    void pauseScreenCapture();

    /**
    * \brief 7.7 **Screen Sharing** Resume screen sharing
    */
    void resumeScreenCapture();

    /**
    * \brief 7.8 **Screen Sharing** Close screen sharing
    */
    void stopScreenCapture();
```

## Setting Image Quality
You can set the screen sharing image quality by using the `setSubStreamEncoderParam` API, which includes resolution, bitrate, and frame rate. The following recommended parameters are provided for your convenience:

| Definition | Resolution | Frame Rate | Bitrate | 
|:-------------:|:---------:|:---------:| :---------: | 
| High | 1920 × 1080 | 10 | 800 Kbps |
| Standard | 1280 × 720 | 10 | 600 Kbps |
| Low | 1280 × 720 | 10 | 400 Kbps |

## Viewing Screen Sharing
When one user in a room starts screen sharing, the other users in the room will get the `onUserSubStreamAvailable` notification through TRTCCloudCallback.
The users who wish to view screen sharing can start rendering the remote user’s auxiliary image through `startRemoteSubStreamView`.

```C++
//Sample code: viewing screen sharing image
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
Currently, one TRTC room can only have one channel of screen sharing at a time.

 **When window sharing (SourceTypeWindow) is specified, will the resolution of the video stream change when the window size changes?**
It will not change because the window image will be proportionately scaled to the target resolution when the window size changes.




