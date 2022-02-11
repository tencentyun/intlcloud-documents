본 문서는 Tencent Cloud TRTC 데스크톱 브라우저 SDK를 사용자의 프로젝트에 빠르게 통합하는 방법을 소개합니다.

## 지원 플랫폼

WebRTC는 Google이 최초 출시한 기술입니다. 현재 데스크톱 Chrome 브라우저, 데스크톱 Edge 브라우저, 데스크톱 Firefox 브라우저, 데스크톱 Safari 브라우저, 모바일 Safari 브라우저에서 비교적 완벽하게 지원되며, 기타 플랫폼(예: Android의 브라우저)에서의 지원은 완전하지 못할 수 있습니다.
- 응용 시나리오가 주로 교육 현장인 경우, 교사는 안정성이 더 높은 [Electron](https://intl.cloud.tencent.com/document/product/647/35097) 솔루션 사용을 권장합니다. 크고 작은 듀얼 채널 화면을 지원하여 더 효율적으로 화면을 공유할 수 있으며 네트워크 신호가 약한 경우 복구 능력이 더욱 뛰어납니다.


<table>
<tr>
<th>운영 체제</th>
<th width="22%">브라우저 유형</th><th>브라우저 최저<br>버전 요건</th><th width="16%">수신(재생)</th><th width="16%">발송(마이크 켜짐)</th><th>화면 공유</th><th>SDK 버전 요구사항</th>
</tr><tr>
<td rowspan="4">Mac OS</td>
<td>데스크톱 Safari 브라우저</td>
<td>11+</td>
<td>지원</td>
<td>지원</td>
<td>지원(Safari13 버전 이상 필요)</td>
<td>-</td>
</tr>
<tr>
<td>데스크톱 Chrome 브라우저</td>
<td>56+</td>
<td>지원</td>
<td>지원</td>
<td>지원(Chrome72 버전 이상 필요)</td>
<td>-</td>
</tr>
<tr>
<td>데스크톱 Firefox 브라우저</td>
<td>56+</td>
<td>지원</td>
<td>지원</td>
<td>지원(Firefox66 버전 이상 필요)</td>
<td>v4.7.0+</td>
</tr>
<tr>
<td>데스크톱 Edge 브라우저</td>
<td>80+</td>
<td>지원</td>
<td>지원</td>
<td>지원</td>
<td>v4.7.0+</td>
</tr>
<tr>
<td  rowspan="4">Windows</td>
<td>데스크톱 Chrome 브라우저</td>
<td>56+</td>
<td>지원</td>
<td>지원</td>
<td>지원(Chrome72 버전 이상 필요)</td>
<td>-</td>
</tr>
<tr>
<td>데스크톱 QQ 브라우저(고속 커널)</td>
<td>10.4+</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
<td>-</td>
</tr>
<tr>
<td>데스크톱 Firefox 브라우저</td>
<td>56+</td>
<td>지원</td>
<td>지원</td>
<td>지원(Firefox66 버전 이상 필요)</td>
<td>v4.7.0+</td>
</tr>
<tr>
<td>데스크톱 Edge 브라우저</td>
<td>80+</td>
<td>지원</td>
<td>지원</td>
<td>지원</td>
<td>v4.7.0+</td>
</tr>
<tr>
<td>iOS 11.1.2+</td>
<td>모바일 Safari 브라우저</td>
<td>11+</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
<td>-</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>WeChat 내부 웹 페이지</td>
<td>-</td>
<td>지원</td>
<td>미지원</td>
<td>미지원</td>
<td>-</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>WeChat 내부 웹 페이지</td>
<td>6.5+(WeChat 버전)</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
<td>-</td>
</tr>
<tr>
<td  rowspan="4">Android</td>
<td>모바일 QQ 브라우저</td>
<td>-</td>
<td>미지원</td>
<td>미지원</td>
<td>미지원</td>
<td>-</td>
</tr><tr>
<td>모바일 UC 브라우저</td>
<td>-</td>
<td>미지원</td>
<td>미지원</td>
<td>미지원</td>
<td>-</td>
</tr>
<tr>
<td>WeChat 내부 웹 페이지(TBS 커널)</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
<td>-</td>
</tr>
<tr>
<td>WeChat 내부 웹 페이지(XWEB 커널)</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
<td>-</td>
</tr>
</table>


> ! 
>- 브라우저에서 [WebRTC 기능 테스트](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) 페이지를 열어 WebRTC가 완벽하게 지원되는지 테스트할 수 있습니다(예: 공식 계정 등 브라우저 환경).
>- H.264 저작권 제한으로 인해 화웨이 시스템의 Chrome 브라우저 및 커널이 Chrome WebView인 브라우저에서는 TRTC 데스크톱 브라우저 SDK가 정상적으로 실행되지 않습니다.


## 방화벽 제한
TRTC 데스크톱 브라우저 SDK는 다음 포트에 종속되어 데이터를 전송합니다. 다음 포트를 방화벽 화이트리스트에 추가하십시오.
- TCP 포트: 8687
- UDP 포트: 8000, 8080, 8800, 843, 443, 16285
- 도메인: qcloud.rtc.qq.com

## TRTC 데스크톱 브라우저 SDK 통합

### NPM 통합

프로젝트에서 npm을 사용하여 SDK 패키지를 설치해야 합니다.

```
npm install trtc-js-sdk --save
```

프로젝트 스크립트에 모듈을 삽입합니다.

```javascript
import TRTC from 'trtc-js-sdk';
```

### Script 통합

Web 페이지에 다음 코드만 추가하면 됩니다.

```html
<script src="trtc.js"></script>
```

## 관련 리소스

SDK 다운로드 주소: [다운로드](https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip) 클릭

더 자세한 초기화 절차 및 API 사용 소개는 다음 가이드를 참조하십시오.

| 기능                       | Sample Code 가이드                                                                                                      |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 기본 멀티미디어 통화             | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-11-basic-video-call.html)                      |
| ILVB                   | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-12-basic-live-video.html)                            |
| 카메라, 마이크 전환         | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html)            |
| 로컬 비디오 속성 설정           | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-14-basic-set-video-profile.html)            |
| 로컬 오디오 또는 비디오 동적 ON/OFF | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-15-basic-dynamic-add-video.html)            |
| 화면 공유                   | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html)                   |
| 음량 크기 검증               | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-17-basic-detect-volume.html)                |
| 사용자 정의 수집 및 사용자 정의 재생 렌더링 | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-20-advanced-customized-capture-rendering.html) |
| 방에서 업스트림 사용자 수 제한     | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-04-info-uplink-limits.html)                |
| 배경 음악 및 음향 효과 구현 솔루션     | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-22-advanced-audio-mixer.html)                  |

