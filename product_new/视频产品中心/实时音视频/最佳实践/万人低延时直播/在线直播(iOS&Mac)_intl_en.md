
## Overview
This document describes how to implement an online live broadcasting service that supports video co-anchoring and viewing by tens of thousands of concurrent viewers based on the TRTC SDK:

- This document only mentions the most basic features. If you want to learn more about advanced features, please see [Advanced Features](https://intl.cloud.tencent.com/document/product/647/35242).
- This document only lists the most commonly used APIs. If you want to learn more about API functions, please see the [API documentation](https://intl.cloud.tencent.com/document/product/647/35119).

## Sample Code

| Platform | Sample Code | 
|---------|---------|
| iOS | TRTCMainViewController.m | 
| macOS | TRTCMainWindowController.m | 
| Android | TRTCVideoRoomActivity.java | 
| Windows (MFC) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows (Duilib) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |


## Live Broadcasting
### 1. Initialize the SDK

The first step in using the TRTC SDK is to get the singleton object of TRTCCloud and register a callback that listens on SDK events.

- First, inherit the `TRTCCloudDelegate` abstract class and override the events that need to be listened on (e.g., room entry, room exit, warning message, and error message).
- Get the TRTCCloud singleton object and call the `setDelegate` method to set the `TRTCCloudDelegate` callback.

```Objective-C
#import "TRTCCloud.h"
#import "TRTCCloudDelegate.h"

// Inherit the `TRTCCloudDelegate` callback 
@interface TRTCViewController() <TRTCCloudDelegate> {
	TRTCCloud       *trtcCloud;
	//...
}
@end

// Get the trtcCloud instance
- (void)viewDidLoad {
	[super viewDidLoad];
	//...
	trtcCloud = [TRTCCloud sharedInstance];
	[trtcCloud setDelegate:self];
}

// Terminate the trtcCloud singleton when the SDK is no longer used in order to reduce the overheads
- (void)dealloc {
    if (trtcCloud != nil) {
        [trtcCloud exitRoom];
    }
    [TRTCCloud destroySharedIntance];
}

// Error notifications should be listened on, as they indicate that the SDK cannot continue to run
- (void)onError:(int)errCode errMsg:(NSString *)errMsg extInfo:(nullable NSDictionary *)extInfo {
	if (errCode == ERR_ROOM_ENTER_FAIL) {
		[self toastTip:[NSString stringWithFormat:@"Failed to enter the room[%@]", errMsg]];
		[self exitRoom];
		return;
	}
}
```

### 2. Assemble `TRTCParams`

`TRTCParams` is the most critical parameter in the SDK. It contains the following four required fields: `sdkAppId`, `userId`, `userSig`, and `roomId`.

- **sdkAppId**
Log in to the [TRTC Console](https://console.cloud.tencent.com/rav). If you don't have an application yet, please create one and you will see the `sdkAppId`.

- **userId**
It can be specified arbitrarily. As it is of string type, it can be directly in line with your existing account system; however, please note that **there should not be identical `userIds` in the same audio/video room**.

- **userSig**
`userSig` can be calculated based on `sdkAppId` and `userId`. For the calculation method, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

- **roomId**
The room number is of numeric type and can be specified arbitrarily; however, please note that **different audio/video rooms in the same application cannot have the same `roomId`**.

### 3. Anchor previews camera image
The TRTC SDK does not enable local camera capture by default. `startLocalPreview` can enable the local camera and display the preview image, while `stopLocalPreview` will disable the camera.

Before local preview is started, `setLocalViewFillMode` can be called to specify the video display mode as `Fill` or `Fit`. In both modes, the video size will be proportionally scaled. The difference is that the `Fill` mode gives priority to ensuring that the window is filled (i.e., if the size of the scaled video does not match the display window size, the excessive video part will be truncated), while the `Fit` mode gives priority to ensuring that all video content is displayed (i.e., if the size of the scaled video does not match the display window size, the excessive window part will be filled with black color blocks).

In addition, there are some differences in the `startLocalPreivew` function between iOS and macOS:
-  On iOS, when `startLocalPreview` is called, the parameters are `frontCamera` (YES: front camera; NO: rear camera) and `view` (UIView control).
-  On macOS, when `startLocalPreview` is called, the parameter is `view` (NSView control).

```Objective-C
/** Enable local camera preview * /
// Sample call on iOS
- (void)startLocalPreview:(BOOL)frontCamera localView:(UIView*)localView {
	[trtcCloud setLocalViewFillMode:TRTCVideoFillMode_Fit];
	[trtcCloud startLocalPreview:frontCamera view:localView];
}

// Sample call on macOS
- (void)startLocalPreview:(NSView*)localView {
	[trtcCloud setLocalViewFillMode:TRTCVideoFillMode_Fit];
	[trtcCloud startLocalPreview:localView];
}
```

> The macOS edition of the SDK uses the current system default device by default. If there are multiple cameras, the camera to be used can be set by calling the `setCurrentCameraDevice` API. The `deviceId` parameter is the camera device ID. The desired `deviceId` can be obtained from the camera device list returned by the `getCameraDevicesList` API.


### 4. Anchor enables mic capture
The TRTC SDK does not enable local mic capture by default. The anchor can call `startLocalAudio` to enable local sound capture and broadcast audio/video data, or call `stopLocalAudio` to disable sound capture. `startLocalAudio` can be called after `startLocalPreview`.

>`startLocalAudio` will check the mic permission. If there is no permission to use the mic, the SDK will ask the user to grant the permission.

### 5. Anchor creates a room and starts broadcasting

The anchor can use `enterRoom` to create an audio/video room. The `roomId` in the `TRTCParams` parameter is used to specify the room number. At the same time, the `role` field should be specified as `TRTCRoleAnchor` (anchor).

The `appScene` parameter specifies the application scenario of the SDK. In this document, `TRTCAppSceneLIVE` (online live broadcasting) is used as an example.

- If the creation is successful, the SDK will call back the `onEnterRoom` API. The `elapsed` parameter represents the time in ms it takes to enter the room.
- If the creation fails, the SDK will call back the `onError` API, which contains the following parameters: `errCode` (error code `ERR_ROOM_ENTER_FAIL`; for more information, please see `TXLiteAVCode.h`), `errMsg` (cause of error), and `extraInfo` (reserved parameter).

```Objective-C
- (void)startBroadCasting {
{
	// For the definition of `TRTCParams`, please see the `TRTCCloudDef.h` header file
	TRTCParams *params = [[TRTCParams alloc] init];
	params.sdkAppId    = sdkappid;
	params.userId      = userid;
	params.userSig     = usersig;
	params.roomId      = 908; // Enter the ID of the room you want to enter
	params.role        = TRTCRoleAnchor; // The current role is anchor
	[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE];
}

- (void)onError:(int)errCode errMsg:(NSString *)errMsg extInfo:(nullable NSDictionary *)extInfo {
	if (errCode == ERR_ROOM_ENTER_FAIL) {
		[self toastTip:[NSString stringWithFormat:@"Failed to enter the room[%@]", errMsg]];
		[self exitRoom];
		return;
	}
}

- (void)onEnterRoom:(NSInteger)elapsed {
	NSString *msg = [NSString stringWithFormat:@"[%@]Entered room successfully[%u]: elapsed[%d]", _userID, _roomID, elapsed];
}
```

### 6. Anchor enables/disables privacy mode
During the live broadcasting, the anchor may want to block local audio/video data for privacy reason. To this end, `muteLocalVideo` and `muteLocalAudio` can be called to block local video and audio capture, respectively.

### 7. Viewer enters the room to view

The viewer can call `enterRoom` to enter the audio/video room. `roomId` in the `TRTCParams` parameter is used to specify the room number.
`appScene` also needs to be specified as `TRTCAppSceneLIVE` (online live broadcasting), but the `role` field needs to be specified as `TRTCRoleAudience` (viewer).

```Objective-C
- (void)startPlaying {
{
	// For the definition of `TRTCParams`, please see the `TRTCCloudDef.h` header file
	TRTCParams *params = [[TRTCParams alloc] init];
	params.sdkAppId    = sdkappid;
	params.userId      = userid;
	params.userSig     = usersig;
	params.roomId      = 908; // Enter the ID of the room you want to enter
	params.role        = TRTCRoleAudience; // The current role is viewer
	[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE];
}
```

If the anchor is in the room, the viewer will get the `userid` of the anchor through the `onUserVideoAvailable` callback in `TRTCCloudDelegate`. After that, the viewer can call the `startRemoteView` method to display the video image of the anchor.

`setRemoteViewFillMode` can be used to specify the video display mode as `Fill` or `Fit`. In both modes, the video size will be proportionally scaled. The difference lies in that:
- The `Fill` mode gives priority to ensuring that the window is filled (i.e., if the size of the scaled video does not match the display window size, the excessive video part will be truncated).
- The `Fit` mode gives priority to ensuring that all video content is displayed (i.e., if the size of the scaled video does not match the display window size, the excessive window part will be filled with black color blocks).

```Objective-C
- (void)onUserVideoAvailable:(NSString *)userId available:(BOOL)available {
    if (userId != nil) {
        TRTCVideoView* remoteView = [_remoteViewDic objectForKey:userId];
        if (available) {
            // Start the remote video decoding and display logic. `FillMode` can be used to set whether to display black bars
            [_trtc startRemoteView:userId view:remoteView];
            [_trtc setRemoteViewFillMode:userId mode:TRTCVideoFillMode_Fit];
        }
        else {
            [_trtc stopRemoteView:userId];
        }
   }  
}
```

> In `TRTCAppSceneLIVE` mode, there is no limit on the number of viewers (TRTCRoleAudience) in one single room.


### 8. Viewer co-anchors with anchor
Both the viewer and anchor can switch their roles through the `switchRole` API provided by TRTCCloud. The most common scenario is that the viewer co-anchors with the anchor: the viewer can call this API to turn themselves into an "assistant anchor" and co-anchor with the original "primary anchor" in the room.

```Objective-C
- (void)onClickedSwitch2Role:(BOOL)isAudience
{
    [_trtc switchRole:(isAudience? TRTCRoleAudience : TRTCRoleAnchor)];
    
    if (!isAudience) {
        // Switch to the "anchor" role and enable local audio/video upstreaming
        [_trtc startLocalAudio];
        [self startPreview];
    }
    else {
        // Switch to "viewer" role and disable local audio/video upstreaming
        [_trtc stopLocalAudio];
        [self stopPreview];
    }
}
```
  
### 9. Exit the room
Call the `exitRoom` method to exit the room. No matter whether or not a video call is currently in progress, calling this method will release all resources related to the video call. After `exitRoom` is called, the SDK will enter a complex exit handshake process, and the resources will be actually released only after the SDK calls back the `onExitRoom` method.

```Objective-C
- (void)exitRoom {
{
	[trtcCloud exitRoom];
}

- (void)onExitRoom:(NSInteger)reason {
	NSString *msg = [NSString stringWithFormat:@"left the room[%u]: reason[%d]", _roomID, reason];
}
```


