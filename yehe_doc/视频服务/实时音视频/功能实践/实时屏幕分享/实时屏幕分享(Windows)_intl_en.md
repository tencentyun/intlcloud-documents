TRTC supports screen sharing via the primary stream and substream on Windows:
- **Substream sharing**
In TRTC, you can share the screen via a dedicated stream, which is called the **substream**. In substream sharing, an anchor publishes camera video and screen sharing images at the same time. This is the scheme used by VooV Meeting. You can enable substream sharing by setting the `TRTCVideoStreamType` parameter to `TRTCVideoStreamTypeSub` when calling the `startScreenCapture` API. To play substream video, call `startRemoteSubStreamView`.

- **Primary stream sharing**
In TRTC, the channel via which camera images are published is the primary stream (**bigstream**). In primary stream sharing, an anchor publishes screen sharing images via the primary stream. As there is only one stream, an anchor cannot publish both camera video and screen sharing images. You can enable this mode by setting the `TRTCVideoStreamType` parameter to `TRTCVideoStreamTypeBig` when calling the `startScreenCapture` API.

## Supported Platforms

| iOS | Android | macOS | Windows | Electron| Chrome |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003;  |  &#10003;  |   &#10003; |   &#10003; | &#10003;  | &#10003; |

## APIs

| Description | C++ |  C# | Electron |
|---------|---------|---------|---------|
| Selects a sharing source | [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9d16af81b2ea2db7b91a8346add13393) | [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2aabe079ed38fb5122be988434a81a92) | [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) |
| Starts screen sharing | [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a984f461eebe77819f40c4129fc5a71bb) | [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e254) | [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) |
| Pauses screen sharing | [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a448e432a91c092f80421d377425fb1bb) | [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture) |
| Resumes screen sharing | [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad1fc32927622168e9b3cbb3f70043450) | [resumeScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeScreenCapture)|
| Ends screen sharing | [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad02093be5c603f66f356978169946a18) | [stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture) |


## Getting Sharable Sources
You can call `getScreenCaptureSources` to get a list of sharable sources, which is returned via the response parameter `sourceInfoList`.
>? On Windows, the desktop also counts as a window. When two monitors are used, each monitor corresponds to a desktop window. The list returned via `getScreenCaptureSources` includes desktop windows.

Each `sourceInfo` object in `sourceInfoList` represents a sharable source, which is described by the following parameters:

| Parameter | Type | Description|
|-------|--------| ---------------|
| type |TRTCScreenCaptureSourceType| Capturing source type, which may be window or screen|
| sourceId | HWND| Capturing source ID. <li>If a window is captured, the value of this parameter is the window handle.</li><li>If a screen is captured, the value of this parameter is the screen ID.</li> |
| sourceName| String | Window name. If a screen is captured, the value of this parameter is `Screen0`, `Screen1`, and so on. |
| thumbWidth| Int32 | Window thumbnail width |
| thumbHeight| Int32 | Window thumbnail height |
| thumbBGRA| Buffer | Window thumbnail binary buffer |
| iconWidth | Int32 | Window icon width |
| iconHeight| Int32 | Window icon height |
| iconBGRA | Buffer | Window icon binary buffer |

Based on the information, you can display a list of sharable sources on the UI for users to choose from.



## Selecting Sharing Source
The TRTC SDK supports three screen sharing modes, which you can specify using `selectScreenCaptureTarget`.

- **Share an entire screen**:
You can share an entire screen by selecting from `sourceInfoList` a source whose `type` is `TRTCScreenCaptureSourceTypeScreen` and setting `captureRect` to {0, 0, 0, 0}. This mode is supported when you split the screen onto multiple monitors.

- **Share a portion of a screen**:
You can share a specific portion of a screen by selecting from `sourceInfoList` a source whose `type` is `TRTCScreenCaptureSourceTypeScreen` and setting `captureRect` to a non-null value, such as {100, 100, 300, 300}.

- **Share a window**:
You can share a window by selecting from `sourceInfoList` a source whose `type` is `TRTCScreenCaptureSourceTypeWindow` and setting `captureRect` to {0, 0, 0, 0}.


>? Two additional parameters:
> - `captureMouse`: specifies whether to capture the cursor.
> - `highlightWindow`: specifies whether to highlight the window being shared and remind users to move the window when it is covered. The relevant UI design is implemented within the SDK.


## Starting Screen Sharing

 - After selecting a sharing source, you can call the `startScreenCapture` API to start screen sharing.
 - During screen sharing, you can call `selectScreenCaptureTarget` to change the sharing source.
 - The difference between `pauseScreenCapture` and `stopScreenCapture` is that the former pauses screen capturing and displays the image at the moment of pausing. Remote users see the last frame of video before pausing until screen capturing is resumed.

```C++
    /**
    * \brief 7.5 **Screen Sharing** Start screen sharing
    * \param: rendHwnd - HWND of the preview window
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
    * \brief 7.8 **Screen Sharing** Stop screen sharing
    */
    void stopScreenCapture();
```

## Setting Video Quality
You can use the `setSubStreamEncoderParam` API to set the video quality of screen sharing, including resolution, bitrate, and frame rate. We recommend the following settings:

| Clarity | Resolution | Frame Rate | Bitrate |
|:-------------:|:---------:|:---------:| :---------: |
| FHD | 1920 × 1080 | 10 | 800 Kbps |
|  HD | 1280 × 720 | 10 | 600 Kbps |
| SD | 960 × 720 | 10 | 400 Kbps |

## Watching Shared Screen
- **Watch screens shared by macOS/Windows users**
  When a macOS/Windows user in a room starts screen sharing, the screen will be shared through a substream, and other users in the room will be notified through [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) in `TRTCCloudDelegate`.
  Users who want to watch the shared screen can start rendering the substream image of the remote user by calling the [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) API.

- **Watch screens shared by Android/iOS users**
  When an Android/iOS user starts screen sharing, the screen will be shared through the primary stream, and other users in the room will be notified through [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) in `TRTCCloudDelegate`.
  Users who want to watch the shared screen can start rendering the primary stream of the remote user by calling the [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) API.

```C++
//Sample code: watch the shared screen
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
 **Can there be multiple channels of screen sharing streams in the same room at the same time?**
Currently, a TRTC room can have only one screen sharing stream at a time.

**When a specified window (`SourceTypeWindow`) is shared, if the window size changes, will the resolution of the video stream change accordingly?**
By default, the SDK automatically adjusts encoding parameters according to the size of the shared window.
If you want a fixed resolution, call the `setSubStreamEncoderParam` API to set encoding parameters for screen sharing or specify the parameters when calling the `startScreenCapture` API.