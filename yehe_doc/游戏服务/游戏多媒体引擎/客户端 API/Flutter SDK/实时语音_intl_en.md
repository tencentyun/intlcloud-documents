This document describes how to integrate with and debug GME client APIs for the real-time voice chat feature for Flutter.

## Key Considerations for Using GME

GME provides the real-time voice chat service, voice messaging and speech-to-text services, which all depend on core APIs such as `Init` and `Poll`.

#### Notes
- You have created a GME application and obtained the SDK `AppID` and key. For more information, see [Activating Services](https://www.tencentcloud.com/document/product/607/10782).

- You have activated **GME real-time voice chat, voice messaging and speech-to-text services**. For more information, see [Activating Services](https://www.tencentcloud.com/document/product/607/10782).

- Configure your project before using GME; otherwise, the SDK will not take effect.

- After a GME API is called successfully, `GmeError.AV_OK` will be returned with the value being `0`.

- GME APIs should be called in the same thread.

- The `Poll` API should be called periodically for GME to trigger event callbacks.

- For detailed error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223).


## Integrating the SDK

### Directions

Key processes involved in SDK integration are as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg)
1. [Initialize GME](https://www.tencentcloud.com/document/product/607/53818).

2. [Call `Poll` periodically to trigger event callbacks](https://www.tencentcloud.com/document/product/607/53818).

3. [Enter a voice chat room](https://www.tencentcloud.com/document/product/607/53818).

4. [Turn on the mic](https://www.tencentcloud.com/document/product/607/53818).

5. [Turn on the speaker](https://www.tencentcloud.com/document/product/607/53818).

6. [Exit the voice chat room](https://www.tencentcloud.com/document/product/607/53818).

7. [Uninitialize GME](https://www.tencentcloud.com/document/product/607/53818).


## Core APIs
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Init</td>

<td rowspan="1" colSpan="1" >Initializes GME.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Poll</td>

<td rowspan="1" colSpan="1" >Triggers the event callback.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Pause</td>

<td rowspan="1" colSpan="1" >Pauses the system.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Resume</td>

<td rowspan="1" colSpan="1" >Resumes the system.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Uninit</td>

<td rowspan="1" colSpan="1" >Uninitializes GME.</td>
</tr>
</table>


### Importing the GME module
``` bash
import 'package:gme/gme.dart';
import 'package:gme/gmeType.dart';
```

### Getting an instance

To use the voice chat feature, get the `GmeSDK` object first.
``` bash
ITMGContext context = ITMGContext.GetInstance();
```



### Initializing the SDK

**You need to initialize the SDK through the `Init` API** before you can use the real-time voice, voice message, and speech-to-text services. The `Init` API must be called in the same thread as other APIs. We recommend you call all APIs in the main thread.

#### API prototype
``` bash
//class ITMGContext
Future<int> InitSDK(String appID, String openID)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sdkAppId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`AppID` provided in the <a href="https://console.cloud.tencent.com/gamegme">GME console</a>, which can be obtained as instructed in <a href="https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0">Activating Services</a>.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`openID` can only be in `int64` type, which is passed in after being converted to a string. You can customize its rules, and it must be unique in the application. To pass in `openID` as a string, <a href="https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1">submit a ticket</a> for application.</td>
</tr>
</table>


#### Returned values
<table>
<tr>
<td rowspan="1" colSpan="1" >Returned Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GmeError.AV_OK= 0</td>

<td rowspan="1" colSpan="1" >SDK initialized successfully.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AV_ERR_SDK_NOT_FULL_UPDATE=7015</td>

<td rowspan="1" colSpan="1" >Solution: Check whether the SDK file is complete. We recommend that you delete it and then import the SDK again.</td>
</tr>
</table>


>! **Notes on 7015 error code**
> 
> - The 7015 error code is identified by MD5. If this error is reported during integration, check the integrity and version of the SDK file as prompted.
> - The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.
> - Due to the third-party enhancement, the Unity packaging mechanism, and other factors, the MD5 value of the library file will be affected, resulting in misjudgment. Therefore, **ignore this error in the logic for official releases**, and avoid displaying it on the UI.


#### Sample code
``` bash
string SDKAPPID3RD = "14000xxxxx";
string openId="10001";
int res = await ITMGContext.GetInstance().InitSDK(SDKAPPID3RD, openId);

if (ret != GmeError.AV_OK)
{
    print("Init SDK Error");
    return;
}
```

### Setting callbacks

The API class uses the `Delegate` method to send callback notifications to the application. Register the callback function to the SDK for receiving callback messages before room entry.

#### Function prototype and sample code

Register the callback function to the SDK for receiving callback messages before room entry.
``` bash
// When initializing the SDK
ITMGContext.GetInstance().SetEvent(handleEventMsg);
// Callback method
void handleEventMsg(int eventType, String data) async {
    // enterRoom event
    print("AddDelegate3" + eventType.toString());
    switch (eventType) {
      case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
        // Callback of room entry	
        }
        break;
      case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE:
        {
         // Callback of room switch
        }
        break;
    }
}
```

### Triggering event callback

You need to periodically call the `Poll` API to trigger event callbacks. The `Poll` API is GME's message pump and should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run abnormally. For more information, see the `EnginePollHelper` file in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).

>? **Call the `Poll` API periodically**
> 
> The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
> 


#### API prototype
``` bash
Future<void> Poll();
```

#### Sample code
``` bash
  Future<void> pollTimer() async {_pollTimer = Timer.periodic(Duration(milliseconds: 100), (Timer timer) {
      ITMGContext.GetInstance().Poll();
    });
  }
```

### Pausing the system

When a `Pause` event occurs in the system, the engine should also be notified for pause. For example, when the application switches to the background (OnApplicationPause, isPause=True), and you do not need the background to play back the audio in the room, please call `Pause` API to pause the GME service.

#### API prototype
``` bash
Future<int> Pause()
```

### Resuming the system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### API prototype
``` bash
Future<int> Resume()
```

### Uninitializing SDK

This API is used to uninitialize the SDK. **If the game business account is bound to `openid`, switching game account requires uninitializing GME and then using the new `openid` to initialize again.**

#### API prototype
``` bash
Future<int> Uninit()
```

## Voice Chat Room APIs

You should initialize and call the SDK to enter a room before voice chat can start.
If you have any questions when using the service, see [Sound and Audio](https://intl.cloud.tencent.com/document/product/607/39524).

![](https://qcloudimg.tencent-cloud.cn/raw/02f98895d0b7bfe1bac774d5983289c1.jpg)
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GenAuthBuffer</td>

<td rowspan="1" colSpan="1" >Calculates the local authentication key.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnterRoom</td>

<td rowspan="1" colSpan="1" >Enters a room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ExitRoom</td>

<td rowspan="1" colSpan="1" >Exits a room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsRoomEntered</td>

<td rowspan="1" colSpan="1" >Determines whether room entry is successful.</td>
</tr>
</table>


### Local authentication key calculation

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, use the backend deployment key as detailed in [Authentication Key](https://www.tencentcloud.com/document/product/607/12218).    

#### API prototype
``` bash
Future<Uint8List> GenAuthBuffer(String appID, String roomID, String openID, String key)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >appID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`AppID` from the Tencent Cloud console</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Room ID, which can contain up to 127 characters.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >User ID, which is the same as `openID` during initialization.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >key</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Permission key from the Tencent Cloud <a href="https://console.cloud.tencent.com/gamegme">console</a>.</td>
</tr>
</table>


#### Sample code
``` bash
 Uint8List userSig = await ITMGContext.GetInstance().GenAuthBuffer(_editAppID.text, _editRoomID.text, _editOpenID.text, _editKey.text);
 int res = await ITMGContext.GetInstance().EnterRoom(_editRoomID.text, 1, userSig);
```

### Entering a room

This API is used to enter a room with the generated authentication information. The mic and speaker are not enabled by default after room entry.

>!
> 
> - If the room entry callback result is `0`, the room entry is successful. If `0` is returned from the `EnterRoom` API, it doesn't necessarily mean that the room entry is successful.
> - The audio type of the room is determined by the first user entering the room. After that, if a member in the room changes the room type, it will take effect for all members there. For example, if the first user entering the room uses the smooth sound quality, and the second user entering the room uses the HD sound quality, the room audio type of the second user will change to the smooth sound quality. Only after a member in the room calls the `ChangeRoomType` API will the audio type of the room be changed.


#### API prototype
``` bash
Future<int> EnterRoom(String roomID, int roomType, Uint8List authBuffer)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Room ID, which can contain up to 127 characters.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomType</td>

<td rowspan="1" colSpan="1" >ITMGRoomType</td>

<td rowspan="1" colSpan="1" >Room type. We recommend that you select `ITMG_ROOM_TYPE_FLUENCY` for games. For more information on room audio types, see <a href="https://intl.cloud.tencent.com/document/product/607/18522">Sound Quality</a>.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >appKey</td>

<td rowspan="1" colSpan="1" >Uint8List</td>

<td rowspan="1" colSpan="1" >Authentication key</td>
</tr>
</table>


#### Sample code
``` bash
int res = await ITMGContext.GetInstance().EnterRoom(_editRoomID.text, 1, authBuffer);
```

### Callback for room entry

After the user enters the room, the `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` event type will be called back to notify the room entry result, which can be listened on for processing. A successful callback means that the room entry is successful, and the billing **starts**.

>! **Billing references:**
> 
> - [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009)
> - [Billing](https://intl.cloud.tencent.com/document/product/607/30255)
> - [Will the billing continue if the client is disconnected from the server when using the voice chat?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)


#### Sample code
``` bash
// Listen on an event:
void handleEventMsg(int eventType, String data) async {
  switch (eventType) {
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
      {
        // The process after room entry
      }
  }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

#### Data details
<table>
<tr>
<td rowspan="1" colSpan="1" >Message</td>

<td rowspan="1" colSpan="1" >Data</td>

<td rowspan="1" colSpan="1" >Sample</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ENTER_ROOM</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"waiting timeout, please check your network","result":0}</td>
</tr>
</table>


If the network is disconnected, there will be a disconnection callback notification `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`. At this time, the SDK will automatically reconnect, and the callback is `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`. When the reconnection is successful, there will be a callback `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS`.

#### Error codes
<table>
<tr>
<td rowspan="1" colSpan="1" >Error Code</td>

<td rowspan="1" colSpan="1" >Cause and Solution</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >7006</td>

<td rowspan="1" colSpan="1" >Authentication failed. Possible causes: <br>- The `AppID` does not exist or is incorrect.<br>- An error occurred while authenticating the `authbuff`.<br>- Authentication expired.<br>- The `OpenId` does not meet the specification.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >7007</td>

<td rowspan="1" colSpan="1" >The user was already in another room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >1001</td>

<td rowspan="1" colSpan="1" >The user was already in the process of entering a room but repeated this operation. We recommend that you not call the room entering API until the room entry callback is returned.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >1003</td>

<td rowspan="1" colSpan="1" >The user was already in the room and called the room entering API again.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >1101</td>

<td rowspan="1" colSpan="1" >Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally.</td>
</tr>
</table>


### Exiting a room

This API is used to exit the current room. It is an async API. The returned value `AV_OK` indicates a successful async delivery. If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API; instead, you can directly call the `EnterRoom` API.

#### API prototype
``` bash
Future<int> ExitRoom()
```

#### Sample code
``` bash
ITMGContext.GetInstance().ExitRoom();
```

#### Callback for room exit

After the user exits a room, a callback will be returned with the message being `ITMG_MAIN_EVENT_TYPE_EXIT_ROOM`. The sample code is shown below:

#### Sample code
``` bash
void handleEventMsg(int eventType, String data) async{
  switch (eventType) {
      case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
      {
      // The process after room exit
        break;
      }
  }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

### Determining whether user has entered room

This API is used to determine whether the user has entered a room. A value in bool type will be returned. Do not call this API during room entry.

#### API prototype
``` bash
Future<bool> IsRoomEntered()
```

#### Sample code
``` bash
bool res = await ITMGContext.GetInstance().IsRoomEntered();
```

## Room Status Maintenance

APIs in this section are used to display speaking members and members entering or exiting the room and mute a member in the room at the business layer.

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)
<table>
<tr>
<td rowspan="1" colSpan="1" >API/Notification</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_USER_UPDATE</td>

<td rowspan="1" colSpan="1" >The member status changed.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AddAudioBlackList</td>

<td rowspan="1" colSpan="1" >Mutes a member in the room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >RemoveAudioBlackList</td>

<td rowspan="1" colSpan="1" >Unmutes a user.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsOpenIdInAudioBlackList</td>

<td rowspan="1" colSpan="1" >Queries whether the user of the specified `openid` is muted.</td>
</tr>
</table>


### Notification events of member room entry and speaking status
- This event is used to get speaking users in the room and display the users on the UI, and to send a notification when someone enters or exits the room.

- A notification for this event will be sent only when the status changes. To get the member status in real time, cache the notification when it is received at the business layer. The event message `ITMG_MAIN_EVNET_TYPE_USER_UPDATE` containing `event_id`, `count`, and `openIdList` will be returned, which will be identified in the `OnEvent` notification.

- Notifications of the `EVENT_ID_ENDPOINT_NO_AUDIO` audio event will be sent only when the threshold is exceeded, that is, other members in the room can receive the notification that the local user stops speaking only after the local client captures no voice for two seconds.

- The audio event returns only the member speaking status but not the specific volume level. If you need the specific volume levels of members in the room, you can use the `GetVolumeById` API.

<table>
<tr>
<td rowspan="1" colSpan="1" >event_id</td>

<td rowspan="1" colSpan="1" >Description</td>

<td rowspan="1" colSpan="1" >Maintenance</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EVENT_ID_ENDPOINT_ENTER</td>

<td rowspan="1" colSpan="1" >Return the `openid` of the member entering the room.</td>

<td rowspan="1" colSpan="1" >Member list</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EVENT_ID_ENDPOINT_EXIT</td>

<td rowspan="1" colSpan="1" >Return the `openid` of the member exiting the room.</td>

<td rowspan="1" colSpan="1" >Member list</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EVENT_ID_ENDPOINT_HAS_AUDIO</td>

<td rowspan="1" colSpan="1" >Return the `openid` of the member sending audio packets in the room. This event can be used to determine whether a user is speaking and display the voiceprint effect.</td>

<td rowspan="1" colSpan="1" >Chat member list</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EVENT_ID_ENDPOINT_NO_AUDIO</td>

<td rowspan="1" colSpan="1" >Return the `openid` of the member stopping sending audio packets in the room.</td>

<td rowspan="1" colSpan="1" >Chat member list</td>
</tr>
</table>


#### Sample code
``` bash
void handleEventMsg(int eventType, String data) async {
  if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
  {
               // Process
            switch (eventID)
             {
             case EVENT_ID_ENDPOINT_ENTER:
                  // A member enters the room
                  break;
             case EVENT_ID_ENDPOINT_EXIT:
                  // A member exits the room
                break;
            case EVENT_ID_ENDPOINT_HAS_AUDIO:
                // A member sends audio packets
                break;
            case EVENT_ID_ENDPOINT_NO_AUDIO:
                // A member stops sending audio packets
                break;

            default:
                break;
             }
        break;
  }
}
```

### Muting a member in the room

This API is used to add an ID to the audio data blocklist. This operation blocks audio from someone and only applies to the local device without affecting other devices. The returned value `0` indicates that the call is successful. Assume that users A, B, and C are all speaking using their mic in a room: 
- If A blocks C, A can only hear B;

- If B blocks neither A nor C, B can hear both of them;

- If C blocks neither A nor B, C can hear both of them.


   This API is suitable for scenarios where a user is muted in a room.


#### API prototype
``` bash
Future<int> AddAudioBlackList(String openID) 
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`openid` of the user to be blocked</td>
</tr>
</table>


#### Sample code
``` bash
res = await ITMGContext.GetInstance().GetAudioCtrl().AddAudioBlackList(_editRoomManagerID.text);
```

### Unmuting

This API is used to remove an ID from the audio data blocklist. A returned value of 0 indicates the call is successful.

#### API prototype
``` bash
Future<int> RemoveAudioBlackList(String openID)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >ID to be unblocked</td>
</tr>
</table>


#### Sample code
``` bash
res = await ITMGContext.GetInstance().GetAudioCtrl().RemoveAudioBlackList(_editRoomManagerID.text);
```

## Voice Chat Capturing APIs
- The voice chat APIs can only be called after SDK initialization and room entry.

- When the user clicks the button of enabling/disabling the mic or speaker on the UI, we recommend you call the `EnableMic` or `EnableSpeaker` API.

- To enable the user to press the mic button on the UI to speak and release it to stop speaking, we recommend you call `EnableAudioCaptureDevice` once during room entry and call `EnableAudioSend` to enable the user to speak while pressing the button.

<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableMic</td>

<td rowspan="1" colSpan="1" >Enables/Disables the mic.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetMicState</td>

<td rowspan="1" colSpan="1" >Gets the mic status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableAudioCaptureDevice</td>

<td rowspan="1" colSpan="1" >Enables/Disables the capturing device.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsAudioCaptureDeviceEnabled</td>

<td rowspan="1" colSpan="1" >Gets the capturing device status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableAudioSend</td>

<td rowspan="1" colSpan="1" >Enables/Disables audio upstreaming.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsAudioSendEnabled</td>

<td rowspan="1" colSpan="1" >Gets the audio upstreaming status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetMicLevel</td>

<td rowspan="1" colSpan="1" >Gets the real-time mic volume level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSendStreamLevel</td>

<td rowspan="1" colSpan="1" >Gets the real-time audio upstreaming volume level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SetMicVolume</td>

<td rowspan="1" colSpan="1" >Sets the mic volume level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetMicVolume</td>

<td rowspan="1" colSpan="1" >Gets the mic volume level.</td>
</tr>
</table>




### Enabling or disabling mic

This API is used to enable/disable the mic. The mic and speaker are not enabled by default after room entry. **EnableMic = EnableAudioCaptureDevice + EnableAudioSend**

#### API prototype
``` bash
Future<int> EnableMic(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isEnabled</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >To enable the mic, set this parameter to `true`; otherwise, set it to `false`.</td>
</tr>
</table>


#### Sample code
``` bash
// Turn on mic
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```

### Getting the mic status

This API is used to get the mic status. The returned value 0 indicates that the mic is off, while 1 is on.

#### API prototype
``` bash
Future<int> GetMicState()
```

#### Sample code
``` bash
int micState = await ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### Enabling or disabling capturing device

This API is used to enable/disable a capturing device. The device is not enabled by default after room entry.
- This API can only be called after room entry. The device will be disabled automatically after room exit.

- Operations such as permission application and volume type adjustment will generally be performed when a capturing device is enabled on a mobile device.


#### API prototype
``` bash
Future<int> EnableAudioCaptureDevice(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >To enable the capturing device, set this parameter to `true`, otherwise, set it to `false`.</td>
</tr>
</table>


#### Sample code
``` bash
// Enable capturing device
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### Getting the capturing device status

This API is used to get the status of a capturing device.

#### API prototype
``` bash
Future<bool> IsAudioCaptureDeviceEnabled()
```

#### Sample code
``` bash
bool res = await ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### Enabling or disabling audio upstreaming

This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, see the `EnableAudioCaptureDevice` API.

#### API prototype
``` bash
Future<int> EnableAudioSend(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isEnabled</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >To enable audio upstreaming, set this parameter to `true`; otherwise, set it to `false`.</td>
</tr>
</table>


#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(isCheck);
```

### Getting audio upstreaming status

This API is used to get the status of audio upstreaming.

#### API prototype
``` bash
Future<bool> IsAudioSendEnabled() 
```

#### Sample code
``` bash
bool IsAudioSend = await ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();
```

### Getting the real-time mic volume

This API is used to get the real-time mic volume level. A number-type value in the range of 0–100 will be returned. We recommend that you call this API once every 20 ms.

#### API prototype
``` bash
Future<int> GetMicLevel()
```

#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### Getting the real-time audio upstreaming volume

This API is used to get the local real-time audio upstreaming volume level. A number-type value in the range of 0–100 will be returned.

#### API prototype
``` bash
Future<int> GetSendStreamLevel()
```

#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();
```

### Setting the mic software volume

This API is used to set the mic volume level. The corresponding parameter is `volume`, which is equivalent to attenuating or gaining the captured sound.

#### API prototype
``` bash
 Future<int> SetMicVolume(int volume)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >Value range: 0–200. Default value: `100`. `0` indicates that the audio is mute, while `100` indicates that the volume level remains unchanged.</td>
</tr>
</table>


#### Sample code
``` bash
int volume = 100;
int res = await ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume(volume);
```

### Getting the mic software volume

This API is used to get the mic volume level. A number-type value will be returned. `101` indicates that the `SetMicVolume` API has not been called.

#### API prototype
``` bash
Future<int> GetMicVolume()
```

#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();
```

## Voice Chat Playback APIs
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableSpeaker</td>

<td rowspan="1" colSpan="1" >Enables/Disables the speaker.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSpeakerState</td>

<td rowspan="1" colSpan="1" >Gets the speaker status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableAudioPlayDevice</td>

<td rowspan="1" colSpan="1" >Enables/Disables the playback device.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsAudioPlayDeviceEnabled</td>

<td rowspan="1" colSpan="1" >Gets the playback device status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableAudioRecv</td>

<td rowspan="1" colSpan="1" >Enables/Disables audio downstreaming.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsAudioRecvEnabled</td>

<td rowspan="1" colSpan="1" >Gets the audio downstreaming status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSpeakerLevel</td>

<td rowspan="1" colSpan="1" >Gets the real-time speaker volume level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetRecvStreamLevel</td>

<td rowspan="1" colSpan="1" >Gets the real-time downstreaming audio levels of other members in the room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SetSpeakerVolume</td>

<td rowspan="1" colSpan="1" >Sets the speaker volume level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSpeakerVolume</td>

<td rowspan="1" colSpan="1" >Gets the speaker volume level.</td>
</tr>
</table>




### Enabling or disabling speaker

This API is used to enable/disable the speaker. **EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**

#### API prototype
``` bash
Future<int> EnableSpeaker(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >bEnable</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >To disable the speaker, set this parameter to `false`; otherwise, set it to `true`.</td>
</tr>
</table>


#### Sample code
``` bash
// Turn on the speaker
await ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(isCheck);
```

### Getting the speaker status

This API is used to get the speaker status. 0 indicates that the speaker is off, and 1 is on.

#### API prototype
``` bash
Future<int> GetSpeakerState() 
```

#### Sample code
``` bash
int spkState = await ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```

### Enabling or disabling playback device

This API is used to enable/disable a playback device.

#### API prototype
``` bash
Future<int> EnableAudioPlayDevice(bool enable) 
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >To disable the playback device, set this parameter to `false`; otherwise, set it to `true`.</td>
</tr>
</table>


#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(isCheck);
```

### Getting the playback device status

This API is used to get the status of a playback device.

#### API prototype
``` bash
Future<bool> IsAudioPlayDeviceEnabled()
```

#### Sample code
``` bash
bool res = await ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### Enabling or disabling audio downstreaming

This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, see the `EnableAudioPlayDevice` API.

#### API prototype
``` bash
Future<int> EnableAudioRecv(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isEnabled</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" > To enable audio downstreaming, set this parameter to `true`; otherwise, set it to `false`.</td>
</tr>
</table>


#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(isCheck);
```

### Getting audio downstreaming status

This API is used to get the status of audio downstreaming.

#### API prototype
``` bash
Future<bool> IsAudioRecvEnabled() 
```

#### Sample code
``` bash
bool res = await ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```

### Getting the real-time speaker volume

This API is used to get the real-time speaker volume level. A number-type value will be returned to indicate the volume level. We recommend that you call this API once every 20 ms.

#### API prototype
``` bash
Future<int> GetSpeakerLevel()
```

#### Sample code
``` bash
bool res = await ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();
```

### Getting the real-time downstreaming audio levels of other members in room

This API is used to get the real-time audio downstreaming volume of other members in the room. A number-type value will be returned. Value range: 0–200.

#### API prototype
``` bash
Future<int> GetRecvStreamLevel(String openID)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`openId` of another member in the room</td>
</tr>
</table>


#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetRecvStreamLevel(_editRoomManagerID.text);
```

### Dynamically setting the volume of a member of the room

This API is used to set the volume of a member in the room. It takes effect only on the local.

#### API prototype
``` bash
Future<int> SetSpeakerVolumeByOpenID(String openId, int volume)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`OpenID` of the target user</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >Percentage. Recommended value range: 0-200. Default value: `100`.</td>
</tr>
</table>


#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolumeByOpenID(_editRoomManagerID.text, 100);
```

### Getting volume percentage

This API is used to get the volume level set by `SetSpeakerVolumeByOpenID`.

#### API prototype
``` bash
Future<int> GetSpeakerVolumeByOpenID(String openId)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`OpenID` of the target user</td>
</tr>
</table>


#### Returned values

API returns volume percentage set by OpenID, where 100 is by default.

#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolumeByOpenID(_editRoomManagerID.text);
```

### Setting the speaker volume

This API is used to set the speaker volume.

#### API prototype
``` bash
Future<int> SetSpeakerVolume(int volume)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >Volume level. Value range: 0-200. Default value: `100`. `0` indicates that the audio is mute, while `100` indicates that the volume level remains unchanged.</td>
</tr>
</table>


#### Sample code
``` bash
int volume = value.toInt();
int res = await ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(volume);
```

### Getting the speaker volume

This API is used to get the speaker volume. A number-type value will be returned to indicate the volume. `101` indicates that the `SetSpeakerVolume` API has not been called.
"Level" indicates the real-time volume, and "Volume" the speaker volume. The final volume = Level * Volume%. For example, if the "Level" is 100 and "Volume" is 60, the final volume is "60".

#### API prototype
``` bash
Future<int> GetSpeakerVolume() 
```

#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();
```

## Advanced APIs

### Enabling in-ear monitoring

This API is used to enable in-ear monitoring. You need to call `EnableLoopBack+EnableSpeaker` before you can hear your own voice.

#### API prototype
``` bash
Future<int> EnableLoopBack(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >Specifies whether to enable.</td>
</tr>
</table>


#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);
```

### Getting user's room audio type

This API is used to get a user's room audio type. The returned value is the room audio type. Value 0 indicates that an error occurred while getting the user's room audio type. For room audio types, see the `EnterRoom` API.

#### API prototype
``` bash
Future<int> GetRoomType()
```

#### Sample code
``` bash
int curType = await ITMGContext.GetInstance().GetRoom().GetRoomType();
```

### Changing the room type

This API is used to modify a user's room audio type. For the result, see the callback event. The event type is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE`. The audio type of the room is determined by the first user to enter the room. After that, if a member in the room changes the room type, it will take effect for all members there.

#### API prototype
``` bash
Future<int> ChangeRoomType(int roomType)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomtype</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >Room type to be switched to. For room audio types, see the `EnterRoom` API.</td>
</tr>
</table>


#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetRoom().ChangeRoomType(1);
```

#### Callback event

After the room type is set, the event message `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE` will be returned in the callback. The returned parameters include `result`, `error_info`, and `new_room_type`. The `new_room_type` represents the following information. The event message will be identified in the `OnEvent` function.
<table>
<tr>
<td rowspan="1" colSpan="1" >Event Subtype</td>

<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_ROOM_CHANGE_EVENT_ENTERROOM</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >Indicates that the existing audio type is inconsistent with and changed to that of the entered room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_ROOM_CHANGE_EVENT_START</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >Indicates that a user is already in the room and the audio type starts changing (e.g., calling the `ChangeRoomType` API to change the audio type).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_ROOM_CHANGE_EVENT_COMPLETE</td>

<td rowspan="1" colSpan="1" >3</td>

<td rowspan="1" colSpan="1" >Indicates that a user is already in the room and the audio type has been changed.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_ROOM_CHANGE_EVENT_REQUEST</td>

<td rowspan="1" colSpan="1" >4</td>

<td rowspan="1" colSpan="1" >Indicates that a room member calls the `ChangeRoomType` API to request a change of room audio type.</td>
</tr>
</table>


#### Sample code
``` bash
case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE:
  {
        // Process room type events
  }
  break;
```

### The monitoring event of room call quality

This is the quality monitoring event used to listen on the network quality. If your network conditions are poor, the business layer will ask you to switch the network through the UI. This event is triggered once every two seconds after room entry, and its message is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `loss`, and `delay`, which are as detailed below:
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >weight</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >Value range: 1–50. `50` indicates excellent sound quality, `1` indicates very poor (barely usable) sound quality, and `0` represents an initial meaningless value. Generally, if the value is below 30, you can remind users that the network is poor and recommend them to switch the network.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >loss</td>

<td rowspan="1" colSpan="1" >var</td>

<td rowspan="1" colSpan="1" >Upstream packet loss rate</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >delay</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >Voice chat delay in ms</td>
</tr>
</table>


### Getting version number

This API is used to get the SDK version number for analysis.

#### API prototype
``` bash
Future<String> GetSDKVersion()
```

#### Sample code
``` bash
_sdkVersions = await ITMGContext.GetInstance().GetSDKVersion();
```

### Setting the application name and version

This API is used to set the application name and version.

#### API prototype
``` bash
Future<void> SetAppVersion(String appVersion)
```

#### Parameter description
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >appVersion</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Application name and version</td>
</tr>
</table>


#### Sample code
``` bash
await ITMGContext.GetInstance().SetAppVersion("gme V2.0.0");
```

### Setting log printing level

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### API prototype
``` bash
Future<int> SetLogLevel(int levelWrite, int levelPrint)
```

#### Parameter description
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >Sets the log level. `TMG_LOG_LEVEL_NONE` indicates not to log. Default value: `TMG_LOG_LEVEL_INFO`.</td>
</tr>
</table>


`level` description:
<table>
<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_NONE</td>

<td rowspan="1" colSpan="1" >Does not print logs</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_ERROR</td>

<td rowspan="1" colSpan="1" >Prints error logs (default)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_INFO</td>

<td rowspan="1" colSpan="1" >Prints info logs</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_DEBUG</td>

<td rowspan="1" colSpan="1" >Prints debug logs</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_VERBOSE</td>

<td rowspan="1" colSpan="1" >Prints verbose logs</td>
</tr>
</table>


#### Sample code
``` bash
ITMGContext.GetInstance().SetLogLevel(ITMG_LOG_LEVEL.TMG_LOG_LEVEL_ERROR, ITMG_LOG_LEVEL.TMG_LOG_LEVEL_ERROR);
```

### Setting the log printing path

This API is used to set the log printing path. The default path is as follows. It needs to be called before Init.

#### API prototype
``` bash
Future<int> SetLogPath(String logDir)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >logPath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Path</td>
</tr>
</table>


#### Sample code
``` bash
String curPath = ""// Set a path by yourself
ITMGContext.GetInstance().SetLogPath(curPath);
```

### Getting the diagnostic messages

This API is used to get information on the quality of real-time audio/video calls, which is mainly used to view real-time call quality and troubleshoot and can be ignored on the business side.

#### API prototype
``` bash
Future<String> GetQualityTips()
```

#### Sample code
``` bash
String curQualityTips = await ITMGContext.GetInstance().GetRoom().GetQualityTips();
```

### Callback message
<table>
<tr>
<td rowspan="1" colSpan="1" >Message</td>

<td rowspan="1" colSpan="1" >Description</td>

<td rowspan="1" colSpan="1" >Data</td>

<td rowspan="1" colSpan="1" >Sample</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ENTER_ROOM</td>

<td rowspan="1" colSpan="1" >A member entered the audio room.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_EXIT_ROOM</td>

<td rowspan="1" colSpan="1" >A member exited the audio room.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT</td>

<td rowspan="1" colSpan="1" >The room was disconnected for network or other reasons.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"waiting timeout, please check your network","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_USER_UPDATE</td>

<td rowspan="1" colSpan="1" >Room members were updated.</td>

<td rowspan="1" colSpan="1" >user_list; event_id</td>

<td rowspan="1" colSpan="1" >{"event_id":1,"user_list":["0"]}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_RECONNECT_START</td>

<td rowspan="1" colSpan="1" >The reconnection to the room started.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS</td>

<td rowspan="1" colSpan="1" >The reconnection to the room succeeded.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM</td>

<td rowspan="1" colSpan="1" >The room was quickly switched.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE</td>

<td rowspan="1" colSpan="1" >The room status was changed.</td>

<td rowspan="1" colSpan="1" >result; error_info; sub_event_type; new_room_type</td>

<td rowspan="1" colSpan="1" >{"error_info":"","new_room_type":0,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_START</td>

<td rowspan="1" colSpan="1" >Cross-room mic connect started.</td>

<td rowspan="1" colSpan="1" >result;</td>

<td rowspan="1" colSpan="1" >{"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_STOP</td>

<td rowspan="1" colSpan="1" >Cross-room mic connect stopped.</td>

<td rowspan="1" colSpan="1" >result;</td>

<td rowspan="1" colSpan="1" >{"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_SPEAKER_DEFAULT_DEVICE_CHANGED</td>

<td rowspan="1" colSpan="1" >The default speaker device was changed.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE</td>

<td rowspan="1" colSpan="1" >A new speaker device was added.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE</td>

<td rowspan="1" colSpan="1" >A speaker device was lost.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE</td>

<td rowspan="1" colSpan="1" >A new mic device was added.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE</td>

<td rowspan="1" colSpan="1" >A mic device was lost.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_MIC_DEFAULT_DEVICE_CHANGED</td>

<td rowspan="1" colSpan="1" >The default mic device was changed.</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY</td>

<td rowspan="1" colSpan="1" >The room quality changed.</td>

<td rowspan="1" colSpan="1" >weight; loss; delay</td>

<td rowspan="1" colSpan="1" >{"weight":5,"loss":0.1,"delay":1}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE</td>

<td rowspan="1" colSpan="1" >Voice message recording was completed.</td>

<td rowspan="1" colSpan="1" >result; file_path</td>

<td rowspan="1" colSpan="1" >{"file_path":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE</td>

<td rowspan="1" colSpan="1" >Voice message upload was completed.</td>

<td rowspan="1" colSpan="1" >result; file_path;file_id</td>

<td rowspan="1" colSpan="1" >{"file_id":"","file_path":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE</td>

<td rowspan="1" colSpan="1" >Voice message download was completed.</td>

<td rowspan="1" colSpan="1" >result; file_path;file_id</td>

<td rowspan="1" colSpan="1" >{"file_id":"","file_path":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE</td>

<td rowspan="1" colSpan="1" >Voice message playback was completed.</td>

<td rowspan="1" colSpan="1" >result; file_path</td>

<td rowspan="1" colSpan="1" >{"file_path":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE</td>

<td rowspan="1" colSpan="1" >Fast speech-to-text conversion was completed.</td>

<td rowspan="1" colSpan="1" >result; text;file_id</td>

<td rowspan="1" colSpan="1" >{"file_id":"","text":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE</td>

<td rowspan="1" colSpan="1" >Streaming speech-to-text conversion was completed.</td>

<td rowspan="1" colSpan="1" >result; file_path; text;file_id</td>

<td rowspan="1" colSpan="1" >{{"file_id":"","file_path":","text":"","result":0}}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING</td>

<td rowspan="1" colSpan="1" >Streaming speech-to-text conversion is in progress.</td>

<td rowspan="1" colSpan="1" >result; file_path; text;file_id</td>

<td rowspan="1" colSpan="1" >{{"file_id":"","file_path":","text":"","result":0}}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_TEXT2SPEECH_COMPLETE</td>

<td rowspan="1" colSpan="1" >Text-to-speech conversion was completed.</td>

<td rowspan="1" colSpan="1" >result; text;file_id</td>

<td rowspan="1" colSpan="1" >{{"file_id":"","text":"","result":0}}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_TRANSLATE_TEXT_COMPLETE</td>

<td rowspan="1" colSpan="1" >Text translation was completed.</td>

<td rowspan="1" colSpan="1" >result; text;file_id</td>

<td rowspan="1" colSpan="1" >{{"file_id":"","text":"","result":0}}</td>
</tr>
</table>
