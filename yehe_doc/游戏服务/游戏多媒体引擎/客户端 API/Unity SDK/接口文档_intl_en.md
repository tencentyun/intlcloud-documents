This document describes how to access and debug the GME APIs for Unity.

>?This document applies to GME SDK version 2.8.

## Key Considerations for Using GME

GME divides into two services: voice chat service and voice messaging and speech-to-text service.

![image](https://main.qcloudimg.com/raw/7a287c9cf60259eaea9469e110927462.png)

### Important APIs

| Important API | Description |
| ------------- | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| EnterRoom | Enters room (voice chat) |
| EnableMic | Enables mic (voice chat) |
| EnableSpeaker | Enables speaker (voice chat) |
| StartRecordingWithStreamingRecognition | Stream records audio and converts to text (voice messaging and speech-to-text) |

### Important notes
- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error codes, please see [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223).

### C# classes

| Class | Description |
| ------ | :----------: |
| ITMGContext | Key APIs |
| ITMGRoom | Room APIs |
| ITMGRoomManager | Room management APIs |
| ITMGAudioCtrl | Audio APIs |
| ITMGAudioEffectCtrl | Sound effect and accompaniment APIs |
| ITMGPTT | Voice messaging and speech-to-text APIs |

## Key APIs

Before the initialization, the SDK is in the uninitialized status, and you need to initialize it through the `Init` API before you can use the voice chat and voice messaging and speech-to-text services. **If you switch the account, please call `UnInit` to uninitialize the SDK.**

If you have any questions when using the service, please see [General FAQs](https://intl.cloud.tencent.com/document/product/607/30254).

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |

### Imported header files

```
using TencentMobileGaming;
```

### Getting an instance
Get the `Context` instance by using the `ITMGContext` method instead of `QAVContext.GetInstance()`.

### Initializing SDK
This API is used to initialize the GME service. It is recommended to call it when initializing the application.
**For more information on how to get the `sdkAppId` parameter, please see [Access Guide](https://intl.cloud.tencent.com/document/product/607/39698)**.
**The openID uniquely identifies a user with the rules stipulated by the application developer and must be greater than 10,000 and unique in the application (currently, only INT64 is supported)**.

> !The SDK must be initialized before an user can enter a voice chat room.

#### Function prototype

```
ITMGContext Init(string sdkAppID, string openID)
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | String | `AppId` provided by the GME service from the [Tencent Cloud Console](https://console.cloud.tencent.com/) |
| openID | String | `OpenID` can only be in Int64 type (converted to string) with **a value greater than 10,000; otherwise, initialization and room entry will fail**. |

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0 | Initialized SDK successfully |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is only a reminder but will not cause an initialization failure.

- If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- If this error is returned after executable file export, please ignore it and try to avoid displaying it in the UI.

#### Sample code 

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
// Determine whether the initialization is successful by the returned value
if (ret != QAVError.OK)
    {
        Debug.Log("SDK initialization failed:"+ret);
        return;
    }
```


### Triggering event callback

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
You can refer to the `EnginePollHelper` file in the demo.

#### Function prototype

```
ITMGContext public abstract int Poll();
```

#### Sample code

```
public void Update()
    {
        ITMGContext.GetInstance().Poll();
    }
```

### Pausing system

When a `Pause` event occurs in the system, the engine should also be notified for pause.

#### Function prototype

```
ITMGContext public abstract int Pause()
```

### Resuming system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### Function prototype

```
ITMGContext  public abstract int Resume()
```



### Uninitializing SDK

This API is used to uninitialize the SDK to make it uninitialized. **Switching accounts requires uninitialization**.

#### Function prototype

```
ITMGContext public abstract int Uninit()
```


## Voice Chat
Voice chat refers to the one-to-one or one-to-many real-time voice call feature.

### Voice chat flowchart

![](https://main.qcloudimg.com/raw/e536525aa47c06a5a84bb6c8d4851b22.png)



### Voice chat room call flowchart

![](https://main.qcloudimg.com/raw/a61ca1d7cdecf09bd223766b2a5cd69f.png)

## Voice Chat Room APIs

You should initialize and call the SDK to enter a room before voice chat can start.
If you have any questions when using the service, please see [FAQs About Voice Chat](https://intl.cloud.tencent.com/document/product/607/30257).


| API | Description |
| -------------- | :------------------: |
| GenAuthBuffer | Initializes authentication |
| EnterRoom | Enters room |
| IsRoomEntered | Indicates whether room entry is successful |
| ExitRoom | Exits room |
| ChangeRoomType | Modifies user's room audio type |
| GetRoomType | Gets user's room audio type |

### Authentication information

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    
To get authentication for voice messaging and speech-to-text, the room ID parameter must be set to `null`.

#### Function prototype

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)

```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| appId | int | `AppId` from the Tencent Cloud console. |
| roomId | string | Room ID, which can contain up to 127 characters (for the voice messaging and speech-to-text service, enter `null`). |
| openId | string | User ID, which is the same as `openID` during initialization. |
| key | string | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |



#### Sample code  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
        return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}
```



### Entering room

When a user enters a room with the generated authentication information, the `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` message will be received as a callback. Mic and speaker are not enabled by default after room entry. The returned value of `AV_OK` indicates a success.

For more information on how to access Range Voice, please see [Range Voice](https://intl.cloud.tencent.com/document/product/607/17972).
#### Function prototype

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```

| Parameter | Type | Description |
| ---------- | :----: | ----------------------- |
| roomId | string | Room ID, which can contain up to 127 characters. |
| roomType | ITMGRoomType | Room audio type |
| authBuffer | Byte[] | Authentication key |

For more information on how to choose a room audio type, please see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).

#### Sample code  

```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);

```

### Callback for room entry
A callback will be required through a delegate function after room entry, which is composed of `result` and `error_info`.
If there is no callback, please check whether the `Poll` function is called periodically.
#### Function prototype
```
Delegate function:
public delegate void QAVEnterRoomComplete(int result, string error_info);
Event function:
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```



#### Sample code  

```
Listen on an event:
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

Process the event listened on:
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
  			ShowLoginPanel("error code:" + err + " error message:" + errInfo);
            return;
	}else{
		// Entered room successfully
    }
}
```

#### Error codes

| Error Code Name | Error Code Value | Cause and Suggested Solution |
|--------|-------|------------|
| AV_ERR_AUTH_FIALD | 7006 | Authentication failed. Possible causes: 1. The `AppID` does not exist or is incorrect. 2. An error occurred while authenticating the `authbuff`. 3. Authentication expired. 4. The `openID` is non-compliant. |
| AV_ERR_IN_OTHER_ROOM | 7007 | Already in another room. |
| ERR_REPETITIVE_OPERATION | 1001 | The user was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned. |
| ERR_HAS_IN_THE_STATE | 1003 | The user was already in the room and called the room entering API again. |
| ERR_CONTEXT_NOT_START | 1101 | Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally. |

### Determining whether user has entered room

This API is used to determine whether the user has entered a room. A bool-type value will be returned.

#### Function prototype  

```
ITMGContext abstract bool IsRoomEntered()
```

#### Sample code  

```
ITMGContext.GetInstance().IsRoomEntered();
```

### Exiting room

This API is called to exit the current room. It is an async API. The returned value of `AV_OK` indicates a successful async delivery.

> !If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the API.

#### Function prototype  

```
ITMGContext ExitRoom()
```

#### Sample code  

```
ITMGContext.GetInstance().ExitRoom();
```

### Callback for room exit
A callback will be executed through a delegate function to pass a message after room exit.
#### Function prototype  
```
Delegate function:
public delegate void QAVExitRoomComplete();
Event function:
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent; 
```
#### Sample code  

```
Listen on an event:
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
Process the event listened on:
void OnExitRoomComplete(){
    // Send a callback after room exit
}
```

### Getting user's room audio type
This API is used to get a user's room audio type. The returned value is the room audio type. Value 0 indicates that an error occurred while getting the user's room audio type. For room audio types, please see the `EnterRoom` API.

#### Function prototype  

```
ITMGContext ITMGRoom public int GetRoomType()
```


#### Sample code  

```
ITMGContext.GetInstance().GetRoom().GetRoomType();
```

### Modifying user's room audio type
This API is used to modify user's room audio type.

#### Function prototype  

```
ITMGContext ITMGRoom public int ChangeRoomType(ITMGRoomType roomtype)
```


| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomtype | ITMGRoomType | Room type to be switched to. For room audio types, please see the `EnterRoom` API. |

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);

```

### Callback for modifying room audio type
Set the room type. After the room type is set, a callback will be executed through a delegate function to pass a message indicating that the modification has been completed.

| Returned Parameter | Description |
| ------------- |:-------------:|
| roomtype | Updated room type returned |


```
Delegate function:
public abstract event QAVCallback OnChangeRoomtypeCallback;

Event function:
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;
```

#### Sample code  

```
Listen on an event:
ITMGContext.GetInstance ().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent (OnRoomTypeChangedEvent);
Process the event listened on:
void OnRoomTypeChangedEvent(int roomtype)
{
        ShowWarnning (string.Format ("RoomTypeChanged current:{0}",roomtype));
}

```

### Notification of room type change
Once the room type is modified by you or another user in the room, this callback function will be called to notify the business layer of the room type change. The returned value will be the room type. For more information, please see the `EnterRoom` API.
```
Delegate function:
public delegate void QAVOnRoomTypeChangedEvent(int roomtype);

Event function:
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;	
```
#### Sample code  
```
Listen on an event:
ITMGContext.GetInstance().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent(OnRoomTypeChangedEvent);
Process the event listened on:
void OnRoomTypeChangedEvent(int roomtype){
    // Send a callback after the room type is changed
}
```



### Member status change
A notification for this event will be sent only when the status changes. To get member status in real time, cache the notification when it is received at the upper layer. The event message `ITMG_MAIN_EVNET_TYPE_USER_UPDATE` containing `event_id`, `count`, and `openIdList` will be returned. The event message will be identified in the `OnEvent` function.
Notifications for audio events are subject to a threshold, and a notification will be sent only when this threshold is exceeded. The notification "A member has stopped sending audio packets" will be sent if no audio packets are received in more than two seconds.


| event_id | Description | Maintenance |
| ------------- |:-------------:|-------------|
| EVENT_ID_ENDPOINT_ENTER | A member enters the room | Member list |
| EVENT_ID_ENDPOINT_EXIT | A member exits the room | Member list |
| EVENT_ID_ENDPOINT_HAS_AUDIO | A member sends audio packets | Chat member list |
| EVENT_ID_ENDPOINT_NO_AUDIO | A member stops sending audio packets | Chat member list |

#### Room member maintenance flowchart

![](https://main.qcloudimg.com/raw/50ef1ceda14eb244e434b8cbe85da5f3.png)

#### Sample code

```
Delegate function:
public delegate void QAVEndpointsUpdateInfo(int eventID, int count, [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)]string[] openIdList);
Event function:
public abstract event QAVEndpointsUpdateInfo OnEndpointsUpdateInfoEvent;

Listen on an event:
ITMGContext.GetInstance().OnEndpointsUpdateInfoEvent += new QAVEndpointsUpdateInfo(OnEndpointsUpdateInfo);
Process the event listened on:
void OnEndpointsUpdateInfo(int eventID, int count, string[] openIdList)
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

```


### Room call quality control event
The message for quality control event triggered once every two seconds after room entry is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `loss`, and `delay`, which represent the following information. The event message will be identified in the `OnEvent` function.

| Parameter | Type | Description |
| ------------- |-------------|-------------|
| weight | int | Value range: 1-50. 50 indicates excellent sound quality, 1 indicates very poor (barely usable) sound quality, and 0 represents an initial meaningless value. Generally, if the value is below 30, you can remind users that the network is poor and recommend them to switch the network. |
| loss | double | Upstream packet loss rate |
| delay | int | Voice chat delay in ms |


## Voice Chat Audio APIs

![Image](https://main.qcloudimg.com/raw/863e0c165c7d43f9db59066befaac1e4.png)

### Notes on voice chat audio connection

The voice chat APIs can only be called after SDK initialization and room entry.
When Enable/Disable Mic/Speaker is clicked on the UI, the following practices are recommended:

- **For most game applications, it is recommended to call the `EnableMic` and `EnableSpeaker` APIs**, which is equivalent to calling the `EnableAudioCaptureDevice/EnableAudioSend` and `EnableAudioPlayDevice/EnableAudioRecv` APIs.
- For other mobile applications (such as social networking applications), enabling/disabling a capturing device will restart both capturing and playback devices. If the application is playing back background music, it will also be interrupted. Playback won't be interrupted if the mic is enabled/disabled through control of upstreaming/downstreaming. **Calling method: call `EnableAudioCaptureDevice(true)` and `EnableAudioPlayDevice(true)` once after room entry, and call `EnableAudioSend/Recv` to send/receive audio streams when Enable/Disable Mic is clicked**.
- For more information on how to release only a capturing or playback device, please see the `EnableAudioCaptureDevice` and `EnableAudioPlayDevice`.
- Call the `pause` API to pause the audio engine and call the `resume` API to resume the audio engine.

### Voice chat audio APIs

| API | Description |
| --------------------------- | :----------------------------: |
| EnableMic | Enables/disables mic |
| GetMicState | Gets mic status |
| EnableAudioCaptureDevice | Enables/disables capturing device |
| IsAudioCaptureDeviceEnabled | Gets capturing device status |
| EnableAudioSend | Enables/disables audio upstreaming |
| IsAudioSendEnabled | Gets audio upstreaming status |
| GetMicLevel | Gets real-time mic volume level |
| GetSendStreamLevel | Gets real-time audio upstreaming volume level |
| SetMicVolume | Sets mic volume level |
| GetMicVolume | Gets mic volume level |
| EnableSpeaker | Enables/disables speaker |
| GetSpeakerState | Gets speaker status |
| EnableAudioPlayDevice | Enables/disables playback device |
| IsAudioPlayDeviceEnabled | Gets playback device status |
| EnableAudioRecv | Enables/disables audio downstreaming |
| IsAudioRecvEnabled | Gets audio downstreaming status |
| GetSpeakerLevel | Gets real-time speaker volume level |
| GetRecvStreamLevel | Gets real-time downstreaming audio levels of other members in room |
| SetSpeakerVolume | Sets speaker volume level |
| GetSpeakerVolume | Gets speaker volume level |
| EnableLoopBack | Enables/disables in-ear monitoring |

## Voice Chat Capturing APIs

### Enabling or disabling mic

This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

EnableMic = EnableAudioCaptureDevice + EnableAudioSend


#### Function prototype  

```
ITMGAudioCtrl EnableMic(bool isEnabled)
```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | To enable the mic, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
Enable the mic
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```

### Getting mic status

This API is used to get the mic status. The returned value 0 indicates that the mic is off, while 1 on.

#### Function prototype  

```
ITMGAudioCtrl GetMicState()
```

#### Sample code  

```
micToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### Enabling or disabling capturing device

This API is used to enable/disable a capturing device. The device is not enabled by default after room entry.

- This API can only be called after room entry. The device will be disabled automatically after room exit.
- Operations such as permission application and volume type adjustment will generally be performed when a capturing device is enabled on a mobile device.

#### Function prototype  

```
ITMGAudioCtrl int EnableAudioPlayDevice(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | bool | To enable a capturing device, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code

```
// Enable capturing device
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### Getting capturing device status

This API is used to get the status of a capturing device.

#### Function prototype

```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()
```

#### Sample code

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### Enabling or disabling audio upstreaming

This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, please see the `EnableAudioCaptureDevice` API.

#### Function prototype

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | bool | To enable audio upstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(true);
```

### Getting audio upstreaming status

This API is used to get the status of audio upstreaming.

#### Function prototype  

```
ITMGAudioCtrl bool IsAudioSendEnabled()
```

#### Sample code  

```
bool IsAudioSend = ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();

```

### Getting real-time mic volume level

This API is used to get the real-time mic volume level. An int-type value in the range of 0-100 will be returned. It is recommended to call this API once every 20 ms.

>?This API is not applicable to the voice messaging service.

#### Function prototype  

```
ITMGAudioCtrl int GetMicLevel
```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### Getting real-time audio upstreaming volume level

This API is used to get the local real-time audio upstreaming volume level. An int-type value in the range of 0-100 will be returned.
>?This API is not applicable to the voice messaging service.

#### Function prototype  

```
ITMGAudioCtrl int GetSendStreamLevel()
```

#### Sample code  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();
```

### Setting mic software volume level

This API is used to set the mic volume level. The corresponding parameter is `volume`, which is equivalent to attenuating or gaining the captured sound. 0 indicates that the audio is mute, while 100 indicates that the volume level remains unchanged. The default value is 100.
>?This API is not applicable to the voice messaging service.
>
#### Function prototype  

```
ITMGAudioCtrl SetMicVolume(int volume)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume | int | Volume level. Value range: 0-200 |

#### Sample code  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);
```

### Getting mic software volume level

This API is used to get the mic volume level. An int-type value will be returned. 101 indicates that the `SetMicVolume` API has not been called.
>?This API is not applicable to the voice messaging service.

#### Function prototype  

```
ITMGAudioCtrl GetMicVolume()
```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();
```

## Voice Chat Playback APIs

### Enabling or disabling speaker

This API is used to enable/disable the speaker.
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.

#### Function prototype  

```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | bool | To disable the speaker, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  
```
// Enable the speaker
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

### Getting speaker status

This API is used to get the speaker status. 0 indicates that the speaker is off, 1 on, and 2 working.

#### Function prototype  

```
ITMGAudioCtrl GetSpeakerState()
```

#### Sample code  

```
speakerToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```



### Enabling or disabling playback device

This API is used to enable/disable a playback device.

#### Function prototype  

```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | bool | To disable a playback device, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
// Enable the playback device
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);
```

### Getting playback device status

This API is used to get the status of a playback device.

#### Function prototype

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```

#### Sample code  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### Enabling or disabling audio downstreaming

This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, please see the `EnableAudioPlayDevice` API.

#### Function prototype  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | bool | To enable audio downstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(true);
```



### Getting audio downstreaming status

This API is used to get the status of audio downstreaming.

#### Function prototype  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

#### Sample code  

```
bool IsAudioRecv = ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```

### Getting real-time speaker volume level

This API is used to get the real-time speaker volume level. An int-type value will be returned to indicate the volume level. It is recommended to call this API once every 20 ms.

#### Function prototype  

```
ITMGAudioCtrl GetSpeakerLevel()
```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();

```

### Getting the real-time downstreaming audio levels of other members in room

This API is used to get the real-time audio downstreaming volume levels of other members in the room. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGAudioCtrl int GetRecvStreamLevel(string openId)
```

| Parameter | Type | Description |
| ------ | :----: | -------------------- |
| openId | string | `openId` of another member in the room |

#### Sample code  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetRecvStreamLevel(openId);
```

### Setting speaker volume level

This API is used to set the speaker volume level.
The corresponding parameter is volume. 0 indicates that the audio is mute, while 100 indicates that the volume level remains unchanged. The default value is 100.

#### Function prototype  

```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume | int | Volume level. Value range: 0-200 |

#### Sample code  

```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);
```

### Getting speaker volume level

This API is used to get the speaker volume level. An int-type value will be returned to indicate the volume level. 101 indicates that the `SetSpeakerVolume` API has not been called.
`Level` indicates the real-time volume level, while `Volume` the speaker volume level. The final volume level equals to Level*Volume%.
For example, if the value of "Level" is 100 and that of “Volume” is 60, then the final volume level will be 60.

#### Function prototype  

```
ITMGAudioCtrl GetSpeakerVolume()
```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();
```

### Enabling in-ear monitoring

This API is used to enable in-ear monitoring. You need to call `EnableLoopBack+EnableSpeaker` before you can hear your own voice.

#### Function prototype  

```
ITMGContext GetAudioCtrl EnableLoopBack(bool enable)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable | bool | Specifies whether to enable |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);
```

### Callback for device use and release
After a device is used or released in a room, a callback will be executed through a delegate function to pass a message of the event.

```
Delegate function:
public delegate void QAVOnDeviceStateChangedEvent(int deviceType, string deviceId, bool openOrClose);
Event function:
public abstract event QAVOnDeviceStateChangedEvent OnDeviceStateChangedEvent;
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| deviceType | int | 1: capturing device, 2: playback device |
| deviceId | string | Device GUID, which is used to identify a device and only applies to Windows and macOS. |
| openOrClose | bool | Use/release of capturing/playback device |

#### Sample code  

```
Listen on an event:
ITMGContext.GetInstance().GetAudioCtrl().OnDeviceStateChangedEvent += new QAVAudioDeviceStateCallback(OnAudioDeviceStateChange);
Process the event listened on:
void QAVAudioDeviceStateCallback(int deviceType, string deviceId, bool openOrClose){
    // Callback for device use and release
}
```
## Voice Messaging and Speech-to-Text

Voice messaging refers to recording and sending a voice message. At the same time, the voice message can be converted to text and translated.

>?It is recommended to use the streaming voice-to-text service.

### Voice messaging and speech-to-text conversion flowchart

<img src="https://main.qcloudimg.com/raw/310eaf2b780c5fc47ffeaf791a6df392.png" width="70%">


| API | Description |
| -------------------------------------- | :------------------------: |
| ApplyPTTAuthbuffer | Initializes authentication |
| SetMaxMessageLength | Specifies maximum length of voice message |
| StartRecording | Starts recording |
| StartRecordingWithStreamingRecognition | Starts streaming recording |
| PauseRecording | Pauses recording |
| ResumeRecording | Resumes recording |
| StopRecording | Stops recording |
| CancelRecording | Cancels recording |
| GetMicLevel | Gets real-time mic volume level |
| SetMicVolume | Sets recording volume level |
| GetMicVolume | Gets recording volume level |
| GetSpeakerLevel | Gets real-time speaker volume level |
| SetSpeakerVolume | Sets playback volume level |
| GetSpeakerVolume | Gets playback volume level |
| UploadRecordedFile | Uploads audio file |
| DownloadRecordedFile | Downloads audio file |
| PlayRecordedFile | Plays back audio |
| StopPlayFile | Stops playing back audio |
| GetFileSize | Gets audio file size |
| GetVoiceFileDuration | Gets audio file duration |
| SpeechToText | Converts speech to text |


### Initializing SDK

Before the initialization, the SDK is in the uninitialized status, and you need to initialize it through the `Init` API before you can use the voice chat and voice messaging and speech-to-text services.

If you have any questions when using the service, please see [Voice Messaging and Speech-to-Text](https://intl.cloud.tencent.com/document/product/607/30258).

### Initialization APIs

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |



### Authentication initialization

Call authentication initialization after initializing the SDK. For more information on how to get the `authBuffer`, please see the voice chat authentication information API.

#### Function prototype  

```
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```

| Parameter | Type | Description |
| ---------- | :----: | ---- |
| authBuffer | byte[] | Authentication |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().ApplyPTTAuthbuffer(authBuffer);
```


## Streaming Speech Recognition


### Starting streaming speech recognition

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. It can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation. **To stop recording, call `StopRecording`**.

#### Function prototype  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath, string translateLanguage,string translateLanguage) 
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | String | Path of stored audio file |
| speechLanguage | String | The language in which the audio file is to be converted to text. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) |
| translateLanguage | String | The language into which the audio file will be translated. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) (This parameter is currently unavailable. Enter the same value as that of `speechLanguage`) |

#### Sample code  

```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath, "cmn-Hans-CN","cmn-Hans-CN");
```


### Callback for streaming speech recognition
After streaming speech recognition is started, you need to listen for callback messages in the callback function `onEvent`. Event messages are divided into:
- `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE` returns text after the recording is stopped and the recognition is completed, which is equivalent to returning the recognized text after a paragraph of speech.
- `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING` returns the recognized text in real-time during the recording, which is equivalent to returning the recognized text while speaking.

The event message will be identified in the `OnEvent function` based on the actual needs. The passed parameters include the following four messages.

| Message Name | Description |
| ------------- |:-------------:|
| result | Returns code indicating whether streaming speech recognition is successful. |
| text | Text converted from speech |
| file_path | Local path of stored recording file |
| file_id | Backend URL address of recording file, which will be retained for 90 days |

>!The file_id is empty when the 'ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING' message is listened.

#### Error codes

| Error Code | Description | Suggested Solution |
| ------------- |:-------------:|:-------------:|
| 32775 | Streaming speech-to-text conversion failed, but recording succeeded.| Call the `UploadRecordedFile` API to upload the recording file and then call the `SpeechToText` API to perform speech-to-text conversion. |
| 32777 | Streaming speech-to-text conversion failed, but recording and upload succeeded.| The message returned contains a backend URL after successful upload. Call the `SpeechToText` API to perform speech-to-text conversion. |
| 32786 | Streaming speech-to-text conversion failed. | During streaming recording, wait for the execution result of the streaming recording API to return. |

#### Sample code  

```
			Listen on an event:
			ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechComplete +=new QAVStreamingRecognitionCallback (OnStreamingSpeechComplete);
			ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechisRunning += new QAVStreamingRecognitionCallback (OnStreamingRecisRunning);
			Process the event listened on:
			void OnStreamingSpeechComplete(int code, string fileid, string filepath, string result){
					// Callback for streaming speech recognition
			}

			void OnStreamingRecisRunning(int code, string fileid, string filePath, string result){
					if (code == 0)
					{
						setBtnText(mStreamBtn, "Streaming");
						InputField field = transform.Find("recordFilePath").GetComponent<InputField>();
						field.text = filePath;

						field = transform.Find("downloadUrl").GetComponent<InputField>();
						field.text = "Stream is Running";

						field = transform.Find("convertTextResult").GetComponent<InputField>();
						field.text = result;
						showWarningText("Recording");
					}	
}
```



## Voice Message Recording

### Specifying maximum duration of voice message

This API is used to specify the maximum duration of a voice message, which can be up to 58 seconds.

#### Function prototype

```
ITMGPTT int SetMaxMessageLength(int msTime)
```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------ |
| msTime | int | Audio duration in ms. Value range: 1000 < msTime <= 58000 |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().SetMaxMessageLength(10000); 
```

### Starting recording

This API is used to start recording. The recording file must be uploaded first before you can perform operations such as speech-to-text conversion.

#### Function prototype  

```
ITMGPTT int StartRecording(string fileDir)
```

| Parameter | Type | Description |
| -------- | :----: | -------------- |
| fileDir | string | Path of stored audio file |

#### Sample code  

```
string recordPath = Application.persistentDataPath + string.Format ("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecording(recordPath);
```

### Callback for recording start
A callback will be executed through a delegate function to pass a message when recording is completed.
#### Function prototype  
```
Delegate function:
public delegate void QAVRecordFileCompleteCallback(int code, string filepath); 
Event function:
public abstract event QAVRecordFileCompleteCallback OnRecordFileComplete;
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| code | string | 0: recording is completed |
| filepath | string | Path of stored recording file |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ------------------------ | ------------------------------------------------------------ |
| 4097 | Parameter is empty. | Check whether the API parameters in the code are correct. |
| 4098 | Initialization error. | Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal. |
| 4099 | Recording is in progress. | Ensure that the SDK recording feature is used at the right time. |
| 4100 | Audio data is not captured. | Check whether the mic is working properly. |
| 4101 | An error occurred while accessing the file during recording. | Ensure the existence of the file and the validity of the file path. |
| 4102 | The mic is not authorized. | Mic permission is required for using the SDK. To add the permission, please see the SDK project configuration document for the corresponding engine or platform. |
| 4103 | The recording duration is too short. | The recording duration should be in ms and longer than 1,000 ms. |
| 4104 | No recording operation is started. | Check whether the recording starting API has been called. |

#### Sample code  

```
Listen on an event:
ITMGContext.GetInstance().GetPttCtrl().OnRecordFileComplete +=  new QAVRecordFileCompleteCallback (OnRecordFileComplete);
Process the event listened on:
void OnRecordFileComplete(int code, string filepath){
    // Callback for recording start
}
```


### Pausing recording

This API is used to pause recording. If you want to resume recording, please call the `ResumeRecording` API.

#### Function prototype  

```
ITMGPTT int PauseRecording()
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().PauseRecording();
```

### Resuming recording

This API is used to resume recording.

#### Function prototype  

```
ITMGPTT int ResumeRecording()
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().ResumeRecording();
```

### Stopping recording

This API is used to stop recording. It is async, and a callback for recording completion will be returned after recording stops. A recording file will be available only after recording succeeds.

#### Function prototype  

```
ITMGPTT int StopRecording()
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```



### Canceling recording

This API is used to cancel recording. There is no callback after cancellation.

#### Function prototype  

```
ITMGPTT int CancelRecording()
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().CancelRecording();
```

### Getting the real-time mic volume level of voice messaging

This API is used to get the real-time mic volume level. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGPTT int GetMicLevel()
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().GetMicLevel();

```

### Setting the recording volume level of voice messaging

This API is used to set the recording volume level of voice messaging. Value range: 0-200.

#### Function prototype  

```
ITMGPTT int SetMicVolume(int vol)
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().SetMicVolume(100);
```

### Getting the recording volume level of voice messaging

This API is used to get the recording volume level of voice messaging. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGPTT int GetMicVolume()
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().GetMicVolume();
```

### Getting the real-time speaker volume level of voice messaging

This API is used to get the real-time speaker volume level. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGPTT int GetSpeakerLevel()
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerLevel();
```

### Setting the playback volume level of voice messaging

This API is used to set the playback volume level of voice messaging. Value range: 0-200.

#### Function prototype  

```
ITMGPTT int SetSpeakerVolume(int vol)
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().SetSpeakerVolume(100);
```

### Getting the playback volume level of voice messaging

This API is used to get the playback volume level of voice messaging. An int-type value will be returned. Value range: 0-200.

#### Function prototype  
```
ITMGPTT int GetSpeakerVolume()
```

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerVolume();
```

## Voice Message Playback
### Playing back audio

This API is used to play back audio.

#### Function prototype  

```
ITMGPTT PlayRecordedFile (string downloadFilePath)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| downloadFilePath | string | File path |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------- | ------------------------------ |
| 20485 | Playback is not started. | Ensure the existence of the file and the validity of the file path. |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().PlayRecordedFile(filePath); 
```

### Callback for audio playback
A callback will be executed through a delegate function to pass a message when an audio file is played back.
#### Function prototype  
```
Delegate function:
public delegate void QAVPlayFileCompleteCallback(int code, string filepath);
Event function:
public abstract event QAVPlayFileCompleteCallback OnPlayFileComplete;
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| code | int | 0: playback is completed |
| filepath | string | Path of stored recording file |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| 20481 | Initialization error. | Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal. |
| 20482 | During playback, the client tried to interrupt and play back the next one but failed (which should succeed normally). | Check whether the code logic is correct. |
| 20483 | Parameter is empty. | Check whether the API parameters in the code are correct. |
| 20484 | Internal error. | An error occurred while initializing the player. This error code is generally caused by failure in decoding, and the error should be located with the aid of logs. |

#### Sample code

```
Listen on an event:
ITMGContext.GetInstance().GetPttCtrl().OnPlayFileComplete +=new  QAVPlayFileCompleteCallback(OnPlayFileComplete);
Process the event listened on:
void OnPlayFileComplete(int code, string filepath){
    // Callback for audio playback
}

```



### Stopping audio playback

This API is used to stop audio playback. There will be a callback for playback completion when the playback stops.

#### Function prototype  

```
ITMGPTT int StopPlayFile()
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().StopPlayFile();
```



### Getting audio file size

This API is used to get the size of an audio file.

#### Function prototype  

```
ITMGPTT GetFileSize(string filePath) 
```

| Parameter | Type | Description |
| -------- | :----: | -------------- |
| filePath | string | Path of audio file, which is a local path. |

#### Sample code  

```
int fileSize = ITMGContext.GetInstance().GetPttCtrl().GetFileSize(filepath);
```

### Getting audio file duration

This API is used to get the duration of an audio file in milliseconds.

#### Function prototype  

```
ITMGPTT int GetVoiceFileDuration(string filePath)
```

| Parameter | Type | Description |
| -------- | :----: | -------------- |
| filePath | string | Path of audio file, which is a local path. |

#### Sample code  

```
int fileDuration = ITMGContext.GetInstance().GetPttCtrl().GetVoiceFileDuration(filepath);
```


## Voice Message Upload and Download

### Uploading audio file

This API is used to upload an audio file.

#### Function prototype  

```
ITMGPTT int UploadRecordedFile (string filePath)
```

| Parameter | Type | Description |
| -------- | :----: | -------------- |
| filePath | String | Path of uploaded audio file, which is a local path. |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().UploadRecordedFile(filePath);
```

### Callback for audio file upload completion
A callback will be executed through a delegate function to pass a message when the upload of audio file is completed.
#### Function prototype

```
Delegate function:
public delegate void QAVUploadFileCompleteCallback(int code, string filepath, string fileid);
Event function:
public abstract event QAVUploadFileCompleteCallback OnUploadFileComplete; 
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| code | int | 0: recording is completed |
| filepath | string | Path of stored recording file |
| fileid | string | URL path of file, which will be retained on the server for 90 days |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ------------------------------ | ------------------------------------------------------ |
| 8193 | An error occurred while accessing the file during upload. | Ensure the existence of the file and the validity of the file path. |
| 8194 | Signature verification failed. | Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized. |
| 8195 | A network error occurred. | Check whether the device can access the internet. |
| 8196 | The network failed while getting the upload parameters. | Check whether the authentication is correct and whether the device can access the internet. |
| 8197 | The packet returned during the process of getting the upload parameters is empty. | Check whether the authentication is correct and whether the device network can normally access the internet. |
| 8198 | Failed to decode the packet returned during the process of getting the upload parameters. | Check whether the authentication is correct and whether the device can access the internet. |
| 8200 | No `appinfo` is set. | Check whether the `apply` API is called or whether the input parameters are empty. |

#### Sample code

```
Listen on an event:
ITMGContext.GetInstance().GetPttCtrl().OnUploadFileComplete +=new QAVUploadFileCompleteCallback (OnUploadFileComplete);
Process the event listened on:
void OnUploadFileComplete(int code, string filepath, string fileid){
    // Callback for audio file upload completion
}
```

### Downloading the audio file

This API is used to download an audio file.

#### Function prototype  

```
ITMGPTT DownloadRecordedFile (string fileID, string downloadFilePath)
```

| Parameter | Type | Description |
| ---------------- | :----: | ------------------------------------- |
| fileID | String | File URL path |
| downloadFilePath | string | Local path of saved file |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().DownloadRecordedFile(fileId, filePath);
```

### Callback for audio file download completion
A callback will be executed through a delegate function to pass a message when the download of audio file is completed.
#### Function prototype  
```
Delegate function:
public delegate void QAVDownloadFileCompleteCallback(int code, string filepath, string fileid);
Event function:
public abstract event QAVDownloadFileCompleteCallback OnDownloadFileComplete;
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| code | int | 0: recording is completed |
| filepath | string | Path of stored recording file |
| fileid | string | URL path of file, which will be retained on the server for 90 days |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| 12289 | An error occurred while accessing the file during download. | Check whether the file path is valid. |
| 12290 | Signature verification failed. | Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized. |
| 12291 | Network storage system exception | The server failed to get the audio file. Check whether the API parameter `fileid` is correct, whether the network is normal, and whether the file exists in COS. |
| 12292 | Server file system error. | Check whether the device can access the internet and whether the file exists on the server. |
| 12293 | The HTTP network failed during the process of getting the download parameters. | Check whether the device can access the internet. |
| 12294 | The packet returned during the process of getting the download parameters is empty. | Check whether the device can access the internet. |
| 12295 | Failed to decode the packet returned during the process of getting the download parameters. | Check whether the device can access the internet. |
| 12297 | No `appinfo` is set. | Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized. |

#### Sample code

```
Listen on an event:
ITMGContext.GetInstance().GetPttCtrl().OnDownloadFileComplete +=new QAVDownloadFileCompleteCallback(OnDownloadFileComplete);
Process the event listened on:
void OnDownloadFileComplete(int code, string filepath, string fileid){
    // Callback for audio file download completion
}

```


## Speech-to-Text Service

### Converting audio file to text

This API is used to convert a specified audio file to text.

#### Function prototype  

```
ITMGPTT int SpeechToText(String fileID)
```

| Parameter | Type | Description |
| ------ | :----: | ---------------------------------- |
| fileID | String | Audio file URL |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID);
```



### Translating audio file into text in specified language

This API can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation.

#### Function prototype  

```
ITMGPTT int SpeechToText(String fileID,String language)
```

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| fileID | String | URL of audio file, which will be retained on the server for 90 days |
| speechLanguage | String | The language in which the audio file is to be converted to text. For parameters, please see [ Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) |
| translatelanguage | String | The language into which the audio file will be translated. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). This parameter is currently unavailable. Enter the same value as that of `speechLanguage`. |

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID,"cmn-Hans-CN","cmn-Hans-CN");
```



### Callback for recognition
A callback will be executed through a delegate function to pass a message when a specified audio file is recognized and converted to text.
#### Function prototype  

```
Delegate function:
public delegate void QAVSpeechToTextCallback(int code, string fileid, string result);
Event function:
public abstract event QAVSpeechToTextCallback OnSpeechToTextComplete;
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| code | int | 0: recording is completed |
| fileid | string | URL of recording file, which will be retained on the server for 90 days |
| result | string | Converted text |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------------------- | ------------------------------------------------------------ |
| 32769 | An internal error occurred. | Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |
| 32770 | Network failed. | Check whether the device can access the internet. |
| 32772 | Failed to decode the returned packet. | Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |
| 32774 | No `appinfo` is set. | Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized. |
| 32776 | `authbuffer` check failed. | Check whether `authbuffer` is correct. |
| 32784 | Incorrect speech-to-text conversion parameter. | Check whether the API parameter `fileid` in the code is empty. |
| 32785 | Speech-to-text translation returned an error. | Error with the backend of voice messaging and speech-to-text feature. Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |

#### Sample code

```
Listen on an event:
ITMGContext.GetInstance().GetPttCtrl().OnSpeechToTextComplete += new QAVSpeechToTextCallback(OnSpeechToTextComplete);
Process the event listened on:
void OnSpeechToTextComplete(int code, string fileid, string result){
    // Callback for recognition
}

```



## Advanced APIs

### Getting version number

This API is used to get the SDK version number for analysis.

#### Function prototype

```
ITMGContext  abstract string GetSDKVersion()
```

#### Sample code  

```
ITMGContext.GetInstance().GetSDKVersion();
```



### Setting log printing level

This API is used to set the level of logs to be printed. It is recommended to keep the default level.

#### Function prototype

```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | Sets the level of logs to be written. `TMG_LOG_LEVEL_NONE` indicates not to write. Default value: TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | Sets the level of logs to be printed. `TMG_LOG_LEVEL_NONE` indicates not to print. Default value: TMG_LOG_LEVEL_ERROR |



| ITMG_LOG_LEVEL | Description |
| ----------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE=0 | Does not print logs |
| TMG_LOG_LEVEL_ERROR=1 | Prints error logs (default) |
| TMG_LOG_LEVEL_INFO=2 | Prints info logs |
| TMG_LOG_LEVEL_DEBUG=3 | Prints debug logs |
| TMG_LOG_LEVEL_VERBOSE=4 | Prints verbose logs |

#### Sample code  

```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### Setting log printing path
This API is used to set the log printing path.
The default path is as follows:

