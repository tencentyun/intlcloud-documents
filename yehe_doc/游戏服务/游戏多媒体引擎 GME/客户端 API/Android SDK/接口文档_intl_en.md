This document describes how to access and debug GME APIs for Android.

>This document applies to GME SDK v2.5.

## Key Considerations for Using GME

| Important API | Description |
| ------------- |:-------------:|
|Init    | Initializes GME |
|Poll    | Triggers event callback |
|EnterRoom | Enters room  |
|EnableMic | Enables mic |
|EnableSpeaker | Enables speaker |

>
- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For GME callback messages, please see the callback message list.
- Operation on devices should be performed after successful room entry.
- For detailed error codes, please see [Error Codes](https://intl.cloud.tencent.com/document/product/607/15173).

## Voice Chat Flowchart
![](https://main.qcloudimg.com/raw/e536525aa47c06a5a84bb6c8d4851b22.png)

## Key APIs
Before the initialization, the SDK is in the uninitialized status, and you need to initialize it through the `Init` API before you can use the voice chat and voice messaging and speech-to-text features.
If you have any questions when using the service, please see [General FAQs](https://intl.cloud.tencent.com/document/product/607/30254).

| API | Description |
| ------------- |:-------------:|
|Init    | Initializes GME |
|Poll    | Triggers event callback |
|Pause   | Pauses system |
|Resume | Resumes system |
|Uninit    | Uninitializes GME |


### Getting a singleton
To use the voice feature, get the `ITMGContext` object first.
#### Function prototype

```
public static ITMGContext GetInstance(Context context)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| context | Context | Application context object |


#### Sample code 

```
import com.tencent.TMG.ITMGContext;
TMGContext.getInstance(this);
```

### Registering callback
The API class uses the `Delegate` method to send callback notifications to the application. Register the callback function to the SDK to receive callback messages.

#### Sample code
```
private ITMGContext.ITMGDelegate itmgDelegate = null;
```
Override this callback function in the constructor to process the parameters of the callback.

| Parameter | Type | Description |
| ------------- |:-------------:| ------------- |
| type    |ITMGContext.ITMG_MAIN_EVENT_TYPE | Event type in the callback response |
| data    | Intent message type | Callback message, i.e., event data |



#### Sample code 
```
itmgDelegate= new ITMGContext.ITMGDelegate() {
            @Override
  public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
                }
        };
```


Register the callback function to the SDK before room entry.
#### Function prototype
```
ITMGContext public int SetTMGDelegate(ITMGDelegate delegate)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| delegate    | ITMGDelegate | SDK callback function |

#### Sample code 
```
TMGContext.GetInstance(this).SetTMGDelegate(itmgDelegate);
```



### Initializing the SDK

For more information on how to get parameters, please see [Access Guide](https://intl.cloud.tencent.com/document/product/607/10782).
This API requires the `AppID` from the Tencent Cloud Console and the `openID` as parameters. The `openID` uniquely identifies a user with the rules stipulated by the application developer and must be unique in the application (currently, only INT64 is supported).

>The SDK must be initialized so that a room can be entered.
#### Function prototype

```
ITMGContext public int Init(String sdkAppId, String openId)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId    |String  | `AppId` from the Tencent Cloud Console. |
| openID    |String  | `OpenID` can only be in Int64 type (converted to string) with a value greater than 10,000, which is used to identify the user. |


| Returned Value | Description |
|----|----|
|QAVError.OK= 0| Initialized SDK successfully. |
|AV_ERR_SDK_NOT_FULL_UPDATE=7015| Check whether the SDK file is complete. You are recommended to delete it and then import the SDK again. |

#### Sample code


```
ITMGContext.GetInstance(this).Init(sdkAppId, openId);
```
### Triggering event callback
The `Poll` API in `updated` should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will not work properly.
#### Function prototype

```
ITMGContext int Poll()
```
#### Sample code
```
ITMGContext.GetInstance(this).Poll();
```

### Pausing the system
When a `Pause` event occurs in the system, the engine should be notified too for pause.
#### Function prototype

```
ITMGContext int Pause()
```

### Resuming the system
When a `Resume` event occurs in the system, the engine should be notified too for resumption. The `Resume` API only supports resuming voice chat.
#### Function prototype

```
ITMGContext int Resume()
```



### Uninitializing the SDK
This API is used to uninitialize the SDK to make it uninitialized. Switching accounts requires uninitialization.
#### Function prototype

```
ITMGContext int Uninit()
```


## Voice Chat Room Call Flowchart

![](https://main.qcloudimg.com/raw/a61ca1d7cdecf09bd223766b2a5cd69f.png)

## Voice Chat Room APIs
You should initialize and call the SDK to enter a room before voice chat can start.
If you have any questions when using the service, please see [FAQs About Voice Chat](https://intl.cloud.tencent.com/document/product/607/30257).
 
| API | Description |
| ------------- |:-------------:|
|GenAuthBuffer    | Initializes authentication |
| EnterRoom | Enters room |
|IsRoomEntered   | Indicates whether room entry is successful |
|ExitRoom | Exits room |
|ChangeRoomType | Modifies user's room audio type |
|GetRoomType | Gets user's room audio type |


### Authentication information
Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).   
To get authentication for voice messaging and speech-to-text, the room ID parameter must be set to `null`.

#### Function prototype
```
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String identifier, String key)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| appId    |int   | `AppId` from the Tencent Cloud Console. |
| roomId    |string   | Room ID, which can contain up to 127 characters (for voice messaging and speech-to-text feature, enter `null`). |
| openId    |string | User ID, which is the same as `openID` during initialization. |
| key    |string | Permission key from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme). |



#### Sample code 
```
import com.tencent.av.sig.AuthBuffer;// Header file
byte[] authBuffer=AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(sdkAppId), strRoomID,identifier, key);
```



### Entering a room
When a client enters a room with the generated authentication information, the `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` message will be received as a callback. Mic and speaker are not enabled by default after room entry. The returned value of `AV_OK` indicates a success.


#### Function prototype
```
ITMGContext public abstract int EnterRoom(String roomId, int roomType, byte[] authBuffer)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId |String | Room ID, which can contain up to 127 characters |
| roomType |int | Room audio type |
| authBuffer |byte[] | Authentication code |

For more information on how to choose a room audio type, please see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).


#### Sample code 
```
ITMGContext.GetInstance(this).EnterRoom(roomId,roomType, authBuffer);   
```

### Callback for room entry
After the client enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function.

```
private ITMGContext.ITMGDelegate itmgDelegate = null;
itmgDelegate= new ITMGContext.ITMGDelegate() {
            @Override
  public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
                }
        };
