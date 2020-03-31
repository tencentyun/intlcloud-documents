## Overview
This document describes how to implement a simple video call feature based on the TRTC SDK:

- This document only mentions the most basic features. If you want to learn more about advanced features, please see [Advanced Features](https://intl.cloud.tencent.com/document/product/647/35242).
- This document only lists the most commonly used APIs. If you want to learn more about API functions, please see the [API documentation](https://intl.cloud.tencent.com/document/product/647/35123/32258).

## Sample Code

| Platform | Sample Code | 
|---------|---------|
| Android | [TRTCVideoRoomActivity.java](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTCDemo/app/src/main/java/com/tencent/liteav/demo/trtc/TRTCVideoRoomActivity.java) | 
| iOS | [TRTCMainViewController.m](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTCDemo/TRTC/TRTCMainViewController.m) | 
| macOS | [TRTCMainWindowController.m](https://github.com/tencentyun/TRTCSDK/blob/master/Mac/TRTCDemo/TRTC/TRTCMainWindowController.m) | 
| Windows (MFC) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows (Duilib) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |

![](https://main.qcloudimg.com/raw/b5013afb3606fa02ce6c622b4e7085db.jpeg)


## Video Call
### 1. Initialize the SDK

The first step in using the TRTC SDK is to get the singleton object of TRTCCloud and register a callback that listens on SDK events.

- First, inherit the `TRTCCloudListener` abstract class and override the events that need to be listened on (e.g., room entry, room exit, warning message, and error message).
- Get the TRTCCloud singleton object and call the `setListener` method to set the `TRTCCloudListener` callback.

```java
import com.tencent.trtc.TRTCCloud;
import com.tencent.trtc.TRTCCloudListener;

// Inherit the `TRTCCloudListener` callback
static class TRTCCloudListenerImpl extends TRTCCloudListener {
	private WeakReference<TRTCMainActivity> mContext;
    public TRTCCloudListenerImpl(TRTCMainActivity activity) {
        super();
        mContext = new WeakReference<>(activity);
    }
	....
	// Error notifications should be listened on, as they indicate that the SDK cannot continue to run
	@Override
	public void onError(int errCode, String errMsg, Bundle extraInfo) {
	    Log.d(TAG, "sdk callback onError");
	    TRTCMainActivity activity = mContext.get();
	    if (activity != null) {
	        Toast.makeText(activity, "onError: " + errMsg + "[" + errCode+ "]" , Toast.LENGTH_SHORT).show();
	        if (errCode == TXLiteAVCode.ERR_ROOM_ENTER_FAIL) {
	            activity.exitRoom();
	        }
	    }
	}
}

// Get the trtcCloud singleton when the activity is created
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	....
	trtcListener = new TRTCCloudListenerImpl(this);
    trtcCloud = TRTCCloud.sharedInstance(this);
    trtcCloud.setListener(listener);
}

// Terminate the trtcCloud singleton when the SDK is no longer used in order to reduce the overheads
@Override
protected void onDestroy() {
    super.onDestroy();
    // Terminate the TRTC instance
    if (trtcCloud != null) {
        trtcCloud.setListener(null);
    }
    trtcCloud = null;
    TRTCCloud.destroySharedInstance();
}

```

### 2. Assemble `TRTCParams`

`TRTCParams` is the most critical parameter in the SDK. It contains the following four required fields: `sdkAppId`, `userId`, `userSig`, and `roomId`.

- **sdkAppId**
Log in to the [TRTC Console](https://console.cloud.tencent.com/rav). If you don't have an application yet, please create one and you will see the `sdkAppId`.
![](https://main.qcloudimg.com/raw/e42c76fd9d4fd3e3e5d80e8fb2763134.png)

- **userId**
It can be specified arbitrarily. As it is of string type, it can be directly in line with your existing account system; however, please note that **there should not be identical `userIds` in the same audio/video room**.

- **userSig**
`userSig` can be calculated based on `sdkAppId` and `userId`. For the calculation method, please see [How to Generate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

- **roomId**
The room number is of numeric type and can be specified arbitrarily; however, please note that **different audio/video rooms in the same application cannot have the same `roomId`**.


### 3. Enter (or create) a room
Call `enterRoom` to enter the audio/video room specified by `roomId` in the `TRTCParams` parameter. If the room does not exist, the SDK will automatically create it with the `roomId` as the room number.

The **appScene** parameter specifies the application scenario of the SDK, which is `TRTCAppSceneVideoCall` (video call) in this document. In this scenario, the SDK's internal codec and network component focus more on video smoothness to reduce call latency and lagging.

- If the room entry succeeds, the SDK will call back the `onEnterRoom` API. Parameters: when `result` is greater than 0, the room entry succeeds, and the value indicates the time in milliseconds (ms) used for entering the room; when `result` is less than 0, the room entry fails, and the value indicates the error code of the failure.
- If the room entry fails, the SDK will also call back the `onError` API, which contains the following parameters: `errCode` (error code `ERR_ROOM_ENTER_FAIL`; for more information, please see `TXLiteAVCode.h`), `errMsg` (cause of error), and `extraInfo` (reserved parameter).
- If you are already in the room, you must call the `exitRoom` method to exit the current room before entering the next room. 

```java
void enterRoom() {
	// For the definition of `TRTCParams`, please see the `TRTCCloudDef.java` header file
	trtcParams = new TRTCCloudDef.TRTCParams();
	trtcParams.sdkAppId = sdkappid;
	trtcParams.userId   = userid;
	trtcParams.userSig  = usersig;
	trtcParams.roomId   = 908; // Enter the ID of the room you want to enter
	trtcCloud.enterRoom(trtcParams, TRTC_APP_SCENE_VIDEOCALL);
}

...

@Override
public void onError(int errCode, String errMsg, Bundle extraInfo) {
    Log.d(TAG, "sdk callback onError");
    TRTCMainActivity activity = mContext.get();
    if (activity != null) {
        Toast.makeText(activity, "onError: " + errMsg + "[" + errCode+ "]" , Toast.LENGTH_SHORT).show();
        if (errCode == TXLiteAVCode.ERR_ROOM_ENTER_FAIL) {
            activity.exitRoom();
        }
    }
}

@Override
public void onEnterRoom(long elapsed) {
    TRTCMainActivity activity = mContext.get();
    if (activity != null) {
        Toast.makeText(activity, "Entered room successfully", Toast.LENGTH_SHORT).show();
    }
}
```

>!Please select the appropriate `scene` parameter according to the actual application scenario. An incorrect selection may lead to higher lagging rate or lower video definition than expected.

### 4. Listen to remote audio stream
The TRTC SDK receives remote audio streams by default, so you don't need to write extra code for this. If you don't want to listen to the audio stream of a certain `userid`, you can mute it by calling `muteRemoteAudio`.

### 5. Watch remote video stream
The TRTC SDK does not pull remote video streams by default. When there is a user upstreaming video data in the room, other users in the room can get the `userid` of the user through the `onUserVideoAvailable` callback in `TRTCCloudListener`. After that, they can call the `startRemoteView` method to display the video image of the user.

`setRemoteViewFillMode` can be used to specify the video display mode as `Fill` or `Fit`. In both modes, the video size will be proportionally scaled. The difference lies in that:
- The `Fill` mode gives priority to ensuring that the window is filled (i.e., if the size of the scaled video does not match the display window size, the excessive video part will be truncated).
- The `Fit` mode gives priority to ensuring that all video content is displayed (i.e., if the size of the scaled video does not match the display window size, the excessive window part will be filled with black color blocks).

```java
@Override
public void onUserVideoAvailable(final String userId, boolean available){
    TRTCMainActivity activity = mContext.get();
    if (activity != null) {
        if (available) {
            // Set `remoteView`
            TXCloudVideoView remoteView = new TXCloudVideoView(mContext);
            mParentView.add(remoteView);
            trtcCloud.setRemoteViewFillMode(userId, TRTCCloudDef.TRTC_VIDEO_RENDER_MODE_FIT);
            trtcCloud.startRemoteView(userId, remoteView);
        } else {
            // Stop viewing the video image
            trtcCloud.stopRemoteView(userId);
        }
    }
}
```

### 6. Enable/disable local sound capture
The TRTC SDK does not enable local mic capture by default. `startLocalAudio` can be called to enable local sound capture and broadcast audio/video data, while `stopLocalAudio` can disable sound capture.

- `startLocalAudio` will check the mic permission. If there is no permission to use the mic, the SDK will ask the user to grant the permission.
- `startLocalAudio` can be called after `startLocalPreview`.

### 7. Enable/disable local video capture

The TRTC SDK does not enable local camera capture by default. `startLocalPreview` can enable the local camera and display the preview image, while `stopLocalPreview` will disable the camera.

- Before local preview is enabled, `setLocalViewFillMode` can be called to specify the video display mode as `Fill` or `Fit`. In both modes, the video size will be proportionally scaled. The difference lies in that:  
	- The `Fill` mode gives priority to ensuring that the window is filled (i.e., if the size of the scaled video does not match the display window size, the excessive video part will be truncated).  
	- The `Fit` mode gives priority to ensuring that all video content is displayed (i.e., if the size of the scaled video does not match the display window size, the excessive window part will be filled with black color blocks).

- Call `startLocalPreview`. Parameters: `frontCamera` (true: front camera; false: rear camera), `view` (TXCloudVideoView SDK's custom rendering control).

```java
/** Enable local camera preview * /
void startLocalPreview(boolean frontCamera, TXCloudVideoView localVideoView) {
	trtcCloud.setLocalViewFillMode(TRTCCloudDef.TRTC_VIDEO_RENDER_MODE_FIT);
    trtcCloud.startLocalPreview(frontCamera, localVideoView);
}
```

### 8. Block audio/video data stream

- **Block local video data**
  If the user wants to block local video data for privacy reason during the call, so that other users in the room cannot temporarily view their video image, `muteLocalVideo` can be called to this end.
  
- **Block local audio data**
  If the user wants to block local audio data for privacy reason during the call, so that other users in the room cannot temporarily hear their sound, `muteLocalAudio` can be called to this end.
  
- **Block remote video data**
  `stopRemoteView` can be called to block the video data of a certain `userid`.
  `stopAllRemoteView` can be called to block the video data of all remote users.
  
- **Block remote audio data**
  `muteRemoteAudio` can be called to block the audio data of a certain `userid`.
  `muteAllRemoteAudio` can be called to block the audio data of all remote users.


### 9. Exit the room

Call the `exitRoom` method to exit the room. No matter whether or not a video call is currently in progress, calling this method will release all resources related to the video call.

>After `exitRoom` is called, the SDK will enter a complex exit handshake process, and the resources will be actually released only after the SDK calls back the `onExitRoom` method.

```java
...
private void exitRoom() {
    if (trtcCloud != null) {
        trtcCloud.exitRoom();
    }
}
...
@Override
public void onExitRoom(int reason) {
    TRTCMainActivity activity = mContext.get();
    if (activity != null) {
        activity.finishActivity();
    }
}

```

