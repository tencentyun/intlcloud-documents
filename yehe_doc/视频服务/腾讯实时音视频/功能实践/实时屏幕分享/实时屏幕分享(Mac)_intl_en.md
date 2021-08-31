TRTC supports screen sharing in primary stream and substream modes on macOS:
- **Substream sharing**
In TRTC, we can separately open one video upstream for screen sharing and call it "**substream**". Substream sharing means that the anchor can upstream both the camera image and the screen at the same time. This is the usage scheme of VooV Meeting. You can enable this mode by specifying the `TRTCVideoStreamType` parameter as `TRTCVideoStreamTypeSub` when calling the `startScreenCapture` API. The dedicated `startRemoteSubStreamView` API is needed to watch this channel of video image.

- **Primary stream sharing**
In TRTC, we generally call the channel of the camera image "**primary stream (aka bigstream)**", and primary stream sharing is to share the screen through the camera channel. In this mode, the anchor has only one video upstream, which can be either the camera image or the screen, and the two are mutually exclusive. You can enable this mode by specifying the `TRTCVideoStreamType` parameter as `TRTCVideoStreamTypeBig` when calling the `startScreenCapture` API.

## Supported Platforms

| iOS | Android | macOS | Windows | Electron | WeChat Mini Program | Chrome Browser|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |   ×   |  &#10003;  |

## Getting Sharing Target
You can enumerate the list of sharable windows by using [getScreenCaptureSourcesWithThumbnailSize](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa8e5286e1035b64b7d2bf8fadd721123), and each sharable target is a `TRTCScreenCaptureSourceInfo` object.

On macOS, the desktop screen is also a sharable target. A general window on macOS is of `TRTCScreenCaptureSourceTypeWindow` type, while the desktop window is of `TRTCScreenCaptureSourceTypeScreen` type.

In addition to `type`, each `TRTCScreenCaptureSourceInfo` also has the following fields:

| Field | Type | Description |
|:-------:|:--------:| :---------------:|
| type |TRTCScreenCaptureSourceType| Capture source type, which can be specified as window or screen |
| sourceId | NSString| Capture source ID. For a window, this field indicates a window handle; <br>for a screen, this field indicates a screen ID |
| sourceName| NSString | Window name. For screens, Screen0, Screen1, and so on will be returned. |
| extInfo| NSDictionary | Additional information of shared window | 
| thumbnail| NSImage | Window thumbnail |
| icon | NSImage | Window icon |

With the information above, you can implement a simple list page to list the sharable targets for users to choose from:

## Selecting Sharing Target
TRTC SDK supports three sharing modes, which can be specified with [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a01ead6fb3106ea266caa922f5901bf18):

- **Full screen sharing**:
This shares the entire screen and supports multi-display screen splitting. Specifically, you need to specify a `screenSource` parameter of `TRTCScreenCaptureSourceTypeScreen` type and set `rect` to { 0, 0, 0, 0 }.

- **Specified area sharing**:
This shares a certain area of the screen, and you need to define the coordinates of the area. Specifically, you need to specify a `screenSource` parameter of `TRTCScreenCaptureSourceTypeScreen` type and set `captureRect` to a non-null value, such as { 100, 100, 300, 300 }.

- **Specified window sharing**:
This shares a specified target window, and you need to select the window to be shared. Specifically, you need to specify a `screenSource` parameter of `TRTCScreenCaptureSourceTypeWindow` type and set `captureRect` to { 0, 0, 0, 0 }.


>? Two additional parameters:
> - The `capturesCursor` parameter is used to specify whether to capture the cursor.
> - The `highlight` parameter is used to specify whether to highlight the currently shared window and whether to highlight a covered window to remind the user to move the covering window away. (This UI effect is implemented internally by the SDK.)


## Starting Screen Sharing

 - After selecting the sharing target, you can start screen sharing by using the [startScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) API.
 - The difference between functions [pauseScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6f536bcc3df21b38885809d840698280) and  [stopScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) is that the former will stop the capture of the screen content and display the image captured at the moment of pausing; therefore, remote users will see a still image of the last frame until [resumeScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af257a8fb6969fe908ca68a039e6dba15).
 
```Objective-C
 /**
 *  7.6 **Screen Sharing**   Start screen sharing
 *  @param view    Parent control of the rendering control
 */
- (void)startScreenCapture:(NSView *)view;

/**
 *  7.7 **Screen Sharing**   Stop screen capture
 *  @return   0: success; <0: failure
 */
- (int)stopScreenCapture;

/**
 *  7.8 **Screen Sharing**   Pause screen sharing
 *  @return   0: success; <0: failure
 */
- (int)pauseScreenCapture;

/**
 *  7.9 **Screen Sharing**   Resume screen sharing
 *
 *  @return   0: success; <0: failure
 */
- (int)resumeScreenCapture;
```

## Setting Image Quality
You can set the screen sharing image quality by using the [setSubStreamEncoderParam](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#abc0f3cd5c320d0e65163bd07c3c0a735) API, which includes resolution, bitrate, and frame rate. The following recommended values are provided for your reference:

| Definition | Resolution | Frame Rate | Bitrate | 
|:-------------:|:---------:|:---------:| :---------: | 
| HD+ | 1920x1080 | 10 | 800 Kbps |
| HD | 1280x720 | 10 | 600 Kbps |
| SD | 960x720 | 10 | 400 Kbps |

## Viewing Shared Screen
- **View macOS/Windows screen sharing**
  When a macOS/Windows user in a room starts screen sharing, the screen will be shared through a substream, and other users in the room will get a notification through the [onUserSubStreamAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#ac45fb0751f7dbd2466a35c8828c9911b) event in `TRTCCloudDelegate`.
  Users who want to view the shared screen can start rendering the substream image of the remote user through the [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a68d048ccd0d018995e33e9e714e14474) API.

- **View Android/iOS screen sharing**
  When an Android/iOS user starts screen sharing, the screen will shared through the primary stream, and other users in the room will get a notification through the [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) event in `TRTCCloudDelegate`.
  Users who want to view the shared screen can start rendering the primary stream image of the remote user through the [startRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) API.



```Objective-C
// Sample code: viewing screen sharing image

- (void)onUserSubStreamAvailable:(NSString *)userId available:(BOOL)available {
    if (available) {
        [self.trtcCloud startRemoteSubStreamView:userId view:self.capturePreviewWindow.contentView];
    } else {
        [self.trtcCloud stopRemoteSubStreamView:userId];
    }
}
```

## FAQs
**Can there be more than one user sharing their screens in the same room at the same time?**
Currently, there can be only one channel of screen sharing in a TRTC room.

**When window sharing (SourceTypeWindow) is specified, will the resolution of the video stream change as the window size changes?**
By default, the SDK will automatically adjust the encoding parameters according to the shared window size.
If you want a fixed resolution, you need to call the `setSubStreamEncoderParam` API to set the encoding parameter for screen sharing or specify the corresponding encoding parameter when calling the `startScreenCapture` API.
