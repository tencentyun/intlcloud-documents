UDP 전송 프로토콜을 기반으로 한 TRTC 서비스로, 프로토콜 전환을 통해 멀티미디어 스트림을 표준 라이브 방송 CDN 시스템으로 연결하며, 해당 프로세스를 “릴레이 푸시 스트림” 또는 "릴레이 라이브 방송"이라고 합니다.
TRTC 콘솔의 릴레이 라이브 방송 활성화 기능을 통해 기능을 활성화하면 자동으로 TRTC 방의 각 멀티미디어 스트림을 획득하게 됩니다. 또한 TRTCCloud에서 제공하는 **setMixTranscodingConfig** 인터페이스를 통해 클라우드의 혼합 스트림 트랜스 코딩을 활성화할 수도 있으며, 해당 기능을 통해 여러 화면을 하나의 라이브 방송 스트림으로 혼합할 수 있습니다.

본 문서에서는 Tencent Live Video Broadcasting(LVB) CDN 시스템에서 표준 **http + flv** 프로토콜을 통해 TRTC 방 안의 각 멀티미디어 스트림을 시청하는 방법에 대해 소개합니다.


## Demo
TRTC [Demo](https://intl.cloud.tencent.com/document/product/647/35076)에는 릴레이 라이브 방송 기능이 추가되어 있습니다. 영상 통화 중 [추가 기능]을 클릭하면 해당 기능을 체험해 볼 수 있는 방법(모바일 라이브 방송 페이지에서 플레이어 TXLivePlayer 다운로드 가능)이 마련되어 있습니다.

## 예시 코드

| 플랫폼 | CDN 시청 주소 계산 | 클라우드 혼합 스트림 매개변수 설정 |
|---------|---------|---------|
| iOS | 파일: [TRTCMoreViewController.m](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTCDemo/TRTC/TRTCMoreViewController.m) <br>함수: onBtnClick() | 파일: [TRTCMainViewController.m](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTCDemo/TRTC/TRTCMainViewController.m)<br>함수: updateCloudMixtureParams() |
| Android | 파일: [CdnPlayManager.java](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTCDemo/app/src/main/java/com/tencent/liteav/demo/trtc/sdkadapter/cdn/CdnPlayManager.java)<br>함수: initPlayUrl() | 파일: [TRTCRemoteUserManager.java](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTCDemo/app/src/main/java/com/tencent/liteav/demo/trtc/sdkadapter/remoteuser/TRTCRemoteUserManager.java)<br>함수: updateCloudMixtureParams() |
| Windows(C++) |  파일: [TRTCSettingViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCSettingViewController.cpp)<br>함수: NotifyOtherTab | 파일: [TRTCCloudCore.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/sdkinterface/TRTCCloudCore.cpp)<br>함수: updateMixTranCodeInfo() |
| Windows(C#) |  파일: [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs)<br>함수: OnShareUrlLabelClick| 파일: [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs)<br>함수: UpdateMixTranCodeInfo() |
| Mac |  현재 없음 | 파일: [TRTCMainWindowController.m](https://github.com/tencentyun/TRTCSDK/blob/master/Mac/TRTCDemo/TRTC/TRTCMainWindowController.m)<br>함수: updateCloudMixtureParams() |

## 응용 시나리오
릴레이 라이브 방송 특성을 기반으로 주요 라이브 방송 플랫폼에서 자주 볼 수 있는 호스트 마이크 연결 및 라이브 방송 PK 기능을 구현할 수 있습니다.

1. 호스트는 TRTCCloud의 `enterRoom()` 인터페이스를 통해 TRTC 방을 생성할 수 있으며, `connectOtherRoom()` 인터페이스를 통해 다른 방 호스트와 실시간 비디오 마이크 연결 PK를 진행할 수 있습니다. 현재 계정에서 "릴레이 라이브 방송" 기능을 활성화하면 해당 방의 라이브 방송 CDN 주소(http - flv 프로토콜 권장, 바로 재생 효과가 뛰어남)를 획득할 수 있습니다.
2. 시청자는 TXLivePlayer 플레이어로 해당 CDN 주소를 통해 시청할 수 있으며, TRTCCloud의 `enterRoom()` 인터페이스를 통해 호스트가 있는 현재 TRTC 방에 입장해 호스트와 실시간 비디오 마이크 연결을 통해 소통할 수 있습니다.
4. 호스트는 마이크 연결 또는 PK 상태가 된 후, TRTCCloud의 `setMixTranscodingConfig()` 인터페이스를 통해 클라우드에 비디오 혼합 스트림 작업(여러 화면을 하나로 혼합) 실행을 공지하여 기존 CDN 주소의 비디오 화면을 단일 사용자 화면에서 다중 사용자 혼합 화면으로 변경할 수 있습니다. 이 과정에서 계속해서 시청하고 있던 시청자는 라이브 방송 CDN 주소를 변경할 필요가 없습니다.
5. 마이크 연결 완료 후, 호스트는 다시 `setMixTranscodingConfig()` 인터페이스를 호출하여 혼합 스트림을 종료할 수 있으며, CDN 주소의 비디오 화면이 단일 사용자 화면으로 복구됩니다.

## 사용 방법

### 1단계: 서비스 활성화

[TRTC 콘솔](https://console.cloud.tencent.com/rav)에 로그인한 후, 대상 애플리케이션을 클릭하고 [기능 설정]을 선택해 "자동 릴레이 라이브 방송" 기능을 활성화할 수 있습니다. 해당 기능을 활성화하기 위해서는 먼저 Tencent Cloud [LVB](https://console.cloud.tencent.com/live) 서비스를 활성화해야 합니다.

### 2단계: 독립 화면

릴레이 라이브 방송 기능을 활성화하면 TRTC 방 안에 있는 모든 채널의 화면이 해당 재생 주소로 준비되며, 주소 포맷은 다음과 같습니다.
```
http://[bizid].liveplay.myqcloud.com/live/[streamid].flv
```

여기에서 `bizid`, `streamid`은 모두 필수 작성 항목이며, 자세한 작성 규칙은 다음과 같습니다.

- bizid: 라이브 방송 서비스와 관련된 숫자입니다. [TRTC 콘솔](https://console.cloud.tencent.com/rav)에서 생성한 애플리케이션을 선택하고 [계정 정보]를 클릭한 후, "라이브 방송 정보"에서 획득할 수 있습니다.

- 스트림 유형: 카메라 화면의 스트림 유형은 main이며, 화면 공유의 스트림 유형은 aux(예외 존재. WebRTC는 동시에 1개의 업스트림만 지원하므로 WebRTC에서의 화면 공유 스트림 유형 또한 main이 됨)입니다.
- `streamid = bizid_MD5(방 번호_userId_스트림 유형)`. 즉, `bizid`, `_`, `“방 번호_userId_스트림 유형”에 대한 MD5 계산 결과`를 조합하여 이루어 집니다.


자세한 계산 예시는 다음과 같습니다. 다음 예시를 참고하여 CDN 재생 주소를 계산할 수 있습니다.
```
예시: bizid = 8888, 릴레이 라이브 방송을 진행하는 방 번호 = 12345, userId = userA이고, 사용자가 현재 카메라를 사용하고 있는 경우.

1. MD5(12345_userA_main) 계산 = 8d0261436c375bb0dea901d86d7d70e8
2. 조합 후 userA의 Tencent Cloud CDN 시청 주소:
 flv 프로토콜: http://8888.liveplay.myqcloud.com/live/8888_8d0261436c375bb0dea901d86d7d70e8.flv
 hls 프로토콜: http://8888.liveplay.myqcloud.com/live/8888_8d0261436c375bb0dea901d86d7d70e8.m3u8
```

>! 위의 예시에서 `[bizid].liveplay.myqcloud.com` 부분을 재생 도메인이라고 합니다. 재생 도메인은 국가의 관련 부분 요구에 부합해야 하며, App을 앱 스토어에 배포할 경우 반드시 직접 신청한 재생 도메인을 사용해야 합니다. 설정 방법은 간단하며, "라이브 방송 콘솔>[도메인 관리](https://console.cloud.tencent.com/live/domainmanage)” 인터페이스에서 귀하의 재생 도메인을 추가하기만 하면 됩니다. `[bizid].liveplay.myqcloud.com` 도메인은 디버깅용으로만 사용할 수 있으며, Tencent Cloud에서 점차적으로 해당 도메인을 회수하고 있어 향후 사용 가능 여부를 보장할 수 없습니다.

### 3단계: 화면 혼합

혼합한 라이브 방송 화면을 획득하고 싶은 경우 TRTCCloud의 `setMixTranscodingConfig` 인터페이스를 호출하여 클라우드 혼합 스트림 트랜스 코딩을 실행해야 합니다. 해당 인터페이스의 매개변수 `TRTCTranscodingConfig`로 설정할 수 있습니다.
 - 각 서브 화면의 노출 위치 및 사이즈
 - 혼합 화면의 화질 및 인코딩 매개변수

자세한 설정 방법은 [클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618)을 참조하십시오.
>! `setMixTranscodingConfig`는 단말에서 스트림 혼합을 진행하는 것이 아니라 혼합 스트림 설정을 클라우드에 전송하고 클라우드 서버에서 스트림 혼합 및 트랜스 코딩을 진행하는 것입니다. 스트림 혼합 및 트랜스 코딩 시에는 기존의 멀티미디어 데이터를 디코딩 및 2차 인코딩이 필요해 처리 시간이 더 오래 걸립니다. 따라서 혼합 화면을 실제로 시청할 때의 딜레이 시간이 독립 화면 시간에 비해 1초~2초 더 길 수 있습니다.

### 4단계: 재생 연결

Tencent Cloud는 `http`를 접두사로 하고 `.flv`가 확장자인 **http - flv** 주소 사용을 권장합니다. 해당 주소에서의 재생은 딜레이 시간이 낮으며 바로 재생 효과가 뛰어나고 안정적이고 신뢰도가 높습니다. 플레이어는 TRTC SDK에 포함되어 있는 TXLivePlayer 사용을 권장하며, 해당 플레이어에 대한 내용은 다음 문서를 참조하십시오.
- TXLivePlayer(iOS)
- TXLivePlayer(Android)


### 5단계: 딜레이 최적화

릴레이 라이브 방송 활성화 후의 http - flv 주소는 라이브 방송 CDN의 배포를 거치므로 시청 시 딜레이가 직접 TRTC 라이브 룸에서의 통화 딜레이보다 더 깁니다. 자세한 딜레이 시간은 현재 Tencent Cloud의 라이브 방송 CDN 기술에 따라 TXLivePlayer를 함께 사용할 경우 다음 딜레이 표준과 같습니다.

| 릴레이 스트림 유형 | TXLivePlayer의 재생 모드 |  평균 딜레이 시간 |
|:-------:|:-------:|:--------:|
| 독립 화면 | 고속 모드(권장) | **2s - 3s** |
| 혼합 화면 | 고속 모드(권장) | **4s - 5s** |


실제 테스트 시 딜레이 시간이 위의 표보다 긴 경우, 다음 가이드에 따라 딜레이를 최적화하십시오.

- **TRTC SDK에 포함된TXLivePlayer 사용**
일반적인 ijkplayer 또는 ffmpeg를 사용하여 라이브 방송 스트림 주소를 재생할 경우 일반적으로 딜레이 시간을 제어할 수 없습니다. 해당 플레이어들은 ffmpeg 커널을 기반으로 패키징한 플레이어이기 때문에 딜레이를 제어할 수 있는 능력이 없기 때문입니다. TXLivePlayer는 Tencent Cloud가 자체개발한 재생 엔진으로, 딜레이 제어 기능을 갖추고 있습니다.

- **TXLivePlayer 재생 모드를 고속 모드로 설정**
TXLivePlayerConfig 매개변수 3개로 고속 모드를 구현할 수 있습니다. 예를 들어 iOS의 코드 설정은 다음과 같습니다.
    ```
    // TXLivePlayer의 재생 모드를 고속 모드로 설정
    TXLivePlayerConfig * config = [[TXLivePlayerConfig alloc] init];
    config.bAutoAdjustCacheTime = YES;
    config.minAutoAdjustCacheTime = 1; // 최소 버퍼 1초
    config.maxAutoAdjustCacheTime = 1; // 최대 버퍼 1초
    [player setConfig:config];
    // 라이브 방송 재생 실행
    ```

## FAQ
**방 입장 인원이 1명인데도 화면이 끊기고 흐릿한 이유는 무엇인가요?**
`enterRoom`의 TRTCAppScene 매개변수를 **TRTCAppSceneLIVE**로 지정하십시오. VideoCall 모드는 영상 통화에 최적화되어 있어 방에 1명의 사용자만 있을 경우 화면이 사용자의 네트워크 트래픽을 절약하기 위해 낮은 비트 레이트와 프레임 레이트를 유지하기 때문에 화면이 멈추고 흐릿한 것처럼 느껴질 수 있습니다.
