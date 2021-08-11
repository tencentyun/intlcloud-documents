This document describes how to access and debug the GME APIs for Unity voice chat.

>?This document applies to GME SDK version 2.8.

## Key Considerations for Using GME

GME provides two services: voice chat service and voice message and speech-to-text service, both of which rely on key APIs such as Init and Poll.

<dx-alert infotype="notice" title="Note on Init API">
If you need to use voice chat and voice message services at the same time, **you only need to call `Init` API once**.
Billing will not start after initialization. After you call <dx-tag-link link="#EnterRoom" tag="API: EnterRoom">Entering a voice chat room</dx-tag-link> to enter the room successfully, the billing will start.
</dx-alert>

![image](https://main.qcloudimg.com/raw/99d612d90268a7248f5b55c385eeb8b8.png)

### Directions

<dx-steps>
-<dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">Entering a voice chat room</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">Enabling the microphone</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">Enabling the speaker</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">Exiting a voice room</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">Uninitializing GME</dx-tag-link>
</dx-steps>


### Important notes

- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error code, please see <dx-tag-link link="https://cloud.tencent.com/document/product/607/15173" tag="ErrorCode">Error Codes</dx-tag-link>.

### C# classes

| Class | Description |
| ------------------- | :----------------: |
| ITMGContext | Key APIs |
| ITMGRoom | Room APIs |
| ITMGRoomManager | Room management APIs |
| ITMGAudioCtrl | Audio APIs |
| ITMGAudioEffectCtrl | Sound effect and accompaniment APIs |

## Key APIs

Before the initialization, the SDK is in the uninitialized status, and **you need to initialize it through the `Init` API** before you can use the voice chat and speech-to-text services.

**You need to call the `Init` API before calling any APIs of GME.**


If you have any questions when using the service, please see [General Issues](https://intl.cloud.tencent.com/document/product/607/30254).

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |

>!If you need to switch the account, please call `UnInit` to uninitialize the SDK. No fee is incurred for calling Init API.

### Imported header files

```
using TencentMobileGaming;
```

### Getting an instance

Get the `Context` instance by using the `ITMGContext` method instead of `QAVContext.GetInstance()`.

### [Initializing SDK](id:Init)

- This API is used to initialize the GME service. It is recommended to call it when initializing the application. No fee is incurred for calling this API.
- **For more information on how to get the `sdkAppID` parameter, please see [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/39698)**.
- **The openID uniquely identifies a user with the rules stipulated by the application developer and unique in the application (currently, only INT64 is supported)**.

> !
>
> - The SDK must be initialized before a user can enter a voice chat room.
> - The Init API must be called in the same thread with other APIs. It is recommended to call all APIs in the main thread.

#### Function prototype

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | `AppID` provided by the GME service from the [Tencent Cloud console](https://console.cloud.tencent.com/gamegme) |
| openID | String | `openID` can only be in Int64 type, which is passed after being converted to a string. |


#### Returned values

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0 | Initialized SDK successfully |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.


<dx-alert infotype="notice" title="Notes on 7015 error code">
- The 7015 error code is judged by md5. If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- Due to the third-party reinforcement, Unity packaging mechanism and other factors, the md5 of the library file will be affected, resulting in misjudgment. **Please ignore this error in the logic for official release**, and try to avoid displaying it in the UI.
</dx-alert>




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


### [Triggering event callback](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
Refer to the EnginePollHelper file in [Demo](https://intl.cloud.tencent.com/document/product/607/18521).


<dx-alert infotype="alarm" title="Calling the `Poll` API periodically">
The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
</dx-alert>




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

### Pausing the system

When a `Pause` event occurs in the system, the engine should also be notified for pause. For example, when the application switches to the background (OnApplicationPause, isPause=True), and you do not need the background to play back the audio in the room, please call `Pause` API to pause the GME service.

#### Function prototype

```
ITMGContext public abstract int Pause()
```

### Resuming the system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### Function prototype

```
ITMGContext  public abstract int Resume()
```



### [Uninitializing SDK](id:UnInit)

This API is used to uninitialize the SDK to make it uninitialized. **Switching accounts requires uninitialization**.

#### Function prototype

```
ITMGContext public abstract int Uninit()
```


## Voice Chat

Voice chat refers to the one-to-one or one-to-many real-time voice call feature.

### Voice chat flowchart

![](https://main.qcloudimg.com/raw/28a13d4beccdfecb0ad7530008ec8da0.png)





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

## Voice Chat Room Call Flowchart

![](https://main.qcloudimg.com/raw/2b5d8f7f7f4b4b3fbce8c9ebf01f78d8.png)

### Authentication information

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    


#### Function prototype

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)


```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| appId | int | `AppID` from the Tencent Cloud console.|
| roomId | string | Room ID, which can contain up to 127 characters. |
| openId | string | User ID, which is the same as `openID` during initialization. |
| key | string | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |



#### Sample code  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
        return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}

```



###  [Entering a room](id:EnterRoom)

When a user enters a room with the generated authentication information, the `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` message will be received as a callback. Mic and speaker are not enabled by default after room entry. The returned value of `AV_OK` indicates a success.

The audio type of the room is determined by the first user to enter the room. After that, if a member in the room changes the room type, it will take effect for all members there. For example, if the first user entering the room uses the smooth sound quality, and the second user entering the room uses the HD sound quality, the room audio type of the second user will become smooth sound quality. Only when a member in the room calls the `ChangeRoomType` API, the audio type of the room will be changed.

For more information on how to choose a room audio type, please see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).

#### Function prototype

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)

```

| Parameter | Type | Description |
| ---------- | :----------: | ----------------------- |
| roomId | string | Room ID, which can contain up to 127 characters |
| roomType | ITMGRoomType | Room audio type |
| authBuffer | Byte[] | Authentication code |




#### Sample code  

```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);


```

### Callback for room entry

After the user enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function for callback and processing. A successful callback means that the room entry is successful, and the billing starts.

<dx-fold-block title="Billing references">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/36276)
[Billing FAQs](https://intl.cloud.tencent.com/document/product/607/30255)
[Will the billing continue if the client is disconnected when using the voice chat?](https://intl.cloud.tencent.com/document/product/607/30255)
</dx-fold-block>

#### Function prototype

```
// Delegate function:
public delegate void QAVEnterRoomComplete(int result, string error_info);
// Event function:
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;

```



#### Sample code  

```
// Listen on an event:
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

// Process the event listened on:
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
  			ShowLoginPanel("error code:" + err + " error message:" + errInfo);
            return;
	}else{
		// Entered room
    }
}

