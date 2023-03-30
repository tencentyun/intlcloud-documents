### 2.25.0 @2022.12.8

**새로운 기능**

- [clearHistoryMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#clearHistoryMessage) API는 로컬 및 클라우드 메시지 비우기를 지원합니다.
- 메시지 확장(플래그십 버전 기능)을 지원합니다.
- 일반 그룹과 커뮤니티 그룹 속성을 지원합니다.
- [wx.chooseMedia](https://developers.weixin.qq.com/miniprogram/dev/api/media/video/wx.chooseMedia.html)와 호환됩니다.
- [Message.readReceiptInfo](https://web.sdk.qcloud.com/im/doc/en/Message.html)는 C2C 수신 확인을 지원합니다(데이터 구조는 NativeIM과 정렬됨).
- 에러 코드 2101: 라이브 그룹에 가입하지 않으면 라이브 그룹에 메시지를 보낼 수 없습니다.

**변경 사항**

- 로그 리포트 백업 채널은 독립 클러스터 도메인 `https://events.im.qcloud.com`을 사용합니다(플랫폼에 수신 도메인 구성이 추가되어야 함).

**오류 수정**

- cookies blocked로 인한 실행 시 오류(Failed to read the 'localStorage' property from 'Window': Access is denied for this document).


### 2.24.1 @2022.11.11

**새로운 기능**

- 영문판 ts 성명 파일.
- restapi는 친구의 사용자 정의 프로필 필드 수정 및 SDK 푸시 지원.

**오류 수정**

- [getMessageListHopping](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageListHopping) 일부 시나리오에서 이상 결과가 반환되는 문제.

### 2.24.0 @2022.11.3

**새로운 기능**

- 미니 게임 환경 통합 지원.
- 로컬 비속어 플러그인 [tim-profanity-filter-plugin](https://www.npmjs.com/package/tim-profanity-filter-plugin), 로컬 비속어 기능 지원.
- [getFriendProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendProfile) 제품 경험을 개선하기 위해 친구 사용자 정의 필드 및 데이터 사용자 정의 필드 가져오기 지원.
- [getGroupApplicationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupApplicationList) 전체 그룹 추가 요청 목록 풀링 지원.
- RESTAPI는 친구의 사용자 정의 필드를 수정 및 SDK 푸시 지원.
- 읽지 않은 것으로 계산되지 않는 토픽 메시지 전송 지원.
- 읽지 않은 것으로 간주되지 않는 일반 커뮤니티 메시지 전송 지원.
- 메시지를 보낼 때 voip push 지원.

**오류 수정**

- 친구 프로필 관련 문제.


### 2.23.1 @2022.9.29

**새로운 기능**

- [createTextMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage) 등 그룹 지향 메시지 생성을 지원하는 인터페이스 추가(즉, 그룹의 일부 그룹 구성원에게 메시지를 전송하면 다른 그룹 구성원은 이러한 메시지를 받지 않습니다).
- mov 형식의 비디오 전송 지원.
- REST API [친구 업데이트](https://intl.cloud.tencent.com/document/product/1047/34904)에서 SDK로의 푸시 지원.
- [getFriendProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendProfile)은 사용자 지정 친구 필드 및 사용자 지정 데이터 필드 풀링 지원.
- [getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList) 인터페이스의 반환된 데이터 새 기능 필드가 SyncCompleted로, 클라우드에서 대화 목록의 동기화 완료 여부 식별에 사용.
- 주제가 속한 커뮤니티 메시지에서 [MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED)를 통해 액세스측 알림 지원.

**오류 수정**

- 그룹 목록이 상한인 5000개를 초과한 후 일부 그룹 대화가 로밍 메시지를 가져올 수 없는 문제
- 해당 대화의 customData가 ’’ 세션 사용자 정의 필드를 설정하기 위해 setConversationCustomData를 호출한 후 다시 로그인하는 문제.

### 2.23.0 @2022.9.16

**새로운 기능**

- SDK 중국 외 환경 지원.
- [getTotalUnreadMessageCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTotalUnreadMessageCount), 읽지 않은 총 세션 수 가져오기 지원.
- [TOTAL_UNREAD_MESSAGE_COUNT_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOTAL_UNREAD_MESSAGE_COUNT_UPDATED), 세션에서 읽지 않은 총 세션 수의 변경 알림을 받기 위해 액세스 측에서 이벤트를 수신 대기하도록 추가.
- [markGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markGroupMemberList), 라이브 그룹 구성원의 태그 지정 지원(플래그십 버전에서만 지원).
- 그룹 구성원이 그룹에서 추방되거나 그룹이 삭제될 때 SDK가 그룹 대화가 있는 대화 그룹을 동기식으로 업데이트하도록 추가.
- uni-apps의 독립적인 하도급 지원.
- 지원되는 SDK는 메시지 신뢰성을 보장하기 위해 Web 다중 인스턴스 로그인 시나리오에서 네트워크 연결 해제 및 재연결 후 가장 최근 연락처의 메시지 기록을 자동으로 복구.

**오류 수정**

- Web 다중 인스턴스 로그인 시나리오에서 세션 lastMessage의 회수 상태가 동기화되지 않는 문제.
- 최근 연락처를 동기화할 때 대화 상단 고정 문제.

### 2.22.0 @2022.8.18

**새로운 기능**

- 오프라인 푸시를 위해 native app에 지원되는 uni-app 패키지. [registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin)을 참고하십시오.
- 라이브 스트림 룸의 온라인 구성원 목록 가져오기 지원. [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList)를 참고하십시오(플래그십 버전에서만 지원).
- 라이브 방송 그룹 구성원 차단 지원. [deleteGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteGroupMember)를 참고하십시오(플래그십 버전에서만 지원).
- [setConversationCustomData](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setConversationCustomData) 대화 설정 사용자 지정 데이터 추가.
- [markConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markConversation) 마크 대화 추가(플래그십 버전에서만 지원).
- [getConversationGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationGroupList) 대화 그룹 목록 가져오기 추가(플래그십 버전에서만 지원).
- [createConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createConversationGroup) 대화 그룹 생성 추가(플래그십 버전에서만 지원).
- [deleteConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationGroup) 대화 그룹 삭제 추가(플래그십 버전에서만 지원).
- [renameConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#renameConversationGroup) 대화 그룹 이름 바꾸기 추가(플래그십 버전에서만 지원).
- [addConversationsToGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addConversationsToGroup) 대화 그룹에 대화 추가 추가(플래그십 버전에서만 지원).
- [deleteConversationsFromGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationsFromGroup) 대화 그룹 대화 삭제 추가(플래그십 버전에서만 지원).

**오류 수정**

- 대화 메시지가 회수되었다는 알림을 받은 후 읽지 않은 대화 수가 업데이트되지 않는 문제.

### 2.21.2 @2022.8.8

**새로운 기능**

- Web에서 음성 메시지 생성 및 전송 지원.
- [createMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createMergerMessage) 병합된 메시지 생성 및 병합된 메시지의 새 기능 ID 필드 추가.

### 2.21.1 @2022.8.3

**오류 수정**

[resendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#resendMessage)로 인해 발생할 수 있는 메시지 중복 문제 수정.

### 2.21.0 @2022.7.28

**새로운 기능**

- [setSelfStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setSelfStatus), 자신의 사용자 정의 상태 추가.
- [getUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserStatus), 사용자 상태 가져오기 추가.
- [subscribeUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#subscribeUserStatus), 구독 사용자 상태 추가.
- [unsubscribeUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#unsubscribeUserStatus), 구독 취소 사용자 상태 추가.
- [setMessageRemindType](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRemindType) 그룹 메시지 및 주제 메시지에 대한 DND 설정의 다중 터미널 및 다중 인스턴스 동기화 지원.
- [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage) 파일 메시지 보내기 지원.
- [modifyMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#modifyMessage) 모든 유형의 메시지에 대해 cloudCustomData 수정 지원.
- [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html) isBroadcastMessage 필드 추가. 라이브 룸 방송 메시지 지원.
- 그룹 추가 옵션으로 다중 터미널 및 다중 인스턴스 동기화 지원.
- 일반 커뮤니티 및 주제 @모든 구성원 및 주제 lastMessage 지원.

**변경 사항**

- webworker는 브라우저가 webworker를 지원하는 경우 글로벌 웹 사이트 및 개인 환경에서 기본적으로 활성화됩니다.

**오류 수정**

- 대화 lastMessage를 업데이트하지 않는 메시지를 수신한 후 lastMessage.payload가 undefined로 설정되는 문제.
- 온라인 메시지로 인한 그룹 메시지 보상이 시작되지 않는 문제.
- 잦은 그룹 탈퇴 및 추가 후 풀 로밍 메시지 문제.
- 페이징 풀 그룹 목록 랙으로 인해 풀 그룹 대화 로밍 메시지가 빈 배열 문제.
- 알려진 문제를 수정.

### 2.20.1 @2022.6.27

**변경 사항**

- 라이브 그룹 외 그룹에서 퇴장/강제 퇴장되거나, 라이브 그룹 외 그룹이 해산된 경우 그룹 기록만 삭제되고, 해당 그룹 대화는 삭제되지 않으며, native와 매칭합니다.
- [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage) 그룹 시스템 삭제 알림을 지원하지 않으며, 특정 오류 메시지가 표시됩니다. 
- 프라이빗 배포된 리치 미디어 메시지는 HTTP 프로토콜을 지원합니다.

**오류 수정**

- 프런트/백그라운드 전환과 같은 시나리오에서 가끔 발생하는 그룹 대화 손실 문제.
- C2C 대화 lastMessage가 비정상적으로 업데이트되는 문제.

### 2.20.0 @2022.6.9

**새로운 기능**

- [modifyMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#modifyMessage), 메시지 변경을 지원합니다.
- [getMessageListHopping](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageListHopping), 지정된 메시지 sequence 또는 메시지 시간에 따라 대화의 메시지 목록 가져오기를 지원합니다.
- 하나 이상의 C2C 메시지 발송에 대한 수신 확인 지원 (플래그십 버전 필요).
- C2C 대화 lastMessage의 추가 필드 isPeerRead는 피어 읽음 여부 식별에 사용.
- 그룹 알림 메시지는 읽지 않은 대화 수에 합산하지 않기 지원.
- [TIM.TYPES.KICKED_OUT_REST_API](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.KICKED_OUT_REST_API) 유형 추가, REST API [kick](https://intl.cloud.tencent.com/document/product/1047/34957) 지원.

**변경 사항**

[getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)에서 로밍 메시지를 가져오기를 개선하고 최적화합니다.

**오류 수정**

- 매개변수 전달 문제로 인해 [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage) 성공 후 대화 목록이 업데이트되지 않습니다.
- 일부 모델에서 디버깅 시 발생한 `Cannot add property markTimeline, Object is not extensible` 문제.

### 2.19.1 @2022.5.7

**새로운 기능**

- [커뮤니티(Community)](https://intl.cloud.tencent.com/document/product/1047/33529)에서 토픽(Topic) 생성을 지원하여, 더 강한 인터랙션 시나리오를 지원합니다.
- [getJoinedCommunityList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getJoinedCommunityList) 지원되는 토픽의 커뮤니티 목록을 가져옵니다.
- [createTopicInCommunity](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTopicInCommunity) 토픽을 생성합니다.
- [deleteTopicFromCommunity](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteTopicFromCommunity) 토픽을 삭제합니다.
- [updateTopicProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateTopicProfile) 토픽 프로필을 설정합니다.
- [getTopicList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTopicList) 토픽 목록을 가져옵니다.
- [TIM.EVENT.TOPIC_CREATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_CREATED) 토픽 생성 시 트리거되는 이벤트입니다.
- [TIM.EVENT.TOPIC_DELETED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_DELETED) 토픽 삭제 시 트리거되는 이벤트입니다.
- [TIM.EVENT.TOPIC_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_UPDATED) 토픽 프로필 업데이트 시 트리거되는 이벤트입니다.

### 2.18.2 @2022.4.22

**변경 사항**

라이브 그룹 사용 경험을 최적화합니다.

**오류 수정**

- 일부 시나리오에서 부정확한 통계 문제 
- 호출 인터페이스에서 [getGroupMessageReadMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList) 반환 결과가 부정확한 문제.

### 2.18.0 @2022.4.8

**새로운 기능**

- 그룹 메시지 수신 확인 발송을 위한 [sendMessageReadReceipt](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessageReadReceipt) 추가.
- 그룹 메시지 수신 확인 목록을 가져오기 위한 [getMessageReadReceiptList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageReadReceiptList) 추가.
- 그룹 메시지를 읽었거나 읽지 않은 구성원 목록을 가져오기 위한 [getGroupMessageReadMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList) 추가.
- messageID로 대화에서 로컬 메시지를 쿼리하기 위한 [findMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#findMessage) 추가.
- NativeIM과 일치하는 메시지 회수 후 읽지 않은 메시지 수 업데이트 경험 개선.

**변경 사항**

- [Message.ID](https://web.sdk.qcloud.com/im/doc/en/Message.html) 스티칭 규칙은 `${senderTinyID}-${clientTime}-${random}`이며 NativeIM 메시지의 ID와 일치.
- SDK not ready 상태인 경우 액세스 측에 대한 특정 이유 제공.

**오류 수정**

그룹 구성원이 그룹에서 퇴장된 후 다른 그룹 구성원이 [CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) 이벤트 콜백에서 얻은 `Conversation.groupProfile.memberCount` 값이 업데이트 되지 않음.

### 2.17.0 @2022.3.2

**새로운 기능**

- [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529) 지원.
- 최근 연락처의 'Conversation.lastMessage'에 대한 그룹 알림 지원.
- `Message.payload.memberList`는 그룹에 가입하거나 탈퇴한 그룹 구성원의 닉네임, 프로필 사진 및 기타 정보를 가져오기 지원.
- 이미지 메시지 전송을 위한 webp 이미지 지원.
- 비디오 메시지 전송을 위한 비디오 커버 [snapshotUrl](https://web.sdk.qcloud.com/im/doc/en/Message.html#.VideoPayload) 지원.
- 메시지 전송 효율성 향상, [CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) 등 이벤트 스로틀링.

**오류 수정**

- 사용자가 사용자 정의 데이터(cloudCustomData)가 포함된 메시지를 보낸 후 사용자가 다시 로그인할 때 cloudCustomData가 비어 있는 문제.
- [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) 실패 후 사용자가 다시 로그인하면 SDK에서 ‘반복 로그인 오류’를 보고하는 문제.
- [getGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupProfile)이 호출된 후 `Conversation.groupProfile`이 최신 그룹 프로필과 일치하지 않는 문제.

### 2.16.3 @2022.2.11

**오류 수정**

Windows 액세스 패키지 Android app(일부 기기)에 액세스할 때 로그인 실패 발생.

### 2.16.2 @2022.2.10

**새로운 기능**

- uni-app 패키지 native app 후 파일 메시지 발송 지원.
- 인도 글로벌 포털 지원.

**오류 수정**

- 일부 emoji 렌더링 문제 수정.

### 2.16.1 @2022.1.14

**새로운 기능**

- .image 이미지를 보내기 위한 Alipay 지원 추가.
- [deleteConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversation)이 대화를 삭제하기 위해 호출되면 대화의 기록 메시지도 삭제됨.

**오류 수정**

- 다운스트림 파일 메시지 `fileName`이 빈 문자열일 때 오류 발생.
- 그룹 속성 API 호출 시퀀스로 인해 발생하는 문제 수정.
- Baidu 등 플랫폼에 대한 uni-app 패키지 앱에서 발생하는 `__wxConfig is not defined` 문제.

### 2.16.0 @2022.1.5

**새로운 기능**

- [setMessageRemindType](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRemindType)은 C2C 대화에 대한 알림 음소거 모드 설정 지원.
- [setAllMessageRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setAllMessageRead)는 모든 대화의 읽지 않은 메시지를 읽은 것으로 빠르게 표시 지원.
- [sendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessage)는 대화의 읽지 않은 메시지 수에서 보낸 메시지를 제외하고 대화의 `lastMessage` 업데이트하지 않음 지원.
- 오디오/비디오 그룹의 새 구성원이 그룹에 가입하기 전에 기록 메시지를 볼 수 있도록 함(기능을 사용하려면 플래그십 버전 패키지를 활성화해야 함).

**변경 사항**

- SDK는 [엄격 모드](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Strict_mode)를 사용합니다.
- 계정이 삭제된 대화는 대화 목록에서 필터링됨.
- 로밍 메시지에 대한 `nick` 및 `avatar` 업데이트 타이밍 최적화.
- 피어(친구) 프로필 업데이트 정보를 수신하면 SDK는 이에 따라 `conversation.userProfile` 업데이트.

**오류 수정**

- 비 UTF-8 문자로 인해 WebSocket 영구 연결이 비정상적으로 끊어지는 문제.
- 복사된 메시지가 [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage)를 호출하기 위해 전달될 때 런타임 오류 `e.getOnlineOnlyFlag is not a function` 발생.
- [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage)가 호출된 후 해당 대화의 `lastMessage`가 올바르게 업데이트되지 않음.
- C2C 대화의 읽지 않은 메시지 수 계산 오류 발생.
- `nick`과 `avatar`가 C2C 대화의 실시간 메시지에 전달되지 않은 경우 렌더링 예외 발생.
- 세션 `lastMessage.payload`가 간헐적으로 `null`인 문제 발생.
- 미리 서명된 이미지 썸네일 업로드 URL 미적용.
- 사용자가 @ 그룹 구성원을 언급하고 로밍 메시지를 가져오기 위해 다시 로그인했을 때 해당 message.atUserList가 빈 배열임.
- 그룹 알림(그룹 소유자 변경) 처리 중 오류 발생.
- 일부 통계 오류.

### 2.15.0 @2021.10.29

**새로운 기능**

- 글로벌 포털 지원.
- [createLocationMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createLocationMessage) 지리적 위치 메시지 전송 지원.
- 쉽게 다운로드하고 미리보기 할 수 있도록 이미지, 비디오, 문서 업로드 지원(uniapp과 호환).
- [Conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html)의 `lastMessage` 데이터 구조에 `nick` 및 `nameCard` 매개변수를 추가하여 그룹 채팅에서 `lastMessage`의 보낸 사람 정보를 더 잘 표시함.

**변경 사항**

- [getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList)는 한 번에 여러 개의 지정된 대화 가져오기 지원.
- 장기간 연결의 안정성 제고.

**오류 수정**

- 대화 목록 캐시가 없거나 최근 연락처에 대한 페이징이 없는 경우 로그인 후 [CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) 이벤트가 전송되지 않는 문제 수정.
- 일부 시나리오에서 `isCompleted` 매개변수가 [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) API 호출에 대한 응답에서 항상 `false`인 문제 수정.
- [createFaceMessage](createFaceMessage) API 호출에서 `index`가 0으로 설정된 경우 수신자 측에서 `index` 매개변수가 누락되는 문제 수정.

### 2.14.0 @2021.9.24

**새로운 기능**

- [pinConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#pinConversation)은 대화를 맨 위에 고정하는 기능 지원.
- [initGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#initGroupAttributes) 및 기타 그룹 속성 관련 API는 오디오 대화방에 대한 좌석 관리 지원.

**변경 사항**

- 그룹 메시지가 전송되면 SDK는 자동으로 `nameCard` 속성을 메시지 본문에 추가하여 액세스 측에서 쉽게 표시 가능.
- 다중 클라이언트 로그인 또는 다중 인스턴스 로그인으로 인한 강제 로그아웃이 더 이상 서버 측 logout 콜백을 트리거하지 않음.

**오류 수정**

- C2C 대화에서 로밍 메시지를 가져올 때 간헐적으로 메시지 손실.
- 그룹 가입 설명(applyMessage) 누락.

### 2.13.1 @2021.8.27

**변경 사항**

- 사용자가 로그인 전에 [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) API를 연속적으로 호출하면 [반복 로그인]을 나타내는 오류 코드 `2025` 반환.
- WebSocket 재연결 후 SDK는 다시 로그인하고 읽지 않은 메시지를 동기화하여 메시지 신뢰성 보장.

**오류 수정**

- 사용자가 로그인 전에 [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) API를 연속으로 호출했을 때 대화의 읽지 않은 메시지 수 오류.
- [setGroupMemberNameCard](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberNameCard) API가 호출될 때 `nameCard`가 빈 문자열로 전달된 경우 SDK에서 오류 보고.
- [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList) API가 호출될 때 반환된 패킷의 `muteUntil` 값 오류.

### 2.13.0 @2021.8.23

**새로운 기능**

친구 관계 체인 지원. 자세한 내용은 [사용 가이드](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html)를 참고하십시오.

**오류 수정**

WebSocket 장기간 연결 중단 시 간헐적인 오류 발생.

### 2.12.2 @2021.8.6

**새로운 기능**

비디오 업로드는 진행률 콜백 지원.

**변경 사항**

대화의 읽지 않은 메시지 수에는 사용자 정의 그룹 필드의 수정 사항을 로밍 서버에 저장하지 않는다는 그룹 알림이 더 이상 포함되지 않음.

**오류 수정**

- 오디오/비디오 그룹의 사용자가 스스로 그룹에 참여하는 그룹 알림을 받지 못하는 간헐적 오류 발생.
- 사용자가 restapi를 사용하여 random이 0으로 설정된 c2c 메시지를 보낼 때 수신자가 [MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED) 이벤트를 두 번 트리거함.

### 2.12.1 @2021.7.20

**새로운 기능**

- Meeting 그룹 읽지 않은 메시지 계산 지원.
- [TIM.EVENT.MESSAGE_MODIFIED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_MODIFIED) 이벤트 추가. 3rd party가 수정된 메시지를 다시 호출하면 SDK는 이 이벤트를 사용하여 메시지 발신자에게 메시지 수정을 알림.

**오류 수정**

- 그룹 로밍 메시지를 가져오면 간헐적으로 사라지는 현상 수정.
- uni-app 통합 중 발생할 수 있는 'xx.toFixed is not a function' 문제 수정.

### 2.12.0 @2021.7.5

**새로운 기능**

- [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage) 메시지 삭제 지원.
- 대화 목록 동기화 중에 `lastMessage`를 회수된 메시지로 설정 가능.
- [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList)는 그룹 가입 시간 `joinTime` 가져오기 지원.

**오류 수정**
사용자가 admin으로 설정되거나 취소될 때 전송되는 알림의 `nick` 값 오류.

### 2.11.2 @2021.6.16

**새로운 기능**

- WebSocket 지원. [WebSocket 업그레이드 가이드](https://web.sdk.qcloud.com/im/doc/en/tutorial-02-upgradeguideline.html).
- uni-app이 이미지, 비디오 및 기타 파일 메시지 발송 지원.

### 2.10.2 @2021.4.27

**새로운 기능**

- 사용자 정의 필드 `cloudCustomData`는 다양한 비즈니스 요구를 충족시키기 위해 메시지 생성 중 설정 가능.
- [createGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createGroup) 또는 [addGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addGroupMember)가 호출될 때 단일 사용자가 ‘단일 사용자가 가입할 수 있는 최대 그룹 수’를 초과하는 경우 `overLimitUserIDList`를 사용하여 액세스 측에 알림.

**오류 수정**

- 오디오/비디오 방(AVChatRoom)이 [콘솔](https://console.cloud.tencent.com/im)에서 생성되고 그룹 소유자가 지정된 후 [Sending System Messages in a Group](https://intl.cloud.tencent.com/document/product/1047/34958)을 위해 REST API에서 보낸 메시지는 그룹 소유자가 그룹에 가입한 후 그룹 소유자 측에서 반복됨.
- [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage)가 호출될 때 닉네임 누락.
- [downloadMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#downloadMergerMessage)가 호출될 때 간헐적 오류 발생.

### 2.10.1 @2021.3.19

**새로운 기능**

- 결합된 메시지를 생성하기 위한 [createMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createMergerMessage) API.
- 전달 메시지를 생성하기 위한 [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage) API.
- 계정이 여러 인스턴스 또는 클라이언트에 로그인할 때 한 인스턴스 또는 클라이언트에서 읽은 대화가 보고되면 Web 클라이언트에서 읽지 않은 대화 수가 동기적으로 삭제됨.

**변경 사항**

MTA 통계 기능은 더 이상 사용되지 않음.

**오류 수정**

- Web: 여러 인스턴스에서 계정 로그인 시, C2C 대화에서 상대방의 프로필 사진과 닉네임 오류.
- 메시지를 보낸 후 자주 메시지를 회수하기 위해 REST API를 호출하고 호출했을 때 일부 메시지가 올바르게 회수되지 않음.

### 2.9.3 @2021.2.3

**변경 사항**

사용자가 그룹(오디오/비디오 그룹이 아님)에 가입하지 않은 경우 [quitGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#quitGroup)을 호출하면 사용자가 그룹에 없음을 나타내는 오류 코드 2623이 반환됨.

**오류 수정**

`avatar`(프로필 사진) 또는 `nick`(닉네임)이 C2C 대화 메시지 목록에서 일치하지 않음.

### 2.9.2 @2021.1.26

**새로운 기능**

- `avatar`(프로필 사진)와 `nick`(닉네임)이 표시된 C2C 메시지 송수신을 지원함.
- Tencent Cloud IM 업로드 플러그인 [tim-upload-plugin](https://www.npmjs.com/package/tim-upload-plugin) 지원. 이 플러그인은 보다 안전한 파일 업로드를 가능하게 하고 Web 및 Baidu, Toutiao, Alipay 플랫폼을 지원하며 26KB에 불과합니다. 자세한 내용은 [registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin)을 참고하십시오.

**오류 수정**

- 사용자가 로그아웃한 후 익명으로 오디오/비디오 그룹에 가입하면 긴 폴링 동안 응답 패킷에 오류 코드 70402가 반환됨.
- Taro 3.0+ 통합 과정에서 브라우저 환경이 잘못 판단됨.
- 이미지 유형 및 크기 확인에 실패했을 때 반환된 데이터 구조에 오류 발생.

### 2.9.1 @2020.12.23

**오류 수정**

개발자 툴의 기본 라이브러리 2.14.1에 [tim-wx-sdk.js](https://www.npmjs.com/package/tim-wx-sdk)를 가져올 때 컴파일 오류 발생.

### 2.9.0 @2020.12.15

**새로운 기능**

- [createTextAtMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage) API를 사용하면 그룹 채팅 중에 @ 특정 구성원 또는 @ 모든 구성원 지정 가능.
- [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)는 그룹 구성원의 그룹 이름 카드(즉, 그룹의 닉네임)를 표시하기 위해 `namecard` 속성 추가.

### 2.8.5 @2020.11.23

**변경 사항**

SDK가 ready되지 않은 경우 [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout) API 호출 가능.

**오류 수정**

- 수신 확인 및 수신 알림이 동시에 존재하는 경우 SDK 작업에서 오류 발생.
- 로그아웃한 후 오디오-비디오 그룹 익명 재가입 시도 실패.
- 그룹 목록이 비정상적으로 삭제됨.

### 2.8.4 @2020.11.4

**새로운 기능**

- Baidu, Toutiao 및 Alipay 플랫폼 지원(현재 Baidu, Toutiao 및 Alipay 플랫폼에서 COS에 업로드해야 하는 이미지, 비디오 또는 파일 메시지 또는 기타 메시지는 보낼 수 없습니다).
- MPX 및 uni-app의 3rd party 프레임워크 지원.

### 2.8.1 @2020.10.29

**새로운 기능**

bmp 형식의 이미지 발송 가능.

**변경 사항**

발신자가 온라인 메시지를 보내고 수신자가 온라인 메시지를 수신하면 [대화 객체](https://web.sdk.qcloud.com/im/doc/en/Conversation.html)의 `unreadCount` 및 `lastMessage`가 업데이트되지 않음.

**오류 수정**

최근 연락처 목록 동기화 문제로 인해 SDK가 ready 상태로 들어갈 수 없는 문제.

### 2.8.0 @2020.10.20

**새로운 기능**

- [getGroupOnlineMemberCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupOnlineMemberCount)는 오디오/비디오 그룹의 온라인 사용자 수 쿼리 지원.
- 이미지 압축 지원. 액세스 측에서는 비즈니스 요구 사항에 따라 원본 이미지 또는 축소판 표시 가능. 자세한 내용은 [ImagePayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.ImagePayload)를 참고하십시오.

**오류 수정**

Taro 3.x가 WebIM을 통합할 때의 호환성 문제.

**변경 사항**

SDK 크기 축소. [tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk)의 크기는 8.5%, [tim-wx-sdk](https://www.npmjs.com/package/tim-wx-sdk)의 크기는 15% 감소.

### 2.7.8 @2020.9.24

**새로운 기능**

[TIM.create](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create) API는 `oversea` 매개변수를 추가합니다. 이 매개변수가 `true`로 설정되면 SDK는 간섭을 피하기 위해 중국 외의 도메인 이름 사용.

**오류 수정**

- SDK가 not ready 상태일 때 관련 API 호출에 대한 반환 값이 `undefined`인 문제.
- 통계 관련 문제.

### 2.7.7 @2020.8.12

**새로운 기능**

[TIM.EVENT.SDK_RELOAD](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.SDK_RELOAD) 이벤트 추가.

**오류 수정**

- 오디오/비디오 그룹은 장시간 연결이 끊긴 후 네트워크가 다시 연결되면 간헐적으로 메시지를 가져오지 못하는 오류가 있습니다.
- 이미지 메시지의 imageFormat 유형 및 값이 실제 이미지와 불일치.
- Work 그룹 및 Public 그룹에 잘못된 닉네임 표시.

### 2.7.6 @2020.7.9

**오류 수정**

오디오/비디오 그룹(AVChatRoom)을 장기간 사용한 경우 메시지를 가져오지 못하는 간헐적 오류.

### 2.7.5 @2020.7.2

**오류 수정**

[작업 그룹 생성](https://intl.cloud.tencent.com/document/product/1047/34895)을 위한 REST API를 호출하여 작업 그룹을 성공적으로 생성하고 그룹 구성원을 지정한 후 그룹 구성원의 메시지 전송 실패.

### 2.7.2 @2020.6.30

**오류 수정**

- [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup) 호출 시 SDK에서 ‘이미 그룹에 있습니다’라는 메시지를 표시했지만 실제로는 사용자가 그룹에 없어 메시지를 송수신 할 수 없는 문제 발생.
- 임시 회의 그룹에서 보낸 메시지 수 오류.

### 2.7.0 @2020.6.8

**새로운 기능**

C2C 메시지 수신 확인 지원(피어가 메시지를 읽음 여부 나타냄). 자세한 내용은 [TIM.EVENT.MESSAGE_READ_BY_PEER](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_READ_BY_PEER) 이벤트를 참고하십시오. 피어가 이미 읽은 [메시지](https://web.sdk.qcloud.com/im/doc/en/Message.html)에서 `isPeerRead`의 값은 `true`.

**오류 수정**

- 사용자가 대화방(ChatRoom)에 참가한 후 새로 생성된 대화에 마지막 메시지가 표시되지 않음.
- 로그인 후 오디오/비디오 그룹(AVChatRoom)에 가입하지 않은 사용자는 여전히 오디오/비디오 그룹(AVChatRoom)에 메시지 발송 가능.

### 2.6.6 @2020.5.27

**오류 수정**

- 오디오/비디오 그룹(AVChatRoom)에서 화면에 메시지 반복 표시.
- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) 빈 메시지 수신 시 오류 보고.
- [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout) 후 다시 [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login)을 호출하면 [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup) 호출 시 70001 오류 간헐적 발생.

### 2.6.4 @2020.5.8

**새로운 기능**

[sendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessage) API는 온라인 메시지 전송(오프라인 또는 로밍 메시지 없음, AVChatRoom 또는 BChatRoom에 사용할 수 없음) 및 [오프라인 푸시](https://intl.cloud.tencent.com/document/product/1047/33525) 구성을 지원하는 전송 옵션 추가.

### 2.6.3 @2020.4.26

**오류 수정**

- [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage)의 입력 payload.data payload.extension 유형이 올바르지 않아 메시지 내용 손실.
- 단일 요청에 대한 응답에 포함된 여러 메시지 무질서.
- 읽지 않은 C2C 변환 수가 오버플로되어 읽기 카운트가 보고된 후 읽지 않은 카운트를 지울 수 없음.
- [TIM.EVENT.ERROR](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.ERROR) event.data.code 및 event.data.undefined가 간헐적 undefined.

### 2.6.2 @2020.4.16

**새로운 기능**

- [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateGroupProfile)은 모두 음소거 및 음소거 해제 지원.
- [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList)는 그룹 구성원 음소거 기한 타임스탬프 [muteUntil](https://web.sdk.qcloud.com/im/doc/en/GroupMember.html) 가져오기 지원.

**오류 수정**

최신 그룹 메시지가 그룹 프롬프트인 경우 읽지 않은 수를 지울 수 없음.

### 2.6.1 @2020.4.8

**오류 수정**

업로드된 COS 서명이 유효하지 않고 적시에 업데이트되지 않으면 파일을 업로드할 수 없는 간헐적 문제.

### 2.6.0 @2020.3.30

**새로운 기능**

- Web 클라이언트는 [createVideoMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createVideoMessage)를 호출하여 최대 100MB의 비디오 메시지 생성 및 전송 지원.
- `nick` 및 `avatar` 속성이 [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)에 추가되어 오디오/비디오 그룹(AVChatRoom)에 있는 메시지 발신자의 닉네임과 프로필 사진 주소 표시. [updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile)을 호출하여 미리 닉네임과 프로필 사진 주소를 설정해야 함.
- Web: 계정이 여러 인스턴스에 로그인하면 C2C 메시지 회수 알림이 이러한 인스턴스에서 동기화 가능.
- [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateGroupProfile)이 사용자 지정 그룹 필드를 성공적으로 수정하도록 호출된 후 그룹 구성원은 그룹 알림을 수신하고 관련 콘텐츠인 [Message.payload.newGroupProfile.groupCustomField](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload)를 얻을 수 있음.

**변경 사항**

[TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED)는 더 이상 사용되지 않으며 [MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED)로 대체됨.

**오류 수정**

[getGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupList) API가 호출될 때 간헐적 오류 발생.

### 2.5.2 @2020.3.13

**변경 사항**

[searchGroupByID](https://web.sdk.qcloud.com/im/doc/en/SDK.html#searchGroupByID)가 실패하면 로그 수준이 Warning으로 저하되고 프롬프트 텍스트가 수정됨.

**오류 수정**

- 익명의 사용자 또는 방문자 [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) 그룹 가입 실패 및 통계적 문제.
- 기타 알려진 문제.

### 2.5.1 @2020.3.5

**변경 사항**

[login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login)에 성공하면 로그인 계정의 반복 로그인을 식별하기 위해 `imResponse.data`콜백 객체에 키-값 쌍 `repeatLogin: true` 추가.

**오류 수정**

오디오/비디오 그룹(AVChatRoom)의 수신자 측에서 수신된 메시지의 우선 순위가 발신자 측에서 설정한 우선 순위와 상이함.

### 2.5.0 @2020.2.28

**새로운 기능**

- 네트워크 상태 변경 이벤트 [TIM.EVENT.NET_STATE_CHANGE](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.NET_STATE_CHANGE)가 추가되며, 액세스 측에서는 이 이벤트를 기반으로 관련 프롬프트 및 안내 생성 가능.

**변경 사항**
[오류 코드](https://web.sdk.qcloud.com/im/doc/en/global.html) 감소 및 최적화.

**오류 수정**

- [콘솔](https://console.cloud.tencent.com/im)에서 오디오/비디오 방(AVChatRoom)을 만들고 그룹 소유자를 지정한 후 그룹 소유자가 그룹에 가입한 후 다른 그룹 구성원이 보낸 메시지가 그룹 소유자 측에서 반복됨.
- [콘솔](https://console.cloud.tencent.com/im)에서 그룹을 생성하고 종료하거나 REST API를 자주 사용하는 경우 SDK가 [TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) 이벤트 미전달.
- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)가 때때로 그룹 메시지 목록 가져오기 실패.

### 2.4.2 @2020.2.7

**새로운 기능**
그룹 메시지에 대한 [메시지 우선 순위](https://intl.cloud.tencent.com/document/product/1047/33526), [열거 값](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_PRIORITY_HIGH) 및 [사용 사례](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage) 설정 가능.

### 2.4.1 @2020.1.14

**변경 사항**
익명의 사용자 또는 방문자는 [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) 그룹에만 가입 가능.

**오류 수정**

- 간헐적 일부 온라인 메시지를 가져올 수 없음.
- 오디오/비디오 그룹(AVChatRoom)에서 시스템 알림을 받은 후 [TIM.EVENT.MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED) 이벤트가 전달되지 않음.
- 일부 시나리오에서 그룹 메시지 회수 결과가 정확하지 않음.
- 기타 알려진 문제.

### 2.4.0 @2020.1.3

**새로운 기능**

- [revokeMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#revokeMessage) API가 추가됨.
- `isRevoked` 속성이 [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)에 추가됨. 속성 값 `true`는 회수된 메시지를 식별함.
- 메시지 회수 이벤트 알림 [TIM.EVENT.MESSAGE_REVOKED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_REVOKED)가 추가됨.
- 강제 로그아웃 이벤트 알림 [TIM.EVENT.KICKED_OUT](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.KICKED_OUT)에 [멀티 클라이언트 로그인으로 인한 강제 로그아웃](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.KICKED_OUT_MULT_ACCOUNT)과 [UserSig 만료로 인한 강제 로그아웃](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.KICKED_OUT_USERSIG_EXPIRED)이 추가됨.

**변경 사항**

- [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage)를 통해 업로드할 수 있는 최대 파일 크기가 20M에서 100M로 증가.
- [그룹 프롬프트](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload)의 `msgMemberInfo` 및 `shutupTime`은 더 이상 사용되지 않음. 대신 `memberList` 및 `muteTime`을 사용하십시오.

**오류 수정**

- [off](https://web.sdk.qcloud.com/im/doc/en/SDK.html#off) API를 호출하여 수신 이벤트를 취소할 수 없음.
- [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)의 `isRead` 속성 값과 유형이 올바르지 않음.
- 전송된 동영상 메시지의 동영상 파일이 최대 크기를 초과했을 때 오류 코드 및 오류 메시지가 잘못됨.
- 업데이트된 사용자 정의 필드의 내용이 때때로 잘못됨.
- [JOIN_STATUS_ALREADY_IN_GROUP](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.JOIN_STATUS_ALREADY_IN_GROUP) 이벤트는 사용자가 로그인하여 오디오/비디오 그룹에 가입할 때 간헐적 발생.
- core-js로 인해 잠재적인 성능 문제 발생.

### 2.3.2 @2019.12.18

**변경 사항**
[getUserProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserProfile) 및 [updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile)은 [사용자 정의 프로필 필드](https://intl.cloud.tencent.com/document/product/1047/33520) 지원.

**오류 수정**
[getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)를 사용하여 얻은 결합된 메시지에서 메시지 손실.

### 2.3.1 @2019.12.13

**새로운 기능**

- [createImageMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createImageMessage) 및 [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage)는 [File](https://developer.mozilla.org/en/docs/Web/API/File) 객체 전달 지원.
- [createFaceMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFaceMessage) API가 이모지 메시지를 생성하기 위해 추가됨.
- [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) 그룹에 대한 메시지 알림 효율성은 사용자 경험을 개선하도록 최적화됨.

**변경 사항**

- 메시지 전송에 실패하면 SDK는 실제 오류 코드와 오류 메시지 반환.
- [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout)이 호출되면 현재 인스턴스의 메시지 채널만 로그아웃됨.
- 액세스 사이드에서 전달한 콜백 함수가 보안을 위해 캡슐화되어 있고 콜백 함수의 논리가 올바르지 않은 경우 오류를 빠르게 캡처하고 찾을 수 있음.
- SDK는 [IM 서버 측 오류 코드](https://intl.cloud.tencent.com/document/product/1047/34348)를 수신할 때 중국어 오류 정보 제공.

**오류 수정**

- [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED)는 메시지가 전송될 때 여러 번 트리거됨.
- SDK는 [registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin)이 호출되지 않거나 잘못된 매개변수가 입력된 경우 이미지와 같은 파일이 업로드될 때 오류 보고됨.
- [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) 그룹이 해체된 후에도 긴 폴링 미중지.
- ‘다중 인스턴스’ 또는 ‘다중 클라이언트’ 로그인이 활성화된 경우 Web 인스턴스가 로그아웃된 후 다른 인스턴스 또는 클라이언트가 메시지를 받지 못함.
- 가져온 세션 목록의 구조로 인해 SDK에서 간헐적 오류 보고.

### 2.2.1 @2019.11.28

**변경 사항**
그룹 로밍 메시지를 가져오는 논리가 최적화됨.

**오류 수정**

- 오디오/비디오 그룹의 그룹 소유자가 그룹 프로필을 수정한 후 SDK에서 [오류 코드 2901](https://web.sdk.qcloud.com/im/doc/en/global.html) 보고.
- 그룹 관리자가 그룹 가입을 위해 앱을 처리한 후, 처리된 앱은 새로고침 후에 받을 수 있음.

### 2.2.0 @2019.11.21

**새로운 기능**

- [createVideoMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createVideoMessage) API를 통한 비디오 메시지 생성 및 전송 지원. 비디오 메시지는 플랫폼 간에 동기화 가능. 최신 버전의 [TUIKit 및 SDK](https://intl.cloud.tencent.com/document/product/1047/33996)로 업데이트해야 함.
- [getGroupMemberProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberProfile) API가 추가됨.
- Native IM v3.x에서 보낸 오디오 및 파일 메시지와 호환됨.
- 위치 메시지 [GeoPayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GeoPayload) 수신 가능.

**변경 사항**
최대 100개의 그룹을 로컬 저장소에 쓰기 가능. 100개 이상의 그룹이 있는 경우 SDK는 전체 그룹 목록을 작성하지 않음.

**오류 수정**

- [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) 그룹의 긴 폴링은 로그아웃 후에도 계속됨.
- [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) 그룹의 메시지 인스턴스에 있는 그룹 연락처 카드에 값이 없음.
- Internet Explorer 10을 사용할 때 오류 보고.
- 사용자는 익명으로 그룹에 가입할 수 없음.

### 2.1.4 @2019.11.7

**변경 사항**

- SDK API에서 반환된 `Promise` 상태가 `rejected`되면 SDK는 더 이상 [TIM.EVENT.ERROR](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.ERROR) 이벤트를 전달하지 않음.
- 사용자 Profile에 대한 업데이트는 즉시 로컬 캐시에 기록됨.

**오류 수정**

- Angular zone.js가 프로토타입 체인을 수정할 때 SDK 통합 후 코드 실행 실패.
- 그룹 소유자가 [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM) 그룹을 만들고 가입한 후 그룹 소유자는 메시지를 받을 수 없음.
- 그룹 목록이 너무 커서 초기화 실패.

### 2.1.3 @2019.10.31

**변경 사항**
REST API 호출 또는 레거시 IM 버전을 통해 전송된 결합된 메시지(하나의 메시지에 여러 메시지 요소) 호환. 자세한 내용은 [호환성 가이드](https://web.sdk.qcloud.com/im/doc/en/tutorial-01-faq.html)를 참고하십시오.

**오류 수정**

- 읽지 않은 개수가 정확하지 않음.
- 읽은 메시지가 리포트되지 않아 메시지가 무질서함.
- 빈 이미지 메시지가 성공적으로 전송되었지만 렌더링할 수 없음. SDK는 빈 이미지 메시지 전송을 지원하지 않음.
- 빈 파일 메시지가 잘못된 메시지 상태로 전송. SDK는 빈 파일 메시지 전송 미지원.
- [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList)가 호출될 때 SDK 코드 오류가 간헐적으로 보고됨.

### 2.1.2 @2019.10.25

**새로운 기능**
 [getGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupList)는 그룹 소유자 ID 및 그룹 구성원 수를 포함하여 그룹 프로필 정보 가져오기 지원.

**오류 수정**

- REST API를 사용하여 오디오/비디오 대화방에서 사용자 지정 그룹 알림을 보낼 때 SDK 코드 오류 보고.
- SDK는 사용자가 왼쪽 그룹에 다시 가입하고 getMessageList API를 호출할 때 기록 메시지를 가져오기 위한 요청 미전송.
- 업로드 실패 시 SDK 코드 오류 보고.

### 2.1.1 @2019.10.18

**새로운 기능**
[오디오 메시지 전송](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createAudioMessage) 지원. 오디오 메시지는 플랫폼 간에 동기화 가능. 최신 버전의 [TUIKit 및 SDK](https://intl.cloud.tencent.com/document/product/1047/33996)로 업데이트해야 함.

**오류 수정**
[getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)는 재가입 후에도 종료 그룹에서 기록 메시지를 가져올 수 있음.

### 2.1.0 @2019.10.16

**새로운 기능**

- Web은 [오디오 메시지](https://web.sdk.qcloud.com/im/doc/en/Message.html#.AudioPayload) 수신 지원.
- Web은 [비디오 메시지](https://web.sdk.qcloud.com/im/doc/en/Message.html#.VideoPayload) 수신 지원.

**변경 사항**

- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) API는 한 번에 최대 15개의 메시지를 가져올 수 있음.
- [TIM.TYPES.MSG_SOUND](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_SOUND)는 더 이상 사용되지 않으며 [TIM.TYPES.MSG_AUDIO](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_AUDIO)로 대체됨.

**오류 수정**

- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)는 삭제된 그룹 채팅에서 메시지를 가져올 수 없음.
- 그룹 시스템 알림에 그룹 이름이 포함되지 않음.
- 새 메시지를 받은 후 대화가 생성되었을 때 변환에 메시지 보낸 사람의 프로필이 없음.

### 2.0.11 @2019.10.12

**오류 수정**
React 프레임워크에서 이미지 메시지 발송 실패.

### 2.0.9 @2019.9.19

**새로운 기능**
이미지 메시지가 전송되기 전에 이미지의 실제 너비와 높이가 감지됨.

**변경 사항**

- HTTPS 프로토콜이 기본적으로 사용됨.
- [TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) 이벤트는 새 그룹 시스템 알림이 수신될 때 전송됨.

**오류 수정**

- 이미지 메시지 시작 화면 전송.
- JPG 또는 기타 이미지 전송에 실패했습니다.
