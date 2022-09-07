This document describes GME APIs for Unreal Engine voice chat.



<dx-alert infotype="explain" title="">
This document applies to GME SDK version 2.8.
</dx-alert>



## Considerations

GME provides voice chat, voice messaging and speech-to-text services, which all require key APIs such as `Init` and `Poll`.

<dx-alert infotype="notice" title="Note on Init API">
You **only need to call `Init` API once** no matter how many GME services you want to use.
Calling `Init` does not trigger billing. The billing starts when the <dx-tag-link link="#EnterRoom" tag="EnterRoom">EnterRoom</dx-tag-link> API is called and users enter the room successfully.
</dx-alert>

![image](https://main.qcloudimg.com/raw/99d612d90268a7248f5b55c385eeb8b8.png)

### Process

<dx-steps>
-<dx-tag-link link="#Init" tag="API: Init">Initialize GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="API: Poll">Periodically trigger event callbacks</dx-tag-link>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">Enter a voice chat room</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">Turn on the microphone</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">Turn on the speaker</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">Exit a voice room</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">Uninitialize GME SDK</dx-tag-link>
</dx-steps>

### Important

- Configure your project before using GME
- If the API is called successfully, the response should be `AV_OK=0`.
- GME APIs should be called in the same thread.
- Call `Poll` periodically to trigger event callbacks.
- For error codes, see <dx-tag-link link="https://intl.cloud.tencent.com/document/product/607/33223" tag="ErrorCode">Error Codes</dx-tag-link>.

### C++ classes

| Class | Description |
| ------------------- | :----------------: |
| ITMGContext | Key APIs |
| ITMGRoom | Room APIs |
| ITMGRoomManager | Room management APIs |
| ITMGAudioCtrl | Audio APIs |
| ITMGAudioEffectCtrl | Sound effect and accompaniment APIs |

## Key APIs

To use GME services, you need to call `Init` API to initialize the SDK.

**Call `Init` before calling any other GME APIs.**

For usage issues, see [General FAQs](https://intl.cloud.tencent.com/document/product/607/30254).

| API | Description |
| ------ | :----------: |
| Init | Initializes GME SDK |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME SDK |

<dx-alert infotype="notice" title="">
If you need to switch the account, call `UnInit` to uninitialize the SDK. Calling `Init` is free of charge.
</dx-alert>



### Preparations

Before accessing to GEM, you need to add the header file `tmg_sdk.h`. The classes in the header file inherit `ITMGDelegate` for message delivery and callback.

#### Sample code  

```
#include "tmg_sdk.h"

class UEDEMO1_API AUEDemoLevelScriptActor : public ALevelScriptActor, public ITMGDelegate
{
public:
...
private:
...
｝
```

### Setting singleton

You need to get `ITMGContext` first before you can call the `EnterRoom` function, because all calls begin with `ITMGContext` and callbacks are passed to the application through `ITMGDelegate`.

#### Sample code 

```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```

### Message delivery

The API class uses the `Delegate` method to send callback notifications to the application. `ITMG_MAIN_EVENT_TYPE` indicates the message type. The data on Windows is in json string format. For the key-value pairs, please see the relevant documentation.

#### Sample code  

```
// Function implementation:
//UEDemoLevelScriptActor.h:
class UEDEMO1_API AUEDemoLevelScriptActor : public ALevelScriptActor, public SetTMGDelegate
{
public:
	void OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data);
｝

//UEDemoLevelScriptActor.cpp:
void AUEDemoLevelScriptActor::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data){
	// Identify the eventType here
}
```

### [Init](id:Init)

- This API is used to initialize the GME service. You need to call it before using GME. No fee is incurred for calling this API.
- **For more information on how to get the `sdkAppID`, see [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0)**.
- **The openID is the unique ID of a user. Only INT64 is supported. The generation rule of the openID is customized by the app developer**.



<dx-alert infotype="notice" title="">
 - The SDK must be initialized before a user can enter a voice chat room.
 - The Init API must be called in the same thread with other APIs. It is recommended to call all APIs in the main thread.
</dx-alert>



#### Function prototype

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

| Parameter     |    Type     | Description                                                         |
| -------- | :---------: | ------------------------------------------------------------ |
| sdkAppId | const char* | `AppID` provided by GME. You can check it in the [GME console](https://console.cloud.tencent.com/gamegme) |
| openId | const char* | It must in Int64, which is passed after being converted to a const char*. |

#### Response

| Response | Description |
| ------------------------------- | --------------------------------------------- |
| AV_OK = 0                  | Initialized SDK successfully. |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | The SDK file is not complete. It’s recommended to delete the file and import again. |

`AV_ERR_SDK_NOT_FULL_UPDATE` is only a reminder. It does not indicate that the initialization is failed.

<dx-alert infotype="notice" title="7015 error code">

- md5. If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- false positive As the MD5 string can be affected by the third-party reinforcement, Unity packaging mechanism and other factors, the md5 of the library file will be affected, resulting in misjudgment. **Ignore this error for official release**, and try to avoid displaying it in the UI.
  </dx-alert>



#### Sample code 

```
std::string appid = TCHAR_TO_UTF8(CurrentWidget->editAppID->GetText().ToString().operator*());
std::string userId = TCHAR_TO_UTF8(CurrentWidget->editUserID->GetText().ToString().operator*());
ITMGContextGetInstance()->Init(appid.c_str(), userId.c_str());
```

### [Poll](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
For details, please see UEDemoLevelScriptActor.cpp file in [Demo](https://intl.cloud.tencent.com/document/product/607/18521).

<dx-alert infotype="alarm" title="Important">
Call `Poll` periodically in the main thread to avoid abnormal API callbacks.
</dx-alert>



#### Function prototype

```
class ITMGContext {
protected:
    virtual ~ITMGContext() {}

public:        
    virtual void Poll()= 0;
}
```

#### Sample code

```
// Declaration in the header file
virtual void Tick(float DeltaSeconds);

void AUEDemoLevelScriptActor::Tick(float DeltaSeconds) {
	Super::Tick(DeltaSeconds);	
	ITMGContextGetInstance()->Poll();
}
```

### Pause

When a `Pause` event occurs in the system, the engine should also be notified for pause. If you do not need the background to play back the audio in the room, please call `Pause` API to pause the GME service.

#### Function prototype

```
ITMGContext int Pause()
```

### Resume

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### Function prototype

```
ITMGContext int Resume()

```



### [UnInit](id:UnInit)

This API is used to uninitialize the SDK. **It’s required when you need to switch the account**.

#### Function prototype

```
ITMGContext int Uninit()

```

## Voice Chat

Voice chat refers to the one-to-one or one-to-many real-time voice call feature.

### Voice chat flowchart

![](https://main.qcloudimg.com/raw/28a13d4beccdfecb0ad7530008ec8da0.png)





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

### Voice chat room call flowchart

![](https://main.qcloudimg.com/raw/2b5d8f7f7f4b4b3fbce8c9ebf01f78d8.png)

### GenAuthBuffer

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    

#### Function prototype

```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);

```

| Parameter         | Type  | Description                                                         |
| ------------- | :---: | ------------------------------------------------------------ |
| dwSdkAppID    |  int  | `AppId`. You can check it in the GME console   |
| strRoomID     | char* | Room ID, which can contain up to 127 characters. |
| strOpenID     | char* | ID of the user. It’s the same as the `openID` used in `Init`. |
| strKey        | char* | Authentication key. You can check it in the [GME console](https://console.cloud.tencent.com/gamegme) |
| strAuthBuffer | char* | Returned `authbuff`                                              |
| bufferLength  |  int  | Length of the `authbuff` passed in. 500 is recommended.                             |



#### Sample code  

```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);

```



### [EnterRoom](id:EnterRoom)

When a user enters a room with the generated authentication information, the callback `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` is sent. The returned value of `AV_OK` indicates a success. Mic and speaker are not enabled by default. 

The audio type of the room defaults to the audio type carried by the first user. Users who enter the room later are changed to the default type automatically, regardless of their original audio types. The audio type of the room is only changed when someone in the room calls `ChangeRoomType`.

For more information about room audio types, see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).

#### Function prototype

```
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)

```

| Parameter       |      Type      | Description                    |
| ---------- | :------------: | ----------------------- |
| roomId     |     char*      | Room ID, which can contain up to 127 characters |
| roomType   | ITMG_ROOM_TYPE | Room audio type            |
| authBuffer |     char*      | Authentication                   |
| buffLen    |      int       | Authentication key length              |



#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);

```

### EnterRoom Callback

After the user enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function for callback and processing. A successful callback means that the room entry is successful, and the billing starts.

<dx-fold-block title="Billing references">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/36276)
[Billing FAQs](https://intl.cloud.tencent.com/document/product/607/30255)
[Will Voice Chat still be charged when the client goes offline?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>


#### Sample code  

```
void UBaseViewController::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char *data) {

	FString jsonData = FString(UTF8_TO_TCHAR(data));
	TSharedPtr<FJsonObject> JsonObject;
	TSharedRef<TJsonReader<>> Reader = TJsonReaderFactory<>::Create(FString(UTF8_TO_TCHAR(data)));
	FJsonSerializer::Deserialize(Reader, JsonObject);


	if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM) {
		int32 result = JsonObject->GetIntegerField(TEXT("result"));
		FString error_info = JsonObject->GetStringField(TEXT("error_info"));
		if (result == 0) {
			GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, TEXT("Enter room success."));
		}
		else {
			FString msg = FString::Printf(TEXT("Enter room failed. result=%d, info = %ls"), result, *error_info);
			GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, *msg);
		}
		onEnterRoomCompleted(result, error_info);
	}
}

```

#### Data details

| Message | Data | Sample |
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM      | result; error_info | {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | result; error_info | {"error_info":"waiting timeout, please check your network","result":0} |

If the network is disconnected, there will be a callback message `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`. Upon receiving of this message, the SDK tries to reconnect with the callback message `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`. When the reconnection is successful, there will be a callback `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS`.

#### Error codes

| Code | Cause and Suggested Solution |
| -------- | ------------------------------------------------------------ |
| 7006 | Authentication failed <li>The `AppID` does not exist or is incorrect.<li>An error occurred while authenticating the `authbuff`.<li>Authentication expired.<li>The `OpenId` does not meet the specification. |
| 7007 | The user is already in another room. |
| 1001 | The user entering a room. It is recommended not to call `EnterRoom` repeatedly until the EnterRoom callback is returned. |
| 1003 | The user is already in the room. |
| 1101 | Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally. |

### [ExitRoom](id:ExitRoom)

This API is called to exit the current room. It is an async API. The reponse `AV_OK` indicates that the task is triggered.



<dx-alert infotype="notice" title="">
For the scenario that a user exits the room and enters again immediately, it’s recommended to set the flow to call `EnterRoom` directly without waiting for the callback `RoomExitComplete` from `ExitRoom`.
</dx-alert>



#### Function prototype  

```
ITMGContext virtual int ExitRoom()

```

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();

```

### ExitRoom Callback

After the user exits a room, a callback is returned with the message `ITMG_MAIN_EVENT_TYPE_EXIT_ROOM`.

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
		{
		// Start processing
		break;
		}
	}
}

