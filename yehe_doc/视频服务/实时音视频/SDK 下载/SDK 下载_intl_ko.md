TRTC는 Tencent Cloud의 LiteAV 시리즈 제품입니다. LiteAV 시스템의 SDK는 모두 동일한 기본 모듈을 사용하기 때문에 프로젝트에 두 개 이상의 LiteAV 시스템 SDK를 동시에 통합하면 부호 충돌 문제(symbol duplicate)가 발생할 수 있습니다. 이에 따라 Tencent Cloud는 서로 다른 제품 기능을 통합한 **라이트 버전(TRTC)**, **프로 버전(Professional)**, **엔터프라이즈 버전(Enterprise)**을 제공하고 있으며, 실제 비즈니스 필요에 따라 각 버전을 선택할 수 있습니다.



<h2 id="TRTC">라이트 버전(TRTC)</h2>  
라이트 버전은 TRTC와 라이브 방송 재생(TXLivePlayer) 기능만 제공하며, App 설치 패키지 용량 증분이 가장 적어 TRTC 관련 기능만 사용하는 사용자에게 적합합니다.

<table>
   <tr>
      <th width="0px" style="text-align:center">소속 플랫폼</td>
      <th width="0px" style="text-align:center">ZIP 패키지</td>
      <th width="0px"  style="text-align:center">Github</td>
      <th width="0px" style="text-align:center">Gitee</td>
      <th width="0px" style="text-align:center">Demo 실행 설명</td>
      <th width="0px" style="text-align:center">SDK 통합 가이드</td>
      <th width="0px" style="text-align:center">설치 패키지 증분</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'zip'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center">3M（arm64）</td>
   </tr>
     <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'zip'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center">jar：546K<br> so（armeabi）：4.5M<br> so（armv7）：4.5M<br>so（arm64）：5.3M</td>
   </tr>
     <tr>
      <td style="text-align:center">Windows(C++)  </td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_cpp', ext1: 'zip'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_cpp', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_cpp', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_cpp', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35085">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_cpp', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35095">DOC</a></td>
      <td style="text-align:center">12.7M（C++ x86）<br>15.6M（C++ x64）</td>
   </tr>
     <tr>
      <td style="text-align:center">Windows(C#) </td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_csharp', ext1: 'zip'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_csharp', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_csharp', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_csharp', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35085">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_csharp', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35095">DOC</a></td>
      <td style="text-align:center">13.8M（C# x64）<br>13.3M（C# x86）</td>
   </tr>
     <tr>
      <td style="text-align:center">Mac</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_mac', ext1: 'zip'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_mac', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_mac', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_mac', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_mac', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35094">DOC</a></td>
      <td style="text-align:center">2.05M（arm64）</td>
   </tr>
     <tr>
      <td style="text-align:center">Web</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_web', ext1: 'zip'})" href="https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_web', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_web', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_web', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35607">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_web', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35096">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
   <tr>
      <td style="text-align:center">Electron  </td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_electron', ext1: 'zip'})" href="https://web.sdk.qcloud.com/trtc/electron/download/TXLiteAVSDK_TRTC_Electron_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_electron', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_electron', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_electron', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35089">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_electron', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35097">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
	    <tr>
      <td style="text-align:center">Flutter</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_flutter', ext1: 'zip'})" href="https://pub.dev/packages/tencent_trtc_cloud/versions">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_flutter', ext1: 'github'})" href="https://github.com/c1avie/trtc_demo">Github</a></td>
      <td style="text-align:center">N/A</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_flutter', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/39243">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_flutter', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35098">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
      <tr>
      <td style="text-align:center">React Native</td>
      <td style="text-align:center">N/A</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_rn', ext1: 'github'})" href="https://github.com/tencentyun/TRTCReactNative">Github</a></td>
      <td style="text-align:center">N/A</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_rn', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/43297">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_rn', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/43298">DOC</a></td>
      <td style="text-align:center">N/A</td>
</tr>
</table>

>? 
>- SDK로 인한 설치 패키지 용량 증분을 줄여야 할 경우, [설치 패키지 용량 축소 방법](https://intl.cloud.tencent.com/document/product/647/35165)을 참고하십시오.
>- QR 코드를 스캔해서 공식 계정을 팔로우하고 SDK의 버전 업데이트 및 최신 기술 동향을 알아보십시오.
> ![](https://main.qcloudimg.com/raw/d8a8c8c130ef7799feff6efbc0260ea2.jpg)


<h2 id="Professional">프로 버전(Professional)</h2>

프로 버전은 TRTC를 포함한 멀티미디어에 관한 핵심 기능이 집약되어 있으며, [Player+](https://intl.cloud.tencent.com/document/product/266/7836), [Mobile Live Video Broadcasting](https://intl.cloud.tencent.com/product/mlvb), [User Generated Short Video SDK](https://intl.cloud.tencent.com/product/ugsv) 등의 다양한 멀티미디어 관련 핵심 기능이 통합되어 있어, 하위 레이어 모듈을 효율적으로 재사용해 증분 용량이 독립적인 SDK 2개를 통합한 용량보다 작고, symbol duplicate 문제를 방지할 수 있습니다.

<table>
   <tr>
      <th width="0px" style="text-align:center">소속 플랫폼</td>
      <th width="0px" style="text-align:center">ZIP 패키지</td>
      <th width="0px"  style="text-align:center">Github</td>
      <th width="0px" style="text-align:center">64비트 지원</td>      
      <th width="0px" style="text-align:center">Demo 실행 설명</td>
      <th width="0px" style="text-align:center">SDK 통합 가이드</td>
      <th width="0px" style="text-align:center">설치 패키지 증분</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'zip', ext2:'professional'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'github', ext2:'professional'})" href="https://github.com/tencentyun/LiteAVProfessional_iOS">Github</a></td>
      <td style="text-align:center">지원</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_demo', ext2:'professional'})" href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_sdk', ext2:'professional'})" href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center">3.2M（arm64）</td>
   </tr>
   <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'zip', ext2:'professional'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'github', ext2:'professional'})" href="https://github.com/tencentyun/LiteAVProfessional_Android">Github</a></td>
      <td style="text-align:center">지원</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_demo', ext2:'professional'})" href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_sdk', ext2:'professional'})" href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center">jar：1M<br> so（armeabi）：5.7M<br> so（armv7）：5.7M<br>so（arm64）：6.8M</td>
   </tr>
