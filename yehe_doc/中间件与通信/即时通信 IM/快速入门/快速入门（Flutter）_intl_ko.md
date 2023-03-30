- [](id:toc)
  본문을 읽으면 Flutter SDK를 통합하는 방법을 알 수 있습니다.

  ## 환경 요건

  | 플랫폼  | 버전                                                         |
  | ------- | ------------------------------------------------------------ |
  | Flutter | IM SDK에는 최소 Flutter 2.2.0 버전이 필요하고 TUIKit 통합 컴포넌트 라이브러리에는 최소 Flutter 2.10.0 버전이 필요합니다. |
  | Android | Android Studio 3.5 및 그 이후 버전. App은 Android 4.1 및 그 이후 버전 디바이스가 필요합니다. |
  | iOS     | Xcode 11.0 및 그 이후 버전. 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인십시오. |

  ## 플랫폼 지원

  당사는 Flutter의 모든 플랫폼을 지원하는 IM SDK 및 TUIKit을 생성하기 위해 최선을 다하고 있으며, 모든 플랫폼에서 하나의 코드 세트를 실행할 수 있도록 지원합니다.

  | 플랫폼                                                       | UI 없는 SDK ([tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk)) | UI 및 기본 비즈니스 로직이 포함된 TUIKit ([tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit)) |
  | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | iOS                                                          | 지원                                                         | 지원                                                         |
  | Android                                                      | 지원                                                         | 지원                                                         |
  | [Web](#web)                                                  | v4.1.1+2부터 지원                                            | v0.1.5부터 지원                                              |
  | [macOS](#pc)                                                 | v4.1.9부터 지원                                              | 곧 출시                                                      |
  | [Windows](#pc)                                               | v4.1.9부터 지원                                              | 곧 출시                                                      |
  | [하이브리드 개발](https://www.tencentcloud.com/document/product/1047/51456) (기존 네이티브 애플리케이션에 Flutter SDK 추가) | v5.0.0부터 지원                                              | v1.0.0부터 지원                                              |

  >? Web/macOS/Windows 플랫폼의 경우 통합을 위해 몇 가지 추가 단계가 필요합니다. 자세한 내용은 [더 많은 플랫폼으로 확장](#more)을 참고하십시오.

  ## Demo

  통합하기 전에 Tencent Cloud IM Flutter 크로스 플랫폼 SDK 및 TUIKit의 기능을 빠르게 이해하기 위해 DEMO를 사용해 볼 수 있습니다.

  **다음 DEMO는 모두 TUIKit이 도입된 동일한 Flutter 프로젝트로 패키징됩니다.** Flutter용 IM SDK는 이미 Desktop 플랫폼(macOS/Windows)을 지원하며 해당 DEMO는 곧 출시될 예정입니다.

  <table style="text-align:center; vertical-align:middle; max-width: 800px">
    <tr>
      <th style="text-align:center;">모바일 APP</th>
      <th style="text-align:center;">WEB - H5</th>
    </tr>
    <tr>
      <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">iOS/Android APP, 플랫폼에 따라 자동으로 다운로드됨<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/ca2aaff551410c74fce48008c771b9f6.png"/></div></td>
      <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">휴대폰으로 QR 코드를 스캔하여 Web DEMO 체험<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/3c79e8bb16dd0eeab35e894a690e0444.png"/></div></td>
    </tr>
  </table>

  ## 준비 작업

  1. [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.
  2. [애플리케이션 생성 및 업그레이드](https://intl.cloud.tencent.com/document/product/1047/34577)를 참고하여 애플리케이션을 생성하고 'SDKAppID'를 기록합니다.
  3. [IM 콘솔](https://console.cloud.tencent.com/im)에서 애플리케이션을 선택하고 왼쪽 사이드바에서 **보조 툴**->**UserSig Generation & Verification**을 클릭하여 두 개의 UserID와 해당 UserSig를 생성하고 `UserID`, `서명(Key)`, `UserSig`를 복사하여 이후 로그인에 사용합니다.
  ![](https://main.qcloudimg.com/raw/8315da2551bf35ec85ce10fd31fe2f52.png)

  >? 이 계정은 개발 및 테스트 전용입니다. 애플리케이션 런칭 전에 올바른 `UserSig` 배포 방식은 서버에서 생성하여, App 지향 인터페이스를 제공하는 것입니다. `UserSig`가 필요할 때, App은 비즈니스 서버에 동적 `UserSig` 가져오기 요청을 발송합니다. 자세한 내용은 [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)를 참고하십시오.

  [](id:part2)

  ## Flutter SDK 통합에 적합한 솔루션 선택

  IM은 통합하는 세 가지 방법을 제공하며, 통합에 가장 적합한 솔루션을 선택할 수 있습니다.

  | 통합 방법                          | 적용 가능한 시나리오                                         |
  | ---------------------------------- | ------------------------------------------------------------ |
  | [DEMO 수정](#part3)                | IM Demo는 완전한 채팅 App이며, 코드는 오픈 소스로, 채팅과 같은 시나리오를 구현해야 하는 경우 Demo를 사용하여 2차 개발을 할 수 있습니다. 바로 [Demo 체험](https://intl.cloud.tencent.com/document/product/1047/34279)할 수 있습니다. |
  | [통합 (UI 포함)](#part4)           | IM의 UI 컴포넌트 라이브러리 `TUIKit`은 일반 UI 컴포넌트를 제공하며, 예를 들어 대화 목록, 채팅 인터페이스 및 연락처 목록 등 개발자는 실제 비즈니스 요구에 따라 이 컴포넌트 라이브러리를 통해 사용자 정의 IM 애플리케이션을 빠르게 구축할 수 있습니다. **이 방법을 먼저 사용할 것을 권장합니다**. |
  | [UI 통합 자체 구현 솔루션](#part5) | TUIKit이 애플리케이션의 인터페이스 요구 사항을 충족할 수 없거나 더 많은 사용자 정의가 필요한 경우 이 솔루션을 사용할 수 있습니다. |

  Tencent Cloud IM SDK 내의 모든 API를 더 잘 이해할 수 있도록 개발 초기 단계에서 SDK API를 테스트하고 특정 API를 호출하기 위한 [API Example](https://github.com/TencentCloud/tc-chat-sdk-flutter/tree/main/example)를 제공합니다.

  [](id:part3)

  ## 솔루션1: Demo 수정

  ### Demo 실행

  1. Demo 소스 코드를 다운로드하고 종속을 설치합니다.
  ```shell
  # Clone the code
  git clone https://github.com/TencentCloud/tc-chat-demo-flutter.git
  
  # Install dependencies
  flutter pub get
  ```
  2. Demo 프로젝트를 실행합니다.
  ```shell
  #demo 프로젝트를 시작하고 SDK_APPID 및 KEY의 두 매개변수 교체
  flutter run --dart-define=SDK_APPID={YOUR_SDKAPPID} --dart-define=ISPRODUCT_ENV=false --dart-define=KEY={YOUR_KEY}
  ```
  >?
  >
  >- `--dart-define=SDK_APPID={YOUR_SDKAPPID}` 중 `{YOUR_SDKAPPID}`는 귀하의 애플리케이션 SDKAppID로 대체합니다.
  >- `--dart-define=ISPRODUCT_ENV=false` 개발 또는 프로덕션 환경을 판단하고 개발 환경이라면 false를 사용하십시오.
  >- `--dart-define=KEY={YOUR_KEY}` 중 `{YOUR_KEY}`는 [파트1: 테스트 사용자 생성](#part1) 의 `키(Key)` 정보로 대체합니다.
  >

  #### IDE를 사용하여 실행할 수도 있습니다: (옵션 단계)

  <dx-tabs>
  ::: Android 플랫폼[](id:android)
  1. Android Studio에 Flutter 및 Dart 플러그인을 설치합니다.
   - Mac: 플러그인 설정으로 이동하여(v3.6.3.0 이상에서 Preferences > Plugins 선택) => Flutter를 선택하고 설치 클릭 => Dart 플러그인 설치 프롬프트가 표시되면 Yes 클릭 => 다시 시작하라는 메시지가 표시되면 Restart를 클릭합니다.
   - Linux 또는 Windows: 플러그인 설정으로 이동하여(File > Settings > Plugins) = > Marketplace를 선택하고 Flutter plugin을 선택한 다음 Install을 클릭합니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/481bc19b55b40051daa8e669325cd123.png)
  2. 프로젝트를 열고 종속성을 가져옵니다.
  Android Studio에서 `im-flutter-uikit` 디렉터리를 엽니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/b22a52c14373a222f9bf55e79b04f12b.png)
  경로에서 다음 명령을 실행하여 종속성을 설치합니다.
  ```shell
  flutter pub get
  ```
  3. 환경 변수를 구성합니다.
  오른쪽 상단 모서리에서 실행 버튼 옆에 있는 `main.dart`로 마우스 hover, `Edit Configurations`를 선택합니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/e2db56849e86dab8f6f0ccb4d3374fce.png)
  팝업 창에서 환경 변수(예: SDKAppID)를 입력하여 `Additional run args`를 구성합니다. 예시:
  ```shell
  # SDK_APPID 및 KEY 매개변수 교체
  --dart-define=SDK_APPID={YOUR_SDKAPPID} --dart-define=ISPRODUCT_ENV=false --dart-define=KEY={YOUR_KEY}
  ```
  ![](https://qcloudimg.tencent-cloud.cn/raw/f022441399d2d6057b86e489593768ad.png)
  4. Android 시뮬레이터를 생성합니다.
  생성한 시뮬레이터를 실행하고 선택합니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/e3aebdd2f6018c8f1fa10d5b5fb62c79.png)
  오른쪽 상단의 Device Manager를 클릭하고 Create devices를 클릭한 다음 시뮬레이터를 생성합니다. Google FCM 푸시 기능이 필요한 경우 Google Play Store를 지원하는 기기를 설치하는 것이 좋습니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/9db005b86f9ffa1052826fe5e11d219a.png)
  5. 프로젝트를 실행합니다.
  필요에 따라 왼쪽의 Run 버튼 또는 오른쪽의 Debug 버튼을 클릭하여 프로젝트를 실행합니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/7b0d4d008f71e1d0d805c9fb3a5de437.png)
  >?UI에 일부 조정 업데이트가 있을 수 있으니 최신 버전을 기준으로 하십시오.
  >:::
  >::: iOS 플랫폼[](id:ios)

  1. Xcode에서 `im-flutter-uikit/ios` 디렉터리를 엽니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/16b555ebe0c2caa77f13ac3b42b20a24.png)
  2. iPhone을 연결하고 **Build And Run**을 클릭한 후 iOS 프로젝트 컴파일이 완료되어 Xcode 프로젝트 창이 팝업될 때까지 기다립니다.
  3. iOS 프로젝트를 열고 기본 Target이 iPhone에서 프로젝트를 실행하도록 Signing & Capabilities(Apple 개발자 계정 필요)를 설정합니다.
  4. 프로젝트를 실행하고, 디바이스에서 Demo 디버깅을 진행합니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/911935cf419e4298edb45cd93bf10852.png)
  :::
  </dx-tabs>

  #### Demo 코드 구조 개요

  >? Demo의 UI 및 비즈니스 로직 부분은 Flutter TUIKit을 사용합니다. Demo 레이어 자체는 App을 구축하고, 내비게이션 리디렉션을 처리하고, 인스턴스화된 TUIKit의 개별 컴포넌트 호출에만 사용됩니다.

  | 폴더          | 소개                                                         |
  | ------------- | ------------------------------------------------------------ |
  | lib           | 프로그램 코어 디렉터리                                       |
  | lib/i18n      | 국제화 관련 코드. 여기서 국제화에는 TUIKit 자체의 국제화 능력 및 국제화 표제를 포함되지 않으므로 필요에 따라 가져올 수 있습니다. |
  | lib/src       | 프로젝트 엔터티 디렉터리                                     |
  | lib/src/pages | 이 Demo의 몇 가지 주요 내비게이션 페이지입니다. 프로젝트가 초기화된 후 `app.dart`는 로딩 애니메이션을 표시하고 로그인 상태를 판단하여 사용자를 `login.dart` 또는 `home_page.dart`로 이동합니다. 사용자가 로그인하면 로그인 정보가 `shared_preference` 플러그 인을 통해 로컬에 저장됩니다. 이후 애플리케이션을 실행할 때마다 원래 로그인 정보가 로컬에서 발견되면 자동으로 해당 정보를 사용하여 로그인합니다. 이 정보가 없거나 로그인에 실패하면 로그인 페이지로 이동합니다. 자동 로그인 프로세스 동안 사용자는 여전히 `app.dart`에 있고 로딩 애니메이션을 볼 수 있습니다. `home_page.dart`에는 이 Demo의 네 가지 주요 기능 페이지 전환을 지원하는 하단 Tab이 포함되어 있습니다. |
  | lib/utils     | 일부 툴 함수 클래스                                          |

  기본적으로 `lib/src`의 각 dart 파일은 TUIKit 컴포넌트를 도입하고 파일에서 컴포넌트를 인스턴스화한 후 페이지를 렌더링할 수 있습니다.

  주요 파일은 다음과 같습니다.

  | lib/src 주요 파일           | 파일 소개                                                    |
  | --------------------------- | ------------------------------------------------------------ |
  | add_friend.dart             | 친구 추가 신청 페이지, `TIMUIKitAddFriend` 컴포넌트 사용     |
  | add_group.dart              | 그룹 신청 페이지, `TIMUIKitAddGroup` 컴포넌트 사용           |
  | blacklist.dart              | 차단 리스트 페이지, `TIMUIKitBlackList` 컴포넌트 사용        |
  | chat.dart                   | 기본 채팅 페이지, 전체 TUIKit 채팅 기능 사용, TIMUIKitChat' 컴포넌트 사용 |
  | chatv2.dart                 | 기본 채팅 페이지, 원자화 기능 사용, `TIMUIKitChat` 컴포넌트 사용 |
  | contact.dart                | 연락처 페이지, `TIMUIKitContact` 컴포넌트 사용               |
  | conversation.dart           | 대화 목록 인터페이스, `TIMUIKitConversation` 컴포넌트 사용   |
  | create_group.dart           | 그룹 채팅 페이지 시작, Demo 단독 구현, 컴포넌트 미사용       |
  | group_application_list.dart | 그룹 신청 목록 페이지, `TIMUIKitGroupApplicationList` 컴포넌트 사용 |
  | group_list.dart             | 그룹 목록 페이지, `TIMUIKitGroup` 컴포넌트 사용              |
  | group_profile.dart          | 그룹 프로필 및 그룹 관리 페이지, `TIMUIKitGroupProfile` 컴포넌트 사용 |
  | newContact.dart             | 연락처 친구 신청 페이지, `TIMUIKitNewContact` 컴포넌트 사용  |
  | routes.dart                 | Demo 경로, 로그인 페이지 `login.dart` 또는 홈 페이지 `home_page.dart`로 이동합니다. |
  | search.dart                 | 전역 검색 및 대화 내 검색 페이지, `TIMUIKitSearch`(전역 검색) 및 `TIMUIKitSearchMsgDetail`(대화 내 검색) 컴포넌트 사용 |
  | user_profile.dart           | 사용자 프로필 및 관계망 유지 관리 페이지, `TIMUIKitProfile` 컴포넌트 사용 |

  대부분의 TUIKit 컴포넌트는 내비게이션 리디렉션 메소드가 필요하므로, Demo 레이어는 'Navigator'를 처리해야 합니다.

  위의 Demo는 2차 개발을 위해 직접 수정하거나 비즈니스 요구 사항을 달성하기 위해 참고할 수 있습니다.

  [](id:part4)

  ## 솔루션2: UI 라이브러리 및 TUIKit 컴포넌트 라이브러리를 사용하여 반나절 만에 IM 기능 이식

  TUIKit은 Tencent Cloud IM SDK 기반의 UI 컴포넌트 라이브러리로 대화 목록, 채팅 인터페이스, 연락처 목록과 같은 일반적인 UI 컴포넌트를 제공하며 개발자는 실제 비즈니스 요구에 따라 이 컴포넌트 라이브러리를 통해 사용자 정의 IM 애플리케이션을 빠르게 구축할 수 있습니다.[TUIKit 그래픽 소개](https://intl.cloud.tencent.com/document/product/1047/50059)를 참고하십시오.

  다음은 TUIKit을 시작하는 데 도움이 되는 간단한 가이드입니다. 자세한 가이드는 [TUIKit 기본 기능 통합](https://intl.cloud.tencent.com/document/product/1047/50054)을 참고하십시오.

  ![](https://qcloudimg.tencent-cloud.cn/raw/f140dd76be01a65abfb7e6ba2bf50ed5.png)

  ### 전제 조건

  Flutter 프로젝트 생성을 완료했거나 구축할 Flutter 프로젝트가 있습니다.

  ### 액세스 단계

  #### 권한 설정

  TUIKit의 실행으로 인해 촬영/갤러리/녹음/네트워크 등의 권한이 필요하며, Native 파일에 수동으로 선언해야 관련 기능을 정상적으로 사용할 수 있습니다.

  **Android**

  `android/app/src/main/AndroidManifest.xml` 을 열고, `<manifest></manifest>`에서 다음 권한을 추가합니다.

  ```xml
      <uses-permission
          android:name="android.permission.INTERNET"/>
      <uses-permission
          android:name="android.permission.RECORD_AUDIO"/>
      <uses-permission
          android:name="android.permission.FOREGROUND_SERVICE"/>
      <uses-permission
          android:name="android.permission.ACCESS_NETWORK_STATE"/>
      <uses-permission
          android:name="android.permission.VIBRATE"/>
      <uses-permission
          android:name="android.permission.ACCESS_BACKGROUND_LOCATION"/>
      <uses-permission
          android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
      <uses-permission
          android:name="android.permission.READ_EXTERNAL_STORAGE"/>
      <uses-permission
          android:name="android.permission.CAMERA"/>
  ```

  **iOS**

  `ios/Podfile` 을 열고 파일 끝에 다음 권한 코드를 추가합니다.

  ```
  post_install do |installer|
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

  >?푸시 기능을 사용하려면 푸시 관련 권한도 추가해야 하며, 자세한 내용은 Flutter 벤더 메시지 푸시 플러그 인 통합 가이드를 참고하십시오.

  #### IM TUIkit 설치

  TUIkit에는 이미 IM SDK가 포함되어 있으므로 기본 Chat SDK를 설치할 필요 없이 `tencent_cloud_chat_uikit`만 설치하면 됩니다.

  ```shell
  # 명령 라인에서 실행:
  flutter pub add tencent_cloud_chat_uikit
  ```

  프로젝트에 Web 지원이 필요한 경우 후속 단계를 수행하기 전에 [Web 호환성 설명 섹션](#web)을 참고하여 JS 파일을 가져오십시오.

  #### 초기화 API

  1. 애플리케이션이 시작되면 TUIKit을 초기화합니다.
  2. 먼저 [`TIMUIKitCore.getInstance()`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/getInstance.html)를 실행한 다음 초기화 함수 [`init()`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/init.html)를 호출합니다. `sdkAppID`를 전달해야 합니다.
  3. API 오류 및 프롬프트를 가져오려면 onTUIKitCallbackListener 리스너를 마운트하는 것이 좋습니다. 자세한 내용은 [여기](https://intl.cloud.tencent.com/document/product/1047/50054#onTUIKitCallbackListener)를 참고하십시오.

  ```dart
  /// main.dart
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
  final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
    @override
   void initState() {
     _coreInstance.init(
       sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
       // language: LanguageEnum.en, // UI 언어. 값을 지정하지 않으면 시스템 언어가 사용됩니다
       loglevel: LogLevelEnum.V2TIM_LOG_DEBUG,
       onTUIKitCallbackListener:  (TIMCallback callbackValue){}, // [리스너 구성](https://intl.cloud.tencent.com/document/product/1047/50054#onTUIKitCallbackListener)
       listener: V2TimSDKListener());
     super.initState();
   }
  }
  ```

  >?이 단계의 await 초기화가 완료되기 전에 후속 단계를 수행하지 마십시오.

  #### 테스트 계정으로 로그인

  1. 콘솔에서 처음 생성된 테스트 계정을 사용하여 로그인 인증을 완료할 수 있습니다.
  2. [`_coreInstance.login`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/login.html) 메소드를 호출하여 테스트 계정으로 로그인합니다.

  ```dart
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
  final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  _coreInstance.login(userID: userID, userSig: userSig);
  ```

  >? 이 계정은 개발 및 테스트 전용입니다. 애플리케이션 런칭 전에 올바른 `UserSig` 배포 방식은 서버에서 생성하여, App 지향 인터페이스를 제공하는 것입니다. `UserSig`가 필요할 때, App은 비즈니스 서버에 동적 `UserSig` 가져오기 요청을 발송합니다. 자세한 내용은 [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)를 참고하십시오.

  #### 구현: 대화 목록 페이지

  대화 기록이 있는 모든 사용자와 그룹 채팅 대화를 포함한 대화 목록을 IM 기능의 메인 화면으로 사용할 수 있습니다.

  <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/279da6d5d41ec1ce0b0cf7fca9a697b8.jpg" />

  `Conversation` 클래스를 생성하고, `body`의 [`TIMUIKitConversation`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitConversation/) 컴포넌트를 사용하여 대화 목록을 렌더링합니다.

  사용자를 특정 채팅 페이지로 리디렉션하려면 `onTapItem` 이벤트 처리 함수만 전달하면 됩니다. `Chat` 클래스는 다음 단계에서 자세히 설명합니다.

  ```dart
  import 'package:flutter/material.dart';
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
  class Conversation extends StatelessWidget {
  const Conversation({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text(
        "Message",
        style: TextStyle(color: Colors.black),
      ),
    ),
    body: TIMUIKitConversation(
      onTapItem: (selectedConv) {
        Navigator.push(
            context,
            MaterialPageRoute(
              builder: (context) => Chat(
                selectedConversation: selectedConv,
              ),
            ));
      },
    ),
  );
  }
  }
  ```

  #### 구현: 채팅 페이지

  페이지는 상단의 엔터티 채팅 기록과 하단의 전송 메시지 모듈로 구성됩니다.
  <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/0c361254fa5117f7580f39e8b523e472.png" />

  `Chat` 클래스를 생성하고, `body`의 [`TIMUIKitChat`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitChat/) 컴포넌트를 사용하여 채팅 페이지를 렌더링합니다.

  연락처의 세부 정보 페이지로 리디렉션하려면 `onTapAvatar` 이벤트 처리 함수를 전달하는 것이 좋습니다. `UserProfile` 클래스는 다음 단계에서 설명합니다.

  ```dart
  import 'package:flutter/material.dart';
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
  class Chat extends StatelessWidget {
  final V2TimConversation selectedConversation;
  const Chat({Key? key, required this.selectedConversation}) : super(key: key);
  String? _getConvID() {
  return selectedConversation.type == 1
      ? selectedConversation.userID
      : selectedConversation.groupID;
  }
  @override
  Widget build(BuildContext context) {
  return TIMUIKitChat(
    conversationID: _getConvID() ?? '', // groupID or UserID
    conversationType: selectedConversation.type ?? 1, // Conversation type
    conversationShowName: selectedConversation.showName ?? "", // Conversation display name
    onTapAvatar: (_) {
          Navigator.push(
              context,
              MaterialPageRoute(
               builder: (context) => UserProfile(userID: userID),
          ));
    }, // Callback for the clicking of the message sender profile photo. This callback can be used with `TIMUIKitProfile`.
  );
  }
  ```

  #### 구현: 사용자 세부 정보 페이지

  기본적으로 이 페이지는 사용자가 친구인지 여부를 결정하고 하나의 'userID'만 전달된 후에 사용자 세부 정보 페이지를 생성합니다.

  `UserProfile` 클래스를 생성하고, `body`의 [`TIMUIKitProfile`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitProfile/) 컴포넌트를 사용하여 사용자 세부 정보 및 관계 체인 페이지를 렌더링합니다.

  >? 이 페이지를 사용자 정의하려면 먼저 [`profileWidgetBuilder`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitProfile/ProfileWidgetBuilder.html)를 사용하여 사용자 지정할 profile 컴포넌트를 전달하고 `profileWidgetsOrder`를 사용하여 수직 표시 순서를 결정하는 것을 고려하십시오. 요구 사항을 충족할 수 없는 경우 `builder`를 대신 사용하십시오.

  <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/5f2e67ffb31adc738165e2c4ce58218c.jpg" />

  ```dart
  import 'package:flutter/material.dart';
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
  class UserProfile extends StatelessWidget {
      final String userID;
      const UserProfile({required this.userID, Key? key}) : super(key: key);
  
      @override
      Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
         title: const Text(
           "Message",
           style: TextStyle(color: Colors.black),
         ),
       ),
       body: TIMUIKitProfile(
            userID: widget.userID,
       ),
      );
    }
  }
  ```

  이제 애플리케이션은 메시지 송수신을 완료하고, 친구 관계를 관리하고, 사용자 세부 정보를 표시하고, 대화 목록을 표시할 수 있습니다.

  #### 더 많은 기능

  다음 TUIKit 플러그 인을 사용하여 IM 기능을 빠르게 구현할 수 있습니다.

  - [TIMUIKitContact](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitContact/): 연락처 목록 페이지.
  - [TIMUIKitGroupProfile](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitGroupProfile/): 사용 모드가 `TIMUIKitProfile`과 기본적으로 동일한 그룹 프로필 페이지.
  - [TIMUIKitGroup](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitGroup/): 그룹 목록 페이지.
  - [TIMUIKitBlackList](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitBlackList/): 블록리스트 페이지.
  - [TIMUIKitNewContact](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitNewContact/): 연락처/친구 요청 목록. 배지를 표시하려면 리스너를 자동으로 마운트할 수 있는 `TIMUIKitUnreadCount` 배지 컴포넌트를 사용할 수 있습니다.
  - [로컬 검색](https://intl.cloud.tencent.com/document/product/1047/50036): `TIMUIKitSearch`는 연락처, 그룹 및 채팅 기록의 글로벌 검색을 지원하는 글로벌 검색 컴포넌트입니다. `TIMUIKitSearchMsgDetail`을 사용하여 특정 대화에서 채팅 기록을 검색할 수도 있습니다. 두 가지 검색 모드 중에서 선택하기 위해 `conversation`을 전달할지 여부를 선택할 수 있습니다.

  UI 컴포넌트에 대한 전체 보기는 [개요 문서](https://intl.cloud.tencent.com/document/product/1047/50059) 또는 [상세 문서](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/)를 참고하십시오.

  [](id:part5)

  ## 솔루션3: 직접 UI 구현

  ### 전제 조건

  Flutter 프로젝트 생성을 완료했거나 구축할 Flutter 프로젝트가 있습니다.

  ### 액세스 단계

  #### IM SDK 설치

  [본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/46264)

  다음 명령을 사용하여 최신 버전의 Flutter IM SDK를 설치하십시오.

  명령 라인에서 실행:

  ```shell
  flutter pub add tencent_cloud_chat_sdk
  ```

  >?
  >프로젝트를 [Web](#web) 또는 [데스크톱(macOS、Windows)](#pc) 플랫폼에도 적용해야 하는 경우 SDK 통합을 위해 몇 가지 추가 단계를 수행해야 합니다. 자세한 내용은 이 문서의 Web용 Flutter 지원 및 데스크톱용 Flutter 지원을 참고하십시오.

  #### SDK 초기화 완료

  [본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/47966)

  'initSDK'를 호출하여 SDK 초기화를 완료하십시오.

  `sdkAppID`를 전달하십시오.

  ```Dart
  import 'package:tencent_cloud_chat_sdk/enum/V2TimSDKListener.dart';
  import 'package:tencent_cloud_chat_sdk/enum/log_level_enum.dart';
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  TencentImSDKPlugin.v2TIMManager.initSDK(
    sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
    loglevel: LogLevelEnum.V2TIM_LOG_DEBUG, // Log
    listener: V2TimSDKListener(),
  );
  ```

  이 단계에서는 주로 네트워크 상태 및 사용자 정보 변경 등을 포함하여 IM SDK에 대한 일부 리스너를 마운트할 수 있습니다. 자세한 내용은 [V2TimSDKListener 클래스](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimSDKListener/V2TimSDKListener-class.html)를 참고하십시오.

  #### 테스트 계정에 로그인

  [본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/47969)

  이제 처음에 콘솔에서 생성한 테스트 계정을 사용하여 로그인 인증을 완료할 수 있습니다.

  'TencentImSDKPlugin.v2TIMManager.login' 메소드를 호출하여 테스트 계정에 로그인합니다.

  반환값 'res.code'가 0이면 로그인이 성공한 것입니다.

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  V2TimCallback res = await TencentImSDKPlugin.v2TIMManager.login(
    userID: userID,
    userSig: userSig,
  );
  ```

  >? 이 계정은 개발 테스트 전용입니다. 애플리케이션이 런칭되기 전에 정확한 `UserSig` 발급 방식은 다음과 같습니다. `UserSig` 계산 코드를 귀하의 서버에 통합하고 App 방향의 인터페이스를 제공합니다. `UserSig`가 필요할 때 귀하의 App이 비즈니스 서버로 동적 `UserSig`를 요청합니다. 자세한 내용은 [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)를 참고하십시오.

  #### 메시지 발송

  [본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/47992)

  다음은 문자 메시지 발송 예이며 프로세스는 다음과 같습니다.

  1. `createTextMessage(String)`를 호출하여 문자 메시지를 생성합니다.
  2. 반환 값에 따라 메시지 ID를 가져옵니다.
  3. `sendMessage()`를 호출하여 해당 ID로 메시지를 발송합니다. `receiver`는 이전에 생성한 다른 테스트 계정 ID로 입력할 수 있습니다. 하나의 채팅 메시지를 발송할 때 `groupID`를 입력할 필요가 없습니다.

  코드 예시:

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
  V2TimValueCallback<V2TimMsgCreateInfoResult> createMessage =
        await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .createTextMessage(text: "The text to create");
  
  String id = createMessage.data!.id!; // The message creation ID
  
  V2TimValueCallback<V2TimMessage> res = await TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .sendMessage(
            id: id, // Pass in the message creation ID to
            receiver: "The userID of the destination user",
            groupID: "The groupID of the destination group",
            );
  ```

  >?만약 sdkAppID가 낯선 사람에게 메시지를 보낼 수 없기 때문에 전송에 실패한다면, 테스트용으로 콘솔에서 활성화할 수 있습니다.
  >
  >[이 링크를 클릭](https://console.cloud.tencent.com/im/login-message)하여, 친구 관계망 확인을 비활성화하십시오.

  #### 대화 목록 가져오기

  [본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/48324)

  이전 단계에서 테스트 메시지를 보내면 다른 테스트 계정에 로그인하여 대화 목록을 가져올 수 있습니다.
  <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/e2fdd7632ebc0c5cde68c91afa914201.jpg" />

  대화 목록을 가져오는 방법은 두 가지입니다.

  1. 장기간 연결 콜백을 수신하여 대화 목록을 실시간으로 업데이트합니다.
  2. API를 요청하여 페이징에 따라 대화 목록을 한번에 가져옵니다.

  일반 응용 시나리오는 다음과 같습니다.

  응용 프로그램을 실행한 후 바로 대화 목록을 가져온 다음 장기간 연결을 수신하여 대화 목록의 변경 사항을 실시간으로 업데이트합니다.

  ##### 일회성 요청 대화 목록

  대화 목록을 가져오려면 현재 위치를 기록하고 'nextSeq'를 유지해야 합니다.

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
  String nextSeq = "0";
  
  getConversationList() async {
    V2TimValueCallback<V2TimConversationResult> res = await TencentImSDKPlugin
        .v2TIMManager
        .getConversationManager()
        .getConversationList(nextSeq: nextSeq, count: 10);
  
    nextSeq = res.data?.nextSeq ?? "0";
  }
  ```

  이때 이전 단계에서 다른 테스트 계정에서 보낸 메시지를 볼 수 있습니다.

  ##### 긴 링크에서 실시간으로 대화 목록 가져오기

  이 단계에서는 SDK에 리스너를 마운트한 다음 콜백 이벤트를 처리하고 UI를 업데이트해야 합니다.

  1. 리스너 마운트.
  ```dart
  await TencentImSDKPlugin.v2TIMManager
        .getConversationManager()
        .setConversationListener(
          listener: new V2TimConversationListener(
            onConversationChanged: (List<V2TimConversation> list){
              _onConversationListChanged(list);
      },
            onNewConversation:(List<V2TimConversation> list){
              _onConversationListChanged(list);
      },
  ```
  2. 콜백 이벤트를 처리하고 UI에 최신 대화 목록을 표시합니다.
  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
  List<V2TimConversation> _conversationList = [];
  
  _onConversationListChanged(List<V2TimConversation> list) {
    for (int element = 0; element < list.length; element++) {
      int index = _conversationList.indexWhere(
          (item) => item!.conversationID == list[element].conversationID);
      if (index > -1) {
        _conversationList.setAll(index, [list[element]]);
      } else {
        _conversationList.add(list[element]);
      }
    }
  ```

  #### 메시지 수신

  [본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/47997)

  Tencent Cloud IM Ffltter SDK를 통해 메시지를 수신하는 두 가지 방법:

  1. 장기간 연결 콜백을 수신하고, 실시간으로 메시지 변경 사항을 가져오고, 렌더링 메시지 기록 목록을 업데이트합니다.
  2. API를 요청하여 페이징에 따라 메시지 기록를 한번에 가져옵니다.

  일반 응용 시나리오는 다음과 같습니다.

  1. 인터페이스는 새로운 대화가 시작되면 먼저 일정량의 메시지 기록을 한꺼번에 요청하여 메시지 기록 목록을 보여 줍니다.
  2. 긴 링크를 수신하여 실시간으로 새로운 메시지를 수신하여 메시지 기록 목록에 추가합니다.

  ##### 일회성 요청 메시지 기록 리스트

  페이지당 풀링하는 메시지의 수는 너무 크면 안 됩니다. 그렇지 않으면 풀링 속도에 영향을 줄 수 있습니다. 약 20으로 설정하는 것이 좋습니다.

  다음 요청 시 현재 페이지 수를 동적으로 기록해야 합니다.

  예시 코드는 다음과 같습니다.

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
    V2TimValueCallback<List<V2TimMessage>> res = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .getGroupHistoryMessageList(
          groupID: "groupID",
          count: 20,
          lastMsgID: "",
        );
  
    List<V2TimMessage> msgList = res.data ?? [];
  
    // here you can use msgList to render your message list
      }
  ```

  ##### 긴 링크를 통해 실시간으로 새 메시지 가져오기

  메시지 기록 리스트가 초기화되면 `V2TimAdvancedMsgListener.onRecvNewMessage`라는 긴 링크에서 새 메시지가 나타납니다.

  `onRecvNewMessage` 콜백이 트리거된 후, 필요에 따라 새 메시지를 메시지 기록 리스트에 추가할 수 있습니다.

  바인딩 리스너의 예시 코드는 다음과 같습니다.

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
  final adVancesMsgListener = V2TimAdvancedMsgListener(
  onRecvNewMessage: (V2TimMessage newMsg) {
    _onReceiveNewMsg(newMsg);
  },
  /// ... other listeners related to message
  );
  
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: adVancesMsgListener);
  ```

  이제 IM 모듈 개발을 완료했으며, 메시지를 주고받거나 다른 대화에 들어갈 수 있습니다.

  귀하는 계속해서 [그룹](https://intl.cloud.tencent.com/document/product/1047/48169), [사용자 프로필](https://intl.cloud.tencent.com/document/product/1047/48160), [관계망](https://intl.cloud.tencent.com/document/product/1047/48157), [오프라인 푸시](https://www.tencentcloud.com/document/product/1047/46306), [로컬 검색](https://intl.cloud.tencent.com/document/product/1047/48135) 등 관련 기능을 개발할 수 있습니다.

  자세한 내용은 [통합 솔루션(UI 없음)](https://www.tencentcloud.com/document/product/1047/34299)을 참고하십시오.

  ## 고급 기능 통합

  ### 더 많은 플러그인으로 Flutter IM 경험 강화

  SDK 및 TUIKit 기본 기능 외에도 IM 기능을 강화하는 데 도움이 되는 4가지 선택적 플러그인을 제공합니다.

  - [메시지 푸시 플러그인](https://intl.cloud.tencent.com/document/product/1047/50032): 벤더의 네이티브 오프라인 푸시 기능을 지원하고 다른 비즈니스 메시지 푸시를 지원하여 메시지 도달률을 개선할 수 있습니다.
  - 통합 코드는 [Demo](https://github.com/TencentCloud/tc-chat-demo-flutter/blob/main/lib/src/pages/app.dart)를 참고하십시오.

  >?좋은 아이디어나 제안이 있으시면 언제든지 [고객센터](https://www.tencentcloud.com/contact-us)로 연락주십시오.

  [](id:more)

  ## 더 많은 플랫폼으로 확장

  Tencent Cloud IM for Flutter SDK는 기본적으로 Android / iOS 플랫폼을 지원합니다. 더 많은 플랫폼( Web/Desktop )으로 확장할 수도 있습니다.

  ### Flutter for Web 지원[](id:web)

  당사의 SDK, TUIKit(tencent_cloud_chat_uikit) 0.1.5 이상 및 no-UI SDK(tencent_cloud_chat_sdk) 4.1.1+2 이상은 Web과 완벽하게 호환됩니다.

  Web 지원을 활성화하려면 Android 및 iOS 지원을 활성화하는 단계와 비교하여 다음과 같은 추가 단계를 수행해야 합니다.

  #### Flutter 3.x로 업그레이드

  Flutter 3.x는 Web 성능에 크게 최적화되었으며 Flutter Web 프로젝트 개발에 적극 권장됩니다.

  #### Flutter for Web 플러그인 SDK 가져오기

  ```dart
  flutter pub add tencent_im_sdk_plugin_web
  ```

  #### JS 가져오기

  >?기존 Flutter 프로젝트가 Web을 지원하지 않는 경우 프로젝트의 루트 디렉터리에서 `flutter create .` 를 실행하여 Web 지원을 추가하십시오.
  >

  프로젝트의 `web/` 디렉터리로 이동하고 `npm` 또는 `yarn`을 사용하여 관련 JS 종속성을 설치합니다. 프로젝트를 초기화하려면 화면의 지시를 따르십시오.

  ```shell
  cd web
  
  npm init
  
  npm i tim-js-sdk
  
  npm i tim-upload-plugin
  ```

  `web/index.html`을 열고, `<head> </head>` JS 파일을 가져옵니다. 아래를 참고하십시오.

  ```html
  <script src="./node_modules/tim-upload-plugin/index.js"></script>
  <script src="./node_modules/tim-js-sdk/tim-js-friendship.js"></script>
  ```

  ![](https://qcloudimg.tencent-cloud.cn/raw/a4d25e02c546e0878ba59fcda87f9c76.png)

  ### Flutter for Desktop(PC) 지원[](id:pc)

  당사의 no-UI SDK(tencent_cloud_chat_sdk) 4.1.9 이상은 macOS 및 Windows 클라이언트와 완벽하게 호환됩니다. macOS 및 Windows에 대한 지원을 활성화하려면 Android 및 iOS에 대한 지원을 활성화하는 단계와 비교하여 다음 추가 단계를 수행해야 합니다.

  #### Flutter 3.x로 업그레이드

  Flutter 3.0 이상에서만 desktop 클라이언트를 지원합니다. 따라서 desktop 클라이언트를 사용해야 하는 경우 Flutter를 Flutter 3.x로 업그레이드하십시오.

  #### Flutter for Desktop 플러그인 SDK 가져오기

  ```dart
  flutter pub add tencent_im_sdk_plugin_desktop
  ```

  #### macOS 구성 수정

  `macos/Runner/DebugProfile.entitlements` 파일을 엽니다.

  `<dict></dict>`에서 다음 `key-value` 키 값 쌍을 추가합니다.

  ```
  <key>com.apple.security.app-sandbox</key>
  <false/>
  ```

  ## FAQ

  ### iOS에서 Pods 종속성 설치에 실패하면 어떻게 해야 하나요?

  #### **솔루션1:** 구성 후, 오류가 발생하면 **Product** > **Clean Build Folder**를 클릭하고 제품을 지운 후 `pod install` 또는 `flutter run`을 다시 실행하십시오.

  ![](https://qcloudimg.tencent-cloud.cn/raw/d495b2e8be86dac4b430e8f46a15cef4.png)

  #### **솔루션2:** `ios/Pods` 폴더와 `ios/Podfile.lock` 파일을 수동으로 삭제하고 다음 명령을 실행하여 종속성을 다시 설치합니다.

  1. M1과 같은 최신 Apple Silicon 칩 시리즈가 탑재된 Mac 장치.
  ![](https://qcloudimg.tencent-cloud.cn/raw/dd87d8ff05aec0ecad461f12ef6c3020.png)
  ```shell
  cd ios
  sudo arch -x86_64 gem install ffi
  arch -x86_64 pod install --repo-update
  ```
  2. 이전 버전의 Intel 칩이 탑재된 Mac 장치.
  ```shell
  cd ios
  sudo gem install ffi
  pod install --repo-update
  ```

  ### Apple Watch를 착용한 상태에서 실제 iOS 기기에서 디버깅 중 오류가 발생하면 어떻게 해야 하나요?

  ![](https://qcloudimg.tencent-cloud.cn/raw/1ffcfe39a18329c86849d7d3b34b9a0e.png)

  Apple Watch를 비행 모드로 조정해 주시고, iPhone의 `설정 => 블루투스`로 이동하여 블루투스를 끕니다.

  Xcode를 다시 시작하고(열린 경우), `flutter run`을 다시 실행합니다.

  ### Flutter 환경 문제

  Flutter 환경에 문제가 있는지 알려면 Flutter Doctor를 실행하여 Flutter 환경이 설치되어 있는지 점검하십시오.

  ### Flutter에서 자동으로 생성된 항목을 사용하여 TUIKit을 도입한 후 Android를 실행하면 오류가 보고됨

  ![](https://qcloudimg.tencent-cloud.cn/raw/d95efdd4ae50f13f38f4c383ca755ae7.png)

  1. `android\app\src\main\AndroidManifest.xml`을 열고, 다음과 같이 `xmlns:tools="http://schemas.android.com/tools"` / `android:label="@string/android_label"` 및 `tools:replace="android:label"`을 완료합니다.
  ```xml
  <manifest xmlns:android="http://schemas.android.com/apk/res/android"
      package="Android 패키지 이름으로 교체"
      xmlns:tools="http://schemas.android.com/tools">
      <application
          android:label="@string/android_label"
          tools:replace="android:label"
          android:icon="@mipmap/ic_launcher" // icon 경로 지정
          android:usesCleartextTraffic="true"
          android:requestLegacyExternalStorage="true">
  ```
  2. `android\app\build.gradle`을 열고 `defaultConfig`에서 `minSdkVersion` 및 `targetSdkVersion`을 완료합니다.
  ```gradle
  defaultConfig {
    applicationId "" // Android 패키지 이름으로 교체
    minSdkVersion 21
    targetSdkVersion 30
  }
  ```

  ### 에러 코드를 쿼리하는 방법은 무엇입니까?

  - IM SDK API 에러 코드는 [에러 코드](https://intl.cloud.tencent.com/document/product/1047/34348)를 참고하십시오.
  - TUIKit 시나리오 코드는 팝업 프롬프트에 사용되며 [onTUIKitCallbackListener](https://intl.cloud.tencent.com/document/product/1047/50054#callback) 를 수신하여 얻을 수 있습니다. 시나리오 코드 목록은 [여기](https://intl.cloud.tencent.com/document/product/1047/50054#infoCode)를 참고하십시오.