```

### IsRoomEntered

This API is used to determine whether the user has entered a room. A bool-type value will be returned. The call is invalid during the process of room entry.

#### Function prototype  

```
ITMGContext virtual bool IsRoomEntered()

```

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->IsRoomEntered();

```



### Member status change

This API is used to obtain the user speaking in the room and display it in the UI, and to send a notification when someone enters or exits the room.
Notification for this event will be sent only when the status changes. To get member status in real time, cache the notification when it is received at an upper layer. The event message is `ITMG_MAIN_EVNET_TYPE_USER_UPDATE`, where the data contains `event_id` and `user_list`. The event message will be identified in the `OnEvent` function.
Audio events are triggered when the threshold is reached. `ITMG_EVENT_ID_USER_NO_AUDIO` is triggered when there are no audio packets from a user for over two seconds.

| event_id | Description | Maintenance |
| ---------------------------- | :----------------------------------------------------------: | ---------------------- |
| ITMG_EVENT_ID_USER_ENTER | A user enters the room | Member list |
| ITMG_EVENT_ID_USER_EXIT | A use exits the room | Member list |
| ITMG_EVENT_ID_USER_HAS_AUDIO | A user sends audio packets. This event can be used to determine whether a user is speaking and display the voiceprint effect | Chat member list |
| ITMG_EVENT_ID_USER_NO_AUDIO | A user stops sending audio packets | Chat member list |

