## Overview
GME is a one-stop voice solution featuring high quality, which comprehensively covers the application scenarios in the gaming industry. It supports various features, including multiplayer voice chat, 3D sound effect, voice message, speech-to-text conversion, and voice content security. This document demonstrates the [3D sound effect feature](https://intl.cloud.tencent.com/document/product/607/18218) of voice chat. It enables players to hear a stereo voice with a sense of direction from characters when characters move. The voice also gets weaker as the distance from the source increases.
>!The demo can run on only Windows PCs.

## Prerequisites

- The demo runs on Windows platform.
- The demo requires a double-opened program on the same machine, or a separate program on two machines on the same LAN.
- Make sure computer headphone and microphone are available.
- You need to activate the real-time voice service of GME and get the `AppId` and `Key` in advance. For more information on how to apply for GME services, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782). **`appId` is the `AppID` and `authKey` is the permission key in the console.** For billing details, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009).


## Directions
### 1. Download the demo

Click to download the [3D sound effect demo](https://picture-1256313114.cos.ap-beijing.myqcloud.com/GMEDemo.zip) and decompress it.

### 2. Open the demo

Double-click to open the executable file **GMEDemo.exe**. Two demos can be opened at the same time on the same device.

### 3. Initialize the demo

<img src="https://main.qcloudimg.com/raw/33540519cd5c2bdde6139f8a4af537a6.png"  width="50%"><br>
To initialize the demo, your need to enter the `AppID` and the permission key, which can be found in **Service Management** in the [GME console](https://console.cloud.tencent.com/gamegme/detail/1400391524).

- appId: Enter the `Appid` from the console.
- userId: It is automatically generated in the demo and can be set as needed. It must be unique.
- authKey: Enter the permission key from the console.
- Click **Initialize** > **Voice Chat** to enter the voice chat room configuration page.

>! 
>- Keep your `AppID` and permission key secure.
>- Make sure the `userId` in the other demo is different from this one.

### 4. Enter a voice room

<img src="https://main.qcloudimg.com/raw/7393dbb31007299894586205cb8b6f9c.jpg"  width="50%">

On the voice room selection page, you can enter a room ID. If you open the other demo, enter the same room ID.

- Enter the room ID, which can be a string or number.
- Click **JoinRoom** to enter the voice room.

### 5. Game UI overview

<img src="https://main.qcloudimg.com/raw/0e451b80402caeb31cf6bd932acee127.png"  width="50%"/></img>

Instructions:

- Exit: Click to exit to the voice room selection page.
- Enable/disable the microphone: the mic of the room is off by default. You need to enable the microphone to make a call.
- Usage: Click to open the usage page.
- Open accompaniment: Click to start playing the accompaniment.
- Bottom right corner of the interface: Room log information showing users who entered and exited the voice room.
- Left side of the interface: local connection button. It needs to be configured before the game officially starts.



### 6. Configure local connection

<img src="https://main.qcloudimg.com/raw/670b24a1133dc07bdc9892ffa12b159f.png" width="50%" /></img>

>!This demo requires a local LAN.

- **The first person entering the room**
  The first person entering the room is the network connection Host. After clicking **LAN Host(H)**, it will generate a character next to the coin.
  <img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/master.gif"  width="50%"/></img>
- **The following persons**
  The following persons need to be connected to the Host by clicking **LAN Client(C)** and the character will be next to the coin. They now can see the first people entering the room.
  <img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/client.gif"  width="50%"/></img>
- **Information for determining whether the connection succeeds**
  1. The game character of the other player can be seen on the game UI. 
  2. In logs in the bottom-right corner of the UI, the room entry records of the `userID` of the game character of the other player are displayed.

### 7. Enable the mic

Click <img src="https://main.qcloudimg.com/raw/1fd9f4e3f35cfc166e04bd26fb520abf.png" width="3%"></img> to enable the mic, and you can talk with people in the room.

### 8. Instructions

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/linaji.gif"  width="50%"/></img>

W", "S", "A" and "D" on the keyboard correspond to "forward", "backward", "left" and "right" respectively. The mouse can be used to adjust the perspective. The connected client can see the character operated by the other client.

### 9. How to experience

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/yuan.gif"  width="50%"/></img>

If you open the demo in two instances locally, you can move the perspective of one demo to the coin and enable the mic, and make the character on the other demo to run away as far as possible and keep talking. In this way, you can try out the 3D sound effect. When the character is at the map border, the voice will be almost inaudible.



