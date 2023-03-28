## 플랫폼 지원 버전

당사는 Flutter의 모든 플랫폼을 지원하는 IM SDK 및 TUIKit을 생성하기 위해 최선을 다하고 있으며, 모든 플랫폼에서 하나의 코드 세트를 실행할 수 있도록 지원합니다.

| 플랫폼 | UI 없는 SDK ([tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk)) | UI 및 기본 비즈니스 로직이 포함된 TUIKit ([tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit)) |
|---------|---------|---------|
| iOS | 모든 버전에서 지원 | 모든 버전에서 지원 |
| Android | 모든 버전에서 지원 | 모든 버전에서 지원 |
| [Web](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.1+2 버전부터 지원                 | 0.1.5 버전부터 지원                          |
| [macOS](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.8 버전부터 지원                   | 출시 예정                                 |
| [Windows](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.8 버전부터 지원                   | 출시 예정                                 |
| [하이브리드 개발](https://tencentcloud.com/document/product/1047/51456) (기존 네이티브 애플리케이션에 Flutter SDK 추가) | 5.0.0 버전부터 지원 | 1.0.0 버전부터 지원 |

>? Web/macOS/Windows 플랫폼의 경우 통합을 위해 몇 가지 추가 단계를 수행해야 합니다. 자세한 내용은 [Flutter for Web 지원](https://intl.cloud.tencent.com/document/product/1047/45907) 및 [Flutter for Desktop(PC) 지원](https://intl.cloud.tencent.com/document/product/1047/45907)을 참고하십시오.

## SDK 설명

IM Flutter SDK(UI 없음)는 모든 IM 클라이언트 API 및 수신 콜백만 포함하는 [tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk) 패키지를 나타냅니다.

IM Flutter TUIKit(UI 포함)은 [tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit) 패키지를 말하며, 완전한 UI 컴포넌트 라이브러리와 UI SDK가 없는 비즈니스 로직을 포함합니다.

>?SDK(UI 없음)는 [tencent_im_sdk_plugin](https://pub.dev/packages/tencent_im_sdk_plugin)에서 [tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk)로 마이그레이션되었으며 TUIKit은 [tim_ui_kit](https://pub.dev/packages/tim_ui_kit)에서 [tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit)로 마이그레이션되었습니다.
> 두 개의 원본 버전 패키지는 향후 유지 관리되지 않습니다. 아직 사용 중이라면 가능한 한 빨리 최신 버전으로 업그레이드하십시오.

## 업데이트 로그

### IM Flutter TUIKit(UI 라이브러리 포함) 1.6.0 @2023.02.08

- 추가: `TIMUIKitConversationController`의 `scrollToConversation`. 이제 대화 목록에서 특정 대화로 쉽게 이동하고 탭 표시줄을 더블 클릭하여 읽지 않은 다음 대화로 이동할 수 있습니다. [Demo 소스 코드 참고](https://github.com/TencentCloud/chat-demo-flutter/blob/main/lib/src/conversation.dart).
- 최적화: 기록 메시지 목록 장시간 스크롤 성능.

### IM Flutter TUIKit(UI 라이브러리 포함) 1.5.0 @2023.02.02

- 추가: 기본 아바타 정의를 목표로 하는 글로벌 `TIMUIKitConfig`의 새로운 구성 `defaultAvatarAssetPath`.
- 추가: Flutter 3.7.0 지원.
- 수정: `chatBgColor` 구성.

### IM Flutter TUIKit(UI 라이브러리 포함) 1.4.0 @2023.01.13

- 추가: 텍스트 메시지 및 답장, 인용 텍스트 번역 기능. 문자 메시지를 길게 누르고 번역을 선택합니다. 이 기능은 `ToolTipsConfig`의 `showTranslation`으로 활성화 여부를 제어할 수 있습니다.
- 최적화: 메시지를 길게 누르면 나타나는 팝업 창 위치.
- 최적화: 키보드 팝업 이벤트.

### IM Flutter SDK(UI 없음) 5.0.8 @2023.01.13

- 추가: 그룹 계산 기능, 일반 및 라이브 그룹 그룹 카운터 meta counter 지원. 자세한 내용은 groupCounter 관련 API를 참고하십시오.

### IM Flutter TUIKit(UI 라이브러리 포함) 1.3.0 @2023.01.11

- 수정: 그룹 소유자를 이전할 때 그룹 Tips에 닉네임이나 설명이 표시되지 않는 문제.
- 최적화: 파일 열기 전 2차 확인 팝업 제거.

### IM Flutter TUIKit(UI 라이브러리 포함) 1.2.0 @2023.01.06

- 수정: TIMUIKitChat에서 녹음에서 키보드로 전환할 때 입력 영역이 표시되지 않는 문제.
- 수정: 첫 번째 수신자만 병합된 여러 전달 메시지 수신 가능.
- 최적화: `MessageItemBuilder`를 병합 메시지 화면 표시에 사용 가능.

### IM Flutter TUIKit(UI 라이브러리 포함) 1.1.0 @2022.12.27

- 추가: 기본적으로 스티커 플러그인이 TUIKit에 포함되었습니다. 이제 Unicode Emoji, 작은 이미지 Emoji 및 큰 이미지 스티커의 세 가지 유형의 스티커를 지원하며 사용이 최적화되었습니다. [이 문서](https://www.tencentcloud.com/document/product/1047/52227)를 참고하십시오.
- 최적화: 테마, 더 많은 사용자 정의 기능 지원.
- 최적화: 입력 영역, 키보드, 스티커 패널 및 기타 패널의 애니메이션.
- 최적화: Unicode 및 작은 이미지인 이모티콘을 문자 메시지의 모든 위치에 삽입 가능.
- 최적화: 프로필의 아바타를 큰 이미지로 미리보기 가능.
- 최적화: 프로필의 사용자 ID 복사 가능.
- 최적화: `TIMUIKitAddFriend`, `TIMUIKitAddGroup`, `TIMUIKitGroupProfile` 및 `TIMUIKitProfile`을 포함한 몇 가지 UI 세부 정보.
- 최적화: `TIMUIKitGroupProfile` 및 `TIMUIKitProfile`은 ID 변경 후 자동 업데이트 가능.
- 최적화: `TIMUIKitGroupChat`에서 이미지/비디오를 다운로드할 때 새로운 Loading 애니메이션 표시.
- 수정: 일부 오류.


### IM Flutter SDK(UI 없음) 5.0.6 @2022.11.29

- 수정: iOS Bundle version 손실 문제.
- 업그레이드: 기본 Native SDK 버전을 6.9.3557 버전으로 업그레이드.

### IM Flutter TUIKit(UI 라이브러리 포함) 1.0.1 @2022.11.28

- 변경: `MessageItemBuilder`에서 `groupTRTCipsItemBuilder`를 제거했습니다. 대신 `customMessageItemBuilder`를 사용하십시오.

### IM Flutter TUIKit(UI 라이브러리 포함) 1.0.0 @2022.11.23

- 추가: 기존 애플리케이션에 Flutter 모듈 추가, 즉 하이브리드 개발을 지원했습니다. 자세한 내용은 [여기](https://www.tencentcloud.com/document/product/1047/51456)를 참고하십시오.
- 추가: 사용자 정의 스티커 및 이모티콘. **사용 방법이 크게 변경되었습니다. 자세한 내용은 [Flutter](https://www.tencentcloud.com/document/product/1047/52227#.E8.A1.A8.E6.83.85.E6.8F.92.E4.BB.B6.E5.8D.87.E7.BA.A7.E6.8C.87.E5.8D.97)를 참고하십시오.**
- 추가: 기존 애플리케이션에 Flutter 모듈 추가, 하이브리드 개발 지원. 자세한 내용은 [여기](https://www.tencentcloud.com/document/product/1047/51456)를 참고하십시오.
- 추가: 사용자 정의 스티커 및 이모티콘 지원. **사용 방법이 크게 변경되었습니다. 자세한 내용은 [Flutter](https://www.tencentcloud.com/document/product/1047/52227#.E8.A1.A8.E6.83.85.E6.8F.92.E4.BB.B6.E5.8D.87.E7.BA.A7.E6.8C.87.E5.8D.97)를 참고하십시오.**
- 최적화: 특히 많은 수의 미디어 및 파일 메시지가 있는 경우 기록 메시지 목록의 로딩 시간을 최적화했습니다.
- 최적화: 더 많은 패널 영역에서 스크롤 지원.
- 최적화: 하단으로 다시 스크롤할 때 최신 메시지를 불러와 로딩이 더 원활해짐.
- 수정: Android 갤러리 이미지 수량 문제.
- 수정: 그룹 프로필 카드에서 긴 텍스트의 경계선을 넘는 문제.
- 수정: 일부 오류.

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

- 최적화: 한 번의 클릭으로 여러 파일 메시지를 선택할 수 있는 파일 일괄 다운로드 큐.
- 최적화: 자동 업데이트가 가능한 그룹 목록 위젯.
- 최적화: 저성능 장치 카메라 촬영 지원, 해상도 자동 조정.
- 최적화: 특히 `TIMUIKitChat` 컴포넌트에서 앱 바의 색상 및 텍스트 스타일 사용자 지정 지원.
- 수정: 그룹 팁에 친구 메모나 대화명이 표시되지 않는 현상.
- 수정: 비디오 재생 오류.
- 수정: 여러 문제.

### IM Flutter SDK(UI 없음) 4.1.8 @2022.10.18

- 추가: macOS 및 Windows를 포함한 PC 플랫폼에 대한 지원
- 추가: 메시지 확장
- 추가: 신호 편집기
- 최적화: 기본 SDK 업그레이드
- 수정: 높은 버전의 JDK 변환 문제
- 수정: 여러 문제

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.7 @2022.10.18

- 추가: 대형 및 RAW 이미지, 특히 최신 버전의 iOS 및 iPhone 14 Pro 시리즈에서 캡처한 이미지, 자동 전송 전에 압축 및 포맷된 이미지 지원
- 최적화: 성능 및 안정성, 특히 기록 메시지 목록 및 시작
- 최적화: 멱등성 작업으로 ‘ TIMUIKitChat ’ 초기화
- 최적화: 맨 아래로 다시 스크롤할 때 최신 뉴스 로딩
- 최적화: Flutter 2.x 및 3.x 시리즈에 대한 최적화된 지원
- 수정: iOS 갤러리에 대한 권한 지원, 일부 사진만 허용
- 수정: 여러 bug

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.5 @2022.09.22

- 추가: Web 지원. 현재 iOS/Android/Web 플랫폼에서 TUIKit 구현
- 추가: 로그인 후 디스크 스토리지 확인, `init`의 `config`에서 제어
- `TIMUIKitChatConfig`에 다음 속성 추가: `timeDividerConfig`, `notificationAndroidSound`(Huawei 및 Google 푸시 사운드 구성), `isSupportMarkdown`(텍스트 메시지가 Markdown 파싱 지원 여부) 및 `onTapLink`
- 삭제: 저작권 문제로 인해 기본 이모티콘 목록이 제거됨. [tim_ui_kit_sticker_plugin](https://pub.dev/packages/tim_ui_kit_sticker_plugin)을 통해 자신만의 이모티콘 목록을 TUIKit에 제공할 수 있습니다.
- 최적화: 대화 목록에서 @메시지 표시 비활성화 가능
- 최적화: `TIMUIKitChatConfig` 및 `MessageItemBuilder`에서 `notificationExt`/`notificationBody`의 반환값은 `null`이며, 특정 경우 필요에 따라 기본값 사용 가능. 즉, 코드에서 TUIKit와 동일한 로직을 재정의하지 않고도 자동 정의 설정 사용 여부 제어 가능
- 최적화: 여러 줄의 텍스트 메시지 지원
- 최적화: `TIMUIKitChat` 경험 개선. `TIMUIKitChatController`를 사용하기 위해서는 [튜토리얼](https://intl.cloud.tencent.com/document/product/1047/50054)에서 보여지는 것처럼 `controler`를 전달해야 합니다.

### IM Flutter SDK(UI 없음) 4.1.3 @2022.09.21

- 일부 Web 문제 해결

### IM Flutter SDK(UI 없음) 4.1.1+2 @2022.08.25

- 기본 라이브러리 버전을 6.6.x로 업그레이드
- Flutter Web에 대한 완전한 지원

### IM Flutter SDK(UI 없음) 4.1.0 @2022.08.09

- 기본 라이브러리 버전 업그레이드

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.3 @2022.08.03

- 추가된 사용자 입력 상태
- 메시지 이모티콘에 응답하는 기능 추가
- 사용자 온라인 상태 표시 추가

### IM Flutter SDK(UI 없음) 4.0.8 @2022.07.25

- 대화 유형/태그별로 세션 목록 그룹화 및 풀링을 지원하는 대화 목록 가져오기를 위한 고급 인터페이스 추가
- 사용자 정의 태그 대화 인터페이스 추가
- 대화 그룹화 기능 추가
- Dart 버전 종속성 2.0.0으로 감소
- Flutter 다중 엔진 지원
- Android에서 지원되는 오프라인 푸시 사운드 효과 구성
- 사용자 지정 사용자 온라인 상태 지원
- 기본 라이브러리 버전을 6.5.x로 업그레이드

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.2 @2022.07.08

- 기존 참조된 타사 기본 녹음 라이브러리 `flutter_record_plugin_plus`를 사용할 수 없는 문제 수정

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.1 @2022.07.07

- 최적화된 이미지 미리보기
- 각 컴포넌트에 대한 LifeCycle hooks 추가
- 그룹 채팅 페이지에 음소거 상태 추가
- 문자 메시지 및 웹사이트 정보 미리보기 카드의 URL을 클릭하여 이동하는 기능 추가
- 프롬프트가 필요한 메시지 언어를 포함한 TUIKit 레이어 전역 이벤트 콜백이 추가됨/ Flutter 레이어 오류 보고서/ IM API 레이어 오류 보고서 반환, TUIKit에서 더 이상 정보를 표시하지 않음, 콜백 및 프롬프트 언어에 따라 팝업 창을 사용자 정의할 수 있음
- 리팩토링된 `TUIKitGroupProfile` 그룹 프로필 컴포넌트 및 `TUIKitProfile` 사용자 프로필 컴포넌트를 사용하여 사용 및 초고속 액세스 간소화

### IM Flutter SDK(UI 없음) 4.0.7 @2022.07.07

- iOS에서 지원되는 사용자 지정 모서리 번호
- 그룹 적용 로직 최적화

### IM Flutter SDK(UI 없음) 4.0.6 @2022.07.04

- 기본 라이브러리 버전을 6.2.x로 업그레이드
- 오프라인 푸시 정보 필드 수정

### IM Flutter SDK(UI 없음) 4.0.5 @2022.07.01

- 사용자 온라인 상태 쿼리 추가
- 메시지 유형별 기록 메시지 목록 요청 지원
- 서식 있는 텍스트 메시지 지원

### IM Flutter TUIKit(UI 라이브러리 포함) 0.1.0 @2022.06.10

- `TIMUIKitChat` 컴포넌트의 원자 개발 기능을 추가했으며 다양한 서브 컴포넌트를 통해 채팅 페이지 직접 구성 가능.
- 메시지 수정 및 UI 업데이트 기능 지원
- 그룹 신청 승인 페이지 컴포넌트 추가
- 국제 언어에 중국어 번체 문자 추가
- 더 많은 사용자 지정 컴포넌트 매개변수 지원

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.9 @2022.05.30

- 새로 출시된 [tim_ui_kit_push_plugin](https://pub.dev/packages/tim_ui_kit_push_plugin) 푸시 플러그인으로 오프라인 푸시 지원
- Flutter 3.0 지원
- 미디어 메시지의 최적화된 로컬 미리보기

### IM Flutter SDK(UI 없음) 4.0.2 @2022.05.27

- 로컬 비디오 경로 수정

### IM Flutter SDK(UI 없음) 4.0.1 @2022.05.23

- 토픽 기능 추가
- 메시지 수정 기능 추가

### IM Flutter SDK(UI 없음) 4.0.0 @2022.04.26

- 기본 라이브러리 버전을 6.2.x로 업그레이드
- 오프라인 푸시 정보 필드 수정

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.8 @2022.04.24

- 그룹 메시지 수신 확인 기능 추가
- 채팅 영역의 오른쪽 하단 모서리에 작은 도구 모음을 추가하여 맨 아래로 돌아가기/새 메시지 수 표시/@메시지 알림 지원

### IM Flutter SDK(UI 없음) 3.9.3 @2022.04.20

- 그룹 음소거 tips boolValue 유실 문제 수정
- 현재 그룹 정보 변경 콜백에서 반환되는 데이터는 key(string)-value(string) 형식이며, key(string)-boolValue(bool) 형식이 추가됨
- 대화 인스턴스가 nameCard 필드를 적게 리졸브하는 문제 수정
- 그룹 메시지 수신 확인을 위한 API 추가
- [sendMessageReadReceptes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessageReadReceipts.html) 그룹 메시지 수신 확인 발송
- [getMessageReadReceptes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReadReceipts.html) 자신이 발송한 메시지에 대한 수신 확인 가져오기
- [getgroupMessageReadMemeberList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupMessageReadMemberList.html) 자신이 발송한 그룹 메시지의 읽은(읽지 않은) 그룹 구성원 목록 가져오기
- Flutter for Web 개선

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.7 @2022.04.13

- 경험 최적화

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.6 @2022.04.08

- 전송된 메시지를 화면에 자동으로 표시하기 위한 API 개방, 더 많은 사용자 정의 기능 매개변수 제공
- 사용자 로그인 인증 최적화
- 개인 정보 보호법에 더 잘 부합하도록 개인 정보 보호 정책 최적화

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.5 @2022.03.24

- 채팅 영역 컴포넌트 `TIMUIKitChat`의 더 많은 사용자 지정 기능 개방

### IM Flutter SDK(UI 없음) 3.9.1 @2022.03.24

- 기본 라이브러리를 v6.1.2155로 업그레이드

### IM Flutter SDK(UI 없음) 3.9.0 @2022.03.22

- 수정된 grouplistener

### IM Flutter SDK(UI 없음) 3.8.9 @2022.03.18

- 등록 결과 듣기 문제 수정

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.4 @2022.03.17

- 이미지 및 비디오 전송 지원 추가
- 테마 양식 최적화
- 검색 컴포넌트 최적화

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.3 @2022.03.14

- 컴포넌트 세부 정보 최적화
- 자동 국제화 기능 개선
- 전역 검색 컴포넌트 `TIMUIKitSearch` 추가
- 대화 내 검색 컴포넌트 `TIMUIKitSearchMsgDetail` 추가
- 친구 추가 컴포넌트 `TIMUIKitAddFriend` 추가
- 그룹 가입 컴포넌트 `TIMUIKitAddGroup` 추가
- 테마 스타일 추가

### IM Flutter SDK(UI 없음) 3.8.4 @2022.03.14

- interface 업데이트

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.2 @2022.03.02

- `TIMUIKitChat` 컴포넌트 최적화
- 중국어 간체와 영어 간의 자동 및 수동 전환 지원

### IM Flutter TUIKit(UI 라이브러리 포함) 0.0.1 @2022.03.01

- Tencent Cloud IM for Flutter(UI 라이브러리 및 비즈니스 로직 포함) 출시
- 채팅 영역/대화 목록/연락처 및 그룹 프로필/연락처 목록/블록리스트/친구 요청 목록을 포함한 처음 7개의 주요 컴포넌트 출시

### IM Flutter SDK(UI 없음) 3.8.3 @2022.03.01

- 환경에 따라 token 인코딩 형식 전환

### IM Flutter SDK(UI 없음) 3.8.2 @2022.02.21

- 그룹 구성원 매개변수 제약 조건 업데이트

### IM Flutter SDK(UI 없음) 3.8.0 @2022.02.17

- 기본 interface 종속성 업그레이드

### IM Flutter SDK(UI 없음) 3.7.8 @2022.02.15

- 강제 언래핑으로 인한 예외 수정

### IM Flutter SDK(UI 없음) 3.7.7 @2022.02.10

- Swift 코드 warning 수정
- Swift의 강제 해제 코드 재작성
- sendMessage API가 반환한 message 인스턴스에 id 필드 추가

### IM Flutter SDK(UI 없음) 3.7.5 @2022.01.23

- 기본 라이브러리를 6.0.1975로 업그레이드
- 오프라인 푸시 설정 TPNS TOKEN 지원

### IM Flutter SDK(UI 없음) 3.7.1 @2022.01.12

- 메시지 전송 진행률 이벤트의 메시지 생성 id 반환
- 콜백 부분을 최적화하여 SDK에서 catch되어 비즈니스측에서 수정해야 하는 오류를 비즈니스측에서 콜백하도록 안내

### IM Flutter SDK(UI 없음) 3.7.0 @2022.01.10

- cloudCustomData 패키지 해제 최적화

### IM Flutter SDK(UI 없음) 3.6.9 @2022.01.06

- 회신 메시지 매개변수 최적화

### IM Flutter SDK(UI 없음) 3.6.8 @2022.01.06

- 회신 메시지 인터페이스 최적화

### IM Flutter SDK(UI 없음) 3.6.7 @2022.01.05

- iOS 컴파일 환경 8.0에서 9.0으로 업그레이드

### IM Flutter SDK(UI 없음) 3.6.6 @2021.12.30

- 메시지 응답 인터페이스 추가
- Web 측에서 release mode의 오류 수정

### IM Flutter SDK(UI 없음) 3.6.5 @2021.12.17

- java 구문 오류 수정

### IM Flutter SDK(UI 없음) 3.6.4  @2021.12.17

- Android 비동기 등록 이벤트에 대한 반환이 없는 bug 수정
- 기본 리스너 이벤트 삭제 시 오류 수정
- 메시지 진행률 이벤트에 전송 중 메시지 uuid 추가

### IM Flutter SDK(UI 없음) 3.6.3 @2021.12.9

- addFriend 인터페이스 최적화: addType을 int에서 FriendTypeEnum으로 변경
- acceptFriendApplication 인터페이스 최적화: acceptType을 int에서 FriendResponseTypeEnum으로 변경
- checkFriend 인터페이스 최적화: checkType을 int에서 FriendTypeEnum으로 변경
- CreateGroup 인터페이스 최적화: addOpt을 int에서 GroupAddOptTypeEnum으로 변경
- deleteFromFriendList 인터페이스 최적화: deleteType을 int에서 FriendTypeEnum으로 변경
- getGroupMemberList 인터페이스 최적화: filter를 int에서 GroupMemberFilterTypeEnum으로 변경
- getHistoryMessageList 인터페이스 최적화: type을 int에서 HistoryMsgGetTypeEnum으로 변경
- getHistoryMessageListWithoutFormat 인터페이스 최적화: type을 int에서 HistoryMsgGetTypeEnum으로 변경
- getGroupMemberList 인터페이스 최적화: type을 int에서 GroupMemberFilterTypeEnum으로 변경
- getGroupMemberList 인터페이스 최적화: filter를 int에서 GroupMemberFilterTypeEnum으로 변경
- initSDK 인터페이스 최적화: loglevel을 int에서 LogLevelEnum으로 변경
- refuseFriendApplication 인터페이스 최적화: acceptType을 int에서 FriendApplicationTypeEnum으로 변경
- sendCustomMessage 인터페이스 최적화: priority를 int에서 MessagePriorityEnum으로 변경
- sendFaceMessage 인터페이스 최적화: priority를 int에서 MessagePriorityEnum으로 변경
- sendFileMessage 인터페이스 최적화: priority를 int에서 MessagePriorityEnum으로 변경
- sendForwardMessage 인터페이스 최적화: priority를 int에서 MessagePriorityEnum으로 변경
- sendImageMessage 인터페이스 최적화: priority를 int에서 MessagePriorityEnum으로 변경
- sendLocationMessage 인터페이스 최적화: priority를 int에서 MessagePriorityEnum으로 변경
- sendMergerMessage 인터페이스 최적화: priority를 int에서 MessagePriorityEnum으로 변경
- sendSoundMessage 인터페이스 최적화: priority를 int에서 MessagePriorityEnum으로 변경
- sendTextAtMessage 인터페이스 최적화: priority를 int에서 MessagePriorityEnum으로 변경
- sendTextMessage 인터페이스 최적화: priority를 int에서 MessagePriorityEnum으로 변경
- setGroupMemberRole 인터페이스 최적화: role을 int에서 GroupMemberRoleTypeEnum으로 변경
- 이벤트 콜백 등록 반환을 비동기화로 수정

### IM Flutter SDK(UI 없음) 3.6.2 @2021.12.9

- 고급 메시지 삭제 시 uuid 미전달 문제 수정

### IM Flutter SDK(UI 없음) 3.6.1 @2021.12.8

- 파일 진행률 이벤트 유실 수정

### IM Flutter SDK(UI 없음) 3.6.0 @2021.12.1

- 각 모듈은 listener의 다중 가입 및 다중 콜백 지원
- 모든 세션을 읽음으로 설정하는 api markAllMessageAsRead 추가
- 결합된 메시지 리졸브 추가
- native 버전을 5.8.1668로 업그레이드

### IM Flutter SDK(UI 없음) 3.5.6 @2021.11.25

- checkFriend 실패 문제 수정
- getC2CHistoryMessageList 후속 메시지 수신 불가 문제 수정

### IM Flutter SDK(UI 없음) 3.5.5 @2021.11.23

- 아키텍처 조정

### IM Flutter SDK(UI 없음) 3.5.4 @2021.11.22

- downloadMergeMesasge 인터페이스 추가

### IM Flutter SDK(UI 없음) 3.5.3 @2021.11.15

- onTotalUnreadMessageCountChanged 이벤트 추가
- 세션 정렬을 위해 V2TimConversation에 orderkey 필드 추가

### IM Flutter SDK(UI 없음) 3.5.2 @2021.11.12

add web support

### IM Flutter SDK(UI 없음) 3.5.1 @2021.11.10

- 배열 인덱스 아웃 오브 바운즈 로직 호환

### IM Flutter SDK(UI 없음) 3.5.0 @2021.10.1

- 몇 가지 알려진 문제 수정
- 새로운 인터페이스:
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

- iOS가 기존 메시지 오류를 가져오는 문제 수정

### IM Flutter SDK(UI 없음) 1.0.33 @2021.03.22

- sdk의 minSdkVersion을 16으로 수정

### IM Flutter SDK(UI 없음) 1.0.32 @2021.03.22

- 세션 정보 lastMessage가 비어 있을 때의 crash 수정

### IM Flutter SDK(UI 없음) 1.0.30-1.0.31 @2021.03.18

- 사용자 정의 메시지 data 필드가 null일 때의 crash 수정

### IM Flutter SDK(UI 없음) 1.0.29 @2021.03.16

- [중요]그룹 참석자 목록 가져오기 및 매개변수 전달 오류 수정

### IM Flutter SDK(UI 없음) 1.0.28 @2021.03.16

- [중요]CheckFriends 인터페이스 입력 매개변수 변경

### IM Flutter SDK(UI 없음) 1.0.15-1.0.27 @2021.03.15

- 그룹 참석자 사용자 정의 필드 추가
- iOS 신호 개선
- iOS 신호 bug 수정
- 사용자 정의 필드를 String으로 리졸브하여 반환
- 개인 사용자 정의 필드에 최적화된 설정
- Android getHistoryMessageList 업데이트
- Android측 매개변수 전달 checkFriend 오류 수정

### IM Flutter SDK(UI 없음) 1.0.5-1.0.14 @2021.02.26

- deleteFriendApplication 매개변수 전달 오류 수정
- native sdk를 5.1.132로 업데이트
- native sdk를 5.1.137로 업데이트
- 신호 초대 인터페이스의 매개변수 전달 bug 수정
- 신호 인터페이스 id 미반환 문제 수정
- sdk 압축 설정 수정
- 신호 콜백 bug 수정
- 사용자 정의 메시지 데이터 반환 수정
- [중요]신호 메시지의 반환 콘텐츠 형식이 수정되었으므로 신호 사용 시 버전을 업데이트 하십시오.

### IM Flutter SDK(UI 없음) 1.0.4 @2021.01.14

- Android SDK 버전을 5.1.129로 업데이트
- iOS SDK 버전을 5.1.129로 업데이트

### IM Flutter SDK(UI 없음) 1.0.3 @2021.01.13

- Android/iOS에 대한 크로스 플랫폼 지원
- 1:1 채팅 및 그룹 채팅(토론 그룹, 라이브 그룹) 세션 유형 지원
- 텍스트, 이모티콘, 이미지, 음성 및 사용자 정의 메시지 지원 추가
- APNs 오프라인 푸시 지원(token 리포트, 포그라운드/백그라운드 전환 이벤트 리포트)
- 메시지 로컬 저장 가능

### IM Flutter SDK(UI 없음) 0.0.1-1.0.2 @2020.12.01

- Flutter SDK 런칭
- 베타 테스트에 초대된 사용자
