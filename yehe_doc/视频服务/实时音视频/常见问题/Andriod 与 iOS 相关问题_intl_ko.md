[](id:que1)
###  모바일(Andriod/iOS)에서는 몇 가지 시스템 음량 모드를 지원합니까?
시스템에서 통화 음량과 미디어 음량 등 2가지 음량 유형을 지원합니다.
- 통화 음량의 경우, 통화를 위해 설계된 음량 유형으로 휴대폰 자체 반향 제거 기능을 사용합니다. 음질이 미디어 음량에 비해 떨어지며 음량 버튼으로 음량을 0까지 조절할 수는 없지만 블루투스 이어폰의 마이크를 지원합니다.
- 미디어 음량의 경우, 음악을 위해 설계된 음량 유형으로 음질이 통화 음량보다 뛰어나며 음량 버튼으로 음량을 0까지 조절할 수 있습니다. 미디어 음량 사용 시 반향 제거(AEC) 기능을 켜면 SDK에 내장된 음향 처리 알고리즘이 활성화되며 음성에 대한 2차 처리를 진행합니다. 미디어 음량 모드에서는 블루투스 이어폰의 자체 마이크로 음성을 캡처할 수 없으며 휴대폰의 마이크로만 음성을 캡처할 수 있습니다.

[](id:que2)
###  모바일 SDK 푸시 스트리밍에서 1080p 해상도를 어떻게 설정합니까?
1080P는 TX_Enum_Type_VideoResolution에서 114로 정의되어 있어, 직접 해상도 열거 값을 설정하면 됩니다.

