## 지원 플랫폼

TRTC Web SDK는 WebRTC를 기반으로 구현되었으며 현재 데스크톱 및 모바일에서 주요 브라우저를 지원합니다. 자세한 내용은 아래 테이블을 참고하십시오.
귀하의 시나리오가 지원되는 테이블에 없는 경우 [TRTC Web SDK 기능 테스트 페이지](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)에서 현재 환경이 WebView 환경 등 WebRTC의 모든 기능을 지원하는지 확인할 수 있습니다.

<table>
<thead>
<tr>
<th>운영 체제</th>
<th>브라우저 유형</th>
<th>브라우저 최저<br>버전 요구사항</th>
<th>SDK 버전 요구사항</th>
<th>수신(재생)</th>
<th>발송(마이크)</th>
<th width=19%>화면 공유</th>
</tr>
</thead>
<tr>
<td rowspan="11">Windows</td>
<td>Chrome 브라우저(데스크톱)</td>
<td>56+</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>Chrome72+ 버전 지원</td>
</tr>
<tr>
<td>QQ 브라우저(데스크톱, WebKit 코어)</td>
<td>10.4+</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
</tr>
<tr>
<td>Firefox 브라우저(데스크톱)</td>
<td>56+</td>
<td>v4.7.0+</td>
<td>지원</td>
<td>지원</td>
<td>Firefox66+ 버전 지원</td>
</tr>
<tr>
<td>Edge 브라우저(데스크톱)</td>
<td>80+</td>
<td>v4.7.0+</td>
<td>지원</td>
<td>지원</td>
<td>지원</td>
</tr>
<tr>
<td>Sogou 브라우저(데스크톱, 고속 모드)</td>
<td>11+</td>
<td>v4.7.0+</td>
<td>지원</td>
<td>지원</td>
<td>지원</td>
</tr>
<tr>
<td>Sogou 브라우저(데스크톱, 호환 모드)</td>
<td>-</td>
<td>-</td>
<td>미지원</td>
<td>미지원</td>
<td>미지원</td>
</tr>
<tr>
<td>Opera 브라우저(데스크톱)</td>
<td>46+</td>
<td>v4.7.0+</td>
<td>지원</td>
<td>지원</td>
<td>Opera60+ 버전 지원</td>
</tr>
<tr>
<td>360 Total Security 브라우저(데스크톱, 고속 모드)</td>
<td>13+</td>
<td>v4.7.0+</td>
<td>지원</td>
<td>지원</td>
<td>지원</td>
</tr>
<tr>
<td>360 Total Security 브라우저(호환 모드)</td>
<td>-</td>
<td>-</td>
<td>미지원</td>
<td>미지원</td>
<td>미지원</td>
</tr>
<tr>
<td>WeChat 내장 브라우저(데스크톱)</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>미지원</td>
<td>미지원</td>
</tr>
<tr>
<td>WeChat 내장 브라우저(데스크톱)</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>미지원</td>
<td>미지원</td>
</tr>
<tr>
<td rowspan="7">Mac OS</td>
<td>Safari 브라우저(데스크톱)</td>
<td>11+</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>Safari13+ 버전 지원</td>
</tr>
<tr>
<td>Chrome 브라우저(데스크톱)</td>
<td>56+</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>Chrome72+ 버전 지원</td>
</tr>
<tr>
<td>Firefox 브라우저(데스크톱)</td>
<td>56+</td>
<td>v4.7.0+</td>
<td>지원</td>
<td>지원</td>
<td>Firefox66+ 버전 지원<a href="#attention3">(주의[3])</a></td>
</tr>
<tr>
<td>Edge 브라우저(데스크톱)</td>
<td>80+</td>
<td>v4.7.0+</td>
<td>지원</td>
<td>지원</td>
<td>지원</td>
</tr>
<tr>
<td>Opera 브라우저(데스크톱)</td>
<td>46+</td>
<td>v4.7.0+</td>
<td>지원</td>
<td>지원</td>
<td>Opera60+ 버전 지원</td>
</tr>
<tr>
<td>WeChat 내장 브라우저(데스크톱)</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>미지원</td>
<td>미지원</td>
</tr>
<tr>
<td>WeChat 내장 브라우저(데스크톱)</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>미지원</td>
<td>미지원</td>
</tr>
<tr>
<td rowspan="6">Android</td>
<td>WeChat 내장 브라우저(TBS 코어)</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
</tr>
<tr>
<td>WeChat 내장 브라우저(XWEB 코어)</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
</tr>
<tr>
<td>WeCom 내장 브라우저</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
</tr>
<tr>
<td>Chrome 브라우저(모바일)</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
</tr>
<tr>
<td>QQ 브라우저(모바일)</td>
<td>-</td>
<td>-</td>
<td>미지원</td>
<td>미지원</td>
<td>미지원</td>
</tr>
<tr>
<td>UC 브라우저(모바일)</td>
<td>-</td>
<td>-</td>
<td>미지원</td>
<td>미지원</td>
<td>미지원</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>WeChat 내장 브라우저</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>미지원</td>
<td>미지원</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>WeChat 내장 브라우저</td>
<td>6.5+ (WeChat 버전)</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
</tr>
<tr>
<td>iOS</td>
<td>WeCom 내장 브라우저</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>미지원</td>
<td>미지원</td>
</tr>
<tr>
<td>iOS 11.1.2+</td>
<td>모바일 Safari 브라우저</td>
<td>11+</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>Chrome 브라우저(모바일)</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>미지원</td>
<td>미지원</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>Chrome 브라우저(모바일)</td>
<td>-</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>미지원</td>
</tr>
</table>

