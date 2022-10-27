
This document describes how to access and debug GME client APIs for the voice chat feature for Cocos2d.

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
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">Enabling the microphone</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">Enabling the speaker</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">Exiting a voice room</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">Uninitializing GME</dx-tag-link>
</dx-steps>


### C++ classes

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


### Preparations
You need to import the header file `tmg_sdk.h` first before you can access GME. The classes in the header file inherit `ITMGDelegate` for message delivery and callback.
#### Sample code  

```
#include "tmg_sdk.h"

class TMGTestScene : public cocos2d::Scene,public ITMGDelegate
{
public:
...
private:
...
｝
```


### Setting a singleton
You need to get `ITMGContext` first before you can call the `EnterRoom` function. All calls begin with `ITMGContext`, which is returned to the application through the `ITMGDelegate` callback and must be set first.
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
//TMGTestScene.h:
class TMGTestScene : public cocos2d::Scene,public ITMGDelegate
{
public:
	void OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data);
｝

//TMGTestScene.cpp:
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	// Identify and manipulate `eventType` here
}
```




[](id:Init)
### Initializing the SDK

**You need to initialize the SDK through the `Init` API** before you can use the real-time voice, voice message, and speech-to-text services. The `Init` API must be called in the same thread as other APIs. We recommend you call all APIs in the main thread.

#### API prototype

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

| Parameter | Type | Description |
| -------- | :---------: | ------------------------------------------------------------ |
| sdkAppId | const char* | `AppID` provided in the [GME console](https://console.cloud.tencent.com/gamegme), which can be obtained as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0). |
| openID   | const char* | `openID` can only be in `Int64` type, which is passed in after being converted to a `const char*`. You can customize its rules, and it must be unique in the application. To pass in `openID` as a string, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) for application.         |

#### Returned values

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| AV_OK = 0                  | Initialized SDK successfully. |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

<dx-alert infotype="notice" title="Notes on 7015 error code">

- The 7015 error code is judged by md5. If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.
- Due to the third-party reinforcement, Unity packaging mechanism and other factors, the md5 of the library file will be affected, resulting in misjudgment. **Please ignore this error in the logic for official release**, and try to avoid displaying it in the UI.
  </dx-alert>

#### Sample code 

```
#define SDKAPPID3RD "14000xxxxx"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```

[](id:Poll)
### Triggering event callback

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. `Poll` is the message pump of GME, and the `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
You can refer to the `EnginePollHelper.cpp` file in the demo.

<dx-alert infotype="alarm" title="Calling the `Poll` API periodically">
The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
</dx-alert>

#### API prototype

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
class TMGTestScene : public cocos2d::Scene,public ITMGDelegate
{
void update(float delta); 
}

// Code implementation
void TMGTestScene::update(float delta)
{
    ITMGContextGetInstance()->Poll();
}
```

### Pausing the system

When a `Pause` event occurs in the system, the engine should also be notified for pause. If you do not need the background to play back the audio in the room, please call `Pause` API to pause the GME service.

#### API prototype

```
ITMGContext int Pause()
```

### Resuming the system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### API prototype

```
ITMGContext int Resume()
```

[](id:UnInit)
### Uninitializing SDK

This API is used to uninitialize the SDK to make it uninitialized. **If the game business account is bound to `openid`, switching game account requires uninitializing GME and then using the new `openid` to initialize again.**

#### API prototype

```
ITMGContext int Uninit()
```
#### Sample code
```
ITMGContext* context = ITMGContextGetInstance();
context->Uninit();
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
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```

