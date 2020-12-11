본 문서에서는 Tencent Cloud TRTC Web SDK를 귀하의 프로젝트에 빠르게 통합하는 방법을 소개합니다.

## 지원 플랫폼

Web에서 TRTC 통화를 구현하기 위해서는 브라우저에서 WebRTC 기능을 완벽하게 지원해야 합니다. 현재 WebRTC를 지원하는 브러우저는 다음과 같습니다.

|운영 체제 플랫폼 | 브라우저/webview | 버전 요구사항 | 비고                                                                                                                              |
| ------------ | -------------- | -------- | ------------------------------------ |
| iOS          | Safari         | 11.1.2   | 애플 Safari에서는 여전히 가끔 bug가 발생하므로 제품화 솔루션 전 먼저 해결하기를 권장합니다.<br > 따라서 iOS는 호환성이 더 좋은 미니프로그램 솔루션 사용을 권장합니다. |
| Android      | TBS            | 43600    | Wechat, 모바일 QQ에는 기본적으로 [TBS](http://x5.tencent.com/) 커널이 내장되어 있습니다.    |
| Android      | Chrome         | 60+      | H264 코딩/디코딩 지원 필요    |
| Mac          | Chrome         | 47+      | - |
| Mac          | Safari         | 11+      | - |
| Windows(PC)  | Chrome         | 52+      | - |
| Windows(PC)  | QQ 브라우저      | 10.2     | - |

>? TBS 커널 WebView 기반인 경우 버전이 ≥ 43600 이어야 합니다.
> 브라우저에서 [WebRTC 능력 테스트](https://www.qcloudtrtc.com/webrtc-samples/abilitytest/index.html) 페이지를 열어 WebRTC를 완벽하게 지원하는지 확인할 수 있습니다. 예시: 공식 계정 등의 브라우저 환경.
> 화웨이 시스템의 Chrome 브라우저와 Chrome WebView 커널의 브라우저는 H264 코딩을 지원하지 않습니다.


## 환경 요건
TRTC Web SDK는 다음 포트에 종속되어 데이터를 전송합니다. 다음 포트를 방화벽 화이트리스트에 추가하십시오.
- TCP 포트: 8687
- UDP 포트: 8000, 8800, 843, 443
- 도메인: qcloud.rtc.qq.com

## TRTC Web SDK 통합

### NPM 통합

프로젝트에서 npm을 사용하여 SDK 패키지를 설치합니다.

```
npm install trtc-js-sdk --save
```

프로젝트 스크립트에 모듈을 삽입합니다.

```javascript
import TRTC from 'trtc-js-sdk';
```

### Script 통합

귀하의 Web 페이지에 다음 코드만 추가하면 됩니다.

```html
<script src="trtc.js"></script>
```

## 관련 리소스

SDK 다운로드 주소: [다운로드](http://trtc-1252463788.cosgz.myqcloud.com/web/sdk/trtc.js) 클릭

더 자세한 초기화 절차 및 API 사용 소개는 다음 가이드를 참조하십시오.

| 기능                       | Sample Code 가이드                                                                                           |
| -------------------------- | --------------------------- |
| 기본 멀티미디어 통화  | [가이드 링크](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-01-basic-video-call.html)           |
| ILVB      | [가이드 링크](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-02-live-video.html)                 |
| 카메라, 마이크 전환   | [가이드 링크](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-03-advanced-switch-camera-mic.html) |
| 로컬 비디오 속성 설정  | [가이드 링크](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-04-advanced-set-video-profile.html) |
| 로컬 오디오 또는 비디오 동적 ON/OFF | [가이드 링크](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-05-advanced-dynamic-add-video.html) |
| 스크린 공유   | [가이드 링크](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-06-advanced-screencast.html)        |
| 음량 크기 점검  | [가이드 링크](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-07-advanced-detect-volume.html)     |


