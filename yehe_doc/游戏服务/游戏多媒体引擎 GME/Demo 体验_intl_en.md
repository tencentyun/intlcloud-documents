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

### Logging in

Enter your UserId and click **Login**. Once logged in, you will see two new buttons **Voice Chat** and **Voice Message** on the login screen.
<img src="https://main.qcloudimg.com/raw/dbacd4455622253ddb07d53e1bc785b8.png" /></img>
- Click **Voice Chat** to start a [voice chat](#test1).
- Click **Voice Message** to send a [voice message](#test2).

<span id="test1"></span>

### Voice chat


1. Upon [login](#test), click **Voice Chat** to enter the voice chat window.
<img src="https://picture-1256313114.cos.ap-beijing.myqcloud.com/IMB_KuI8ov.GIF" /></img>
 - RoomId: ID of the voice chat room. Users using the same room ID will enter the same room.
 - RoomType: select voice quality.
    - Fluency: offers smooth audio playback with ultra low latency for team voice chat, ideal for FPS and MOBA games.
    - Standard: offers high sound quality with low latency for voice chat in casual games such as Werewolf and board games.
    - High Quality: offers ultra-high sound quality for music & dance games and voice chat apps that require music playback or online karaoke. Latency may be relatively high. 


2. Click **JoinRoom** to enter a room:
<img src="https://picture-1256313114.cos.ap-beijing.myqcloud.com/IMB_8zP4w2.GIF" /></img>
 - Talking Members: indicates the members who are talking in the room by displaying their IDs on the screen.
 - Mic: check this box, and your mic is on. 
 - Speaker: check this box, and your speaker is on.
 - 3D Voice Effect: if you check this box, 3D voice effect is on, and you may configure the following:
    - Range: specifies the distance range for receiving audio in the unit of your game engine.
    - X: audio position along the X axis.
    - Y: audio position along the Y axis.
    - Z: audio position along the Z axis.
    - XR: the degrees by which audio rotates around the X axis.
    - YR: the degrees by which audio rotates around the Y axis.
    - ZR: the degrees by which audio rotates around the Z axis.
 - Voice Change: provides various sound effects for you to choose from. For more information, see [Real-time Sound Effect](https://intl.cloud.tencent.com/document/product/607/31503).


<span id="test2"></span>

### Voice message

Upon [login](#test), click **Voice Message** to enter the voice message window.
<img src="https://picture-1256313114.cos.ap-beijing.myqcloud.com/IMB_DsvaLv.GIF" /></img>
- Language: the language used in a voice message.
- Audio: the content and duration of a voice message. Click <img src="https://main.qcloudimg.com/raw/7d268c4b1bb7e1998792b19a23e7bb63.png" width="3%"></img> to play back the recording, and click it again to stop.
- Audio-to-Text: text converted from a voice message. Click and hold **Push To Talk** to start recording a voice message, and release to finish.

