This document describes how to access and debug GME client APIs for the multi-voice chat room feature for Unity.

## Key Considerations for Using GME

GME provides the real-time voice, voice message, and speech-to-text services, which all depend on core APIs such as `Init` and `Poll`. The multi-voice chat room feature incorporates the following changes compared with the general room entry feature of GME:

1. To use the multi-voice chat room feature, you need to contact GME developers to get the GME SDK supporting this feature.
2. To enable the multi-voice chat room feature, you need to call the advanced API before `Init`.
3. You need to use `ITMGContext.GetSubInstance("roomid")` to call the APIs for room entry and operations in a room.
4. `roomid` in the ITMGContext.GetSubInstance("roomid") instance indicates the room to be manipulated.
5. All callbacks are returned in the `OnEvent` event.
6. For the billing mode of the multi-voice chat room feature, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009).



## Connecting to the SDK

### Preparations
- You have created a GME application and obtained the `AppID` and `Key` of the SDK as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- You have **activated the real-time voice, voice message, and speech-to-text services of GME** as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- Configure your project before using GME; otherwise, the SDK will not take effect.

### Notes
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error codes, see <dx-tag-link link="https://intl.cloud.tencent.com/document/product/607/33223" tag="ErrorCode">Error Codes</dx-tag-link>.

### Directions

Key processes involved in SDK connection are as follows:

<img src="https://qcloudimg.tencent-cloud.cn/raw/a69ce208fb05dd336ad6618264caf6c2.jpg"  width="70%" /></img>

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
using TencentMobileGaming;
```

### Getting an instance

Get the `Context` instance by using the `ITMGContext.GetInstance()` method instead of `QAVContext.GetInstance()`.

When using the multi-voice chat room feature, you need to use `ITMGContext.GetSubInstance(sRoomID)` to get an instance. Different `Roomid` values indicate different instances and rooms. For example, you can get instance A/B to enter room A/B and use the instance to enable the mic and speaker in room A/B.

>!One instance can enter only one room; for example, `ITMGContext.GetSubInstance("1")` can only enter room 1.

### Using the multi-voice chat room feature

To use the multi-voice chat room feature, you need to call the `SetAdvanceParams` API before `Init`.

```
ITMGContext.GetInstance().SetAdvanceParams("enableMulRoom", "1");
```

### [Initializing the SDK](id:Init)

**You need to initialize the SDK through the `Init` API** before you can use the real-time voice, voice message, and speech-to-text services.

#### Function prototype

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | `AppID` provided in the [GME console](https://console.cloud.tencent.com/gamegme), which can be obtained as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0). |
| openID   | string | `openID` can only be in `Int64` type, which is passed in after being converted to a string. You can customize its rules, and it must be unique in the application. |

#### Returned values

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0 | Initialized SDK successfully |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.

<dx-alert infotype="notice" title="Notes on 7015 error code">
<ul style="margin:0;">
<li>The error code 7015 is identified based on the MD5 value. If this error is reported during connection, check the integrity and version of the SDK file as prompted.</li>
<li>Due to the third-party enhancement, the Unity packaging mechanism, and other factors, the MD5 value of the library file will be affected, resulting in misjudgment. Therefore, <b>ignore this error in the logic for official releases</b>, and avoid displaying it on the UI.</li>
</ul>
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

<dx-alert infotype="notice" title="Note on Init API">
<ul style="margin:0;">
<li>If you need to use the real-time voice and voice message services at the same time, <b>you only need to call the `Init` API once</b>.</li>
<li>Billing will not start after initialization. After you call the <dx-tag-link link="#EnterRoom" tag="API: EnterRoom">EnterRoom</dx-tag-link> API to enter the room successfully, billing will start.</li>
<li>If a user enters two rooms at the same time in the application, the durations in the rooms will be added up for billing. For example, if user A enters voice rooms X and Y at 12:00 and exits them at 12:40, the total voice chat duration will be 80 minutes (40 minutes in each voice room).</li>
<li>The SDK must be initialized before a user can enter a voice chat room.</li>
<li>The `Init` API must be called in the same thread as other APIs. We recommend you call all APIs in the main thread.</li>
</ul>
</dx-alert>

### [Triggering an event callback](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API is GME's message pump and should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run abnormally. For more information, see the `EnginePollHelper` file in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).

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

When a `Pause` event occurs in the system, the engine should also be notified for pause. For example, when the application switches to the background (OnApplicationPause, isPause=True), and you don't need the background to play back the audio in the room, you can call the `Pause` API to pause the GME service.

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

### [Uninitializing the SDK](id:UnInit)

This API is used to uninitialize the SDK to make it uninitialized. **If the game business account is bound to `openid`, switching game account requires uninitializing GME and then using the new `openid` to initialize again.**

#### Function prototype

```
ITMGContext public abstract int Uninit()

