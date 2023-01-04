## 플랫폼 지원 버전

당사는 Flutter의 모든 플랫폼을 지원하는 IM SDK 및 TUIKit을 생성하기 위해 최선을 다하고 있으며, 모든 플랫폼에서 하나의 코드 세트를 실행할 수 있도록 지원합니다.

| 플랫폼                                                         | UI SDK 없음 (tencent_im_sdk_plugin) | UI 및 기본 비즈니스 로직 TUIKit 포함 (tim_ui_kit) |
| ------------------------------------------------------------ | --------------------------------- | ---------------------------------------- |
| iOS                                                          | 모든 버전 지원                      | 모든 버전 지원                             |
| Android                                                      | 모든 버전 지원                      | 모든 버전 지원                             |
| [Web](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.1+2 버전부터 지원                 | 0.1.5 버전부터 지원                          |
| [macOS](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.8 버전부터 지원                   | 출시 예정                                 |
| [Windows](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.8 버전부터 지원                   | 출시 예정                                 |

>? Web/macOS/Windows 플랫폼에는 몇 가지 간단한 추가 단계가 필요합니다. 자세한 내용은 [Web 호환성](https://intl.cloud.tencent.com/document/product/1047/45907) 및 [Desktop 호환성](https://intl.cloud.tencent.com/document/product/1047/45907) 가이드를 참고하십시오.

## 업데이트 로그
>?
>
>- IM Flutter SDK(UI 없음)는 모든 IM 클라이언트 API 및 수신 콜백만 포함하는 [tencent_im_sdk_plugin](https://pub.dev/packages/tencent_im_sdk_plugin) 패키지를 나타냅니다.
>- IM Flutter TUIKit(UI 포함)은 [tim_ui_kit](https://pub.dev/packages/tim_ui_kit) 패키지를 말하며, 완전한 UI 컴포넌트 라이브러리와 UI SDK가 없는 비즈니스 로직을 포함합니다.

## IM Flutter TUIKit 0.1.8 @2022.10.21

- 최적화: 한 번의 클릭으로 여러 파일 메시지를 선택할 수 있는 파일 일괄 다운로드 대기열.
- 최적화: 자동으로 업데이트될 수 있는 그룹 목록 위젯.
- 최적화: 카메라 촬영이 저성능 장치를 지원하고 자동으로 해상도를 조정.
- 최적화: 특히 TIMUIKitChat 컴포넌트에서 앱 바의 색상 및 텍스트 스타일을 사용자 지정하기 위한 지원.
- 수정: 그룹 팁에 친구 메모나 대화명이 표시되지 않던 현상.
- 수정: 비디오 재생 오류.
- 수정: 여러 문제.

## IM Flutter SDK 4.1.8 @2022.10.18
- 추가: macOS 및 Windows를 포함한 PC 플랫폼에 대한 지원
- 추가: 메시지 확장
- 추가: 신호 편집기
- 최적화: 기본 SDK 업그레이드
- 수정: 높은 버전의 JDK 변환 문제
- 수정: 여러 문제

## IM Flutter TUIKit 0.1.7 @2022.10.18
- 추가: 대형 및 RAW 이미지, 특히 최신 버전의 iOS 및 iPhone 14 Pro 시리즈에서 캡처한 이미지, 자동 전송 전에 압축 및 포맷된 이미지 지원
- 최적화: 성능 및 안정성, 특히 기록 메시지 목록 및 시작
- 최적화: 멱등성 작업으로 ‘ TIMUIKitChat ’ 초기화
- 최적화: 맨 아래로 다시 스크롤할 때 최신 뉴스 로딩
- 최적화: Flutter 2.x 및 3.x 시리즈에 대한 최적화된 지원
- 수정: iOS 갤러리에 대한 권한 지원, 일부 사진만 허용
- 수정: 여러 bug

## IM Flutter TUIKit 0.1.5 @2022.09.22
- 추가: Web 지원. 현재 iOS/Android/Web 플랫폼에서 TUIKit 구현
- 추가: 로그인 후 디스크 스토리지 확인, `init`의 `config`에서 제어
- 추가: `TIMUIKitChatConfig`에 추가: `timeDividerConfig`, `notificationAndroidSound` Huawei Google 푸시 사운드 구성, `isSupportMarkdown` 텍스트 메시지가 Markdown 파싱 지원 여부, `onTapLink`
- 제거: 저작권 문제로 인한 기본 Emoji 목록, [tim_ui_kit_sticker_plugin](https://pub.dev/packages/tim_ui_kit_sticker_plugin)을 통해 자신만의 이모티콘 목록을 TUIKit에 제공
- 최적화: 대화 목록에서 @메시지 표시 비활성화
- 최적화: `TIMUIKitChatConfig` 및 `MessageItemBuilder`에서 `notificationExt/notificationBody`의 반환값은 `null`이며, 특정 경우 필요에 따라 기본값 사용 가능. 즉, 코드에서 TUIKit와 동일한 로직을 재정의하지 않고도 자동 정의 설정을 사용할지 여부를 제어할 수 있음
- 최적화: 여러 줄의 텍스트 메시지 지원
- 최적화: `TIMUIKitChat` 경험 개선. `TIMUIKitChatController`를 사용하기 위해서는 [튜토리얼](https://www.tencentcloud.com/document/product/1047/50054)에서 보여지는 것처럼 `controler`를 전달해야 함.

## IM Flutter SDK 4.1.3 @2022.09.21
- 일부 Web 문제 해결

## IM Flutter SDK 4.1.1+2 @2022.08.25
- 기본 라이브러리 버전을 6.6.x로 업그레이드
- Flutter Web에 대한 완전한 지원

## IM Flutter SDK 4.1.0 @2022.08.09
- 기본 라이브러리 버전 업그레이드

## IM Flutter TUIKit 0.1.3 @2022.08.03
- 추가된 사용자 입력 상태
- 메시지 이모티콘에 응답하는 기능 추가
- 사용자 온라인 상태 표시 추가

## IM Flutter SDK 4.0.8 @2022.07.25
- 대화 유형/태그별로 세션 목록 그룹화 및 풀링을 지원하는 대화 목록 가져오기를 위한 고급 인터페이스 추가
- 사용자 정의 태그 대화 인터페이스 추가
- 대화 그룹화 기능 추가
- Dart 버전 종속성 2.0.0으로 감소
- Flutter 다중 엔진 지원
- Android에서 지원되는 오프라인 푸시 사운드 효과 구성
- 사용자 지정 사용자 온라인 상태 지원
- 기본 라이브러리 버전을 6.5.x로 업그레이드

## IM Flutter TUIKit 0.1.2 @2022.07.08
- 원래 참조된 타사 기본 녹음 라이브러리 `flutter_record_plugin_plus` 를 사용할 수 없는 문제 수정

## IM Flutter TUIKit 0.1.1 @2022.07.07
- 최적화된 이미지 미리보기
- 각 컴포넌트에 대한 LifeCycle hooks 추가
- 그룹 채팅 페이지에 음소거 상태 추가
- 문자 메시지 및 웹사이트 정보 미리보기 카드의 URL을 클릭하여 이동하는 기능 추가
- 프롬프트가 필요한 메시지 언어를 포함한 TUIKit 레이어 전역 이벤트 콜백이 추가됨/ Flutter 레이어 오류 보고서/ IM API 레이어 오류 보고서 반환, TUIKit에서 더 이상 정보를 표시하지 않음, 콜백 및 프롬프트 언어에 따라 팝업 창을 사용자 정의할 수 있음
- 리팩토링된 `TUIKitGroupProfile` 그룹 프로필 컴포넌트 및 `TUIKitProfile` 사용자 프로필 컴포넌트를 사용하여 사용 및 초고속 액세스 간소화

## IM Flutter SDK 4.0.7 @2022.07.07
- iOS에서 지원되는 사용자 지정 모서리 번호
- 그룹 적용 로직 최적화

## IM Flutter SDK 4.0.6 @2022.07.04
- 기본 라이브러리 버전을 6.2.x로 업그레이드
- 오프라인 푸시 정보 필드 수정

## IM Flutter SDK 4.0.5 @2022.07.01
- 사용자 온라인 상태 쿼리 추가
- 메시지 유형별 기록 메시지 목록 요청 지원
- 서식 있는 텍스트 메시지 지원

## IM Flutter TUIKit 0.1.0 @2022.06.10
- `TIMUIKitChat` 컴포넌트의 원자 개발 기능을 추가했으며 다양한 서브 컴포넌트를 통해 채팅 페이지 직접 구성 가능.
- 메시지 수정 및 UI 업데이트 기능 지원
- 그룹 신청 승인 페이지 컴포넌트 추가
- 국제 언어에 중국어 번체 문자 추가
- 더 많은 사용자 지정 컴포넌트 매개변수 지원

## IM Flutter TUIKit 0.0.9 @2022.05.30
- 새로 출시된 [tim_ui_kit_push_plugin](https://pub.dev/packages/tim_ui_kit_push_plugin) 푸시 플러그인으로 오프라인 푸시 지원
- Flutter 3.0 지원
- 미디어 메시지의 최적화된 로컬 미리보기

## IM Flutter SDK 4.0.2 @2022.05.27
- 로컬 비디오 경로 수정

## IM Flutter SDK 4.0.1 @2022.05.23
- 토픽 기능 추가
- 메시지 수정 기능 추가

## IM Flutter SDK 4.0.0 @2022.04.26
- 기본 라이브러리 버전을 6.2.x로 업그레이드
- 오프라인 푸시 정보 필드 수정

## IM Flutter TUIKit 0.0.8 @2022.04.24
- 그룹 메시지 수신 확인 기능 추가
- 채팅 영역의 오른쪽 하단 모서리에 작은 도구 모음을 추가하여 맨 아래로 돌아가기/새 메시지 수 표시/@메시지 알림 지원

## IM Flutter SDK 3.9.3 @2022.4.20
- 그룹 음소거 tips boolValue 유실 문제 수정
 - 현재 그룹 정보 변경 콜백에서 반환되는 데이터는 key(string)-value(string) 형식이며, key(string)-boolValue(bool) 형식이 추가됨
- 대화 인스턴스가 nameCard 필드를 적게 리졸브하는 문제 수정
- 그룹 메시지 수신 확인을 위한 API 추가
 - [sendMessageReadReceptes](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessageReadReceipts.html) 그룹 메시지 수신 확인 발송
 - [getMessageReadReceptes](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReadReceipts.html) 자신이 발송한 메시지에 대한 수신 확인 가져오기
 - [getgroupMessageReadMemeberList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupMessageReadMemberList.html) 자신이 발송한 그룹 메시지의 읽은(읽지 않은) 그룹 구성원 목록 가져오기
- Flutter for Web 개선

## IM Flutter SDK 3.9.1 @2022.3.24
- 기본 라이브러리를 v6.1.2155로 업그레이드

## IM Flutter SDK 3.9.0 @2022.3.22
- 수정된 grouplistener

## IM Flutter SDK 3.8.9 @2022.3.18
- 등록 결과 듣기 문제 수정

## IM Flutter SDK 3.8.4 @2022.3.14
- 업데이트된 interface

## IM Flutter SDK 3.8.3 @2022.3.1
- 환경에 따라 token 인코딩 형식 전환

## IM Flutter SDK 3.8.2 @2022.2.21
- 업데이트된 그룹 구성원 매개변수 제약 조건

## IM Flutter SDK 3.8.0 @2022.2.17
- 기본 interface 종속성 업그레이드

## IM Flutter SDK 3.7.8 @2022.2.15
- 강제 언래핑으로 인한 예외 수정

## IM Flutter SDK 3.7.7 @2022.2.10
- Swift 코드 warning 수정
- Swift의 강제 해제 코드 재작성
- sendMessage API가 반환한 message 인스턴스에 id 필드 추가


## IM Flutter SDK 3.7.5 @2022.01.23
- 기본 라이브러리를 6.0.1975로 업그레이드
- 오프라인 푸시 설정 TPNS TOKEN 지원


## IM Flutter SDK 3.7.1 @2022.01.12
- 메시지 전송 진행률 이벤트의 메시지 생성 id 반환
- 콜백 부분을 최적화하여 SDK에서 catch되어 비즈니스측에서 수정해야 하는 오류를 비즈니스측에서 콜백하도록 안내

## IM Flutter SDK 3.7.0 @2022.01.10
- cloudCustomData 패키지 해제 최적화


## IM Flutter SDK 3.6.9 @2022.01.06
- 회신 메시지 매개변수 최적화


## IM Flutter SDK 3.6.8 @2022.01.06
- 회신 메시지 인터페이스 최적화


## IM Flutter SDK 3.6.7 @2022.01.05
- iOS 컴파일 환경 8.0에서 9.0으로 업그레이드


## IM Flutter SDK 3.6.6 @2021.12.30
- 메시지 응답 인터페이스 추가
- Web 측에서 release mode의 오류 수정


## IM Flutter SDK 3.6.5 @2021.12.17
- java 구문 오류 수정

## IM Flutter SDK 3.6.4  @2021.12.17
- Android 비동기 등록 이벤트에 대한 반환이 없는 bug 수정
- 기본 리스너 이벤트 삭제 시 오류 수정
- 메시지 진행률 이벤트에 전송 중 메시지 uuid 추가

## IM Flutter SDK 3.6.3 @2021.12.9
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

## IM Flutter SDK 3.6.2 @2021.12.9
- 고급 메시지 삭제 시 uuid 미전달 문제 수정


## IM Flutter SDK 3.6.1 @2021.12.8
- 파일 진행률 이벤트 유실 수정


## IM Flutter SDK 3.6.0 @2021.12.1
- 각 모듈은 listener의 다중 가입 및 다중 콜백 지원
- 모든 세션을 읽음으로 설정하는 api markAllMessageAsRead 추가
- 결합된 메시지 리졸브 추가
- native 버전을 5.8.1668로 업그레이드


## IM Flutter SDK 3.5.6 @2021.11.25
- checkFriend 실패 문제 수정
- getC2CHistoryMessageList 후속 메시지 수신 불가 문제 수정

## IM Flutter SDK 3.5.5 @2021.11.23
- 아키텍처 조정


## IM Flutter SDK 3.5.4 @2021.11.22
- downloadMergeMesasge 인터페이스 추가


## IM Flutter SDK 3.5.3 @2021.11.15
- onTotalUnreadMessageCountChanged 이벤트 추가
- 세션 정렬을 위해 V2TimConversation에 orderkey 필드 추가


## IM Flutter SDK 3.5.2 @2021.11.12
add web support

## IM Flutter SDK 3.5.1 @2021.11.10
- 배열 인덱스 아웃 오브 바운즈 로직 호환


## IM Flutter SDK 3.5.0 @2021.10.1
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

## IM Flutter SDK 1.0.34 @2021.03.22
- iOS가 기존 메시지 오류를 가져오는 문제 수정

## IM Flutter SDK 1.0.33 @2021.03.22
- sdk의 minSdkVersion을 16으로 수정

## IM Flutter SDK 1.0.32 @2021.03.22
- 세션 정보 lastMessage가 비어 있을 때의 crash 수정

## IM Flutter SDK 1.0.30-1.0.31 @2021.03.18
- 사용자 정의 메시지 data 필드가 null일 때의 crash 수정

## IM Flutter SDK 1.0.29 @2021.03.16
- [중요]그룹 참석자 목록 가져오기 및 매개변수 전달 오류 수정

## IM Flutter SDK 1.0.28 @2021.03.16
- [중요]CheckFriends 인터페이스 입력 매개변수 변경

## IM Flutter SDK 1.0.15-1.0.27 @2021.03.15
- 그룹 참석자 사용자 정의 필드 추가
- iOS 신호 개선
- iOS 신호 bug 수정
- 사용자 정의 필드를 String으로 리졸브하여 반환
- 개인 사용자 정의 필드에 최적화된 설정
- Android getHistoryMessageList 업데이트
- Android측 매개변수 전달 checkFriend 오류 수정

## IM Flutter SDK 1.0.5-1.0.14 @2021.02.26
- deleteFriendApplication 매개변수 전달 오류 수정
- native sdk를 5.1.132로 업데이트
- native sdk를 5.1.137로 업데이트
- 신호 초대 인터페이스의 매개변수 전달 bug 수정
- 신호 인터페이스 id 미반환 문제 수정
- sdk 압축 설정 수정
- 신호 콜백 bug 수정
- 사용자 정의 메시지 데이터 반환 수정
- [중요]신호 메시지의 반환 콘텐츠 형식이 수정되었으므로 신호 사용 시 버전을 업데이트 하십시오.


## IM Flutter SDK 1.0.4 @2021.01.14

- Android SDK 버전을 5.1.129로 업데이트
- iOS SDK 버전을 5.1.129로 업데이트

## IM Flutter SDK 1.0.3 @2021.01.13
- Android/iOS에 대한 크로스 플랫폼 지원
- 1:1 채팅 및 그룹 채팅(토론 그룹, 라이브 그룹) 세션 유형 지원
- 텍스트, 이모티콘, 이미지, 음성 및 사용자 정의 메시지 지원 추가
- APNs 오프라인 푸시 지원(token 리포트, 포그라운드/백그라운드 전환 이벤트 리포트)
- 메시지 로컬 저장 가능

## IM Flutter SDK 0.0.1-1.0.2 @2020.12.01
- Flutter SDK 런칭
- 베타 테스트에 초대된 사용자
