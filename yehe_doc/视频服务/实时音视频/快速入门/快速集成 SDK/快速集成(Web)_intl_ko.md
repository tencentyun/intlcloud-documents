본 문서에서는 Tencent Cloud TRTC Web SDK를 귀하의 프로젝트에 빠르게 통합하는 방법을 소개합니다.

## 지원 플랫폼

WebRTC 기술은 Google이 처음 고안한 기술로 Chrome, Edge, Firefox, Safari, Opera 브라우저 등에서 지원되고 있습니다. Tencent Cloud TRTC Web SDK는 WebRTC 패키지를 기반으로 하며 Tencent Cloud TRTC Web SDK에 대한 자세한 지원도는 플랫폼 지원을 참고하십시오.
- 교육 시나리오의 경우, 강의측에 안정성이 더 높은 [Electron](https://intl.cloud.tencent.com/document/product/647/35097) 솔루션 사용을 권장합니다. 크고 작은 듀얼 채널 화면을 지원하여 더 효율적으로 화면을 공유할 수 있으며 네트워크 신호가 약한 경우 복구 능력이 더욱 뛰어납니다.


Tencent Cloud TRTC Web SDK의 상세 지원 관련 내용은 [지원 플랫폼](https://intl.cloud.tencent.com/document/product/647/41664)을 참고하십시오.

> ! 
> - 브라우저에서 [TRTC Web SDK 기능 테스트 페이지](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 열어 WebRTC의 모든 기능이 지원되는지 테스트할 수 있습니다(예: WebView 등 브라우저 환경).
> - H.264 버전 권한 제한으로 인해, Huawei 디바이스 상의 Chrome 브라우저와 Chrome WebView 커널의 브라우저에서는 TRTC Web SDK가 정상적으로 실행되지 않습니다.

## URL 도메인 프로토콜 제한
| 응용 시나리오     | 프로토콜             | 수신(재생) | 발송(마이크 켜짐) | 화면 공유 | 비고 |
| ------------ | :--------------- | :----------- | ------------ | -------- | ---- |
| 프로덕션 환경     | HTTPS 프로토콜        | 지원         | 지원         | 지원     | 권장 |
| 프로덕션 환경     | HTTP 프로토콜         | 지원         | 미지원       | 미지원   |      |
| 로컬 개발 환경 | http://localhost | 지원         | 지원         | 지원     | 권장 |
| 로컬 개발 환경 | http://127.0.0.1 | 지원         | 지원         | 지원     |      |
| 로컬 개발 환경 | http://[로컬 IP]  | 지원         | 미지원       | 미지원   |      |
| 로컬 개발 환경 | file:///         | 지원         | 지원         | 지원     |      |

## 방화벽 제한
TRTC Web SDK는 다음 포트에 종속되어 데이터를 전송합니다. 다음 포트를 방화벽 얼로우리스트에 추가하십시오.
- TCP 포트: 8687
- UDP 포트: 8000, 8080, 8800, 843, 443, 16285
- 도메인: qcloud.rtc.qq.com

## TRTC Web SDK 통합

### NPM 통합

1. 프로젝트에서 npm을 사용하여 SDK 패키지를 설치해야 합니다.
```
npm install trtc-js-sdk --save
```
2. 프로젝트 스크립트에 모듈을 삽입합니다.
```javascript
import TRTC from 'trtc-js-sdk';
```

### Script 통합

귀하의 Web 페이지에 다음 코드만 추가하면 됩니다.

```html
<script src="trtc.js"></script>
```

## 관련 리소스

SDK 다운로드 주소: [클릭하여 다운로드](https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip) .

더 자세한 초기화 절차 및 API 사용 소개는 다음 가이드를 참고하십시오.

| 기능                       | Sample Code 가이드                                                                                                      |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 기본 음성/영상 통화 | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-11-basic-video-call.html) |
| 인터랙티브 라이브 스트리밍 | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-12-basic-live-video.html) |
| 카메라/마이크 전환 | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html) |
| 로컬 비디오 속성 설정 | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-14-basic-set-video-profile.html) |
| 로컬 오디오 또는 비디오 동적 ON/OFF | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-15-basic-dynamic-add-video.html) |
| 화면 공유 | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html) |
| 볼륨 감지 | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-17-basic-detect-volume.html) |
| 사용자 정의 수집 및 사용자 정의 재생 렌더링 | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-20-advanced-customized-capture-rendering.html) |
| 방의 업스트림 사용 인원 제한     | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-04-info-uplink-limits.html) |
| 배경 음악/음향 효과 구현     | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-22-advanced-audio-mixer.html) |
| 통화 전 환경 및 디바이스 점검| [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-23-advanced-support-detection.html) |
| 통화 전 네트워크 품질 점검| [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html) |
| 장치 연결/해제 동작 감지| [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-25-advanced-device-change.html)|
| CDN에 푸시 스트림 구현| [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-26-advanced-publish-cdn-stream.html) |
| 이중 스트림 활성화| [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-27-advanced-small-stream.html) |
| 뷰티 필터 활성화| [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-28-advanced-beauty.html) |
| 워터마크 활성화| [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-29-advance-water-mark.html) |
| 크로스 룸 연결 구현| [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-30-advanced-cross-room-link.html) |

>? [클릭](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-10-basic-get-started-with-demo.html)하여 더 많은 기능을 확인하십시오.