```

## Voice Chat Room APIs

You should initialize and call the SDK to enter a room before voice chat can start.
If you have any questions when using the service, please see [FAQs About Voice Chat](https://intl.cloud.tencent.com/document/product/607/39524).

| API | Description |
| -------------- | :------------------: |
| GenAuthBuffer | Initializes authentication |
| EnterRoom | Enters room |
| IsRoomEntered | Indicates whether room entry is successful |
| ExitRoom | Exits room |
| ChangeRoomType | Modifies user's room audio type |
| GetRoomType | Gets user's room audio type |

### Multi-voice chat room call flowchart
<img src="https://qcloudimg.tencent-cloud.cn/raw/da14cd0db1c7efde6659120ba07e1e9c.jpg" width="70%"/>


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
| openId | string | User ID, which is the same as `openID` during initialization.                       |
| key | string | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |

#### Sample code  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
        return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}

```

### [Entering a room](id:EnterRoom)

Use the `GetSubInstance` API to enter a room with the generated authentication information. The mic and speaker are not enabled by default after room entry. The returned value `AV_OK` indicates successful API call but not successful room entry.

#### Function prototype

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)

```

| Parameter | Type | Description |
| ---------- | :----------: | ------------------------------------------ |
| roomId     |    string    | Room ID, which can contain up to 127 characters.                    |
| roomType   | ITMGRoomType | Just enter `ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY` |
| authBuffer |    Byte[]    | Authentication key                                     |

#### Sample code  

```
// Enter the first room
ITMGContext.GetSubInstance("room1").EnterRoom("room1", ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);
// Enter the second room
ITMGContext.GetSubInstance("room2").EnterRoom("room2", ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);

```

### Callback for room entry

After the user enters the room, the room entry result will be returned through the `OnEvent` callback. The result contains the ID of the room where the event occurs and can be listened on for processing. If a success is called back, it means that the room entry is successful, and the billing **starts**.

<dx-fold-block title="Billing references">
For the billing mode of the multi-voice chat room feature, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009).
[Billing FAQs](https://intl.cloud.tencent.com/document/product/607/30255)
[Will Voice Chat still be charged when client is offlined?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>

#### Sample code  

```
// Listen on an event:
ITMGContext.GetInstance().onEventCallBack += new QAVOnEventCallBack(OnEvent);

// Room entry callback in `JsonData` format
string roomID = string.Empty;
JsonData root = JsonMapper.ToObject(data);
if (root != null && root.ContainsKey("roomID")) 

// Process the listening event
void OnEvent(int eventType, int subEventType, string data)
{
	string roomID = string.Empty;
	JsonData root = JsonMapper.ToObject(data);
	if (root != null && root.ContainsKey("roomID"))
	{
		if (root["roomID"] != null)
		{
			roomID = root["roomID"].ToString();
		}
	}
		
	switch (eventType)
	{
		case (int)ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
			OnEnterRoomComplete(0, "");
		}
		break;
	}
}

```

#### Data details

| Message | Data | Sample |
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM      | result; error_info | {"error_info":"","result":0,"roomID":""}                     |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT                   |                result; error_info                 | {"error_info":"waiting timeout, please check your network","result":0} |

If the network is disconnected, there will be a disconnected callback prompt `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`. At this time, the SDK will automatically reconnect, and the callback is `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`. When the reconnection is successful, there will be a callback `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS`.

#### Error codes

| Error Code Value | Cause and Suggested Solution |
| -------- | ------------------------------------------------------------ |
| 7006     | Authentication failed. Possible causes:<ul style="margin:0;"><li>The `AppID` does not exist or is incorrect.</li><li>An error occurred while authenticating the `authbuff`.</li><li>Authentication expired.</li><li>The `OpenId` does not meet the specification.</li></ul> |
| 7007 | Already in another room. |
| 1001 | The user was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned. |
| 1003 | The user was already in the room and called the room entering API again. |
| 1101 | Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally. |

### [Exiting the room](id:ExitRoom)

This API is called to exit the current room. It is an async API. The returned value of `AV_OK` indicates a successful async delivery.

If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the `EnterRoom` API.

#### Function prototype  

```
ITMGContext ExitRoom()

```

#### Sample code  

```
ITMGContext.GetSubInstance("room1").ExitRoom();

```

### Callback for room exit

A callback will be executed through a delegate function to pass a message after room exit.

#### Sample code  

```
// Listen on an event:
ITMGContext.GetInstance().onEventCallBack += new QAVOnEventCallBack(OnEvent);

