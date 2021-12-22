## 지원 플랫폼

WebRTC는 Google이 최초 출시한 기술입니다. 현재 Chrome 브라우저(데스크톱), Edge 브라우저(데스크톱), Firefox 브라우저(데스크톱), Safari 브라우저(데스크톱), Safari 브라우저(모바일)에서 비교적 완벽하게 지원되며, 기타 플랫폼(예: Android 브라우저)에 대한 지원은 완전하지 못할 수 있습니다.

교육 시나리오의 경우, 교사는 안정성이 더 높은 [Electron](https://intl.cloud.tencent.com/document/product/647/35097) 솔루션 사용을 권장합니다. 크고 작은 듀얼 채널 화면이 지원되어 더 효율적으로 화면을 공유할 수 있으며 네트워크 신호가 약한 경우 복구 능력이 더욱 뛰어납니다.

<table>
<tr>
<th>운영 체제</th>
<th>브라우저 유형</th>
<th>브라우저 최저<br> 버전 요구사항</th>
<th>SDK 버전 요구사항</th>
<th>수신(재생)</th>
<th>발송(마이크)</th>
<th>화면 공유</th>
</tr>
<tr>
<td rowspan="11">Windows</td>
<td>Chrome 브라우저(데스크톱)</td>
<td>56+</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>지원(Chrome72 이후 버전)</td>
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
<td>지원(Firefox66 이후 버전)</td>
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
<td>지원(Opera60 이후 버전)</td>
</tr>
<tr>
<td>360 Total Security 브라우저(데스크톱, 초고속 모드)</td>
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
<td>WeCom 내장 브라우저(데스크톱)</td>
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
<td>지원(Safari13 이후 버전)</td>
</tr>
<tr>
<td>Chrome 브라우저(데스크톱)</td>
<td>56+</td>
<td>-</td>
<td>지원</td>
<td>지원</td>
<td>지원(Chrome72 이후 버전)</td>
</tr>
<tr>
<td>Firefox 브라우저(데스크톱)</td>
<td>56+</td>
<td>v4.7.0+</td>
<td>지원</td>
<td>지원</td>
<td>지원(Firefox66 이후 버전)</td>
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
<td>지원(Opera60 이후 버전)</td>
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
<td>WeCom 내장 브라우저(데스크톱)</td>
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
<td>6.5+(WeChat 버전)</td>
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
<td>Safari 브라우저(모바일)</td>
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
>- 브라우저에서 [TRTC Web SDK 기능 테스트 페이지](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 열어 현재 브라우저에서 WebRTC의 모든 기능이 지원되는지 테스트할 수 있습니다(예: WebView 등 브라우저 환경).
>- H.264 버전 권한 제한으로 인해 Huawei 시스템의 Chrome 브라우저와 Chrome WebView 코어 브라우저에서는 TRTC Web SDK가 정상적으로 실행되지 않습니다.

## URL 도메인 프로토콜 제한
| 응용 시나리오     | 프로토콜             | 수신(재생) | 발송(마이크 켜짐) | 화면 공유 | 비고 |
| ------------ | :--------------- | :----------- | ------------ | -------- | ---- |
| 프로덕션 환경     | https 프로토콜        | 지원         | 지원         | 지원     | 권장 |
| 프로덕션 환경     | http 프로토콜         | 지원         | 미지원       | 미지원   |      |
| 로컬 개발 환경 | http://localhost | 지원         | 지원         | 지원     | 권장 |
| 로컬 개발 환경 | http://127.0.0.1 | 지원         | 지원         | 지원     |      |
| 로컬 개발 환경 | http://[로컬 컴퓨터 IP]  | 지원         | 미지원       | 미지원   |      |
| 로컬 개발 환경 | file:///         | 지원         | 지원         | 지원     |      |

## API 사용 튜토리얼
자세한 API 사용법은 다음 튜토리얼을 참고하십시오.

| 기능    | Sample Code 튜토리얼       |
| -------------------------- | ---------------------------------------------- |
| 기본 음성/영상 통화     | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-11-basic-video-call.html)           |
| 인터랙티브 라이브 스트리밍             | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-12-basic-live-video.html)    |
| 카메라/마이크 전환         | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-13-basic-switch-camera-mic.html)    |
| 로컬 비디오 속성 설정           | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-14-basic-set-video-profile.html)    |
| 로컬 오디오/비디오 동적 활성화/비활성화 | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-15-basic-dynamic-add-video.html)    |
| 화면 공유           | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html)           |
| 볼륨 감지       | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-17-basic-detect-volume.html)        |
| 사용자 정의 수집 및 사용자 정의 재생 렌더링 | [가이드 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-20-advanced-customized-capture-rendering.html) |
| 방의 업스트림 사용 인원 제한     | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-04-info-uplink-limits.html)        |
| 배경 음악/음향 효과 구현     | [튜토리얼 링크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-22-advanced-audio-mixer.html)          |


## TRTC

