[](id:que1)
###  모바일(Andriod/iOS)에서는 몇 가지 시스템 음량 모드를 지원하나요?
통화 음량과 미디어 음량의 2가지 시스템 음량 유형을 지원합니다.
- 통화 음량의 경우, 통화 시나리오를 위해 설계된 음량 유형으로 휴대폰에 내장된 음향 반향 제거 기능을 사용하여 음질이 미디어 음량에 비해 떨어지며 음량 버튼으로 음량을 0까지 조절할 수는 없지만, 블루투스 이어폰의 마이크를 지원합니다.
- 미디어 음량의 경우, 음악 시나리오를 위해 설계된 음량 유형으로 음질이 통화 음량보다 뛰어나며 음량 버튼으로 음량을 0까지 조절할 수 있습니다. 미디어 음량 사용 시 반향 제거(AEC) 기능을 켜면 SDK에 내장된 음향 처리 알고리즘이 활성화되며 음성에 대한 2차 처리를 진행합니다. 미디어 음량 모드에서는 블루투스 이어폰의 자체 마이크로 음성을 수집할 수 없으며 휴대폰의 마이크로만 음성을 수집할 수 있습니다.

[](id:que2)
###  모바일 SDK 푸시 스트림에서 1080p 해상도를 어떻게 설정하나요?
1080P는 TX_Enum_Type_VideoResolution에서 114로 정의되어 있어, 직접 해상도 열거 값을 설정하면 됩니다.

[](id:que3)
### 미니프로그램에서 방을 만들 경우 모바일에서도 입장이 가능합니까?
가능합니다. TRTC는 모든 플랫폼의 통신을 지원합니다.

[](id:que4)
###  TRTC 모바일에서 어떻게 녹화(화면 공유)를 하나요?	
- **Android**: Version 7.2 이상에서 모바일 녹화를 지원하며, 자세한 방법은 [실시간 화면 공유(Android)](https://intl.cloud.tencent.com/document/product/647/37337)를 참조하십시오.
- **iOS**: Version 7.2 이상에서는 App 내 녹화를 지원하며, Version 7.6 이상에서는 모바일 녹화 및 App 내 녹화를 지원합니다. 자세한 방법은 [실시간 화면 공유(iOS)](https://intl.cloud.tencent.com/document/product/647/37338)를 참조하십시오.



[](id:que5)
###  TRTC Android에서 64비트 arm64-v8a 아키텍처를 지원하나요?
TRTC 6.3 버전부터 arm64-v8a 아키텍처를 제공하여 ABI를 지원하고 있습니다.




[](id:que7)
###  iOS에서 Swift 통합을 지원하나요?
지원합니다. 3rd party 라이브러리 통합을 지원하는 프로세스에 따라 SDK를 통합하면 됩니다. [Demo 실행(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086)을 참조하십시오.




[](id:que9)
###  TRTC SDK에서 iOS 백그라운드 실행을 지원하나요?
지원합니다. 현재 프로젝트를 선택한 후 **Capabilities**에서 **Background Modes**를 **ON**으로 설정하고, **Audio, AirPlay and Picture in Picture**를 선택하기만 하면 백그라운드에서 실행할 수 있습니다. 자세한 내용은 다음 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

[](id:que10)
### iOS에서 리스너를 원격으로 퇴장시킬 수 있나요?
[onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28)을 사용하여 리스너를 원격으로 퇴장시킬 수 있습니다. 또한 해당 인터페이스는 VideoCall의 모든 사용자 및 LIVE 모드의 호스트가 퇴장했을 때만 콜백이 트리거되며 시청자가 퇴장했을 때에는 콜백이 없습니다. 

[](id:que11)
### 휴대폰 잠금 화면 상태에서는 비디오를 어떻게 연결하나요?
오프라인 수신 등의 기능이 있습니다. 자세한 내용은 [오프라인 수신](https://intl.cloud.tencent.com/document/product/647/36068)을 참조하십시오.

[](id:que12)
### Android와 웹 간 통신을 지원하나요?
지원합니다. 동일한 [SDKAppID](https://console.cloud.tencent.com/trtc/app)를 사용하여 같은 방에 들어가면 통화할 수 있습니다. 자세한 내용은 다음 문서에 링크된 Demo 설정을 참조하십시오.
- [Demo 실행(Android)](https://intl.cloud.tencent.com/document/product/647/35084)
- [Demo 실행(데스크톱 브라우저)](https://intl.cloud.tencent.com/document/product/647/35607)

[](id:que13)
### 라이브 방송 시 호스트와 관객 모두 마이크를 연결할 수 있나요?
양쪽 모두 가능하며, 관객과 호스트는 시작 로직이 일치합니다. 자세한 내용은 [라이브 방송 모드 실행(Android)](https://intl.cloud.tencent.com/document/product/647/35108)을 참조하십시오.

[](id:que14)
### 다중 사용자 화상 회의 시, 모바일과 웹에서 같은 방에 입장할 수 있나요?
가능합니다. [SDKAppID](https://console.cloud.tencent.com/trtc/app)와 방 번호가 일치하고 사용자 ID가 다르면 됩니다.

[](id:que15)
### 동일한 페이지에서 N개의 TRTC 객체를 생성한 후 N개의 UserID를 사용하여 각각 N개의 방에 로그인할 수 있나요?
가능합니다. [Version 7.6 버전](https://intl.cloud.tencent.com/document/product/647/34615)부터 한 명의 사용자가 여러 개의 방에 입장할 수 있습니다.


[](id:que16)
### SDK 최신 버전 넘버는 어떻게 조회하나요?
- 자동 로딩 방식을 사용하는 경우, `latest.release`가 최신 버전과 매칭되어 자동 로딩되므로 버전 넘버를 수정하지 않아도 됩니다. 자세한 방법은 [1분 내에 SDK 통합하기](https://intl.cloud.tencent.com/document/product/647/35092)를 참조하십시오.
- 현재 SDK 최신 버전 넘버는 로그 배포를 통해 조회 가능하며, 자세한 내용은 다음을 참조하십시오.
  - iOS & Android는 [로그 배포(App)](https://intl.cloud.tencent.com/document/product/647/39426)를 참조하십시오.
  -  Web[로그 배포(Web)](https://intl.cloud.tencent.com/document/product/647/39779)를 참조하십시오.
  - Electron은 [로그 배포(Electron)](https://intl.cloud.tencent.com/document/product/647/38702)를 참조하십시오.






