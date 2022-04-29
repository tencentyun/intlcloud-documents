<style>
.markdown-text-box table th,.markdown-text-box table td{text-align: center;}
.inbuttom{height: 30px;width: 150px;min-width: 24px;padding: 0 20px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;vertical-align: middle;white-space: nowrap;}
.preview-demo-section .preview-demo-item {
    display: inline-block;
    width: 200px;
    height: 300px;
    background: #fff;
    box-shadow: 0 1px 8px 0 rgba(156,175,204,0.25);
    border-radius: 1px;
    text-align: center;
    padding: 0 15px;
    margin: 10px 10px 10px 0;
    vertical-align: top;
}

.preview-demo-section .preview-demo-item .demo-item-header {
    margin-top: 30px;
}

.preview-demo-section .preview-demo-item .demo-item-desc {
    font-size: 12px;
}

.preview-demo-section .preview-demo-item .demo-item-platform {
    font-size: 20px;
    font-weight: bold;
}
.preview-demo-section .preview-demo-item .demo-logo-wrapper {
    line-height: 1;
}
.preview-demo-section .preview-demo-item .demo-item-header img {
    box-shadow: none;
    width: 40px;
    height: 40px;
}
.preview-demo-section .preview-demo-item.style-qrcode .demo-item-download {
    margin-top: 15px;
}
.preview-demo-section .preview-demo-item.style-web .demo-item-download {
    margin-top: 25px;
}
.preview-demo-section .preview-demo-item.style-single-download-btn .demo-item-download {
    margin-top: 50px;
}
.preview-demo-section .preview-demo-item.style-flutter .demo-item-download {
    margin-top: 55px;
}
.preview-demo-section .preview-demo-item.style-electron .demo-item-download {
    margin-top: 25px;
}
.preview-demo-section .preview-demo-item.style-electron .demo-item-download-btn:first-child {
    margin-bottom: 10px;
}
.preview-demo-section .preview-demo-item .demo-item-download img {
    box-shadow: none;
    width: 110px;
    height: 110px;
}
.preview-demo-section .preview-demo-item .demo-item-download .demo-item-download-btn {
    background-color: #00a4ff;
    border-radius: 20px;
    color: #fff;
    font-size: 14px;
    width: 135px;
    height: 35px;
    line-height: 35px;
    margin: 0 auto;
}
.preview-demo-section .preview-demo-item.style-web .demo-item-download .demo-item-download-btn {
    color: #fff;
    background-color: #00a4ff;
    height: 24px;
    line-height: 24px;
    margin-bottom: 6px;
}
.preview-demo-section .preview-demo-item .demo-item-download .demo-item-download-btn:hover {
    cursor: pointer;
}
</style>