```

#### Data details

| Message | Data | Sample |
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM | result; error_info | {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | result; error_info | {"error_info":"waiting timeout, please check your network","result":0} |


If the network is disconnected, there will be a disconnected callback prompt `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`. At this time, the SDK will automatically reconnect, and the callback is `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`. When the reconnection is successful, there will be a callback `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS`.


#### Error codes

| Error Code Value | Cause and Suggested Solution |
| -------- | ------------------------------------------------------------ |
| 7006 | Authentication failed <li>The `AppID` does not exist or is incorrect.<li>An error occurred while authenticating the `authbuff`.<li>Authentication expired.<li>The `OpenId` does not meet the specification. |
| 7007 | Already in another room. |
| 1001 | The user was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned. |
| 1003 | The user was already in the room and called the room entering API again. |
| 1101 | Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally. |

### [Exiting the room](id:ExitRoom)

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
public delegate void QAVExitRoomComplete();
Event function:
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent; 

```

#### Sample code  

```
Listen on an event:
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
Process the event listened on:
void OnExitRoomComplete(){
    // Send a callback after room exit
}

```

### Determining whether user has entered room

This API is used to determine whether the user has entered a room. A bool-type value will be returned. The call is invalid during the process of room entry.

#### Function prototype  

```
ITMGContext abstract bool IsRoomEntered()

```

#### Sample code  

```
ITMGContext.GetInstance().IsRoomEntered();

```



### Switching room

User can call this API to quickly switch the voice chat room after entering the room. After the room is switched, the device is not reset, that is, if the microphone is already enabled in this room, the microphone will keep enabled after the room is switched.

The callback for quickly switching rooms is `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM`, and the fields are `error_info` and `result`.

#### API prototype

```
public abstract int SwitchRoom(string roomID, byte[] authBuffer);

```

#### Type descriptions

| Parameter | Type | Description |
| ------------ | ------ | ------------------------------ |
| targetRoomID | String | ID of the room to enter |
| authBuffer | byte[] | Generates a new authentication with the ID of the room to enter |



### Cross-room mic connection

Call this API to connect the microphones across rooms after the room entry. After the call, the local user can communicate with the target OpenID user in the target room.

#### API prototype

