<style>
    .card-container {
        width: 380px;
        display: block;
        float: left;
        padding-left: 15px;
        padding-right: 15px;
        box-sizing: border-box;
    }

    .card {
        border-radius: 10px;
        padding-top: 10px;
        padding-left: 10px;
        padding-right: 10px;
        padding-bottom: 10px;
        margin-top: 30px;
        border: 1px solid #ebeef5;
        background-color: #fff;
        overflow: hidden;
        box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
        text-align: center;
    }
    
    .markdown-text-box img {
        box-shadow: none;
    }


    .titlename {
                color:#191919;
        position: relative;
        top: -2px;
                font-weight: bolder;
                font-size: larger;
    }
        
        @media (max-width: 768px){
                .card-container,
                .scene-card-container{
                        width: 100%;
                }
                .scene-card > div{
                        width: 100%!important;
                        margin-left: 0!important;
                }
                img {
        box-shadow: none;
    }
        }
</style>

## SDK Download
TRTC is a set of low-latency and high-quality audio/video communication services provided by Tencent Cloud. It offers stable and reliable audio/video transmission capabilities at a low cost. TRTC services are implemented via a global transmission network and an SDK. You can find below different editions of the TRTC SDK, which cover mainstream platforms and software frameworks.



### Web

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
  <div class="card-container">
      <div class="card">
        <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
        <p class="titlename">TRTC Stable</p>
        <p style="color:#586376;">Integrates TRTC features; allows your users to make audio/video calls without having to install an app; compatible with mainstream desktop and mobile browsers.</p>
        <a onclick="reportEvent({name: 'download-click-web', ext1: 'zip'})" target="_blank" href="https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip">ZIP file</a>
        <a style="margin-left: 10px;" onclick="reportEvent({name: 'download-click-web', ext1: 'github'})" target="_blank" href="https://github.com/LiteAVSDK/TRTC_Web">GitHub</a>
        <a style="margin-left: 10px;" onclick="reportEvent({name: 'download-click-web', ext1: 'doc-sdk'})" target="_blank" href="https://intl.cloud.tencent.com/document/product/647/35096">Integration guide</a>
        <a style="margin-left: 10px;" onclick="reportEvent({name: 'download-click-web', ext1: 'doc-demo'})" target="_blank" href="https://intl.cloud.tencent.com/document/product/647/35607">Demo guide</a>
      </div>
  </div>
</div>

### Android

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                            <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                                <p class="titlename">TRTC Lite</p>
                <p style="color:#586376;">Integrates TRTC features and TXLivePlayer; compact and stable.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip">ZIP file</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Android">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35093">Integration guide</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35084">Demo guide</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                                <p class="titlename">TRTC Professional</p>
                <p style="color:#586376;">Integrates a full range of features including TRTC, live streaming, short video making, and video on demand, with slightly bigger storage footprint than TRTC Lite.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">ZIP file</a>
                <a style="margin-left: 10px;" href="https://github.com/tencentyun/LiteAVProfessional_Android">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35093">Integration guide</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35084">Demo guide</a>
            </div>
        </div>
</div>

### iOS

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                                <p class="titlename">TRTC Lite</p>
                <p style="color:#586376;">Integrates TRTC features and TXLivePlayer; compact and stable.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip">ZIP file</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_iOS">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35092">Integration guide</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35086">Demo guide</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                                <p class="titlename">TRTC Professional</p>
                 <p style="color:#586376;">Integrates a full range of features including TRTC, live streaming, short video making, and video on demand, with slightly bigger storage footprint than TRTC Lite.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">ZIP file</a>
                <a style="margin-left: 10px;" href="https://github.com/tencentyun/LiteAVProfessional_iOS">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35092">Integration guide</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35086">Demo guide</a>
            </div>
        </div>
</div>

