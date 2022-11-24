This document describes how to access and debug GME APIs for the commanding voice mode.

## Overview

In commanding game scenarios, GME provides the host and listener roles. If a user sets the role to host before room entry, the user can enable the mic to speak and enable the speaker to hear others talking in the room after room entry. If the user enters the room as a listener, the user cannot speak in the room after room entry even the mic is enabled.

## Prerequisites

- You have created a GME application and obtained the `AppID` and `Key` of the SDK as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- You have **activated the real-time voice service of GME** as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- You have **integrated the GME SDK** as instructed in [Native SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/40858).

## Access directions

Below is the process of connecting to the commanding voice mode:

<dx-steps>
-<dx-tag-link link="#enable" tag="console">Use GME services</dx-tag-link>
-<dx-tag-link link="#config" tag="console">Set the role</dx-tag-link>
-<dx-tag-link link="#access" tag="business">Use the real-time voice service</dx-tag-link>
-<dx-tag-link link="#callback" tag="business">Enable the mic</dx-tag-link> 
-<dx-tag-link link="#result" tag="console">Change the role</dx-tag-link>
-<dx-tag-link link="#usage" tag="console">Exit the room</dx-tag-link>
</dx-steps>

 [](id:enable)
### Step 1. Use GME

For more information on how to call and integrate the GME SDK, see [Native SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), and [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545).

[](id:config)
### Step 2. Set the role

Before calling the `EnterRoom` API, you need to call the `SetAudioRole` API to set the role of the current user in the commanding voice mode.

#### Function prototype
```
public abstract int SetAudioRole(ITMG_AUDIO_MEMBER_ROLE role); 
```

| Parameter | Type | Description |
| ---- | ---------------------- | ------------------------------------------------------------ |
| role | ITMG_AUDIO_MEMBER_ROLE | <li>ITMG_AUDIO_MEMBER_ROLE_ANCHOR: Host, who can enable the mic and speaker in the room</li><li>ITMG_AUDIO_MEMBER_ROLE_AUDIENCE: Listener, who can enable only the speaker in the room to listen to others</li> |

#### Sample code
```
ITMGContext.GetInstance().SetAudioRole(ITMG_AUDIO_MEMBER_ROLE.ITMG_AUDIO_MEMBER_ROLE_AUDIENCE);
```

[](id:access)
### Step 3. Use the real-time voice service 

Call the `EnterRoom` API to enter a voice chat room.

[](id:callback)
### Step 4. Enable the mic 

- If your role is host, you can normally call the `EnableMic` and `EnableSpeaker` APIs to enable the mic and speaker respectively.
- If your role is listener, you can normally use the `EnableSpeaker` API to enable the speaker, but the `AV_ERR_INVALID_ARGUMENT` error code (1004) will be returned to remind that your are in listener mode and the mic cannot be enabled when you call the `EnableMic` API.

[](id:result)
### Step 5. Change the role

In the room, you can call `SetAudioRole` to change the role.
- If the role is not set, the new role will be used.
- If the role is set, the new role will be used.
- If no role is set or the role is host and you are speaking with the mic enabled, but the mic is still enabled after the role is changed to listener, we recommend you call the `EnableMic` API at the business layer to change the mic status and the mic UI status.

[](id:usage)
### Step 6. Exit the room 

After the `ExitRoom` API is called to exit the voice chat room, the role status becomes invalid, and the role needs to be set again.
