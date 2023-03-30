1. [](id:toc)
   이 솔루션을 사용하면 Tencent Cloud IM Flutter SDK를 기존 Android / iOS 애플리케이션에 통합할 수 있습니다.

   Flutter에서 전체 애플리케이션을 한 번에 다시 작성하는 것이 실용적이지 않은 경우가 있습니다. 이러한 상황에서 Flutter는 라이브러리 또는 모듈로 기존 APP에 단편적으로 통합될 수 있습니다. 그런 다음 해당 모듈을 Android 또는 iOS(현재 지원되는 플랫폼) APP으로 가져와 Flutter에서 APP UI의 일부를 렌더링할 수 있습니다.

   **기존의 IM 및 통화 모듈을 추가하여 워크로드를 크게 줄일 수 있습니다.**

   ![](https://qcloudimg.tencent-cloud.cn/raw/0a54bc281851a147b0f034a74c6001e5.png)

   ## 환경 요건

   | 환경                 | 버전                                                         |
   | -------------------- | ------------------------------------------------------------ |
   | Flutter              | SDK에는 최소 Flutter 2.2.0 버전이 필요하고 TUIKit 통합 컴포넌트 라이브러리에는 최소 Flutter 2.10.0 버전이 필요합니다. |
   | Android              | Android Studio 3.5 및 그 이후 버전. App은 Android 4.1 및 그 이후 버전 디바이스가 필요합니다. |
   | iOS                  | Xcode 11.0 및 그 이후 버전. 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인십시오. |
   | Tencent Cloud IM SDK | [tencent_im_sdk_plugin](https://pub.dev/packages/tencent_im_sdk_plugin) 5.0 이후 버전, [tim_ui_kit](https://pub.dev/packages/tim_ui_kit) 0.2 이후 버전. |

   >?
   >
   >상기 Demo 프로젝트의 소스 코드는 [GitHub 레지스트리](https://github.com/TencentCloud/tencentchat-add-flutter-to-app)에서 찾아 확인할 수 있습니다.

   ## 사전 지식

   시작하기 전에 Tencent Cloud IM Flutter SDK 및 TUIKit의 사용법에 대해 알고 기존 앱에 Flutter 모듈을 추가하는 것이 좋습니다.

   ### Tencent Cloud IM

   #### 시작하기

   시작하기 전에 Tencent Cloud IM Flutter의 SDK 및 기본 사용법에 대해 잘 알고 있어야 합니다.

   [non-UI SDK](https://cloud.tencent.com/document/product/269/68823#.E7.AC.AC.E4.BA.94.E9.83.A8.E5.88.86.EF.BC.9A.E8.87.AA.E5.AE.9E.E7.8E.B0-ui-.E9.9B.86.E6.88.90) 및 [TUIKit](https://cloud.tencent.com/document/product/269/70747)의 두 가지 주요 SDK가 포함됩니다. 이 튜토리얼에서는 주로 UI 라이브러리와 기본 비즈니스 로직을 사용하여 [TUIKit](https://cloud.tencent.com/document/product/269/70747)으로 개발합니다.

   **[시작하기](https://cloud.tencent.com/document/product/269/68823)를 통해 Tencent Cloud IM Flutter에 대해 알 수 있습니다.**

   [](id:modules)

   #### 두 개의 모듈

   Tencent Cloud IM에는 두 가지 주요 모듈인 Chat과 Call이 포함됩니다.

   Chat 모듈에는 메시지 송수신, 대화 관리, 관계 관리 등이 포함됩니다.

   Call 모듈에는 일대일 통화 및 그룹 통화를 포함한 음성 통화 및 영상 통화가 포함됩니다.

   ### 네이티브 앱에 Flutter 추가

   이 솔루션의 핵심은 Flutter module을 서브 프로젝트의 Native 애플리케이션에 포함하는 것입니다. Flutter의 크로스 플랫폼 기능으로 단일 Flutter module을 Android/iOS 프로젝트 모두에 추가할 수 있습니다.

   기존 애플리케이션이 Tencent Cloud IM 관련 페이지를 표시해야 하는 경우 Flutter를 호스팅하는 해당 Activity(Android) 또는 ViewController(iOS)를 로딩할 수 있습니다.

   [Method Channel](https://docs.flutter.dev/development/platform-integration/platform-channels#channels-and-platform-threading)은 현재 사용자 정보, 오프라인 푸시 및 음성/영상 통화 데이터의 EXT 전송과 같이 필요한 경우 Native APP와 Flutter 모듈 간에 통신하는 데 사용할 수 있습니다. 메소드 채널에서 메소드를 호출하고 미리 설정된 [MethodCallHandler](https://docs.flutter.dev/development/platform-integration/platform-channels#executing-channel-handlers-on-background-threads)로 호출을 수신합니다.

   [](id:android)

   #### Android 앱에 추가

   [세부 문서](https://docs.flutter.dev/development/add-to-app/android/project-setup)

   Gradle에서 Flutter module을 기존 앱의 종속성으로 추가합니다. 이를 구현하는 방법에는 두 가지가 있습니다.

   ##### Android 방법1: Android Archive (AAR)에 따라 다름

   AAR 메커니즘은 Flutter module 패키징을 위한 중개자로서 일반 Android AAR을 생성합니다. 자주 빌드하는 경우 빌드 단계를 추가합니다.

   이 방법은 Flutter 라이브러리를 AAR 및 POM 아티팩트로 구성된 일반 로컬 Maven 리포지토리로 패키징합니다. 이 방법을 사용하면 팀에서 Flutter SDK를 설치하지 않고도 호스트 앱을 빌드할 수 있습니다. 그런 다음 로컬 또는 원격 리포지토리에서 아티팩트를 배포할 수 있습니다.

   릴리스된 버전에 대해 이 방법을 사용하는 것이 좋습니다.

   **자세한 방법:**

   Flutter module에서 다음 명령을 실행합니다.

   ```shell
   flutter build aar
   ```

   그런 다음 화면의 지시에 따라 통합합니다.

   ![](https://qcloudimg.tencent-cloud.cn/raw/32e9376de02da10e97a8c54b9ab2b51c.png)

   이제 앱에 Flutter 모듈이 종속 항목으로 포함됩니다.

   ##### Android 방법2: Flutter module의 소스 코드에 따라 다름

   소스 코드 서브 프로젝트 메커니즘은 편리한 원스텝 빌드 프로세스이지만 Flutter SDK가 필요합니다. 이것은 Android Studio IDE 플러그인에서 사용하는 메커니즘입니다.

   이 방법을 사용하면 Android 프로젝트와 Flutter 프로젝트 모두에 대해 원스텝 빌드가 가능합니다. 이 방법은 두 부분에서 동시에 작업하고 빠르게 반복할 때 편리하지만 팀에서 호스트 앱을 빌드하려면 Flutter SDK를 설치해야 합니다.

   개발 및 디버깅 시 이 방법을 사용하는 것이 좋습니다.

   **자세한 방법:**

   호스트 앱의 `settings.gradle`에 서브 프로젝트로 Flutter module을 추가합니다.

   ```gradle
   // Include the host app project.
   include ':app'                                    // assumed existing content
   setBinding(new Binding([gradle: this]))                                // new
   evaluate(new File(                                                     // new
     settingsDir.parentFile,                                              // new
     'tencent_chat_module/.android/include_flutter.groovy'                // new
   ))                                                                     // new
   ```

   애플리케이션에서 `app/build.gradle => dependencies` 에서 Flutter module 의 `implementation` 을 가져옵니다.

   ```gradle
   dependencies{
     implementation project(':flutter')
   }
   ```

   이제 앱에 Flutter 모듈이 종속 항목으로 포함됩니다.

   [](id:ios)

   #### Flutter 모듈을 iOS 앱에 추가

   [세부 문서](https://docs.flutter.dev/development/add-to-app/ios/project-setup#embed-the-flutter-module-in-your-existing-application)

   기존 애플리케이션에 Flutter를 임베드하는 방법에는 두 가지가 있습니다.

   ##### iOS 방법1: CocoaPods 및 Flutter SDK 임베드

   CocoaPods 종속 항목 관리자를 사용하고 Flutter SDK를 설치합니다. 이 방법을 사용하려면 프로젝트에서 작업하는 모든 개발자가 Flutter SDK의 로컬 버전을 설치해야 합니다.

   스크립트를 자동으로 실행하여 DART 및 플러그인 코드를 포함하도록 Xcode에서 애플리케이션을 빌드하기만 하면 됩니다. 이를 통해 Xcode 외부에서 추가 명령을 실행하지 않고도 Flutter 모듈의 최신 버전으로 빠르게 반복할 수 있습니다.

   개발 및 디버깅 시 이 방법을 사용하는 것이 좋습니다.

   **자세한 방법:**

   Podfile에 다음 코드를 추가합니다.

   ```
   // Flutter Module의 경로
   flutter_chat_application_path = '../tencent_chat_module'
   
   load File.join(flutter_chat_application_path, '.ios', 'Flutter', 'podhelper.rb')
   ```

   Flutter를 임베드해야 하는 각 [Podfile target](https://guides.cocoapods.org/syntax/podfile.html#target)에 대해 `install_all_flutter_pods(flutter_chat_application_path)`을 호출합니다.

   ```
   target 'MyApp' do
     install_all_flutter_pods(flutter_chat_application_path)
   end
   ```

   Podfile의 `post_install` 블록에서 `flutter_post_install(installer)`를 호출하고 마이크 권한/카메라 권한/앨범 권한을 포함하여 [Tencent Cloud IM TUIKit](https://cloud.tencent.com/document/product/269/70747)에서 요구하는 권한 성명을 완료합니다.

   ```
   post_install do |installer|
     flutter_post_install(installer) if defined?(flutter_post_install)
     installer.pods_project.targets.each do |target|
         flutter_additional_ios_build_settings(target)
         target.build_configurations.each do |config|
               config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] ||= [
                 '$(inherited)',
                 'PERMISSION_MICROPHONE=1',
                 'PERMISSION_CAMERA=1',
                 'PERMISSION_PHOTOS=1',
               ]
             end
       end
   end
   ```

   'pod install'을 진행합니다.
   > ?
   >
   > - `tencent_chat_module/pubspec.yaml`에서 Flutter 플러그인 종속성을 변경할 때 Flutter Module 디렉터리에서 `flutter pub get`을 실행하여 `podhelper.rb` 스크립트에서 읽은 플러그인 목록을 새로 고칩니다. 그 다음 애플리케이션의 루트 디렉터리에서 `pod install`을 다시 실행합니다.
   > - Apple Silicon 칩 arm64 아키텍처가 있는 Mac 컴퓨터에서 `arch -x86_64 pod install --repo-update`를 실행해야 할 수도 있습니다.

   `podhelper.rb` 스크립트는 플러그인, / `Flutter.framework` / `App.framework`를 프로젝트에 임베드합니다.

   ##### iOS 방법2: Xcode에 frameworks 임베드

   Flutter 엔진, 컴파일된 DART 코드 및 모든 Flutter 플러그인용 프레임워크를 생성합니다. 프레임워크를 수동으로 임베드하고 Xcode에서 기존 앱의 빌드 설정을 업데이트합니다.

   또는 기존 Xcode 프로젝트를 수동으로 편집하여 필요한 framework를 생성하고 애플리케이션에 임베드할 수 있습니다. 팀 구성원이 Flutter SDK 및 CocoaPods를 로컬에 설치할 수 없거나 기존 애플리케이션에서 CocoaPods를 종속 항목 관리자로 사용하고 싶지 않은 경우 이렇게 할 수 있습니다. Flutter 모듈에서 코드를 변경할 때마다 `flutter build ios-framework`를 실행해야 합니다.

   릴리스된 버전에 대해 이 방법을 사용하는 것이 좋습니다.

   **자세한 방법:**

   Flutter module에서 다음 명령을 실행합니다.

   다음 예시에서는 framework를 `some/path/MyApp/Flutter/`에 생성한다고 가정합니다.

   ```shell
   flutter build ios-framework --output=some/path/MyApp/Flutter/
   ```

   생성된 frameworks를 Xcode의 기존 애플리케이션에 임베드하고 연결합니다. 예를 들어 `some/path/MyApp/Flutter/Release/` 디렉터리에서 애플리케이션 target 컴파일 설정의 General > Frameworks, Libraries, and Embedded Content로 frameworks를 드래그한 다음 Embed 드롭다운 목록에서‘Embed & Sign’을 선택할 수 있습니다.


   ## 추가 모드

   기존 애플리케이션에 Flutter Module을 추가하는 것이 좋습니다.

   Native 프로젝트에서 Flutter의 Chat 및 Call 모듈을 수행할 Flutter 엔진을 빌드합니다. 자세한 내용은 [여기](#modules)를 참고하십시오.

   Flutter 엔진의 두 가지 모드(단일 FlutterEngine 또는 FlutterEngineGroup이 있는 두 개의 FlutterEngine)가 제공됩니다.

   | 엔진 모드                      | 소개                                                         | 장점                                                         | 단점                                                         | Demo 소스 코드 다운로드                                      |
   | ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
   | [단일 Flutter 엔진](#single)   | Chat과 Call 모두 하나의 FlutterEngine으로 통합됩니다.        | 편리하고 모든 Flutter 코드가 균일하게 유지됩니다.            | Call 플러그인으로 인해 전화가 걸려오면 통화 상태를 표시하기 위해 Flutter 페이지로 이동해야 하며 이로 인해 현재 상태가 중단될 수 있으며 상대적으로 좋지 않은 경험을 할 수 있습니다. | [GitHub](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Single%20Flutter%20Engines) |
   | [멀티 Flutter 엔진](#multiple) | 두 개의 개별 FlutterEngine에 있는 Chat 및 Call 모듈이며, Flutter 엔진 그룹은 두 엔진을 통합 관리하는 데 사용됩니다. | Call 플러그인은 Flutter 엔진에 독립적으로 존재하며 독립적인 페이지에 의해 제어됩니다. 전화가 오면 통화 페이지는 별도로 존재해야 하며, 통화가 끝나면 현재 상태를 탐색하지 않고 자동으로 해제하여 더 나은 경험을 제공합니다. | 통화 페이지 최소화는 허용되지 않습니다.                      | [GitHub](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Multiple%20Flutter%20Engines) |

   또한 IM Native SDK와 Flutter SDK를 모두 통합하는 솔루션도 제공됩니다. 자세한 내용은 [여기](#native)를 참고하십시오. Demo는 [GitHub](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Initialize%20from%20Native)에서 확인할 수 있습니다.

   [](id:multiple)

   ## 솔루션1: 멀티 FlutterEngine[권장]

   이 솔루션에서 Chat 및 Call 모듈은 서로 다른 Flutter 엔진과 독립적입니다.

   멀티 Flutter 엔진을 사용할 때의 이점은 각 인스턴스가 독립적이고 자체 내부 탐색 스택, UI 및 애플리케이션 상태를 유지한다는 것입니다. 이는 상태 유지에 대한 전체 애플리케이션 코드의 책임을 단순화하고 모듈성을 향상시킵니다.

   ![](https://qcloudimg.tencent-cloud.cn/raw/87cc37d846388fb3c66aab6743cfede2.png)

   Android 및 iOS에 여러 Flutter 엔진을 추가하는 것은 주로 FlutterEngineGroup 클래스(Android API, iOS API)를 기반으로 하여 여러 FlutterEngine(Flutter 엔진)을 구성하고 관리합니다.

   당사 프로젝트에서는 하나의 FlutterEngineGroup이 Chat 및 Calling 모듈을 포함하여 두 개의 FlutterEngine을 관리하는 데 사용됩니다.

   [![](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Multiple%20Flutter%20Engines)

   ### Flutter Module 개발

   Flutter를 기존 애플리케이션에 임베드하려면 먼저 Flutter 모듈을 생성하십시오.

   명령줄에서 다음을 실행합니다.

   ```
   cd some/path/
   flutter create --template module tencent_chat_module
   ```

   Flutter 모듈 프로젝트는 some/path/tencent_chat_module/에 생성됩니다. 해당 디렉터리에서 `flutter run --debug` 또는 `flutter build ios`와 같은 다른 Flutter 프로젝트에서와 동일한 Flutter 명령을 실행할 수 있습니다. Flutter 및 Dart 플러그인을 사용하여 Android Studio, IntelliJ 또는 VS Code에서 모듈을 실행할 수도 있습니다. 이 프로젝트에는 기존 애플리케이션에 임베드되기 전에 모듈의 단일 보기 예시 버전이 포함되어 있으며, 이는 코드의 Flutter 전용 부분을 점진적으로 테스트하는 데 유용합니다.

   `tencent_chat_module` 모듈 디렉터리 구조는 일반 Flutter 애플리케이션과 유사합니다.

   ```
   tencent_chat_module/
   ├── .ios/
   │   ├── Runner.xcworkspace
   │   └── Flutter/podhelper.rb
   ├── lib/
   │   └── main.dart
   ├── test/
   └── pubspec.yaml
   ```

   이제 `lib/` 내에서 코딩할 수 있습니다.

   #### Flutter lib의 구조

   >?
   >
   >다음 구조와 코드는 데모용이며 실제 요구 사항에 맞게 동적으로 수정할 수 있습니다. 필요에 따라 Tencent Cloud IM Flutter를 가져올 수 있습니다.

   이제 `lib/` 내에 `call`, `chat`, `common`을 포함하여 세 개의 디렉터리를 생성해 보겠습니다. 통화 엔진, IM 엔진 및 일반적인 model 클래스에 별도로 사용됩니다.

   ```
   tencent_chat_module/
   ├── lib/
   │   └── call/
   │   └── chat/
   │   └── common/
   ```

   #### 일반적인 model 클래스 모듈

   새 파일 `common/common_model.dart`에 다음 두 class를 추가합니다. 네이티브와 Flutter 간의 통신 프록시를 정의하는 데 사용됩니다.

   ```dart
   class ChatInfo {
     String? sdkappid;
     String? userSig;
     String? userID;
   
     ChatInfo.fromJSON(Map<String, dynamic> json) {
       sdkappid = json["sdkappid"].toString();
       userSig = json["userSig"].toString();
       userID = json["userID"].toString();
     }
   
     Map<String, String> toMap(){
       final Map<String, String> map = {};
       if(sdkappid != null){
         map["sdkappid"] = sdkappid!;
       }
       if(userSig != null){
         map["userSig"] = userSig!;
       }
       if(userID != null){
         map["userID"] = userID!;
       }
       return map;
     }
   }
   
   class CallInfo{
     String? userID;
     String? groupID;
   
     CallInfo();
   
     CallInfo.fromJSON(Map<String, dynamic> json) {
       groupID = json["groupID"].toString();
       userID = json["userID"].toString();
     }
   
     Map<String, String> toMap(){
       final Map<String, String> map = {};
       if(userID != null){
         map["userID"] = userID!;
       }
       if(groupID != null){
         map["groupID"] = groupID!;
       }
       return map;
     }
   }
   ```

   #### Chat 모듈

   **먼저 IM 엔진을 작성합니다. 이 모듈의 모든 코드와 파일은 `lib/chat` 디렉터리에 있습니다.**

   1. 글로벌 상태 관리 Model로 사용되는 `model.dart` 파일을 생성합니다.
      이 Model은 Tencent Cloud IM Flutter 모듈, 오프라인 회선 푸시 모듈, 글로벌 상태 관리 및 Native 앱과의 통신을 초기화하고 유지하는 데 사용됩니다.
      Chat 모듈의 핵심입니다.
      자세한 구현은 Demo의 소스 코드를 참고할 수 있지만 다음 세 가지 기능에 집중하는 것이 좋습니다.
       - Future<dynamic> _handleMessage(MethodCall call): 로그인 정보, 클릭 푸시 이벤트 등 Native 앱에서 호출한 메시지를 수신합니다.
       - Future<void> handleClickNotification(Map<String, dynamic> msg): Native 패스스루 전송에서 이벤트를 처리하려면 알림을 클릭하고 Map에서 데이터를 가져오고 특정 세션과 같은 해당 서브 모듈로 리디렉션합니다.
       - Future<void> initChat(): Tencent Cloud IM SDK 및 오프라인 푸시 플러그인을 초기화하고 로그인하고 Token을 업로드합니다. 이 방법은 동기화 잠금 메커니즘을 사용하여 동시에 하나만 실행할 수 있도록 하고 초기화가 성공한 후에는 반복적으로 실행되지 않습니다.

   > ?
   >
   > Token을 업로드하기 전에 오프라인 푸시를 구성하고 이 [문서](https://cloud.tencent.com/document/product/269/74605)를 참고하여 이 기능을 사용하십시오.

   2. Chat 모듈의 주 게이트로 사용되는 `chat_main.dart` 파일을 생성합니다.
      - 또한 Flutter Chat 모듈의 홈 페이지로 사용됩니다.
      - Demo에서는 로그인하기 전에 로드 상태를 표시한 다음 대화 목록을 표시합니다.
      - 또한 여기에서 'didChangeAppLifecycleState' 모니터링 및 각 포그라운드/백그라운드 전환 시 애플리케이션의 현재 상태를 Tencent Cloud Chat 백엔드에 리포트해야 합니다. 자세한 내용은 [문서](https://cloud.tencent.com/document/product/269/74605#.E6.AD.A5.E9.AA.A45.EF.BC.9A.E5.89.8D.E5.90.8E.E5.8F.B0.E5.88.87.E6.8D.A2.E7.9B.91.E5.90.AC.3Ca-id.3D.22step_5.22.3E.3C.2Fa.3E)를 참고하십시오.
      - 자세한 구현은 Demo의 소스 코드를 참고하십시오.

   3. 싱글톤 관리 [오프라인 푸시 플러그인](https://cloud.tencent.com/document/product/269/74605)을 유지 관리하는 데 사용되는 `push.dart` 파일을 생성합니다. Token 획득 및 리포트/푸시 권한 획득 등의 작업에 사용됩니다. 자세한 구현은 Demo의 소스 코드를 참고하십시오.

   4. TUIKit의 대화 목록 위젯 `TIMUIKitConversation`을 구현하는 데 사용되는 `conversation.dart` 파일을 생성합니다. 자세한 구현은 Demo의 소스 코드를 참고하십시오.

   5. TUIKit의 기록 메시지 목록을 구현하고 메시지 위젯 `TIMUIKitChat`을 보내는 데 사용되는 `chat.dart` 파일을 생성합니다.
      이 페이지는 Profile 및 Group Profile로 리디렉션할 수도 있습니다.
      자세한 구현은 Demo의 소스 코드를 참고하십시오.

   6. TUIKit의 사용자 프로필 위젯 `TIMUIKitProfile`을 구현하는 데 사용되는 `user_profile.dart` 파일을 생성합니다. 자세한 구현은 Demo의 소스 코드를 참고하십시오.

   7. TUIKit의 그룹 프로필 위젯 `TIMUIKitGroupProfile`을 구현하는 데 사용되는 `group_profile.dart` 파일을 생성합니다. 자세한 구현은 Demo의 소스 코드를 참고하십시오.

   이제 다음과 같은 구조로 Chat 모듈이 개발되었습니다.

   ```
   tencent_chat_module/
   ├── lib/
   │   └── call/
   │       └── chat.dart
   │       └── model.dart
   │       └── chat_main.dart
   │       └── push.dart
   │       └── conversation.dart
   │       └── user_profile.dart
   │       └── group_profile.dart
   │   └── chat/
   │   └── common/
   ```

   #### Call 모듈

   [음성/영상 통화 플러그인](https://pub.dev/packages/tim_ui_kit_calling_plugin)에서 제공하는 음성 통화 및 영상 통화에 사용되는 모듈입니다.

   이 모듈의 핵심 기능은 걸려오는 전화를 수신할 때 Native에 이 페이지를 보여달라고 요청하는 메소드를 호출하는 것입니다. 또는 Native를 통해 Chat 모듈에서 요청을 수신하면 다른 사람에게 전화를 걸 수 있습니다.

   ** 먼저 IM 엔진을 작성하십시오. 다음 코드 및 파일은 `lib/call` 디렉터리에 있습니다.**

   1. 글로벌 상태 관리 Model로 사용되는 `model.dart` 파일을 생성합니다.
      이 Model은 [음성/영상 통화 플러그인](https://pub.dev/packages/tim_ui_kit_calling_plugin)의 인스턴스 초기화 및 관리, 전역 상태 관리, Native 앱과의 통신에 사용됩니다.
      Call 모듈의 핵심입니다.
      자세한 구현은 Demo의 소스 코드를 참고할 수 있지만 다음 세 가지 기능에 집중하는 것이 좋습니다.
       - _onRtcListener = TUICallingListener(...): 통화 이벤트의 리스너, Method Channel을 통해 Native 레이어에 알리고, Call 모듈이 속한 ViewController(iOS)/Activity(Android)의 프런트 엔드 표시 여부를 동적으로 제어합니다.
       - Future<dynamic> _handleMessage(MethodCall call): Native를 통해 Call 모듈에서 요청을 수신할 때 주로 다른 사람에게 통화를 시작하는 데 사용되는 메소드 채널 호출 이벤트의 리스너입니다.

   2. Call 모듈의 주 게이트로 사용되는 `call_main.dart` 파일을 생성합니다.
         시작 호출 페이지에 사용되며 [음성/영상 통화 플러그인에 바인딩해야 하는 navigatorKey](https://pub.dev/packages/tim_ui_kit_calling_plugin)는 여기에 추가되어야 합니다.
         자세한 구현은 Demo의 소스 코드를 참고하십시오.


   #### 각 Flutter 엔진의 게이트 구성

   상기 세가지 모듈을 개발한 후 이제 FlutterEngine의 게이트로 사용되는 각 모듈의 게이트를 구성할 수 있습니다.

   1. 기본 게이트

   `lib/main.dart`를 열고 빈 MaterialApp을 반환하도록 기본 `main()` 기능을 수정합니다.

   이 메소드는 Flutter Module의 기본 게이트로 사용되며, FlutterEngineGroup을 사용하는 Flutter 멀티 엔진 관리에서 서브 Flutter Engine이 없고 entry point가 설정되지 않은 경우 이 메소드는 사용되지 않습니다.

   예를 들어 이 시나리오에서는 기본 `main()` 메소드가 사용되지 않습니다.

   ```dart
   void main() {
     WidgetsFlutterBinding.ensureInitialized();
   
     runApp(MaterialApp(
       title: 'Flutter Demo',
       theme: ThemeData(
         primarySwatch: Colors.blue,
       ),
       home: Container(),
     ));
   }
   ```

   2. Chat 모듈 게이트

   메소드를 `entry-point`로 표시하려면 `@pragma('vm:entry-point')` 주석을 사용합니다. 메소드 이름 `chatMain`은 항목의 이름입니다. Native에서 이 이름은 해당 FlutterEngine을 생성하는 데에도 사용됩니다.

   전역 `ChangeNotifierProvider` 상태 관리를 사용하여 `ChatInfoModel` 데이터 및 비즈니스 로직을 유지합니다.

   ```dart
   @pragma('vm:entry-point')
   void chatMain() {
     // This call ensures the Flutter binding has been set up before creating the
     // MethodChannel-based model.
     WidgetsFlutterBinding.ensureInitialized();
   
     final model = ChatInfoModel();
   
     runApp(
       ChangeNotifierProvider.value(
         value: model,
         child: const ChatAPP(),
       ),
     );
   }
   ```

   3. Call 모듈 게이트

   이 게이트의 이름은 `callMain`으로 지정됩니다.

   전역 `ChangeNotifierProvider` 상태 관리를 사용하여 `CallInfoModel` 데이터 및 비즈니스 로직을 유지합니다.

   ```dart
   @pragma('vm:entry-point')
   void callMain() {
     // This call ensures the Flutter binding has been set up before creating the
     // MethodChannel-based model.
     WidgetsFlutterBinding.ensureInitialized();
   
     final model = CallInfoModel();
   
     runApp(
       ChangeNotifierProvider.value(
         value: model,
         child: const CallAPP(),
       ),
     );
   }
   ```

   여기까지 Flutter Module용 Dart 코드가 작성 완료되었습니다.

   이제 기존 앱의 Native 통합을 살펴보겠습니다.

   ### iOS Native 개발

   여기에서는 Swift를 예로 듭니다.

   >?
   >
   >다음 구조와 코드는 데모용이며 실제 요구 사항에 맞게 효율적으로 구성할 수 있습니다.

   XCode 내에서 iOS 프로젝트를 엽니다.

   기존 애플리케이션(`MyApp`)에 아직 Podfile이 없는 경우 [CocoaPods 시작하기 가이드](https://guides.cocoapods.org/using/using-cocoapods.html)에 따라 프로젝트에 `Podfile`을 추가하십시오.

   #### Flutter Module 가져오기

   기존 iOS 앱에 Flutter module을 추가하는 부분은 [이 부분](#ios)을 참고하십시오.

   #### iOS 프로젝트에서 FlutterEngine 관리

   ![](https://qcloudimg.tencent-cloud.cn/raw/039ec36a5696f2188f9fa8ab11071210.png)

   **`FlutterEngineGroup`을 생성하여 여러 엔진 인스턴스를 통합 관리합니다.**

   `AppDelegate.swift`에 다음을 추가합니다.

   ```swift
   @UIApplicationMain
   class AppDelegate: FlutterAppDelegate {
     lazy var flutterEngines = FlutterEngineGroup(name: "chat.flutter.tencent", project: nil)
     ...
   }
   ```

   **FlutterEngine을 관리할 싱글톤 객체를 생성합니다.**

   이 Swift 싱글톤 객체는 한 곳에서 Flutter 인스턴스를 관리하는 데 사용되며 메소드를 호출하기 위해 전체 프로젝트에 메소드를 제공합니다.

   Demo의 기본 구현 로직은 Chat의 ViewController에 대한 새 네비게이터를 사용하는 동안 자동으로 Call의 ViewController를 present 및 dismiss하는 것입니다.

   새 파일 `FlutterUtils.swift`를 생성하고 코딩합니다. 자세한 코드는 Demo 소스 코드를 참고하십시오.

   주로 다음에 초점을 맞춥니다:
   - private override init(): 각 Flutter 엔진 인스턴스를 초기화하고 Method Channel 이벤트를 등록합니다.
   - func reportChatInfo(): Tencent Cloud IM SDK 초기화 및 로그인을 위해 현재 사용자 로그인 정보 및 SDKAPPID를 Flutter Module에 리포트합니다.
   - func launchCallFunc(): Call을 시작하는 데 사용되는 Flutter 페이지는 통화 초대를 받는 Call 모듈이나 적극적으로 통화를 시작하는 Chat 모듈에 의해 트리거될 수 있습니다.
   - func triggerNotification(msg: String): iOS Native 레이어에서 받은 오프라인 푸시 메시지 클릭 이벤트와 그 안에 포함된 ext 정보를 Flutter 레이어에 바인딩된 수신 처리 이벤트에 JSON String 형태로 패스스루합니다. 예를 들어 해당 세션으로의 오프라인 푸시 클릭 리디렉션을 처리하는 데 사용됩니다.

   **오프라인 푸시 클릭 이벤트 수신 및 포워딩**

   오프라인 푸시 초기화/Token 업로드/클릭 이벤트에 따른 세션 리디렉션 처리 등은 Flutter Chat 모듈에서 모두 이루어졌기 때문에 Native 영역에서는 클릭 알림 이벤트의 ext만 전달하면 됩니다.

   이렇게 해야 하는 이유는 클릭 알람 이벤트가 Native에서 소비되었기 때문에 Flutter 레이어에서 직접 가져올 수 없으며 Native를 통해 포워딩해야 하기 때문입니다.

   `AppDelegate.swift` 파일에 다음 코드를 추가합니다. 특정 코드는 Demo 소스 코드를 참고하십시오.

   ![](https://qcloudimg.tencent-cloud.cn/raw/9c816ae4745e5a8d2b9b1d64167e1fc5.png)

   이제 iOS Native 레이어 작성을 완료했습니다.

   ### Android Native 개발

   여기서는 Kotlin을 예로 듭니다.

   >?
   >
   >다음 구조와 코드는 데모용이며 실제 요구 사항에 맞게 효율적으로 구성할 수 있습니다.

   #### Flutter Module 가져오기

   기존 Android 앱에 Flutter module을 추가하는 부분은 [이 부분](#android)을 참고하십시오. 방법2를 권장합니다.

   #### Android 프로젝트에서 FlutterEngine 관리

   **FlutterEngine을 관리할 싱글톤 객체를 생성합니다.**

   이 Kotlin 싱글톤 객체는 한 곳에서 Flutter 인스턴스를 관리하는 데 사용되며 메소드를 호출하기 위해 전체 프로젝트에 메소드를 제공합니다.

   새 파일 `FlutterUtils.kt`를 생성하고 정적 객체 `FlutterUtils`를 정의합니다.

   ```kotlin
   @SuppressLint("StaticFieldLeak")
   object FlutterUtils {}
   ```

   **`FlutterEngineGroup`을 생성하여 여러 엔진 인스턴스를 통합 관리합니다.**

   `FlutterUtils.kt` 파일에서 `FlutterEngineGroup`을 정의하고, 각 FlutterEngine 인스턴스와 MethodChannel을 지원하며 초기화 시 초기화합니다.

   ```kotlin
   lateinit var context : Context
   lateinit var flutterEngines: FlutterEngineGroup
   private lateinit var chatFlutterEngine:FlutterEngine
   private lateinit var callFlutterEngine:FlutterEngine
   
   lateinit var chatMethodChannel: MethodChannel
   lateinit var callMethodChannel: MethodChannel
   
   // 초기화
   flutterEngines = FlutterEngineGroup(context)
   ...
   ```

   **Flutter 엔진을 관리하는 싱글톤 객체를 계속 완료합니다.**

   Demo의 기본 구현 로직은 Chat과 Call 모두의 Activity에 대한 새 네비게이터를 사용하는 것입니다.

   Chat의 Activity는 사용자가 들어가고 나가는 반면, Call의 Activity는 자동으로 들어가고 나가며, 리스너에 의해 트리거되거나 수동으로 전화를 겁니다.

   주로 다음에 초점을 맞춥니다:
   - fun init(): 각 Flutter 엔진 인스턴스를 초기화하고 Method Channel을 등록하고 이벤트를 수신합니다.
   - fun reportChatInfo(): Flutter 레이어를 초기화하고 Tencent Cloud IM에 로그인할 수 있도록 사용자 로그인 정보 및 SDKAPPID를 Flutter Module에 패스스루합니다.
   - fun launchCallFunc(): Call을 시작하는 데 사용되는 Flutter 페이지는 통화 초대를 받는 Call 모듈이나 통화를 시작하는 Chat 모듈에 의해 트리거될 수 있습니다.
   - fun triggerNotification(msg: String): iOS Native 레이어에서 받은 오프라인 푸시 메시지 클릭 이벤트와 그 안에 포함된 ext 정보를 Flutter 레이어에 바인딩된 수신 처리 이벤트에 JSON String 형태로 패스스루합니다. 예를 들어 해당 세션으로의 오프라인 푸시 클릭 리디렉션을 처리하는 데 사용됩니다.

   이 싱글톤 object에 대한 Demo 소스 코드를 참고하십시오.

   **주 게이트 `MyApplication`에서 위의 객체를 초기화합니다.**

   `MyApplication.kt` 파일에서 전역 context를 싱글톤 객체로 전송하고 초기화합니다.

   ```kotlin
   class MyApplication : MultiDexApplication() {
   
       override fun onCreate() {
           super.onCreate()
           FlutterUtils.context = this // new
           FlutterUtils.init()         // new
       }
   }
   ```

   **오프라인 푸시 클릭 이벤트 수신 및 포워딩**

   오프라인 푸시 초기화/Token 업로드/클릭 이벤트에 따른 세션 리디렉션 처리 등은 Flutter Chat 모듈에서 모두 이루어졌기 때문에 Native 영역에서는 클릭 알림 이벤트의 ext만 전달하면 됩니다.

   이렇게 해야 하는 이유는 클릭 알람 이벤트가 Native에서 소비되었기 때문에 Flutter 레이어에서 직접 가져올 수 없으며 Native를 통해 포워딩해야 하기 때문입니다.

   >! 다양한 벤더 간의 오프라인 푸시 액세스 단계는 일치하지 않습니다. 본문에서는 OPPO를 예로 들어 설명하였습니다. 전체 벤더의 액세스 솔루션은 [이 문서](https://www.tencentcloud.com/document/product/1047/39156)를 참고하십시오.

   Tencent Cloud IM 콘솔에 OPPO의 푸시 인증서를 추가하고 '후속 작업 클릭', `앱에서 지정된 페이지 열기`를 선택하면 `인앱 페이지`는 오프라인 푸시 정보를 처리하기 위한 페이지를 `Activity`로 구성하며, 앱의 홈 페이지로 설정하는 것이 좋습니다. 예를 들어 Demo 구성은 `com.tencent.chat.android.MainActivity`입니다.

   ![](https://qcloudimg.tencent-cloud.cn/raw/fd384ea1140199113d01a6650c0c8f3d.png)

   상기 콘솔에 대해 설정된 오프라인 푸시를 위한 Activity 파일에 다음 코드를 추가합니다.

   이 코드의 기능은 벤더가 해당 Activity를 가져올 때 Bundle에서 HashMap 형식의 ext 정보를 꺼내고 싱글톤 객체의 메소드를 트리거하고 이 정보를 Flutter에 수동으로 포워딩할 수 있습니다. 이 기능에 대한 Demo 소스 코드를 참고하십시오.

   ![](https://qcloudimg.tencent-cloud.cn/raw/2ec45c1a8b3bd952bcb86a8095f91515.png)

   이제 Android Native 레이어 작성을 완료했습니다.


   [](id:single)

   ## 솔루션2: 단일 FlutterEngine

   이 솔루션에서 Chat 모듈과 Call 모듈은 단일 Flutter 엔진 인스턴스에 포함됩니다.

   ![](https://qcloudimg.tencent-cloud.cn/raw/115b917df15da5d84ea6794774a3b080.png)

   결과적으로 이러한 모듈은 동시에 표시하거나 숨길 수만 있으며 하나의 Flutter 엔진만 점검하면 됩니다.

   ![](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Single%20Flutter%20Engines)

   ### Flutter Module 개발

   Flutter를 기존 애플리케이션에 임베드하려면 먼저 Flutter 모듈을 생성하십시오.

   명령줄에서 다음을 실행합니다.

   ```
   cd some/path/
   flutter create --template module tencent_chat_module
   ```

   Flutter 모듈 프로젝트는 some/path/tencent_chat_module/에 생성됩니다. 해당 디렉터리에서 `flutter run --debug` 또는 `flutter build ios`와 같은 다른 Flutter 프로젝트에서와 동일한 Flutter 명령을 실행할 수 있습니다. Flutter 및 Dart 플러그인을 사용하여 Android Studio, IntelliJ 또는 VS Code에서 모듈을 실행할 수도 있습니다. 이 프로젝트에는 기존 애플리케이션에 임베드되기 전에 모듈의 단일 보기 예제 버전이 포함되어 있으며, 이는 코드의 Flutter 전용 부분을 점진적으로 테스트하는 데 유용합니다.

   `tencent_chat_module` 모듈 디렉터리 구조는 일반 Flutter 애플리케이션과 유사합니다.

   ```
   tencent_chat_module/
   ├── .ios/
   │   ├── Runner.xcworkspace
   │   └── Flutter/podhelper.rb
   ├── lib/
   │   └── main.dart
   ├── test/
   └── pubspec.yaml
   ```

   이제 `lib/` 내에서 코딩할 수 있습니다.

   #### main.dart

   `main.dart`를 수정하여 [TUIKi](https://cloud.tencent.com/document/product/269/70747), [오프라인 푸시 플러그인](https://cloud.tencent.com/document/product/269/74605) 및 [통화 플러그인](https://pub.dev/packages/tim_ui_kit_calling_plugin)을 통합합니다.

   글로벌 상태인 IM SDK 및 Method Channel과 Native 통신 상태는 `ChatInfoModel`에서 관리됩니다.

   Native로부터 로그인 사용자 정보 및 SDKAPPID를 받은 후 `_coreInstance.init()`, `_coreInstance.login() `을 호출하여 Tencent Cloud IM SDK를 초기화하고 로그인합니다. 또한 오디오/비디오 푸시 플러그인과 오프라인 푸시 플러그인도 초기화하고 푸시 Token 리포트를 완료합니다.

   > ?
   >
   > Token을 업로드하기 전에 벤더의 오프라인 푸시를 구성하고 이 [오프라인 푸시 엑세스 가이드](https://cloud.tencent.com/document/product/269/74605)를 참고하여 이 기능을 사용하십시오.

   음성/영상 통화 플러그인에 대한 팁:
   - 통화 초대를 수신하고 Native 메소드를 호출하여 사용자가 현재 이 Flutter 모듈 페이지에 있는지 여부를 Native가 점검하도록 합니다. 현재 위치에 있지 않은 경우 수신 전화 페이지를 표시하려면 프런트 엔드 페이지를 이 모듈로 강제 조정해야 합니다.

   오프라인 푸시 플러그인에 대한 팁:
   - 알림을 클릭하여 Native 패스스루 전송에서 이벤트를 처리하고, Map에서 데이터를 가져오고, 특정 세션과 같은 해당 서브 모듈로 이동합니다.

   홈페이지 제작을 완료하고 로그인하기 전에 로딩 상태를 표시하고, 로그인 후 대화 목록 페이지를 표시합니다.

   또한 여기에서 `didChangeAppLifecycleState` 수신 및 각 포그라운드/백그라운드 전환 시 애플리케이션의 현재 상태를 리포트해야 합니다. 자세한 내용은 [오프라인 푸시 플러그인 문서 5단계](https://cloud.tencent.com/document/product/269/74605#.E6.AD.A5.E9.AA.A45.EF.BC.9A.E5.89.8D.E5.90.8E.E5.8F.B0.E5.88.87.E6.8D.A2.E7.9B.91.E5.90.AC.3Ca-id.3D.22step_5.22.3E.3C.2Fa.3E)를 참고하십시오.

   자세한 구현은 Demo의 소스 코드를 참고하십시오.

   #### TUIKit의 다른 모듈 가져오기

   1. 싱글톤 관리 [오프라인 푸시 플러그인](https://cloud.tencent.com/document/product/269/74605)을 유지 관리하는 데 사용되는 `push.dart` 파일을 생성합니다. Token 획득 및 리포트/푸시 권한 획득 등의 작업에 사용됩니다. 자세한 구현은 Demo의 소스 코드를 참고하십시오.

   2. TUIKit의 대화 목록 위젯 `TIMUIKitConversation`을 구현하는 데 사용되는 `conversation.dart` 파일을 생성합니다. 자세한 구현은 Demo의 소스 코드를 참고하십시오.

   3. TUIKit의 기록 메시지 목록을 구현하고 메시지 위젯 `TIMUIKitChat`을 보내는 데 사용되는 `chat.dart` 파일을 생성합니다.
      이 페이지는 Profile 및 Group Profile로 리디렉션할 수도 있습니다.
      자세한 구현은 Demo의 소스 코드를 참고하십시오.

   4. TUIKit의 사용자 프로필 위젯 `TIMUIKitProfile`을 구현하는 데 사용되는 `user_profile.dart` 파일을 생성합니다. 자세한 구현은 Demo의 소스 코드를 참고하십시오.

   5. TUIKit의 그룹 프로필 위젯 `TIMUIKitGroupProfile`을 구현하는 데 사용되는 `group_profile.dart` 파일을 생성합니다. 자세한 구현은 Demo의 소스 코드를 참고하십시오.

   이제 Flutter Module이 개발되었습니다.

   ### iOS Native 개발

   여기에서는 Swift를 예로 들어 Objective-C도 사용할 수 있습니다.

   >?
   >
   >다음 구조와 코드는 데모용이며 실제 요구 사항에 맞게 효율적으로 구성할 수 있습니다.

   XCode 내에서 iOS 프로젝트를 엽니다.

   기존 애플리케이션(`MyApp`)에 아직 Podfile이 없는 경우 [CocoaPods 시작하기 가이드](https://guides.cocoapods.org/using/using-cocoapods.html)에 따라 프로젝트에 `Podfile`을 추가하십시오.

   #### Flutter Module 가져오기

   기존 iOS 앱에 Flutter module을 추가하는 부분은 [이 부분](#ios)을 참고하십시오.

   #### iOS 프로젝트에서 FlutterEngine 관리

   **FlutterEngine을 생성합니다.**

   FlutterEngine을 생성하는 적절한 위치는 호스트 앱에 따라 다릅니다. 예를 들어 `AppDelegate`에서 app 시작 시 속성으로 노출되는 FlutterEngine 생성을 시연합니다.

   ```swift
   import UIKit
   import Flutter
   import FlutterPluginRegistrant
   
   @UIApplicationMain
   class AppDelegate: FlutterAppDelegate { // More on the FlutterAppDelegate.
     lazy var flutterEngine = FlutterEngine(name: "tencent cloud chat")
   
     override func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
       // Runs the default Dart entrypoint with a default Flutter route.
       flutterEngine.run();
       GeneratedPluginRegistrant.register(with: self.flutterEngine);
       return super.application(application, didFinishLaunchingWithOptions: launchOptions);
     }
   }
   ```

   **FlutterEngine을 관리할 싱글톤 객체를 생성합니다.**

   이 Swift 싱글톤 객체는 한 곳에서 Flutter Method Channel을 관리하는 데 사용되며 Flutter Module 통신 메소드를 호출하기 위해 전체 프로젝트에 메소드를 제공합니다.

   주로 다음에 초점을 맞춥니다:
   - private override init(): 각 Flutter 인스턴스를 초기화하고 Method Channel 이벤트를 등록합니다.
   - func reportChatInfo(): Tencent Cloud IM SDK 초기화 및 로그인을 위해 현재 사용자 로그인 정보 및 SDKAPPID를 Flutter Module에 리포트합니다.
   - func launchChatFunc(): Flutter Module용 ViewController를 표시합니다.
   - func triggerNotification(msg: String): iOS Native 레이어에서 받은 오프라인 푸시 메시지 클릭 이벤트와 그 안에 포함된 ext 정보를 Flutter 레이어에 바인딩된 수신 처리 이벤트에 JSON String 형태로 패스스루합니다. 예를 들어 해당 세션으로의 오프라인 푸시 클릭 리디렉션을 처리하는 데 사용됩니다.

   자세한 구현은 Demo의 소스 코드를 참고하십시오.

   **오프라인 푸시 클릭 이벤트 수신 및 포워딩**

   오프라인 푸시 초기화/Token 업로드/클릭 이벤트에 따른 세션 리디렉션 처리 등은 Flutter Chat 모듈에서 모두 이루어졌기 때문에 Native 영역에서는 클릭 알림 이벤트의 ext만 전달하면 됩니다.

   이렇게 해야 하는 이유는 클릭 알람 이벤트가 Native에서 소비되었기 때문에 Flutter 레이어에서 직접 가져올 수 없으며 Native를 통해 포워딩해야 하기 때문입니다.

   `AppDelegate.swift` 파일에 다음 코드를 추가합니다. 특정 코드는 Demo 소스 코드를 참고하십시오.

   ![](https://qcloudimg.tencent-cloud.cn/raw/0ea48d21696a1e696ab98091983168f9.png)

   이제 iOS Native 레이어 작성을 완료했습니다.

   ### Android Native 개발

   여기서는 Kotlin을 예로 들지만 Java도 사용할 수 있습니다.

   >?
   >
   >다음 구조와 코드는 데모용이며 실제 요구 사항에 맞게 효율적으로 구성할 수 있습니다.

   #### Flutter Module 가져오기

   기존 Android 앱에 Flutter module을 추가하는 부분은 [이 부분](#android)을 참고하십시오. 방법2를 권장합니다.

   #### Android 프로젝트에서 FlutterEngine 관리

   **FlutterEngine을 관리할 싱글톤 객체를 생성합니다.**

   이 Kotlin 싱글톤 객체는 한 곳에서 Flutter Method Channel을 관리하는 데 사용되며 Flutter Module 통신 메소드를 호출하기 위해 전체 프로젝트에 메소드를 제공합니다.

   새 파일 `FlutterUtils.kt`를 생성하고 정적 객체 `FlutterUtils`를 정의합니다.

   ```kotlin
   @SuppressLint("StaticFieldLeak")
   object FlutterUtils {}
   ```

   **`FlutterEngine` (Flutter 엔진)을 생성합니다.**

   `FlutterUtils.kt` 파일에서 `FlutterEngine`을 정의하고 초기화 시 초기화합니다.

   ```kotlin
   lateinit var context : Context
   private lateinit var flutterEngine:FlutterEngine
   
   // 초기화
   flutterEngine = FlutterEngine(context)
   ```

   **Flutter 엔진을 관리하는 싱글톤 객체를 위해 추가로 개발되었습니다.**

   Demo의 기본 구현 로직은 Chat과 Call 모두의 Activity에 대한 새 네비게이터를 사용하는 것입니다.

   Chat의 Activity는 사용자가 들어가고 나가는 반면, Call의 Activity는 자동으로 들어가고 나가며, 리스너에 의해 트리거되거나 수동으로 전화를 겁니다.

   주로 다음에 초점을 맞춥니다:
   - fun init(): 각 Method Channel을 초기화하고 메소드 채널 이벤트를 등록합니다.
   - fun reportChatInfo(): Flutter 레이어를 초기화하고 Tencent Cloud IM에 로그인할 수 있도록 사용자 로그인 정보 및 SDKAPPID를 Flutter Module에 패스스루합니다.
   - fun launchChatFunc(): Flutter Module용 ViewController를 표시합니다.
   - fun triggerNotification(msg: String): iOS Native 레이어에서 받은 오프라인 푸시 메시지 클릭 이벤트와 그 안에 포함된 ext 정보를 Flutter 레이어에 바인딩된 수신 처리 이벤트에 JSON String 형태로 패스스루합니다. 예를 들어 해당 세션으로의 오프라인 푸시 클릭 리디렉션을 처리하는 데 사용됩니다.

   이 싱글톤 object에 대한 Demo 소스 코드를 참고하십시오.

   **주 게이트 `MyApplication`에서 상기 객체를 초기화합니다.**

   `MyApplication.kt` 파일에서 전역 context를 싱글톤 객체로 전송하고 초기화합니다.

   ```kotlin
   class MyApplication : MultiDexApplication() {
   
       override fun onCreate() {
           super.onCreate()
           FlutterUtils.context = this // new
           FlutterUtils.init()         // new
       }
   }
   ```

   **오프라인 푸시 클릭 이벤트 수신 및 포워딩**

   오프라인 푸시 초기화/Token 업로드/클릭 이벤트에 따른 세션 리디렉션 처리 등은 Flutter Chat 모듈에서 모두 이루어졌기 때문에 Native 영역에서는 클릭 알림 이벤트의 ext만 전달하면 됩니다.

   이렇게 해야 하는 이유는 클릭 알람 이벤트가 Native에서 소비되었기 때문에 Flutter 레이어에서 직접 가져올 수 없으며 Native를 통해 포워딩해야 하기 때문입니다.

   >! 다양한 벤더 간의 오프라인 푸시 액세스 단계가 일치하지 않기 때문에, 본문에서는 OPPO를 예로 들 뿐입니다. 전체 벤더의 액세스 솔루션은 [이 문서](https://cloud.tencent.com/document/product/269/75428)를 참고하십시오.

   Tencent Cloud IM 콘솔에 OPPO의 푸시 인증서를 추가하고 '후속 작업 클릭', `앱에서 지정된 페이지 열기`를 선택하면 `인앱 페이지`는 오프라인 푸시 정보를 처리하기 위한 페이지를 `Activity`로 구성하며, 앱의 홈 페이지로 설정하는 것이 좋습니다. 예를 들어 Demo 구성은 `com.tencent.chat.android.MainActivity`입니다.

   ![](https://qcloudimg.tencent-cloud.cn/raw/fd384ea1140199113d01a6650c0c8f3d.png)

   상기 콘솔에 대해 설정된 오프라인 푸시를 위한 Activity 파일에 다음 코드를 추가합니다.

   이 코드의 기능은 벤더가 해당 Activity를 가져올 때 Bundle에서 HashMap 형식의 ext 정보를 꺼내고 싱글톤 객체의 메소드를 트리거하고 이 정보를 Flutter에 수동으로 포워딩할 수 있습니다. 이 기능에 대한 Demo 소스 코드를 참고하십시오.

   ![](https://qcloudimg.tencent-cloud.cn/raw/2ec45c1a8b3bd952bcb86a8095f91515.png)

   이제 Android Native 레이어 작성을 완료했습니다.

   [](id:native)

   ## 추가 솔루션: Native 레이어에서 Tencent Cloud IM 초기화 및 로그인

   경우에 따라 복잡한 Chat 및 Call 페이지 없이 기존 UI에 Chat 및 Call 모듈을 통합하는 것을 선호할 수 있습니다.

   예를 들어 게임이 있고 전체 화면 채팅 페이지로 이동하지 않고도 플레이어가 경기 중에 서로 채팅할 수 있기를 바랍니다.

   즉, 사용자가 채팅 페이지로 전환하기 전에 복잡한 Flutter Module을 시작하고 싶지 않을 수 있지만 사용자가 여전히 작은 Chat 모듈에서 직접 채팅할 수 있기를 바랄 수 있습니다.

   이 경우 Native SDK로 Tencent Cloud IM을 초기화 및 로그인 메소드를 호출할 수 있으며, Tencent Cloud IM Native SDK를 직접 사용하여 필요한 빈도가 높고 간단한 시나리오에서 In-App Chat 기능을 구축할 수 있습니다.

   >?
   >그러나 필요에 따라 Flutter 내에서 초기화하고 로그인하도록 선택할 수도 있습니다. 이 프로세스는 어디서 실행하든 한 번만 실행해야 합니다.

   Flutter SDK를 사용하면 Native SDK를 통합할 수 있으므로 수동으로 Native SDK를 가져올 필요가 없습니다.

   ### Native 초기화 및 로그인

   iOS Swift 코드를 예로 들어 Native 레이어에서 초기화하고 로그인하는 방법을 보여줍니다.

   ```swift
   import ImSDK_Plus
   
   
   func initTencentChat(){
           if(isLoginSuccess == true){
               return
           }
           let data = V2TIMManager.sharedInstance().initSDK( 귀하의 SDKAPPID , config: nil);
           if (data == true){
               V2TIMManager.sharedInstance().login(
                   chatInfo.userID,
                   userSig: chatInfo.userSig,
                   succ: {
                       self.isLoginSuccess = true
                       self.reportChatInfo()
                   },
                   fail: onLoginFailed()
               )
           }
   }
   ```

   그 다음 Native SDK에서 제공하는 API를 사용하여 채팅 모듈을 기존 UI 페이지에 수동으로 구현할 수 있습니다. 자세한 내용은 [iOS 시작하기]() 또는 [Android 시작하기](https://cloud.tencent.com/document/product/269/36838)를 참고하십시오.

   ### Flutter TUIKit 초기화

   현재 사용자 정보는 `_coreInstance.setDataFromNative()`를 호출하여 Native 레이어에서 초기화 및 로그인한 후 Flutter TUIKit에 제공되어야 합니다.

   ```dart
   final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
   _coreInstance.setDataFromNative(userId: chatInfo?.userID ?? "");
   ```
   **이 모듈의 Demo 소스 코드를 참고하십시오.**

   [![](https://qcloudimg.tencent-cloud.cn/raw/9ab7dc1c98627885eea01ddfd1803bb3.png)](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Initialize%20from%20Native)

   -----

   이제 Tencent Cloud IM Flutter를 기존 애플리케이션에 추가하는 방법에 대한 소개가 끝났습니다.

   본문에서 제공된 솔루션을 기반으로 Flutter SDK와 동일한 Flutter 코드 세트를 사용하여 기존 네이티브 Android/iOS APP 개발에 Chat 및 Call 모듈 기능을 빠르게 추가할 수 있습니다.

   여전히 궁금한 점이 있으시면 언제든지 문의해 주십시오.
   - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
   - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)


   ## Reference

   1. [Integrate a Flutter module into your Android project](https://docs.flutter.dev/development/add-to-app/android/project-setup).
   2. [Integrate a Flutter module into your iOS project](https://docs.flutter.dev/development/add-to-app/ios/project-setup).
   3. [Adding a Flutter screen to an iOS app](https://docs.flutter.dev/development/add-to-app/ios/add-flutter-screen?tab=no-engine-vc-swift-tab).
   4. [Multiple Flutter screens or views](https://docs.flutter.dev/development/add-to-app/multiple-flutters).