```
Sample code for processing the callback:
#### Sample code 
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           // Receive the event of successful room entry
        }
}
```

#### Data details
| Message | Data | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info |{"error_info":"","result":0}|

#### Error codes
| Error Code Value | Cause and Suggested Solution |
|--------|-------|------------|
|7006| Authentication failed. Possible causes: 1. The `AppID` does not exist or is incorrect; 2. An error occurred while authenticating the `authbuff`; 3. Authentication expired; 4. The `openID` is non-compliant. |
|7007| Already in another room. |
|1001   | The client was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned. |
|1003   | The client was already in the room and called the room entering API again. |
|1101   | Ensure that the SDK is initialized, the APIs are called in the same thread, and the `Poll` API is called normally. |

### Determining whether client has entered room
This API is used to determine whether the client has entered a room. A bool-type value will be returned.
#### Function prototype 
```
ITMGContext public boolean IsRoomEntered()
```
#### Sample code 
```
ITMGContext.GetInstance(this).IsRoomEntered();
```

### Exiting a room
This API is called to exit the current room. It is an async API. The returned value of `AV_OK` indicates a successful async delivery.

>If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the API.

#### Function prototype 
```
ITMGContext public int ExitRoom()
```
#### Sample code 
```
ITMGContext.GetInstance(this).ExitRoom();
```

### Callback for room exit
After the client exits a room, a callback will be returned with the message being `ITMG_MAIN_EVENT_TYPE_EXIT_ROOM`.
#### Sample code 
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM == type)
        {
            // Receive the event of successful room exit
        }
}
```

#### Data details
| Message | Data | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|


### Modifying user's room audio type
This API is used to modify a user's room audio type. For the result, please see the callback event. The event type is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE`.
#### Function prototype 
```
IITMGContext TMGRoom public int ChangeRoomType(int nRoomType)
```


| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| nRoomType    | int    | Room type to be switched to. For room audio types, please see the `EnterRoom` API |

#### Sample code 
```
ITMGContext.GetInstance(this).GetRoom().ChangeRoomType(nRoomType);
```


### Getting user's room audio type
This API is used to get a user's room audio type. The returned value is the room audio type. Value 0 indicates that an error occurred while getting the user's room audio type. For room audio types, please see the `EnterRoom` API.

#### Function prototype 
```
IITMGContext TMGRoom public int GetRoomType()
```

#### Sample code 
```
ITMGContext.GetInstance(this).GetRoom().GetRoomType();
```


### Callback for room type setting completion
After the room type is set, the event message `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE` will be returned in the callback. The returned parameters include `result`, `error_info`, and `new_room_type`. The `new_room_type` represents the following information. The event message will be identified in the `OnEvent` function.

| Event Subtype | Parameter | Description |
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM|1 | Indicates that the existing audio type is inconsistent with and changed to that of the entered room|
| ITMG_ROOM_CHANGE_EVENT_START |2 | Indicates that a client is already in the room and the audio type starts changing (e.g., calling the `ChangeRoomType` API to change the audio type) |
| ITMG_ROOM_CHANGE_EVENT_COMPLETE |3 | Indicates that a client is already in the room and the audio type has been changed |
| ITMG_ROOM_CHANGE_EVENT_REQUEST |4 | Indicates that a room member calls the `ChangeRoomType` API to request a change of room audio type |


#### Sample code 
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
// Process room type events
}
}
```

#### Data details
| Message | Data | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type |{"error_info":"","new_room_type":0,"result":0}|


### Member status change
Notification for this event will be sent only when the status changes. To get member status in real time, cache the notification when it is received at a higher layer. The event message is `ITMG_MAIN_EVNET_TYPE_USER_UPDATE`, where the data contains `event_id` and `user_list`. The event message will be identified in the `OnEvent` function.
Notifications for audio events are subject to a threshold, and a notification will be sent only when this threshold is exceeded. The notification "A member has stopped sending audio packets" will be sent if no audio packets are received in more than two seconds.

|event_id     | Description | Maintenance |
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    | A member enters the room | Member list |
|ITMG_EVENT_ID_USER_EXIT    | A member exits the room | Member list |
|ITMG_EVENT_ID_USER_HAS_AUDIO    | A member sends audio packets | Chat member list |
|ITMG_EVENT_ID_USER_NO_AUDIO    | A member stops sending audio packets | Chat member list |

#### Room member maintenance flowchart

![](https://main.qcloudimg.com/raw/50ef1ceda14eb244e434b8cbe85da5f3.png)


#### Sample code
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_USER_UPDATE == type)
        {
// Update member status
int nEventID = data.getIntExtra("event_id", 0);
String[] identifierList =data.getStringArrayExtra("user_list");
switch (nEventID)
      {
      case ITMG_EVENT_ID_USER_ENTER:
      // A member enters the room
      break;
      case ITMG_EVENT_ID_USER_EXIT:
      // A member exits the room
    break;
    case ITMG_EVENT_ID_USER_HAS_AUDIO:
    // A member sends audio packets
    break;
    case ITMG_EVENT_ID_USER_NO_AUDIO:
    // A member stops sending audio packets
    break;
    default:
    break;
      }
}
}
```

### Room call quality control event
The message for quality control event is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `floss`, and `delay`, which represent the following information. The event message will be identified in the `OnEvent` function.

| Parameter | Description |
| ------------- |-------------|
|weight    | Value range: 1–5. 5 indicates excellent sound quality, 1 indicates very poor (barely usable) sound quality, and 0 represents an initial meaningless value |
|floss    | Packet loss rate |
|delay    | Voice chat delay in ms |




### Message details

