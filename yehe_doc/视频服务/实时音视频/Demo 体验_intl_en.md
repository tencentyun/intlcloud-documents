<style>
.markdown-text-box table th,.markdown-text-box table td{text-align: center;}
.inbuttom{height: 30px;width: 150px;min-width: 24px;padding: 0 20px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;vertical-align: middle;white-space: nowrap;}
</style>

## Native Demos
<table>
<tr>
<th>iOS</th><th>Android</th><th>Windows</th><th >macOS</th>
</tr>
<tr>
<td><img style="width:150px" src="https://main.qcloudimg.com/raw/a1a6fd4a9bc3ad2b5fe60e31202c8fda.png" data-nonescope="true"></td>
<td><a onclick="window.open('https://dldir1.qq.com/hudongzhibo/liteav/TRTCDemo.apk')"><button style="width:150px;height: 150px;border:none;background-image:url(https://main.qcloudimg.com/raw/8a603ced0a61983018c794df842f7029.png);background-size: cover;">
</button></a></td>
<td><a onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Win_Demo.exe')"><button style="width:150px;height: 150px;border:none;background-image:url(https://main.qcloudimg.com/raw/e80b8f4462e2904b31dcdcaabe71c484.png);background-size: cover;">
</button></a></td>
<td><a onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Mac_Demo.tar.bz2')"><button style="width:150px;height: 150px;border:none;background-image:url(https://main.qcloudimg.com/raw/e80b8f4462e2904b31dcdcaabe71c484.png);background-size: cover;">
</button></a></td>
</tr>
</table>


## Cross-Platform Demos
<table>
<tr>
</td>
<input type="button" value="Video call" class="inbuttom" onclick="window.open('https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/official-demo/index.html')" /><br><br>
<input type="button" value="Interactive live streaming" class="inbuttom" onclick="window.open('https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html')" />
</td>
</td>
<a onclick="window.open('https://www.pgyer.com/KP03')" value="Flutter_iOS">
	<button style="width:150px;height: 83px;border:none;background-image:url(https://main.qcloudimg.com/raw/6d4d839ef8050cd3839b86f98bd7c35f.png);background-size: cover;">
</button>
</a>
<br>
<a onclick="window.open('https://comm.qq.com/im_demo_download/trtc_flutter_demo.apk')" value="Flutter_Android"> 
	<button style="width:150px;height: 83px;border:none;background-image:url(https://main.qcloudimg.com/raw/f53741b9ad7567c475841e68cc65dbc3.png);background-size: cover;">
</button>
</a></td>
</td>
<input type="button" value="Windows" class="inbuttom"  onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo%20Setup%201.1.0.exe')" /><br><br>
<input type="button" value="macOS" class="inbuttom" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo-1.1.0.dmg')" /></td>
</tr>
</table>





## Video Call
TRTC supports one-to-one and group video calls at a resolution of 720p or 1080p. In the video call mode, each room allows a maximum of 300 participants, and up to 50 participants can keep their cameras on at the same time. Common video call scenarios include one-to-one video call, video conference with up to 300 people, online medical consultation, video chat, video customer service, video interviews, audio/video recording, online insurance claim settlement, video Werewolf, etc.
<dx-tabs>
::: iOS & Android

<table>
<tr>
   <th>Call</th>
   <th>Answer</th>
 </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/group-call.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/group-recv.gif"/></td>
