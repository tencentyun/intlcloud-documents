## 플랫폼 지원 버전

당사는 Flutter의 모든 플랫폼을 지원하는 IM SDK 및 TUIKit을 생성하기 위해 최선을 다하고 있으며, 모든 플랫폼에서 하나의 코드 세트를 실행할 수 있도록 지원합니다.

| 플랫폼 | UI 없는 SDK ([tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk)) | UI 및 기본 비즈니스 로직이 포함된 ([tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit)) |
|---------|---------|---------|
| iOS | 모든 버전에서 지원 | 모든 버전에서 지원 |
| Android | 모든 버전에서 지원 | 모든 버전에서 지원 |
| [Web](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.1+2 버전부터 지원                 | 0.1.5 버전부터 지원                          |
| [macOS](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.8 버전부터 지원                   | 출시 예정                                 |
| [Windows](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.8 버전부터 지원                   | 출시 예정                                 |
| [하이브리드 개발](https://www.tencentcloud.com/document/product/1047/51456) (기존 네이티브 애플리케이션에 Flutter SDK 추가) | 5.0.0 버전부터 지원 | 1.0.0 버전부터 지원 |

>? Web/macOS/Windows 플랫폼에는 몇 가지 간단한 추가 단계가 필요합니다. 자세한 내용은 [Web 호환성](https://intl.cloud.tencent.com/document/product/1047/45907) 및 [Desktop 호환성](https://intl.cloud.tencent.com/document/product/1047/45907) 가이드를 참고하십시오.

## SDK 설명

IM Flutter SDK(UI 없음)는 모든 IM 클라이언트 API 및 수신 콜백만 포함하는 [tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk) 패키지를 나타냅니다.

IM Flutter TUIKit(UI 포함)은 [tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit) 패키지를 말하며, 완전한 UI 컴포넌트 라이브러리와 UI SDK가 없는 비즈니스 로직을 포함합니다.

>?SDK(UI 없음)는 [tencent_im_sdk_plugin](https://pub.dev/packages/tencent_im_sdk_plugin)에서 [tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk)로 마이그레이션되었으며 TUIKit은 [tim_ui_kit](https://pub.dev/packages/tim_ui_kit)에서 [tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit)로 마이그레이션되었습니다.
> 두 개의 원본 버전 패키지는 향후 유지 관리되지 않습니다. 아직 사용 중이라면 가능한 한 빨리 최신 버전으로 업그레이드하십시오.

## 업데이트 로그

### IM Flutter SDK(UI 없음) 5.0.6 @2022.11.29

- iOS Bundle version 손실 문제를 수정했습니다.
- 기본 Native SDK 버전을 6.9.3557로 업그레이드했습니다.

### IM Flutter TUIKit(UI 라이브러리 포함) 1.0.1 @2022.11.28

- `MessageItemBuilder`에서 `groupTRTCipsItemBuilder`를 제거했습니다. 대신 `customMessageItemBuilder`를 사용하십시오.
- `TIMUIKitConversation` 및 `TIMUIKitChat`에서 오디오/비디오 통화 기록 정보의 기본 파싱을 제거했습니다. 대신 오디오/비디오 통화 기록 정보를 수동으로 파싱하거나 통화 기록 정보 구성 요소를 전달해야 합니다. 자세한 내용은 [업그레이드 가이드](https://www.tencentcloud.com/document/product/1047/50023#updateuikit)를 참고하십시오.

### IM Flutter TUIKit(UI 라이브러리 포함) 1.0.0 @2022.11.23

- 기존 애플리케이션에 Flutter 모듈 추가, 즉 하이브리드 개발을 지원했습니다. 자세한 내용은 [여기](https://www.tencentcloud.com/document/product/1047/51456)를 참고하십시오.
- 사용자 정의 스티커 및 이모티콘 지원 추가. **사용 방법이 크게 변경되었습니다. 자세한 내용은 [여기](https://www.tencentcloud.com/document/product/1047/52227#.E8.A1.A8.E6.83.85.E6.8F.92.E4.BB.B6.E5.8D.87.E7.BA.A7.E6.8C.87.E5.8D.97)를 참고하십시오.**
- 기존 애플리케이션에 Flutter 모듈 추가, 즉 하이브리드 개발을 지원했습니다. 자세한 내용은 [여기](https://www.tencentcloud.com/document/product/1047/51456)를 참고하십시오.
- 사용자 정의 스티커 및 이모티콘 지원 추가. **사용 방법이 크게 변경되었습니다. 자세한 내용은 [Flutter](https://www.tencentcloud.com/document/product/1047/52227#.E8.A1.A8.E6.83.85.E6.8F.92.E4.BB.B6.E5.8D.87.E7.BA.A7.E6.8C.87.E5.8D.97)를 참고하십시오.**
- 특히 많은 수의 미디어 및 파일 메시지가 있는 경우 기록 메시지 목록의 로드 시간을 최적화했습니다.
- 더 많은 패널 영역에서 스크롤을 지원했습니다.
- 원활한 로딩을 위해 하단으로 다시 스크롤할 때 최신 메시지를 불러오는 기능을 최적화했습니다.
- Android 갤러리 이미지 수량 문제를 수정했습니다.
- 그룹 프로필 카드에서 긴 텍스트의 경계선을 넘는 문제를 수정했습니다.
- 수정: **음성/영상 통화 플러그인을 Calling할 때 통화 기록 정보 컴포넌트를 `TIMUIKitChat`의 `messageItemBuilder` => `customMessageItemBuilder`에 수동으로 전달해야 합니다. 자세한 내용은 [업그레이드 가이드](https://www.tencentcloud.com/document/product/1047/50023#updateuikit)를 참고하십시오.**
- 일부 오류를 수정했습니다.

>?TUIKit을 이 버전으로 업그레이드할 경우 이모티콘 부분(두 번째 업데이트 항목) 및 음성/영상 통화 부분(마지막 업데이트 항목)의 변경 사항에 특히 주의하십시오. 그렇지 않으면 관련 기능이 제대로 작동하지 않습니다.
> 수정 과정에서 궁금한 점이 있으면 언제든지 고객센터로 문의해 주십시오.

### IM Flutter SDK(UI 없음) 5.0.4 @2022.11.23

- 멀티미디어 메시지 온라인 URL은 더 이상 기본적으로 반환되지 않습니다. `getMessageOnlineUrl` API를 호출하여 가져와야 합니다.
- 멀티미디어 메시지 로컬 URL(localurl)은 더 이상 기본적으로 반환되지 않습니다. downloadMessage API를 호출하여 메시지를 성공적으로 다운로드한 후에만 반환됩니다.
- `onMessageDownloadProgressCallback` 콜백이 `advanceMessageListener`에 추가되었으며 멀티미디어 메시지 다운로드 진행률이 업데이트될 때 트리거됩니다.
- iOS 클라이언트에 `disableBadgeNumber 메소드를 추가했습니다. 메소드가 호출된 후 애플리케이션이 백그라운드로 전환될 때 애플리케이션 배지(badge)는 기본적으로 설정되지 않습니다.
- 기존 애플리케이션에 Flutter 모듈 추가, 즉 하이브리드 개발을 지원했습니다. 자세한 내용은 [여기](https://www.tencentcloud.com/document/product/1047/51456)를 참고하십시오.
- PC 클라이언트용 기본 동적 라이브러리 다운로드 로직을 최적화했습니다.
- 기본 SDK 버전을 6.8로 업그레이드했습니다.
- Web 클라이언트 기본 SDK를 재구성했습니다. [여기](https://intl.cloud.tencent.com/document/product/1047/45907)에 설명된 대로 `npm`을 통해 해당 JS를 가져와야 합니다.
- Mac 클라이언트 기본 SDK를 재구성했습니다. [여기](https://intl.cloud.tencent.com/document/product/1047/45907)에 설명된 대로 SDK를 가져와야 합니다.

>?멀티미디어 메시지 및 파일 메시지가 크게 변경되었습니다. 처음 네 가지 업데이트에 따라 이러한 메시지를 얻고 렌더링하기 위한 기존 로직을 수정하십시오. 그렇지 않으면 메시지가 표시되지 않습니다.
> 수정 과정에서 궁금한 점이 있으면 언제든지 고객센터로 문의해 주십시오.

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.8 @2022.10.21

- 사용자가 한 번의 클릭으로 여러 파일 메시지를 선택할 수 있도록 파일 일괄 다운로드 큐를 최적화했습니다.
- 자동 업데이트를 지원하도록 그룹 목록 위젯을 최적화했습니다.
- 카메라 촬영을 최적화하여 저사양 기기를 지원하고 해당 기기의 해상도를 자동으로 조정합니다.
- 특히 `TIMUIKitChat` 컴포넌트에서 앱 바의 색상 및 텍스트 스타일을 사용자 지정하기 위한 지원을 최적화했습니다.
- 그룹 팁에서 친구 메모나 대화명을 표시할 수 없던 현상이 수정되었습니다.
- 비디오 재생 오류를 수정했습니다.
- 몇 가지 문제를 수정했습니다.

### IM Flutter SDK(UI 없음) 4.1.8 @2022.10.18

- macOS 및 Windows를 포함한 PC 플랫폼에 대한 지원이 추가되었습니다
- 메시지 확장을 추가했습니다
- 신호 편집을 추가했습니다
- 기본 SDK를 업그레이드했습니다
- 높은 버전의 JDK 변환 문제를 수정했습니다
- 몇 가지 문제를 수정했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.7 @2022.10.18

- 대용량 및 RAW 이미지, 특히 최신 버전의 iOS 및 iPhone 14 Pro 시리즈에서 캡처한 이미지, 자동 전송 전에 압축 및 포맷된 이미지에 대한 지원이 추가되었습니다
- 최적화된 성능 및 안정성, 특히 기록 메시지 목록 및 시작
- 멱등성 작업으로 ‘ TIMUIKitChat ’의 초기화를 최적화했습니다
- 맨 아래로 다시 스크롤할 때 최신 메시지 로딩을 지원했습니다
- Flutter 2.x 및 3.x 시리즈에 대한 지원이 최적화되었습니다
- iOS 앨범에 대한 권한 지원: 특정 이미지만 허용합니다
- 몇 가지 bug를 수정했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.5 @2022.09.22

- Web 지원이 추가되었습니다. 이제 iOS/Android/Web 플랫폼에서 TUIKit을 구현할 수 있습니다
- `init`의 `config`에서 구성할 수 있는 로그인 후 디스크 스토리지 확인 기능을 추가했습니다
- `TIMUIKitChatConfig`에 다음 속성 추가: `timeDividerConfig`, `notificationAndroidSound`(Huawei 및 Google 푸시 사운드 구성), `isSupportMarkdown`(텍스트 메시지가 Markdown 파싱 지원 여부) 및 `onTapLink`
- 저작권 문제로 인해 기본 이모티콘 목록이 제거되었습니다. [tim_ui_kit_sticker_plugin](https://pub.dev/packages/tim_ui_kit_sticker_plugin)을 통해 자신만의 이모티콘 목록을 TUIKit에 제공할 수 있습니다.
- 최적화: 이제 대화 목록에서 @ 메시지 표시를 비활성화할 수 있습니다
- 최적화: `TIMUIKitChatConfig` 및 `MessageItemBuilder`에서 `notificationExt`/`notificationBody`의 반환값을 `null`로 설정할 수 있으며 특정 경우에는 필요에 따라 기본값을 사용할 수 있습니다. 즉, 코드에서 TUIKit과 동일한 로직을 재정의하지 않고도 사용자 지정 설정을 사용할지 여부를 제어할 수 있습니다.
- 최적화: 여러 줄의 텍스트 메시지를 지원합니다
- `TIMUIKitChat` 경험을 최적화했습니다. `TIMUIKitChatController`를 사용하려면 [Flutter](https://www.tencentcloud.com/document/product/1047/50054)에서 설명된 대로 `controler`를 전달해야 합니다.

### IM Flutter SDK(UI 없음) 4.1.3 @2022.09.21

- 일부 Web 문제를 수정했습니다

### IM Flutter SDK(UI 없음) 4.1.1+2 @2022.08.25

- 기본 라이브러리 버전을 6.6.x로 업그레이드했습니다
- Flutter Web SDK를 완벽하게 지원합니다

### IM Flutter SDK(UI 없음) 4.1.0 @2022.08.09

- 기본 라이브러리 버전을 업그레이드했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.3 @2022.08.03

- 사용자 입력 상태를 추가했습니다
- 메시지 이모티콘에 응답하는 기능을 추가했습니다
- 사용자 온라인 상태 표시를 추가했습니다

### IM Flutter SDK(UI 없음) 4.0.8 @2022.07.25

- 대화 유형/태그별로 대화 목록 가져오기를 지원하는 대화 목록 가져오기를 위한 고급 API를 추가했습니다
- 대화 표시를 사용자 지정하기 위한 API를 추가했습니다
- 대화 그룹화 기능을 추가했습니다
- 종속 Dart 버전을 2.0.0으로 낮췄습니다
- 다중 엔진 Flutter를 지원합니다
- Android에서 오프라인 푸시 사운드 효과 구성을 지원했습니다
- 사용자 지정 사용자 온라인 상태를 지원했습니다
- 기본 라이브러리 버전을 6.5.x로 업그레이드했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.2 @2022.07.08

- 원본 참조 타사 기본 녹음 라이브러리 `flutter_record_plugin_plus` 를 사용할 수 없는 문제를 수정했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.1 @2022.07.07

- 이미지 미리보기 로직을 최적화했습니다
- 각 컴포넌트에 대한 LifeCycle hooks를 추가했습니다
- 그룹 채팅 페이지에 음소거 상태를 추가했습니다
- 문자 메시지의 URL 클릭 시 리디렉션을 지원하고 웹사이트 정보 미리보기 카드를 추가했습니다
- 프롬프트가 필요한 메시지/Flutter 레이어 오류/IM API 레이어 오류에 대한 콜백을 포함하여 TUIKit 레이어 전역 이벤트 콜백을 추가했습니다. TUIKit은 더 이상 메시지 팝업을 제공하지 않습니다. 콜백 및 프롬프트를 기반으로 팝업 창을 사용자 정의할 수 있습니다.
- 그룹 프로필 컴포넌트 `TUIKitGroupProfile` 및 사용자 프로필 컴포넌트 `TUIKitProfile`을 재구성하여 사용을 단순화하고 초고속 액세스를 가능하게 합니다

### IM Flutter SDK(UI 없음) 4.0.7 @2022.07.07

- iOS에서 지원되는 사용자 지정 배지 번호입니다
- 그룹 가입 요청 로직을 최적화했습니다

### IM Flutter SDK(UI 없음) 4.0.6 @2022.07.04

- 기본 라이브러리 버전을 6.2.x로 업그레이드했습니다
- 오프라인 푸시 정보 필드를 수정했습니다

### IM Flutter SDK(UI 없음) 4.0.5 @2022.07.01

- 사용자 온라인 상태 쿼리를 추가했습니다
- 메시지 유형별로 기록 메시지 요청을 지원했습니다
- 서식 있는 텍스트 메시지 전송을 지원했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.0 @2022.06.10

- `TIMUIKitChat` 컴포넌트의 원자적 개발 기능을 추가했으며 다양한 서브 컴포넌트를 통해 직접 채팅 페이지를 구성할 수 있습니다.
- 메시지 편집 및 UI 업데이트 기능을 지원했습니다
- 그룹 가입 요청 승인 페이지 컴포넌트를 추가했습니다
- 중국어 번체를 언어 옵션으로 추가했습니다
- 더 많은 사용자 지정 컴포넌트 매개변수를 오픈했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.9 @2022.05.30

- 새로 출시된 [tim_ui_kit_push_plugin](https://pub.dev/packages/tim_ui_kit_push_plugin) 푸시 플러그인으로 오프라인 푸시를 지원했습니다
- Flutter 3.0을 지원합니다
- 미디어 메시지의 로컬 미리보기를 최적화했습니다

### IM Flutter SDK(UI 없음) 4.0.2 @2022.05.27

- 로컬 비디오 경로 문제를 수정했습니다

### IM Flutter SDK(UI 없음) 4.0.1 @2022.05.23

- 토픽 기능을 추가했습니다
- 메시지 편집 기능을 추가했습니다

### IM Flutter SDK(UI 없음) 4.0.0 @2022.04.26

- 기본 라이브러리 버전을 6.2.x로 업그레이드했습니다
- 오프라인 푸시 정보 필드를 수정했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.8 @2022.04.24

- 그룹 메시지 읽기 확인 기능을 추가했습니다
- 맨 아래로 돌아가기/새 메시지 수 표시/@메시지 알림을 지원하기 위해 채팅 영역의 오른쪽 하단에 작은 도구 모음을 추가했습니다.

### IM Flutter SDK(UI 없음) 3.9.3 @2022.04.20

- 그룹 음소거 tips의 boolValue가 유실되는 문제를 수정했습니다
- 그룹 정보 수정을 위한 콜백에 기존 key(string)-value(string)외에 key(string)-boolValue(bool) 형식을 추가했습니다
- 대화의 nameCard 필드가 인스턴스에 의해 파싱되지 않는 문제를 수정했습니다
- 그룹 메시지 수신 확인을 위한 API가 추가되었습니다
- [sendMessageReadReceptes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessageReadReceipts.html) 그룹 메시지 수신 확인을 보냅니다
- [getMessageReadReceptes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReadReceipts.html) 자신이 발송한 메시지에 대한 수신 확인을 가져옵니다
- [getgroupMessageReadMemeberList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupMessageReadMemberList.html) 자신이 발송한 그룹 메시지를 읽은(읽지 않은) 그룹 구성원 목록을 가져옵니다
- Flutter for Web이 개선되었습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.7 @2022.04.13

- 최적화된 경험입니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.6 @2022.04.08

- 전송된 메시지를 화면에 자동으로 표시하기 위한 API를 열고 더 많은 사용자 정의 기능 매개변수를 제공했습니다
- 사용자 로그인 인증이 최적화되었습니다
- 개인 정보 보호법에 더 잘 부합하도록 개인 정보 보호 정책을 최적화했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.5 @2022.03.24

- 채팅 영역 구성 요소 `TIMUIKitChat`의 더 많은 사용자 지정 기능이 지원됩니다

### IM Flutter SDK(UI 없음) 3.9.1 @2022.03.24

- 기본 라이브러리를 v6.1.2155로 업그레이드했습니다

### IM Flutter SDK(UI 없음) 3.9.0 @2022.03.22

- grouplistener가 수정되었습니다

### IM Flutter SDK(UI 없음) 3.8.9 @2022.03.18

- 등록 결과 듣기 문제를 수정했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.4 @2022.03.17

- 이미지 및 비디오 전송에 대한 지원이 추가되었습니다
- 주제 스타일이 가 최적화되었습니다
- 검색 컴포넌트가 최적화되었습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.3 @2022.03.14

- 컴포넌트 세부 정보가 최적화되었습니다
- 자동 국제화 기능을 개선했습니다
- 전역 검색 컴포넌트 `TIMUIKitSearch`를 추가했습니다
- 대화 중 검색 컴포넌트 `TIMUIKitSearchMsgDetail`을 추가했습니다
- 친구 추가 컴포넌트`TIMUIKitAddFriend`를 추가했습니다
- 그룹 가입 컴포넌트 TIMUIKitAddGroup을 추가했습니다
- 주제 스타일이 추가되었습니다

### IM Flutter SDK(UI 없음) 3.8.4 @2022.03.14

- interface를 업데이트했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.2 @2022.03.02

- `TIMUIKitChat` 컴포넌트를 최적화했습니다
- 중국어 간체와 영어 간의 자동 및 수동 전환을 지원했습니다

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.1 @2022.03.01

- Tencent Cloud IM for Flutter(UI 라이브러리 및 비즈니스 로직 포함)를 출시했습니다
- 채팅 영역/대화 목록/연락처 및 그룹 프로필/연락처 목록/블록리스트/친구 요청 목록을 포함한 처음 7개의 주요 컴포넌트를 릴리스했습니다.

### IM Flutter SDK(UI 없음) 3.8.3 @2022.03.01

- 환경에 따라 token 인코딩 형식을 전환했습니다

### IM Flutter SDK(UI 없음) 3.8.2 @2022.02.21

- 그룹 구성원 매개변수 제약 조건을 업데이트했습니다

### IM Flutter SDK(UI 없음) 3.8.0 @2022.02.17

- 기본 interface 종속성을 업그레이드했습니다

### IM Flutter SDK(UI 없음) 3.7.8 @2022.02.15

- 강제 언래핑으로 인한 예외를 수정했습니다

### IM Flutter SDK(UI 없음) 3.7.7 @2022.02.10

- Swift 코드 warning을 수정했습니다
- Swift의 강제 해제 코드를 다시 작성했습니다
- sendMessage API에서 반환된 message 인스턴스에 id 필드를 추가했습니다

### IM Flutter SDK(UI 없음) 3.7.5 @2022.01.23

- 기본 라이브러리를 6.0.1975로 업그레이드했습니다
- 오프라인 푸시 구성을 위해 TPNS TOKEN을 지원했습니다

### IM Flutter SDK(UI 없음) 3.7.1 @2022.01.12

- 메시지 전송 진행 이벤트에 메시지 생성 id를 반환하는 기능이 추가되었습니다.
- 콜백 오류가 SDK에서 catch되었으며 수정해야 함을 비즈니스 측에 상기시켜 콜백을 최적화했습니다

### IM Flutter SDK(UI 없음) 3.7.0 @2022.01.10

- cloudCustomData의 패키지 해제를 최적화했습니다

### IM Flutter SDK(UI 없음) 3.6.9 @2022.01.06

- 메시지 회신 매개변수를 최적화했습니다

### IM Flutter SDK(UI 없음) 3.6.8 @2022.01.06

- 메시지 회신 API를 최적화했습니다.

### IM Flutter SDK(UI 없음) 3.6.7 @2022.01.05

- iOS 컴파일 환경을 8.0에서 9.0으로 업그레이드했습니다

### IM Flutter SDK(UI 없음) 3.6.6 @2021.12.30

- 메시지 응답 API를 추가했습니다
- release mode에서 오류가 발생하는 Web 문제를 수정했습니다

### IM Flutter SDK(UI 없음) 3.6.5 @2021.12.17

- java의 구문 오류가 수정되었습니다

### IM Flutter SDK(UI 없음) 3.6.4  @2021.12.17

- Android 비동기 등록 이벤트에 대한 반환이 없는 bug를 수정했습니다
- 일반 수신 이벤트를 제거하면 오류가 발생하는 문제가 수정되었습니다
- 진행 이벤트에서 전송 중인 메시지의 uuid를 추가했습니다

### IM Flutter SDK(UI 없음) 3.6.3 @2021.12.9

- addFriend API 최적화: addType을 int에서 FriendTypeEnum으로 변경했습니다
- acceptFriendApplication API 최적화: acceptType을 int에서 FriendResponseTypeEnum으로 변경했습니다
- checkFriend API 최적화: checkType을 int에서 FriendTypeEnum으로 변경했습니다
- CreateGroup API 최적화: addOpt을 int에서 GroupAddOptTypeEnum으로 변경했습니다
- deleteFromFriendList API 최적화: deleteType을 int에서 FriendTypeEnum으로 변경했습니다
- getGroupMemberList API 최적화: filter를 int에서 GroupMemberFilterTypeEnum으로 변경했습니다
- getHistoryMessageList API 최적화: type을 int에서 HistoryMsgGetTypeEnum으로 변경했습니다
- getHistoryMessageListWithoutFormat API 최적화: type을 int에서 HistoryMsgGetTypeEnum으로 변경했습니다
- getGroupMemberList API 최적화: type을 int에서 GroupMemberFilterTypeEnum으로 변경했습니다
- getGroupMemberList API 최적화: filter를 int에서 GroupMemberFilterTypeEnum으로 변경했습니다
- initSDK API 최적화: loglevel을 int에서 LogLevelEnum으로 변경했습니다
- refuseFriendApplication API 최적화: acceptType을 int에서 FriendApplicationTypeEnum으로 변경했습니다
- sendCustomMessage API 최적화: priority를 int에서 MessagePriorityEnum으로 변경했습니다
- sendFaceMessage API 최적화: priority를 int에서 MessagePriorityEnum으로 변경했습니다
- sendFileMessage API 최적화: priority를 int에서 MessagePriorityEnum으로 변경했습니다
- sendForwardMessage API 최적화: priority를 int에서 MessagePriorityEnum으로 변경했습니다
- sendImageMessage API 최적화: priority를 int에서 MessagePriorityEnum으로 변경했습니다
- sendLocationMessage API 최적화: priority를 int에서 MessagePriorityEnum으로 변경했습니다
- sendMergerMessage API 최적화: priority를 int에서 MessagePriorityEnum으로 변경했습니다
- sendSoundMessage API 최적화: priority를 int에서 MessagePriorityEnum으로 변경했습니다
- sendTextAtMessage API 최적화: priority를 int에서 MessagePriorityEnum으로 변경했습니다
- sendTextMessage API 최적화: priority를 int에서 MessagePriorityEnum으로 변경했습니다
- setGroupMemberRole API 최적화: role을 int에서 GroupMemberRoleTypeEnum으로 변경했습니다
- 이벤트 콜백 모드를 비동기식으로 변경했습니다

### IM Flutter SDK(UI 없음) 3.6.2 @2021.12.9

- 고급 메시지 제거를 위해 전달된 uuid가 없는 문제를 수정했습니다

### IM Flutter SDK(UI 없음) 3.6.1 @2021.12.8

- 파일 진행 이벤트의 유실을 수정했습니다

### IM Flutter SDK(UI 없음) 3.6.0 @2021.12.1

- 모듈에서 다중 listener 등록 및 콜백에 대한 지원을 추가했습니다
- 모든 메시지를 읽음으로 표시하기 위한 markAllMessageAsRead API를 추가했습니다
- 결합된 메시지를 파싱하는 기능을 추가했습니다
- native SDK를 v5.8.1668로 업그레이드했습니다

### IM Flutter SDK(UI 없음) 3.5.6 @2021.11.25

- checkFriend 실패를 수정했습니다
- getC2CHistoryMessageList API가 후속 메시지를 가져오지 못하는 문제를 수정했습니다

### IM Flutter SDK(UI 없음) 3.5.5 @2021.11.23

- 아키텍처를 조정했습니다.

### IM Flutter SDK(UI 없음) 3.5.4 @2021.11.22

- downloadMergeMesasge API를 추가했습니다

### IM Flutter SDK(UI 없음) 3.5.3 @2021.11.15

- onTotalUnreadMessageCountChanged 이벤트를 추가했습니다
- 대화 정렬을 위해 V2TimConversation API에 orderkey 필드를 추가했습니다

### IM Flutter SDK(UI 없음) 3.5.2 @2021.11.12

add web support

### IM Flutter SDK(UI 없음) 3.5.1 @2021.11.10

- 범위를 벗어난 배열 인덱스와 호환되도록 로직을 추가했습니다

### IM Flutter SDK(UI 없음) 3.5.0 @2021.10.1

- 몇 가지 알려진 문제를 수정했습니다
- 다음 API를 추가했습니다.
- callExperimentalAPI
- clearC2CHistoryMessage
- clearGroupHistoryMessage
- searchLocalMessages
- findMessages
- searchGroups
- searchGroupMembers
- getSignalingInfo
- addInvitedSignaling
- searchFriends

### IM Flutter SDK(UI 없음) 1.0.34 @2021.03.22

- 메시지 기록을 가져올 때 오류가 발생하는 iOS 문제를 수정했습니다

### IM Flutter SDK(UI 없음) 1.0.33 @2021.03.22

- sdk의 minSdkVersion 값을 16으로 변경했습니다

### IM Flutter SDK(UI 없음) 1.0.32 @2021.03.22

- 대화 정보의 lastMessage가 비어있을 때 발생하는 crash를 수정했습니다

### IM Flutter SDK(UI 없음) 1.0.30-1.0.31 @2021.03.18

- 사용자 지정 메시지의 data 필드가 null일 때 발생하는 crash를 수정했습니다

### IM Flutter SDK(UI 없음) 1.0.29 @2021.03.16

- [중요]그룹 구성원 목록을 가져오기 위해 매개변수를 전달하면 오류가 발생하는 문제가 수정되었습니다

### IM Flutter SDK(UI 없음) 1.0.28 @2021.03.16

- [중요]CheckFriends API의 입력 매개변수가 변경되었습니다

### IM Flutter SDK(UI 없음) 1.0.15-1.0.27 @2021.03.15

- 그룹 구성원 사용자 지정 필드를 추가했습니다
- iOS 시그널링이 개선되었습니다
- iOS 시그널링 bug가 수정되었습니다
- 사용자 지정 필드를 반환하기 전에 String으로 파싱하는 기능을 추가했습니다
- 프로필의 사용자 지정 필드 설정을 최적화했습니다
- Android getHistoryMessageList API를 업데이트했습니다
- Android에서 checkFriend API에 대한 매개변수 전달 시 오류가 발생하는 문제가 수정되었습니다

### IM Flutter SDK(UI 없음) 1.0.5-1.0.14 @2021.02.26

- deleteFriendApplication API에 대한 매개변수 전달 시 오류가 발생하는 문제를 수정했습니다
- native sdk를 v5.1.132로 업데이트했습니다
- native sdk를 v5.1.137로 업데이트했습니다
- 시그널링 초대 API에 대한 매개변수를 전달할 때 발생하는 bug를 수정했습니다
- 시그널링 API가 id를 반환하지 않던 문제를 수정했습니다
- sdk 압축 구성을 수정했습니다
- 시그널링 콜백 bug를 수정했습니다
- 사용자 지정 메시지의 반환 데이터를 수정했습니다
- [중요] 시그널링 메시지에 대해 반환된 콘텐츠 형식을 수정했습니다. 시그널링을 사용하려면 이 버전 이상으로 업그레이드하십시오.

### IM Flutter SDK(UI 없음) 1.0.4 @2021.01.14

- Android용 SDK를 v5.1.129로 업그레이드했습니다
- iOS SDK용 SDK를 v5.1.129로 업그레이드했습니다

### IM Flutter SDK(UI 없음) 1.0.3 @2021.01.13

- Android/iOS 플랫폼에 대한 지원이 추가되었습니다
- 1:1 채팅 및 그룹 채팅(토론 및 오디오-비디오 그룹)에 대한 지원이 추가되었습니다
- 텍스트, 이모티콘, 이미지, 오디오 및 사용자 지정 메시지에 대한 지원이 추가되었습니다
- APNs 오프라인 푸시(token 및 포그라운드/백그라운드 전환 보고)에 대한 지원이 추가되었습니다.
- 메시지를 로컬에 저장하는 기능을 추가했습니다

### IM Flutter SDK(UI 없음) 0.0.1-1.0.2 @2020.12.01

- Flutter용 SDK를 런칭했습니다
- 사용자를 베타 테스트에 초대했습니다

