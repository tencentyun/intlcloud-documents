This document describes how to access and debug GME client APIs for the voice chat feature for Unity.

## Key Considerations for Using GME

GME provides the real-time voice, voice message, and speech-to-text services, which all depend on core APIs such as `Init` and `Poll`.

#### Key notes

- You have created a GME application and obtained the `AppID` and `Key` of the SDK as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- You have **activated the real-time voice, voice message, and speech-to-text services of GME** as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error code, please see <dx-tag-link link="https://intl.cloud.tencent.com/document/product/607/33223" tag="ErrorCode">Error Codes</dx-tag-link>.

## Connecting to the SDK

### Directions

Key processes involved in SDK connection are as follows:

<img src="https://qcloudimg.tencent-cloud.cn/raw/5e05e6ffe1749725a6ba077926286f16.png"  width="70%" /></img>

<dx-steps>
-<dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">Entering a voice chat room</dx-tag-link>
-<dx-tag-link  tag="Callback: QAVEnterRoomComplete">Callback of Room Entry</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">Enabling the microphone</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">Enabling the speaker</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">Exiting a voice room</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">Uninitializing GME</dx-tag-link>
</dx-steps>

### C# classes

| Class | Description |
| ------------------- | :----------------: |
| ITMGContext | Key APIs |
| ITMGRoom | Room APIs |
| ITMGRoomManager | Room management APIs |
| ITMGAudioCtrl | Audio APIs |
| ITMGAudioEffectCtrl | Sound effect and accompaniment APIs |

## Key APIs

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |

### Importing the header file

```
using GME;
```

### Getting an instance

Get the `Context` instance by using the `ITMGContext` method instead of `QAVContext.GetInstance()`.

[](id:Init)
### Initializing the SDK

**You need to initialize the SDK through the `Init` API** before you can use the real-time voice, voice message, and speech-to-text services. The `Init` API must be called in the same thread as other APIs. We recommend you call all APIs in the main thread.

#### API prototype

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | `AppID` provided in the [GME console](https://console.cloud.tencent.com/gamegme), which can be obtained as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0). |
| openID   | string | `openID` can only be in `Int64` type, which is passed in after being converted to a string. You can customize its rules, and it must be unique in the application. To pass in `openID` as a string, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) for application. |

#### Returned values

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0 | Initialized SDK successfully |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

<dx-alert infotype="notice" title="Notes on 7015 error code">

- The 7015 error code is judged by md5. If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.
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

[](id:Poll)
### Triggering event callback

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API is GME's message pump and should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run abnormally. For more information, see the `EnginePollHelper` file in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).

<dx-alert infotype="alarm" title="Calling the `Poll` API periodically">
The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
</dx-alert>

#### API prototype

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

#### API prototype

```
ITMGContext public abstract int Pause()
```

### Resuming the system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### API prototype

```
ITMGContext  public abstract int Resume()
```

[](id:UnInit)
### Uninitializing the SDK

This API is used to uninitialize the SDK to make it uninitialized. **If the game business account is bound to `openid`, switching game account requires uninitializing GME and then using the new `openid` to initialize again.**

#### API prototype

```
ITMGContext public abstract int Uninit()
```

## Voice Chat Room APIs

You should initialize and call the SDK to enter a room before voice chat can start.
If you have any questions when using the service, please see [FAQs About Voice Chat](https://intl.cloud.tencent.com/document/product/607/39524).

![](https://qcloudimg.tencent-cloud.cn/raw/a32a684c9d6f3dd6d9c26b0168e61de6.png)

| API | Description |
| ------------- | :------------------: |
| GenAuthBuffer |     Calculates the local authentication key     |
| EnterRoom     |       Enters a room       |
| ExitRoom      |       Exits the room       |
| IsRoomEntered | Determines whether room entry is successful |
| SwitchRoom    |     Switches the room quickly     |

### Local authentication key calculation

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    

#### API prototype

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)

```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| appId | int | `AppID` from the Tencent Cloud console.|
| roomId | string | Room ID, which can contain up to 127 characters. |
| openId | string | User ID, which is the same as `openID` during initialization.                       |
| key | string | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |

#### Sample code  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
        return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}

```

[](id:EnterRoom)
### Entering a room

This API is used to enter a room with the generated authentication information. The mic and speaker are not enabled by default after room entry.

<dx-alert infotype="alarm" title="Note">
- If the room entry callback result is `0`, the room entry is successful. If `0` is returned from the `EnterRoom` API, it doesn't necessarily mean that the room entry is successful.
- The audio type of the room is determined by the first user entering the room. After that, if a member in the room changes the room type, it will take effect for all members there. For example, if the first user entering the room uses the smooth sound quality, and the second user entering the room uses the HD sound quality, the room audio type of the second user will change to the smooth sound quality. Only after a member in the room calls the `ChangeRoomType` API will the audio type of the room be changed.
</dx-alert>

#### API prototype

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)

