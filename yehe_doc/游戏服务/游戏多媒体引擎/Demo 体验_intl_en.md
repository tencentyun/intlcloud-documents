
<table>
  <tbody><tr>
    <th style="text-align:center;" width="150px"><b>Android<br></b>Scan QR code below</th>
    <th style="text-align:center;" width="150px"><b>iOS<br></b>Scan QR code below</th>
  </tr>
  <tr>
    <td style="
    text-align: center;
"><img style="width:150px; max-width: inherit;" src="https://main.qcloudimg.com/raw/17b2a65547432f5d81391fce1fa17a90.png" class="zoom-img-hover"></td>
    <td style="
    text-align: center;
"><img style="width:150px; max-width: inherit;" src="https://main.qcloudimg.com/raw/17b2a65547432f5d81391fce1fa17a90.png" class="zoom-img-hover"></td>
  </tr>
</tbody></table>

## Android/iOS Unity Demo

<span id="test"></span>

### Login

Enter your UserID and click **Login**. Once you are logged in, you will see two new buttons **Voice Chat** and **Voice Message** on the screen.
<img src="https://main.qcloudimg.com/raw/dbacd4455622253ddb07d53e1bc785b8.png"  width="80%" /></img><br>
- Click **Voice Chat** to start a [voice chat](#test1).
- Click **Voice Message** to send a [voice message](#test2).

<span id="test1"></span>

### Voice chat


1. After [logging in](#test), click **Voice Chat** to enter the voice chat page.
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="80%"/></img><br>
 - RoomId: ID of the room. Users with the same room ID will enter the same room.
 - RoomType: Controls the voice quality.
    - Fluency: Offers smooth audio playback with ultra low latency for team voice chat in game genres such as FPS and MOBA.
    - Standard: Offers high sound quality and low latency for voice chat in casual games such as Werewolf and board games.
    - High Quality: Offers ultra-high sound quality and high latency for music & dancing games and voice chat apps that may involve music playback or online karaoke.


2. Click **JoinRoom** to enter a room:
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_8zP4w2.gif"  width="80%"/><br>
 - Talking Members: specifies the members who are talking in the room. Their IDs will be displayed on the room screen.
 - Mic: ticking this box enables the microphone. 
 - Speaker: ticking this box enables the speaker.
 - 3D Voice Effect: ticking this box enables the 3D voice effect, for which you should configure the following:
    - Range: specifies the distance range for receiving audio using the distance unit of your own game engine.
    - X: the audio position along the X axis.
    - Y: the audio position along the Y axis.
    - Z: the audio position along the Z axis.
    - XR: the degrees by which the audio rotates around the X axis.
    - YR: the degrees by which the audio rotates around the Y axis.
    - ZR: the degrees by which the audio rotates around the Z axis.
 - Voice Change: Provides various real-time voice sound effects. For more information, see [Real-time Sound Effects](https://intl.cloud.tencent.com/document/product/607/31503#k-.E6.AD.8C.E9.9F.B3.E6.95.88.E7.89.B9.E6.95.88).


<span id="test2"></span>

### Voice message

After [logging in](#test), click **Voice Message** to enter the voice message page.
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_DsvaLv.gif"  width="80%"/></img><br>
- Language: specifies the language used in a voice message.
- Audio: includes the recording and duration of a voice message. Click <img src="https://main.qcloudimg.com/raw/7d268c4b1bb7e1998792b19a23e7bb63.png" width="3%"></img> to play back the recording, and click it again to stop it.
- Audio-to-Text: the text converted from an audio. Click and hold **Push To Talk** to start recording, and release this button to stop it.


## Windows 3D Voice Demo


### Prerequisites
- The demo runs on a Windows platform.
- The demo requires two running sessions of the program on the same device, or running the program on two devices on the same LAN.
- The computer headset and microphone are available.
- Apply for GME Voice Chat service in advance.

### 1. Download a package

Click to download [3D Voice Demo](https://picture-1256313114.cos.ap-beijing.myqcloud.com/GMEDemo.zip) and decompress it.

### 2. Open the Demo

Double-click to open the file **GMEDemo.exe**. Two Demos can be opened at the same time on the same device.

### 3. Initialize

To initialize the Demo, you need to enter the AppID and the key, which can be found in **Service Management** in [Game Multimedia Engine Console](https://console.cloud.tencent.com/gamegme/detail/1400391524). To apply for GME service, see [Access Guide](https://intl.cloud.tencent.com/document/product/607/10782). 


<dx-alert infotype="explain" title="">
- Keep the AppID and key secretly.
- Make sure the userId in the other demo application is different from the current userId.
</dx-alert>



<img src="https://main.qcloudimg.com/raw/f27ce333719f70f03447dcd97c5c9f3a.png"  width="80%"><br>
Click **Initialize** > **Voice Chat** to enter the Voice Chat room filling page.

### 4. Enter a voice room

Now you can enter a room number. If you open another demo, please enter the same room number, and click **JoinRoom** to enter the **Same voice room**.

<img src="https://main.qcloudimg.com/raw/8774bd52027febc15582e3d9f700eff8.jpg"  width="80%">

### 5. Game interface

See the interface details below:
- Exit: Go back to the voice room selection page.
- Microphone on/off: Mic is off by default. Turn it on to make a call.
- Help: Check the user guide.
- Accompaniment on: Play the accompaniment.
- Bottom-right corner: Logs of users entering and exiting the room.
- Top-left corner: Configure the local information to start the game.
<img src="https://main.qcloudimg.com/raw/ae3f7726b2669c57466194a6e3e1e567.png"  width="80%"/></img>

### 6. Local connection

This demo requires a local LAN connection base.
<img src="https://main.qcloudimg.com/raw/7779b1359844c1465d613586aab2c06d.png" width="80%" /></img>

- The first room member:
The person who entered a room first is adopted as the host of the network connection. Therefore, the first member should click **LAN Host (H)** and then the member avatar will appear next to the coin.


- Other room members:
People entered the room later should connect with the host. Therefore, they need to click **LAN Client (C)** and then their avatars will appear next to the coin, and they can see the first member.


### 7. Turn on the microphone

Click <img src="https://main.qcloudimg.com/raw/1fd9f4e3f35cfc166e04bd26fb520abf.png" width="3%"></img> to turn on the microphone and speak to room members.

### 8. Manipulate the avatar

After successfully connected, you can see other avatars. Press the keys *W*, *S*, *A*, and *D* to manipulate the avatar to go forward, backward, left, and right, and move your mouse to change the visual angle.
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/linaji.gif"  width="80%"/></img>

### 9. Experience

If you open two sessions of the demo on one device, move the visual angle of the avatar on one demo to the coin. Then turn on the microphone. Manipulate the avatar on the other demo to run away, and keep speaking to test the 3D voice effect. If you run to the map edge, the sound is barely heard.
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/yuan.gif"  width="80%"/></img>


## Voice Changing effects

GME provides various voice changing effects.

### Prerequisites
- The demo runs on a Windows platform.
- Make sure computer headphone and microphone are available.
- Apply for GME Voice Chat service in advance.

### Open demo

Click to download [Voice Changing Demo](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GMEDemoWithVoicemod_1.0.zip) and decompress it. Double-click to open the file **TMGSDK_For_Audio_ApiExample.exe** and run the Demo.

### Running interface

<img src="https://qcloudimg.tencent-cloud.cn/raw/b4e2a3c8ef86b7ce8a8750adbc21cae8.png" width=80%/><img>

###1. Enter AppID and Key

To initialize the Demo, you need to enter the AppID and the key, which can be found in **Service Management** in [Game Multimedia Engine Console](https://console.cloud.tencent.com/gamegme/detail/1400391524). To apply for GME service, see [Access Guide](https://intl.cloud.tencent.com/document/product/607/10782). 


<dx-alert infotype="explain" title="">
- Keep the AppID and key secretly.
- Make sure the userId in the other demo application is different from the current userId.
</dx-alert>

### 2. Initialize
Click **Init** to initialize.

### 3. Enter the room
Click **EnterRoom** to enter the room.

### 4. Enable devices

Click **EnableMic**, **EnableSpeaker**, **EnableLoopback** to enable devices and in-ear monitoring.

### 5. Experience

Speak into the microphone and experience the voice changing effect.

configuration description:

<img src="https://qcloudimg.tencent-cloud.cn/raw/dc5f3b8312cc4cab666c2d43719f79cc.png" width=80%/><img>

### 6. Exit the room
When the test is over, click **ExitRoom** to exit the room. Otherwise, it may incur additional charges.
