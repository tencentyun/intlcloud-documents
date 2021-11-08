On macOS, TRTC supports screen sharing via the primary stream and substream:
- **Substream sharing**
In TRTC, you can share the screen via a dedicated stream, which is called the **substream**. In substream sharing, an anchor publishes camera video and screen sharing images at the same time. This is the scheme used by VooV Meeting. You can enable substream sharing by setting the `TRTCVideoStreamType` parameter to `TRTCVideoStreamTypeSub` when calling the `startScreenCapture` API. To play substream video, call `startRemoteSubStreamView`.

- **Primary stream sharing**
In TRTC, the channel via which camera images are published is the primary stream (**bigstream**). In primary stream sharing, an anchor publishes screen sharing images via the primary stream. As there is only one stream, an anchor cannot publish both camera video and screen sharing images. You can enable this mode by setting the `TRTCVideoStreamType` parameter to `TRTCVideoStreamTypeBig` when calling the `startScreenCapture` API.

## Supported Platforms

| iOS | Android | macOS | Windows | Electron| Chrome |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |  &#10003;  |

## Getting Sharable Sources
You can call [getScreenCaptureSourcesWithThumbnailSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a37df498cbc8d9b1135e3caafdcee906f) to enumerate sharable sources. Each sharable source is a `TRTCScreenCaptureSourceInfo` object.

The desktop of macOS is also a sharable source. The type of sharable windows on macOS is `TRTCScreenCaptureSourceTypeWindow`, while that of the desktop is `TRTCScreenCaptureSourceTypeScreen`.

You can find the following information, including `type`, for each `TRTCScreenCaptureSourceInfo` object:

| Parameter | Type | Description|
|:-------:|:--------:| :---------------:|
| type |TRTCScreenCaptureSourceType| Capturing source type, which may be window or screen|
| sourceId | NSString| Capturing source ID. If a window is captured, the value of this parameter is the window handle.<br>If a screen is captured, the value of this parameter is the screen ID. |
| sourceName| NSString | Window name. If a screen is captured, the value of this parameter is `Screen0`, `Screen1`, and so on. |
| extInfo| NSDictionary | Extra information |
| Thumbnail| NSImage | Window thumbnail |
| Icon | NSImage | Window icon |

Based on the information, you can display a list of sharable sources on the UI for users to choose from.


## Selecting Sharing Source
The TRTC SDK supports three sharing modes, which can be specified via [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a01ead6fb3106ea266caa922f5901bf18).

- **Share an entire screen**:
You can share an entire screen by selecting a source whose `type` is `TRTCScreenCaptureSourceTypeScreen` and setting `rect` to {0, 0, 0, 0}. This mode is supported when you split the screen onto multiple monitors.

- **Share a portion of a screen**:
You can share a specific portion of a screen by selecting a source whose `type` is `TRTCScreenCaptureSourceTypeScreen` and setting `rect` to a non-null value, such as {100, 100, 300, 300}.

- **Share a window**:
You can share a window by selecting a source whose `type` is `TRTCScreenCaptureSourceTypeWindow` and setting `rect` to {0, 0, 0, 0}.


>? Two additional parameters:
> - `capturesCursor`: specifies whether to capture the cursor.
> - `highlight`: specifies whether to highlight the window being shared and remind the user to move the window when it is covered. The relevant UI design is implemented within the SDK.


## Starting Screen Sharing

 - After selecting a sharing source, you can call [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) to start screen sharing.
 - The API [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6f536bcc3df21b38885809d840698280) differs from [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) in that it stops screen capturing and displays the image captured at the moment of pausing. As a result, remote users will see a still image until [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af257a8fb6969fe908ca68a039e6dba15) is called.

```Objective-C
 /**
 * 7.6 **Screen Sharing** Start screen sharing
 * @param view Parent control of the rendering control
 */
- (void)startScreenCapture:(NSView *)view;

/**
 * 7.7 **Screen Sharing** Stop screen sharing
 * @return `0`: successful; negative number: failed
 */
- (int)stopScreenCapture;

/**
 * 7.8 **Screen Sharing** Pause screen sharing
 * @return `0`: successful; negative number: failed
 */
- (int)pauseScreenCapture;

/**
 * 7.9 **Screen Sharing** Resume screen sharing
 *
 * @return `0`: successful; negative number: failed
 */
- (int)resumeScreenCapture;
```

## Setting Video Quality
You can use [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abc0f3cd5c320d0e65163bd07c3c0a735) to set the video quality of screen sharing, including resolution, bitrate, and frame rate. We recommend the following settings:

| Clarity | Resolution | Frame Rate | Bitrate |
|:-------------:|:---------:|:---------:| :---------: |
| FHD | 1920 × 1080 | 10 | 800 Kbps |
| HD | 1280 × 720 | 10 | 600 Kbps |
| SD | 960 × 720 | 10 | 400 Kbps |

## Watching Shared Screen
- **Watch screens shared by macOS/Windows users**
  When a macOS/Windows user in a room starts screen sharing, the screen will be shared through a substream, and other users in the room will be notified through [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ac45fb0751f7dbd2466a35c8828c9911b) in `TRTCCloudDelegate`.
  Users who want to watch the shared screen can start rendering the substream image of the remote user by calling the [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a68d048ccd0d018995e33e9e714e14474) API.

- **Watch screens shared by Android/iOS users**
  When an Android/iOS user starts screen sharing, the screen will be shared through the primary stream, and other users in the room will be notified through [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) in `TRTCCloudDelegate`.
  Users who want to watch the shared screen can start rendering the primary stream of the remote user by calling the [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) API.

```Objective-C
//Sample code: watch the shared screen

- (void)onUserSubStreamAvailable:(NSString *)userId available:(BOOL)available {
    if (available) {
        [self.trtcCloud startRemoteSubStreamView:userId view:self.capturePreviewWindow.contentView];
    } else {
        [self.trtcCloud stopRemoteSubStreamView:userId];
    }
}
```

## FAQs
**Can more than one user in a room share their screens at the same time?**
Currently, a TRTC room can have only one screen sharing stream at a time.

**When a specified window (`SourceTypeWindow`) is shared, if the window size changes, will the resolution of the video stream change accordingly?**
By default, the SDK automatically adjusts encoding parameters according to the size of the shared window.
If you want a fixed resolution, call the `setSubStreamEncoderParam` API to set encoding parameters for screen sharing or specify the parameters when calling the `startScreenCapture` API.