```

| Parameter | Type | Description |
| ---------- | :----------: | ------------------------------------------ |
| roomId     |    string    | Room ID, which can contain up to 127 characters.                    |
| roomType   | ITMGRoomType | Room type. We recommend you select `ITMG_ROOM_TYPE_FLUENCY` for games. For more information on room audio types, see [Sound Quality](https://intl.cloud.tencent.com/document/product/607/18522). |
| authBuffer |    Byte[]    | Authentication key                                     |

#### Sample code  

```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);

```

### Callback for room entry

After the user enters the room, the room entry result will be called back, which can be listened on for processing. A successful callback means that the room entry is successful, and the billing **starts**.

<dx-fold-block title="Billing references">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009)
[Billing FAQs](https://intl.cloud.tencent.com/document/product/607/30255)
[Will Voice Chat still be charged when client is offlined?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>

#### API prototype

```
public delegate void QAVEnterRoomComplete(int result, string error_info);
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
		// Entered room successfully
    }
}
```

#### Data details

| Message | Data | Sample |
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM      | result; error_info | {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT                   |                result; error_info                 | {"error_info":"waiting timeout, please check your network","result":0} |

If the network is disconnected, there will be a disconnection callback notification `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`. At this time, the SDK will automatically reconnect, and the callback is `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`. When the reconnection is successful, there will be a callback `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS`.

#### Error codes

| Error Code Value | Cause and Suggested Solution |
| -------- | ------------------------------------------------------------ |
| 7006     | Authentication failed. Possible causes: <li>The `AppID` does not exist or is incorrect.<li>An error occurred while authenticating the `authbuff`.<li>Authentication expired.<li>The `OpenId` does not meet the specification. |
| 7007 | Already in another room. |
| 1001 | The user was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned. |
| 1003 | The user was already in the room and called the room entering API again. |
| 1101 | Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally. |


[](id:ExitRoom)	
### Exiting a room

This API is used to exit the current room. It is an async API. The returned value `AV_OK` indicates a successful async delivery. If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the `EnterRoom` API.

#### API prototype  

```
ITMGContext ExitRoom()
```

#### Sample code  

```
ITMGContext.GetInstance().ExitRoom();
```

#### Callback for room exit

A callback will be executed through a delegate function to pass a message after room exit.

#### API prototype  

```
public delegate void QAVExitRoomComplete();
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

### Determining whether a user has entered a room

This API is used to determine whether the user has entered a room. A value in bool type will be returned. Do not call this API during room entry.

#### API prototype  

```
ITMGContext abstract bool IsRoomEntered()
```

#### Sample code  

```
ITMGContext.GetInstance().IsRoomEntered();
```

### Switching a room

User can call this API to quickly switch the voice chat room after entering the room. After the room is switched, the device is not reset, that is, if the microphone is already enabled in this room, the microphone will keep enabled after the room is switched.
The callback for quickly switching rooms is `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM`, and the fields are `error_info` and `result`.

#### API prototype

```
public abstract int SwitchRoom(string targetRoomID, byte[] authBuffer);
```

#### Type descriptions

| Parameter | Type | Description |
| ------------ | ------ | ------------------------------ |
| targetRoomID | String | ID of the room to enter |
| authBuffer | byte[] | Generates a new authentication with the ID of the room to enter |

## Room Status Maintenance

APIs in this section are used to display speaking members and members entering or exiting the room and mute a member in the room at the business layer.

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

| API/Notification | Description |
| -------------------------------- | :--------------: |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | The member status changed |
| AddAudioBlackList                | Mutes a member in the room |
| RemoveAudioBlackList             |     Unmutes a user     |

### Notification events of member room entry and speaking status