</table>

>? 
>- Windows와 Mac 버전의 SDK는 현재 단일 버전만 제공되며, 라이트 버전, 프로 버전 및 엔터프라이즈 버전의 구분이 없습니다.
>- LiteAV 시스템의 SDK는 모두 동일한 기본 모듈을 사용하기 때문에 프로젝트에 두 개 이상의 LiteAV 시스템 SDK를 동시에 통합하면 부호 충돌 문제(symbol duplicate)가 발생할 수 있습니다. 이는 프로 버전의 LiteAVSDK를 통합하여 해결할 수 있습니다.
>- SDK로 인한 설치 패키지 용량 증분을 줄여야 할 경우, [설치 패키지 용량 축소 방법](https://intl.cloud.tencent.com/document/product/647/35165)을 참고하십시오.


<h2 id="Enterprise">엔터프라이즈 버전(Enterprise)</h2>

프로 버전의 모든 기능 외에도 엔터프라이즈 버전에는 눈 확대, 얼굴 슬리밍, 뷰티 필터 및 애니메이션 스티커와 같은 AI 뷰티 필터 특수 효과 컴포넌트가 포함되어 있습니다. 과금에 관한 내용은 [문의하기](https://intl.cloud.tencent.com/contact-us)를 참고하십시오. 엔터프라이즈 버전 다운로드 후 뷰티 필터 SDK의 압축 해제 비밀번호와 인증 License가 있어야 실행되므로, [문의하기](https://intl.cloud.tencent.com/contact-us)를 통해 암호 해제 비밀번호와 인증 License를 획득하십시오.

<table>
   <tr>
      <th width="0px" style="text-align:center">소속 플랫폼</td>
      <th width="0px" style="text-align:center">ZIP 패키지</td>
      <th width="0px" style="text-align:center">64비트 지원</td>
      <th width="0px" style="text-align:center">Demo 실행 설명</td>
      <th width="0px" style="text-align:center">SDK 통합 가이드</td>
      <th width="0px" style="text-align:center">설치 패키지 증분</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'zip', ext2:'enterprise'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Enterprise_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center">지원</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_demo', ext2:'enterprise'})" href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_sdk', ext2:'enterprise'})" href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center"> 5.5M（arm64）</td>
   </tr>
   <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'zip', ext2:'enterprise'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Enterprise_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center">지원</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_demo', ext2:'enterprise'})" href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_sdk', ext2:'enterprise'})" href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center"> jar：2.2M<br>so(armeabi)：9.3M</td>
   </tr>
</table>

>?
>- Windows와 Mac 버전의 SDK는 현재 AI 뷰티 필터 특수 효과 모듈을 지원하지 않으며, 라이트 버전, 프로 버전 및 엔터프라이즈 버전의 구분이 없습니다.
>- SDK가 가져오는 설치 패키지 용량 증분을 줄여야 할 경우, [설치 패키지 용량 축소 방법](https://intl.cloud.tencent.com/document/product/647/35165)을 참고하십시오.


## 각 버전 차이 대조표

![](https://main.qcloudimg.com/raw/d3c876e8d751709e1df52faf4c0bf012.jpg)

<table>
  <tr>
    <th width="100px" style="text-align:center">기능 모듈</th>
    <th width="100px" style="text-align:center">기능 항목</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/1071/38150">라이브 방송 기본 버전</a><br>LiteAV_Smart</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/1069/37914">UGSV 버전</a><br>LiteAV_UGC</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/34615">TRTC 버전</a><br>LiteAV_TRTC</th>
    <th width="100px" style="text-align:center">플레이어 버전<br>LiteAV_Player</th>
    <th width="100px" style="text-align:center"><a href="#Professional">프로 버전</a><br>Professional</th>
    <th width="100px" style="text-align:center"><a href="#Enterprise">엔터프라이즈 버전</a><br>Enterprise</th>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">라이브 방송 푸시 스트림</td>
    <td style="text-align:center">카메라 푸시 스트림</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">녹화 푸시 스트림</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">라이브 방송 재생</td>
    <td style="text-align:center">RTMP 프로토콜</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HTTP - FLV</td>
    <td style="text-align:center">&#10003;</td>
     <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">VOD 재생</td>
    <td style="text-align:center">MP4 포맷</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">DRM 암호화</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">뷰티 필터</td>
    <td style="text-align:center">기본 뷰티 필터</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">기본 필터</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">라이브 방송 마이크 연결</td>
    <td style="text-align:center">마이크 연결 인터랙션</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">크로스 룸 PK</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">영상 통화</td>
    <td style="text-align:center">2인 통화</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">화상 회의</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">UGSV</td>
    <td style="text-align:center">녹화 및 촬영</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">편집 및 스티칭</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">‘TikTok’ 특수 효과</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">비디오 업로드</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">AI 뷰티 필터 특수 효과</td>
    <td style="text-align:center">큰 눈과 갸름한 얼굴</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">V라인과 오똑한 코</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">애니메이션 스티커</td>
   <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">그린 스크린 크로마 키</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
</table>


