
## Overview
This document describes how to implement an online live broadcasting service that supports video co-anchoring and viewing by tens of thousands of concurrent viewers based on the TRTC SDK:

- This document only mentions the most basic features. If you want to learn more about advanced features, please see [Advanced Features](https://intl.cloud.tencent.com/document/product/647/35123/32227).
- This document only lists the most commonly used APIs. If you want to learn more about API functions, please see the [API documentation](https://intl.cloud.tencent.com/document/product/647/35123/32228).

## Sample Code

| Platform | Sample Code | 
|---------|---------|
| Android | [TRTCVideoRoomActivity.java](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTCDemo/app/src/main/java/com/tencent/liteav/demo/trtc/TRTCVideoRoomActivity.java) | 
| iOS | [TRTCMainViewController.m](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTCDemo/TRTC/TRTCMainViewController.m) | 
| macOS | [TRTCMainWindowController.m](https://github.com/tencentyun/TRTCSDK/blob/master/Mac/TRTCDemo/TRTC/TRTCMainWindowController.m) | 
| Windows (MFC) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows (Duilib) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |

![](https://main.qcloudimg.com/raw/b5013afb3606fa02ce6c622b4e7085db.jpeg)

## Live Broadcasting
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

### 3. Anchor previews camera image
The TRTC SDK does not enable local camera capture by default. `startLocalPreview` can enable the local camera and display the preview image, while `stopLocalPreview` will disable the camera.

Before local preview is started, `setLocalViewFillMode` can be called to specify the video display mode as `Fill` or `Fit`. In both modes, the video size will be proportionally scaled. The difference is that the `Fill` mode gives priority to ensuring that the window is filled (i.e., if the size of the scaled video does not match the display window size, the excessive video part will be truncated), while the `Fit` mode gives priority to ensuring that all video content is displayed (i.e., if the size of the scaled video does not match the display window size, the excessive window part will be filled with black color blocks).

```java
/** Enable local camera preview * /
void startLocalPreview(boolean frontCamera, TXCloudVideoView localVideoView) {
	trtcCloud.setLocalViewFillMode(TRTCCloudDef.TRTC_VIDEO_RENDER_MODE_FIT);
	trtcCloud.startLocalPreview(frontCamera, localVideoView);
}
```

### 4. Anchor enables mic capture
The TRTC SDK does not enable local mic capture by default. The anchor can call `startLocalAudio` to enable local sound capture and broadcast audio/video data, or call `stopLocalAudio` to disable sound capture. `startLocalAudio` can be called after `startLocalPreview`.

>`startLocalAudio` will check the mic permission. If there is no permission to use the mic, the SDK will ask the user to grant the permission.

### 5. Anchor creates a room and starts broadcasting

The anchor can use `enterRoom` to create an audio/video room. The `roomId` in the `TRTCParams` parameter is used to specify the room number. At the same time, the `role` field should be specified as `TRTCRoleAnchor` (anchor).

The `appScene` parameter specifies the application scenario of the SDK. In this document, `TRTC_APP_SCENE_LIVE` (online live broadcasting) is used as an example.

- If the creation is successful, the SDK will call back the `onEnterRoom` API. The `elapsed` parameter represents the time in ms it takes to enter the room.
- If the creation fails, the SDK will call back the `onError` API, which contains the following parameters: `errCode` (error code `ERR_ROOM_ENTER_FAIL`; for more information, please see `TXLiteAVCode.h`), `errMsg` (cause of error), and `extraInfo` (reserved parameter).

```java
void startBroadCasting() {
	// For the definition of `TRTCParams`, please see the `TRTCCloudDef.java` header file
	trtcParams = new TRTCCloudDef.TRTCParams();
	trtcParams.sdkAppId = sdkappid;
	trtcParams.userId   = userid;
	trtcParams.userSig  = usersig;
	trtcParams.roomId   = 908; // Enter the ID of the room you want to enter
	trtcParams.role     = TRTCRoleAnchor; // The current role is anchor
	trtcCloud.enterRoom(trtcParams, TRTC_APP_SCENE_LIVE);
}

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

### 6. Anchor enables/disables privacy mode
During the live broadcasting, the anchor may want to block local audio/video data for privacy reason. To this end, `muteLocalVideo` and `muteLocalAudio` can be called to block local video and audio capture, respectively.
	
### 7. Viewer enters the room to view

The viewer can call `enterRoom` to enter the audio/video room. `roomId` in the `TRTCParams` parameter is used to specify the room number.
`appScene` also needs to be specified as `TRTC_APP_SCENE_LIVE` (online live broadcasting), but the `role` field needs to be specified as `TRTCRoleAudience` (viewer).

```java
- (void)startPlaying {
	// For the definition of `TRTCParams`, please see the `TRTCCloudDef.java` header file
	trtcParams = new TRTCCloudDef.TRTCParams();
	trtcParams.sdkAppId = sdkappid;
	trtcParams.userId   = userid;
	trtcParams.userSig  = usersig;
	trtcParams.roomId   = 908; // Enter the ID of the room you want to enter
	trtcParams.role     = TRTCRoleAudience; // The current role is viewer
	trtcCloud.enterRoom(trtcParams, TRTC_APP_SCENE_LIVE);
}
```

If the anchor is in the room, the viewer will get the `userid` of the anchor through the `onUserVideoAvailable` callback in `TRTCCloudListener`. After that, the viewer can call the `startRemoteView` method to display the video image of the anchor.

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

> ! In `TRTC_APP_SCENE_LIVE` mode, there is no limit on the number of viewers (TRTCRoleAudience) in one single room.


### 8. Viewer co-anchors with anchor
	
Both the viewer and anchor can switch their roles through the `switchRole` API provided by TRTCCloud. The most common scenario is that the viewer co-anchors with the anchor: the viewer can switch to the anchor role through the following code, which is to turn themselves into an "assistant anchor" so that they can co-anchor with the original "primary anchor" in the room.

```java
public void onChangeRole(int role) {
	trtcCloud.switchRole(role);
        
if (role == TRTCCloudDef.TRTCRoleAnchor) { // Switch to the "anchor" role
	startLocalVideo(true); // Enable local video
	trtcCloud.startLocalAudio(); // Enable local audio
} else { // Switch to "viewer" role which does not need to upstream audio and video
	startLocalVideo(false);
	trtcCloud.stopLocalAudio();
}
}
```
  
### 9. Exit the room
Call the `exitRoom` method to exit the room. No matter whether or not a video call is currently in progress, calling this method will release all resources related to the video call. After `exitRoom` is called, the SDK will enter a complex exit handshake process, and the resources will be actually released only after the SDK calls back the `onExitRoom` method.

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


