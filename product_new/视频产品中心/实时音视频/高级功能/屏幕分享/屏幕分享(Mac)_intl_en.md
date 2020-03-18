
Tencent Cloud TRTC service supports a screen sharing feature in which the screen sharing image uses an independent single-channel audio/video stream and can be viewed as a split screen with the camera’s image. It also supports audio-video synchronization. We generally call the channel with the camera image the “main channel (or primary image)” and the channel with the screen sharing the “auxiliary channel (**substream**)”. This document mainly describes how to use TRTC SDK to provide a screen sharing feature on the Mac OS platform.

## Supported Platforms

| iOS | Android | Mac OS | Windows | WeChat Mini Program | Chrome Browser|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|     ✖  |    ✖    |    ✔   |    ✔    |    ✖     |   ✔     |

## Capturing the Sharing Target
You can make a list of sharable windows by using `getScreenCaptureSourcesWithThumbnailSize`, with each sharable target being a `TRTCScreenCaptureSourceInfo` object.

The desktop screen of Mac OS is also a sharable target. The type for ordinary Mac windows is `TRTCScreenCaptureSourceTypeWindow`, and the type for the desktop screen is `TRTCScreenCaptureSourceTypeScreen`.

In addition to its type, each `TRTCScreenCaptureSourceInfo` also has the following field information:

| Field | Type | Description|
|:-------:|:--------:| :---------------:|
| Type |TRTCScreenCaptureSourceType| Capture source type: specify type as window or screen|
| SourceId | NSString| Capture source ID: for a window, this field indicates window handle;<br>for a screen, this field indicates screen ID |
| SourceName| NSString | Window name, if screen then returns Screen0 Screen1... |
| ExtInfo| NSDictionary | Shared window’s extra information | 
| Thumbnail| NSImage | Window thumbnail |
| Icon | NSImage | Window icon |

With all this information, you can make a simple list page to list the sharable targets for users to choose from, as shown below:
![](https://main.qcloudimg.com/raw/ae43c4ec148a0e25368fea0ea20063b7.jpg)

## Selecting sharing targets
TRTC SDK supports three sharing modes, which you can specify using `selectScreenCaptureTarget`.

- **Full screen sharing**:
This shares the entire screen window, and multi-screen split screen is supported. You will need to specify the screenSource parameter of one type as `TRTCScreenCaptureSourceTypeScreen` and set its rect as { 0, 0, 0, 0 }.

- **Specific region sharing**:
This shares a certain region of the screen. The user needs to define the coordinates of the region’s location. You will need to specify the screenSource parameter of one type as `TRTCScreenCaptureSourceTypeScreen` and set its captureRect as non-null, such as { 100, 100, 300, 300 }.

- **Specific window sharing**:
This shares the contents of a target window. The user needs to select which window is to be shared. You will need to specify the screenSource parameter of one type as `TRTCScreenCaptureSourceTypeWindow` and set its captureRect as { 0, 0, 0, 0 }.


>? Two additional parameters
> - The capturesCursor parameter is used to specify whether or not to capture the cursor.
> - The highlight parameter is used to specify whether or not to highlight the window being shared and to remind the user to remove the mask when the captured image is masked. (This UI effect is achieved in SDK.)


## Starting Screen Sharing

 - After selecting the sharing target, you can start screen sharing by using the `startScreenCapture` API.
 - The difference between the two functions of `pauseScreenCapture` and `stopScreenCapture` is that pause will stop the capture of the screen contents and stay on the pause image displayed at the moment of pausing. Therefore, the remote end will see a still image of the last frame until it is resumed.
 
```Objective-C
 /**
 * 7.6 **Screen Sharing** Activate screen sharing
 * @param view the parent control of the render control
 */
- (void)startScreenCapture:(NSView *)view;

/**
 * 7.7 **Screen Sharing** Stop screen capture
 * @return 0: success < 0: failure
 */
- (int)stopScreenCapture;

/**
 * 7.8 **Screen Sharing** Pause screen sharing
 * @return 0: success < 0: failure
 */
- (int)pauseScreenCapture;

/**
 * 7.9 **Screen Sharing** Resume screen sharing
 *
 * @return 0: success < 0: failure
 */
- (int)resumeScreenCapture;
```

## Setting Image Quality
You can set the screen sharing image quality by using the `setSubStreamEncoderParam` API, which includes resolution, bitrate, and frame rate. The following recommended parameters are provided for your convenience:

| Definition | Resolution | Frame Rate | Bitrate | 
|:-------------:|:---------:|:---------:| :---------: | 
| High | 1920 × 1080 | 10 | 800 Kbps |
| Standard | 1280 × 720 | 10 | 600 Kbps |
| Low | 1280 × 720 | 10 | 400 Kbps |

## Viewing Screen Sharing
After one user in a room starts screen sharing, the other users in the room will get the `onUserSubStreamAvailable` notification through TRTCCloudDelegate.
After that, the users who wish to view screen sharing can start rendering the remote user’s auxiliary image through `startRemoteSubStreamView`.

```Objective-C
//Sample code: viewing screen sharing image

- (void)onUserSubStreamAvailable:(NSString *)userId available:(BOOL)available {
    if (available) {
        [self.trtcCloud startRemoteSubStreamView:userId view:self.capturePreviewWindow.contentView];
    } else {
        [self.trtcCloud stopRemoteSubStreamView:userId];
    }
}
```

## FAQs
** Can more than one person in the same room share their screen at the same time?**
Currently, one TRTC room can only have one channel of screen sharing at a time.

**When window sharing (SourceTypeWindow) is specified, will the resolution of the video stream change when the window size changes?**
It will not change because the window image will be proportionately scaled to the target resolution when the window size changes.