#### Room member maintenance flowchart

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

#### Sample code

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		// Start processing
		// Parse the parameter to get `eventID` and `user_list`
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    // A user enters the room
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    // A user exits the room
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    // A user sends audio packets
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    // A user stops sending audio packets
			    break;
 		    default:
			    break;
		    }
		break;
		}
	}
}

```

### AddAudioBlackList

This API is used to add an ID to the audio data blocklist. It only works on the initiator side. A returned value of `0` indicates the call is successful. Assume that users A, B, and C are all speaking using their mic in a room: 

- If A blocks C, A can only hear B;
- If B blocks neither A nor C, B can hear both of them;
- If C blocks neither A nor B, C can hear both of them.

此接口适用于在语音房间中将某用户禁言的场景。



#### Function prototype  

```
ITMGContext ITMGAudioCtrl int AddAudioBlackList(const char* openId)

```

| Parameter   | Type  | Description               |
| ------ | :---: | ------------------ |
| openId | char* |  ID of the user to be muted |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->AddAudioBlackList(openId);

```

### RemoveAudioBlackList

This API is used to remove an ID from the audio blocklist. A returned value of 0 indicates the call is successful.

#### Function prototype  

```
ITMGContext ITMGAudioCtrl int RemoveAudioBlackList(const char* openId)

```