- This event is used to get the user speaking in the room and display the user on the UI, and to send a notification when someone enters or exits the room.
- A notification for this event will be sent only when the status changes. To get the member status in real time, cache the notification when it is received at the business layer. The event message `ITMG_MAIN_EVNET_TYPE_USER_UPDATE` containing `event_id`, `count`, and `openIdList` will be returned, which will be identified in the `OnEvent` notification.
- Notifications of the `EVENT_ID_ENDPOINT_NO_AUDIO` audio event will be sent only when the threshold is exceeded, that is, other members in the room can receive the notification that the local user stops speaking only after the local client captures no voice for two seconds.
- The audio event returns only the member speaking status but not the specific volume level. If you need the specific volume levels of members in the room, you can use the `GetVolumeById` API.

| event_id                     |         Description         | Maintenance         |
| --------------------------- | :---------------------------------------------------: | ---------------------- |
| EVENT_ID_ENDPOINT_ENTER     |         Return the `openid` of the member entering the room.         | Member list     |
| EVENT_ID_ENDPOINT_EXIT      |         Return the `openid` of the member exiting the room.         | Member list     |
| EVENT_ID_ENDPOINT_HAS_AUDIO |     Return the `openid` of the member sending audio packets in the room. This event can be used to determine whether a user is speaking and display the voiceprint effect.     | Chat member list |
| EVENT_ID_ENDPOINT_NO_AUDIO  | Return the `openid` of the member stopping sending audio packets in the room. | Chat member list |

#### Sample code

```
public delegate void QAVEndpointsUpdateInfo(int eventID, int count, [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)]string[] openIdList);
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

### Muting a member in the room

This API is used to add an ID to the audio data blocklist. This operation blocks audio from someone and only applies to the local device without affecting other devices. The returned value `0` indicates that the call is successful. Assume that users A, B, and C are all speaking using their mic in a room: 

- If A blocks C, A can only hear B;
- If B blocks neither A nor C, B can hear both of them;
- If C blocks neither A nor B, C can hear both of them.

This API is suitable for scenarios where a user is muted in a room.

#### API prototype  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```

| Parameter | Type | Description |
| ------ | :----: | ------------------------- |
| openId | String | ID to be blocked openid |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl ().AddAudioBlackList (openId);
```

### Unmuting

This API is used to remove an ID from the audio data blacklist. A returned value of 0 indicates the call is successful.

#### API prototype  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)
```

| Parameter | Type | Description |
| ------ | :----: | ------------------------- |
| openId | String | ID to be unblocked openid |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (openId);
```



## Voice Chat Capturing APIs

- The voice chat APIs can only be called after SDK initialization and room entry.
- When the user clicks the button of enabling/disabling the mic or speaker on the UI, we recommend you call the `EnableMic` or `EnableSpeaker` API.
- To enable the user to press the mic button on the UI to speak and release it to stop speaking, we recommend you call `EnableAudioCaptureDevice` once during room entry and call `EnableAudioSend` to enable the user to speak while pressing the button.

| API | Description |
| --------------------------- | :------------------: |
| EnableMic                   |      Enables/Disables the mic      |
| GetMicState                 |    Gets the mic status    |
| EnableAudioCaptureDevice    |     Enables/Disables the capturing device     |
| IsAudioCaptureDeviceEnabled |   Gets the capturing device status   |
| EnableAudioSend             |   Enables/Disables audio upstreaming   |
| IsAudioSendEnabled          |   Gets the audio upstreaming status   |
| GetMicLevel                 |  Gets the real-time mic volume level  |
| GetSendStreamLevel | Gets real-time audio upstreaming volume |
| SetMicVolume                |    Sets the mic volume level    |
| GetMicVolume                |    Gets the mic volume level    |


[](id:EnableMic)	
### Enabling or disabling mic

This API is used to enable/disable the mic. The mic and speaker are not enabled by default after room entry. **EnableMic = EnableAudioCaptureDevice + EnableAudioSend**

#### API prototype  

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

#### API prototype  

```
ITMGAudioCtrl GetMicState()
```

#### Sample code  

```
micToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### Enabling or disabling the capturing device

This API is used to enable/disable a capturing device. The device is not enabled by default after room entry.

- This API can only be called after room entry. The device will be disabled automatically after room exit.
- Operations such as permission application and volume type adjustment will generally be performed when a capturing device is enabled on a mobile device.

