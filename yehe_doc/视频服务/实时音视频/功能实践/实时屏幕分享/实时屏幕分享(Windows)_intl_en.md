TRTC supports screen sharing in primary stream and substream modes on Windows:
- **Substream sharing**
In TRTC, we can separately open one video upstream for screen sharing and call it "**substream**". Substream sharing means that the anchor can upstream both the camera image and the screen at the same time. This is the usage scheme of VooV Meeting. You can enable this mode by specifying the `TRTCVideoStreamType` parameter as `TRTCVideoStreamTypeSub` when calling the `startScreenCapture` API. The dedicated `startRemoteSubStreamView` API is needed to watch this channel of video image.

- **Primary stream sharing**
In TRTC, we generally call the channel of the camera image "**primary stream (aka bigstream)**", and primary stream sharing is to share the screen through the camera channel. In this mode, the anchor has only one video upstream, which can be either the camera image or the screen, and the two are mutually exclusive. You can enable this mode by specifying the `TRTCVideoStreamType` parameter as `TRTCVideoStreamTypeBig` when calling the `startScreenCapture` API.

## Supported Platforms

| iOS | Android | macOS | Windows | Electron | WeChat Mini Program | Chrome Browser |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003;  |  &#10003;  |   &#10003; |   &#10003; | &#10003;  | ×    |  &#10003; |

## Dependent APIs

| API Feature | C++ Edition |  C# Edition | Electron Edition | 
|---------|---------|---------|---------|
| Selects sharing target | [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa5c3c7ed12993c155de77fb43ba0cf3b) | [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a2aabe079ed38fb5122be988434a81a92) | [selectScreenCaptureTarget](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#selectScreenCaptureTarget) |
| Starts screen sharing | [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af83efff2a1020580bcb0bb89a8ffe4b0) | [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e254) | [startScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startScreenCapture) |
| Pauses screen sharing | [pauseScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | [pauseScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a448e432a91c092f80421d377425fb1bb) | [pauseScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pauseScreenCapture) |
| Resumes screen sharing | [resumeScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | [resumeScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#ad1fc32927622168e9b3cbb3f70043450) | [resumeScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumeScreenCapture)|
| Ends screen sharing | [stopScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | [stopScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#ad02093be5c603f66f356978169946a18) | [stopScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopScreenCapture) |


## Getting Sharing Target
You can enumerate the list of sharable windows by using `getScreenCaptureSources`, and the list will be returned through the output parameter `sourceInfoList`.
>? The desktop screen in Windows is also a window called the desktop window. When there are two displays, each display has its own desktop window. Therefore, the window list returned by `getScreenCaptureSources` will also include the desktop windows.

Each `sourceInfo` in `sourceInfoList` can be a sharing target and is described by the following fields:

| Field | Type | Description |
|-------|--------| ---------------|
| type |TRTCScreenCaptureSourceType| Capture source type, which can be specified as window or screen |
| sourceId | HWND| Capture source ID. <li>For a window, this field indicates a window handle; </li><li>for a screen, this field indicates a screen ID</li> |
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


>? Two additional parameters:
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
- **View macOS/Windows screen sharing**
  When a macOS/Windows user in a room starts screen sharing, the screen will be shared through a substream, and other users in the room will get a notification through the [onUserSubStreamAvailable](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) event in `TRTCCloudDelegate`.
  Users who want to view the shared screen can start rendering the substream image of the remote user through the [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) API.

- **View Android/iOS screen sharing**
  When an Android/iOS user starts screen sharing, the screen will shared through the primary stream, and other users in the room will get a notification through the [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) event in `TRTCCloudDelegate`.
  Users who want to view the shared screen can start rendering the primary stream image of the remote user through the [startRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) API.



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
By default, the SDK will automatically adjust the encoding parameters according to the shared window size.
If you want a fixed resolution, you need to call the `setSubStreamEncoderParam` API to set the encoding parameter for screen sharing or specify the corresponding encoding parameter when calling the `startScreenCapture` API.
