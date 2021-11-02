<table>
  <tbody><tr>
    <th style="text-align:center;" width="150px"><b>Android<br></b>Scan the QR code below</th>
    <th style="text-align:center;" width="150px"><b>iOS<br></b>Scan the QR code below</th>
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

## Demo for Unity on Android and iOS


<span id="test"></span>

### Login

Enter your `UserId`, click **Login**, then you will see two buttons **Voice Chat** and **Voice Message** on the login interface.
<img src="https://main.qcloudimg.com/raw/dbacd4455622253ddb07d53e1bc785b8.png"  width="80%" /></img><br>
- Click **Voice Chat** to start a [voice chat](#test1).
- Click **Voice Message** to send a [voice message](#test2).

<span id="test1"></span>

### Voice chat


1. After [login](#test), click **Voice Chat** to open a voice chat window.
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="80%"/></img><br>
 - RoomId: ID of a room. Users with the same room ID will enter the same room.
 - RoomType: controls the voice quality.
    - Fluency: offers smooth audio playback with ultra-low latency for team voice chat in game genres such as FPS and MOBA.
    - Standard: offers high sound quality and low latency for voice chat in casual games such as Werewolf and board games.
    - High Quality: offers ultra-high sound quality and high latency for music & dancing games and voice chat apps that may involve music playback or online karaoke.


2. Click **JoinRoom** to enter a room:
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_8zP4w2.gif"  width="80%"/><br>
 - Talking Members: specifies the members who are talking in the room. Their IDs will be displayed on the room screen.
 - Mic: ticking this box enables the microphone. 
 - Speaker (Speak): ticking this box enables the speaker.
 - 3D Voice Effect: ticking this box enables the 3D voice effect, for which you should configure the following:
    - Range: specifies the distance range for receiving audio using the distance unit of your own game engine.
    - X: the audio position along the X axis.
    - Y: the audio position along the Y axis.
    - Z: the audio position along the Z axis.
    - XR: the degrees by which the audio rotates around the X axis.
    - YR: the degrees by which the audio rotates around the Y axis.
    - ZR: the degrees by which the audio rotates around the Z axis.
 - Voice Change: provides various change effects for you to choose from. For more information, see [Real-time Sound Effect](https://intl.cloud.tencent.com/document/product/607/31503).


<span id="test2"></span>

### Speech-to-text conversion

After [login](#test), click **Voice Message** to enter the language setting page.
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_DsvaLv.gif"  width="80%"/></img><br>
- Language: specifies the language used in a voice message.
- Audio: includes the recording and duration of a voice message. Click <img src="https://main.qcloudimg.com/raw/7d268c4b1bb7e1998792b19a23e7bb63.png" width="3%"></img> to play back the recording, and click it again to stop it.
- Audio-to-Text: the text converted from a voice message. Click and hold **Push To Talk** to start recording a voice message, and release this button to finish it.


## Demo for 3D Voice Effect Experience on Windows


### Prerequisites
- The demo should be run on Windows.
- To run the demo, please use one device to open it in two windows, or use two devices under the same LAN network to open it respectively.
- Please make sure that the computer headset and microphone are available.

### 1. Download

Download and then decompress the [3D Audio Demo](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.8.4/Other/GMEDemo_intl.zip).

### 2. Run the demo

Please double-click the executable file (GMEDemo.exe). You can use a device to open the demo in two windows at the same time.

### 3. Initialize it

For initialization, you need to enter the `AppID` and access key obtained from the **Service Management** page in the [GME console](https://console.cloud.tencent.com/gamegme/detail/1400391524) first. To access GME service, please see [Access Guide](https://intl.cloud.tencent.com/document/product/607/39698). **appId** refers to the `AppID` in the console, and `authKey` refers to the access key in the console.
>!
>- Please prevent your `AppID` and access key from leakage.
>- The `userId` used in two windows should be different.
>
<img src="https://main.qcloudimg.com/raw/f27ce333719f70f03447dcd97c5c9f3a.png"  width="80%"><br>
Finally, click **Initialize** -> **Voice Chat**.

### 4. Enter a voice chat room

Please enter a room ID and then click **JoinRoom**. If you have opened the demo in another window, please enter the same room ID to enter the **same voice chat room*.*

<img src="https://main.qcloudimg.com/raw/8774bd52027febc15582e3d9f700eff8.jpg"  width="80%">

### 5. Game interface introduction

Please see the interface details below:
- Exit : clicking it to back to the voice room selection page.
- Microphone on/off : the microphone is disabled by default. You need to enable it for communication.
- Help : clicking it to see the user guide.
- Accompaniment on : clicking it to play back the accompaniment.
- Logs at the bottom-right corner: displays the information of the users entering and exiting the room.
- Local connection buttons at the top-left corner: they need to be configured before a game can be started.
<img src="https://main.qcloudimg.com/raw/ae3f7726b2669c57466194a6e3e1e567.png"  width="80%"/></img>

### 6. Local connection

**To run the demo, the local LAN network connection should have been successfully configured first.**
<img src="https://main.qcloudimg.com/raw/7779b1359844c1465d613586aab2c06d.png" width="80%" /></img>

- The first room member:
The person who entered a room first is adopted as the host of the network connection. Therefore, the first member should click **LAN Host (H)** and then the member avatar will appear next to the coin.

- Other room members:
People entered the room later should connect with the host. Therefore, they need to click **LAN Client (C)** and then their avatars will appear next to the coin, and they can see the first member.

### 7. Enable the microphone

Click <img src="https://main.qcloudimg.com/raw/1fd9f4e3f35cfc166e04bd26fb520abf.png" width="3%"></img> to enable the microphone and speak to other members.

### 8. Manipulate the avatar

After successfully connected, you can see other avatars. You can also press the keys `W`, `S`, `A`, and `D` to manipulate the avatar to go forward, backward, left, and right, and move your mouse to change the visual angle.
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/linaji.gif"  width="80%"/></img>

### 9. Experience

If you use one device to open the demo in two windows, you can move the visual angle of an avatar to the coin, enable the microphone of another avatar, manipulate the avatar to run away, and keep speaking to test the 3D voice effect. If you run to the map edge, the sound will be decreased to nearly none.
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/yuan.gif"  width="80%"/></img>


