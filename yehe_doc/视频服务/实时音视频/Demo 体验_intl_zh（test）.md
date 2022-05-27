<style>
.demo-card{
    overflow: auto;
    text-align: center;
    padding:27px 0 0 0;
}
.demo-tab{
    width: 172px;
    height: 258px;
    background: #FFFFFF;
    box-shadow: 0px 1px 8px rgba(156, 175, 204, 0.25);
    border-radius: 4px; 
    float:left;
    margin-left:10px;
}
.card-name{
    font-family: 'PingFang SC';
    font-style: normal;
    font-weight: 600;
    font-size: 14px;
    line-height: 20px;
    color: #000000;
    margin: 0 auto;
}
.card-description{
    font-family: 'PingFang SC';
    font-style: normal;
    font-weight: 400;
    font-size: 12px;
    line-height: 17px;
    text-align: center;
    color: #666666;
    width: 146px;
    height: 34px;
    margin:12px auto;
}
.description-short{
    width: 120px;
}
.description-medium{
    width:140px;
}
.card-button{
    width: 116px;
    height: 32px;
    background: #4DA3F8;
    border-radius: 24px;
    border:0;
    font-family: 'PingFang SC';
    font-style: normal;
    font-weight: 500;
    font-size: 12px;
    line-height: 17px;
    text-align: center;
    color: #FFFFFF;
    margin:44px auto;
}
.web-button{
    width: 116px;
    height: 24px;
    background: #4DA3F8;
    border-radius: 24px;
    font-family: 'PingFang SC';
    font-style: normal;
    font-weight: 500;
    font-size: 12px;
    line-height: 17px;
    text-align: center;
    color: #FFFFFF;
    border:0;
    margin-top:6px;
}
.electron-button{
    width: 116px;
    height: 32px;
    background: #4DA3F8;
    border-radius: 24px;
    font-family: 'PingFang SC';
    font-style: normal;
    font-weight: 500;
    font-size: 12px;
    line-height: 17px;
    text-align: center;
    color: #FFFFFF;
    margin-top:8px;
    border:0;
}
.support-platform{
    width: 56px;
    height: 24px;
    font-family: PingFangSC-Regular;
    font-weight: 400;
    font-size: 14px;
    color: #333333;
    letter-spacing: 0;
    line-height: 24px;
}
.tab-bottom{
    width: 760px;
    height: 172px;
    background: #EDF1F5;
    border-radius: 8px;
    display:flex;
    justify-content: center;
    align-items: center;
}
.tab-support{
    height:24px;
    text-align:center;
    padding: 24px 0 0 0;
}
.platform-img{
    width: 18px;
    height: 18px;
    box-shadow: 0 0 0 0 #FFFFFF;
    vertical-align:-4px;
    padding:0 8px;
}
.tab-experience{
    width: 150px;
    height: 40px;
    background: #FFFFFF;
    box-shadow: 0 2px 4px 0 rgba(215,226,236,0.40);
    border-radius: 20px;
    border:0;
    color:#06A4FF;
    line-height:40px;
}
.tab-img{
    width:760px;
}
.tab-android{left:84px;}
.tab-ios{left:266px}
.tab-windows{left:448px}
.tab-mac{left:630px}
.demo-card{top:146px;}
.over-demo{top:476px}
</style>

