
This document provides a detailed description of using Unity Demo that makes it easy for Unity developers to debug and integrate the APIs for Game Multimedia Engine (GME).
<span id="test"></span>
## Login

Enter your UserID and click **Login**. Once you are logged in, you will see two new buttons **Voice Chat** and **Voice Message** on the login screen.
- Click **Voice Chat** to start a [voice chat](#test1).
- Click **Voice Message** to send a [voice message](#test2).

![](https://main.qcloudimg.com/raw/dbacd4455622253ddb07d53e1bc785b8.png)

<span id="test1"></span>
## Voice Chat

1. Upon [login](#test), click **Voice Chat** to enter the voice chat window.
![](https://main.qcloudimg.com/raw/3807e7d6946948c06e47f51ad9e7a2b4.png)
 - RoomId: ID of the room. Users with the same room ID will enter the same room.
 - RoomType: controls the voice quality.
    - Fluency: offers smooth audio playback with ultra low latency for team voice chat in game genres such as FPS and MOBA.
    - Standard: offers high sound quality and low latency for voice chat in casual games such as Werewolf and board games.
    - High Quality: offers ultra-high sound quality and high latency for music & dancing games and voice chat apps that may involve music playback or online karaoke.
  


2. Click **JoinRoom** to enter a room:
![image](https://main.qcloudimg.com/raw/a2ac816eacd95dfa89c8a5cee4f93f40.png)
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
 - Voice Change: provides various change effects for you to choose from. For more information, see [Real-time Sound Effects](https://intl.cloud.tencent.com/document/product/607/31503).
 



<span id="test2"></span>
## Voice Message

Upon [login](#test), click **Voice Message** to enter the voice message window.
![](https://main.qcloudimg.com/raw/c3461b2510032f033f0417890c636f2d.png)
- Language: specifies the language used in a voice message.
- Audio: includes the recording and duration of a voice message. Click <img src="https://main.qcloudimg.com/raw/7d268c4b1bb7e1998792b19a23e7bb63.png" width="3%"></img> to play back the recording, and click it again to stop it.
- Audio-to-Text: the text converted from a voice message. Click and hold **Push To Talk** to start recording a voice message, and release this button to stop it.



