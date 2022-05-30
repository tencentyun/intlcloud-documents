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

## SDK 다운로드
TRTC는 Tencent Cloud에서 제공하는 저지연 고품질 오디오/비디오 통신 서비스 세트입니다. 안정적인 오디오/비디오 전송 기능을 저렴한 비용으로 제공합니다. TRTC 서비스는 글로벌 전송 네트워크와 SDK를 통해 구현됩니다. 주류 플랫폼 및 소프트웨어 프레임워크를 다루는 다양한 버전의 TRTC SDK(음성/영상 통화 SDK)를 아래에서 찾을 수 있습니다.

>? 현재 Github에 대한 네트워크 액세스 속도가 이상적이지 않은 경우 [여기를 클릭](https://gitee.com/liteavsdk)하여 Gitee의 이미지 레지스트리에 액세스할 수 있습니다.

### Web SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
  <div class="card-container">
      <div class="card">
        <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
        <p class="titlename">안정 버전(TRTC)SDK</p>
        <p style="color:#586376;">TRTC 기능을 포함하며, App을 설치하지 않고도 음성 및 영상 통화를 할 수 있으며 주요 데스크톱 및 모바일 브라우저와 호환됩니다.</p>
        <a onclick="reportEvent({name: 'download-click-web', ext1: 'zip'})" target="_blank" href="https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip">ZIP 다운로드</a>
        <a style="margin-left: 10px;" onclick="reportEvent({name: 'download-click-web', ext1: 'github'})" target="_blank" href="https://github.com/LiteAVSDK/TRTC_Web">GitHub</a>
        <a style="margin-left: 10px;" onclick="reportEvent({name: 'download-click-web', ext1: 'doc-sdk'})" target="_blank" href="https://intl.cloud.tencent.com/document/product/647/35096">통합 가이드</a>
        <a style="margin-left: 10px;" onclick="reportEvent({name: 'download-click-web', ext1: 'doc-demo'})" target="_blank" href="https://intl.cloud.tencent.com/document/product/647/35607">Demo 실행</a>
      </div>
  </div>
</div>

### Android SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                            <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                                <p class="titlename">라이트 버전(TRTC)SDK</p>
                <p style="color:#586376;">TRTC와 TXLivePlayer의 두 가지 기능을 포함하는 SDK는 용량이 작고 기능이 안정적입니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Android">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35093">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35084">Demo 실행</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                                <p class="titlename">다기능 버전(Professional)SDK</p>
                <p style="color:#586376;">TRTC, 라이브 스트리밍, 쇼트 비디오 제작 및 VOD 등 다양한 기능이 포함되어있으며, SDK는 라이트 버전보다 약간 큽니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/tencentyun/LiteAVProfessional_Android">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35093">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35084">Demo 실행</a>
            </div>
        </div>
</div>

### iOS SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                                <p class="titlename">라이트 버전(TRTC)SDK</p>
                <p style="color:#586376;">TRTC와 TXLivePlayer의 두 가지 기능이 포함되어 있으며, SDK는 용량이 작고 기능이 안정적입니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_iOS">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35092">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35086">Demo 실행</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                                <p class="titlename">다기능 버전(Professional)SDK</p>
                 <p style="color:#586376;">TRTC, 라이브 스트리밍, 쇼트 비디오 제작 및 VOD 등 다양한 기능이 포함되어있으며, SDK는 라이트 버전보다 약간 큽니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/tencentyun/LiteAVProfessional_iOS">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35092">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35086">Demo 실행</a>
            </div>
        </div>
</div>

### Windows SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/104e3aadbd4515f61c3f2f5378948cfb.svg" data-nonescope="true">
                                <p class="titlename">Windows SDK(C++ 버전)</p>
                <p style="color:#586376;">TRTC, TXLivePusher, TXLivePlayer 및 TXVodPlayer의 네 가지 기능이 포함되어 있습니다.</p>
                          <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Windows">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/46745">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/46748">Demo 실행</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/104e3aadbd4515f61c3f2f5378948cfb.svg" data-nonescope="true">
                                <p class="titlename">Windows SDK(C# 버전)</p>
                <p style="color:#586376;">TRTC, TXLivePusher, TXLivePlayer 및 TXVodPlayer의 네 가지 기능이 포함되어 있습니다.</p>
                          <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_CSharp_latest.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Windows">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35095">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/46747">Demo 실행</a>
            </div>
        </div>
</div>

### Mac OS SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                                <img src="https://qcloudimg.tencent-cloud.cn/raw/4f5b5b301babc3ddf4d2867b37c30ffc.png" data-nonescope="true">
                                <p class="titlename">Mac OS SDK</p>
                <p style="color:#586376;">TRTC, TXLivePusher, TXLivePlayer 및 TXVodPlayer의 네 가지 기능이 포함되어 있습니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Mac">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35094">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35086">Demo 실행</a>
            </div>
        </div>
</div>


### 크로스 플랫폼 SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
									<img src="https://qcloudimg.tencent-cloud.cn/raw/d6fd52f011bdbb13302b2ae261e8a756.png" data-nonescope="true"/>
								<p class="titlename">Electron SDK</p>
                <p style="color:#586376;">Electron 프레임워크 캡슐화를 기반으로 하며, Web 기술을 기반으로 Windows 및 Mac 플랫폼에서 애플리케이션을 빠르게 구축할 수 있습니다.</p>
							<a href="https://web.sdk.qcloud.com/trtc/electron/download/TXLiteAVSDK_TRTC_Electron_latest.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Electron">GitHub</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35097">통합 가이드</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35089">Demo 실행</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
									<img src="https://qcloudimg.tencent-cloud.cn/raw/3b6929f89ce1113bc2005873f2338de9.png" data-nonescope="true"/>
									<p class="titlename">Flutter SDK</p>
                <p style="color:#586376;">Flutter 프레임워크로 캡슐화된 TRTC SDK 기반 코드 세트로 다양한 플랫폼에서 실행할 수 있는 App을 빠르게 구축할 수 있습니다.</p>
								<a href="https://pub.dev/packages/tencent_trtc_cloud/versions">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/c1avie/trtc_demo">GitHub</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35098">통합 가이드</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/39243">Demo 실행</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                            <img src="https://qcloudimg.tencent-cloud.cn/raw/90f1ef49218b43d7042bb05b1c0a3959.png" data-nonescope="true">
                                <p class="titlename">React Native SDK</p>
                <p style="color:#586376;">React Native 프레임워크로 캡슐화된 TRTC SDK 기반 코드 세트로 모바일 App을 빠르게 구축할 수 있습니다.</p>
                <a style="margin-left: 10px;" href="https://github.com/tencentyun/TRTCReactNative">GitHub</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/43298">통합 가이드</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/43297">Demo 실행</a>
            </div>
        </div>
				<div class="card-container">
            <div class="card">
                            <img src="https://qcloudimg.tencent-cloud.cn/raw/e9d18b164152f08bc0694c01e966daea.png" data-nonescope="true">
                                <p class="titlename">uni-app SDK</p>
                <p style="color:#586376;">uni-app 플러그 인으로 캡슐화된 TRTC SDK를 사용하면 실시간 멀티미디어 서비스를 빠르고 쉽게 통합할 수 있습니다.</p>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_UniApp">GitHub</a>
								<a style="margin-left: 10px;" Demo 실행</a>
            </div>
        </div>
</div>



## 버전 비교
<table>
  <tr>
    <th width="100px" style="text-align:center">기능 모듈</th>
    <th width="100px" style="text-align:center">기능 세부 사항</th>
    <th width="100px" style="text-align:center">TRTC 라이트 버전</th>
    <th width="100px" style="text-align:center">다기능 버전</th>
  </tr>
    <tr>
    <td rowspan='2' style="text-align:center">영상 통화</td>
    <td style="text-align:center">2인 통화</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">그룹 회의</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">라이브 방송 마이크 연결</td>
    <td style="text-align:center">방 내 마이크 연결</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">방 간 마이크 연결</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2'  style="text-align:center">기본 뷰티 필터</td>
    <td style="text-align:center">피부 미백</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">컬러 필터</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
    <tr>
    <td rowspan='2' style="text-align:center">라이브 방송 푸시 스트림</td>
    <td style="text-align:center">카메라 푸시 스트림</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">녹화 푸시 스트림</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">라이브 방송 재생</td>
    <td style="text-align:center">RTMP 프로토콜</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HTTP - FLV</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">VOD 재생</td>
    <td style="text-align:center">MP4 포맷</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">DRM 암호화</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">쇼트 비디오</td>
    <td style="text-align:center">녹화 및 촬영</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">클리핑 및 스플라이싱</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">'TikTok' 특수 효과</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">비디오 업로드</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td rowspan='4' style="text-align:center">사이즈</td>
    <td style="text-align:center">Android</td>
    <td style="text-align:center">armv7: 3.97M<br>arm64: 4.33M</td>
    <td style="text-align:center">armv7: 9.15M<br>arm64: 10.4M</td>
  </tr>
    <tr>
    <td style="text-align:center">iOS</td>
    <td style="text-align:center">arm64: 3.15M</td>
    <td style="text-align:center">N/A</td>
  </tr>
</table>

>! Windows SDK 및 Mac OS SDK에는 TRTC, TXLivePusher, TXLivePlayer 및 TXVodPlayer 등 네 가지 기능이 포함되고, 쇼트 비디오 관련 기능은 당분간 지원하지 않으며, 라이트 버전과 다기능 버전의 구분은 없습니다.

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
