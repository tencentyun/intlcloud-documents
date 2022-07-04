This document describes how to share the screen. Currently, a TRTC room can have only one screen sharing stream at a time.

TRTC supports screen sharing in primary stream and substream modes on Windows.

- **Substream sharing**
In TRTC, you can share the screen via a dedicated stream called the **substream**. In substream sharing, an anchor publishes camera video and screen sharing images at the same time. This is the scheme used by VooV Meeting. You can enable substream sharing by setting the `TRTCVideoStreamType` parameter to `TRTCVideoStreamTypeSub` when calling the `startScreenCapture` API.

- **Primary stream sharing**
In TRTC, the image from the user’s camera is published via the primary stream (**bigstream**). In primary stream sharing, an anchor publishes screen sharing images via the primary stream. Because there is only one stream, an anchor cannot publish both camera video and screen sharing images. You can enable this mode by setting the `TRTCVideoStreamType` parameter to `TRTCVideoStreamTypeBig` when calling the `startScreenCapture` API.

## APIs

| Description | C++ |  C# | Electron |
|---------|---------|---------|---------|
| Selects a sharing source | [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9d16af81b2ea2db7b91a8346add13393) | [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2aabe079ed38fb5122be988434a81a92) | [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) |
| Starts screen sharing | [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a984f461eebe77819f40c4129fc5a71bb) | [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e254) | [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) |
| Pauses screen sharing | [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a448e432a91c092f80421d377425fb1bb) | [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture) |
| Resumes screen sharing | [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad1fc32927622168e9b3cbb3f70043450) | [resumeScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeScreenCapture)|
| Ends screen sharing | [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad02093be5c603f66f356978169946a18) | [stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture) |


## Getting Sharing Sources
You can call `getScreenCaptureSources` to get a list of sharable sources, which is returned via the response parameter `sourceInfoList`.
>? On Windows, the desktop also counts as a window. When two monitors are used, each monitor corresponds to a desktop window. The list returned via `getScreenCaptureSources` includes desktop windows.

Based on the obtained window information, you can display a list of sharable sources on the UI for users to choose from.

## Starting Screen Sharing

 - After selecting a sharing source, you can call the `startScreenCapture` API to start screen sharing.
 - During screen sharing, you can call `selectScreenCaptureTarget` to change the sharing source.
 - The difference between `pauseScreenCapture` and `stopScreenCapture` is that `pauseScreenCapture` pauses screen capturing and displays the image at the moment it is paused. Remote users see the paused video image until screen capturing is resumed.


## Setting Video Quality
You can use the `setSubStreamEncoderParam` API to set the video quality of screen sharing, including resolution, bitrate, and frame rate. We recommend the following settings:

| Clarity | Resolution | Frame Rate | Bitrate |
|:-------------:|:---------:|:---------:| :---------: |
| FHD | 1920 x 1080 | 10 | 800 Kbps |
|  HD | 1280 x 720 | 10 | 600 Kbps |
| SD | 960 x 720 | 10 | 400 Kbps |

## Watching Shared Screen
  When a user in a room starts screen sharing, the screen will be shared through a substream, and other users in the room will be notified through [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html) in `ITRTCCloudCallback`.
  Users who want to view the shared screen can start rendering the substream image of the remote user by calling the [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html) API.

```C++
//Sample code: Watch the shared screen
void CTRTCCloudSDK::onUserSubStreamAvailable(const char * userId, bool available) {
    LINFO(L"onUserSubStreamAvailable userId[%s] available[%d]\n", UTF82Wide(userId).c_str(), available);
    liteav::ITRTCCloud* trtc_cloud_ = getTRTCShareInstance();
    if (available) {
        trtc_cloud_->startRemoteView(userId, liteav::TRTCVideoStreamTypeSub, hWnd);
    } else {
        trtc_cloud_->stopRemoteView(userId, liteav::TRTCVideoStreamTypeSub);
    }
}
```

## FAQs
#### 1. Can there be multiple channels of screen sharing streams in a room at the same time?
Currently, a TRTC room can have only one screen sharing stream at a time.

#### 2. When a specified window (`SourceTypeWindow`) is shared, if the window size changes, will the resolution of the video stream change accordingly?
By default, the SDK automatically adjusts encoding parameters according to the size of the shared window.
If you want a fixed resolution, call the `setSubStreamEncoderParam` API to set encoding parameters for screen sharing or specify the parameters when calling the `startScreenCapture` API.
