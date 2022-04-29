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
            音视频通话、多人会议、KTV、语音聊天室、互动直播等
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
            音视频通话、多人会议、KTV、语音聊天室、互动直播等
        </div>
        <div class="demo-item-download">
            <img src="https://web.sdk.qcloud.com/document/assets/ios-download.png" data-nonescope="true">
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
            音视频通话、多人会议、<br>语音聊天室
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Win_Demo.exe');reportEvent({name: 'demo-click-native', ext1: 'windows'});">立即下载</div>
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
            音视频通话、多人会议、<br>语音聊天室
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Mac_Demo.tar.bz2');reportEvent({name: 'demo-click-native', ext1: 'windows'});">立即下载</div>
        </div>
    </div>
    <div class="preview-demo-item style-qrcode">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/f86154130067ff386c90306fd71dfdce.svg" alt="">
            </div>
            <div class="demo-item-platform">微信小程序</div>
        </div>
        <div class="demo-item-desc">
            语音聊天室、音视频通话、<br>多人会议
        </div>
        <div class="demo-item-download">
            <img src="https://main.qcloudimg.com/raw/4cfc59a1b60c02fc975c8b3e23169fc7.png" data-nonescope="true">
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
           单击即可体验
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-rtc.html');reportEvent({name: 'demo-click-web', ext1: 'api-example'});">视频通话</div>
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/pusher.html');reportEvent({name: 'demo-click-web', ext1: 'pusher'});">互动直播推流</div>
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/player.html');reportEvent({name: 'demo-click-web', ext1: 'player'});">互动直播拉流</div>
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/component/trtccalling/demo/web/latest/index.html');reportEvent({name: 'demo-click-web', ext1: 'calling'});">1v1音视频通话</div>
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
            音视频通话、多人会议等
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://comm.qq.com/im_demo_download/trtc_flutter_demo.apk');reportEvent({name: 'demo-click-flutter', ext1: 'android'});">立即下载</div>
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
            音视频通话、多人会议、<br>屏幕分享等
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-windows-latest.zip');reportEvent({name: 'demo-click-electron', ext1: 'windows'});">下载 Windows 版</div>
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-mac-latest.zip');reportEvent({name: 'demo-click-electron', ext1: 'mac'});">下载 Mac OS 版</div>
        </div>
    </div>
</div> 




## 视频通话场景
视频通话场景即两人或多人视频通话，支持720P、1080P高清画质；单个房间最多支持300人同时在线，最多支持50人同时开启摄像头。常见应用场景有1对1视频通话、300人视频会议、在线问诊、视频聊天、视频客服、视频面审、视频双录、在线理赔、视频狼人杀等。
<dx-tabs>
::: iOS&Android
<table>
<tr>
   <th>主动呼叫</th>
   <th>被叫接听</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/ef83db73d0a8c487e72986dd1f92e361.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/f57ed3a55112233b05260f5dc37342ca.jpeg"/></td>
</tr>
</table>
:::

</dx-tabs>

## 语音通话场景
语音通话场景即两人或多人语音通话，支持 48kHz，支持双声道；单个房间最多支持300人同时在线，最多支持50人同时开启麦克风。常见应用场景有1对1语音通话、多人语音通话、语音聊天、语音会议、语音客服、狼人杀等。
<dx-tabs>
::: iOS&Android
<table>
<tr>
   <th>主动呼叫</th>
   <th>被叫接听</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/7b03f80d5ad33bd33b6fb551e392b4d3.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/60581f007dda722e06af6333b13afbd4.jpeg"/></td>
</tr>
</table>
:::

</dx-tabs>

## 视频互动直播场景
视频互动直播场景支持主播与观众视频连麦互动；支持主播跨房间（跨直播间）PK；支持平滑上下麦，切换过程无需等待，主播延时小于300ms；单个房间可连麦人数无限制，最多支持50人同时连麦；低延时直播模式下，支持10万观众同时播放，播放延时低至1000ms；CDN 旁路直播模式下，观众数量无限制。常见应用场景有视频低延时直播、十万人互动课堂、视频直播 PK、视频相亲房、互动课堂、远程培训、大型会议等。
<dx-tabs>
::: iOS&Android
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
## 语音互动直播场景
语音互动直播场景支持主播与观众语音连麦互动；支持主播跨房间（跨直播间）PK；支持平滑上下麦，切换过程无需等待，主播延时小于300ms；单个房间可连麦人数无限制，最多支持50人同时连麦；低延时直播模式下，支持10万观众同时播放，播放延时低至1000ms；CDN 旁路直播模式下，观众数量无限制。常见应用场景有语音低延时直播、语音直播连麦、语音直播 PK、语聊房、语音相亲房、K 歌房、FM 电台等。
<table>
     <tr>
         <th>主播麦位操作</th>  
         <th>观众麦位操作</th>  
     </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/dd836080683a49418bc548bfb9f59857.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/7b73bfdd915a0ba281c52b9ac0518b80.jpeg"/></td>
</tr>
</table>
:::
</dx-tabs>

## 视频会议场景
视频会议场景支持 支持1080p高清画质与48kHz高音质，音视频时延低于300ms，畅享流畅高清的会议体验；支持屏幕分享、文件分享，让会议更高效；并结合即时通信，支持文字图片等多种形式辅助讨论，不干扰会议进程。常见的应用场景有全媒体客服、在线会议、政企业直播等。
<table>
     <tr>
         <th>进入会议</th>  
         <th>屏幕分享</th>  
     </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/a1fc2d23946377cb9466d8b645c14d24.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/5c613b7c7ee890b7e3feb7a3270a9a89.jpeg"/></td>
</tr>
</table>

## 互动课堂场景
互动课堂场景支持老师和学生互动连麦，最多支持50人同时连麦，平滑上下麦，切换过程无需等待，沟通时延低于300ms；低延时直播模式下，支持10万学生同时观看，观看时延低至1000ms，CDN 旁路直播下，观众人数无限制；支持屏幕共享、互动白板、录制回放等多种课堂应用功能，打造形式更加丰富的线上教学。常见业务场景有大班课、小班课、超级小班课、AI课堂、招生课、内训直播课、1V1在线教育等。

| <img src="https://main.qcloudimg.com/raw/e08f0225d255b94c31b03512553a654b.png" alt="wecom-temp-799c836bbc6c6c3cd9fed14d03465f5d" style="zoom:50%;" /> | <img src="https://main.qcloudimg.com/raw/ca1e4f364230e18b78c7789cf8db08ae.png" alt="wecom-temp-d05e8b456350695101a745553926b07e" style="zoom:28%;" /> |
| ------------------------------------------------------------ | ------------------------------------------------------------ |


## 在线 K 歌（KTV 场景）
KTV 场景支持主播与观众上麦唱歌；支持平滑上下麦，切换过程无需等待，主播延时小于300ms；单个房间可连麦人数无限制，最多支持50人同时连麦；低延时直播模式下，支持10万观众同时播放，播放延时低至1000ms；CDN 旁路直播模式下，观众数量无限制。常见应用场景有语音低延时直播、语音直播连麦、语音直播 PK、语聊房、语音相亲房、K 歌房、FM 电台等。
<table>
     <tr>
         <th>房主点歌操作</th>  
         <th>观众点歌操作</th>  
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
