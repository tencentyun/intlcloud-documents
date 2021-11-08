TRTC supports screen sharing on Android. This means a user can share the screen content of the local system with other users in the same room through the TRTC SDK. Pay attention to the following points regarding this feature:

- Unlike the desktop edition, for Android, SDK versions earlier than v8.6 do not support substream screen sharing. Therefore, video capturing by the camera must be stopped first before screen sharing can start. Substream screen sharing is supported on v8.6 and later versions, so there is no need to stop video capturing by the camera.
- Screen sharing consumes CPU. On Android, a background app consuming CPU continuously is very likely to be killed by the system. The solution to this problem is creating a floating window after screen sharing starts. As Android does not kill apps with foreground views, your app can share the screen continuously without being killed by the system.



## Supported Platforms

| iOS | Android | macOS | Windows | Electron| Chrome |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |  &#10003;  |

## Starting Screen Sharing
To start screen sharing on Android, simply call the [startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58) API in `TRTCCloud`. However, to ensure the stability and video quality of screen sharing, you need to do the following:

#### Adding an activity
Copy the activity below and paste it in the manifest file. You can skip this if the activity is already included in your project code.
```xml
<activity 
    android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity" 
    android:theme="@android:style/Theme.Translucent"/>
```

#### Setting video encoding parameters
By setting the first parameter `encParams` in [startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58), you can specify the encoding quality of screen sharing. If `encParams` is set to `null`, the SDK will use the encoding parameters set previously. We recommend the following settings:

| Item | Parameter | Recommended Value for Regular Scenarios | Recommended Value for Text-based Teaching |
|---------|---------|---------|-----|
| Resolution | videoResolution | 1280 × 720 | 1920 × 1080 |
| Frame rate | videoFps | 10 fps | 8 fps |
| Highest bitrate | videoBitrate| 1600 Kbps | 2000 Kbps |
| Resolution adaption | enableAdjustRes | NO | NO |

- As screen content generally does not change drastically, it is not economical to use a high frame rate. We recommend setting it to 10 fps.
- If the screen you share contains a large amount of text, you can increase the resolution and bitrate accordingly.
- The highest bitrate (`videoBitrate`) refers to the highest output bitrate when a shared screen changes dramatically. If the shared content does not change a lot, the actual encoding bitrate will be lower.

#### Displaying a floating window
Since Android 7.0, apps running in the background tend to be killed by the system if they consume CPU. To prevent your app from being killed when it is sharing the screen in the background, you need to create a floating window when screen sharing starts, which also serves the purpose of reminding the user to avoid displaying personal information as his or her screen is being shared.

- **Method 1: displaying a common floating window**
The code in [FloatingView.java](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTC-API-Example/Basic/ScreenShare/src/main/java/com/tencent/trtc/screenshare/FloatingView.java) offers an example of how to create a mini floating window similar to the one in VooV Meeting:
```java
public void showView(View view, int width, int height) {
        mWindowManager = (WindowManager) mContext.getSystemService(Context.WINDOW_SERVICE);
        // `TYPE_TOAST` applies only to Android 4.4 and above. On earlier versions, use `TYPE_SYSTEM_ALERT` (the permission needs to be declared in `manifest`).
        // Android 7.1 and above set restrictions on `TYPE_TOAST`.
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

- **Method 2: displaying a camera preview window**
Unlike the desktop edition, for Android, SDK versions earlier than v8.6 do not support substream screen sharing (supported on v8.6 and later versions), so during screen sharing, the primary stream cannot be used to send camera video.
What if a user wants to share the screen and send camera video at the same time?
Just display a floating window of the camera preview on the screen, and the window will be captured during screen sharing and shared together with the screen.

## Watching Shared Screen
- **Watch screens shared by macOS/Windows users**
  When a macOS/Windows user in a room starts screen sharing, the screen will be shared through a substream, and other users in the room will be notified through [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) in `TRTCCloudDelegate`.
  Users who want to watch the shared screen can start rendering the substream image of the remote user by calling the [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) API.

- **Watch screens shared by Android/iOS users**
  When an Android/iOS user starts screen sharing, the screen will be shared through the primary stream, and other users in the room will be notified through [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) in `TRTCCloudListener`.
  Users who want to watch the shared screen can start rendering the primary stream of the remote user by calling the [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) API.


```java
//Sample code: watch the shared screen
 @Override
 public void onUserSubStreamAvailable(String userId, boolean available) {
    startRemoteSubStreamView(userId);
}
```

## FAQs
 **Can there be multiple channels of screen sharing streams in a room at the same time?**
Currently, each TRTC room can have only one channel of screen sharing stream.
