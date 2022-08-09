[](id:toc)
본문을 읽으면 Flutter SDK를 통합하는 방법을 알 수 있습니다.

## 환경 요건

|   | 버전 |
|---------|---------|
| Flutter | IM SDK에는 최소 Flutter 2.2.0 버전이 필요하고 TUIKit 통합 컴포넌트 라이브러리에는 최소 Flutter 2.10.0 버전이 필요합니다.|
|Android|Android Studio 3.5 및 그 이후 버전. App은 Android 4.1 및 그 이후 버전 디바이스가 필요합니다.|
|iOS|Xcode 11.0 및 그 이후 버전. 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인십시오.|

## 전제 조건

1. [Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.
2. [애플리케이션 생성 및 업그레이드](https://intl.cloud.tencent.com/document/product/1047/34577)를 참고하여 애플리케이션을 생성하고 'SDKAppID'를 기록합니다.

[](id:part1)

## 파트1: 테스트 사용자 생성

[IM 콘솔](https://console.cloud.tencent.com/im)에서 애플리케이션을 선택하고 왼쪽 사이드바에서 **보조 툴**->**UserSig Generation & Verification**을 클릭하여 두 개의 UserID와 해당 UserSig를 생성하고 `UserID`, `서명(Key)`, `UserSig`를 복사하여 이후 로그인에 사용합니다.

>? 이 계정은 개발 및 테스트 전용입니다. 애플리케이션 런칭 전에 올바른 `UserSig` 배포 방식은 서버에서 생성하여, App 지향 인터페이스를 제공하는 것입니다. `UserSig`가 필요할 때, App은 비즈니스 서버에 동적 `UserSig` 가져오기 요청을 발송합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.

![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:part2)

## 파트2: Flutter SDK 통합에 적합한 솔루션 선택


IM은 통합하는 세 가지 방법을 제공하며, 통합에 가장 적합한 솔루션을 선택할 수 있습니다.

|   | 적용 시나리오 |
|---------|---------|
| [DEMO 사용](#part3) | IM Demo는 완전한 채팅 App이며, 코드는 오픈 소스로, 채팅과 같은 시나리오를 구현해야 하는 경우 Demo를 사용하여 2차 개발을 할 수 있습니다. 바로 [Demo 체험](https://intl.cloud.tencent.com/document/product/1047/34279)할 수 있습니다. |
| [통합 (UI 포함)](#part4) | IM의 UI 컴포넌트 라이브러리 `TUIKit`은 일반 UI 컴포넌트를 제공하며, 예를 들어 대화 목록, 채팅 인터페이스 및 연락처 목록 등 개발자는 실제 비즈니스 요구에 따라 이 컴포넌트 라이브러리를 통해 사용자 정의 IM 애플리케이션을 빠르게 구축할 수 있습니다. **이 방법을 먼저 사용할 것을 권장합니다**. |
| [UI 통합 자체 구현 솔루션](#part5) | TUIKit이 애플리케이션의 인터페이스 요구 사항을 충족할 수 없거나 더 많은 사용자 정의가 필요한 경우 이 솔루션을 사용할 수 있습니다. |


IM SDK의 다양한 API에 대한 이해를 돕기 위해 각 API의 호출 및 모니터링 트리거를 설명하는 [API Example](https://github.com/TencentCloud/TIMSDK/tree/master/Flutter/IMSDK/im-flutter-plugin/tencent_im_sdk_plugin/example)도 제공합니다.


[](id:part3)

## 파트3: Demo 사용

### 데모 실행

1. Demo 소스 코드를 다운로드하고 종속을 설치합니다.
```shell
#clone 코드
git clone https://github.com/TencentCloud/TIMSDK.git

#flutter의 demo 디렉터리 입력
cd TIMSDK/Flutter/Demo/im-flutter-uikit

#종속 설치
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
1. Android Studio에서 discuss/andorid 디렉터리를 엽니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6516f9b17c58915c4ebc93c5c8829831.png)
2. Android 에뮬레이터를 실행하고 **Build And Run**을 클릭하면 Demo를 실행할 수 있습니다. 임의의 UserID(숫자, 알파벳 조합)를 입력할 수 있습니다.
>?UI에 일부 조정 업데이트가 있을 수 있으니 최신 버전을 기준으로 하십시오.
:::
::: iOS 플랫폼[](id:ios)
1. Xcode를 열고, discuss/ios/Runner.xcodeproj 파일을 엽니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6d74814ba9bce54c7439e8b3cea53e73.png)
2. iPhone을 연결하고 **Build And Run**을 클릭한 후 iOS 프로젝트 컴파일이 완료되어 Xcode 프로젝트 창이 팝업될 때까지 기다립니다.
3. iOS 프로젝트를 열고, 주 Target의 Signing & Capabilities(Apple 개발자 계정 필요)를 설정하여, iPhone 디바이스에서 프로젝트가 실행될 수 있도록 합니다.
4. 프로젝트를 실행하고, 디바이스에서 Demo 디버깅을 진행합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3fe6bbac88bb21ad7a7822bb297793b3.png)
:::
</dx-tabs>

#### Demo 코드 구조 개요

>? Demo의 UI 및 비즈니스 로직 부분은 Flutter TUIKit을 사용합니다. Demo 레이어 자체는 App을 구축하고, 내비게이션 리디렉션을 처리하고, 인스턴스화된 TUIKit의 개별 컴포넌트 호출에만 사용됩니다.


|  폴더  | 소개 |
|---------|---------|
| lib | 프로그램 코어 디렉터리 |
| lib/i18n | 국제화 관련 코드. 여기서 국제화에는 TUIKit 자체의 국제화 능력 및 국제화 표제를 포함되지 않으므로 필요에 따라 가져올 수 있습니다. |
| lib/src | 프로젝트 엔터티 디렉터리 |
| lib/src/pages | 이 Demo의 몇 가지 주요 내비게이션 페이지입니다. 프로젝트가 초기화된 후 `app.dart`는 로딩 애니메이션을 표시하고 로그인 상태를 판단하여 사용자를 `login.dart` 또는 `home_page.dart`로 이동합니다. 사용자가 로그인하면 로그인 정보가 `shared_preference` 플러그 인을 통해 로컬에 저장됩니다. 이후 애플리케이션을 실행할 때마다 원래 로그인 정보가 로컬에서 발견되면 자동으로 해당 정보를 사용하여 로그인합니다. 이 정보가 없거나 로그인에 실패하면 로그인 페이지로 이동합니다. 자동 로그인 프로세스 동안 사용자는 여전히 `app.dart`에 있고 로딩 애니메이션을 볼 수 있습니다. `home_page.dart`에는 이 Demo의 네 가지 주요 기능 페이지 전환을 지원하는 하단 Tab이 포함되어 있습니다. |
| lib/utils | 일부 툴 함수 클래스 |


기본적으로 `lib/src`의 각 dart 파일은 TUIKit 컴포넌트를 도입하고 파일에서 컴포넌트를 인스턴스화한 후 페이지를 렌더링할 수 있습니다.

주요 파일은 다음과 같습니다.


|  lib/src 주요 파일  | 파일 소개 |
|---------|---------|
| add_friend.dart | 친구 추가 신청 페이지, `TIMUIKitAddFriend` 컴포넌트 사용|
| add_group.dart | 그룹 신청 페이지, `TIMUIKitAddGroup` 컴포넌트 사용|
| blacklist.dart| 차단 리스트 페이지, `TIMUIKitBlackList` 컴포넌트 사용 |
| chat.dart | 기본 채팅 페이지, 전체 TUIKit 채팅 기능 사용, TIMUIKitChat' 컴포넌트 사용 |
| chatv2.dart | 기본 채팅 페이지, 원자화 기능 사용, `TIMUIKitChat` 컴포넌트 사용 |
| contact.dart | 연락처 페이지, `TIMUIKitContact` 컴포넌트 사용|
| conversation.dart | 대화 목록 인터페이스, `TIMUIKitConversation` 컴포넌트 사용 |
| create_group.dart | 그룹 채팅 페이지 시작, Demo 단독 구현, 컴포넌트 미사용 |
| group_application_list.dart | 그룹 신청 목록 페이지, `TIMUIKitGroupApplicationList` 컴포넌트 사용 |
| group_list.dart | 그룹 목록 페이지, `TIMUIKitGroup` 컴포넌트 사용  |
| group_profile.dart | 그룹 프로필 및 그룹 관리 페이지, `TIMUIKitGroupProfile` 컴포넌트 사용 |
| newContact.dart | 연락처 친구 신청 페이지, `TIMUIKitNewContact` 컴포넌트 사용 |
| routes.dart | Demo 경로, 로그인 페이지 `login.dart` 또는 홈 페이지 `home_page.dart`로 이동합니다. |
| search.dart | 전역 검색 및 대화 내 검색 페이지, `TIMUIKitSearch`(전역 검색) 및 `TIMUIKitSearchMsgDetail`(대화 내 검색) 컴포넌트 사용 |
| user_profile.dart | 사용자 프로필 및 관계망 유지 관리 페이지, `TIMUIKitProfile` 컴포넌트 사용|

대부분의 TUIKit 컴포넌트는 내비게이션 리디렉션 메소드가 필요하므로, Demo 레이어는 'Navigator'를 처리해야 합니다.

위의 Demo는 2차 개발을 위해 직접 수정하거나 비즈니스 요구 사항을 달성하기 위해 참고할 수 있습니다.

[](id:part4)

## 파트4: UI 포함 통합, TUIKit 컴포넌트 라이브러리를 사용, 반나절 만에 IM 기능 삽입 완료

TUIKit은 Tencent Cloud IM SDK 기반의 UI 컴포넌트 라이브러리로 대화 목록, 채팅 인터페이스, 연락처 목록과 같은 일반적인 UI 컴포넌트를 제공하며 개발자는 실제 비즈니스 요구에 따라 이 컴포넌트 라이브러리를 통해 사용자 정의 IM 애플리케이션을 빠르게 구축할 수 있습니다.[TUIKit 상세 안내](https://intl.cloud.tencent.com/document/product/1047/46576)를 참고하십시오.

### 전제 조건

Flutter 프로젝트를 생성했거나 기반으로 할 수 있는 Flutter 프로젝트가 있습니다.

### 액세스 단계

#### IM TUIkit 설치

TUIkit에는 이미 IM SDK가 포함되어 있으므로 기본 IM SDK를 설치할 필요 없이 `tim_ui_kit`만 설치하면 됩니다.

```shell
# 명령 라인에서 실행:
flutter pub add tim_ui_kit
```

#### 초기화

1. 애플리케이션이 시작되면 TUIKit을 초기화합니다.
2. 먼저 `TIMUIKitCore.getInstance()`를 실행하고, 초기화 함수 `init()`을 호출하고 `sdkAppID`를 전달합니다.
```dart
/// main.dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  @override
 void initState() {
   _coreInstance.init(
     sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
     loglevel: LogLevelEnum.V2TIM_LOG_DEBUG,
     listener: V2TimSDKListener());    
   super.initState();
 }
}
```

#### 테스트 계정에 로그인
1. 이제 처음에 콘솔에서 생성된 테스트 계정을 사용하여 로그인 인증을 완료할 수 있습니다.
2. `_coreInstance.login` 메소드를 호출하여 테스트 계정에 로그인합니다.
```dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
_coreInstance.login(userID: userID, userSig: userSig);
```

>? 이 계정은 개발 및 테스트 전용입니다. 애플리케이션 런칭 전에 올바른 `UserSig` 배포 방식은 서버에서 생성하여, App 지향 인터페이스를 제공하는 것입니다. `UserSig`가 필요할 때, App은 비즈니스 서버에 동적 `UserSig` 가져오기 요청을 발송합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.

#### 구현: 대화 목록 페이지

대화 기록이 있는 모든 사용자와 그룹 채팅 대화를 포함한 대화 목록을 IM 기능의 메인 화면으로 사용할 수 있습니다.

<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/279da6d5d41ec1ce0b0cf7fca9a697b8.jpg" />

`Conversation` 클래스를 생성하고 `body`의 'TIMUIKitConversation' 컴포넌트를 사용하여 대화 목록을 렌더링하십시오.

특정 대화 채팅 페이지로 리디렉션의 내비게이션으로 사용되는 'onTapItem' 이벤트의 처리 함수만 전달하면 됩니다. `Chat` 클래스에 대해서는 다음 단계에서 설명합니다.

```dart
import 'package:flutter/material.dart';
import 'package:tim_ui_kit/tim_ui_kit.dart';

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

#### 구현: 대화 채팅 페이지

페이지는 상단의 엔터티 채팅 기록과 하단의 전송 메시지 모듈로 구성됩니다.
<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/0c361254fa5117f7580f39e8b523e472.png" />

'Chat' 클래스를 생성하고 'body'의 'TIMUIKitChat' 컴포넌트를 사용하여 채팅 페이지를 렌더링하십시오.

연락처의 세부 정보 페이지로 리디렉션하려면 `onTapAvatar` 이벤트 처리 함수를 전달하는 것이 좋습니다. `UserProfile` 클래스는 다음 단계에서 설명합니다.

```dart
import 'package:flutter/material.dart';
import 'package:tim_ui_kit/tim_ui_kit.dart';

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

기본적으로 이 페이지는 'userID'가 하나만 전달될 때 친구 여부에 따라 사용자 세부 정보 페이지를 자동으로 생성할 수 있습니다.

`UserProfile` 클래스를 생성하고, `body`에서 `TIMUIKitProfile` 컴포넌트를 사용하여 사용자 세부 정보와 관계망 페이지를 렌더링하십시오.

>? 이 페이지를 사용자 정의하려면 'profileWidgetBuilder'를 사용하여 사용자 정의할 profile 컴포넌트를 전달하고 'profileWidgetsOrder'에 맞춰 수직 배열 순서를 정하십시오. 충족하지 않으면 `builder`를 사용하십시오.

<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/5f2e67ffb31adc738165e2c4ce58218c.jpg" />

```dart
import 'package:flutter/material.dart';
import 'package:tim_ui_kit/tim_ui_kit.dart';

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

[TIMUIKitContact](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitcontact): 연락처 목록 페이지입니다.

[TIMUIKitGroupProfile](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitgroupprofile): 그룹 프로필 페이지의 사용법은 기본적으로 'TIMUIKitProfile'과 동일합니다.

[TIMUIKitGroup](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitgroup): 그룹 목록 인터페이스입니다.

[TIMUIKitBlackList](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitblacklist): 차단 리스트 인터페이스입니다.

[TIMUIKitNewContact](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitnewcontact): 연락처(친구) 신청 목록입니다. 작은 빨간색 점을 외부에 표시하려면 `TIMUIKitUnreadCount` 작은 빨간색 점 컴포넌트를 사용하면 리스너가 자동으로 마운트됩니다.

[TIMUIKitSearch](https://pub.dev/documentation/tim_ui_kit/latest/ui_views_TIMUIKitSearch_tim_uikit_search/TIMUIKitSearch-class.html): 검색 구성 요소는 연락처/그룹/채팅 기록의 전역 검색을 지원하고, 특정 대화의 채팅 기록 검색도 지원합니다. 두 가지 모드는 `conversation` 전달 여부에 따라 다릅니다.

자세한 UI 플러그인 가이드는 [본 문서](https://intl.cloud.tencent.com/document/product/1047/46297) 또는 [플러그 인 README](https://pub.dev/packages/tim_ui_kit)를 참고하십시오.

[](id:part5)

## 파트5: 자체 구현 UI 통합

### 전제 조건

Flutter 프로젝트 생성을 완료했거나 구축할 Flutter 프로젝트가 있습니다.

### 액세스 단계

#### IM SDK 설치

[본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/46264)

다음 명령을 사용하여 최신 버전의 Flutter IM SDK를 설치하십시오.

명령 라인에서 실행:

```shell
flutter pub add tencent_im_sdk_plugin
```

#### SDK 초기화 완료

[본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/47966)

'initSDK'를 호출하여 SDK 초기화를 완료하십시오.

`sdkAppID`를 전달하십시오.

```Dart
import 'package:tencent_im_sdk_plugin/enum/V2TimSDKListener.dart';
import 'package:tencent_im_sdk_plugin/enum/log_level_enum.dart';
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';
    TencentImSDKPlugin.v2TIMManager.initSDK(
    sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
    loglevel: LogLevelEnum.V2TIM_LOG_DEBUG, // Log
    listener: V2TimSDKListener(),
  );
```

이 단계에서는 주로 네트워크 상태 및 사용자 정보 변경 등을 포함하여 IM SDK에 대한 일부 리스너를 마운트할 수 있습니다. 자세한 내용은 [V2TimSDKListener 클래스](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimSDKListener/V2TimSDKListener-class.html)를 참고하십시오.

#### 테스트 계정에 로그인

[본 섹션의 상세 문서](https://cloud.tencent.com/document/product/269/75296)

이제 처음에 콘솔에서 생성한 테스트 계정을 사용하여 로그인 인증을 완료할 수 있습니다.

'TencentImSDKPlugin.v2TIMManager.login' 메소드를 호출하여 테스트 계정에 로그인합니다.

반환값 'res.code'가 0이면 로그인이 성공한 것입니다.

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';
 V2TimCallback res = await TencentImSDKPlugin.v2TIMManager.login(
    userID: userID,
    userSig: userSig, 
  );
```

>? 이 계정은 개발 테스트 전용입니다. 애플리케이션이 런칭되기 전에 정확한 `UserSig` 발급 방식은 다음과 같습니다. `UserSig` 계산 코드를 귀하의 서버에 통합하고 App 방향의 인터페이스를 제공합니다. `UserSig`가 필요할 때 귀하의 App이 비즈니스 서버로 동적 `UserSig`를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.

#### 메시지 발송

[본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/47992)

다음은 문자 메시지 발송 예이며 프로세스는 다음과 같습니다.

1. `createTextMessage(String)`를 호출하여 문자 메시지를 생성합니다.
2. 반환 값에 따라 메시지 ID를 가져옵니다.
3. `sendMessage()`를 호출하여 해당 ID로 메시지를 발송합니다. `receiver`는 이전에 생성한 다른 테스트 계정 ID로 입력할 수 있습니다. 하나의 채팅 메시지를 발송할 때 `groupID`를 입력할 필요가 없습니다.

코드 예시:

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

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
> [이 링크를 클릭](https://console.cloud.tencent.com/im/login-message)하여, 친구 관계망 확인을 비활성화하십시오.

#### 대화 목록 가져오기

[본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/48321)

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
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

String nextSeq = "0";

getConversationList() async {
  V2TimValueCallback<V2TimConversationResult> res = await TencentImSDKPlugin
      .v2TIMManager
      .getConversationManager()
      .getConversationList(nextSeq: nextSeq, count: 10);
  
  nextSeq = res.data?.nextSeq ?? "0";
}
```

이제 이전 단계에서 다른 테스트 계정을 사용하여 보낸 메시지의 대화를 볼 수 있습니다.

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

2. 콜백 이벤트를 처리하고 최신 대화 목록을 인터페이스에 표시합니다.
```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

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
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

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
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

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

귀하는 계속해서 [그룹](https://intl.cloud.tencent.com/document/product/1047/48169), [사용자 프로필](https://intl.cloud.tencent.com/document/product/1047/48160), [관계망](https://intl.cloud.tencent.com/document/product/1047/48157), [오프라인 푸시](https://intl.cloud.tencent.com/document/product/1047/46306), [로컬 검색](https://intl.cloud.tencent.com/document/product/1047/48135) 등 관련 기능을 개발할 수 있습니다.



## FAQ

### 어떤 플랫폼이 지원됩니까?
- 현재 [IMSDK(tencent_im_sdk_plugin)](https://intl.cloud.tencent.com/document/product/1047/46264)는 iOS, Android, Web 3개의 플랫폼을 지원하고 있으며 Windows와 Mac 버전은 현재 개발 중이오니 많은 관심 부탁드립니다.
- [TUIKit](https://intl.cloud.tencent.com/document/product/1047/46576) 및 [패키지 풀버전 인터랙티브 Demo](https://github.com/TencentCloud/TIMSDK/tree/master/Flutter/Demo/im-flutter-uikit)는 iOS 및 Android 두 개의 모바일 플랫폼을 지원합니다.

### Android에서 Build And Run 클릭 후, 사용 가능한 디바이스를 찾을 수 없다는 오류가 보고되면 어떻게 해야 합니까?

디바이스가 다른 리소스에 의해 점유되어 있지 않은지 확인하거나, **Build**를 클릭하여 APK 패키지를 생성한 다음 에뮬레이터로 드래그하여 실행합니다.

### iOS 최초 실행 시 오류가 보고되면 어떻게 합니까?

설정을 실행한 후, 오류가 보고되면 **Product** > **Clean Build Folder***를 클릭하고 산출물을 지운 후 다시 `pod install` 또는 `flutter run`을 불러올 수 있습니다.

![20220714152720](https://tuikit-1251787278.cos.ap-guangzhou.myqcloud.com/20220714152720.png)

### Apple Watch 착용 시 실제 기기 디버깅 iOS 오류

![20220714152340](https://tuikit-1251787278.cos.ap-guangzhou.myqcloud.com/20220714152340.png)

Apple Watch를 비행 모드로 조정해 주시고, iPhone의 블루투스 기능을 `설정 => 블루투스`를 통해 완전히 끄십시오.

Xcode를 다시 시작하고(열린 경우), flutter run'을 다시 시작합니다.

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

## 문의하기
액세스 및 이용 중 궁금한 사항이 있으시면 QQ그룹: 788910197 추가 후 상담해 주십시오.