// Process the listening event
void OnEvent(int eventType, int subEventType, string data)
{
	string roomID = string.Empty;
	JsonData root = JsonMapper.ToObject(data);
	if (root != null && root.ContainsKey("roomID"))
	{
		if (root["roomID"] != null)
		{
			roomID = root["roomID"].ToString();
		}
	}
		
	case (int)ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
	{
		if (mMulForbiddedMembers.ContainsKey(roomID))
		{
			mMulForbiddedMembers.Remove(roomID);
		}

		if (mMulSpeakingMembers.ContainsKey(roomID))
		{
			mMulSpeakingMembers.Remove(roomID);
		}
	}
	break;
}

```

### Notifications of member room entry and speaking status

This API is used to obtain the user speaking in the room and display it in the UI, and to send a notification when someone entering or exiting the room.

A notification for this event will be sent only when the status changes. To get member status in real time, cache the notification when it is received at the upper layer. The event message `ITMG_MAIN_EVNET_TYPE_USER_UPDATE` containing `event_id`, `count`, and `openIdList` will be returned. The event message will be identified in the `OnEvent` function.
Notifications for audio events are subject to a threshold, and a notification will be sent only when this threshold is exceeded. The notification "A member has stopped sending audio packets" will be sent if no audio packets are received in more than two seconds. This event only returns the member speaking event but not the specific volume level. If you need the specific volume levels of members in the room, use the `GetVolumeById` API.

| event_id                    |                          Description                           | Maintenance         |
| --------------------------- | :-----------------------------------------------------: | ---------------------- |
| EVENT_ID_ENDPOINT_ENTER | Return all `openid` values when a member enters the room. | Member list |
| EVENT_ID_ENDPOINT_EXIT | Return all `openid` values when a member exits the room. | Member list |
| EVENT_ID_ENDPOINT_HAS_AUDIO | Return the `openid` of all members speaking in the room when a member sends audio packets. | Chat member list |
| EVENT_ID_ENDPOINT_NO_AUDIO | Return all the openid that stop chatting when a member stops sending audio packets | Chat member list |

#### Room member maintenance flowchart

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

#### Sample code

```
// Listen on an event:
ITMGContext.GetInstance().onEventCallBack += new QAVOnEventCallBack(OnEvent);

// Process the listening event
void OnEvent(int eventType, int subEventType, string data)
{
	string roomID = string.Empty;
	JsonData root = JsonMapper.ToObject(data);
	if (root != null && root.ContainsKey("roomID"))
	{
		if (root["roomID"] != null)
		{
			roomID = root["roomID"].ToString();
		}
	}
		
	case (int)ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
	{
		UserListInfo userListInfo = JsonUtility.FromJson<UserListInfo>(data);
		if (userListInfo.event_id == QAVContext.EVENT_ID_ENDPOINT_HAS_AUDIO)
		{
			foreach (string openId in userListInfo.user_list)
			{
				if (!mMulSpeakingMembers.ContainsKey(roomID))
                      {
					mMulSpeakingMembers.Add(roomID, new HashSet<string>());
				}
				mMulSpeakingMembers[roomID].Add(openId);
			}
		}
		else if (userListInfo.event_id == QAVContext.EVENT_ID_ENDPOINT_NO_AUDIO)
		{
			foreach (string openId in userListInfo.user_list)
			{
				if (mMulSpeakingMembers.ContainsKey(roomID)
					&& mMulSpeakingMembers[roomID]!= null
					&& mMulSpeakingMembers[roomID].Contains(openId))
				{
					mMulSpeakingMembers[roomID].Remove(openId);
				}
			}
		}
	}
	break;

}

```

### Muting in a room

This API is used to add an ID to the audio data blocklist. This operation blocks audio from someone and only applies to the local device without affecting other devices. The returned value `0` indicates that the call is successful. Assume that users A, B, and C are all speaking using their mic in a room: 

- If A blocks C, A can only hear B;
- If B blocks neither A nor C, B can hear both of them;
- If C blocks neither A nor B, C can hear both of them.

This API is suitable for scenarios where a user is muted in a room.

#### Function prototype  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)

```

| Parameter | Type | Description |
| ------ | :----: | ------------------------- |
| openId | String | ID to be blocked openid |

#### Sample code  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl ().AddAudioBlackList (openId);

```

### Unmuting

This API is used to remove an ID from the audio data blacklist. A returned value of 0 indicates the call is successful.

#### Function prototype  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)


```

| Parameter | Type | Description |
| ------ | :----: | ------------------------- |
| openId | String | ID to be unblocked openid |

#### Sample code  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl ().RemoveAudioBlackList (openId);


```



## Voice Chat Capturing APIs

### [Enabling or disabling the mic](id:EnableMic)

This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.

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
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableMic(true);
```

### Getting the mic status

This API is used to get the mic status. The returned value 0 indicates that the mic is off, while 1 is on.

#### Function prototype  

```
ITMGAudioCtrl GetMicState()
```

