
Tencent Cloud TRTC supports screen sharing where the screen sharing image uses an independent channel of audio/video stream in parallel to the camera image. It also supports audio/video sync. Generally, the channel of the camera image is called the "primary channel (or primary image)", and the channel of screen sharing is called the "secondary channel (**substream**)". This document describes how to use the screen sharing feature of the TRTC SDK for macOS.

## Supported Platforms

| iOS | Android | macOS | Windows | Electron | WeChat Mini Program | Chrome Browser|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |   ×   |  &#10003;  |

## Getting Sharing Target
You can enumerate the list of sharable windows by using `getScreenCaptureSourcesWithThumbnailSize`, and each sharable target is a `TRTCScreenCaptureSourceInfo` object.

On macOS, the desktop screen is also a sharable target. A general window on macOS is of `TRTCScreenCaptureSourceTypeWindow` type, while the desktop window is of `TRTCScreenCaptureSourceTypeScreen` type.

In addition to `type`, each `TRTCScreenCaptureSourceInfo` also has the following fields:

| Field | Type | Description |
|:-------:|:--------:| :---------------:|
| type |TRTCScreenCaptureSourceType| Capture source type, which can be specified as window or screen |
| sourceId | NSString| Capture source ID. For a window, this field indicates a window handle; <br>for a screen, this field indicates a screen ID |
| sourceName| NSString | Window name. For screens, Screen0, Screen1, and so on will be returned |
| extInfo| NSDictionary | Additional information of shared window | 
| thumbnail| NSImage | Window thumbnail |
| icon | NSImage | Window icon |

With the information above, you can implement a simple list page to list the sharable targets for users to choose from as shown below:
![](https://main.qcloudimg.com/raw/c65302c0353f6cb6a70d71da30115da8.png)

## Selecting Sharing Target
TRTC SDK supports three sharing modes, which can be specified with `selectScreenCaptureTarget`.

- **Full screen sharing**:
This shares the entire screen and supports multi-display screen splitting. Specifically, you need to specify a `screenSource` parameter of `TRTCScreenCaptureSourceTypeScreen` type and set `rect` to { 0, 0, 0, 0 }.

- **Specified area sharing**:
This shares a certain area of the screen, and you need to define the coordinates of the area. Specifically, you need to specify a `screenSource` parameter of `TRTCScreenCaptureSourceTypeScreen` type and set `captureRect` to a non-null value, such as { 100, 100, 300, 300 }.

- **Specified window sharing**:
This shares a specified target window, and you need to select the window to be shared. Specifically, you need to specify a `screenSource` parameter of `TRTCScreenCaptureSourceTypeWindow` type and set `captureRect` to { 0, 0, 0, 0 }.


> Two additional parameters:
> - The `capturesCursor` parameter is used to specify whether to capture the cursor.
> - The `highlight` parameter is used to specify whether to highlight the currently shared window and whether to highlight a covered window to remind the user to move the covering window away. (This UI effect is implemented internally by the SDK.)


## Starting Screen Sharing

 - After selecting the sharing target, you can start screen sharing by using the `startScreenCapture` API.
 - The difference between functions `pauseScreenCapture` and `stopScreenCapture` is that the former will stop the capture of the screen content and display the image captured at the moment of pausing. Therefore, remote users will see a still image of the last frame until the sharing is resumed.
 
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
You can set the screen sharing image quality by using the `setSubStreamEncoderParam` API, which includes resolution, bitrate, and frame rate. The following recommended values are provided for your reference:

| Definition | Resolution | Frame Rate | Bitrate | 
|:-------------:|:---------:|:---------:| :---------: | 
| HD+ | 1920x1080 | 10 | 800 Kbps |
| HD | 1280x720 | 10 | 600 Kbps |
| SD | 960x720 | 10 | 400 Kbps |

## Viewing Shared Screen
When a user in a room starts screen sharing, other users in the room will get a notification through `onUserSubStreamAvailable` in `TRTCCloudDelegate`.
Then, users who want to view the shared screen can start rendering the secondary stream image of the remote user through `startRemoteSubStreamView`.

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
By default, the SDK will automatically adjust the encoding parameter according to the shared window size.
If you want a fixed resolution, you need to call the `setSubStreamEncoderParam` API to set the encoding parameter for screen sharing or specify the corresponding encoding parameter when calling `startScreenCapture`.