[](id:que4)
###  TRTC 모바일에서 어떻게 녹화(화면 공유)를 합니까?	
- **Android**: Version 7.2 이상에서 모바일 녹화를 지원하며, 자세한 방법은 [실시간 화면 공유(Android)](https://intl.cloud.tencent.com/document/product/647/37337)를 참조하십시오.
- **iOS**: Version 7.2 이상에서는 App 내 녹화를 지원하며, Version 7.6 이상에서는 모바일 녹화 및 App 내 녹화를 지원합니다. 자세한 방법은 [실시간 화면 공유(iOS)](https://intl.cloud.tencent.com/document/product/647/37338)를 참조하십시오.



[](id:que5)
###  TRTC Android에서 64비트 arm64-v8a 구성을 지원합니까?
TRTC 6.3 버전부터 arm64-v8a 구성을 제공하여 ABI를 지원하고 있습니다.


[](id:que7)
###  iOS에서 Swift 통합을 지원합니까?
지원합니다. Third Party 라이브러리 통합을 지원하는 프로세스에 따라 SDK를 통합하면 됩니다. [Demo 실행(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086)을 참조하십시오.


[](id:que9)
###  TRTC SDK에서 iOS 백그라운드 실행을 지원합니까?
지원합니다. 현재 프로젝트를 선택한 후 **Capabilities**에서 **Background Modes**를 **ON**으로 설정하고, **Audio，AirPlay and Picture in Picture**를 선택하면 백그라운드에서 실행할 수 있습니다. 자세한 내용은 다음 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

[](id:que10)
### iOS에서 리스너를 원격으로 퇴장시킬 수 있습니까?
[onRemoteUserLeaveRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28)을 사용하여 리스너를 원격으로 퇴장시킬 수 있습니다. 또한 해당 인터페이스는 VideoCall의 모든 사용자 및 LIVE 모드의 호스트가 나갈 때만 콜백이 트리거되며 관객이 나갈 때는 콜백이 없습니다. 

[](id:que11)
### 휴대폰 잠금 화면 상태에서는 비디오를 어떻게 연결합니까?
오프라인 수신 등의 기능이 있습니다. 자세한 내용은 [오프라인 수신](https://intl.cloud.tencent.com/document/product/647/36068)을 참조하십시오.

[](id:que12)
### Android와 웹 간 통신을 지원합니까?
지원합니다. 동일한 [SDKAppID](https://console.cloud.tencent.com/trtc/app)를 사용하여 같은 방에 들어가면 통화할 수 있습니다. 자세한 내용은 다음 문서에 링크된 Demo 설정을 참조하십시오.
- [Demo 제작(Android)](https://intl.cloud.tencent.com/document/product/647/35084)
- [Demo 제작(데스크톱 브라우저)](https://intl.cloud.tencent.com/document/product/647/35607)

[](id:que13)
### 라이브 방송 시 호스트와 관객 모두 마이크를 연결할 수 있습니까?
양쪽 모두 가능하며, 관객과 호스트는 시작 로직이 일치합니다. 자세한 내용은 [라이브 방송 모드 제작(Android)](https://intl.cloud.tencent.com/document/product/647/35108)을 참조하십시오.

[](id:que14)
### 다중 사용자 화상 회의 시 모바일과 웹에서 같은 방에 입장할 수 있습니까?
가능합니다. [SDKAppID](https://console.cloud.tencent.com/trtc/app)와 방 번호가 일치하고 사용자 ID가 다르면 됩니다.

[](id:que15)
### 동일한 페이지에서 N개의 TRTC 객체를 생성한 후 N개의 UserID를 사용하여 각각 N개의 방에 로그인할 수 있습니까?
가능합니다. [Version 7.6 버전](https://intl.cloud.tencent.com/document/product/647/34615)부터 한 명의 사용자가 여러 개의 방에 입장할 수 있습니다.

[](id:que16_flutter)
###  2대의 휴대폰에서 동시에 Demo를 실행했을 때, 서로의 화면이 보이지 않는 이유는 무엇입니까?
2대의 모바일에서 Demo를 실행할 경우 각자 다른 UserID를 사용해야 합니다. TRTC에서는 동일 UserID(SDKAppID가 다를 경우 제외)를 2개의 터미널에서 동시에 사용할 수 없습니다.

[](id:que17_flutter)
### 방화벽에는 어떤 제한이 있습니까?
SDK는 UDP 프로토콜을 통해 멀티미디어를 전송하므로, UDP를 차단하는 기업용 네트워크에서는 사용할 수 없습니다. 이와 유사한 문제가 발생하는 경우 [기업용 방화벽 제한 대응](https://intl.cloud.tencent.com/document/product/647/35164)을 참조하여 해결하십시오.

[](id:que18_flutter)
### iOS 패키징에 Crash가 실행됩니다.
iOS14 이상의 debug 모드 문제인지 확인하십시오. 자세한 내용은 [공식 홈페이지 설명](https://flutter.cn/docs/development/ios-14#launching-debug-flutter-without-a-host-computer)을 참조하십시오.

[](id:que19_flutter)
### iOS에서 비디오가 표시되지 않습니다. (Android는 정상)
프로젝트 `info.plist`에 `io.flutter.embedded_views_preview` 값이 YES인지 확인하십시오.

[](id:que20_flutter)
### SDK 버전 업데이트 후 iOS CocoaPods 실행 시 오류가 발생합니다.
1. iOS 디렉터리에서 `Podfile.lock` 파일을 삭제합니다.
2. `pod repo update`를 진행합니다.
3. `pod install`을 진행합니다.
4. 재실행합니다.

[](id:que21_flutter)
### Android Manifest merge failed 컴파일에 실패합니다.
1. `/example/android/app/src/main/AndroidManifest.xml` 파일을 엽니다.
2. `xmlns:tools="http://schemas.android.com/tools"`를 manifest에 추가합니다.
3. `tools:replace="android:label"`을 application에 추가합니다.

![img](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

[](id:que22_flutter)
### 서명이 없어 실제 기기에서 디버깅 오류가 발생합니다.
오류 정보가 다음과 같은 경우,
![](https://main.qcloudimg.com/raw/809ae94061575b4e670f3a80ac9f3781.png)
1. Apple 인증서를 구매하여 설정, 서명 작업을 완료한 후 실제 기기 상에서 디버깅할 수 있습니다.
2. 인증서 구매 후, `target > signing & capabilities`에서 설정을 진행합니다.

[](id:que23_flutter)
### 플러그 인 내에 swift 파일에 추가/삭제 후, build 시 상응하는 파일을 찾을 수 없습니다.
메인 프로그램 디렉터리의 `/ios` 파일 경로에서 `pod install`을 진행하면 됩니다.

[](id:que24_flutter)
### Run 오류 “Info.plit, error: No value at that key path or invalid key path: NSBonjourServices”가 발생합니다.
`flutter clean` 진행 후, 재실행하면 됩니다.

[](id:que25_flutter)
### Pod install 오류가 발생합니다.
오류 정보가 다음과 같은 경우,
![](https://main.qcloudimg.com/raw/73db67cfc9e6b934fed947b63c6d2120.png)
오류 정보에 pod install이 표시되는 경우 `generated.xconfig` 파일이 존재하지 않아 실행 오류가 발생하는 것입니다. **flutter pub get 진행** 안내에 따라 해결하십시오.
>? 해당 문제는 flutter 컴파일 이후의 문제로, 신규 프로젝트 또는 `flutter clean`을 진행한 경우 해당 문제가 발생하지 않습니다.

[](id:que26_flutter)
### Run 시 iOS 버전에 따른 오류가 발생합니다.
오류 정보가 다음과 같은 경우,
![](https://main.qcloudimg.com/raw/9102b3394560ca9df2f70549baabe3ff.png)
pods의 target 버전이 종속된 플러그 인에 적합하지 않아 오류가 발생하는 것일 수 있습니다. 오류가 발생하는 pods의 target을 상응하는 버전으로 수정하십시오.