</tr>
</table>
:::
::: Flutter\s(iOS/Android)
![](https://imgcache.qq.com/operation/dianshi/other/8d81a52d-ffd3-4bbd-bd09-1a1648569b2d.453825bf12c01b9fe937ca8d7291f3c44b48cced.gif)
:::
::: Windows
![](https://imgcache.qq.com/operation/dianshi/other/win.836bd473a766ea962d0b40117888e99aad5db6c8.gif)
:::
::: macOS
![](https://imgcache.qq.com/operation/dianshi/other/macOS.cd7d6d7e8a7fcc388ec27e41c6952b8615ce9d34.gif)
:::
::: Desktop Browser
![](https://imgcache.qq.com/operation/dianshi/other/058ffcf5-60f0-430c-96c7-e1760b93e444.fdd0f2c10a8242dadbf99108a48a59124124b437.gif)

<table>
<tr><th>Call</th><th>Answer</th> </tr>
<tr>
<td><img src="https://webim-1252463788.cos.ap-shanghai.myqcloud.com/trtc-calling-doc-assets/videocall.gif"/></td>
<td><img src="https://webim-1252463788.cos.ap-shanghai.myqcloud.com/trtc-calling-doc-assets/videoaccept.gif"/></td>
</tr>
</table>

:::
</dx-tabs>

## Audio Call
TRTC supports one-to-one or group audio calls with dual sound channels and a sample rate of 48 kHz. In the audio call mode, each room allows a maximum of 300 participants, and up to 50 participants can keep their mics on at the same time. Common audio call scenarios include one-to-one audio call, group audio call, audio chat, audio conferencing, audio customer service, audio Werewolf, etc.
<dx-tabs>
::: iOS & Android

<table>
<tr>
   <th>Call</th>
   <th>Answer</th>
 </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/call.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/recv.gif"/></td>
</tr>
</table>

## Interactive Live Video Streaming
The interactive live video streaming mode supports co-anchoring between anchors and audience and cross-room anchor competition. It allows smooth mic on/off without waiting, with anchor latency shorter than 300 ms. There is no limit on the cumulative number of co-anchors in a room, and up to 50 users can co-anchor at the same time. In the low-latency mode, up to 100,000 users can play back at the same time, with latency as low as 1,000 ms. In the relaying mode, there is no limit on audience size. Common interactive live video streaming scenarios include low-latency video streaming, interactive classroom for up to 100,000 participants, live video competition, video dating, remote training, large conference, etc.
<dx-tabs>
::: iOS & Android
<table>
<tr>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/beauty.gif"/></td>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/join.gif"/></td>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/msg.gif"/></td>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/pk.gif"/></td>
</tr>
</table>
:::
::: Desktop Browser
![](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/doc-assets/demo-official-website.gif)
:::
</dx-tabs>

## Interactive Live Audio Streaming
In the interactive live audio streaming mode, listeners can become speakers and interact with the room owner, and speakers from different rooms can compete with each other. The mode supports smooth mic on/off without waiting, with speaker latency shorter than 300 ms. There is no limit on the cumulative number of speakers in a room, and up to 50 users can speak at the same time. In the low-latency mode, up to 100,000 users can play back at the same time, with playback latency as low as 1,000 ms. In the relaying mode, there is no limit on audience size. Common interactive live audio streaming scenarios include low-latency audio streaming, live audio interaction, live audio competition, audio chat room, audio dating, karaoke room, FM radio, etc.
<table>
     <tr>
         <th>Room Owner</th>  
         <th>Listener</th>  
     </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/voiceroom_pick_seat.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/voiceroom_enter_seat.gif"/></td>
</tr>
</table>


## Video Conferencing
The video conferencing mode offers smooth and HD conference experience. It supports 1080p video and 48 kHz audio, with latency shorter than 300 ms. The screen sharing and file sharing features help make conferences more efficient, and instant messaging enables text- and image-based discussion without interrupting a conference. Common video conferencing scenarios including omni-channel customer service, online conference, government/corporate live streaming, etc.
<table>
     <tr>
         <th>Join Conference</th>  
         <th>Share Screen</th>  
     </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/enterroom.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/enterroom.gif"/></td>
</tr>
</table>

## Interactive Classroom
In the interactive classroom mode, students can turn on their mics and interact with the teacher, with latency shorter than 300 ms. The mode allows smooth mic on/off without waiting, and up to 50 users can keep their cameras on at the same time. In the low-latency mode, up to 100,000 students can play the teacher’s video at the same time, with playback latency as low as 1,000 ms. In the relaying mode, there is no limit on audience size. The screen sharing, whiteboard, recording, and replay features deliver richer online education experience. Common interactive classroom scenarios include large class, small class, mini class, AI class, open class for enrollment purpose, corporate training, one-to-one tutoring, etc.
<table>
     <tr>
         <th>Teacher (Electron)</th>  
         <th>Student (Electron)</th>  
     </tr>
<tr>
<td><img src="https://imgcache.qq.com/operation/dianshi/other/Electron_teacher.76058b065f0b01ccc5d6bfd058c6b655e69a149c.gif"/></td>
<td><img src="https://imgcache.qq.com/operation/dianshi/other/Electron_stu.9e3f55291b657d94878963ad86471b331190f47c.gif"/></td>
</tr>
</table>