| Message | Description  
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM           | Indicates that a member enters an audio/video room |
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             | Indicates that a member exits an audio/video room |
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           | Indicates that a room is disconnected for network or other reasons |
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | Indicates a room type change event |

### Details of data corresponding to the message
| Message | Data | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info |{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    |result; error_info  |{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type |{"error_info":"","new_room_type":0,"result":0}|


## Voice Chat Audio APIs
The voice chat APIs can only be called after SDK initialization and room entry.
When Enable/Disable Mic/Speaker is tapped/clicked on the UI, the following practices are recommended:
- For most game applications, it is recommended to call the `EnableMic` and `EnableSpeaker` APIs, which is equivalent to calling the `EnableAudioCaptureDevice/EnableAudioSend` and `EnableAudioPlayDevice/EnableAudioRecv` APIs;
- For other mobile applications (such as social networking applications), enabling/disabling a capturing device will restart both capturing and playback devices. If the application is playing back background music, it will also be interrupted. Playback won't be interrupted if the mic is enabled/disabled through control of upstreaming/downstreaming. Calling method: call `EnableAudioCaptureDevice(true)` and `EnableAudioPlayDevice(true)` once after room entry, and call `EnableAudioSend/Recv` to send/receive audio streams when Enable/Disable Mic is tapped.
- For more information on how to release only a capturing or playback device, please see the `EnableAudioCaptureDevice` and `EnableAudioPlayDevice`.
- Call the `pause` API to pause the audio engine and call the `resume` API to resume the audio engine.

| API | Description |
| ------------- |:-------------:|
|EnableMic | Enables/disables mic |
|GetMicState    | Gets mic status |
|EnableAudioCaptureDevice    | Enables/disables capturing device |
|IsAudioCaptureDeviceEnabled    | Gets capturing device status |
|EnableAudioSend    | Enables/disables audio upstreaming |
|IsAudioSendEnabled    | Gets audio upstreaming status |
|GetMicLevel    | Gets real-time mic volume level|
|GetSendStreamLevel| Gets real-time audio upstreaming volume level |
|SetMicVolume    | Sets mic volume level |
|GetMicVolume    | Gets mic volume level |
|EnableSpeaker    | Enables/disables speaker |
|GetSpeakerState    | Gets speaker status |
|EnableAudioPlayDevice    | Enables/disables playback device |
|IsAudioPlayDeviceEnabled    | Gets playback device status |
|EnableAudioRecv    | Enables/disables audio downstreaming |
|IsAudioRecvEnabled    | Gets audio downstreaming status |
|GetSpeakerLevel    | Gets real-time speaker volume level |
|GetRecvStreamLevel | Gets real-time downstreaming audio levels of other members in room |
|SetSpeakerVolume    | Sets speaker volume level |
|GetSpeakerVolume    | Gets speaker volume level |
|EnableLoopBack    | Enables/disables in-ear monitoring |



### Enabling/Disabling the mic
This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
#### Function prototype 
```
ITMGContext public int EnableMic(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | To enable the mic, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code 
```
Enable the mic:
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
```

### Getting mic status
This API is used to get the mic status. The returned value 0 indicates that the mic is off, while 1 on.
#### Function prototype 
```
ITMGContext TMGAudioCtrl int GetMicState()
```
#### Sample code 
```
int micState = ITMGContext.GetInstance(this).GetAudioCtrl().GetMicState();
```

### Enabling/Disabling capture device
This API is used to enable/disable a capturing device. The device is not enabled by default after room entry.
- This API can only be called after room entry. The device will be disabled automatically after room exit.
- Operations such as permission application and volume type adjustment will generally be performed when a capturing device is enabled on a mobile device.

#### Function prototype 
```
ITMGContext public int EnableAudioCaptureDevice(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | To enable a capturing device, set this parameter to `true`; otherwise, set it to `false` |

#### Sample code

```
Enable a capturing device
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### Getting capturing device status
This API is used to get the status of a capturing device.
#### Function prototype

```
ITMGContext public boolean IsAudioCaptureDeviceEnabled()
```
#### Sample code

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### Enabling/Disabling audio upstreaming
This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, please see the `EnableAudioCaptureDevice` API.

#### Function prototype

```
ITMGContext public int EnableAudioSend(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | To enable audio upstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code 

```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioSend(true);
```

### Getting audio upstreaming status
This API is used to get the status of audio upstreaming.
#### Function prototype 
```
ITMGContext TMGAudioCtrl boolean IsAudioSendEnabled()
```
#### Sample code 
```
bool IsAudioSend = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioSendEnabled();
```

### Getting real-time mic volume level
This API is used to get the real-time mic volume level. An int-type value will be returned. It is recommended to call this API once every 20 ms.
#### Function prototype 
```
ITMGContext TMGAudioCtrl int GetMicLevel()
```
#### Sample code 
```
int micLevel = ITMGContext.GetInstance(this).GetAudioCtrl().GetMicLevel();
```

### Getting real-time audio upstreaming volume level
This API is used to get the real-time audio upstreaming volume level. An int-type value will be returned. Value range: 0–100.
#### Function prototype 
```
ITMGContext TMGAudioCtrl int GetSendStreamLevel()
```
#### Sample code 
```
int Level = ITMGContext.GetInstance(this).GetAudioCtrl().GetSendStreamLevel();
```

### Setting mic volume level
This API is used to set the mic volume level. The corresponding parameter is `volume`. 0 indicates that the audio is mute, while 100 indicates that the volume level remains unchanged. The default value is 100.

#### Function prototype 
```
ITMGContext TMGAudioCtrl int SetMicVolume(int volume)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume | int | Sets volume level. Value range: 0–200 |

#### Sample code 
```
ITMGContext.GetInstance(this).GetAudioCtrl().SetMicVolume(volume);
```
### Getting mic volume level
This API is used to get the mic volume level. An int-type value will be returned. 101 indicates that the `SetMicVolume` API has not been called.

#### Function prototype 
```
ITMGContext TMGAudioCtrl public int GetMicVolume()
```
#### Sample code 
```
ITMGContext.GetInstance(this).GetAudioCtrl().GetMicVolume();
```

### Enabling/Disabling the speaker
This API is used to enable/disable the speaker.
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
#### Function prototype 
```
ITMGContext public int EnableSpeaker(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       | To disable the speaker, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code 
```
Enable the speaker
ITMGContext.GetInstance(this).GetAudioCtrl().EnableSpeaker(true);
```

### Getting speaker status
This API is used to get the speaker status. 0 indicates that the speaker is off, 1 on, and 2 working.
#### Function prototype 
```
ITMGContext TMGAudioCtrl public int GetSpeakerState()
```

#### Sample code 
```
int micState = ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerState();
```



### Enabling/Disabling playback device
This API is used to enable/disable a playback device.

#### Function prototype 
```
ITMGContext public int EnableAudioPlayDevice(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       | To disable a playback device, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code 
```
Enable a playback device
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioPlayDevice(true);
```

### Getting playback device status
This API is used to get the status of a playback device.
#### Function prototype

```
ITMGContext public int IsAudioPlayDeviceEnabled()
```
#### Sample code 

```
bool IsAudioPlayDevice = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### Enabling/Disabling audio downstreaming
This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, please see the `EnableAudioPlayDevice` API.

#### Function prototype 

```
ITMGContext public int EnableAudioRecv(boolean isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | To enable audio downstreaming, set this parameter to `true`; otherwise, set it to `false` |

#### Sample code 

```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioRecv(true);
```



### Getting audio downstreaming status
This API is used to get the status of audio downstreaming.
#### Function prototype 
```
ITMGContext TMGAudioCtrl public boolean IsAudioRecvEnabled()
```

#### Sample code 
```
bool IsAudioRecv = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioRecvEnabled();
```

### Getting real-time speaker volume level
This API is used to get the real-time speaker volume level. An int-type value will be returned to indicate the volume level. It is recommended to call this API once every 20 ms.
#### Function prototype 
```
ITMGContext TMGAudioCtrl public int GetSpeakerLevel()
```

#### Sample code 
```
int SpeakLevel = ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerLevel();
```

### Getting real-time downstreaming audio levels of other members in room
This API is used to get the real-time audio downstreaming volume levels of other members in the room. An int-type value will be returned. Value range: 0–100.
#### Function prototype 
```
ITMGContext TMGAudioCtrl public int GetRecvStreamLevel(string openId)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| openId    |string    | `openId` of another member in the room |

#### Sample code 
```
int Level = ITMGContext.GetInstance(this).GetAudioCtrl().GetRecvStreamLevel(openId);
```

### Setting speaker volume level
This API is used to set the speaker volume level.
The corresponding parameter is `volume`. 0 indicates that the audio is mute, while 100 indicates that the volume level remains unchanged. The default value is 100.

#### Function prototype 
```
ITMGContext TMGAudioCtrl public int SetSpeakerVolume(int volume)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume | int | Sets volume level. Value range: 0–200 |

#### Sample code 
```
int speVol = (int)(value * 100);
ITMGContext.GetInstance(this).GetAudioCtrl().SetSpeakerVolume(volume);
```

### Getting speaker volume level

This API is used to get the speaker volume level. An int-type value will be returned to indicate the volume level. 101 indicates that the `SetSpeakerVolume` API has not been called.
`Level` indicates the real-time volume level, while `Volume` the speaker volume level. The final volume level equals to Level*Volume%. For example, if the value of "Level" is 100 and that of `Volume` is 60, then the final volume level will be 60.

#### Function prototype 
```
ITMGContext TMGAudioCtrl public int GetSpeakerVolume()
```
#### Sample code 
```
ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerVolume();
```


### Enabling in-ear monitoring
This API is used to enable in-ear monitoring.
#### Function prototype 
```
ITMGContext TMGAudioCtrl public int EnableLoopBack(boolean enable)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable    |boolean         | Specifies whether to enable |

#### Sample code 
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableLoopBack(true);
```


## Speech-to-Text Conversion Flowchart
<img src="https://main.qcloudimg.com/raw/310eaf2b780c5fc47ffeaf791a6df392.png" width="70%">



## Voice Messaging and Speech-to-Text
Before the initialization, the SDK is in the uninitialized status, and you need to initialize it through the `Init` API before you can use the voice chat and voice messaging and speech-to-text features.
If you have any questions when using the service, please see [FAQs About Voice Messaging and Speech-to-Text](https://intl.cloud.tencent.com/document/product/607/30258).


### Initialization APIs

| API | Description |
| ------------- |:-------------:|
|Init    | Initializes GME |
|Poll    | Triggers event callback |
|Pause   | Pauses system |
|Resume | Resumes system |
|Uninit    | Uninitializes GME |


### Voice messaging and speech-to-text APIs
| API | Description |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    | Initializes authentication |
|SetMaxMessageLength    | Specifies maximum length of voice message |
|StartRecording | Starts recording |
|StartRecordingWithStreamingRecognition | Starts streaming recording |
|PauseRecording| Pauses recording |
|ResumeRecording| Resumes recording |
|StopRecording    | Stops recording |
|CancelRecording | Cancels recording |
|GetMicLevel| Gets the real-time mic volume level of voice messaging |
|SetMicVolume| Sets the recording volume level of voice messaging |
|GetMicVolume| Gets the recording volume level of voice messaging |
|GetSpeakerLevel    | Gets the real-time speaker volume level of voice messaging |
|SetSpeakerVolume| Sets the playback volume level of voice messaging |
|GetSpeakerVolume| Gets the playback volume level of voice messaging |
|UploadRecordedFile | Uploads audio file |
|DownloadRecordedFile | Downloads audio file |
|PlayRecordedFile | Plays back audio |
|StopPlayFile | Stops playing back audio |
|GetFileSize | Gets audio file size|
|GetVoiceFileDuration| Gets audio file duration|
|SpeechToText | Converts speech to text |

### Authentication initialization
Call authentication initialization after initializing the SDK. For more information on how to get the `authBuffer`, please see the voice chat authentication information API.
#### Function prototype 
```
ITMGContext TMGPTT public int ApplyPTTAuthbuffer(String authBuffer)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| authBuffer | String | Authentication |

#### Sample code 
```
ITMGContext.GetInstance(this).GetPTT().ApplyPTTAuthbuffer(authBuffer);
```

### Spe
