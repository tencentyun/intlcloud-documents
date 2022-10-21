## TUICalling

TUICalling is based on two services: TRTC and IM. It supports one-to-one and group video calls

- [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/39169): Used as a low-latency audio/video call component.
- [IM SDK](https://intl.cloud.tencent.com/document/product/1047/40124): Used to send and process signaling messages.
Audio/Video call UIs are shown as follows:

<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" width="300px"><b>Video Call<br></b></th>
    <th style="text-align:center;" width="300px"><b>Audio Call</b><br></th>
  </tr>
  <tr>
    <td><img style="width:300px" 
		src="https://qcloudimg.tencent-cloud.cn/raw/5a2c54f73bce1e71645f01f0eecee827.png"  />    </td>
    <td><img style="width:300px" 
		src="https://qcloudimg.tencent-cloud.cn/raw/80e65e5c0a6ab703740a40b12ae2806b.png" />     </td>
	 </tr>
</table>

## `TUICalling` API Overview
### Basic APIs

- [init](#init): Initializes a TUICalling instance.
- [sharedInstance](#sharedinstance): Gets a component singleton.
- [call](#call): Starts a one-to-one call.
- [groupCall](#groupcall): Starts a group call.
- [destroy](#destroy): Terminates TUICalling.
- [setCallingListener](#setcallinglistener): Sets a listener.
- [removeCallingListener](#removecallinglistener): Removes a listener.
- [enableCustomViewRoute](#enableCustomViewRoute): Enables/Disables custom views.

### Basic add-ons
- `CallMessageItem`: Customizes an audio/video call message.
- `isCallingData`: Checks whether the message is an audio/video call message.

## Prerequisites
- Create a Flutter application.
- Add `tim_ui_kit_calling_plugin` under `dependencies` in the `pubspec.yaml` file, or run the following command:
```dart
/// Step 1:
flutter pub add tim_ui_kit_calling_plugin

/// Step 2:
flutter pub get
```

Enable the push plugin in the plugin marketplace as instructed [here](https://intl.cloud.tencent.com/document/product/1047/48568).

## Directions
### Step 1. Import `navigatorKey`
Add `navigatorKey` to your `MateriaApp`, so that the call window can be opened when an audio call is received.
```dart
import 'package:tim_ui_kit_calling_plugin/tim_ui_kit_calling_plugin.dart';


MaterialApp(
    navigatorKey: TUICalling.navigatorKey,
    ...
)
```

### Step 2. Initialize the TUICalling instance
Log in before initializing the TUICalling instance if you integrate the audio/video call feature into an existing IM for Flutter application.
 During TUICalling instance initialization, the call window will automatically pop up after an audio/video call is received. In addition, IM will be automatically initialized and logged in to send an audio/video call invitation signaling.
```dart
    class  HomePageState extends State<HomePage> {
        final TUICalling _calling = TUICalling();
            
        @override
        initState() {
            super.initState();  
            final userID = '1234756';
            final userSig = '';
            final sdkAppId = 0; /// SDKAppID obtained from the console
            _calling.init(sdkAppID: sdkAppId, userID: userID, userSig: userSig);
        }
    }
```

>?The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [here](https://intl.cloud.tencent.com/document/product/647/35166).

## Definitions of Basic Functions
### init[](id:init)
Initialization
```dart
 Future<void> init({required int sdkAppID, required String userID,required String userSig});
```
### call[](id:call)
This function is used to make a one-to-one call.
```dart
 Future<void> call(String userId,CallingScenes type,)
```

### groupCall[](id:groupcall)
This function is used to make a group call.
```dart
 Future<void> call(List<String> userIdList, CallingScenes type, String? groupId)
```

### destroy[](id:destroy)
Termination
```dart
 void destroy()
```

### enableCustomViewRoute[](id:enableCustomViewRoute)
This API is used to enable/disable custom views.
```dart
 void enableCustomViewRoute(bool isEnable)
```
### setCallingListener[](id:setcallinglistener)
This API is used to set the listener.
```dart
 void setCallingListener(TUICallingListener listener);
```
### removeCallingListener[](id:removecallinglistener)
This API is used to remove a listener.
```dart
 void removeCallingListener(TUICallingListener listener);
```

### sharedInstance[](id:sharedinstance)
```dart
    Future<TRTCCalling> sharedInstance();
```

### TUICallingListener[](id:TUICallingListener)
``` dart
  /// Callback for error. This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.
  ///
  /// param:
  ///
  /// errCode Error code
  ///
  /// errMsg	Error message
  ///
  /// extraInfo Extended field. Certain error codes may carry extra information for troubleshooting
  onError,

  /// Callback for warning. This callback alerts you to non-serious problems such as stutter or recoverable decoding failure.
  ///
  /// param:
  ///
  /// warningCode Warning code
  ///
  /// warningMsg Warning message
  ///
  /// extraInfo Extended field. Certain warning codes may carry extra information for troubleshooting
  onWarning,

  // Local room entry
  ///
  /// If room entry succeeded, `result` would be a positive number (`result` > 0), indicating the time in milliseconds (ms) room entry took.
  ///
  /// If room entry failed, `result` would be a negative number (`result` < 0), which represents the error code.
  ///
  /// param:
  ///
  /// If `result` is greater than 0, it indicates the time (in ms) room entry takes; if `result` is less than 0, it represents the error code.
  onEnterRoom,

  /// Callback for the entry of a remote user
  ///
  /// param:
  ///
  /// userId User ID
  onUserEnter,

  /// Callback for the exit of a remote user
  ///
  /// param:
  ///
  /// userId User ID
  ///
  /// reason Reason for exiting the room. 0: the user proactively exited the room; 1: the user exited the room due to timeout; 2: the user was kicked out of the room.
  onUserLeave,

  /*
  * Another attendee invited a user to an IM group call.
  * For example, if A, B, and C are in an IM group, and A calls D and E, B and C will receive callbacks from D and E.
  * At this point, if A invites F to the group chat, B and C will receive callbacks from D, E, and F.
  * @param userIdList Invitee group
  */
  onGroupCallInviteeListUpdate,

  /*
  * A call invitation was received.
  * @param sponsor Inviter
  * @param userIdList Users invited to the same call
  * @param isFromGroup Whether it is an IM group invitation
  * @param callType Call type. 1: Audio; 2: Video
  */
  onInvited,

  /*
   * 1. In a one-to-one call, only the caller will receive the rejection callback.
   * For example, if A calls B and C, and B rejects the call, A receives the callback but C does not.
   *
   * 2. In an IM group call, all invitees can receive this callback.
   * For example, if A calls B and C, and B rejects the call, both A and C can receive the callback.
   * @param userId User rejecting the call
   */
  onReject,

  /*
    * 1 In a one-to-one call, only the caller will receive the callback for no users answering the call.
    * For example, if A calls B and C, but B doesn't answer the call, A receives the callback but C does not.
    *
    * 2. In an IM group call, all invitees can receive this callback.
    * For example, if A calls B and C, but B doesn't answer the call, both A and C can receive the callback.
    * @param userId
    */
  onNoResp,

  /*
   * The invitee is busy
   * @param userId Busy user
   */
  onLineBusy,

  /*
   * If this callback is received by the invitee, the call was canceled.
   */
  onCallingCancel,

  /*
  * If this callback is received by the invitee, the call was not answered due to timeout.
  */
  onCallingTimeout,

  /*
  * This callback indicates that the current call was ended.
  */
  onCallEnd,

  /// Callback of whether a remote user has playable video in the primary stream (usually used for camera video)
  ///
  /// The `onUserVideoAvailable(userId, true)` callback indicates that the user has playable video frames. You can call `startRemoteView(userid)` to load the user’s video, and will receive the `onFirstVideoFrame(userid)` callback, which indicates that the first video frame has been rendered.
  ///
  /// The `onUserVideoAvailable(userId, false)` callback indicates that the remote user has disabled video. It may be because the user called `muteLocalVideo()` or `stopLocalPreview()`.
  ///
  /// param:
  ///
  /// userId User ID
  ///
  /// available Whether image is enabled
  onUserVideoAvailable,

  /// Callback of whether a remote user has playable video in the primary stream (usually used for camera video)
  ///
  /// The `onUserVideoAvailable(userId, true)` callback indicates that the user has playable video frames. You can call `startRemoteView(userid)` to load the user’s video, and will receive the `onFirstVideoFrame(userid)` callback, which indicates that the first video frame has been rendered.
  ///
  /// The `onUserVideoAvailable(userId, false)` callback indicates that the remote user has disabled video. It may be because the user called `muteLocalVideo()` or `stopLocalPreview()`.
  ///
  /// param:
  ///
  /// userId User ID
  ///
  /// available Whether image is enabled
  onUserAudioAvailable,

  /// Callback for volume, including the volume of each `userId` and total remote volume
  ///
  /// The `enableAudioVolumeEvaluation` API in `TRTCCloud` can be used to enable this callback or set its triggering interval. It should be noted that after `enableAudioVolumeEvaluation` is called to enable the volume callback, no matter whether there is a user speaking in the channel, the callback will be called at the set time interval. If there is no one speaking, `userVolumes` will be empty, and `totalVolume` will be `0`.
  ///
  /// Note: if `userId` is the local user ID, it indicates the volume of the local user. `userVolumes` only includes the volume information of users who are speaking (i.e., volume is not 0).
  ///
  /// param:
  ///
  /// userVolumes Volume of all members who are speaking in the room. Value range: 0–100.
  ///
  /// totalVolume Total volume of all remote members. Value range: 0–100.
  onUserVoiceVolume,

  // Callback for being kicked offline because another user logged in to the same account.
  onKickedOffline
```


## FAQs
### How do I customize the call UI?
TUICalling provides the one-to-one and group call features. To customize the call UI, you need to call the `enableCustomViewRoute` method to enable custom views, after which the audio/video call window will not be automatically opened after an audio/video call is received. You can call the `setCallingListener` method to set listeners for messages and room entry to implement invitation sending/receiving and audio/video calls. In addition, you can call `sharedInstance` to get the TRTCCalling instance, which provides TRTC capabilities such as camera enabling/disabling, mic enabling/disabling, hanging up, and answering.