#### API prototype  

```
ITMGAudioCtrl int EnableAudioCaptureDevice(bool isEnabled)
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To enable a capturing device, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code

```
// Enable capturing device
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### Getting the capturing device status

This API is used to get the status of a capturing device.

#### API prototype

```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()
```

#### Sample code

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### Enabling or disabling audio upstreaming

This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, please see the `EnableAudioCaptureDevice` API.

#### API prototype

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To enable audio upstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(true);
```

### Getting the audio upstreaming status

This API is used to get the status of audio upstreaming.

#### API prototype  

```
ITMGAudioCtrl bool IsAudioSendEnabled()
```

#### Sample code  

```
bool IsAudioSend = ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();
```

### Getting the real-time mic volume

This API is used to get the real-time mic volume. An int-type value in the range of 0-100 will be returned. It is recommended to call this API once every 20 ms.

 

#### API prototype  

```
ITMGAudioCtrl int GetMicLevel
```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### Getting the real-time audio upstreaming volume

This API is used to get the local real-time audio upstreaming volume. An int-type value in the range of 0-100 will be returned.

 

#### API prototype  

```
ITMGAudioCtrl int GetSendStreamLevel()
```

#### Sample code  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();
```

### Setting the mic software volume

This API is used to set the mic volume level. The corresponding parameter is `volume`, which is equivalent to attenuating or gaining the captured sound.

 

#### API prototype  

```
ITMGAudioCtrl SetMicVolume(int volume)
```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| volume | int  | Value range: 0–200. Default value: 100. `0` indicates that the audio is mute, while `100` indicates that the volume level remains unchanged. |

#### Sample code  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);
```

### Getting the mic software volume

This API is used to obtain the microphone volume. An "int" value is returned. Value 101 represents API SetMicVolume has not been called.

 

#### API prototype  

```
ITMGAudioCtrl GetMicVolume()
```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();
```

## Voice Chat Playback APIs

| API | Description |
| ------------------------ | :----------------------------: |
| EnableSpeaker            |           Enables/Disables the speaker           |
| GetSpeakerState          |         Gets the speaker status         |
| EnableAudioPlayDevice    |          Enables/Disables the playback device          |
| IsAudioPlayDeviceEnabled | Gets playback device status |
| EnableAudioRecv          |        Enables/Disables audio downstreaming        |
| IsAudioRecvEnabled       |        Gets the audio downstreaming status        |
| GetSpeakerLevel          |       Gets the real-time speaker volume level       |
| GetRecvStreamLevel       | Gets the real-time downstreaming audio volume levels of other members in the room |
| SetSpeakerVolume         |         Sets the speaker volume level         |
| GetSpeakerVolume         |         Gets the speaker volume level         |


[](id:EnableSpeaker)	
### Enabling or disabling the speaker

This API is used to enable/disable the speaker. **EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**

#### API prototype  

```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To disable the speaker, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
// Enable the speaker
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

### Getting the speaker status

This API is used to get the speaker status. 0 indicates that the speaker is off, and 1 is on.

#### API prototype  

```
ITMGAudioCtrl GetSpeakerState()
```

#### Sample code  

```
speakerToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```



### Enabling or disabling the playback device

This API is used to enable/disable a playback device.

#### API prototype  

```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To disable a playback device, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);
```

### Getting the playback device status

This API is used to get the status of a playback device.

#### API prototype

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```

#### Sample code  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### Enabling or disabling audio downstreaming

This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, please see the `EnableAudioPlayDevice` API.

#### API prototype  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To enable audio downstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(true);
```



### Getting audio downstreaming status

This API is used to get the status of audio downstreaming.

#### API prototype  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

#### Sample code  

```
bool IsAudioRecv = ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```

### Getting the real-time speaker volume

This API is used to get the real-time speaker volume. An int-type value will be returned to indicate the volume. It is recommended to call this API once every 20 ms.

#### API prototype  

```
ITMGAudioCtrl GetSpeakerLevel()
```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();
```

### Getting the real-time downstreaming audio levels of other members in the room

This API is used to get the real-time audio downstreaming volume of other members in the room. An int-type value will be returned. Value range: 0-200.

#### API prototype  

```
ITMGAudioCtrl int GetRecvStreamLevel(string openId)
```

