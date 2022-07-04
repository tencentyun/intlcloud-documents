This document describes how to actively exit the current TRTC room and in which cases will a user be forced to exit a room.
![](https://qcloudimg.tencent-cloud.cn/raw/ea39f08a98dc41195ae63a6ecae803b8.png)

## Call Guide


[](id:step1)
### Step 1. Perform prerequisite steps
Import the SDK and configure the application permissions as instructed in [iOS](https://intl.cloud.tencent.com/document/product/647/35092).
Enter the room as instructed in [Entering a Room](https://intl.cloud.tencent.com/document/product/647/47645).

[](id:step2)
### Step 2. Actively exit the current room
Call the `exitRoom` API to exit the current room, and the SDK will use the `onExitRoom(int reason)` callback to notify you of the reason the room was exited.
<dx-codeblock>
::: Android  java
// Exit the current room
mCloud.exitRoom();
:::
::: iOS&Mac  swift
self.trtcCloud = [TRTCCloud sharedInstance];
// Exit the current room
[self.trtcCloud exitRoom];
:::
::: Windows  C++
trtc_cloud_ = getTRTCShareInstance();
// Exit the current room
trtc_cloud_->exitRoom();
:::
</dx-codeblock>

After the `exitRoom` API is called, the SDK will enter the room exit process, where two key tasks need to be completed:
- **1. Notify the exit of the current user**
Notify other users in the room of the upcoming room exit, and they will receive the **onRemoteUserLeaveRoom** callback from the current user; otherwise, other users may think the current user's video image is simply frozen.
- **2. Revoke device permissions**
If the current user is publishing an audio/video stream before exiting the room, the user needs to turn off the camera and mic and release the device permissions during the room exit process.

Therefore, we recommend you release the `TRTCCloud` instance after receiving the `onExitRoom` callback.


[](id:step3)
### Step 3. Be forced to exit the current room
The `onExitRoom(int reason)` callback will also be received in other two cases in addition to active room exit:
- **Case 1. A user is kicked out of the room**
You can use the [RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) or [RemoveUserByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39630) API to kick a user out of a TRTC room. After being kicked out, the user will receive the `onExitRoom(1)` callback.

- **Case 2. The current room is closed**
You can call the [DismissRoom](https://intl.cloud.tencent.com/document/product/647/34269) or [DismissRoomByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39631) API to close a TRTC room. After the room is closed, all users in the room will receive the `onExitRoom(2)` callback.


<dx-codeblock>
::: Android  java
// Listen for the `onExitRoom` callback to get the reason for room exit
@Override
public void onExitRoom(int reason) {
    if (reason == 0) {
        Log.d(TAG, "Exit current room by calling the 'exitRoom' api of sdk ...");
    } else if (reason == 1) {
        Log.d(TAG, "Kicked out of the current room by server through the restful api...");
    } else if (reason == 2) {
        Log.d(TAG, "Current room is dissolved by server through the restful api...");
    }
}
:::
::: iOS&Mac  ObjC
// Listen for the `onExitRoom` callback to get the reason for room exit
- (void)onExitRoom:(NSInteger)reason {
    if (reason == 0) {
        NSLog(@"Exit current room by calling the 'exitRoom' api of sdk ...");
    } else if (reason == 1) {
        NSLog(@"Kicked out of the current room by server through the restful api...");
    } else if (reason == 2) {
        NSLog(@"Current room is dissolved by server through the restful api...");
    }
}
:::
::: Windows  C++
// Listen for the `onExitRoom` callback to get the reason for room exit
void onExitRoom(int reason) {
    if (reason == 0) {
        printf("Exit current room by calling the 'exitRoom' api of sdk ...");
    } else if (reason == 1) {
        printf("Kicked out of the current room by server through the restful api...");
    } else if (reason == 2) {
        printf("Current room is dissolved by server through the restful api...");
    }
}
:::
</dx-codeblock>