| Parameter   | Type  | Description              |
| ------ | :---: | ----------------- |
| openId | char* | ID of the user to be unmuted |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->RemoveAudioBlackList(openId);

```

## Voice Chat Audio APIs

![Image](https://main.qcloudimg.com/raw/c85fe68b4b26555adf8ad01c82711f5b.png)

### Must-knows

The voice chat APIs can only be called when the SDK is initialized and the user has entered the room.
When the user turns on/off the mic or speaker on the UI, the following practices are recommended:

- **Games**: Call `EnableMic` and `EnableSpeaker`, which is equivalent to call both `EnableAudioCaptureDevice/EnableAudioSend` and `EnableAudioPlayDevice/EnableAudioRecv`.
- **Social apps and others**: Call `EnableAudioCaptureDevice(true)` and `EnableAudioPlayDevice(true)` once after a user enters the room. When the user clicks to enable/disable the mic, call only `EnableAudioSend/Recv` to send/receive audio streams. 
- For more information on how to release only a capturing or playback device, see the `EnableAudioCaptureDevice` and `EnableAudioPlayDevice`.
- Call `Pause` to pause the audio engine and call `Resume` to resume the audio engine.

### Voice chat audio APIs

| API                        |            Description            |
| --------------------------- | :----------------------------: |
| GetMicListCount             |       Gets the number of mics       |
| GetMicList                  |         Lists mics         |
| GetSpeakerListCount         |       Gets the number of speakers       |
| GetSpeakerList              |         Lists speakers         |
| SelectMic                   |         Selects mics         |
| SelectSpeaker               |         Selects speakers         |
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

### EnableMic

This API is used to enable/disable the mic. By default, the mic and speaker are not enabled when a user enters the room.
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

EnableMic = EnableAudioCaptureDevice + EnableAudioSend

#### Function prototype  

```
ITMGAudioCtrl virtual int EnableMic(bool bEnabled)

