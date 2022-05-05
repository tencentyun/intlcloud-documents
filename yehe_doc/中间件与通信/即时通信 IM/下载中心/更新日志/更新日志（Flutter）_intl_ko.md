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
- Android 비동기화 가입 이벤트가 반환되지 않는 bug 수정
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
- 베타에 사용자 초대
