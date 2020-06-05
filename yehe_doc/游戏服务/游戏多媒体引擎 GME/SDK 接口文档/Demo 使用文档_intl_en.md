## Overview
This document describes how to use the GME Native Sample Code.




## Basic Process Table
The voice chat UI in Sample Code is as shown below (in the demo for iOS):

<img src="https://main.qcloudimg.com/raw/1a65f3e7fe35da963bd48ab5a0f8bb4a.jpg" width="40%">

**The following steps apply to all platforms:**

|Step|Button Name|Feature|
|----|----|---|
|1|Init| Initializes SDK|
|2|Enterroom| Enters the audio room whose room number is specified by `RoomID`|
|3|Capture| Enables capture device|
|4|Send| Enables audio upstreaming (then, audio can be sent and users in the same room can receive the voice chat audio)|
|5|Play| Enables playback device|
|6|Rec| Enables audio downstreaming (if another user in the same room has upstreaming audio at the same time, you can hear the corresponding voice chat audio)|
|7|ExitRoom| Exits room (then, you cannot hear other users' audio nor send your audio to them)|
|8|Uninit| Uninitializes SDK and completely exits GME|

> 
>- As steps 3 and 5 are performed at the hardware level, they will take some time to complete.
>- Only after steps 3 and 4 are completed can audio be upstreamed. Similarly, audio can be played back only after steps 5 and 6 are completed.

## Directions

### 1. Set the account and openID
>You can skip this step and use the test account provided by GME by default.

Before initializing the SDK, modify the `Appid`, `Key`, and `OpenID` parameters on the voice chat UI and click **Init**.
<img src="https://main.qcloudimg.com/raw/2498f0fc3c90eeea5b0cefccaf591f39.png" width="60%">


For the source of the `Appid` and `Key` parameters, please see [Access Guide](https://intl.cloud.tencent.com/document/product/607/10782).
The `OpenID` parameter is used to identify the local user, and its value must be above 10,000.

### 2. Click Init 
After setting the account and `openID`, click "Init" to initialize the SDK. You can perform other operations after initialization.


### 3. Click EnterRoom 
Click "EnterRoom" to enter a desired voice chat room. You can manipulate the devices only after room entry. `RoomId` specifies the ID of the room to be entered. Only users under the same room ID can talk to each other.

### 4. Manipulate devices
Manipulate the devices. If there are other users in the room, you can communicate with them.
During the test, you can use another device with the same `Appid` and different `OpenID` to enter the same room. After enabling the mic and speaker, your two devices can communicate with each other.

|Button Name|Feature|
|----|---|
|Capture| Enables capture device|
|Send| Enables audio upstreaming (then, audio can be sent and users in the same room can receive the voice chat audio)|
|Play| Enables playback device|
|Rec| Enables audio downstreaming (if another user in the same room has upstreaming audio at the same time, you can hear the corresponding voice chat audio)|

## Advanced Operations
### Changing room audio type
- Before room entry, you can select the audio type. For more information on the effects, please see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).
<img src="https://main.qcloudimg.com/raw/25929745d76d6e1de3adc16055729d0e/iosSimpleCode_2.png" width="20%">
- After room entry, you can click **ChangeRoomType** to change the room audio type.


### Setting volume level
You can drag the slider to set the volume level after room entry.
- The left slider is used to set the capture device volume level, which determines the volume level of the captured audio.
- The right slider is used to set the playback device volume level, which determines the volume level of the audio played back.

<img src="https://main.qcloudimg.com/raw/be4a7063f30e264ac8adf45e95d08598/iosSimpleCode_3.png" width="40%">

### Enabling/Disabling in-ear monitoring
You can click the button next to "Loopback" to enable/disable in-ear monitoring. If it is enabled, you will be able to hear your own voice from the playback device.

### Setting accompaniment
After entering the room and performing steps 3, 4, 5, and 6, you can click the button next to "Accomp" to enable other users in the same room to hear your accompaniment. If in-ear monitoring is enabled, you can also hear your accompaniment.

### Setting karaoke effect
Enter the corresponding parameter in the input box next to **ChangeKaraoke** and click **ChangeKaraoke**, then the sent real-time audio will have the corresponding karaoke effect. The effect parameters are as detailed below:

|Parameter|Description|
|-------------|------------- |
|0	| Original voice			|
|1	| Pop			|
|2	| Rock			|
|3	| Hip hop			|
|4	| Dance music			|
|5	| Ethereal voice			|
|6	| Speech synthesis		|

### Setting voice changing effect
Enter the corresponding parameter in the input box next to "ChangeVoiceType" and click "ChangeVoiceType", then the sent real-time audio will have the corresponding voice changing effect. The effect parameters are as detailed below:

|Parameter|Description|
|-------------|------------- |
|0	| Original voice			|
|1	| Little girl			|
|2	| Middle-aged man			|
|3	| Ethereal voice			|
|4	| Chubby			|
|5	| Heavy metal			|
|6	| Non-native speaker			|
|7	| Being cold			|
|8	| Furious animal			|
|9	| Heavy machinery			|
|10	| Strong electric current			|
|11	| Preschooler			|
|12	| Minion			|


## Notes
Some special APIs for testing the SDK are used in the demo. You should not call them:
```
SetAppVersion
GetSDKVersion
SetAdvanceParams
SetTestEnv
SetRecvMixStreamCount
```