>!
>- H.264 버전 권한 제한으로 인해, Huawei Chrome 88 이하 버전은 H264 코덱을 사용할 수 없습니다(즉, 스트림 푸시 불가). Huawei 기기의 Chrome 브라우저에서 TRTC Web SDK를 사용하여 스트림을 푸시하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 VP8 코덱 활성화를 신청하십시오.
>- Mac OS에서 Firefox의 화면 공유 효과가 상대적으로 낮고 아직 해결책이 없는 상황이므로 Chrome 또는 Safari를 통한 화면 공유를 권장합니다.[](id:attention3)
>- Web 스트리밍 시 듀얼 사운드 채널 인코딩 지원을 원하시면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 WebRTC 듀얼 사운드 채널 인코딩을 신청하십시오.
>- 더 나은 제품 안정성과 온라인 지원을 위해 TRTC Web SDK를 최신 버전으로 업데이트할 것을 권장합니다. 버전 업데이트에 대한 주의 사항은 [업데이트 가이드](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html)를 참고하십시오.

## URL 도메인 프로토콜 제한
브라우저 보안 정책의 제한으로 인해 WebRTC 기능을 사용하려면 페이지의 액세스 프로토콜에 대한 엄격한 요구 사항이 있으므로 다음 테이블을 참고하여 애플리케이션을 개발하고 배포하십시오.

| 응용 시나리오     | 프로토콜             | 수신(재생) | 발송(마이크 켜짐) | 화면 공유 | 비고     |
|----------|:-----------------|:---------|----------|--------|----------|
| 프로덕션 환경     | HTTPS 프로토콜         | 지원      | 지원      | 지원               | **권장** |
| 프로덕션 환경     | HTTP 프로토콜         | 지원         | 미지원       | 미지원   |      |
| 로컬 개발 환경 | http://localhost | 지원         | 지원         | 지원     | **권장** |
| 로컬 개발 환경 | http://127.0.0.1 | 지원         | 지원         | 지원     |      |
| 로컬 개발 환경 | http://[로컬 IP]  | 지원         | 미지원       | 미지원   |      |
| 로컬 개발 환경 | file:///         | 지원         | 지원         | 지원     |      |

## API 사용 가이드
더 자세한 초기화 절차 및 API 사용 소개는 다음 튜토리얼을 참고하십시오.

| 기능    | Sample Code 튜토리얼       |
|--------------------------|----------------------|
| 기본 음성/영상 통화     | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-11-basic-video-call.html)           |
| 인터랙티브 라이브 스트리밍 마이크 연결 구현             | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-12-basic-live-video.html)    |
| 카메라/마이크 전환         | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html)    |
| 로컬 비디오 속성 설정           | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-14-basic-set-video-profile.html)    |
| 로컬 오디오/비디오 동적 활성화/비활성화 | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-15-basic-dynamic-add-video.html)    |
| 화면 공유           | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html)           |
| 볼륨 감지       | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-17-basic-detect-volume.html)        |
| 사용자 정의 수집 및 사용자 정의 재생 렌더링 | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-20-advanced-customized-capture-rendering.html) |
| 방의 업스트림 사용 인원 제한     | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-04-info-uplink-limits.html)        |
| 배경 음악/음향 효과 구현     | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-22-advanced-audio-mixer.html)          |
| 통화 전 환경 및 디바이스 점검| [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-23-advanced-support-detection.html) |
| 통화 전 네트워크 품질 점검| [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html) |
| 장치 연결/해제 동작 감지| [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-25-advanced-device-change.html)|
| CDN에 푸시 스트림 구현|- |
| 듀얼 스트림 활성화| [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-27-advanced-small-stream.html) |
| 뷰티 필터 활성화| [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-28-advanced-beauty.html) |
| 워터마크 활성화| [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-29-advance-water-mark.html) |
| 크로스 룸 연결 구현| [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-30-advanced-cross-room-link.html) |
| 클라우드 혼합 스트림 구현     | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-31-advanced-mix-transcode.html)  |
| 클라우드 녹화 구현     | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-32-advanced-cloud-record.html)   |