```
/// <summary> Enable the room sharing, and connect the mic of the OpenID in another room.</summary>
public abstract int StartRoomSharing(string targetRoomID, string targetOpenID, byte[] authBuffer);
/// <summary> Stop the enabled room sharing.</summary>
public abstract int StopRoomSharing();

```

#### Type descriptions

| Parameter | Type | Description |
| ------------ | ------ | ----------------------- |
| targetRoomID | String | ID of the room to connect mic |
| targetOpenID | String | The target OpenID to connect mic |
| authBuffer | byte[] | Reserved flag. You just need to enter NULL. |


### Member status change

This API is used to obtain the user speaking in the room and display it in the UI, and to send a notification when someone entering or exiting the room.
A notification for this event will be sent only when the status changes. To get member status in real time, cache the notification when it is received at the upper layer. The event message `ITMG_MAIN_EVNET_TYPE_USER_UPDATE` containing `event_id`, `count`, and `openIdList` will be returned. The event message will be identified in the `OnEvent` function.
Notifications for audio events are subject to a threshold, and a notification will be sent only when this threshold is exceeded. The notification "A member has stopped sending audio packets" will be sent if no audio packets are received in more than two seconds.


| event_id | Description | Maintenance |
| --------------------------- | :------------------: | ---------------------- |
| EVENT_ID_ENDPOINT_ENTER | A member enters the room | Member list |
| EVENT_ID_ENDPOINT_EXIT | A member exits the room | Member list |
| EVENT_ID_ENDPOINT_HAS_AUDIO | A member sends audio packets | Chat member list |
| EVENT_ID_ENDPOINT_NO_AUDIO | A member stops sending audio packets | Chat member list |

#### Room member maintenance flowchart

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

#### Sample code

```
// Delegate function:
public delegate void QAVEndpointsUpdateInfo(int eventID, int count, [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)]string[] openIdList);
// Event function:
public abstract event QAVEndpointsUpdateInfo OnEndpointsUpdateInfoEvent;

// Listen on an event:
ITMGContext.GetInstance().OnEndpointsUpdateInfoEvent += new QAVEndpointsUpdateInfo(OnEndpointsUpdateInfo);
// Process the event listened on:
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

### Muting in a room


This API is used to add an ID to the audio data blocklist. This operation blocks audio from someone and only applies to the local device. A returned value of `0` indicates the call is successful. Assume that users A, B, and C are all speaking using their mic in a room: 

- If A blocks C, A can only hear B;
- If B blocks neither A nor C, B can hear both of them;
- If C blocks neither A nor B, C can hear both of them.

This API is suitable for scenarios where a user is muted in a room.

#### Function prototype  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)

```

| Parameter | Type | Description |
| ------ | :----: | ----------------- |
| openId | String | ID to be blocked |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl ().AddAudioBlackList (openId);

```

### Unmuting

This API is used to remove an ID from the audio data blacklist. A returned value of 0 indicates the call is successful.

#### Function prototype  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)

```

| Parameter | Type | Description |
| ------ | :----: | ----------------- |
| openId | String | ID to be unblocked |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (openId);

```

## Voice Chat Audio APIs

![Image](https://main.qcloudimg.com/raw/c85fe68b4b26555adf8ad01c82711f5b.png)

### Notes on voice chat audio connection

The voice chat APIs can only be called after SDK initialization and room entry.
When Enable/Disable Mic/Speaker is clicked on the UI, the following practices are recommended:

- **For most game applications, it is recommended to call the `EnableMic` and `EnableSpeaker` APIs**, which is equivalent to calling the `EnableAudioCaptureDevice/EnableAudioSend` and `EnableAudioPlayDevice/EnableAudioRecv` APIs.
- For other mobile applications (such as social networking applications), enabling/disabling a capturing device will restart both capturing and playback devices. If the application is playing back background music, it will also be interrupted. Playback will not be interrupted if the mic is enabled/disabled through control of upstreaming/downstreaming. **Calling method: call `EnableAudioCaptureDevice(true)` and `EnableAudioPlayDevice(true)` once after room entry, and call `EnableAudioSend/Recv` to send/receive audio streams when Enable/Disable Mic is clicked**.
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
| GetMicLevel | Gets real-time mic volume |
| GetSendStreamLevel | Gets real-time audio upstreaming volume |
| SetMicVolume | Sets mic volume |
| GetMicVolume | Gets mic volume |
| EnableSpeaker | Enables/disables speaker |
| GetSpeakerState | Gets speaker status |
| EnableAudioPlayDevice | Enables/disables playback device |
| IsAudioPlayDeviceEnabled | Gets playback device status |
| EnableAudioRecv | Enables/disables audio downstreaming |
| IsAudioRecvEnabled | Gets audio downstreaming status |
| GetSpeakerLevel | Gets real-time speaker volume |
| GetRecvStreamLevel | Gets real-time downstreaming audio levels of other members in room |
| SetSpeakerVolume | Sets speaker volume |
| GetSpeakerVolume | Gets speaker volume |
| EnableLoopBack | Enables/disables in-ear monitoring |

## Voice Chat Capturing APIs

### [Enabling or disabling the microphone](id:EnableMic)

This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

**EnableMic = EnableAudioCaptureDevice + EnableAudioSend**


#### Function prototype  

```
ITMGAudioCtrl EnableMic(bool isEnabled)