| Parameter | Type | Description |
| ------------- | :---: | ------------------------------------------------------------ |
| dwSdkAppID    |  unsigned int  | `AppId` from the Tencent Cloud console                              |
| strRoomID     | const char* | Room ID, which can contain up to 127 characters.                                      |
| strOpenID     | const char* | User ID, which is the same as `openID` during initialization.                        |
| strKey        | const char* | Permission key from the [Tencent Cloud console](https://console.cloud.tencent.com/gamegme) |
| strAuthBuffer | const char* | Returned `authbuff`                                              |
| bufferLength  |  int  | The length of the returned `authbuff`. `500` is recommended.                             |

#### Sample code  

```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
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
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)
```

| Parameter | Type | Description |
| ---------- | :------------: | ----------------------- |
| roomID     |    const char*      | Room ID, which can contain up to 127 characters. |
| roomType   | ITMG_ROOM_TYPE | Room type. We recommend you select `ITMG_ROOM_TYPE_FLUENCY` for games. For more information on room audio types, see [Sound Quality](https://intl.cloud.tencent.com/document/product/607/18522).            |
| authBuffer |    const char*      | Authentication key                  |
| buffLen    |      int       | Authentication key length              |

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_FLUENCY, (char*)retAuthBuff,bufferLen);
```

### Callback for room entry

After the user enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function for callback and processing. A successful callback means that the room entry is successful, and the billing starts.

<dx-fold-block title="Billing references">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009)
[Billing FAQs](https://intl.cloud.tencent.com/document/product/607/30255)
[Will Voice Chat still be charged when client is offlined?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		// Process
		break;
		}
	}
}
```

#### Data details

| Message | Data | Sample |
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM      | result; error_info | {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT                   |                result; error_info                 | {"error_info":"waiting timeout, please check your network","result":0} |

If the network is disconnected, there will be a disconnected callback prompt `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`. At this time, the SDK will automatically reconnect, and the callback is `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`. When the reconnection is successful, there will be a callback `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS`.

#### Error codes

| Error Code Value | Cause and Suggested Solution |
| -------- | ------------------------------------------------------------ |
| 7006 | Authentication failed <li>The `AppID` does not exist or is incorrect.<li>An error occurred while authenticating the `authbuff`.<li>Authentication expired.<li>The `OpenId` does not meet the specification. |
| 7007 | Already in another room. |
| 1001 | The user was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned. |
| 1003 | The user was already in the room and called the room entering API again. |
| 1101 | Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally. |


[](id:ExitRoom)	
### Exiting a room

This API is used to exit the current room. It is an async API. The returned value `AV_OK` indicates a successful async delivery. If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the `EnterRoom` API.

#### API prototype  

```
ITMGContext virtual int ExitRoom()
```

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();
```

#### Callback for room exit

After the user exits a room, a callback will be returned with the message being `ITMG_MAIN_EVENT_TYPE_EXIT_ROOM`.

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
		{
		// Process
		break;
		}
	}
}
```

#### Data details

| Message | Data | Sample |
| ------------------------------ | :----------------: | ---------------------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | result; error_info | {"error_info":"","result":0} |

### Determining whether a user has entered a room

This API is used to determine whether the user has entered a room. A value in bool type will be returned. Do not call this API during room entry.

#### API prototype  

```
ITMGContext virtual bool IsRoomEntered()
```

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->IsRoomEntered();

```

### Switching room

User can call this API to quickly switch the voice chat room after entering the room. After the room is switched, the device is not reset, that is, if the microphone is already enabled in this room, the microphone will keep enabled after the room is switched.
The callback for quickly switching rooms is `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM`, and the fields are `error_info` and `result`.

#### API prototype

```
ITMGContext virtual int SwitchRoom(const char* targetRoomID, const char* authBuff, int buffLen);
```

#### Type descriptions

| Parameter | Type | Description |
| ------------ | ------ | ------------------------------ |
| targetRoomID | const char* | ID of the room to enter               |
| authBuffer   | const char* | Generates a new authentication key with the ID of the room to enter |
| buffLen   | int | Authentication key length  |

## Room Status Maintenance

APIs in this section are used to display speaking members and members entering or exiting the room and mute a member in the room at the business layer.

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

| API/Notification | Description |
| -------------------------------- | :--------------: |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | The member status changed |
| AddAudioBlackList                | Mutes a member in the room |
| RemoveAudioBlackList             |     Unmutes a user     |

### Notification events of member room entry and speaking status


This API is used to obtain the user speaking in the room and display it in the UI, and to send a notification when someone entering or exiting the room.
Notification for this event will be sent only when the status changes. To get member status in real time, cache the notification when it is received at a higher layer. The event message is `ITMG_MAIN_EVNET_TYPE_USER_UPDATE`, where the data contains `event_id` and `user_list`. The event message will be identified in the `OnEvent` function.
Notifications for audio events are subject to a threshold, and a notification will be sent only when this threshold is exceeded. The notification "A member has stopped sending audio packets" will be sent if no audio packets are received in more than two seconds.

| event_id | Description | Maintenance |
| ---------------------------- | :----------------------------------------------------------: | ---------------------- |
| ITMG_EVENT_ID_USER_ENTER     |                     Return the `openid` of the member entering the room.                       | Member list     |
| ITMG_EVENT_ID_USER_EXIT      |                 Return the `openid` of the member exiting the room.           | Member list     |
| ITMG_EVENT_ID_USER_HAS_AUDIO | Return the `openid` of the member sending audio packets in the room. This event can be used to determine whether a user is speaking and display the voiceprint effect.  | Chat member list |
| ITMG_EVENT_ID_USER_NO_AUDIO  |                     Return the `openid` of the member stopping sending audio packets in the room.                     | Chat member list |

#### Sample code
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		// Process
		// Parse the parameter to get `eventID` and `user_list`
		    switch (eventID)
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
		break;
		}
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

```
ITMGContext ITMGAudioCtrl int AddAudioBlackList(const char* openId)
```

| Parameter | Type | Description |
| ------ | :---: | ------------------ |
| openId | char* | `openid` of the user to be blocked |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->AddAudioBlackList(openId);
```

### Unmuting

This API is used to remove an ID from the audio data blacklist. A returned value of 0 indicates the call is successful.

#### API prototype  

```
ITMGContext ITMGAudioCtrl int RemoveAudioBlackList(const char* openId)
```

| Parameter | Type | Description |
| ------ | :---: | ----------------- |
| openId | char* | ID to be unblocked |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->RemoveAudioBlackList(openId);
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
ITMGAudioCtrl virtual int EnableMic(bool bEnabled)
```

| Parameter    | Type   | Description                                                                                                                    |
| -------- | :--: | ------------------------------------------------------------ |
| bEnabled | bool | To enable the mic, set this parameter to `true`, otherwise, set it to `false`. |

#### Sample code  

```
// Enable mic
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```

### Getting the mic status

This API is used to get the mic status. The returned value 0 indicates that the mic is off, while 1 is on.

#### API prototype  

```
ITMGAudioCtrl virtual int GetMicState()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicState();
```

### Enabling or disabling capturing device

This API is used to enable/disable a capturing device. The device is not enabled by default after room entry.

- This API can only be called after room entry. The device will be disabled automatically after room exit.
- Operations such as permission application and volume type adjustment will generally be performed when a capturing device is enabled on a mobile device.

#### API prototype  

```
ITMGAudioCtrl virtual int EnableAudioCaptureDevice(bool enable)
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| enable | bool | To enable the capturing device, set this parameter to `true`, otherwise, set it to `false`. |

#### Sample code

```
// Enable capturing device
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioCaptureDevice(true);
```

### Getting the capturing device status

This API is used to get the status of a capturing device.

#### API prototype

```
ITMGContext virtual bool IsAudioCaptureDeviceEnabled()
```

#### Sample code

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioCaptureDeviceEnabled();
```

### Enabling or disabling audio upstreaming

This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, please see the `EnableAudioCaptureDevice` API.

#### API prototype

```
ITMGContext  virtual int EnableAudioSend(bool bEnable)
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| bEnable | bool | To enable audio upstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioSend(true);
```

### Getting audio upstreaming status

This API is used to get the status of audio upstreaming.

#### API prototype  

```
ITMGContext virtual bool IsAudioSendEnabled()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioSendEnabled();
```

### Getting the real-time mic volume

This API is used to get the real-time mic volume. An int-type value in the range of 0-100 will be returned. It is recommended to call this API once every 20 ms.

 

#### API prototype  

```
ITMGAudioCtrl virtual int GetMicLevel()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicLevel();
```

### Getting the real-time audio upstreaming volume

This API is used to get the local real-time audio upstreaming volume. An int-type value in the range of 0-100 will be returned.

 

#### API prototype  

```
ITMGAudioCtrl virtual int GetSendStreamLevel()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSendStreamLevel();
```

### Setting the mic software volume

This API is used to set the mic volume level. The corresponding parameter is `volume`, which is equivalent to attenuating or gaining the captured sound.

 

#### API prototype  

```
ITMGAudioCtrl virtual int SetMicVolume(int vol)
```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| vol  | int  | Value range: 0–200. Default value: 100. `0` indicates that the audio is mute, while `100` indicates that the volume level remains unchanged. |

#### Sample code  

```
int micVol = (int)(value * 100);
ITMGContextGetInstance()->GetAudioCtrl()->SetMicVolume(vol);
```

### Getting the mic software volume

This API is used to obtain the microphone volume. An "int" value is returned. Value 101 represents API SetMicVolume has not been called.

 

#### API prototype  

```
ITMGAudioCtrl virtual int GetMicVolume()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicVolume();
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
### Enabling or disabling speaker

This API is used to enable/disable the speaker. **EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**

#### API prototype  

```
ITMGAudioCtrl virtual int EnableSpeaker(bool enable)
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| enable | bool | To disable the speaker, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
// Enable the speaker
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```

### Getting the speaker status

This API is used to get the speaker status. 0 indicates that the speaker is off, and 1 is on.

#### API prototype  

```
ITMGAudioCtrl virtual int GetSpeakerState()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerState();
```



### Enabling or disabling playback device

This API is used to enable/disable a playback device.

#### API prototype  

```
ITMGAudioCtrl virtual int EnableAudioPlayDevice(bool enable) 
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| enable | bool | To disable the playback device, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioPlayDevice(true);
```

### Getting the playback device status

This API is used to get the status of a playback device.

#### API prototype

```
ITMGAudioCtrl virtual bool IsAudioPlayDeviceEnabled()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioPlayDeviceEnabled();
```

### Enabling or disabling audio downstreaming

This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, please see the `EnableAudioPlayDevice` API.

#### API prototype  

```
ITMGAudioCtrl virtual int EnableAudioRecv(bool enable)
```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| enable | bool | To enable audio downstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioRecv(true);
```



### Getting audio downstreaming status

This API is used to get the status of audio downstreaming.

#### API prototype  

```
ITMGAudioCtrl virtual bool IsAudioRecvEnabled() 
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioRecvEnabled();
```

### Getting the real-time speaker volume

This API is used to get the real-time speaker volume. An int-type value will be returned to indicate the volume. It is recommended to call this API once every 20 ms.

#### API prototype  

```
ITMGAudioCtrl virtual int GetSpeakerLevel()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerLevel();
```

### Getting the real-time downstreaming audio levels of other members in the room

This API is used to get the real-time audio downstreaming volume of other members in the room. An int-type value will be returned. Value range: 0-200.

#### API prototype  

```
ITMGAudioCtrl virtual int GetRecvStreamLevel(const char* openId)
```

| Parameter | Type | Description |
| ------ | :----: | --------------------- |
| openId | char* | `openId` of other members in the room |

#### Sample code  

```
iter->second.level = ITMGContextGetInstance()->GetAudioCtrl()->GetRecvStreamLevel(iter->second.openid.c_str());
```

### Setting the speaker volume

This API is used to set the speaker volume.

#### API prototype  

```
ITMGAudioCtrl virtual int SetSpeakerVolume(int vol)
```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| vol  | int  | Volume level. Value range: 0–200. Default value: 100. `0` indicates that the audio is mute, while `100` indicates that the volume level remains unchanged. |

#### Sample code  

```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetSpeakerVolume(vol);
```

### Getting the speaker volume

This API is used to get the speaker volume. An int-type value will be returned to indicate the volume. 101 indicates that the `SetSpeakerVolume` API has not been called.
"Level" indicates the real-time volume, and "Volume" the speaker volume. The final volume = Level * Volume%. For example, if the "Level" is 100 and "Volume" is 60, the final volume is "60".

#### API prototype  

```
ITMGAudioCtrl virtual int GetSpeakerVolume()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerVolume();
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
ITMGAudioCtrl virtual int GetMicListCount()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicListCount();
```

### Enumerating mics

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

| Parameter | Type | Description |
| ---------------- | :----------------: | -------------------- |
| ppDeviceInfoList | TMGAudioDeviceInfo | Device list             |
| nCount           |        int         | Number of the mics |

| `TMGAudioDeviceInfo` Parameter | Type | Description |
| ---------------- | :----------------: | ------------------- |
| pDeviceID | const char*  | Device ID |
| pDeviceName | const char*  | Device name |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicList(ppDeviceInfoList,nCount);
```



### Selecting a mic

This API is used to select a mic. If this API is not called or `DEVICEID_DEFAULT` is passed in, the default mic will be selected.
The 0th device id returned in the GetMicList API is the default device of the call device. If there is a selected call device, it will be maintained by service. If it is unplugged, the call device will be changed back into the default device.

#### Function prototype  

```
ITMGAudioCtrl virtual int SelectMic(const char* pMicID)

```

| Parameter | Type | Description |
| ------ | :---: | ------------- |
| pMicID | const char* | Mic ID, which is from the list returned by `GetMicList`. |

#### Sample code  

```
const char* pMicID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectMic(pMicID);
```


### Getting the number of speakers
This API is used to get the number of speakers.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerListCount()

```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerListCount();

```

### Enumerating speakers

This API is used together with the `GetSpeakerListCount` API to enumerate speakers.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)
```

| Parameter | Type | Description |
| ---------------- | :----------------: | -------------------- |
| ppDeviceInfoList | TMGAudioDeviceInfo | Device list             |
| nCount           |        int         | Number of the speakers |

| `TMGAudioDeviceInfo` Parameter | Type | Description |
| ---------------- | :----------------: | ------------------- |
| pDeviceID | const char* | Device ID |
| pDeviceName | const char* | Device name |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerList(ppDeviceInfoList,nCount);

```

### Selecting a speaker

This API is used to select a playback device. If this API is not called or `DEVICEID_DEFAULT` is passed in, the default playback device will be selected.

#### Function prototype  

```
ITMGAudioCtrl virtual int SelectSpeaker(const char* pSpeakerID)

```

| Parameter | Type | Description |
| ---------- | :---: | ------------- |
| pSpeakerID | const char* | Speaker ID, which is from the list returned by `GetSpeakerList`. |

#### Sample code  

```
const char* pSpeakerID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectSpeaker(pSpeakerID);

```


## Advanced APIs

### Enabling in-ear monitoring

This API is used to enable in-ear monitoring. You need to call `EnableLoopBack+EnableSpeaker` before you can hear your own voice.

#### API prototype  

```
ITMGAudioCtrl virtual int EnableLoopBack(bool enable)
```

| Parameter | Type | Description |
| ------ | :--: | ------------ |
| enable | bool | Specifies whether to enable |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableLoopBack(true);

```

### Getting a user's room audio type

This API is used to get a user's room audio type. The returned value is the room audio type. Value 0 indicates that an error occurred while getting the user's room audio type. For room audio types, please see the `EnterRoom` API.

#### API prototype  

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

### Changing the room type

This API is used to modify a user's room audio type. For the result, please see the callback event. The event type is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE`. The audio type of the room is determined by the first user to enter the room. After that, if a member in the room changes the room type, it will take effect for all members there.
#### API prototype  

```
IITMGContext TMGRoom public int ChangeRoomType((ITMG_ROOM_TYPE roomType)
```

| Parameter | Type | Description |
| -------- | :------------: | ----------------------------------------------------- |
| roomType | ITMG_ROOM_TYPE | Room type to be switched to the target type. For room audio types, please see the `EnterRoom` API. |

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```



#### Data details

| Message | Data | Sample |
| ------------------------------------- | :-------------------------------: | ---------------------------------------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | result; error_info; new_room_type | {"error_info":"","new_room_type":0,"result":0} |

### Callback for room type setting completion

After the room type is set, the event message `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE` will be returned in the callback. The returned parameters include `result`, `error_info`, and `new_room_type`. The `new_room_type` represents the following information. The event message will be identified in the `OnEvent` function.

| Event Subtype | Parameter | Description |
| -------------------------------- | :------: | ------------------------------------------------------------ |
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM | 1 | Indicates that the existing audio type is inconsistent with and changed to that of the entered room. |
| ITMG_ROOM_CHANGE_EVENT_START | 2 | Indicates that a user is already in the room and the audio type starts changing (e.g., calling the `ChangeRoomType` API to change the audio type). |
| ITMG_ROOM_CHANGE_EVENT_COMPLETE | 3 | Indicates that a user is already in the room and the audio type has been changed. |
| ITMG_ROOM_CHANGE_EVENT_REQUEST | 4 | Indicates that a room member calls the `ChangeRoomType` API to request a change of room audio type. |

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
		// Process room type events
	 }
}
```



### The monitoring event of room call quality

This is the quality monitoring event, which is triggered once every two seconds after room entry, and its message is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `loss`, and `delay`, which are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int | Value range: 1-50. 50 indicates excellent sound quality, 1 indicates very poor (barely usable) sound quality, and 0 represents an initial meaningless value. Generally, if the value is below 30, the business layer will remind users that the network is poor and recommend them to switch the network. |
| loss | double | Upstream packet loss rate |
| delay | int | Voice chat delay in ms |

### Getting the version number

This API is used to get the SDK version number for analysis.

#### API prototype

```
ITMGContext virtual const char* GetSDKVersion()
```

#### Sample code  

```
ITMGContextGetInstance()->GetSDKVersion();
```



### Setting the log printing level

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### API prototype

```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
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
ITMGContextGetInstance()->SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
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
ITMGContext virtual int SetLogPath(const char* logDir) 

```

| Parameter | Type | Description |
| ------ | :----: | ---- |
| logDir | const char* | Path |

#### Sample code  

```
cosnt char* logDir = ""// Set a path by yourself

ITMGContext* context = ITMGContextGetInstance();
context->SetLogPath(logDir);

```

### Getting the diagnostic messages

This API is used to get information on the quality of real-time audio/video calls, which is mainly used to view real-time call quality and troubleshoot and can be ignored on the business side.

#### API prototype  

```
ITMGRoom virtual const char* GetQualityTips()
```

#### Sample code  

```
ITMGContextGetInstance()->GetRoom()->GetQualityTips();

```
## Callback Messages


| Message										| Description | Parameter | Sample |
| ----------------------------------------	|-----| :-----------------------------------------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM						| A member entered the audio room			|result; error_info	| {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM						| A member exited the audio room			|result; error_info	| {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT					| The room was disconnected for network or other reasons |result; error_info	| {"error_info":"waiting timeout, please check your network","result":0} |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE						| The room members were updated |user_list; event_id| {"event_id":1,"user_list":["0"]}                             |
| ITMG_MAIN_EVENT_TYPE_RECONNECT_START					| Room reconnection started |result; error_info	| {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS				| Room reconnection succeeded |result; error_info	| {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM						| The room was quickly switched |result; error_info	| {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE					| The room status changed |result; error_info; sub_event_type; new_room_type | {"error_info":"","new_room_type":0,"result":0}               |
| ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_START				| Cross-room mic connect started |result;			| {"result":0} |
| ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_STOP				| Cross-room mic connect stopped |result;			| {"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_DEFAULT_DEVICE_CHANGED	| The default speaker was changed |result; error_info	| {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE				| A speaker was added |                result; error_info                 | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE				| A speaker was lost | result; error_info                 | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE			| A mic was added |result; error_info                 | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"mic (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE			| A mic was lost |result; error_info                 | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_DEFAULT_DEVICE_CHANGED	| The default mic was changed |result; error_info                 | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY		| Room quality message |weight; loss; delay                | {"weight":5,"loss":0.1,"delay":1}                            |
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE		| Recording of a voice message was completed |          result; file_path                 | {"file_path":"","result":0}                                  |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE		| Upload of a voice message was completed |result; file_path;file_id             | {"file_id":"","file_path":"","result":0}                     |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE		| Download of a voice message was completed |result; file_path;file_id             | {"file_id":"","file_path":"","result":0}                     |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE		| Playback of a voice message was completed |result; file_path                 | {"file_path":"","result":0}                                  |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE		| Fast recording-to-text conversion was completed |result; text;file_id                | {"file_id":"","text":"","result":0}                          |
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE| Streaming speech-to-text conversion was completed |result; file_path; text;file_id          | {"file_id":"","file_path":","text":"","result":0}            |
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING | A voice message is being converted into text in a streaming manner |result; file_path; text;file_id          | {"file_id":"","file_path":","text":"","result":0}            |
| ITMG_MAIN_EVNET_TYPE_PTT_TEXT2SPEECH_COMPLETE		| Text-to-speech conversion was completed |result; text;file_id                | {"file_id":"","text":"","result":0}                          |
| ITMG_MAIN_EVNET_TYPE_PTT_TRANSLATE_TEXT_COMPLETE	| Text translation was completed |result; text;file_id                | {"file_id":"","text":"","result":0}                          |


​	
