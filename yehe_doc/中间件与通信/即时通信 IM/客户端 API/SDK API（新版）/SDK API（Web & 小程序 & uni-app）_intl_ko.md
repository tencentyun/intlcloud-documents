## TIM

TIM은 IM Web SDK의 네임스페이스이며 SDK 인스턴스를 생성하기 위한 정적 메서드 [create()](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create), 이벤트 상수 [EVENT](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html) 및 유형 상수 [TYPES](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html)를 제공합니다.

**초기화**

| API   | 설명  |
| --- | --- |
| [create](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create) | SDK 인스턴스 생성. |

## SDK 인스턴스

| 기본 개념 | 설명 |
| :--- | :---- |
| Message(메시지) | IM SDK의 [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)는 보낼 내용을 나타내며 발신자, 발신자 계정, 메시지 생성 시간 등을 지정하는 여러 속성을 전달합니다. |
| Conversation(대화) | IM SDK의 [Conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html)은 두 가지 유형을 사용할 수 있습니다. <li> C2C(Client to Client): 두 명의 참가자만 참여하는 일대일 채팅입니다. </li><li> GROUP(그룹): 두 명 이상의 참가자가 참여하는 그룹 채팅입니다.</li> |
| Profile(프로필) | IM SDK의 [Profile](https://web.sdk.qcloud.com/im/doc/en/Profile.html)은 닉네임, 성별, 개인 서명, 프로필 사진 주소 등 사용자의 기본 정보를 설명합니다. |
| Friend(친구) | IM SDK의 [Friend](https://web.sdk.qcloud.com/im/doc/en/Friend.html)는 비고, 친구 목록 등 친구의 기본 정보를 설명합니다. |
| FriendApplication(친구 신청)| IM SDK의 [FriendApplication](https://web.sdk.qcloud.com/im/doc/en/FriendApplication.html)은 친구 요청의 기본 정보와 친구 출처, 비고 등을 설명합니다. |
| FriendGroup(친구 그룹)| IM SDK의 [FriendGroup](https://web.sdk.qcloud.com/im/doc/en/FriendGroup.html)은 친구 목록 이름 및 구성원을 포함하여 친구 목록의 기본 정보를 설명합니다.
| Group(그룹) | IM SDK의 [Group](https://web.sdk.qcloud.com/im/doc/en/Group.html)은 업무, 공개, 회의, AVChatRoom 등 그룹 채팅을 위한 커뮤니케이션 시스템을 의미합니다. |
| GroupMember(그룹 구성원) | IM SDK의 [GroupMember](https://web.sdk.qcloud.com/im/doc/en/GroupMember.html)는 ID, 닉네임, 역할, 그룹 가입 시간 등 각 그룹 구성원의 기본 정보를 나타냅니다. |
| 그룹 알림 | 그룹 구성원 추가 또는 삭제와 같은 이벤트가 발생하면 그룹 알림이 생성됩니다. 액세스 측은 그룹 구성원에게 그룹 알림을 표시할지 여부를 구성할 수 있습니다. <br/>그룹 알림 유형에 대한 자세한 내용은 [Message.GroupTipPayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload)를 참고하십시오.|
| 그룹 시스템 메시지 | 예를 들어 사용자가 그룹 가입을 요청하면 그룹 관리자는 시스템 메시지를 받습니다. 관리자가 요청을 수락하거나 거부하면 IM SDK는 결과를 액세스 측에 반환한 다음 결과를 사용자에게 표시합니다. <br/>그룹 시스템 메시지 유형에 대한 자세한 내용은 [Message.GroupSystemNoticePayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupSystemNoticePayload)를 참고핫십시오.  |
| 화면에 메시지 표시 | 텍스트 세그먼트 및 이미지를 포함하여 보낸 메시지는 컴퓨터 또는 휴대폰 화면에 표시됩니다. |

### 이벤트
| API   | 설명  |
| --- | --- |
| [on](https://web.sdk.qcloud.com/im/doc/en/SDK.html#on) | 이벤트 수신을 활성화합니다. |
| [off](https://web.sdk.qcloud.com/im/doc/en/SDK.html#off) | 이벤트 수신을 비활성화합니다. |

### 플러그인 등록
| API   | 설명  |
| --- | --- |
| [registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin) | 플러그인을 등록합니다. |

### 로그 레벨 설정
| API   | 설명  |
| --- | --- |
| [setLogLevel](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setLogLevel) | 로그 레벨을 설정합니다. |

### SDK 인스턴스 종료
| API   | 설명  |
| --- | --- |
| [destroy](https://web.sdk.qcloud.com/im/doc/en/SDK.html#destroy)  | 인스턴스를 종료합니다. |

### 로그인
| API   | 설명  |
| --- | --- |
| [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) | 로그인합니다. |
| [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout) | 로그아웃합니다. |

### 메시지
| API   | 설명  |
| --- | --- |
| [createTextMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage) | 텍스트 메시지를 생성합니다. |
| [createTextAtMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextAtMessage) |@ 알림 기능으로 문자 메시지를 작성합니다. |
| [createImageMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createImageMessage) | 이미지 메시지를 생성합니다. |
| [createAudioMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createAudioMessage) | 음성 메시지를 생성합니다. |
| [createVideoMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createVideoMessage) | 비디오 메시지를 생성합니다. |
| [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage) | 사용자 정의 메시지를 생성합니다. |
| [createFaceMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFaceMessage) | 이모티콘 메시지를 생성합니다. |
| [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage) | 파일 메시지를 생성합니다. |
| [createLocationMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createLocationMessage) | 지리적 위치 메시지를 생성합니다. |
| [createMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createMergerMessage) | 결합된 메시지를 생성합니다. |
| [downloadMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#downloadMergerMessage) | 결합된 메시지를 다운로드합니다. |
| [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage) | 포워딩 메시지를 생성합니다. |
| [sendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessage) | 메시지를 보냅니다. |
| [revokeMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#revokeMessage) | 메시지를 회수합니다. |
| [resendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#resendMessage) | 메시지를 다시 보냅니다. |
| [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage) | 메시지를 삭제합니다. |
| [setMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageExtensions) | 메시지 확장을 설정합니다. |
| [getMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageExtensions) | 메시지 확장을 가져옵니다. |
| [deleteMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessageExtensions) | 메시지 확장을 삭제합니다. |

### 대화
| API   | 설명  |
| --- | --- |
| [modifyMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#modifyMessage) | 메시지를 수정합니다.
| [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) | 메시지 목록을 가져옵니다.  |
| [getMessageListHopping](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageListHopping) | 지정된 sequence 또는 시간 범위로 대화 메시지 목록을 가져옵니다.|
| [sendMessageReadReceipt](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessageReadReceipt) | 메시지 수신 확인을 보냅니다.|
| [getMessageReadReceiptList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageReadReceiptList) | 메시지 수신 확인 목록을 풀링합니다.|
| [getGroupMessageReadMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList) | 그룹 메시지를 읽은(또는 읽지 않은) 구성원 목록을 가져옵니다.|
| [findMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#findMessage) | 지정된 대화의 로컬 메시지를 messageID로 쿼리합니다.|
| [setMessageRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRead) | 메시지를 읽은 상태로 설정합니다.  |
| [getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList) | 대화 목록을 가져옵니다. |
| [getConversationProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationProfile) | 대화 정보를 가져옵니다. |
| [deleteConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversation) | 대화를 삭제합니다. |
| [clearHistoryMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#clearHistoryMessage) | 일대일 또는 그룹 채팅의 로컬 및 클라우드 메시지를 지웁니다(대화는 삭제하지 않음). |
| [pinConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#pinConversation) | 대화를 상단에 고정/고정 해제합니다. |
| [setAllMessageRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setAllMessageRead) | 모든 대화의 읽지 않은 메시지를 읽은 것으로 표시합니다. |
| [setMessageRemindType](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRemindType) | 대화 메시지 알림 유형을 설정합니다. 이 API를 사용하여 ‘알림을 음소거’하거나 ‘메시지를 거부’할 수 있습니다. |
| [getTotalUnreadMessageCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTotalUnreadMessageCount) | 읽지 않은 세션의 총 수를 가져옵니다.|

### 대화 그룹
| API   | 설명  |
| --- | --- |
| [setConversationCustomData](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setConversationCustomData) | 사용자 정의 대화 데이터를 설정합니다.|
| [markConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markConversation) | 대화를 표시합니다. |
| [getConversationGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationGroupList) | 대화 그룹 목록을 가져옵니다.|
| [createConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createConversationGroup) | 대화 그룹을 생성합니다.|
| [deleteConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationGroup) | 대화 그룹을 삭제합니다.|
| [renameConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#renameConversationGroup) | 대화 그룹의 이름을 변경합니다.|
| [addConversationsToGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addConversationsToGroup) | 대화를 대화 그룹에 추가합니다.|
| [deleteConversationsFromGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationsFromGroup) | 대화 그룹에서 대화를 삭제합니다.|

### 프로필
| API   | 설명  |
| --- | --- |
| [getMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMyProfile) | 개인 프로필을 가져옵니다. |
| [getUserProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserProfile) | 다른 사용자의 프로필을 가져옵니다. |
| [updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile) | 개인 프로필을 업데이트합니다. |
| [getBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getBlacklist) | 블록리스트를 가져옵니다. |
| [addToBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addToBlacklist) | 블록리스트에 사용자를 추가합니다. |
| [removeFromBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#removeFromBlacklist) | 블록리스트에서 사용자를 제거합니다. |

### 사용자 상태
| API   | 설명  |
| --- | --- |
| [setSelfStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setSelfStatus) | 자신의 사용자 지정 상태를 설정합니다. |
| [getUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserStatus) | 사용자의 상태를 쿼리합니다. |
| [subscribeUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#subscribeUserStatus) | 사용자의 상태를 구독합니다. |
| [unsubscribeUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#unsubscribeUserStatus) | 사용자의 상태 구독을 취소합니다. |

### 관계 체인
| API   | 설명  |
| --- | --- |
| [getFriendList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendList) | SDK 캐시에 있는 친구 목록을 가져옵니다. |
| [addFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addFriend) | 친구를 추가합니다. |
| [deleteFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriend) | 친구를 삭제합니다. |
| [checkFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#checkFriend) | 친구를 인증합니다. |
| [getFriendProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendProfile) | 지정된 사용자의 친구 데이터 및 프로필 데이터를 가져옵니다. |
| [updateFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateFriend) | 친구의 관계 체인 데이터를 업데이트합니다. |
| [getFriendApplicationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendApplicationList) | SDK 캐시에 있는 친구 요청 목록을 가져옵니다. |
| [acceptFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#acceptFriendApplication) | 친구 요청을 수락합니다. |
| [refuseFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#refuseFriendApplication) | 친구 요청을 거부합니다. |
| [deleteFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriendApplication) | 친구 요청을 삭제합니다. |
| [setFriendApplicationRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setFriendApplicationRead) | 친구 요청을 읽음으로 설정합니다. |
| [getFriendGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendGroupList) | SDK 캐시에서 친구 목록을 가져옵니다. |
| [createFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFriendGroup) | 친구 목록을 생성합니다. |
| [deleteFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriendGroup) | 친구 목록을 삭제합니다. |
| [addToFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addToFriendGroup) | 친구 목록에 친구를 추가합니다. |
| [removeFromFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#removeFromFriendGroup) | 친구 목록에서 친구를 제거합니다. |
| [renameFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#renameFriendGroup) | 친구 목록의 이름을 수정합니다. |

### 그룹
| API   | 설명  |
| --- | --- |
| [getGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupList) | 그룹 목록을 가져옵니다. |
| [getGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupProfile) | 그룹 프로필을 가져옵니다. |
| [createGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createGroup) | 그룹을 생성합니다. |
| [dismissGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#dismissGroup) | 그룹을 삭제합니다. |
| [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateGroupProfile) | 그룹 프로필을 수정합니다. |
| [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup) | 그룹 가입을 신청합니다. |
| [quitGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#quitGroup) | 그룹을 종료합니다. |
| [searchGroupByID](https://web.sdk.qcloud.com/im/doc/en/SDK.html#searchGroupByID) | 그룹을 검색합니다. |
| [getGroupOnlineMemberCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupOnlineMemberCount) | 라이브 방송 그룹의 온라인 사용자 수를 가져옵니다. |
| [changeGroupOwner](https://web.sdk.qcloud.com/im/doc/en/SDK.html#changeGroupOwner) | 그룹 소유권을 이전합니다. |
| [getGroupApplicationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupApplicationList) | 그룹 가입 신청 목록을 가져옵니다.|
| [handleGroupApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#handleGroupApplication) | 그룹 가입 요청을 처리합니다. |
| [initGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#initGroupAttributes) | 그룹 속성을 초기화합니다. |
| [setGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupAttributes) | 그룹 속성을 설정합니다. |
| [deleteGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteGroupAttributes) | 그룹 속성을 삭제합니다. |
| [getGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupAttributes) | 그룹 속성을 가져옵니다. |

### 그룹 구성원
| API   | 설명  |
| --- | --- |
| [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList) | 그룹 구성원 목록을 가져옵니다. |
| [getGroupMemberProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberProfile) | 그룹 구성원의 프로필을 가져옵니다. |
| [addGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addGroupMember) | 그룹 구성원을 추가합니다. |
| [deleteGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteGroupMember) | 그룹 구성원을 삭제합니다. |
| [setGroupMemberMuteTime](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberMuteTime) |음소거 기간을 구성합니다.|
| [setGroupMemberRole](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberRole) | 그룹 구성원의 역할을 수정합니다. |
| [setGroupMemberNameCard](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberNameCard) | 그룹 구성원의 이름 카드를 설정합니다. |
| [setGroupMemberCustomField](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberCustomField) | 그룹 구성원에 대한 사용자 정의 필드를 설정합니다. |
| [markGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markGroupMemberList) | 그룹 구성원을 표시합니다.|

### 주제
| API   | 설명  |
| --- | --- |
| [getJoinedCommunityList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getJoinedCommunityList) | 현재 사용자가 가입한 커뮤니티 그룹 목록을 가져옵니다. |
| [createTopicInCommunity](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTopicInCommunity) | 주제를 생성합니다. |
| [deleteTopicFromCommunity](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteTopicFromCommunity) | 주제를 삭제합니다. |
| [updateTopicProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateTopicProfile) | 주제 프로필을 업데이트합니다. |
| [getTopicList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTopicList) |주제 목록을 가져옵니다.|