<div class="demo-card" id="demo-card">
    <div class="demo-tab tab-android demo-card">
        <img src="https://qcloudimg.tencent-cloud.cn/raw/53be7f245c4d11d3aefcb6dc53918757.svg" data-nonescope="true">
        <div class="card-name">Android</div>
        <div class="card-description">音视频通话·多人会议·KTV语音聊天·互动直播等等</div>
        <img style="width:101.2px;height: 98.56px;" src="https://main.qcloudimg.com/raw/8a603ced0a61983018c794df842f7029.png" data-nonescope="true">
    </div>
    <div class="demo-tab tab-ios demo-card">
        <img src="https://qcloudimg.tencent-cloud.cn/raw/36154dc8bb7c93826dbdc6fdcec4e194.svg" data-nonescope="true">
        <div class="card-name">iOS</div>
        <div class="card-description">音视频通话·多人会议·KTV语音聊天·互动直播等等</div>
        <img style="width:101.2px;height: 98.56px;" src="https://web.sdk.qcloud.com/document/assets/ios-download.png" data-nonescope="true">
    </div>
    <div class="demo-tab tab-windows demo-card">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/7622934bfd307936181d3a57ed69706d.svg" data-nonescope="true">
         <div class="card-name">Windows</div>
         <div class="card-description description-short">音视频通话·多人会议语音聊天室</div>
         <a onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Win_Demo.exe');reportEvent({name: 'demo-click-native', ext1: 'windows'});"><button class="card-button">立即下载</button></a>
    </div>
    <div class="demo-tab tab-mac demo-card">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/2f867a868913c590fbb2929b8b240f45.svg" data-nonescope="true">
         <div class="card-name">Mac OS</div>
         <div class="card-description description-short">音视频通话·多人会议语音聊天室</div>
         <a onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Mac_Demo.tar.bz2');reportEvent({name: 'demo-click-native', ext1: 'windows'});"><button class="card-button">立即下载</button></a>
    </div>
</div>

<div class="demo-card">
    <div class="demo-tab tab-ios demo-card">
        <img src="https://qcloudimg.tencent-cloud.cn/raw/ff4dc34a1c72fdb26fc41c1268898025.svg" data-nonescope="true">
        <div class="card-name">Web</div>
        <div class="card-description">单击即可体验</div>
        <input type="button" value="视频通话" class="web-button" onclick="window.open('https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/login.html');reportEvent({name: 'intl-demo-click-web', ext1: 'api-sample'});" />
        <input type="button" value="互动直播推流" class="web-button" onclick="window.open('https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/login.html');reportEvent({name: 'intl-demo-click-web', ext1: 'pusher'});" />
        <input type="button" value="互动直播拉流" class="web-button" onclick="window.open('https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/login.html');reportEvent({name: 'intl-demo-click-web', ext1: 'player'});" />
    </div>
    <div class="demo-tab tab-windows demo-card">
        <img src="https://qcloudimg.tencent-cloud.cn/raw/0fae0aca728ba2ce98e66d1b9641aa56.svg" data-nonescope="true">
        <div class="card-name">Flutter</div>
        <div class="card-description" style="width:74px">音视频通话 多人会议等等</div>
        <a onclick="window.open('https://comm.qq.com/im_demo_download/trtc_flutter_demo.apk');reportEvent({name: 'demo-click-flutter', ext1: 'android'});"><button class="card-button">立即下载</button></a>
    </div>
    <div class="demo-tab tab-mac demo-card">
        <img src="https://qcloudimg.tencent-cloud.cn/raw/96a6b7e86eb8d7a93f830d3686d3164c.svg" data-nonescope="true">
        <div class="card-name">Electron</div>
        <div class="card-description description-short">音视频通话·多人会议 屏幕分享等等</div>
        <input type="button" value="下载Windows版" class="electron-button" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-windows-latest.zip');reportEvent({name: 'demo-click-electron', ext1: 'windows'});"/>
        <input type="button" value="下载Mac OS版" class="electron-button" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-mac-latest.zip');reportEvent({name: 'demo-click-electron', ext1: 'mac'});" />
        </div>  
</div>


## 音视频通话场景

<dx-tabs>
::: iOS&Android
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/f3ac5b4c3da1c11a5007be44ccf023b8.png"/>
</div>
:::
::: Web
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/2d0a1b7f1de11f5672c0bf90e7e7260d.png"/>
</div>
:::
</dx-tabs>
<div class="tab-bottom">
    <div style="margin-bottom:24px;">
         <div class="tab-support">
        <span class="support-platform">Demo支持平台</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/cf4c9ee1645ee381b7fec591223b8f75.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/584b9e4444422c19af20536317680ed3.svg" class="platform-img">Uni-App</span>
    </div>
    <div style="text-align:center;height:60px;line-height:60px;"><a href="#demo-card"><button class="tab-experience">立即体验</button></a></div>
    <div style="text-align:center;">您可以点击<a href="https://intl.cloud.tencent.com/zh/document/product/647/46660" style="color:#06A4FF;">接入指引</a>了解如何快速集成，或点击<a href="https://github.com/tencentyun/TUICalling" style="color:#06A4FF;">源码下载</a>到Github下载最新代码</div>
    </div>