>!본문은 4.x.x 버전의 TRTC Web SDK에 적용됩니다.

TRTC는 [TRTC Web SDK](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/index.html)의 메인 엔트리입니다. TRTC 메소드를 통해 실시간 멀티미디어 통신을 위한 클라이언트 객체(Client) 및 로컬 오디오/비디오 스트림 객체(Stream)를 생성하고, 브라우저 호환성 및 화면 공유 지원 여부를 확인하고, 로그 레벨과 로그 업로드를 설정할 수 있습니다.

| API               | 설명               |
| ----------------------------------------- | ---------------------------------------- |
| [VERSION](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.VERSION)         | TRTC Web SDK 버전 번호.           |
| [checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.checkSystemRequirements) | 브라우저의 TRTC Web SDK 호환 여부 확인. 호환되지 않는 경우 사용자에게 최신 버전의 Chrome 브라우저 다운로드를 권고하시기 바랍니다.          |
| [isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.isScreenShareSupported)   | 브라우저의 화면 공유 지원 여부 확인. 화면 공유 스트림을 생성하기 전에 이 메소드를 호출해 현재 브라우저의 화면 공유 지원 여부를 확인하십시오.               |
| [getDevices](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getDevices)           | 미디어 입/출력 장치 목록 반환.             |
| [getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getCameras)           | 카메라 장치 목록 반환.          |
| [getMicrophones](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getMicrophones)           | 마이크 장치 목록 반환.          |
| [getSpeakers](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getSpeakers)         | 스피커 장치 목록 반환.          |
| [createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)    | 실시간 음성/영상 통화를 위한 클라이언트 객체 생성. 각 세션당 한 번만 호출합니다.          |
| [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)    | 로컬 스트림 Stream 객체 생성. 로컬 스트림 Stream 객체는 [publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish) 메소드를 사용하여 로컬 오디오/비디오 스트림을 게시합니다. |

## TRTC.Logger

[로그 출력 레벨](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.LogLevel), 로그 업로드 활성화/비활성화 등 로그 설정 메소드를 제공합니다.

| API        | 설명       |
| ---------------------------------- | ------------------ |
| [setLogLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.setLogLevel)           | 로그 출력 레벨 설정. |
| [enableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.enableUploadLog)   | 로그 업로드 활성화.     |
| [disableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.disableUploadLog) | 로그 업로드 비활성화.     |

## Client

음성/영상 통화 클라이언트 객체 Client는 [createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)를 통해 생성되며, 음성/영상 통화를 나타냅니다.