| OS | Path |
| ------------- |-------------|
| Windows | %appdata%\Tencent\GME\ProcessName |
| iOS | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files |
| Mac | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

#### Function prototype

```
ITMGContext  SetLogPath(string logDir)
```

| Parameter | Type | Description |
| ------ | :----: | ---- |
| logDir | String | Path |

#### Sample code  

```
ITMGContext.GetInstance().SetLogPath(path);
```

### Getting diagnostic messages

This API is used to get information on the quality of real-time audio/video calls, which is mainly used to view real-time call quality and troubleshoot problems and can be ignored on the business side.

#### Function prototype  

```
ITMGRoom GetQualityTips()
```

#### Sample code  

```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();
```

### Blocking audio data

This API is used to add an ID to the audio data blocklist. This operation blocks audio from someone and only applies to the local device. A returned value of `0` indicates the call is successful. Assume that users A, B, and C are all speaking using their mic in a room: 
- If A blocks C, A can only hear B;
- If B blocks neither A nor C, B can hear both of them;
- If C blocks neither A nor B, C can hear both of them.

#### Function prototype  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```

| Parameter | Type | Description |
| ------ | :----: | ----------------- |
| openId | String | ID to be blocked |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl ().AddAudioBlackList (id);
```

### Unblocking audio data

This API is used to remove an ID from the audio data blocklist. A returned value of `0` indicates the call is successful.

#### Function prototype  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| openId | NSString | ID to be unblocked |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (id);
```