```

| Parameter    | Type   | Description                                                                                                                    |
| -------- | :--: | ------------------------------------------------------------ |
| bEnabled | bool | `true`: Enable the mic; `false`: Disable the mic. |

#### Sample code  

```
void UBaseViewController::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char *data) {

	FString jsonData = FString(UTF8_TO_TCHAR(data));
	TSharedPtr<FJsonObject> JsonObject;
	TSharedRef<TJsonReader<>> Reader = TJsonReaderFactory<>::Create(FString(UTF8_TO_TCHAR(data)));
	FJsonSerializer::Deserialize(Reader, JsonObject);


	if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM) {
		int32 result = JsonObject->GetIntegerField(TEXT("result"));
		FString error_info = JsonObject->GetStringField(TEXT("error_info"));
		if (result == 0) {
			GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, TEXT("Enter room success."));
			// Enable the mic
			ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
		}
		else {
			FString msg = FString::Printf(TEXT("Enter room failed. result=%d, info = %ls"), result, *error_info);
			GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, *msg);
		}
		onEnterRoomCompleted(result, error_info);
	}
}


```

### GetMicState

This API is used to query the mic status. `0`: The mic is off. `1·: The mic is on.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetMicState()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicState();

```

### EnableAudioCaptureDevice

This API is used to enable/disable an audio capturing device. By default, the audio capturing device is not enabled when the user enters the room.

- This API can only be called after EnterRoom. The device is disabled automatically after the user exits the room.
- This API is usually used in combination with actions like permission application and volume type adjustment.

#### Function prototype  

```
ITMGContext virtual int EnableAudioCaptureDevice(bool enable)

```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| enable | bool | `true`: Enable the device; `false`: Disable the device. |

#### Sample code

```
// Enable capturing device
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioCaptureDevice(true);

```

### IsAudioCaptureDeviceEnabled

This API is used to get the status of the audio capturing device.

#### Function prototype

```
ITMGContext virtual bool IsAudioCaptureDeviceEnabled()

```

#### Sample code

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioCaptureDeviceEnabled();

```

### EnableAudioSend

This API is used to enable/disable audio upstreaming. Note that the user need to enable the capturing device by calling `EnableAudioCaptureDevice`.

#### Function prototype

```
ITMGContext  virtual int EnableAudioSend(bool bEnable)

```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| enable | bool | `true`: Enable upstreaming; `false`: Disable upstreaming. |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioSend(true);

```

### IsAudioSendEnabled

This API is used to get the status of audio upstreaming.

#### Function prototype  

```
ITMGContext virtual bool IsAudioSendEnabled()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioSendEnabled();


```

### GetMicLevel

This API is used to get the real-time mic volume level. An int-type value in the range of 0-100 is returned. It is recommended to call this API once every 20 ms.

**This API is not applicable to the voice messaging service.**

#### Function prototype  

```
ITMGAudioCtrl virtual int GetMicLevel()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicLevel();

```

### GetSendStreamLevel

This API is used to get the local upstream volume. An int-type value in the range of 0-100 is returned.

**This API is not applicable to the voice message service.**

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSendStreamLevel()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSendStreamLevel();

```

### SetMicVolume

This API is used to set the mic volume. 
**This API is not applicable to the voice message service.**

#### Function prototype  

```
ITMGAudioCtrl virtual int SetMicVolume(int vol)

```

| Parameter | Type | Description |
| ---- | :--: | ----------------------- |
| vol  | int  | Volume level. Value range: 0-200. `0`: Mute the audio; `100` : (Default) Remain the original volume. |

#### Sample code  

```
int micVol = (int)(value * 100);
ITMGContextGetInstance()->GetAudioCtrl()->SetMicVolume(vol);


```

### GetMicVolume

This API is used to get the mic volume level. An int-type value will be returned. 101 indicates that the `SetMicVolume` API has not been called.

**This API is not applicable to the voice message service.**

#### Function prototype  

```
ITMGAudioCtrl virtual int GetMicVolume()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicVolume();

```

## Voice Chat Playback APIs

### Getting the number of speakers

### EnableSpeaker

