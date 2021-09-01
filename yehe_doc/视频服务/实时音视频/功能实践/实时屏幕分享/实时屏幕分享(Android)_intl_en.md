TRTC supports screen sharing on Android, i.e., sharing the screen content of the local system to other users in the same room through the TRTC SDK. You need to pay attention to the following points for this feature:

- Unlike the desktop edition, TRTC for Android does not support "substream sharing" during screen sharing. Therefore, before starting screen sharing, you need to stop the camera capture first to avoid the conflict.
- If an application on the background on Android uses the CPU continuously, it is very likely to be forcibly killed by the system, but screen sharing must use CPU. To solve this dilemma, you need to activate a floating window when starting screen sharing in an application. As Android does not forcibly kill application processes with foreground UI, this solution allows your application to continuously share the screen content without being automatically repossessed by the system.


## Supported Platforms

| iOS | Android | macOS | Windows | Electron |  Chrome Browser|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |  &#10003;  |

## Starting Screen Sharing
To start screen sharing on Android, you only need to call the [startScreenCapture()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58) API in `TRTCCloud`. If you want to achieve a more stable and clearer sharing effect, you need to address the following two issues:

#### Setting video encoding parameters
By setting the first parameter `encParams` in [startScreenCapture()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58), you can specify the encoding quality of screen sharing. If `encParams` is set to `null`, the SDK will automatically use the previously set encoding parameter. We recommend you use the following parameter values:

| Parameter Item | Parameter Name | Common Recommended Value | Recommended Value for Text-based Teaching |
|---------|---------|---------|-----|
| Resolution | videoResolution | 1280x720 | 1920x1080 |
| Frame rate | videoFps | 10 FPS | 8 FPS |
| Highest bitrate | videoBitrate| 1,600 Kbps | 2,000 Kbps |
| Resolution adaption | enableAdjustRes | No | No |

- As the content in screen sharing generally does not change drastically, it is not economical to set a high FPS, and 10 FPS is recommended.
- If the screen sharing content contains many words, you can increase the resolution and bitrate accordingly.
- The highest bitrate (`videoBitrate`) refers to the highest output bitrate when the image content changes dramatically. If the screen content does not change a lot, the actual encoding bitrate will be lower.

#### Displaying floating window to avoid forced kill
Starting from Android 7.0, common applications running on the background tend to be forcibly killed by the system if they use the CPU. Therefore, if an application carrying out screen sharing enters the background, you can display a floating window to prevent it from being killed by the system. In addition, a pop-up floating window also informs the user of the ongoing screen sharing, helping avoid the leakage of confidential information.

- **Solution 1. Display a common floating window**
You can display a mini floating window similar to that in VooV Meeting based on the implementation in the sample code [FloatingView.java](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTC-API-Example/Basic/ScreenShare/src/main/java/com/tencent/trtc/screenshare/FloatingView.java)

```java
public void showView(View view, int width, int height) {
        mWindowManager = (WindowManager) mContext.getSystemService(Context.WINDOW_SERVICE);
        // `TYPE_TOAST` is applicable to only Android 4.4 and above. If you want to use it on an older version, use `TYPE_SYSTEM_ALERT` (the permission needs to be declared in `manifest`)
        // Android 7.1 and above places restrictions on `TYPE_TOAST`
        int type = WindowManager.LayoutParams.TYPE_TOAST;
        if (Build.VERSION.SDK_INT > Build.VERSION_CODES.N) {
            type = WindowManager.LayoutParams.TYPE_PHONE;
        }
        mLayoutParams = new WindowManager.LayoutParams(type);
        mLayoutParams.flags = WindowManager.LayoutParams.FLAG_NOT_FOCUSABLE;
        mLayoutParams.flags |= WindowManager.LayoutParams.FLAG_WATCH_OUTSIDE_TOUCH;
        mLayoutParams.width = width;
        mLayoutParams.height = height;
        mLayoutParams.format = PixelFormat.TRANSLUCENT;
        mWindowManager.addView(view, mLayoutParams);
}
```

- **Solution 2. Display the camera preview popup**
Unlike the desktop edition, TRTC for Android does not support "substream sharing" in screen sharing. Therefore, during screen sharing, the camera video data cannot be upstreamed; otherwise, a conflict will occur.
Then, what should be done to share the screen and camera image at the same time?
The solution is simple: you only need to display a floating window of the camera image on the screen. In this way, TRTC can share the camera image together when capturing the screen image.

## Viewing Shared Screen
- **View macOS/Windows screen sharing**
  When a macOS/Windows user in a room starts screen sharing, the screen will be shared through a substream, and other users in the room will get a notification through the [onUserSubStreamAvailable](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) event in `TRTCCloudDelegate`.
  Users who want to view the shared screen can start rendering the substream image of the remote user through the [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) API.

- **View Android/iOS screen sharing**
  When an Android/iOS user starts screen sharing, the screen will shared through the primary stream, and other users in the room will get a notification through the [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) event in `TRTCCloudListener`.
  Users who want to view the shared screen can start rendering the primary stream image of the remote user through the [startRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) API.


```java
// Sample code: viewing screen sharing image
 @Override
 public void onUserSubStreamAvailable(String userId, boolean available) {
    startRemoteSubStreamView(userId);
}
```

## FAQs
 **Can there be more than one channel of screen sharing in the same room at the same time?**
Currently, there can be only one channel of screen sharing in a TRTC room.


