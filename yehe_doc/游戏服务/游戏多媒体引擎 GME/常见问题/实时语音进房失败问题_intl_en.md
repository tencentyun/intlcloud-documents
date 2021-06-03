## General Issues

### Is there a limit on the number of voice chat rooms and members in GME?

No.

### How many room members can speak at the same time?

It only supports up to 6 members to speak at the same time.
>! GME supports up to 20 mixing channels. We do not recommend more channels as it will be hard to know which player is speaking.

### Is there a requirement for the value of room ID?

A room ID is up to 127 characters (for voice message room, enter `null`).

### Why is there no callback information after calling the `EnterRoom` API?

Follow the steps below for troubleshooting:
1. Check whether the initialization is successful (i.e., the returned value is 0).
2. Check whether the Poll function is called periodically.
3. Check whether all the APIs are called in the main thread.

### I called the `EnterRoom` API and 0 is returned, but why I still failed to enter a room?

A callback will be returned after the `EnterRoom` API is called, which, instead of the API returned value, should be used to determine whether room entry succeeds.

### Why is the HTTP Invalid ID returned when I enter a room in the app?

If your account mapped by the `OpenId` parameter when you call the `EnterRoom` API starts from 0, we recommend adding 10000 to it. For example, if your account is 999, 10999 should be entered as your `OpenId`.

## Voice Chat Room Entering Failed

### How to troubleshoot issues when 10001 or other error codes are returned when I failed to enter a room?

Follow the steps below for troubleshooting:
1. Check whether the parameters of the `EnterRoom` API are valid, such as `AppID`, `UIN`, and `AuthBuffer`. For more information, please see [relevant API documentation](https://intl.cloud.tencent.com/zh/document/product/607/18522).
2. Check whether the relevant parameters in the console match the local ones.
3. Go to the console and check whether your account is in arrears.
4. Check whether your testing devices are in the private network or public network. If they are in the private network, please troubleshoot as instructed in [How to Deal with the Restrictions of Corporate Firewall](https://intl.cloud.tencent.com/document/product/607/35232).

### After calling the `Init` method, I called the `EnterRoom` API to enter a room, then the error code 1101 was returned. How to fix it?

Please make sure that all APIs are called in the same thread and the Poll API is called periodically.


## Voice Chat Room Entering Succeeded

### After entering a voice chat room, will the client be removed from the room if it switches to another app?

The server will have a heartbeat connection with the client. If the heartbeat pauses for 90 seconds, the server will remove the client.

### What should I do if a client is disconnected from a voice chat room?

If the network connection is interrupted, the client will try reconnecting to the room in 60 minutes. `ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT` will be called back after 60 minutes. After the reconnection, the microphone and speaker status do not need to be set.

### Is there an API for repossessing room IDs?

No. A room ID will be terminated when the last member exits the room.

### What to do with API calls if I enter a room immediately after exiting the room?

If you enter a room immediately after exiting the room in the application, you can directly call the `EnterRoom` API with no need to wait for the `RoomExitComplete` notification in the callback information of `ExitRoom`.

### Can I call `EnterRoom` and `ExitRoom` at the same time?

No. You need to call `ExitRoom` to exit the current room first, and then call `EnterRoom` to enter another room after receiving the callback information indicating a successful operation.

### When is the member status synced? Will a user receive a notification when entering the room for the first time?

- Notifications for audio events are triggered when reaching a preset threshold. The notification that "A member sends an audio packet" is sent when this threshold is reached. If a room member does not speak for two seconds, the notification "A member stops sending audio packets" will be sent.
- A user will receive the status notification when the user enters the room for the first time.

### If I add a member to the blocklist and then I exit the room, will the blocklist still be valid?

No. The blocklist will be invalid if its creator exits the room.

### I use the range voice feature and the 3D sound effect feature at the same time, only the range voice feature is effective. I have set the 3D sound effect file, but the return value is 0. How to fix it?

Please check whether the 3D sound effect API `EnableSpatializer` is enabled, and then check whether its position is updated as instructed in [3D Sound Effect](https://intl.cloud.tencent.com/document/product/607/18218).