| Parameter | Type | Description |
| ------ | :----: | --------------------- |
| openId | string | `openId` of another member in the room |

#### Sample code  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetRecvStreamLevel(openId);
```

### Setting the speaker volume

This API is used to set the speaker volume.

#### API prototype  

```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| volume | int  | Value range: 0–200. Default value: 100. `0` indicates that the audio is mute, while `100` indicates that the volume level remains unchanged. |

#### Sample code  

```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);
```

### Getting the speaker volume

This API is used to get the speaker volume. An int-type value will be returned to indicate the volume. 101 indicates that the `SetSpeakerVolume` API has not been called.
"Level" indicates the real-time volume, and "Volume" the speaker volume. The final volume = Level * Volume%. For example, if the "Level" is 100 and "Volume" is 60, the final volume is "60".

#### API prototype  

```
ITMGAudioCtrl GetSpeakerVolume()
```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();
```

## Device Selection APIs

Device selection APIs can be used only on PC.

| API | Description |
| --------------------------- | :------------------: |
| GetMicListCount             |       Gets the number of mics       |
| GetMicList                  |         Lists mics         |
| GetSpeakerListCount         |       Gets the number of speakers       |
| GetSpeakerList              |         Lists speakers         |
| SelectMic                   |         Selects mics         |
| SelectSpeaker               |         Selects speakers         |

### Getting the number of mics

This API is used to get the number of mics.

#### Function prototype  

```
public abstract int GetMicListCount()

```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicListCount();
```

### Enumerating mics

This API is used together with the `GetMicListCount` API to enumerate mics.

#### Function prototype 

```
public abstract int GetMicList(out List<TMGAudioDeviceInfo> devicesInfo, int count)

```

| Parameter | Type | Description |
| ---------------- | :----------------: | -------------------- |
| ppDeviceInfoList | TMGAudioDeviceInfo | Device list             |
| count           |        int         | The number of mics |

| `TMGAudioDeviceInfo` Parameter | Type | Description |
| ---------------- | :----------------: | ------------------- |
| m_strDeviceID | string | Device name |
| m_strDeviceID | string | Device ID |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicList(devicesInfo,count);
```



### Selecting a mic

This API is used to select a mic. If this API is not called or `DEVICEID_DEFAULT` is passed in, the default mic will be selected.
The 0th device id returned in the GetMicList API is the default device of the call device. If there is a selected call device, it will be maintained by service. If it is unplugged, the call device will be changed back into the default device.

#### Function prototype  

```
public abstract int SelectMic(string micID);
```

| Parameter | Type | Description |
| ------ | :---: | ------------- |
| pMicID | string | Mic ID, which is from the list returned by `GetMicList`. |

#### Sample code  

```
string deviceID = DEVICE_ID_DEFAULT;
                if (index != 0)
                {
                    deviceID = listMicInfo[index - 1].m_strDeviceID;
                }
                ITMGContext.GetInstance().GetAudioCtrl().SelectMic(deviceID);
                selectedMicID = deviceID;
```

This API is used to get the number of speakers.

#### Function prototype  

```
public abstract int GetSpeakerListCount();

```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerListCount();

```

### Enumerating speakers

This API is used together with the `GetSpeakerListCount` API to enumerate speakers.

#### Function prototype  

```
public abstract int GetSpeakerList(out List<TMGAudioDeviceInfo> devicesInfo, int count)
```

| Parameter | Type | Description |
| ---------------- | :----------------: | -------------------- |
| ppDeviceInfoList | TMGAudioDeviceInfo | Device list             |
| count           |        int         | The number of speakers |

| `TMGAudioDeviceInfo` Parameter | Type | Description |
| ---------------- | :----------------: | ------------------- |
| m_strDeviceID | string | Device name |
| m_strDeviceID | string | Device ID |

#### Sample code  

```
int speakerCount = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerListCount();
Debug.LogFormat("speakerCount = {0}", speakerCount);
if (speakerCount > 0)
	{
		int ret = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerList(out listSpeakerInfo, speakerCount);
		Debug.LogFormat("GetSpeakerList ret = {0}", ret);
		if (ret != 0)
		{
			listSpeakerInfo = null;
		}
	}
}
```

### Selecting a speaker

This API is used to select a playback device. If this API is not called or `DEVICEID_DEFAULT` is passed in, the default playback device will be selected.

#### Function prototype  