>? 
>- [클릭](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-10-basic-get-started-with-demo.html)하여 더 많은 기능을 확인하십시오.
>- FAQ는 [Web 관련](https://intl.cloud.tencent.com/document/product/647/37340)을 참고하십시오.

## API 소개
### TRTC

>!본문은 4.x.x 버전의 TRTC Web SDK에 적용됩니다.

TRTC는 [TRTC Web SDK](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/index.html)의 메인 엔트리입니다. TRTC 메소드를 통해 실시간 멀티미디어 통신을 위한 클라이언트 객체(Client) 및 로컬 오디오/비디오 스트림 객체(Stream)를 생성하고, 브라우저 호환성 및 화면 공유 지원 여부를 확인하고, 로그 레벨과 로그 업로드를 설정할 수 있습니다.

| API             | 설명     |
|----------------------------|-----------------------|
| [VERSION](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.VERSION)   | TRTC Web SDK 버전 넘버.       |
| [checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.checkSystemRequirements) | 브라우저의 TRTC Web SDK 호환 여부 확인. 호환되지 않는 경우 사용자에게 최신 버전의 Chrome 브라우저 다운로드를 권고하시기 바랍니다.          |
| [isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.isScreenShareSupported)   | 브라우저의 화면 공유 지원 여부 확인. 화면 공유 스트림을 생성하기 전에 이 메소드를 호출해 현재 브라우저의 화면 공유 지원 여부를 확인하십시오.    |
| [isSmallStreamSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#isSmallStreamSupported)    | 브라우저가 듀얼 스트림 모드 지원 여부 확인. 듀얼 스트림 모드를 활성화하기 전에 이 API를 호출하십시오.     |
| [getDevices](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getDevices)           | 미디어 입/출력 장치 목록 반환.             |
| [getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getCameras)           | 카메라 장치 목록 반환.          |
| [getMicrophones](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getMicrophones)           | 마이크 장치 목록 반환.          |
| [getSpeakers](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getSpeakers)         | 스피커 장치 목록 반환.          |
| [createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient)    | 실시간 음성/영상 통화를 위한 클라이언트 객체를 생성하여 방 출입, 오디오 및 비디오 스트림 배포 및 구독과 같은 기능 구현.          |
| [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createStream)    | 로컬 스트림 Stream 객체 생성. 로컬 스트림 Stream 객체는 [publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish) 메소드를 사용하여 로컬 오디오/비디오 스트림을 게시합니다. |

### TRTC.Logger

[로그 출력 레벨](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.LogLevel), 로그 업로드 활성화/비활성화 등 로그 설정 메소드를 제공합니다.

| API        | 설명       |
| ---------------------------------- | ------------------ |
| [setLogLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.setLogLevel)           | 로그 출력 레벨 설정. |
| [enableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.enableUploadLog)   | 로그 업로드 활성화.     |
| [disableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.disableUploadLog) | 로그 업로드 비활성화.     |

### Client

음성/영상 통화 클라이언트 객체 Client는 [createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient)를 통해 생성되며, 음성/영상 통화를 나타냅니다.

| API        | 설명   |
|----------------------------|---------------------|
| [setProxyServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setProxyServer)           | 프록시 서버 설정. 이 메소드는 기업이 nginx+coturn 같은 프록시 서버를 직접 배포하는 경우에 적합합니다.       |
| [setTurnServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setTurnServer)     | TURN 서버 설정. 이 메소드는 [setProxyServer()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setProxyServer)와 함께 사용되며, 기업이 프록시 및 TURN 서버를 직접 배포하는 경우에 적합합니다. |
| [join](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#join)       | 음성/영상 통화를 시작하는 방에 입장. 방이 없으면 시스템에서 방을 자동 생성합니다.  |
| [leave](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#leave)     | 음성/영상 통화 방 퇴장 및 음성/영상 통화 종료.         |
| [publish](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish)         | 로컬 오디오/비디오 스트림 게시. 이 메소드는 [join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#join) 메소드를 사용하여 방에 입장한 후에만 호출할 수 있으며, 하나의 음성/영상 통화는 하나의 로컬 스트림만 게시할 수 있습니다.           |
| [unpublish](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#unpublish)          | 로컬 스트림 게시 취소.     |
| [subscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#subscribe)          | 원격 스트림 구독.         |
| [unsubscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#unsubscribe)         | 원격 스트림 구독 취소.     |
| [switchRole](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#switchRole)           | 사용자 역할 전환. 이 메소드는 ‘live’ 인터랙티브 라이브 스트리밍 모드에서만 작동합니다.           |
| [sendSEIMessage](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#sendSEIMessage) |  SEI 메세지 발송. |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#on)           | 클라이언트 객체 이벤트 수신.         |
| [off](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#off)           | 클라이언트 객체 이벤트 수신 취소.         |
| [getRemoteMutedState](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteMutedState) | 방에 있는 원격 사용자의 오디오/비디오 mute 상태 목록 가져오기.             |
| [getTransportStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getTransportStats)       | 현재 네트워크 전송 상태 통계 데이터 테이블 가져오기.    |
| [getLocalAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getLocalAudioStats)   | 게시된 로컬 스트림의 오디오 통계 데이터 가져오기. 이 메소드는 [publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish) 호출 후에만 사용 가능합니다.           |
| [getLocalVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getLocalVideoStats)   | 게시된 로컬 스트림의 비디오 통계 데이터 가져오기. 이 메소드는 [publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish) 호출 후에만 사용 가능합니다.           |
| [getRemoteAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteAudioStats)   | 모든 원격 스트림의 오디오 통계 데이터 가져오기.  |
| [getRemoteVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteVideoStats)   | 모든 원격 스트림의 비디오 통계 데이터 가져오기.  |
| [startPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startPublishCDNStream)             | 현재 클라이언트의 오디오 및 비디오 스트림 CDN에 배포 시작.              |
| [stopPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopPublishCDNStream)               | 현재 클라이언트의 오디오 및 비디오 스트림 CDN에 배포 중지.  |
| [startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startMixTranscode)       | 믹스 트랜스코딩 시작. 방 입장 및 스트림 푸시 후 이 인터페이스를 호출하십시오.           |
| [stopMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopMixTranscode)         | 믹스 트랜스코딩 중지. 로컬 스트림을 성공적으로 게시(publish)하고 믹스 트랜스코딩 [startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startMixTranscode)를 시작한 후 이 인터페이스를 호출하십시오. |
| [enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableAudioVolumeEvaluation) | 볼륨 크기 콜백 ​​활성화 또는 비활성화.            |
| [enableSmallStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableSmallStream)       | 푸시 스트림측 듀얼 스트림 모드 활성화.              |
| [disableSmallStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#disableSmallStream)     | 푸시 스트림측 듀얼 스트림 모드 비활성화.              |
| [setSmallStreamProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setSmallStreamProfile)             | 작은 스트림 매개변수 설정.     |
| [setRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopPublishCDNStream)           | 시청측의 스트림 크기 속성 전환. 원격으로 작은 스트림을 활성화한 후에만 전환할 수 있습니다.            |

### LocalStream

LocalStream 로컬 오디오/비디오 스트림은 [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createStream)을 통해 생성되며, [Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html)의 하위 클래스입니다.

| API           | 설명          |
|--------------------------|--------------------------|
| [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)           | 로컬 오디오/비디오 스트림 객체 초기화.      |
| [setAudioProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioProfile)         | 오디오 Profile 설정. 이 메소드는 [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)가 호출되기 이전에만 사용할 수 있습니다.          |
| [setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setVideoProfile)         | 비디오 Profile 설정. 이 메소드는 [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)가 호출되기 이전에만 사용할 수 있습니다.          |
| [setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setScreenProfile)       | 화면 공유 Profile 설정. 이 메소드는 [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)가 호출되기 이전에만 사용할 수 있습니다.      |
| [setVideoContentHint](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setVideoContentHint) | 비디오 콘텐츠 힌트 설정. 주로 다양한 시나리오에서 비디오 인코딩 품질을 개선하기 위해 사용됩니다. 이 메소드는 [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)가 호출된 이후에만 사용할 수 있습니다. |
| [switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#switchDevice)       | 미디어 입력 장치 전환. |
| [addTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#addTrack)    | 오디오/비디오 트랙 추가. |
| [removeTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#removeTrack)         | 비디오 트랙 제거. |
| [replaceTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#replaceTrack)       | 오디오/비디오 트랙 교체. |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#play)                 | 오디오/비디오 스트림 재생. |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#stop)                 | 오디오/비디오 스트림 재생 중지. |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#resume)           | 오디오/비디오 재생 재개. |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#close)                | 오디오/비디오 스트림 비활성화. |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#muteAudio)          | 오디오 트랙 비활성화. |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#muteVideo)          | 비디오 트랙 비활성화. |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#unmuteAudio)         | 오디오 트랙 활성화. |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#unmuteVideo)         | 비디오 트랙 활성화. |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getId)                  | Stream 의 고유 ID 가져오기. |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getUserId)          | 스트림이 소속된 사용자 ID 가져오기. |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioOutput)           | 오디오 출력 장치 설정.            |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getAudioLevel)     | 현재 볼륨 가져오기. 이 메소드는 로컬 스트림 또는 원격 스트림에 오디오 데이터가 있는 경우에만 작동합니다.        |
| [setAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioCaptureVolume) | 마이크 수집 볼륨 설정. |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#hasAudio)           | 오디오 트랙 포함 여부. |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#hasVideo)          | 비디오 트랙 포함 여부. |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getAudioTrack)            | 오디오 트랙 가져오기. |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getVideoTrack)                | 비디오 트랙 가져오기. |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getVideoFrame)              | 현재 비디오 프레임 가져오기. |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#on)     |  Stream 이벤트 수신. |
| [off](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#off)           |  Stream 이벤트 수신 취소.            |



### RemoteStream

[Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_ADDED) 수신을 통해 얻은 원격 오디오/비디오 스트림은 [Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html)의 하위 클래스입니다.

| API  | 설명              |
|-----------------|-----------|
| [getType](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getType)       | 원격 스트림 유형 가져오기. 주로 원격 스트림이 메인 오디오/비디오 스트림인지 또는 보조 비디오 스트림(일반적으로 화면 공유 스트림)인지 판단하는데 사용됩니다. |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#play)       | 오디오/비디오 스트림 재생.              |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#stop)       | 오디오/비디오 스트림 재생 중지.            |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#resume)         | 오디오/비디오 스트림 재개.    |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#close)           | 오디오/비디오 스트림 비활성화.      |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#muteAudio)           | 오디오 트랙 비활성화.      |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#muteVideo)           | 비디오 트랙 비활성화.      |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#unmuteAudio)       | 오디오 트랙 활성화.      |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#unmuteVideo)       | 비디오 트랙 활성화.      |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getId)     | Stream 의 고유 ID 가져오기.     |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getUserId)           | 스트림이 소속된 사용자 ID 가져오기.        |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#setAudioOutput) | 오디오 출력 장치 설정.          |
| [setAudioVolume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#setAudioVolume) | 재생 볼륨 설정.          |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getAudioLevel)   | 현재 볼륨 가져오기. 이 메소드는 로컬 스트림 또는 원격 스트림에 오디오 데이터가 있는 경우에만 작동합니다.        |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#hasAudio)     | 오디오 트랙 포함 여부.            |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#hasVideo)     | 비디오 트랙 포함 여부.            |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getAudioTrack)   | 오디오 트랙 가져오기.      |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getVideoTrack)   | 비디오 트랙 가져오기.      |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getVideoFrame)   | 현재 비디오 프레임 가져오기.    |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#on)           |  Stream 이벤트 수신.            |
| [off](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#off)         | Stream 이벤트 수신 취소.          |


### RtcError

RtcError 객체.

| API    | 설명        |
|-----------------------|-----------|
| [getCode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RtcError.html#getCode) | 오류 코드 가져오기. |

### ClientEvent
Client에 의해 트리거될 이벤트 목록, 즉 'client.on('eventName')' 이벤트 수신의 이벤트 이름 'eventName'입니다.

| API   | 설명             |
| ---------- | ---------- |
| [stream-added](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_ADDED) | 원격 스트림 추가 이벤트는 원격 사용자가 스트림을 배포할 때 공지를 받습니다.             |
| [stream-removed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_REMOVED) | 원격 스트림 제거 이벤트. 원격 사용자가 스트림 게시를 취소하면 공지를 받습니다.         |
| [stream-updated](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_UPDATED) | 원격 스트림 업데이트 이벤트. 원격 사용자가 오디오 및 비디오 트랙을 추가, 제거 또는 교체할 때 공지를 받습니다. |
| [stream-subscribed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_SUBSCRIBED) | subscribe()가 성공적으로 호출될 때 트리거되는 원격 스트림 구독 성공 이벤트.    |
| [connection-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CONNECTION_STATE_CHANGED) | 로컬 client와 Tencent Cloud 간의 연결 상태 변경 이벤트.       |
| [peer-join](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.PEER_JOIN) | 원격 사용자 방 입장 이벤트.      |
| [peer-leave](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.PEER_LEAVE) | 원격 사용자 퇴장 이벤트 알림.      |
| [mute-audio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.MUTE_AUDIO) | 원격 스트림의 오디오 비활성화 이벤트. 원격 사용자가 오디오를 비활성화할 때 트리거됩니다.         |
| [mute-video](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.MUTE_VIDEO) | 원격 스트림의 비디오 비활성화 이벤트. 원격 사용자가 비디오를 비활성화할 때 트리거됩니다.         |
| [unmute-audio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.UNMUTE_AUDIO) | 원격 스트림의 오디오 활성화 이벤트. 원격 사용자가 오디오를 활성화할 때 트리거됩니다.         |
| [unmute-video](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.UNMUTE_VIDEO) | 원격 스트림의 비디오 활성화 이벤트. 원격 사용자가 비디오를 활성화할 때 트리거됩니다.         |
| [client-banned](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CLIENT_BANNED) | 사용자 강제 퇴장 이벤트. 강제 퇴장 이유: <ul style="margin:0"><li/>같은 이름의 사용자가 같은 방에 입장하는 경우. **참고**: 같은 이름의 사용자가 같은 방에 동시에 입장하는 것은 금지되며, 이는 두 사람 사이에 비정상적인 음성 및 영상 통화가 발생할 수 있으므로 서비스측에서 이러한 상황을 방지해야 합니다.<li/>서버 API를 사용하는 계정 관리자에 의해 퇴장 당하는 경우.</ul> |
| [network-quality](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.NETWORK_QUALITY) | 네트워크 품질 통계 데이터 이벤트. 방에 입장한 후 시작되며 업스트림 및 다운스트림 네트워크 품질 데이터를 포함하여 2초마다 트리거됩니다. |
| [audio-volume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.AUDIO_VOLUME) | 볼륨 크기 이벤트.<br>볼륨 크기 콜백을 ​​활성화하기 위해 [enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableAudioVolumeEvaluation) 인터페이스를 호출한 후 SDK는 주기적으로 이 이벤트를 발생시켜 각 userId의 볼륨 크기를 공지합니다. |
| [sei-message](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.SEI_MESSAGE) | sei 메세지 수신. |
| [error](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.ERROR) | 복구할 수 없는 오류가 발생할 때 발생되는 오류 이벤트. [오류 코드](https://intl.cloud.tencent.com/document/product/647/41665)를 참고하십시오. |

### StreamEvent
Stream에 의해 트리거된 이벤트 목록입니다.

| API     | 설명   |
| ------------- | ------------- |
| [player-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.PLAYER_STATE_CHANGED)         | Audio/Video Player 상태 변경 이벤트.              |
| [screen-sharing-stopped](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.SCREEN_SHARING_STOPPED)     | 로컬 화면 공유 중지 이벤트. 로컬 화면 공유 스트림에만 유효합니다.  |
| [connection-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.CONNECTION_STATE_CHANGED) | Stream 연결 상태 변경 이벤트. 'stream-added' 이벤트 콜백에서 이 이벤트를 수신하고, 'stream-removed' 이벤트 콜백에서 수신하는 이벤트를 취소합니다. |
| [error](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.ERROR)     | 복구할 수 없는 오류가 발생할 때 발생되는 오류 이벤트. [오류 코드](https://intl.cloud.tencent.com/document/product/647/41665)를 참고하십시오. |


## 문의하기

문의사항은 colleenyu@tencent.com으로 이메일을 보내주십시오.