<div class="preview-demo-section">
    <div class="preview-demo-item style-qrcode">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/53be7f245c4d11d3aefcb6dc53918757.svg" alt="">
            </div>
            <div class="demo-item-platform">Android</div>
        </div>
        <div class="demo-item-desc">
            Audio/Video call, group conference, karaoke, <br>audio chat room,interactive live streaming
        </div>
        <div class="demo-item-download">
            <img src="https://main.qcloudimg.com/raw/8a603ced0a61983018c794df842f7029.png" data-nonescope="true">
        </div>
    </div>
    <div class="preview-demo-item style-qrcode">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/36154dc8bb7c93826dbdc6fdcec4e194.svg" alt="">
            </div>
            <div class="demo-item-platform">iOS</div>
        </div>
        <div class="demo-item-desc">
            Audio/Video call, group conference, karaoke, <br>audio chat room,interactive live streaming
        </div>
        <div class="demo-item-download">
            <img src="https://main.qcloudimg.com/raw/a1a6fd4a9bc3ad2b5fe60e31202c8fda.png" data-nonescope="true">
        </div>
    </div>
    <div class="preview-demo-item style-single-download-btn">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/7622934bfd307936181d3a57ed69706d.svg" alt="">
            </div>
            <div class="demo-item-platform">Windows</div>
        </div>
        <div class="demo-item-desc">
            Audio/Video call, group conference, audio chat room
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Win_Demo.exe');reportEvent({name: 'demo-click-native', ext1: 'windows'});">Download</div>
        </div>
    </div>
    <div class="preview-demo-item style-single-download-btn">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/2f867a868913c590fbb2929b8b240f45.svg" alt="">
            </div>
            <div class="demo-item-platform">Mac OS</div>
        </div>
        <div class="demo-item-desc">
            Audio/Video call, group conference, audio chat room
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Mac_Demo.tar.bz2');reportEvent({name: 'demo-click-native', ext1: 'windows'});">Download/div>
        </div>
    </div>
    <div class="preview-demo-item style-web">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/ff4dc34a1c72fdb26fc41c1268898025.svg" alt="">
            </div>
            <div class="demo-item-platform">Web</div>
        </div>
        <div class="demo-item-desc">
           Try now
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-rtc.html');reportEvent({name: 'demo-click-web', ext1: 'api-example'});">Video call</div>
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/pusher.html');reportEvent({name: 'demo-click-web', ext1: 'pusher'});">interactive live streaming-Pusher</div>
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/player.html');reportEvent({name: 'demo-click-web', ext1: 'player'});">interactive live streaming-Player</div>
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/component/trtccalling/demo/web/latest/index.html');reportEvent({name: 'demo-click-web', ext1: 'calling'});">One-to-one audio/video call</div>
        </div>
    </div>
    <div class="preview-demo-item style-flutter">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/0fae0aca728ba2ce98e66d1b9641aa56.svg" alt="">
            </div>
            <div class="demo-item-platform">Flutter</div>
        </div>
        <div class="demo-item-desc">
            Audio/Video call, group conference
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://comm.qq.com/im_demo_download/trtc_flutter_demo.apk');reportEvent({name: 'demo-click-flutter', ext1: 'android'});">Download</div>
        </div>
    </div>
    <div class="preview-demo-item style-electron">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/96a6b7e86eb8d7a93f830d3686d3164c.svg" alt="">
            </div>
            <div class="demo-item-platform">Electron</div>
        </div>
        <div class="demo-item-desc">
            Audio/Video call, group conference, screen sharing
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-windows-latest.zip');reportEvent({name: 'demo-click-electron', ext1: 'windows'});">Windows</div>
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-mac-latest.zip');reportEvent({name: 'demo-click-electron', ext1: 'mac'});">macOS</div>
        </div>
    </div>
</div> 


## Video Call
TRTC supports one-to-one and group video calls at a resolution of 720p or 1080p. In the video call mode, each room allows a maximum of 300 concurrent participants, and up to 50 participants can keep their cameras on at the same time. Common video call scenarios include one-to-one video call, video conference with up to 300 people, online medical consultation, video chat, video customer service, video interviews, audio/video recording, online insurance claim settlement, video Werewolf, etc.
<dx-tabs>
::: iOS & Android
<table>
<tr>
   <th>Call</th>
   <th>Answer</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/ef83db73d0a8c487e72986dd1f92e361.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/f57ed3a55112233b05260f5dc37342ca.jpeg"/></td>
</tr>
</table>
:::

</dx-tabs>

## Audio Call
TRTC supports one-to-one or group audio calls with dual sound channels and a sample rate of 48 kHz. In the audio call mode, each room allows a maximum of 300 concurrent participants, and up to 50 participants can keep their mics on at the same time. Common audio call scenarios include one-to-one audio call, group audio call, audio chat, audio conferencing, audio customer service, audio Werewolf, etc.
<dx-tabs>
::: iOS & Android
<table>
<tr>
   <th>Call</th>
   <th>Answer</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/7b03f80d5ad33bd33b6fb551e392b4d3.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/60581f007dda722e06af6333b13afbd4.jpeg"/></td>
</tr>
</table>
:::

</dx-tabs>

## Interactive Live Video Streaming
The interactive live video streaming mode supports co-anchoring between anchors and audience and cross-room anchor competition. It allows smooth mic on/off without waiting, with anchor latency shorter than 300 ms. There is no limit on the cumulative number of co-anchors in a room, and up to 50 users can co-anchor at the same time. In the low-latency mode, up to 100,000 users can play back at the same time, with latency as low as 1,000 ms. In the CDN live streaming mode, there is no limit on audience size. Common interactive live video streaming scenarios include low-latency video streaming, interactive classroom for up to 100,000 participants, live video competition, video dating, remote training, large conference, etc.
<dx-tabs>
::: iOS & Android
<table>
<tr>
<td><img width="260" height="561" src="https://main.qcloudimg.com/raw/317b3eb7ebf971ef7291dec2bacfa18a.jpeg"/></td>
<td><img width="260" height="561" src="https://main.qcloudimg.com/raw/162112aa8768d0db63e1850c2495a370.jpeg"/></td>
<td><img width="260" height="561" src="https://main.qcloudimg.com/raw/dab9fe1e5c93deb5ee02155b27bdf639.jpeg"/></td>
<td><img width="260" height="561" src="https://main.qcloudimg.com/raw/3182620f791a594d555ecab0cd170e1f.jpeg"/></td>
</tr>
</table>
                                                                                                            
