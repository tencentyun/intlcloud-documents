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
TRTC는 Tencent Cloud 고객에게 안정적이고 신뢰도 높은 저비용 멀티미디어 전송 능력을 제공하기 위해 Tencent Cloud가 제공하는 저지연, 고품질 멀티미디어 통신 서비스 세트입니다. 이 서비스는 전 세계의 멀티미디어 전송 네트워크와 터미널 SDK 세트로 구성되어 있으며 이 페이지에서 현재 주요 클라이언트 플랫폼과 인기 있는 프레임워크를 포괄하는 터미널 SDK를 다운로드할 수 있습니다.

>? 현재 Github에 대한 네트워크 액세스 속도가 이상적이지 않은 경우 [여기를 클릭](https://gitee.com/cloudtencent/TRTCSDK)하여 Gitee의 이미지 레지스트리에 액세스할 수 있습니다.

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
                                <p class="titlename">미리보기 버전(TRTC)SDK</p>
                <p style="color:#586376;">새로운 아키텍처를 사용하여 기능이 안정적이고 용량은 더 작으며 성능이 더 좋습니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/preview/TXLiteAVSDK_TRTC_Android_preview.zip">ZIP 다운로드</a>
                                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36060">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35084">Demo 실행</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                            <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                                <p class="titlename">안정 버전(TRTC)SDK</p>
                <p style="color:#586376;">TRTC와 라이브 방송 재생(TXLivePlayer)의 두 가지 기능이 포함되어 있으며, 용량이 작고 기능이 안정적입니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/en/TXLiteAVSDK_TRTC_Android_en_latest.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Android">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35093">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35084">Demo 실행</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                                <p class="titlename">다기능 버전(Professional)SDK</p>
                <p style="color:#586376;">TRTC, 라이브 방송, 쇼트 비디오, VOD 등 다양하고 강력한 기능이 포함되어 있습니다!</p>
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
                                <p class="titlename">미리보기 버전(TRTC)SDK</p>
                <p style="color:#586376;">새로운 아키텍처를 사용하여 기능이 안정적이고 용량은 더 작으며 성능이 더 좋습니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/preview/TXLiteAVSDK_TRTC_iOS_preview.zip">ZIP 다운로드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35092">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35086">Demo 실행</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                                <p class="titlename">안정 버전(TRTC)SDK</p>
                <p style="color:#586376;">TRTC와 라이브 방송 재생(TXLivePlayer)의 두 가지 기능이 포함되어 있으며, 용량이 작고 기능이 안정적입니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/en/TXLiteAVSDK_TRTC_iOS_en_latest.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_iOS">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35092">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35086">Demo 실행</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                                <p class="titlename">다기능 버전(Professional)SDK</p>
                 <p style="color:#586376;">TRTC, 라이브 방송, 쇼트 비디오, VOD 등 다양하고 강력한 기능이 포함되어 있습니다!</p>
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
                                <p class="titlename">미리보기 버전(TRTC)SDK</p>
                <p style="color:#586376;">새로운 아키텍처를 사용하여 기능이 안정적이고 용량은 더 작으며 성능이 더 좋습니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/preview/TXLiteAVSDK_TRTC_Win_preview.zip">ZIP 다운로드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35095">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35085">Demo 실행</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/104e3aadbd4515f61c3f2f5378948cfb.svg" data-nonescope="true">
                                <p class="titlename">안정 버전(TRTC)SDK</p>
                <p style="color:#586376;">TRTC, 라이브 방송 재생(TXLivePlayer) 및 VOD 재생(TXVodPlayer)의 세 가지 기능이 포함되어 있습니다.</p>
                          <a href="https://liteav.sdk.qcloud.com/download/latest/en/TXLiteAVSDK_TRTC_Win_en_latest.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Windows">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35095">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35085">Demo 실행</a>
            </div>
        </div>
</div>

### Mac SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/98394fa5d669de7fb7a187565d138cdb.svg" data-nonescope="true">
                                <p class="titlename">미리보기 버전(TRTC)SDK</p>
                <p style="color:#586376;">새로운 아키텍처를 사용하여 기능이 안정적이고 용량은 더 작으며 성능이 더 좋습니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/preview/TXLiteAVSDK_TRTC_Mac_preview.zip">ZIP 다운로드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/36067">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/36067">Demo 실행</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/98394fa5d669de7fb7a187565d138cdb.svg" data-nonescope="true">
                                <p class="titlename">안정 버전(TRTC)SDK</p>
                <p style="color:#586376;">TRTC, 라이브 방송 재생(TXLivePlayer) 및 VOD 재생(TXVodPlayer)의 세 가지 기능이 포함되어 있습니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/en/TXLiteAVSDK_TRTC_Mac_en_latest.zip">ZIP 다운로드</a>
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
                                <a href="https://comm.qq.com/trtc/TRTC-Simple-Demo_en.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Flutter">GitHub</a>
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
</div>


## 버전 비교
<table>
  <tr>
    <th width="100px" style="text-align:center">기능 모듈</th>
    <th width="100px" style="text-align:center">기능 세부 사항</th>
    <th width="100px" style="text-align:center">미리보기 버전</th>
    <th width="100px" style="text-align:center">안정 버전</th>
    <th width="100px" style="text-align:center">다기능 버전</th>
  </tr>
    <tr>
    <td rowspan='2' style="text-align:center">영상 통화</td>
    <td style="text-align:center">2인 통화</td>
        <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">그룹 회의</td>
        <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">라이브 방송 마이크 연결</td>
    <td style="text-align:center">방 내 마이크 연결</td>
        <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">방 간 마이크 연결</td>
        <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2'  style="text-align:center">기본 뷰티 필터</td>
    <td style="text-align:center">피부 미백</td>
    <td style="text-align:center">&#10003;</td>
        <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">컬러 필터</td>
    <td style="text-align:center">&#10003;</td>
        <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
    <tr>
    <td rowspan='2' style="text-align:center">라이브 방송 푸시 스트림</td>
    <td style="text-align:center">카메라 푸시 스트림</td>
    <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">녹화 푸시 스트림</td>
        <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">라이브 방송 재생</td>
    <td style="text-align:center">RTMP 프로토콜</td>
    <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HTTP - FLV</td>
    <td style="text-align:center">&#10003;</td>
        <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">VOD 재생</td>
    <td style="text-align:center">MP4 포맷</td>
    <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">DRM 암호화</td>
    <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">쇼트 비디오</td>
    <td style="text-align:center">녹화 및 촬영</td>
    <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">클리핑 및 스플라이싱</td>
    <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">'TikTok' 특수 효과</td>
    <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">비디오 업로드</td>
    <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td rowspan='4' style="text-align:center">사이즈</td>
    <td style="text-align:center">Android</td>
    <td style="text-align:center">armv7: 3.97M<br>arm64: 4.33M</td>
    <td style="text-align:center">armv7: 6.95M<br>arm64: 7.94M</td>
    <td style="text-align:center">armv7: 9.15M<br>arm64: 10.4M</td>
  </tr>
    <tr>
    <td style="text-align:center">iOS</td>
    <td style="text-align:center">arm64: 3.15M</td>
    <td style="text-align:center">arm64: 3.23M</td>
    <td style="text-align:center">N/A</td>
  </tr>
    <tr>
    <td style="text-align:center">Windows</td>
        <td style="text-align:center">Win32: 13.0M <br>Win64: 15.4M</td>
    <td style="text-align:center">Win32: 21.3M <br>Win64: 26.9M</td>
    <td style="text-align:center">N/A</td>
  </tr>
    <tr>
    <td style="text-align:center">Mac</td>
        <td style="text-align:center"> x86_64：15.8M</td>
    <td style="text-align:center">x86_64：18.1M</td>
    <td style="text-align:center">N/A</td>
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