```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | To enable the mic, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
// Enable mic
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);

```

### Getting the mic status

This API is used to get the mic status. The returned value 0 indicates that the mic is off, while 1 is on.

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
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To enable a capturing device, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code

```
// Enable capturing device
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);

```

### Getting the capturing device status

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
| --------- | :--: | ------------------------------------------------------------ |
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

### Getting the real-time mic volume

This API is used to get the real-time mic volume. An int-type value in the range of 0-100 will be returned. It is recommended to call this API once every 20 ms.

**This API is not applicable to the voice message service.**

#### Function prototype  

```
ITMGAudioCtrl int GetMicLevel

```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();

```

### Getting the real-time audio upstreaming volume

This API is used to get the local real-time audio upstreaming volume. An int-type value in the range of 0-100 will be returned.

**This API is not applicable to the voice message service.**

#### Function prototype  

```
ITMGAudioCtrl int GetSendStreamLevel()

```

#### Sample code  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();

```

### Setting the mic software volume

This API is used to set the mic volume. The corresponding parameter is `volume`, which is equivalent to attenuating or gaining the captured sound. 0 indicates that the audio is mute, while 100 indicates that the volume remains unchanged. The default value is 100.

**This API is not applicable to the voice message service.**

#### Function prototype  

```
ITMGAudioCtrl SetMicVolume(int volume)

```

| Parameter | Type | Description |
| ------ | :--: | --------------------- |
| volume | int | Sets volume. Value range: 0-200 |

#### Sample code  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);

```

### Getting the mic software volume

This API is used to obtain the microphone volume. An "int" value is returned. Value 101 represents API SetMicVolume has not been called.

**This API is not applicable to the voice message service.**

#### Function prototype  

```
ITMGAudioCtrl GetMicVolume()

```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();

```

## Voice Chat Playback APIs

### [Enabling or disabling the speaker](id:EnableSpeaker)

This API is used to enable/disable the speaker.
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

**EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**

#### Function prototype  

```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)

```

| Parameter | Type | Description |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To disable the speaker, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
// Enable the speaker
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);

```

### Getting the speaker status

This API is used to get the speaker status.

- 0 indicates that the speaker is off.
- 1 indicates that the speaker is on.
- 2 indicates that the speaker is being manipulated.

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
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To disable a playback device, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
// Enable the playback device
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);

```

### Getting the playback device status

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
| --------- | :--: | ------------------------------------------------------------ |
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

### Getting the real-time speaker volume

This API is used to get the real-time speaker volume. An int-type value will be returned to indicate the volume. It is recommended to call this API once every 20 ms.

#### Function prototype  

```
ITMGAudioCtrl GetSpeakerLevel()

```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();

```

### Getting the real-time downstreaming audio levels of other members in room

This API is used to get the real-time audio downstreaming volume of other members in the room. An int-type value will be returned. Value range: 0-200.

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

### Setting the speaker volume

This API is used to set the speaker volume.
The corresponding parameter is volume. 0 indicates that the audio is mute, while 100 indicates that the volume remains unchanged. The default value is 100.

#### Function prototype  

```
ITMGAudioCtrl SetSpeakerVolume(int volume)

```

| Parameter | Type | Description |
| ------ | :--: | -------------------- |
| volume | int | Sets volume. Value range: 0-200 |

#### Sample code  

```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);