#### Sample code  

```
micToggle.isOn = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetMicState();
```

### Enabling or disabling the capturing device

This API is used to enable/disable a capturing device. The device is not enabled by default after room entry.

- This API can only be called after room entry. The device will be disabled automatically after room exit.
- Operations such as permission application and volume type adjustment will generally be performed when a capturing device is enabled on a mobile device.

#### Function prototype  

```
ITMGAudioCtrl int EnableAudioCaptureDevice(bool isEnabled)


```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To enable a capturing device, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code

```
// Enable capturing device
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableAudioCaptureDevice(true);


```

### Getting the capturing device status

This API is used to get the status of a capturing device.

#### Function prototype

```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()


```

#### Sample code

```
bool IsAudioCaptureDevice = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().IsAudioCaptureDeviceEnabled();


```

### Enabling or disabling audio upstreaming

This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, please see the `EnableAudioCaptureDevice` API.

#### Function prototype

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)


```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To enable audio upstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableAudioSend(true);


```

### Getting the audio upstreaming status

This API is used to get the status of audio upstreaming.

#### Function prototype  

```
ITMGAudioCtrl bool IsAudioSendEnabled()


```

#### Sample code  

```
bool IsAudioSend = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().IsAudioSendEnabled();


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
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetMicLevel();


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
int Level = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetSendStreamLevel();
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
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().SetMicVolume (micVol);
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
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetMicVolume();
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

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To disable the speaker, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
// Enable the speaker
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableSpeaker(true);
```

### Getting the speaker status

This API is used to get the speaker status. 0 indicates that the speaker is off, and 1 is on.

#### Function prototype  

```
ITMGAudioCtrl GetSpeakerState()
```

#### Sample code  

```
speakerToggle.isOn = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetSpeakerState();
```



### Enabling or disabling the playback device

This API is used to enable/disable a playback device.

#### Function prototype  

```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To disable a playback device, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
// Enable the playback device
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableAudioPlayDevice(true);
```

### Getting the playback device status

This API is used to get the status of a playback device.

#### Function prototype

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```

#### Sample code  

```
bool IsAudioPlayDevice = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### Enabling or disabling audio downstreaming

This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, please see the `EnableAudioPlayDevice` API.

#### Function prototype  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To enable audio downstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableAudioRecv(true);
```



### Getting the audio downstreaming status

This API is used to get the status of audio downstreaming.

#### Function prototype  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

#### Sample code  

```
bool IsAudioRecv = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().IsAudioRecvEnabled();
```

### Getting the real-time speaker volume

This API is used to get the real-time speaker volume. An int-type value will be returned to indicate the volume. It is recommended to call this API once every 20 ms.

#### Function prototype  

```
ITMGAudioCtrl GetSpeakerLevel()
```

#### Sample code  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetSpeakerLevel();
```

### Getting the real-time downstreaming audio levels of other members in the room

This API is used to get the real-time audio downstreaming volume of other members in the room. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGAudioCtrl int GetRecvStreamLevel(string openId)
```

| Parameter | Type | Description |
| ------ | :----: | --------------------- |
| openId | string | `openId` of another member in the room |

#### Sample code  

```
int Level = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetRecvStreamLevel(openId);
```

### Setting the speaker volume

This API is used to set the speaker volume.
The corresponding parameter is volume. 0 indicates that the audio is mute, while 100 indicates that the volume remains unchanged. The default value is 100.

#### Function prototype  

```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```

| Parameter | Type | Description |
| ------ | :--: | --------------------- |
| volume | int | Sets volume. Value range: 0-200 |

#### Sample code  

```
int speVol = (int)(value * 100);
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().SetSpeakerVolume(speVol);
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
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetSpeakerVolume();
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
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableLoopBack(true);
```

### The monitoring event of room call quality

The message for quality control event triggered once every two seconds after room entry is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `loss`, and `delay`, which represent the following information. The event message will be identified in the `OnEvent` function.

This API is used to monitor the network quality. If the user's network is poor, the business layer will remind the user to switch to a better network through the UI.

| Parameter | Type | Description |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int | Value range: 1-50. 50 indicates excellent sound quality, 1 indicates very poor (barely usable) sound quality, and 0 represents an initial meaningless value. Generally, if the value is below 30, the business layer will remind users that the network is poor and recommend them to switch the network. |
| loss | double | Upstream packet loss rate |
| delay | int | Voice chat delay in ms |

### Getting the version number

This API is used to get the SDK version number for analysis.

#### Function prototype

```
ITMGContext  abstract string GetSDKVersion()
```

#### Sample code  

```
ITMGContext.GetInstance().GetSDKVersion();
```





### Setting the log printing level

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

`TMG_LOG_LEVEL` description:

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