</div>

</dx-tabs>

## 视频互动直播场景
<dx-tabs>
::: iOS&Android
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/2e36776b2d39ebc96b6cf710d26bbac1.png"/>
</div>
:::
::: Web
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/a1b695299411c75c31799f648732a4c8.png"/>
</div>
:::
</dx-tabs>
<div class="tab-bottom">
    <div style="margin-bottom:24px;">
         <div class="tab-support">
        <span class="support-platform">Demo支持平台</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/cf4c9ee1645ee381b7fec591223b8f75.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/4dcbeb0def10b73f0ce7bee9609054a4.svg" class="platform-img">H5</span>
    </div>
    <div style="text-align:center;height:60px;line-height:60px;"><a href="#demo-card"><button class="tab-experience">立即体验</button></a></div>
    <div style="text-align:center;">您可以点击<a href="https://intl.cloud.tencent.com/zh/document/product/647/46666" style="color:#06A4FF;">接入指引</a>了解如何快速集成，或点击<a href="https://github.com/tencentyun/TUILiveRoom" style="color:#06A4FF;">源码下载</a>到Github下载最新代码</div>
    </div>
</div>

</dx-tabs>

## 语音互动直播场景
<dx-tabs>
::: iOS&Android
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/5209e7aafb9e6af42864b98d8866992f.png"/>
</div>
:::
</dx-tabs>
<div class="tab-bottom">
    <div style="margin-bottom:24px;">
         <div class="tab-support">
        <span class="support-platform">Demo支持平台</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
    </div>
    <div style="text-align:center;height:60px;line-height:60px;"><a href="#demo-card"><button class="tab-experience">立即体验</button></a></div>
    <div style="text-align:center;">您可以点击<a href="https://intl.cloud.tencent.com/zh/document/product/647/46664" style="color:#06A4FF;">接入指引</a>了解如何快速集成，或点击<a href="" style="color:#06A4FF;">源码下载</a>到Github下载最新代码</div>
    </div>
</div>

</dx-tabs>
## 视频会议场景
<dx-tabs>
::: iOS&Android
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/079d1517df12400d24a7f64cf18e4078.png"/>
</div>
:::
::: Web
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/9e6ae0ed1111c51b746434d5a3932a07.png"/>
</div>
:::
::: Windows & Mac
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/453ddd0cf87b703fb053337d4bcd0683.png"/>
</div>
:::
</dx-tabs>
<div class="tab-bottom">
    <div style="margin-bottom:24px;">
         <div class="tab-support">
        <span class="support-platform">Demo支持平台</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/cf4c9ee1645ee381b7fec591223b8f75.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/4dcbeb0def10b73f0ce7bee9609054a4.svg" class="platform-img">Flutter</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">Windows</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/4dcbeb0def10b73f0ce7bee9609054a4.svg" class="platform-img">Mac OS</span>
    </div>
   <div style="text-align:center;height:60px;line-height:60px;"><a href="#demo-card"><button class="tab-experience">立即体验</button></a></div>
    <div style="text-align:center;">您可以点击<a href="https://intl.cloud.tencent.com/zh/document/product/647/46662" style="color:#06A4FF;">接入指引</a>了解如何快速集成，或点击<a href="https://github.com/tencentyun/TUIRoom" style="color:#06A4FF;">源码下载</a>到Github下载最新代码</div>
    </div>
</div>

</dx-tabs>

## 在线K歌场景
<dx-tabs>
::: iOS&Android
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/c9a605c93ec8f19a13ede4089ccb2591.png"/>
</div>
:::
</dx-tabs>
<div class="tab-bottom">
    <div style="margin-bottom:24px;">
         <div class="tab-support">
        <span class="support-platform">Demo支持平台</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
    </div>
    <div style="text-align:center;height:60px;line-height:60px;"><a href="#demo-card"><button class="tab-experience">立即体验</button></a></div>
    <div style="text-align:center;">您可以点击<a href="https://intl.cloud.tencent.com/zh/document/product/647/46668" style="color:#06A4FF;">接入指引</a>了解如何快速集成，或点击<a href="https://github.com/tencentyun/TUIKaraoke" style="color:#06A4FF;">源码下载</a>到Github下载最新代码</div>
    </div>
</div>

</dx-tabs>

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