```

### Getting the speaker volume

This API is used to get the speaker volume. An int-type value will be returned to indicate the volume. 101 indicates that the `SetSpeakerVolume` API has not been called.
"Level" indicates the real-time volume, and "Volume" the speaker volume. The final volume = Level * Volume%. For example, if the "Level" is 100 and "Volume" is 60, the final volume is "60".

#### Function prototype  

```
ITMGAudioCtrl GetSpeakerVolume()

```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();

```



## Advanced APIs


### Enabling in-ear monitoring

This API is used to enable in-ear monitoring. You need to call `EnableLoopBack+EnableSpeaker` before you can hear your own voice.

#### Function prototype  

```
ITMGContext GetAudioCtrl EnableLoopBack(bool enable)

```

| Parameter | Type | Description |
| ------ | :--: | ------------ |
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
| ----------- | :----: | ----------------------------------------------------- |
| deviceType | int | <li>1: capturing device, <li>2: playback device |
| deviceId | string | Device GUID, which is used to identify a device and only applies to Windows and macOS. |
| openOrClose | bool | Occupies or releases a capturing/playback device |

#### Sample code  

```
Listen on an event:
ITMGContext.GetInstance().GetAudioCtrl().OnDeviceStateChangedEvent += new QAVAudioDeviceStateCallback(OnAudioDeviceStateChange);
Process the event listened on:
void QAVAudioDeviceStateCallback(int deviceType, string deviceId, bool openOrClose){
    // Callback for device occupancy and release
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

### Callback for modifying the room type

#### Function prototype  

```
ITMGContext ITMGRoom public int ChangeRoomType(ITMGRoomType roomtype)

```


| Parameter | Type | Description |
| -------- | :----------: | ----------------------------------------------------- |
| roomtype | ITMGRoomType | Room type to be switched to. For room audio types, please see the `EnterRoom` API. |

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);


```

### Callback for modifying room audio type

Set the room type. After the room type is set, a callback will be executed through a delegate function to pass a message indicating that the modification has been completed.

| Returned Parameter | Description |
| ---------- | :------------------------: |
| roomtype | Updated room type returned |


```
// Delegate function:
public abstract event QAVCallback OnChangeRoomtypeCallback;

// Event function:
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;

```

#### Sample code  

```
// Listen on an event:
ITMGContext.GetInstance ().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent (OnRoomTypeChangedEvent);
// Process the event listened on:
void OnRoomTypeChangedEvent(int roomtype)
{
        ShowWarnning (string.Format ("RoomTypeChanged current:{0}",roomtype));
}


```

### Notification of room type change

Once the room type is modified by you or another user in the room, this callback function will be called to notify the business layer of the room type change. The returned value will be the room type. For more information, please see the `EnterRoom` API.

```
// Delegate function:
public delegate void QAVOnRoomTypeChangedEvent(int roomtype);

// Event function:
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;	

```

#### Sample code  

```
// Listen on an event:
ITMGContext.GetInstance().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent(OnRoomTypeChangedEvent);
// Process the event listened on:
void OnRoomTypeChangedEvent(int roomtype){
    // Send a callback after the room type is changed
}

```



### The monitoring event of room call quality

The message for quality control event triggered once every two seconds after room entry is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `loss`, and `delay`, which represent the following information. The event message will be identified in the `OnEvent` function.

This API is used to monitor the network quality. If the user's network is poor, the business layer will remind the user to switch to a better network through the UI.

| Parameter | Type | Description |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int | Value range: 1-50. 50 indicates excellent sound quality, 1 indicates very poor (barely usable) sound quality, and 0 represents an initial meaningless value. Generally, if the value is below 30, the business layer will remind users that the network is poor and recommend them to switch the network. |
| loss | double | Upstream packet loss rate |
| delay | int | Voice chat delay in ms |


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

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

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
| --------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE | Does not print logs |
| TMG_LOG_LEVEL_ERROR | Prints error logs (default) |
| TMG_LOG_LEVEL_INFO | Prints info logs |
| TMG_LOG_LEVEL_DEBUG | Prints debug logs |
| TMG_LOG_LEVEL_VERBOSE | Prints verbose logs |

#### Sample code  

```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);

```



### Setting the log printing path

This API is used to set the log printing path. The default path is as follows:

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName |
| iOS | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

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

### Getting the diagnostic messages

This API is used to get information on the quality of real-time audio/video calls, which is mainly used to view real-time call quality and troubleshoot and can be ignored on the business side.

#### Function prototype  

```
ITMGRoom GetQualityTips()

```

#### Sample code  

```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();

```

