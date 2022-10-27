GME is a one-stop voice solution featuring high quality, which comprehensively covers the application scenarios in the gaming industry. It supports various features, including multiplayer voice chat, 3D sound effect, voice message, speech-to-text conversion, and voice content security.
>!The demo in this document can run on mobile phones only on Android or iOS.

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


## Demo Features
The demo demonstrates the following basic GME features:

<table>
   <tr>
      <th>Basic Feature</th>
      <th>Subfeature</th>
   </tr>
   <tr>
      <td  rowspan="4">Voice chat</td>
      <td>Sound quality options: Smooth, standard, and HD sound quality</td>
   </tr>
   <tr>
      <td>Voice chat room</td>
   </tr>
	    <tr>
      <td>3D sound effect</td>
   </tr>
      <td>Voice changing effect for voice chat (basic voice changing)</td>
   </tr>
      <td>Voice message</td>
			<td>Audio recording by pressing the button, voice message upload, and voice message playback by clicking the button</td>
   </tr>
      <td>Speech-to-text conversion</td>
			<td>Voice messages uploaded in the demo can be converted to text in various languages automatically.</td>
   </tr>
</table>

<span id="test"></span>

## Login Page

### 1. Log in to the system

Enter your UserID and click **Login**. Once you are logged in, you will see two new buttons **Voice Chat** and **Voice Message** on the screen.

<img src="https://main.qcloudimg.com/raw/dbacd4455622253ddb07d53e1bc785b8.png"  width="50%" /></img><br>

### 2. Select a feature

- Click **Voice Chat** to start a [voice chat](#test1).
- Click **Voice Message** to send a [voice message](#test2).

<span id="test1"></span>


## Trying out the Voice Chat Feature

### 1. Enter a voice room 

 After [login](#test), click **Voice Chat** to enter the voice chat page.

 <img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="50%"/></img><br>

- **RoomId**: Room ID. Users with the same room ID will enter the same room.
- **RoomType**: Sound quality.
  - Fluency: offers smooth audio playback with ultra low latency for team voice chat in game genres such as FPS and MOBA.
  - Standard: offers high sound quality and low latency for voice chat in casual games such as Werewolf and board games.
  - High Quality: It offers an HD sound quality with a relative high delay, and is suitable for gaming scenarios demanding high sound quality such as music playback.

### 2. Perform voice chat operations

On the voice chat page, click **JoinRoom** to enter a room:

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_8zP4w2.gif"  width="50%"/><br>

- **Talking Members**: IDs of the members talking in the room.
- **Mic**: If it is selected, the mic is enabled. 
- **Speaker**: If it is selected, the speaker is enabled.
- **3D Voice Effect**: If it is selected, 3D sound effect is enabled. You can configure this feature by setting the following parameters:
  - Range: specifies the distance range for receiving audio using the distance unit of your own game engine.
  - X: the audio position along the X axis.
  - Y: the audio position along the Y axis.
  - Z: the audio position along the Z axis.
  - XR: the degrees by which the audio rotates around the X axis.
  - YR: the degrees by which the audio rotates around the Y axis.
  - ZR: the degrees by which the audio rotates around the Z axis.
- **Voice Change**: Sound effect for voice chat. You can select different effects. For more information, see [Real-time Sound Effect](https://intl.cloud.tencent.com/document/product/607/31503).
- **QuitRoom**: You can click it to exit the voice chat room and return to the previous page.

<span id="test2"></span>

## Trying out the Voice Message and Speech-to-Text Conversion Features

### 1. Enter the voice message page

Upon [login](#test), click **Voice Message** to enter the voice message page.

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_DsvaLv.gif"  width="50%"/></img><br>

### 2. Perform operations on the page

- **Language**: Select the language of the recorded speech. After recording, the speech will be converted to text in the specified language and displayed after **Audio-to-Text**.
- **Push To Talk**: Press and hold **Push To Talk** to start recording and release it to stop recording.
- **Audio**: Recorded voice message and its duration. Click <img src="https://main.qcloudimg.com/raw/7d268c4b1bb7e1998792b19a23e7bb63.png" width="3%"></img> to play back the recording, and click it again to stop the playback.
- **Audio-to-Text**: Output text.

