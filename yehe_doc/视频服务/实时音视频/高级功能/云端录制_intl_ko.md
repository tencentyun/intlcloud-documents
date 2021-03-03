비즈니스용 멀티미디어 솔루션은 증거 수집, 자격 증명, 심사, 저장 등을 위한 녹화 기능이 필요할 수 있습니다. TRTC 서비스는 [LVB](https://intl.cloud.tencent.com/document/product/267) 서비스의 기능을 사용해 전체적인 클라우드 녹화 기능을 제공하며, 녹화한 파일은 [VOD](https://intl.cloud.tencent.com/document/product/266) 플랫폼을 통해 획득할 수 있습니다.


>?
>- 처음에는 클라우드 녹화 기능이 비활성화 상태이므로 클라우드 녹화 기능을 사용하려면 먼저 [LVB](https://console.cloud.tencent.com/live)와 [VOD](https://console.cloud.tencent.com/vod) 서비스를 활성화해야 합니다.
>- 클라우드 녹화 기능을 사용하는 경우 LVB 서비스의 녹화 비용 및 VOD 서비스의 스토리지 비용이 발생합니다. 또한 녹화한 비디오 파일을 재생하거나 다운로드해야 할 경우 VOD 서비스로 인한 트래픽(비디오 가속) 비용이 발생할 수 있습니다. 과금 규정에 대한 자세한 사항은 [클라우드 녹화 관련 요금](https://intl.cloud.tencent.com/document/product/647/34614#.E4.BA.91.E7.AB.AF.E5.BD.95.E5.88.B6.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8) 문서를 참조하십시오. 

## 플랫폼 지원

|   iOS    | Android  |  Mac OS  | Windows  | WeChat 미니프로그램 | Chrome 브라우저 |
| :------: | :------: | :------: | :------: | :--------: | :----------: |
| &#10003; | &#10003; | &#10003; | &#10003; |  &#10003;  |   &#10003;   |

## 클라우드 녹화 활성화

1. [LVB](https://console.cloud.tencent.com/live)와 [VOD](https://console.cloud.tencent.com/vod) 서비스가 모두 활성화되어 있는지 확인합니다.
2. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인한 후, [애플리케이션 관리] 페이지로 이동하여 [릴레이 라이브 방송]이 "활성화" 상태인지 확인합니다. [릴레이 라이브 방송] 상태가 "비활성화" 상태인 경우 애플리케이션 리스트 오른쪽에 있는 [기능 설정]을 클릭한 후 설정 페이지에서 활성화할 수 있습니다.
3. [애플리케이션 관리] 페이지에서 [전체 클라우드 녹화 설정]을 클릭하여 [전체 클라우드 자동 녹화]를 활성화하고 녹화 파일 포맷을 설정합니다.

    전체 클라우드 자동 녹화를 활성화하면 현재 Tencent Cloud 계정의 모든 TRTC 애플리케이션에서 자동 녹화되는 비디오 포맷은 귀하가 설정한 저장 포맷으로 저장됩니다.

## 화면 혼합

TRTC의 멀티미디어 방은 기본적으로 혼합 스트림 기능이 활성화되어 있지 않으며, 클라우드 녹화 기능을 활성화하면 기본적으로 TRTC 방 안에 있는 모든 채널(메인 채널 및 보조 채널)의 업스트림 비디오가 개별 녹화됩니다. 혼합 후 화면을 녹화하고 싶은 경우 [클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618)을 사용해야 합니다. 즉, TRTCCloud의 `setMixTranscodingConfig` 인터페이스를 호출하여 혼합 화면 비디오를 하나의 독립된 파일로 저장합니다.

## 비디오 파일 획득


### 방법1: 콘솔에서 조회

VOD 콘솔의 [비디오 관리](https://console.cloud.tencent.com/vod/media) 인터페이스에서 녹화한 비디오 파일을 조회할 수 있습니다. Tencent Cloud 공식 홈페이지의 [Demo](https://intl.cloud.tencent.com/document/product/647/35076)를 기준으로 한 자세한 방법은 다음과 같습니다.

1. Tencent Cloud 공식 홈페이지의 Demo에 포함된 계정의 LVB bizid는 3891이며, [TRTC 콘솔](https://console.cloud.tencent.com/rav)>[애플리케이션 관리]>[애플리케이션 정보]>[릴레이 라이브 방송 정보]에서 해당 bizid를 확인할 수 있습니다.
2. Demo를 사용하여 라이브 룸을 생성하고, ID는 `12345`, 사용자 이름이 `userA`인 경우, 해당 방을 계산하는 해당 라이브 스트림 ID는 `MD5(12345_userA_main)`, 즉, `3891_8d0261436c375bb0dea901d86d7d70e8`이 됩니다. 자세한 계산 방법은 문서 [CDN 릴레이 라이브 방송](https://intl.cloud.tencent.com/document/product/647/34617) 중 라이브 방송 주소 설명 부분을 참조하십시오.
3. 라이브 룸 퇴장 후, VOD 콘솔의 [비디오 관리](https://console.cloud.tencent.com/vod/media) 인터페이스에서 직접 해당 파일을 직접 찾아보거나 라이브 방송 스트림 ID 접두사 검색으로 해당 파일을 찾을 수 있습니다.




### 방법2: REST API 조회

VOD 서비스에서 제공하는 REST API [SearchMedia 인터페이스](https://intl.cloud.tencent.com/document/product/266/34179)를 호출하고 해당 StreamId 매개변수를 지정하여 녹화 파일을 조회할 수 있습니다. StreamId(즉, 라이브 방송 스트림 ID) 획득 방법은 [CDN 릴레이 라이브 방송](https://intl.cloud.tencent.com/document/product/647/34617) 중 라이브 방송 주소 설명 부분을 참조하십시오.