### Windows

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/104e3aadbd4515f61c3f2f5378948cfb.svg" data-nonescope="true">
                                <p class="titlename">Windows SDK (C++)</p>
                <p style="color:#586376;">Integrates TRTC, TXLivePusher, TXLivePlayer, and TXVodPlayer.</p>
                          <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">ZIP file</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Windows">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/46745">Integration guide</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/46748">Demo guide</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/104e3aadbd4515f61c3f2f5378948cfb.svg" data-nonescope="true">
                                <p class="titlename">Windows SDK (C#)</p>
                <p style="color:#586376;">Integrates TRTC, TXLivePusher, TXLivePlayer, and TXVodPlayer.</p>
                          <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_CSharp_latest.zip">ZIP file</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Windows">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35095">Integration guide</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/46747">Demo guide</a>
            </div>
        </div>
</div>

### macOS

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                                <img src="https://qcloudimg.tencent-cloud.cn/raw/4f5b5b301babc3ddf4d2867b37c30ffc.png" data-nonescope="true">
                                <p class="titlename">macOS SDK</p>
                <p style="color:#586376;">Integrates TRTC, TXLivePusher, TXLivePlayer, and TXVodPlayer.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2">ZIP file</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Mac">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35094">Integration guide</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35086">Demo guide</a>
            </div>
        </div>
</div>


### Cross-platform

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
									<img src="https://qcloudimg.tencent-cloud.cn/raw/d6fd52f011bdbb13302b2ae261e8a756.png" data-nonescope="true"/>
								<p class="titlename">Electron SDK</p>
                <p style="color:#586376;">An SDK packaged for Electron, which allows you to quickly build apps for Windows or macOS with web technologies.</p>
							<a href="https://web.sdk.qcloud.com/trtc/electron/download/TXLiteAVSDK_TRTC_Electron_latest.zip">ZIP file</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Electron">GitHub</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35097">Integration guide</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35089">Demo guide</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
									<img src="https://qcloudimg.tencent-cloud.cn/raw/3b6929f89ce1113bc2005873f2338de9.png" data-nonescope="true"/>
									<p class="titlename">Flutter SDK</p>
                <p style="color:#586376;">An SDK packaged for Flutter, which allows you to quickly build apps for different platforms using one set of code.</p>
								<a href="https://pub.dev/packages/tencent_trtc_cloud/versions">ZIP file</a>
                <a style="margin-left: 10px;" href="https://github.com/c1avie/trtc_demo">GitHub</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35098">Integration guide</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/39243">Demo guide</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                            <img src="https://qcloudimg.tencent-cloud.cn/raw/90f1ef49218b43d7042bb05b1c0a3959.png" data-nonescope="true">
                                <p class="titlename">React Native SDK</p>
                <p style="color:#586376;">An SDK packaged for React Native, which allows you to quickly build mobile apps using one set of code.</p>
                <a style="margin-left: 10px;" href="https://github.com/tencentyun/TRTCReactNative">GitHub</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/43298">Integration guide</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/43297">Demo guide</a>
            </div>
        </div>
				<div class="card-container">
            <div class="card">
                            <img src="https://qcloudimg.tencent-cloud.cn/raw/e9d18b164152f08bc0694c01e966daea.png" data-nonescope="true">
                                <p class="titlename">uni-app SDK</p>
                <p style="color:#586376;">An SDK packaged for uni-app, which allows you to quickly integrate TRTC capabilities into your project.</p>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_UniApp">GitHub</a>
								<a style="margin-left: 10px;" Demo guide</a>
            </div>
        </div>
</div>



## Edition Comparison
<table>
  <tr>
    <th width="100px" style="text-align:center">Module</th>
    <th width="100px" style="text-align:center">Feature</th>
    <th width="100px" style="text-align:center">TRTC Lite</th>
    <th width="100px" style="text-align:center">TRTC Professional</th>
  </tr>
    <tr>
    <td rowspan='2' style="text-align:center">Video call</td>
    <td style="text-align:center">One-to-one call</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Group conference</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">Co-anchoring</td>
    <td style="text-align:center">Same-room communication</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Cross-room communication</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">Basic beauty filters</td>
    <td style="text-align:center">Skin brightening/smoothing</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Color filters</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
    <tr>
    <td rowspan='2' style="text-align:center">Publishing</td>
    <td style="text-align:center">Camera</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">Screen</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">Playing</td>
    <td style="text-align:center">RTMP</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HTTP-FLV</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HLS (M3U8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">Video on demand</td>
    <td style="text-align:center">MP4</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">HLS (M3U8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">DRM</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">Short video making</td>
    <td style="text-align:center">Recording/Shooting</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Clipping/Splicing</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">TikTok-like special effects</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Video upload</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td rowspan='4' style="text-align:center">Size</td>
    <td style="text-align:center">Android</td>
    <td style="text-align:center">ARMv7: 3.97 MB<br>ARM64: 4.33 MB</td>
    <td style="text-align:center">ARMv7: 9.15 MB<br>ARM64: 10.4 MB</td>
  </tr>
    <tr>
    <td style="text-align:center">iOS</td>
    <td style="text-align:center">ARM64: 3.15 MB</td>
    <td style="text-align:center">N/A</td>
  </tr>
</table>

>! The Windows and macOS SDKs integrate TRTC, TXLivePusher, TXLivePlayer, and TXVodPlayer, but do not offer short video capabilities. They do not come in lite and professional editions.

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