This API is used to enable/disable the speaker.
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv

#### Function prototype  

```
ITMGAudioCtrl virtual int EnableSpeaker(bool enabled)

```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| enable | bool | `true`: Enable the speaker; `false`: Disable the speaker. |

#### Sample code  

```
// Enable the speaker
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);

```

### GetSpeakerState

This API is used to get the speaker status. `0`: speaker off; `1`: speaker on; `2`: in the progress of changing speaker status

- 返回值0为关闭扬声器状态。
- 返回值1为打开扬声器状态。

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerState()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerState();

```



### EnableAudioPlayDevice

This API is used to enable/disable a playback device.

#### Function prototype  

```
ITMGContext virtual int EnableAudioPlayDevice(bool enable) 

```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| enable | bool | `true`: Enable the device; `false`: Disable the device. |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioPlayDevice(true);

```

### IsAudioPlayDeviceEnabled

This API is used to get the status of a playback device.

#### Function prototype

```
ITMGContext virtual bool IsAudioPlayDeviceEnabled()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioPlayDeviceEnabled();

```

### EnableAudioRecv

This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, please see the `EnableAudioPlayDevice` API.

#### Function prototype  

```
ITMGContext virtual int EnableAudioRecv(bool enable)

```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| enable | bool | `true`: Enable audio downstreaming; `false`: Disable audio downstreaming. |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioRecv(true);

```

### IsAudioRecvEnabled

This API is used to get the status of audio downstreaming.

#### Function prototype  

```
ITMGContext virtual bool IsAudioRecvEnabled() 

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioRecvEnabled();

```

### GetSpeakerLevel

This API is used to get the real-time speaker volume level. An int-type value will be returned to indicate the volume level. It is recommended to call this API once every 20 ms.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerLevel()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerLevel();

```

### GetRecvStreamLevel

This API is used to get the real-time audio downstreaming volume levels of other members in the room. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetRecvStreamLevel(const char* openId)

```

| Parameter   | Type  | Description                 |
| ------ | :---: | -------------------- |
| openId | char* | `openId` of other members in the room |

#### Sample code  

```
iter->second.level = ITMGContextGetInstance()->GetAudioCtrl()->GetRecvStreamLevel(iter->second.openid.c_str());

```

### SetSpeakerVolume

This API is used to set the speaker volume.
参数 volume 用于设置扬声器的音量，当数值为0时，表示静音，当数值为100时，表示音量不增不减，默认数值为 100。

#### Function prototype  

```
ITMGAudioCtrl virtual int SetSpeakerVolume(int vol)

```

| Parameter | Type | Description |
| ---- | :--: | ----------------------- |
| vol  | int  | Volume level. Value range: 0-200. `0`: Mute the audio; `100` : (Default) Remain the original volume. |

#### Sample code  

```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetSpeakerVolume(vol);

```

### GetSpeakerVolume

This API is used to get the speaker volume. An int-type value will be returned to indicate the volume. 101 indicates that the `SetSpeakerVolume` API has not been called.
`Level` indicates the real-time volume, and `Volume` the speaker volume. The actual volume = Level * Volume%. For example, if the `Level` is 100 and `Volume` is 60, the actual volume is 60.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerVolume()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerVolume();

```



## Advanced APIs

### GetMicListCount

This API is used to get the number of mics connected to the room.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetMicListCount()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicListCount();

```

### GetMicList

This API is used together with the `GetMicListCount` API to enumerate mics.

#### Function prototype 

```
ITMGAudioCtrl virtual int GetMicList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
public:
	const char* pDeviceID;
	const char* pDeviceName;
};

```

| Parameter             |        Type        | Description                 |
| ---------------- | :----------------: | -------------------- |
| ppDeviceInfoList | TMGAudioDeviceInfo | Device list             |
| nCount           |        int         | Number of the mics |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicList(ppDeviceInfoList,nCount);

```



### SelectMic