```
public abstract int SelectSpeaker(string speaker);

```

| Parameter | Type | Description |
| ---------- | :---: | ------------- |
| speaker | string | Speaker ID, which is from the list returned by `GetSpeakerList`. |

#### Sample code  

```
speakerDropdown = transform.Find("DevicePanel/SpeakerSelect").GetComponent<Dropdown>();
        if (speakerDropdown != null)
        {
            speakerDropdown.onValueChanged.AddListener(delegate (int index)
            {
                string deviceID = DEVICE_ID_DEFAULT;
                if (index != 0)
                {
                    deviceID = listSpeakerInfo[index - 1].m_strDeviceID;
                }
                ITMGContext.GetInstance().GetAudioCtrl().SelectSpeaker(deviceID);
                selectedSpeakerID = deviceID;
            });
        }
```


## Advanced APIs

### Enabling in-ear monitoring

This API is used to enable in-ear monitoring. You need to call `EnableLoopBack+EnableSpeaker` before you can hear your own voice.

#### API prototype  

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
public delegate void QAVOnDeviceStateChangedEvent(int deviceType, string deviceId, bool openOrClose);
public abstract event QAVOnDeviceStateChangedEvent OnDeviceStateChangedEvent;
```

| Parameter | Type | Description |
| ----------- | :----: | ----------------------------------------------------- |
| deviceType  |  int   | <li>1: Capturing device<li>2: Playback device                  |
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

### Getting a user's room audio type

This API is used to get a user's room audio type. The returned value is the room audio type. Value 0 indicates that an error occurred while getting the user's room audio type. For room audio types, please see the `EnterRoom` API.

#### API prototype  

```
ITMGContext ITMGRoom public int GetRoomType()
```

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().GetRoomType();
```

### Changing the room type

This API is used to modify a user's room audio type. For the result, please see the callback event. The event type is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE`. The audio type of the room is determined by the first user to enter the room. After that, if a member in the room changes the room type, it will take effect for all members there.
#### API prototype  

```
ITMGContext ITMGRoom public int ChangeRoomType(ITMGRoomType roomtype)
```

| Parameter | Type | Description |
| -------- | :----------: | ----------------------------------------------------- |
| roomtype | ITMGRoomType | Room type to be switched to. For room audio types, see the `EnterRoom` API.  |

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```

#### Callback event

Set the room type. After the room type is set, a callback will be executed through a delegate function to pass a message indicating that the modification has been completed.

| Returned Parameter | Description |
| ---------- | :------------------------: |
| roomtype | Updated room type returned |

```
public abstract event QAVCallback OnChangeRoomtypeCallback;
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

#### Notification of room type change

Once the room type is changed by you or another user in the room, this notification event will be used to notify the business layer of the room type change. The returned value will be the room type. For more information, see the `EnterRoom` API.

```
public delegate void QAVOnRoomTypeChangedEvent(int roomtype);
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

This is the quality monitoring event used to listen on the network quality. If your network conditions are poor, the business layer will ask you to switch the network through the UI. This event is triggered once every two seconds after room entry, and its message is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `loss`, and `delay`, which are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int | Value range: 1-50. 50 indicates excellent sound quality, 1 indicates very poor (barely usable) sound quality, and 0 represents an initial meaningless value. Generally, if the value is below 30, the business layer will remind users that the network is poor and recommend them to switch the network. |
| loss   | double | Upstream packet loss rate |
| delay | int | Voice chat delay in ms |




### Getting the version number

This API is used to get the SDK version number for analysis.

#### API prototype

```
ITMGContext  abstract string GetSDKVersion()
```

#### Sample code  

```
ITMGContext.GetInstance().GetSDKVersion();
```



### Setting the log printing level

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### API prototype

```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | Sets the level of logs to be written. `TMG_LOG_LEVEL_NONE` indicates not to write. Default value: TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | Sets the level of logs to be printed. `TMG_LOG_LEVEL_NONE` indicates not to print. Default value: TMG_LOG_LEVEL_ERROR |

`ITMG_LOG_LEVEL` is as detailed below:

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

This API is used to set the log printing path. The default path is as follows. It needs to be called before Init.

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName |
| iOS | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files |
| Mac | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

#### API prototype

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

#### API prototype  

```
ITMGRoom GetQualityTips()
```

#### Sample code  

```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();

```