| API        | 설명         |
| ---------------------------------- | ---------------------------------------------------------- |
| [setProxyServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#setProxyServer)           | 프록시 서버 설정. 이 메소드는 기업이 nginx+coturn 같은 프록시 서버를 직접 배포하는 경우에 적합합니다.       |
| [setTurnServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#setTurnServer)     | TURN 서버 설정. 이 메소드는 [setProxyServer()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#setProxyServer)와 함께 사용되며, 기업이 프록시 및 TURN 서버를 직접 배포하는 경우에 적합합니다. |
| [join](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)       | 음성/영상 통화를 시작하는 방에 입장. 방이 없으면 시스템에서 방을 자동 생성합니다.            |
| [leave](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave)     | 음성/영상 통화 방 퇴장. 음성/영상 통화를 종료합니다.         |
| [publish](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish)         | 로컬 오디오/비디오 스트림 게시. 이 메소드는 [join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join) 메소드를 사용하여 방에 입장한 후에만 호출할 수 있으며, 하나의 음성/영상 통화는 하나의 로컬 스트림만 게시할 수 있습니다.           |
| [unpublish](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#unpublish)          | 로컬 스트림 게시 취소.     |
| [subscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe)          | 원격 스트림 구독.         |
| [unsubscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#unsubscribe)         | 원격 스트림 구독 취소.     |
| [switchRole](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole)           | 사용자 역할 전환. 이 메소드는 ‘live’ 인터랙티브 라이브 스트리밍 모드에서만 작동합니다.           |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#on)           | 클라이언트 객체 이벤트 수신.         |
| [getRemoteMutedState](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteMutedState) | 방에 있는 원격 사용자의 오디오/비디오 mute 상태 목록 가져오기.             |
| [getLocalAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getLocalAudioStats)   | 게시된 로컬 스트림의 오디오 통계 데이터 가져오기. 이 메소드는 [publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish) 호출 후에만 사용 가능합니다.           |
| [getLocalVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getLocalVideoStats)   | 게시된 로컬 스트림의 비디오 통계 데이터 가져오기. 이 메소드는 [publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish) 호출 후에만 사용 가능합니다.           |
| [getRemoteAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteAudioStats) | 모든 원격 스트림의 오디오 통계 데이터 가져오기.           |
| [Client.getRemoteVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteVideoStats) 모든 원격 스트림의 비디오 통계 데이터 가져오기.  |

## LocalStream

LocalStream 로컬 오디오/비디오 스트림은 [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)을 통해 생성되며, [Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html)의 하위 클래스입니다.

| API             | 설명               |
| --------------------------------------- | ------------------------------------------ |
| [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)           | 로컬 오디오/비디오 스트림 객체 초기화.      |
| [setAudioProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setAudioProfile)         | 오디오 Profile 설정. 이 메소드는 [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)가 호출되기 이전에만 사용할 수 있습니다.          |
| [setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setVideoProfile)         | 비디오 Profile 설정. 이 메소드는 [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)가 호출되기 이전에만 사용할 수 있습니다.          |
| [setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setScreenProfile)       | 화면 공유 Profile 설정. 이 메소드는 [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)가 호출되기 이전에만 사용할 수 있습니다.      |
| [setVideoContentHint](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setVideoContentHint) | 비디오 콘텐츠 힌트 설정. 주로 다양한 시나리오에서 비디오 인코딩 품질을 개선하기 위해 사용됩니다. 이 메소드는 [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)가 호출된 이후에만 사용할 수 있습니다. |
| [switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#switchDevice)       | 미디어 입력 장치 전환.            |
| [addTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#addTrack)    | 오디오/비디오 트랙 추가.          |
| [removeTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#removeTrack)         | 비디오 트랙 제거.        |
| [replaceTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#replaceTrack)       | 오디오/비디오 트랙 교체.          |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#play)       | 오디오/비디오 스트림 재생.              |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#stop)       | 오디오/비디오 스트림 재생 중지.            |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#resume)           | 오디오/비디오 재생 재개.              |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#close)     | 오디오/비디오 스트림 비활성화.        |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#muteAudio)          | 오디오 트랙 비활성화.        |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#muteVideo)          | 비디오 트랙 비활성화.        |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#unmuteAudio)         | 오디오 트랙 활성화.        |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#unmuteVideo)         | 비디오 트랙 활성화.        |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getId)     | Stream 의 고유 ID 가져오기.     |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getUserId)          | 스트림이 소속된 사용자 ID 가져오기.       |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setAudioOutput)           | 오디오 출력 장치 설정.            |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioLevel)     | 현재 볼륨 가져오기. 이 메소드는 로컬 스트림 또는 원격 스트림에 오디오 데이터가 있는 경우에만 작동합니다.        |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#hasAudio)    | 오디오 트랙 포함 여부.            |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#hasVideo)    | 비디오 트랙 포함 여부.            |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioTrack)     | 오디오 트랙 가져오기.        |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getVideoTrack)     | 비디오 트랙 가져오기.        |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getVideoFrame)     | 현재 비디오 프레임 가져오기.              |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#on)           |  Stream 이벤트 수신.            |



## RemoteStream

[Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED)수신을 통해 얻은 원격 오디오/비디오 스트림은 [Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html)의 하위 클래스입니다.

| API    | 설명           |
| ------------------------------ | --------------------------- |
| [getType](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getType)       | 원격 스트림 유형 가져오기. 주로 원격 스트림이 메인 오디오/비디오 스트림인지 또는 보조 비디오 스트림(일반적으로 화면 공유 스트림)인지 판단하는데 사용됩니다. |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#play)          | 오디오/비디오 스트림 재생.    |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#stop)          | 오디오/비디오 스트림 중지.          |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#resume)         | 오디오/비디오 스트림 재개.    |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#close)           | 오디오/비디오 스트림 비활성화.      |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#muteAudio)           | 오디오 트랙 비활성화.      |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#muteVideo)           | 비디오 트랙 비활성화.      |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#unmuteAudio)       | 오디오 트랙 활성화.      |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#unmuteVideo)       | 비디오 트랙 활성화.      |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getId)           | 스트림의 고유 ID 가져오기.      |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getUserId)           | 스트림이 소속된 사용자 ID 가져오기.        |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#setAudioOutput) | 오디오 출력 장치 설정.          |
| [setAudioVolume](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#setAudioVolume) | 재생 볼륨 설정.          |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getAudioLevel)   | 현재 볼륨 가져오기. 이 메소드는 로컬 스트림 또는 원격 스트림에 오디오 데이터가 있는 경우에만 작동합니다.        |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#hasAudio)     | 오디오 트랙 포함 여부.            |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#hasVideo)     | 비디오 트랙 포함 여부.            |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getAudioTrack)   | 오디오 트랙 가져오기.      |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getVideoTrack)   | 비디오 트랙 가져오기.      |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getVideoFrame)   | 현재 비디오 프레임 가져오기.    |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#on)         | Stream 이벤트 수신.          |


## RtcError

RtcError 객체.

| API          | 설명         |
| ------------------------------------- | ------------ |
| [getCode](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RtcError.html#getCode) | 오류 코드 가져오기. |



## 문의하기

문의사항은 colleenyu@tencent.com으로 이메일을 보내주십시오.