This API is used to select a mic. If this API is not called or `DEVICEID_DEFAULT` is passed in, the default mic will be selected. The device ID is from the list returned by `GetMicList`.
The 0th device id returned in the GetMicList API is the default device of the call device. If there is a selected call device, it will be maintained by service. If it is unplugged, the call device will be changed back into the default device.

#### Function prototype  

```
ITMGAudioCtrl virtual int SelectMic(const char* pMicID)

```

| Parameter    | Type   | Description          |
| ------ | :---: | ------------- |
| pMicID | char* | Mic device ID |

#### Sample code  

```
const char* pMicID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectMic(pMicID);

```

This API is used to get the number of speakers.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerListCount()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerListCount();

```

### GetSpeakerList

This API is used together with the `GetSpeakerListCount` API to enumerate speakers.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
public:
	const char* pDeviceID;
	const char* pDeviceName;
};

```

| Parameter             |        Type        | Description                 |
| ---------------- | :----------------: | -------------------- |
| ppDeviceInfoList | TMGAudioDeviceInfo | Device list             |
| nCount           |        int         | Number of the speakers |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerList(ppDeviceInfoList,nCount);

```

### SelectSpeaker

This API is used to select a playback device. If this API is not called or `DEVICEID_DEFAULT` is passed in, the default playback device will be selected. The device ID is from the list returned by `GetSpeakerList`.

#### Function prototype  

```
ITMGAudioCtrl virtual int SelectSpeaker(const char* pSpeakerID)

```

| Parameter       | Type  | Description          |
| ---------- | :---: | ------------- |
| pSpeakerID | char* | Speaker device ID |

#### Sample code  

```
const char* pSpeakerID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectSpeaker(pSpeakerID);

```

### EnableLoopBack

This API is used to enable in-ear monitoring. You need to call `EnableLoopBack+EnableSpeaker` before you can hear your own voice.

#### Function prototype  

```
ITMGAudioCtrl virtual int EnableLoopBack(bool enable)

```

| Parameter   | Type | Description         |
| ------ | :--: | ------------ |
| enable | bool | Specifies whether to enable |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableLoopBack(true);

```

### GetRoomType

This API is used to get a user's room audio type. The returned value is the room audio type. Value 0 indicates that an error occurred while getting the user's room audio type. For room audio types, please see the `EnterRoom` API.

#### Function prototype  

```
class ITMGRoom {
public:
	virtual ~ITMGRoom() {} ;
	virtual int GetRoomType() = 0;

};

```

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->GetRoomType();

```

### ChangeRoomType

This API is used to modify a user's room audio type. For the result, please see the callback event. The event type is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE`. The audio type of the room is determined by the first user to enter the room. After that, if a member in the room changes the room type, it will take effect for all members there.

#### Function prototype  

```
IITMGContext TMGRoom public int ChangeRoomType((ITMG_ROOM_TYPE roomType)

```

| Parameter     |      Type      | Description                                                  |
| -------- | :------------: | ----------------------------------------------------- |
| roomType | ITMG_ROOM_TYPE | The target room type. For room audio types, please see the `EnterRoom` API. |

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);

```



#### Data details

| Message | Data | Sample |
| ------------------------------------- | :-------------------------------: | ---------------------------------------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | result; error_info; new_room_type | {"error_info":"","new_room_type":0,"result":0} |

### ChangeRoomType Callback

After the room type is set, the event message `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE` will be returned in the callback. The returned parameters include `result`, `error_info`, and `new_room_type`. The `new_room_type` represents the following information. The event message will be identified in the `OnEvent` function.

| Event Subtype | Value | Description |
| -------------------------------- | :------: | ------------------------------------------------------------ |
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM | 1 | Indicates that the existing audio type is inconsistent with and changed to that of the entered room. |
| ITMG_ROOM_CHANGE_EVENT_START | 2 | Indicates that a user is already in the room and the audio type starts changing (e.g., calling the `ChangeRoomType` API to change the audio type). |
| ITMG_ROOM_CHANGE_EVENT_COMPLETE | 3 | Indicates that a user is already in the room and the audio type has been changed. |
| ITMG_ROOM_CHANGE_EVENT_REQUEST | 4 | A room member calls `ChangeRoomType` to request changing the room audio type. |

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
		// Process room type events
	 }
}

```



