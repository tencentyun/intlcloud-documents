## Discord 개요

Discord는 커뮤니티를 위해 설계된 무료 온라인 실시간 통화 소프트웨어 및 디지털 배포 플랫폼입니다. 게임, 교육 및 비즈니스 분야의 사용자는 소프트웨어의 채팅 채널에서 메시지, 이미지, 영상 및 음성을 통해 서로 통신할 수 있습니다.

## Discord 개념

### 서버

Discord에는 서버(커뮤니티와 유사)라는 일반적인 통신 소프트웨어 그룹과 다른 일종의 그룹 채팅이 있으며, 서버 소유자는 서버에서 자신의 커뮤니티를 만들 수 있습니다.

### 채널

서버에서 음성 및 텍스트 채널을 포함한 채팅 채널을 만들 수 있습니다. 음성 채널은 게임 방송, 채팅 등을 위해 사용할 수 있습니다. 다양한 권한을 ID 그룹과 통합하도록 채널을 설정하여 Discord 커뮤니티 시스템을 더욱 다양하게 만들 수 있습니다.

### 스레드

사용자는 스레드에서 특정 토픽에 대해 토론할 수 있습니다.

## 준비 작업

### Tencent Cloud IM 애플리케이션 생성

이 튜토리얼은 Tencent Cloud IM을 기반으로 합니다. 따라서 [Tencent Cloud IM 콘솔](https://console.cloud.tencent.com/im)에서 애플리케이션을 생성해야 합니다. 아래 이미지를 참고하십시오. 

애플리케이션이 성공적으로 생성되면 [IM 콘솔 애플리케이션의 기본 정보 페이지](https://console.cloud.tencent.com/im/detail)에서 애플리케이션의 기본 정보를 확인할 수 있습니다.

### 관련 구성 및 기능 이해

Tencent Cloud IM을 사용하여 Discord 기능을 구현하려면 Tencent Cloud IM과 관련된 기본 개념과 이 튜토리얼의 뒷부분에서 언급되는 몇 가지 고유 명사를 미리 이해해야 합니다. 다음을 포함하되 이에 국한되지 않습니다:

- SDKAppID: Tencent Cloud IM은 각 애플리케이션에 SDKAppID를 할당합니다. 애플리케이션의 SDKAppID는 애플리케이션이 콘솔에서 생성된 후 애플리케이션 세부 정보 페이지에서 볼 수 있으며 IM SDK를 초기화하고 사용자 로그인 티켓을 계산할 때 사용됩니다. 자세한 내용은 UISDK [초기화](https://intl.cloud.tencent.com/document/product/1047/47968) 및 [로그인](https://intl.cloud.tencent.com/document/product/1047/47971)을 참고하십시오.
- 키: 애플리케이션의 키는 Tencent Cloud IM 콘솔 애플리케이션 세부 정보 페이지에서 볼 수 있으며 사용자의 SDK 로그인 티켓을 계산하는 데 사용됩니다.
- 사용자 계정: Tencent Cloud IM 계정이 있는 사용자만 Tencent Cloud IM에 로그인할 수 있습니다. 사용자가 클라이언트 SDK를 통해 성공적으로 [Login](https://intl.cloud.tencent.com/document/product/1047/47971)하면 IM 백엔드가 사용자의 IM 계정을 자동으로 생성합니다. 또한 IM에서 제공하는 서버 API를 사용하여 [Importing a Single Account](https://intl.cloud.tencent.com/document/product/1047/34953)할 수 있습니다.
- 그룹: 지금까지 IM은 사용자가 메시지를 보내고 받을 수 있는 다양한 시나리오에 대해 [5가지 유형의 그룹](https://intl.cloud.tencent.com/document/product/1047/33529)을 제공합니다.
- 콜백 구성: IM에서 제공하는 클라이언트 및 서버 API를 사전에 통합할 수 있으며 IM은 특정 비즈니스 로직이 트리거될 때 필요한 정보를 서버에 자동으로 반환합니다. 채팅 콘솔의 [콜백 구성](https://console.cloud.tencent.com/im/callback-setting) 모듈에서 관련 구성을 완료하기만 하면 됩니다. IM은 다양한 콜백 구성을 제공하고 콜백 이벤트에 대한 높은 안정성을 보장합니다. 콜백를 사용하여 다양한 사용자 지정 요구 사항을 구현할 수 있습니다.
- 사용자 지정 필드: 기본적으로 Tencent Cloud IM은 개발자의 요구 사항을 대부분 충족하는 필드를 제공합니다. 또한 확장 필드에 대한 사용자의 요구를 충족하기 위해 각 모듈에 대해 다음과 같은 사용자 정의 필드를 제공합니다.
    - [사용자 지정 사용자 필드](https://console.cloud.tencent.com/im/user-data)
    - [사용자 지정 친구 필드](https://console.cloud.tencent.com/im/friends-diy-vars)
    - [사용자 지정 그룹 필드](https://console.cloud.tencent.com/im/qun-setting)
    - [사용자 지정 구성원 필드](https://console.cloud.tencent.com/im/qun-setting)
  >?사용자 지정 필드를 사용하려면 콘솔에서 구성한 다음 SDK\API를 통해 읽고 쓸 수 있습니다.

### 클라이언트&서버 SDK 통합

Discord 관련 기능을 구현하려면 Tencent Cloud IMSDK를 통합해야 합니다. IM은 다양하고 사용하기 쉬운 SDK와 서버 API를 제공합니다. 동일한 SDKAppID로 애플리케이션에 로그인하면 메시지가 클라이언트 간에 동기화됩니다. 비즈니스 요구 사항 시나리오 및 기술 스택에 따라 적절한 SDK를 선택합니다.

## Discord 기능 분석 

상기 이미지에서 볼 수 있듯이 Discord 기능에는 서버, 채널 및 스레드가 포함됩니다. 각기 다른 콘텐츠에는 다른 서버가 사용됩니다. 예를 들어 Honor of Kings 서버와 Game for Peace 서버가 있습니다. 문자 채널, 음성 채널, 알림 채널 등 다양한 형태의 채널을 서버에서 생성할 수 있으며 사용자는 채널에서 서로 통신합니다. 특정 토픽에 대해 더 많은 아이디어가 있는 경우 추가 토론을 위한 스레드를 만들 수 있습니다. 다음은 Tencent Cloud IM을 통해 이러한 주요 Discord 기능을 구현하는 방법을 하나씩 소개합니다.

>?**코드 데모의 경우 Android 클라이언트(Java SDK)를 예로 사용합니다. 다른 SDK 버전의 API 호출은 [통합 솔루션(UI 없음)](https://intl.cloud.tencent.com/document/product/1047/34306)을 참고하십시오.**

### 서버

#### 서버 생성 

분석 결과 Discord 서버 목록의 다음과 같은 특징을 알 수 있습니다.

1. 서버에는 방대한 수의 사용자가 있을 수 있습니다.
2. 사용자는 실제로 서버에서 서로 통신하지 않습니다. 대신 서버의 채널이나 스레드에서만 채팅합니다.
3. 서버의 채팅 메시지 기록은 로밍 서버에 저장해야 합니다.
4. 자유롭게 액세스할 수 있습니다.
5. 서버에서 채널을 생성할 수 있습니다.

IM은 5가지 유형의 그룹을 제공하지만 [커뮤니티 그룹(Community)](https://intl.cloud.tencent.com/document/product/1047/33529)만이 Discord 서버의 특성을 충족합니다. IM 커뮤니티 그룹은 사용자가 자유롭게 가입 및 탈퇴할 수 있으며 최대 10만 명의 구성원을 지원하고 메시지 기록을 저장합니다. 그룹에 가입하려면 사용자는 그룹 ID를 검색하고 신청해야 하며, 신청서는 관리자의 승인 없이 그룹에 가입할 수 있습니다.

createGroup API를 사용하여 서버(그룹)를 생성할 수 있습니다. 그룹 유형은 Community 이고 [setSupportTopic](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html#af97a85fc91302dbbdf0f6c0a0a022ccd)이 true로 설정되어야 서버에서 채널이 생성될 수 있습니다. 다음은 샘플 코드입니다.

```java
V2TIMGroupInfo  groupinfo = new V2TIMGroupInfo();
groupinfo.setGroupName("테스트 서버");
groupinfo.setSupportTopic(true);
// 초기 그룹 구성원
List<V2TIMCreateGroupMemberInfo> memberList = new LinkedList<V2TIMCreateGroupMemberInfo>();
// 서버 프로필 사진과 같은 기타 구성
V2TIMManager.getGroupManager().createGroup(groupinfo, memberList, new V2TIMValueCallback<String>() {
            @Override
            public void onError(int i, String s) {
                // 생성 실패
            }

            @Override
            public void onSuccess(String s) {
            	// 생성 성공, 서버 ID가 반환됩니다
            }
});
```

API가 성공적으로 호출되면 onSuccess 콜백에 서버 ID가 반환되며 이는 나중에 서버에서 채널을 생성할 때 사용됩니다.

>!IM에서 제공하는 [서버 생성 API](https://intl.cloud.tencent.com/document/product/1047/34895)를 이용해도 됩니다. 주요 매개변수는 다음과 같습니다.
>
>```json
{
    "Type": "Community", // 그룹 유형(필수)
    "Name": "TestCommunityGroup", // 그룹 이름(필수)
    "SupportTopic": 1            // 토픽 옵션 지원 여부. 유효한 값: 1 yes, 0 no
}
```

###### 서버 목록

Discord의 맨 왼쪽에는 현재 사용자가 가입한 서버 목록이 있습니다. 커뮤니티 시나리오의 경우, Tencent Cloud IM은 서버 목록 조회 전용 API를 제공합니다.

```java
V2TIMManager.getGroupManager().getJoinedCommunityList(new V2TIMValueCallback<List<V2TIMGroupInfo>>() {
            @Override
            public void onSuccess(List<V2TIMGroupInfo> v2TIMGroupInfos) {
                // 서버 목록 가져오기 성공, 반환된 List<V2TIMGroupInfo>에 서버 목록의 기본 정보가 제공됩니다.
            }

            @Override
            public void onError(int i, String s) {
              // 서비스 목록 가져오기 실패
            }
});
```

반환된 [V2TIMGroupInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html)는 기본 서버 정보를 제공합니다. 그러나 반환된 서버 정보에는 읽지 않은 메시지 수 및 사용자 지정 상태와 같은 정보가 포함되지 않습니다. Discord에서와 동일한 효과를 얻으려면 IM에서 제공하는 다른 API를 사용하여 서버 목록에 대한 읽지 않은 메시지 수를 구현해야 합니다. 본 문서의 뒷부분에서 이에 대해 설명합니다.

#### 서버 카테고리

서버가 생성되면 기본 카테고리가 생성됩니다. 서버가 생성된 후 새 카테고리를 생성할 수 있습니다. Tencent Cloud IM에서 서버는 본질적으로 커뮤니티입니다. 따라서 커뮤니티 그룹에 대한 사용자 정의 필드를 설정하여 서버 유형 기능을 구현할 수 있습니다. 사용자 정의 그룹 필드를 사용하려면 아래 2단계를 수행하십시오.

1. 콘솔에서 사용자 정의 필드 key를 활성화합니다.
2. 클라이언트 SDK\서버 API를 사용하여 사용자 지정 필드를 읽고 씁니다. 

[서버 API](https://intl.cloud.tencent.com/document/product/1047/34962)와 [클라이언트 SDK](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad4ceef92975fa00c4a5dddc8f7e1edcf)를 이용하여 사용자 지정 그룹 필드를 설정합니다.

>!커뮤니티 그룹 기능은 프리미엄 에디션에서만 사용할 수 있습니다. 커뮤니티 그룹에 대한 사용자 지정 필드를 설정하기 전에 프리미엄 에디션을 구입해야 합니다.

#### 서버의 읽지 않은 메시지 수&사용자 지정 상태 표시

![image-20221205031412051](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-12-04-191412.png)

![image-20221205031429070](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-12-04-191429.png)

이전에 언급했듯이, 가입한 서버 목록을 가져오는 API는 읽지 않은 메시지 수 및 서버 상태와 같은 정보를 반환하지 않습니다. 이 데이터를 가져오는 것뿐만 아니라 이 데이터의 변경을 수신하여 클라이언트 UI를 적시에 업데이트해야 합니다. 서버는 IM 커뮤니티 그룹에 의해 구현되며, IM에서 커뮤니티 그룹은 대화를 생성하지 않으므로 모든 공개 및 비공개 채널 대화의 읽지 않은 메시지 수의 합계를 계산해야 합니다. [V2TIMTopicInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html)의 [getUnreadCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html#ac2e3266d20b348145d75079020ac50c7) API를 사용하여 공개 채널의 읽지 않은 메시지 수를 가져오고, 비공개 채널의 읽지 않은 메시지 수는 work 그룹을 통해 구현되기 때문에, [getConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a619aaff2bb5664e094d2341819b95096) API를 사용하여 가져옵니다.

```java
// 공개 채널
List<String> conversationIDList = new LinkedList();
conversationIDList.add("GROUP_$GROUPID");
V2TIMManager.getConversationManager().getConversationList(conversationIDList, new V2TIMValueCallback<List<V2TIMConversation>>() {
            @Override
            public void onError(int i, String s) {
                // 서버의 대화 정보 가져오기 실패
            }

            @Override
            public void onSuccess(V2TIMConversationList List<V2TIMConversation>) {
               // 서버의 대화 정보 가져오기 완료
            }
});
// 비공개 채널
V2TIMManager.getGroupManager().getTopicInfoList(groupID, topicIDList, new V2TIMValueCallback<List<V2TIMTopicInfoResult>>() {
                @Override
                public void onSuccess(List<V2TIMTopicInfoResult> v2TIMTopicInfoResults) {
                    
                }

                @Override
                public void onError(int i, String s) {
                }
});
```

서버에 대한 사용자 지정 상태 기능을 구현하기 위해 [setConversationCustomData](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ac11ca7227145e3f359f6a3473ed600a5) API를 사용하여 사용자 지정 서버 대화 데이터를 설정할 수 있습니다.

```java
List<String> conversationIDList = new LinkedList();
String customData = "통화 중"
V2TIMManager.getConversationManager().setConversationCustomData(conversationIDList, customData, new V2TIMValueCallback<List<V2TIMConversationOperationResult>>() {
            @Override
            public void onSuccess(List<V2TIMConversationOperationResult> v2TIMConversationOperationResults) {
                // 사용자 지정 그룹 대화 데이터 설정 성공
            }

            @Override
            public void onError(int i, String s) {
                // 사용자 지정 그룹 대화 데이터 설정 실패
            }
});
```

서버 대화와 관련된 데이터가 변경되면 클라이언트는 UI 표시 업데이트를 시도해야 합니다. 서버 대화 변경 사항을 수신하기 위해 IM은 해당 이벤트 리스너 함수 [addConversationListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4)를 제공합니다. 이 콜백 함수는 다음과 같은 경우에 트리거됩니다.

1. 서버 메시지 추가, 삭제 또는 수정
2. 읽지 않은 서버 메시지 수 변경
3. 사용자 지정 서버 정보 수정
4. 서버 상단 고정
5. 서버 메시지 수신 구성 수정
6. 서버 마크 수정
7. 서버 그룹 수정
8. ...

```java
V2TIMConversationListener conversationLister = new V2TIMConversationListener() {
            @Override
            public void onSyncServerStart() {
            }

            @Override
            public void onSyncServerFinish() {
            }

            @Override
            public void onSyncServerFailed() {
            }

            @Override
            public void onNewConversation(List<V2TIMConversation> conversationList) {
            }

            @Override
            public void onConversationChanged(List<V2TIMConversation> conversationList) {
            }
            @Override
            public void onTotalUnreadMessageCountChanged(long totalUnreadCount) {
            }

            @Override
            public void onConversationGroupCreated(String groupName, List<V2TIMConversation> conversationList) {
            }

            @Override
            public void onConversationGroupDeleted(String groupName) {
            }

            @Override
            public void onConversationGroupNameChanged(String oldName, String newName) {
            }

            @Override
            public void onConversationsAddedToGroup(String groupName, List<V2TIMConversation> conversationList) {、
            }

            @Override
            public void onConversationsDeletedFromGroup(String groupName, List<V2TIMConversation> conversationList) {
            }
}
V2TIMManager.getConversationManager().addConversationListener(conversationLister);
```

상기 내용을 요약하면, getJoinedCommunityList 및 getConversationList API와 addConversationListener 콜백을 사용하여 Discord의 서버 목록을 표시 기능을 구현할 수 있습니다.

### 채널

서버에 여러 채널을 생성할 수 있습니다. 아래 이미지와 같이 서버 아래에 4개의 채널이 생성되고 4개의 채널이 2개의 카테고리에 배치됩니다. 

사용자는 다른 사람을 채널에 초대하고 채널의 기본 설정을 수정할 수 있습니다. 사용자는 대부분의 채팅을 채널 내에서 진행하므로, 채널 기능은 Discord에서 가장 중요합니다. Discord의 채널 기능은 Tencent Cloud IM의 토픽 기능에 해당합니다. IM의 커뮤니티 그룹은 그룹 내 토픽 생성 기능을 제공합니다.

#### 기본 채널

서버가 생성되면 Discord는 서버에 대해 4개의 기본 채널을 생성합니다. Tencent Cloud IM도 이러한 기능을 구현할 수 있습니다. 프로세스는 다음과 같습니다.

1. [그룹 생성 후 콜백](https://console.cloud.tencent.com/im/callback-setting)을 통해 서버 생성 성공을 비즈니스 서버에 알립니다.
2. 비즈니스측은 생성된 그룹이 커뮤니티 그룹인지 판단하여 다른 그룹과 관련된 비즈니스에 영향을 미치지 않도록 합니다.
3. 서버 속성을 기반으로 서버에서 [Creating Topic](https://intl.cloud.tencent.com/document/product/1047/49471)합니다.

서버 토픽 생성 매개변수는 다음과 같습니다.

```json
{
    "GroupId": "@TGS#_@TGS#cQVLVHIM62CJ", // 토픽의 그룹 ID(필수)
    "TopicId": "@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic",     // 사용자 지정 토픽 ID(옵션)
    "TopicName": "TestTopic",         // 토픽 이름(필수)
    "From_Account": "1400187352", // 토픽을 생성하는 구성원
    "CustomString": "This is a custom string",    // 사용자 지정 문자열
    "FaceUrl": "http://this.is.face.url", // 토픽 프로필 사진 URL(옵션)
    "Notification": "This is topic Notification", // 토픽 알림(옵션)
    "Introduction": "This is topic Introduction" // 토픽 소개(옵션)
}
```

![image-20221205094226037](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-12-05-014226.png)

#### 채널 생성

Discord 클라이언트에서 사용자는 아래 이미지와 같이 다양한 채널 카테고리 아래에 채널을 만들 수 있습니다. 

Discord에서의 채널 생성은 IM의 커뮤니티 그룹에서의 토픽 생성과 같습니다. IM에서 토픽 생성 시 토픽의 카테고리와 기본 정보를 설정할 수 있습니다. 

[createTopicInCommunity](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a52eed1b07ad64a3aa3d3561d8cd147f0) API를 사용하여 관련 기능을 구현할 수 있습니다.

```java
String groupID = "서버 ID"
V2TIMTopicInfo info = new V2TIMTopicInfo();
info.setCustomString("{'categray':'게임','type':'text'}") // // 채널 카테고리 및 유형 설정
// V2TIMTopicInfo 기본 정보 설정
V2TIMManager.getGroupManager().createTopicInCommunity(groupID, info, new V2TIMValueCallback<String>() {
            @Override
            public void onSuccess(String s) {
                // 채널 생성 성공
            }

            @Override
            public void onError(int i, String s) {
                // 채널 생성 실패
            }
});
```

채널 생성 시 [V2TIMTopicInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html) 메소드를 호출하여 채널 정보를 설정하고 [setCustomString](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html#aad0cc8249c21c5ccae385fdfb8ba32ea) API를 호출하여 채널 카테고리 및 유형을 설정할 수 있습니다. 

채널을 생성할 때 비공개 채널 여부를 지정할 수 있습니다. 비공개 채널은 일반 채널과 다릅니다.

1. 사용자가 서버에 가입한 후, 비공개 채널에 가입되지 않습니다.
2. 사용자는 서버 관리자가 초대한 경우에만 비공개 채널에 참여할 수 있습니다.

따라서 work 그룹을 사용하여 비공개 채널 기능을 구현할 수 있습니다. 그러나 서버와 바인딩된 비공개 채널에 대한 정보는 비즈니스측에 저장되어야 합니다.

#### 채널 유형

Discord에서 채널을 생성할 때 채널 유형을 음성 또는 텍스트로 설정할 수 있습니다. 텍스트 채널은 텍스트, 이모티콘, 이미지를 기반으로 채팅이 가능하고 음성 채널은 음성/영상 채팅이 가능합니다. 사용자는 동시에 하나의 음성 채널에만 참여할 수 있습니다. 새로운 음성 채널에 참여하려면 사용자는 현재 참여하고 있는 음성 채널에서 나가야 합니다. 

다음 4가지 사항에 주의하십시오.

1. 채널 생성 시 채널 유형을 설정해야 합니다. 채널 생성 섹션에서 설정 방법을 찾으실 수 있습니다.
2. 사용자가 음성 채널에 참여할 때 시스템은 사용자가 이미 다른 음성 채널에 있는지 확인해야 합니다.
3. 음성 채널은 전역적입니다.
4. Tencent Cloud IM은 현재 사용자 음성 채널 참여 여부와 어떤 음성 채널에 참여 중인지 쿼리하는 API를 제공하지 않습니다. 해당 관련 데이터는 비즈니스측에서 유지 관리해야 합니다.

상기 4번 사항과 관련하여 개발자는 Tencent Cloud IM에서 제공하는 그룹 참여 및 탈퇴 콜백을 사용하여 사용자의 음성 채널 상태를 유지하고 비즈니스측에 상태를 저장할 수 있습니다. Tencent Cloud IM에서 제공하는 콜백에는 지연이 있을 수 있습니다. 즉, 사용자가 한 음성 채널을 떠난 후 짧은 시간 동안 다른 음성 채널에 참여하지 못할 수 있습니다. 따라서 이 문제를 해결하기 위해 클라이언트를 사용하여 사용자의 음성 채널 참여 또는 퇴장 상태를 비즈니스 서버에 실시간으로 리포트할 수도 있습니다.

#### 채널에 사용자 초대

사용자의 채널 참여는 다음 세 가지 방법이 있습니다.

1. 다른 사용자의 초대를 받아 서버에 가입합니다. 사용자가 서버에 가입하면 사용자는 서버의 모든 공개 채널에 가입됩니다.
2. 서버 검색을 통해 서버에 가입합니다.
3. 서버 관리자의 초대를 받아 비공개 채널에 가입합니다.

커뮤니티의 특성에 따라 사용자는 서버에 가입하기만 하면 공개 채널에 가입할 수 있습니다.

1. 정확한 그룹 ID 검색을 통한 서버 가입을 지원합니다.
2. 초대를 통한 서버 가입을 지원합니다.
3. 서버 가입 신청을 지원하며 승인이 필요하지 않습니다.



#### 채널 설정

채널을 음소거 또는 음소거 해제하고 채널에 대한 알림을 구성할 수 있습니다. 해당 API는 각각 [setAllMute](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html#a13fbe06ce357215cfd7053954552030b) 및 [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e)입니다.

```java
// 기본 채널 정보 설정
V2TIMManager.getGroupManager().setTopicInfo(topicInfo, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        // 설정 완료
    }

    @Override
    public void onError(int i, String s) {
        // 설정 실패
    }
});
```

```java
// 해당 채널의 메시지 수신 옵션 설정
String groupID = "topicid"
int opt = 0; 
V2TIMManager.getMessageManager().setGroupReceiveMessageOpt(groupID, opt, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

#### 채널 메시지 목록

[getHistoryMessageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a97fe2d6a7bab8f45b758f84df48c0b12) API를 사용하여 채널의 기록 메시지를 가져올 수 있습니다.

```java
final V2TIMMessageListGetOption option = new V2TIMMessageListGetOption();
option.setGroupID("채널 ID");
option.setCount(20);
// 기타 구성
V2TIMManager.getMessageManager().getHistoryMessageList(option, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        // 채널 기록 메시지 가져오기 완료
    }

    @Override
    public void onError(int code, String desc) {
        // 채널 기록 메시지 가져오기 실패
    }
});
```

#### 채널의 읽지 않은 메시지 수

채널의 읽지 않은 메시지 수는 서버의 읽지 않은 메시지 수와 다릅니다. 서버의 읽지 않은 메시지 수는 대화 정보에 있고 채널의 읽지 않은 메시지 수는 채널 기본 정보에 있습니다. Tencent Cloud IM에서 제공하는 그룹 콜백 [onTopicInfoChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a29285e4e127337e299bd2b695a1afdeb)를 사용하여 읽지 않은 메시지 수를 실시간으로 가져올 수 있습니다.

```java
String groupID = "서버 ID";
List< String > topicIDList= new LinkedList(); // 채널 메시지 목록
V2TIMManager.getGroupManager().getTopicInfoList(groupID, topicIDList, new V2TIMValueCallback<List<V2TIMTopicInfoResult>>() {
    @Override
    public void onSuccess(List<V2TIMTopicInfoResult> v2TIMTopicInfoResults) {
        // 채널 ID, 이름, 읽지 않은 메시지 수와 같은 채널 정보 가져오기
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

#### 채널 구성원 목록

서버에 가입하는 사용자는 기본적으로 서버 아래의 모든 공개 채널에 가입됩니다. 따라서 공개 채널 구성원 목록을 가져오려면 서버의 그룹 구성원 목록만 가져오면 됩니다. 다음은 공개 채널 구성원 목록을 가져오는 방법입니다.

```java
String groupID = "서버 ID";
int filter = 0; // 그룹 구성원 역할: 관리자, 일반 구성원...
long nextSeq = 0;// 페이징 매개변수
V2TIMManager.getGroupManager().getGroupMemberList(groupID, filter, nextSeq , new V2TIMValueCallback<V2TIMGroupMemberInfoResult>() {
    @Override
    public void onError(int i, String s) {
        CommonUtil.returnError(result,i,s);
    }

    @Override
    public void onSuccess(V2TIMGroupMemberInfoResult v2TIMGroupMemberInfoResult) {
        
    }
});
```

비공개 채널의 구성원 목록을 가져오려면 [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) API를 호출하여 비공개 채널의 그룹 ID를 전달하면 됩니다.

### 스레드

스레드는 채널의 특정 토픽에 대한 토론 그룹입니다. 사용자는 스레드 내의 특정 토픽에 대한 메시지를 찾아볼 수 있으며, 스레드 요약은 채널의 메시지 목록에서도 볼 수 있습니다. 스레드도 Tencent Cloud IM에서 그룹으로 간주됩니다.

#### 스레드 생성

스레드는 별도로 생성하거나 채널의 메시지와 바인딩하여 생성할 수 있습니다. Tencent Cloud IM에서 제공하는 createGroup API를 사용하여 스레드를 생성할 수 있습니다. 다음 사항에 주의하십시오.

1. 스레드가 생성되면 기본적으로 현재 서버의 모든 구성원이 스레드에 있습니다.
2. 스레드가 생성된 후 서버에 가입한 구성원도 스레드에 추가됩니다.
3. 나중에 스레드에 참여하는 사용자는 스레드가 생성된 이후의 스레드 채팅 기록을 볼 수 있습니다.

상기 내용을 요약하면, 스레드/그룹이 생성되면 서버의 그룹 구성원이 스레드에 추가되고, 사용자가 서버에 참여하려면 사용자 그룹 참여 콜백에서 서버의 모든 스레드에 사용자를 추가해야 합니다. 다음 API를 사용하여 비즈니스 서버 측에서 이 두 단계를 구현하는 것이 가장 좋습니다.

1. [Getting Group Member Profiles](https://intl.cloud.tencent.com/document/product/1047/34948).
2. [Creating a Group](https://intl.cloud.tencent.com/document/product/1047/34895).
3. [Adding Group Members](https://intl.cloud.tencent.com/document/product/1047/34921).

서버 측 콜백은 [After a User Joins a Group](https://intl.cloud.tencent.com/document/product/1047/34372) 콜백입니다.

#### 스레드 수

채널 목록에서 채널의 스레드 목록을 가져올 수 있습니다. 따라서 스레드와 서버 간에 다대일 관계를 설정해야 합니다. 스레드에 기록 메시지가 있는 경우 스레드와 메시지 간의 일대일 관계도 설정해야 합니다. Tencent Cloud IM은 현재 이러한 관계를 설정할 수 있는 기능을 제공하지 않으므로, 비즈니스측에서 이러한 관계를 유지 관리해야 합니다. 비즈니스측에서 제공하는 HTTP API를 사용하여 스레드 수와 스레드 목록을 가져오고, 온라인 메시지 전송을 통해 스레드 목록을 실시간으로 업데이트할 수 있습니다.

#### 스레드 요약

사용자가 메시지에 대한 스레드를 생성하면 사용자는 메시지 목록에서 다음과 같은 메시지 요약 정보를 볼 수 있습니다.

1. 스레드 메시지 수.
2. 스레드 lastMessage 관련 정보.
3. 기타 실시간으로 메시지 목록에 표시되어야 하는 정보

스레드 메시지 요약 기능을 구현하려면 그룹 메시지 전송 콜백 및 메시지 편집 기능을 사용해야 합니다. 사용자가 스레드에서 메시지를 보낸 후, IM 서비스는 메시지 전송 콜백을 트리거하고 관련 정보를 비즈니스측에 동기화합니다. 그 다음 비즈니스는 스레드의 메시지 수를 세고, lastMessage 정보를 유지하는 동시에 메시지 편집 API를 통해 정보를 메시지에 저장합니다.

### 메시지 관련

#### 메시지 피드백

메시지 피드백은 아래 이미지와 같이 사용자를 위한 메시지의 확장입니다. 

모든 유형의 메시지는 편집 및 피드백이 지원되며, 커뮤니티 그룹 지원이 필요하므로 cloudCustomData 필드에 데이터를 저장하는 것이 좋습니다. 다음은 자세한 데이터 저장 형식(참고용)입니다.

```json
{
  "reaction": {
    "simle":["user1","user2"]
  }
}
```

```java
V2TIMManager.getMessageManager().modifyMessage(modifiedMessage, new V2TIMCompleteCallback<V2TIMMessage>() {
    @Override
    public void onComplete(int i, String s, V2TIMMessage v2TIMMessage) {
        // 메시지 수정 완료
    }
});
```

#### 메시지 편집

메시지 편집은 메시지 피드백과 동일하게 작동하며, 구성된 사용자 지정 데이터의 몇 가지 차이점만 있습니다. 모든 메시지의 편집을 지원하려면 cloudCustomData 필드에서 데이터를 편집하는 것이 좋습니다. 데이터 형식은 다음과 같습니다.

```json
{
  "isEdited": true
}
```

```java
V2TIMManager.getMessageManager().modifyMessage(modifiedMessage, new V2TIMCompleteCallback<V2TIMMessage>() {
    @Override
    public void onComplete(int i, String s, V2TIMMessage v2TIMMessage) {
        // 메시지 편집 완료
    }
});
```

#### 메시지 별표  

메시지 별표는 다른 사용자가 별표 표시된 메시지를 볼 수 있도록 그룹 채팅에서 메시지에 별표를 표시하는 것입니다. 커뮤니티 그룹은 그룹 속성을 지원하지 않으므로 사용자 지정 메시지를 사용하여 메시지 별표 기능을 구현합니다.

사용자 지정 그룹 메시지를 사용하려면 먼저 [Tencent Cloud IM 콘솔](https://console.cloud.tencent.com/im/qun-setting)에서 아래 이미지와 같이 구성해야 합니다.

그 다음 다음과 같이 설정합니다.

```java
V2TIMGroupInfo info =  new V2TIMGroupInfo();
info.setCustomInfo("pin data");
V2TIMManager.getGroupManager().setGroupInfo(info, new V2TIMCallback() {
    @Override
    public void onError(int i, String s) {
        // 설정 실패
    }

    @Override
    public void onSuccess() {
        // 설정 성공
    }
});
```

설정 성공 후 그룹 구성원은 [onMemberInfoChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a4ac777faad07e32408ae7ef5e2e3fc86) 이벤트를 수신할 수 있으며 오프라인 사용자도 그룹 프로필을 통해 별표 표시된 메시지 콘텐츠를 얻을 수 있습니다.

```java
List< String > groupIDList = new LinkedList();
V2TIMManager.getGroupManager().getGroupsInfo(groupIDList, new V2TIMValueCallback<List<V2TIMGroupInfoResult>>() {
    @Override
    public void onError(int i, String s) {
        
    }

    @Override
    public void onSuccess(List<V2TIMGroupInfoResult> v2TIMGroupInfoResults) {
        
    }
});
```

사용자 지정 필드는 현재 채널이 아닌 서버에서만 구성할 수 있습니다.

#### 입력 중 상태

친구가 입력 중일 때 다른 클라이언트의 사용자는 상기 이미지와 같이 사용자의 입력 중 상태를 볼 수 있습니다. Tencent Cloud IM의 온라인 메시지 기능을 사용하여 이 기능을 구현할 수 있습니다. 입력 중 상태 메시지는:

1. 온라인 사용자만 받을 수 있습니다.
2. 로밍 서버에 저장되지 않습니다.

또한 성능 향상을 위해 다음과 같이 최적화되었습니다.

- 입력 중 상태 메시지 전송은 두 사용자가 20s 이내에 서로 메시지를 보낸 경우에만 트리거됩니다.
- 동일한 문자 메시지는 온라인 메시지 전송을 여러 번 트리거하지 않습니다.

### 비공개 메시지

비공개 메시지는 Discord 사용자 간 전송하는 메시지이며, 친구 여부는 관계가 없습니다.

- 친구가 아닌 다른 사용자에게 비공개 메시지를 보내려면 해당 사용자의 사용자 ID를 알아야 하며, Tencent Cloud IM 콘솔에서 [메시지 전송 점검](https://console.cloud.tencent.com/im/login-message)을 비활성화해야 합니다. 그렇지 않으면 메시지 전송에 실패합니다.
- 또는 [addFriend](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208) API를 호출하여 해당 사용자를 친구로 추가하고 [getFriendList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae478de55db21d42b72a6c5a6a5d16624) API를 사용하여 연락처를 가져올 수 있습니다.

관련 코드는 다음과 같습니다.

```java
// 친구 추가
V2TIMManager.getFriendshipManager().addFriend(info, new V2TIMValueCallback<V2TIMFriendOperationResult>() {
            @Override
            public void onError(int i, String s) {
                // 친구 추가 실패
            }

            @Override
            public void onSuccess(V2TIMFriendOperationResult v2TIMFriendOperationResult) {
               // 친구 추가 성공
            }
});
```

```java
// 연락처 가져오기
V2TIMManager.getFriendshipManager().getFriendList(new V2TIMValueCallback<List<V2TIMFriendInfo>>() {
            @Override
            public void onError(int i, String s) {
               // 연락처 가져오기 실패
            }

            @Override
            public void onSuccess(List<V2TIMFriendInfo> v2TIMFriendInfos) {
               // 연락처 가져오기 성공
            }
});
```

### 마이페이지

#### 온라인 상태 
Discord 사용자 패널의 온라인 상태 기능은 Tencent Cloud IM에서 제공하는 온라인 상태 API로 다음과 같이 구현할 수 있습니다.

- [setSelfStatus](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7520045679f1493c890f2b3b5eee7b84)를 통해 자신만의 사용자 지정 온라인 상태를 설정하기 위한 API입니다. 사용자의 온라인/오프라인 상태는 Tencent Cloud IM에서 설정하며 개발자가 수정할 수 없습니다.
- [getUserStatus](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a2428c7f87859dd85bed1730ad8d3b92a)를 통해 친구의 온라인 상태를 가져옵니다.
- [onUserStatusChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94251d1971d7b6692b3278ed0d42b73e)를 통해 친구의 온라인 상태 변경을 수신합니다.

관련 코드는 다음과 같습니다.

```java
// 자신의 온라인 상태 설정
V2TIMUserStatus customStatus = new V2TIMUserStatus();
V2TIMManager.getInstance().setSelfStatus(customStatus, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

```java
// 친구의 온라인 상태 가져오기
List<String> userIDList = new LinkerList();
V2TIMManager.getInstance().getUserStatus(userIDList, new V2TIMValueCallback<List<V2TIMUserStatus>>() {
    @Override
    public void onSuccess(List<V2TIMUserStatus> v2TIMUserStatuses) {
       
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

#### 개인 정보 관련

개인 정보 관련 기능은 Tencent Cloud IM에서 제공하는 관계 체인 관련 API로 다음과 같이 구현할 수 있습니다.

- 사용자 프로필 가져오기 [getUsersInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e).
- 사용자 프로필 설정 [setSelfInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a).

```java
// 사용자 프로필 설정
final V2TIMUserFullInfo userFullInfo = new V2TIMUserFullInfo();
V2TIMManager.getInstance().setSelfInfo(userFullInfo, new V2TIMCallback() {
    @Override
    public void onError(int i, String s) {
        
    }

    @Override
    public void onSuccess() {
        
    }
});
```

```java
// 사용자 프로필 가져오기
List<String> userIDList = new LinkedList();
V2TIMManager.getInstance().getUsersInfo(userIDList, new V2TIMValueCallback<List<V2TIMUserFullInfo>>() {
    @Override
    public void onError(int i, String s) {
        
    }

    @Override
    public void onSuccess(List<V2TIMUserFullInfo> v2TIMUserFullInfos) {
        
    }
});
```

### 기타

#### 검색 기능

Discord는 다음과 같은 검색 기능을 제공합니다. 

Tencent Cloud IM은 다음과 같은 풍부한 검색 기능을 제공합니다.

- 메시지 검색 [searchLocalMessages](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a9364c8a0c6a0899b17c0a479b8ca848a).
- 그룹 검색 [searchGroups](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a94a72082b7e2682942f35196a7e28023).
- 그룹 구성원 검색 [searchGroupMembers](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a493fb73258019961f3ca8934ff625b0a).
- 친구 검색 [searchFriends](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3e657c9ec5d68a4c423a64d71f5f9c6e).

API 사용 방법은 [공식 문서](https://intl.cloud.tencent.com/document/product/1047/48134)를 참고하십시오.

#### 오프라인 푸시

Tencent Cloud IM의 온라인 메시지는 오프라인 사용자에게 도달할 수 없습니다. 이 문제를 해결하려면 디바이스 벤더가 제공하는 오프라인 푸시 기능을 Tencent Cloud IM에 통합해야 합니다. 자세한 내용은 [오프라인 푸시](https://intl.cloud.tencent.com/document/product/1047/39156)를 참고하십시오.

#### 민감한 문자 확인

Discord에서 정보 및 구성을 보낼 때 콘텐츠 필터링이 필요합니다. Tencent Cloud IM은 또한 사용자가 규정을 준수하여 IM을 사용할 수 있도록 이러한 체계를 제공합니다.