:::
::: Web
## Interactive Live Audio Streaming
In the interactive live audio streaming mode, listeners can become speakers and interact with the room owner, and room owners can compete with each other. It supports smooth mic on/off without waiting, with speaker latency shorter than 300 ms. There is no limit on the cumulative number of speakers in a room, and up to 50 users can speak at the same time. In the low-latency mode, up to 100,000 users can play back at the same time, with latency as low as 1,000 ms. In the CDN live streaming mode, there is no limit on audience size. Common interactive live audio streaming scenarios include low-latency audio streaming, live audio interaction, live audio competition, audio chat room, audio dating, karaoke room, FM radio, etc.
<table>
     <tr>
         <th>Room Owner</th>  
         <th>Audience</th>  
     </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/dd836080683a49418bc548bfb9f59857.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/7b73bfdd915a0ba281c52b9ac0518b80.jpeg"/></td>
</tr>
</table>
:::
</dx-tabs>

## Video Conferencing
The video conferencing mode offers smooth and HD conference experience. It supports 1080p video and 48 kHz audio, with latency shorter than 300 ms. The screen sharing and file sharing features help make conferences more efficient, and instant messaging enables text- and image-based discussion without interrupting a conference. Common video conferencing scenarios including omni-channel customer service, online conference, government/corporate live streaming, etc.
<table>
     <tr>
         <th>Join Conference</th>  
         <th>Share Screen</th>  
     </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/a1fc2d23946377cb9466d8b645c14d24.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/5c613b7c7ee890b7e3feb7a3270a9a89.jpeg"/></td>
</tr>
</table>

## Interactive Classroom
The interactive classroom mode allows teacher-student interaction and smooth mic on/off without waiting. Up to 50 participants can keep their mics on at the same time, with latency shorter than 300 ms. In the low-latency mode, up to 100,000 students can play the teacher’s video at the same time, with latency as low as 1,000 ms. In the CDN live streaming mode, there is no limit on audience size. The screen sharing, whiteboard, recording, and replay features help enrich online education experience. Common interactive classroom scenarios include large class, small class, mini class, AI class, open class for enrollment purposes, corporate training, one-to-one tutoring, etc.

| <img src="https://main.qcloudimg.com/raw/76cb1831b3f4b5340243a6b7406d8d73.png" alt="wecom-temp-799c836bbc6c6c3cd9fed14d03465f5d" style="zoom:50%;" /> | <img src="https://main.qcloudimg.com/raw/ca1e4f364230e18b78c7789cf8db08ae.png" alt="wecom-temp-d05e8b456350695101a745553926b07e" style="zoom:28%;" /> |
| ------------------------------------------------------------ | ------------------------------------------------------------ |


## Online Karaoke
In the karaoke mode, the room owner and audience can turn their mics on and sing. It supports smooth mic on/off without waiting, with singer latency shorter than 300 ms. There is no limit on the cumulative number of singers in a room, and up to 50 users can sing at the same time. In the low-latency mode, up to 100,000 users can play back at the same time, with latency as low as 1,000 ms. In the CDN live streaming mode, there is no limit on audience size. Common karaoke scenarios include low-latency audio streaming, live audio interaction, live audio competition, audio chat room, audio dating, karaoke room, FM radio, etc.
<table>
     <tr>
         <th>Request Song (Room Owner)</th>  
         <th>Request Song (Audience)</th>  
     </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/dcb4f550d478b35212f4b7ef5c332fcf.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/90dff32d6b506237ce3725083b47421a.jpeg"/></td>
</tr>
</table>


<script src="https://cdn-go.cn/aegis/aegis-sdk/latest/aegis.min.js"></script>
<script>
let aegis;
if(Aegis) {
    aegis = new Aegis({
        id: 'iHWefAYqlXjjlfAkpx',
        uin: document.cookie.replace(/(?:(?:^|.*;\s*)uin\s*\=\s*([^;]*).*$)|^.*$/, "$1")|| '',
        reportApiSpeed: false,
        reportAssetSpeed: false
    });
}
function reportEvent(options){ aegis && aegis.reportEvent(options); }
</script>