### The monitoring event of room call quality

The message for quality control event triggered once every two seconds after room entry is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `loss`, and `delay`, which represent the following information. The event message will be identified in the `OnEvent` function.

This API is used to monitor the network quality. If the user's network is poor, the business layer will remind the user to switch to a better network through the UI.

| Parameter   | Type   | Description                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int | Value range: 1 (Worst) - 50 (Best).. `0` is the initial value and is meaningless. It’s recommended to send users alerts about poor network condition when the value is below 30. |
| loss | double | Upstream packet loss rate |
| delay | int | Voice chat delay in ms |

### GetSDKVersion

This API is used to get the SDK version number.

#### Function prototype

```
ITMGContext virtual const char* GetSDKVersion()

```



#### Sample code  

```
ITMGContextGetInstance()->GetSDKVersion();

```



### SetLogLevel

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### Function prototype

```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)

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



### SetLogPath

This API is used to set the log printing path. The default path is as follows:

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

#### Function prototype

```
ITMGContext virtual int SetLogPath(const char* logDir) 

```

| Parameter | Type | Description |
| ------ | :---: | ---- |
| logDir | char* | Path |

#### Sample code  

```
cosnt char* logDir = ""// Set a path by yourself

ITMGContext* context = ITMGContextGetInstance();
context->SetLogPath(logDir);

```

### GetQualityTips

This API is used to get information on the quality of real-time audio/video calls, which is mainly used to view real-time call quality and troubleshoot.

#### Function prototype

```
ITMGRoom virtual const char* GetQualityTips()

```

#### Sample code  

```
ITMGContextGetInstance()->GetRoom()->GetQualityTips();

```

## Callback Messages

### Message list

| Message | Description |   
| ------------- |:-------------:|
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM | The user enters the room. |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | The user exists the room. |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | The room is disconnected. |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | The room type is changed. |
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE | A new microphone is connected. |
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE | The mic is disconnected. |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE | A new speaker is connected.|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE | The speaker is disconnected. |
| ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH | The accompaniment is over. |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | There are updates on room members. |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_USERS_UPDATE | The number of room members is changed. |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_AUDIOSTREAMS_UPDATE | The number of room audio streams is changed. |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY | The sound quality of the room is changed. |
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE | The PTT audio recording is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE | The PTT upload is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE | The PTT download is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE | The PTT playback is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE | The speech-to-text conversion is completed. |

### Data list

| Message | Data | Sample |
| ------------------------------------------------------ | :-----------------------------------------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM                        |                result; error_info                 | {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM                         |                result; error_info                 | {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT                   |                result; error_info                 | {"error_info":"waiting timeout, please check your network","result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE                  | result; error_info; sub_event_type; new_room_type | {"error_info":"","new_room_type":0,"result":0}               |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE | result; error_info | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE | result; error_info | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE | result; error_info | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE | result; error_info | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE                       |               user_list;  event_id                | {"event_id":1,"user_list":["0"]}                             |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_USERS_UPDATE            |            AllUser; AccUser; ProxyUser            | {"AllUser":3,"AccUser":2,"ProxyUser":1}                      |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_AUDIOSTREAMS_UPDATE     |                   AudioStreams                    | {"AudioStreams":3}                                           |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY               |                weight; loss; delay                | {"weight":5,"loss":0.1,"delay":1}                            |
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE               |                 result; file_path                 | {"file_path":"","result":0}                                  |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE               |             result; file_path;file_id             | {"file_id":"","file_path":"","result":0}                     |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE             |             result; file_path;file_id             | {"file_id":"","file_path":"","result":0}                     |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE                 |                 result; file_path                 | {"file_path":"","result":0}                                  |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE          |               result; text;file_id                | {"file_id":"","text":"","result":0}                          |
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE |          result; file_path; text;file_id          | {"file_id":"","file_path":","text":"","result":0}            |


​	
