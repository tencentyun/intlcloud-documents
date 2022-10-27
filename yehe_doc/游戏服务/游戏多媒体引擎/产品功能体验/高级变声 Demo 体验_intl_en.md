## Overview
GME is a one-stop voice solution featuring high quality, which comprehensively covers the application scenarios in the gaming industry. It supports various features, including multiplayer voice chat, 3D sound effect, voice message, speech-to-text conversion, and voice content security. By using GME's advanced voice changing effects, players can freely change their voice in voice chat in the game.
>!The demo can run on only Windows PCs.

## Prerequisites

- The demo runs on Windows platform.
- The demo requires a double-opened program on the same machine, or a separate program on two machines on the same LAN.
- Make sure computer headphone and microphone are available.
- You need to activate the real-time voice service of GME and get the `AppId` and `Key` in advance. For more information on how to apply for GME services, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782). **`appId` is the `AppID` and `authKey` is the permission key in the console.** For billing details, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009).

## Directions
### 1. Open the demo

Click to download [Advanced Voice Changing effect experience Demo](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GMEDemoWithVoicemod_1.0.zip) and decompress it. Double-click to open the file **TMGSDK_For_Audio_ApiExample.exe** and run the Demo.

The UI is as follows:

<img src="https://qcloudimg.tencent-cloud.cn/raw/ced85aa2b117bad61fe538c2e3a1252e.png" width=80%/><img>

### 2. Enter AppID and Key

To initialize the demo, your need to enter the `AppID` and the permission key, which can be found in **Service Management** in the [GME console](https://console.cloud.tencent.com/gamegme). You can apply for GME services as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782). **`AppID` and `Key` are the `AppID` and permission key in the console respectively.**

<dx-alert infotype="explain" title="">

- Please save your AppID and key well.
- Make sure the userId in the other demo application is different from the current userId number.
  </dx-alert>

### 3. Initialize the demo

Click **Init** to initialize.

### 4. Enter a room

Click **EnterRoom** to enter the room.

### 5. Enable devices

Click **EnableMic**、**EnableSpeaker**、**EnableLoopback** to enable devices and in-ear monitoring.

### 6. Try out the effect

Speak into the microphone and experience the voice changing effect.

configuration description:

<img src="https://qcloudimg.tencent-cloud.cn/raw/791e556855f15dfb3005040a8c4d1d27.png" width=80%/><img>

### 7. Exit the room

When the test is over, click **ExitRoom** to exit the room. Otherwise, it may incur additional charges.



