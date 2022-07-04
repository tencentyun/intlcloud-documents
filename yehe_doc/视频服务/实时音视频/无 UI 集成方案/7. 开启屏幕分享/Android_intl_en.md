This document describes how to share the screen. Currently, a TRTC room can have only one screen sharing stream at a time.

## Call Guide
### Enabling screen sharing

[](id:step1)
#### Step 1. Add an Activity
Copy the activity below and paste it in the manifest file. You can skip this if the activity is already included in your project code.
```xml
<activity 
    android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity" 
    android:theme="@android:style/Theme.Translucent"/>
```

[](id:step2)
#### Step 2. Start screen sharing
To start screen sharing on Android, simply call the [startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58) API in `TRTCCloud`.

By setting the first parameter `encParams` in [startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58), you can specify the encoding quality of screen sharing. If `encParams` is set to `null`, the SDK will use the encoding parameters set previously. We recommend the following settings:

| Item | Parameter | Recommended Value for Regular Scenarios | Recommended Value for Text-based Teaching |
|---------|---------|---------|-----|
| Resolution | videoResolution | 1280 × 720 | 1920 × 1080 |
| Frame rate | videoFps | 10 fps | 8 fps |
| Highest bitrate | videoBitrate| 1600 Kbps | 2000 Kbps |
| Resolution adaption | enableAdjustRes | NO | NO |

- As screen content generally does not change drastically, it is not economical to use a high frame rate. We recommend setting it to 10 fps.
- If the screen you share contains a large amount of text, you can increase the resolution and bitrate accordingly.
- The highest bitrate (`videoBitrate`) refers to the highest output bitrate when a shared screen changes dramatically. If the shared content does not change a lot, the actual encoding bitrate will be lower.

[](id:step3)
#### Step 3. Display a floating window to avoid the application being closed (optional)
Since Android 7.0, apps running in the background tend to be closed by the system if they consume CPU. To prevent your app from being closed when it is sharing the screen in the background, you need to create a floating window when screen sharing starts. This also serves the purpose of reminding the user to avoid displaying personal information as his or her screen is being shared.

The code in [FloatingView.java](https://github.com/LiteAVSDK/TRTC_Android/tree/main/TRTC-API-Example/Basic/ScreenShare/src/main/java/com/tencent/trtc/screenshare/FloatingView.java) offers an example of how to create a mini floating window:
```java
public void showView(View view, int width, int height) {
        mWindowManager = (WindowManager) mContext.getSystemService(Context.WINDOW_SERVICE);
        int type = WindowManager.LayoutParams.TYPE_TOAST;
        // `TYPE_TOAST` applies only to Android 4.4 and later. On earlier versions, use `TYPE_SYSTEM_ALERT` (the permission needs to be declared in `manifest`).
        // Android 7.1 and later set restrictions on `TYPE_TOAST`.
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            type = WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY;
        } else if (Build.VERSION.SDK_INT > Build.VERSION_CODES.N) {
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

### Watching shared screen
- **Watch screens shared by macOS/Windows users**
  When a macOS/Windows user in a room starts screen sharing, the screen will be shared through a substream, and other users in the room will be notified through [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a80bcaac82e5372245746a4bc63656390) in `TRTCCloudListener`.

- **Watch screens shared by Android/iOS users**
  When an Android/iOS user starts screen sharing, the screen will be shared through the primary stream, and other users in the room will be notified through [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) in `TRTCCloudListener`.
  

Users who want to view the shared screen can start rendering the primary stream of the remote user by calling the [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) API.