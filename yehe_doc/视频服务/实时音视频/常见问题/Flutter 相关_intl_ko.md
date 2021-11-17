[](id:que1)
### 2대의 휴대폰에서 동시에 Demo를 실행할 경우 서로의 화면이 보이지 않는 이유는 무엇인가요?
2대의 휴대폰에서 Demo를 실행할 경우 각자 다른 UserID를 사용해야 합니다. TRTC에서는 동일 UserID(SDKAppID가 다를 경우 제외)를 2개의 단말에서 동시에 사용할 수 없습니다.

[](id:que2)
### 방화벽에 어떤 제한이 있나요?
SDK는 UDP 프로토콜을 통해 멀티미디어를 전송하므로, UDP를 차단하는 공용 네트워크에서는 사용할 수 없습니다. 이와 유사한 문제가 발생하는 경우 [방화벽 제한 대응 관련 질문](https://intl.cloud.tencent.com/document/product/647/35164)을 참고하여 진단 및 해결하십시오.

[](id:que3)
### iOS 패키지 실행 시 Crash가 발생합니다.
iOS14 이상의 debug 모드 문제가 아닌지 확인하시기 바랍니다. 자세한 내용은 [공식 설명](https://flutter.cn/docs/development/ios-14#launching-debug-flutter-without-a-host-computer)을 참고하십시오.

[](id:que4)
### iOS에서 비디오가 표시되지 않습니다. (Android는 정상)
프로젝트 'info.plist'의 'io.flutter.embedded_views_preview' 값이 YES인지 확인하십시오.

[](id:que5)
### SDK 버전 업데이트 후 iOS CocoaPods 실행 시 오류가 발생합니다.
1. iOS 디렉터리에서 'Podfile.lock' 파일을 삭제합니다.
2. 'pod repo update'를 진행합니다.
3. 'pod install'을 진행합니다.
4. 재실행합니다.

[](id:que6)
### Android Manifest merge failed 컴파일에 실패합니다.
1. '/example/android/app/src/main/AndroidManifest.xml' 파일을 엽니다.
2. 'xmlns:tools="http://schemas.android.com/tools"'를 manifest에 추가합니다.
3. `tools:replace="android:label"`을 application에 추가합니다.

![img](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

[](id:que7)
### 서명이 없어 실제 기기에서 디버깅 오류가 발생합니다.
오류 정보가 다음 이미지와 같은 경우,
![](https://main.qcloudimg.com/raw/809ae94061575b4e670f3a80ac9f3781.png)
1. Apple 인증서를 구매하여 설정 및 서명 작업을 완료한 후, 실제 기기 상에서 디버깅할 수 있습니다.
2. 인증서 구매 후, 'target > signing & capabilities'에서 설정을 진행합니다.

[](id:que8)
### 플러그 인 내 swift 파일 추가/삭제 후, build 시 해당 파일을 찾을 수 없습니다.
메인 프로젝트 디렉터리의 '/ios' 파일 경로에서 'pod install'을 진행하면 됩니다.

[](id:que9)
### Run 오류 “Info.plit, error: No value at that key path or invalid key path: NSBonjourServices”가 발생합니다.
`flutter clean` 진행 후, 재실행하면 됩니다.

[](id:que10)
### Pod install 오류가 발생합니다.
오류 정보가 다음 이미지와 같은 경우,
![](https://main.qcloudimg.com/raw/73db67cfc9e6b934fed947b63c6d2120.png)
오류 정보에 pod install이 표시되는 경우 'generated.xconfig' 파일이 존재하지 않아 실행 오류가 발생하는 것입니다. **flutter pub get 실행** 안내에 따라 해결하십시오.
>? 해당 문제는 flutter 컴파일 이후의 문제로, 신규 프로젝트 또는 `flutter clean`을 실행한 후에는 해당 문제가 발생하지 않습니다.

[](id:que11)
### Run 실행 시 iOS 버전에 오류가 발생합니다.
오류 정보가 다음 이미지와 같은 경우,
![](https://main.qcloudimg.com/raw/9102b3394560ca9df2f70549baabe3ff.png)
pods의 target 버전이 종속된 플러그 인에 적합하지 않아 오류가 발생하는 것일 수 있습니다. 오류가 발생하는 pods의 target을 해당 버전으로 수정하십시오.

[](id:que12)
### Flutter는 사용자 정의 수집 및 렌더링이 지원됩니까?
현재는 지원되지 않습니다. 사용자 정의 수집 및 렌더링 플랫폼 지원에 대한 자세한 내용은 [지원 플랫폼](https://intl.cloud.tencent.com/document/product/647/35158)을 참고하십시오.
