## 기능 설명
그룹 구성원 관리에는 구성원 목록 가져오기, 그룹 구성원 음소거, 그룹 구성원 제거, 권한 부여 및 그룹 소유권 이전이 포함되며 `TencentImSDKPlugin.v2TIMManager.getGroupManager()` 코어 클래스의 메소드를 통해 구현할 수 있습니다.

[](id:getGroupMemberList)

## 그룹 구성원 목록 가져오기

지정된 그룹의 구성원 목록을 가져오려면 `getGroupMemberList`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupMemberList.html))를 호출하십시오. 이 목록에는 사용자 ID(`userID`), 그룹 이름 카드(`nameCard`), 프로필 사진(`faceUrl`), 닉네임(`nickName`), 그룹 가입 시간(`joinTime`)과 같은 각 구성원의 프로필 정보가 포함됩니다.

그룹에 많은 구성원(예: 5000+)이 있는 경우 그룹 구성원 목록을 가져오기 위한 API의 필터(`filter`) 및 페이징 풀링(`nextSeq`) 고급 기능을 사용할 수 있습니다.

### 필터(filter)
`getGroupMemberList` API([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupMemberList.html))를 호출할 때 `filter`를 지정하여 지정된 역할의 정보 목록을 풀링할 수 있습니다.

| 필터                                                     | 유형                   |
| ---------------------------------------------------------- | -------------------------- |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ALL    | 모든 그룹 구성원의 정보 목록 풀링   |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_OWNER  | 그룹 소유자의 정보 목록 풀링       |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN  | 그룹 관리자의 정보 목록 풀링   |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_COMMON | 일반 그룹 구성원의 정보 목록 풀링 |

예시 코드는 다음과 같습니다.



```java
// 그룹 소유자의 프로필만 가져오도록 지정하려면 filter 매개변수 사용
groupManager.getGroupMemberList(count: 10,filter: GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN,nextSeq: '0',offset: 0,groupID: "",);
```


### 페이징 풀링(nextSeq)
대부분의 경우 사용자 UI에는 모든 그룹 구성원의 정보가 아닌 그룹 구성원 목록의 첫 번째 페이지만 표시되어야 합니다. 더 많은 그룹 구성원은 사용자가 ‘다음 페이지’를 클릭하거나 목록 페이지를 새로고침할 때만 풀링하면 됩니다. 이 경우 페이징 풀링을 사용할 수 있습니다.

페이징 풀링 방법:
1. 처음으로 `getGroupMemberList`를 호출할 때 `nextSeq`를 0으로 설정합니다(처음부터 그룹 구성원 목록 풀링을 나타냄). 한 번에 최대 50개의 그룹 구성원 객체를 풀링할 수 있습니다.
2. 그룹 구성원 목록이 처음으로 성공적으로 풀링되면 `getGroupMemberList`의 `V2TIMGroupMemberInfoResult` 콜백에 `nextSeq`(다음 풀링에 대한 필드)가 포함됩니다.
   * `nextSeq`가 0이면 모든 그룹 구성원이 풀링된 것입니다.
   * `nextSeq`가 0보다 크면 풀링할 수 있는 그룹 구성원이 더 많습니다. 이는 구성원 목록의 ‘다음 페이지’가 즉시 풀링된다는 것을 의미하지 않습니다. 일반적인 통신 소프트웨어에서 페이징 풀링은 종종 스와이프 작업에 의해 트리거됩니다.
3. 사용자가 그룹 구성원 목록을 계속 가져올 때 풀링할 수 있는 구성원이 더 있으면 계속해서 `getGroupMemberList` API를 호출하고 다음 풀링을 위해 `nextSeq` 매개변수(값은 마지막 풀링에서 반환된 `V2TIMGroupMemberInfoResult` 객체에서 가져옴)를 전달할 수 있습니다.
4. `nextSeq`가 0이 될 때까지 [3단계]를 반복합니다.

예시 코드는 다음과 같습니다.



```java
// filter 매개변수를 통해 그룹 소유자의 프로필을 풀링하도록 지정
groupManager.getGroupMemberList(count: 10,filter: GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN,nextSeq: '0',offset: 0,groupID: "",);
```


[](id:mute)
## 음소거

### 지정된 그룹 구성원 음소거
그룹 소유자 또는 관리자는 `muteGroupMember`([세부 정보](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/muteGroupMember.html))를 호출하여 지정된 그룹 구성원을 음소거하고 음소거 기간을 초 단위로 설정할 수 있습니다. 음소거 정보는 그룹 구성원의 `muteUtil` 속성에 저장됩니다.

그룹 구성원이 음소거된 후 모든 그룹 구성원(음소거된 구성원 포함)은 `onMemberInfoChanged` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnMemberInfoChangedCallback.html)) 콜백을 수신합니다.

### 전체 그룹 음소거
그룹 소유자 또는 관리자는 `setGroupInfo` API([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html))를 호출하여 `allMuted` 특성을 `true`로 설정하여 전체 그룹을 음소거할 수도 있습니다. 전체 그룹은 무제한으로 음소거할 수 있으며 그룹 프로필의 `setAllMuted(false)`를 통해 음소거 해제해야 합니다.

> ? 모든 그룹 구성원을 음소거하면 `onGroupInfoChanged` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnGroupInfoChangedCallback.html)) 콜백이 트리거됩니다. 이 기능은 기본적으로 비활성화되어 있으며 콘솔에서 활성화할 수 있습니다.
>  방법: IM 콘솔의 [그룹 구성](https://console.cloud.tencent.com/im/qun-setting) 모듈로 이동하여 그룹 시스템 알림 구성을 선택하고 작업 열에서 **편집**을 클릭하고 ‘모든 음소거 변경 사항 알림’을 수정합니다.

예시 코드는 다음과 같습니다.
```dart
// 10분 동안 그룹 구성원 userB 음소거
groupManager.muteGroupMember(groupID: '',userID: 'userB',seconds: 10);

// 모든 구성원 음소거
groupManager.setGroupInfo(info: V2TimGroupInfo(isAllMuted: true,groupID: '',groupType: 'Public'));

TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onMemberInfoChanged: (groupID, v2TIMGroupMemberChangeInfoList) {
    //그룹 구성원 정보 변경
  },
  onGroupInfoChanged: (groupID,info){
    // 그룹 프로필 수정
  }
  ));
```

>? 그룹 소유자만 관리자를 음소거할 수 있습니다.



[](id:kickGroupMember)
## 그룹 구성원 제거
그룹 소유자 또는 관리자는 그룹에서 지정된 일반 그룹 구성원을 제거하기 위해 `kickGroupMember` API([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/kickGroupMember.html))를 호출할 수 있습니다.

일반 그룹 구성원이 제거된 후 모든 구성원(제거된 구성원 포함)은 `onMemberKicked` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnMemberKickedCallback.html)) 콜백을 받습니다.

라이브 방송 그룹(AVChatRoom)은 자유롭게 가입할 수 있으므로 라이브 방송 그룹(AVChatRoom)에서 그룹 구성원을 제거하는 API는 없습니다. `muteGroupMember` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/muteGroupMember.html)를 사용하여 지정된 구성원을 음소거하여 유사한 제어를 구현할 수 있습니다. 자세한 지침은 [음소거](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/muteGroupMember.html)를 참고하십시오.

> ? 그룹 소유자만 관리자를 그룹에서 제거할 수 있습니다.

예시 코드는 다음과 같습니다.



```dart
groupManager.kickGroupMember(groupID: '',memberList: []);
```


## 관리자 설정
그룹 소유자는 `setGroupMemberRole` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/setGroupMemberRole.html))를 호출하여 공용 그룹(Public) 또는 회의 그룹(Meeting)의 그룹 구성원을 관리자로 설정할 수 있습니다.

관리자로 설정된 일반 구성원은 다음 작업을 수행할 수 있는 관리자 권한을 가집니다.
* 기본 그룹 프로필 수정
* 그룹에서 일반 구성원 제거
* 일반 구성원 음소거(지정된 시간 동안 구성원이 발언하지 못하도록 차단)
* 그룹 가입 요청 승인

자세한 내용은 [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529)을 참고하십시오.

일반 구성원이 관리자로 설정되면 모든 구성원(일반 구성원 포함)이 `onGrantAdministrator` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnGrantAdministratorCallback.html)) 콜백을 받게 됩니다.

일반 구성원이 관리자로 설정 해제되면 모든 구성원(일반 구성원 포함)이 `onRevokeAdministrator` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRevokeAdministratorCallback.html)) 콜백을 받게 됩니다.

예시 코드는 다음과 같습니다.


```dart
groupManager.setGroupMemberRole(groupID: '',userID: '',role: GroupMemberRoleTypeEnum.V2TIM_GROUP_MEMBER_ROLE_ADMIN);

// 역할 변경 수신
TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onMemberInfoChanged: (groupID, v2TIMGroupMemberChangeInfoList) {

  },
  onGroupInfoChanged: (groupID,info){

  },
  onGrantAdministrator: (String groupID, V2TimGroupMemberInfo info, List<V2TimGroupMemberInfo> infolist){},
  onRevokeAdministrator: (String groupID, V2TimGroupMemberInfo info, List<V2TimGroupMemberInfo> infolist){},
  ));
```


[](id:transfer)

## 그룹 소유권 이전
그룹 소유자는 [transferGroupOwner](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/transferGroupOwner.html)를 호출하여 그룹 소유권을 다른 그룹 구성원에게 이전할 수 있습니다.

그룹 소유권이 이전된 후 모든 그룹 구성원은 [onGroupInfoChanged](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnGroupInfoChangedCallback.html) 콜백을 수신합니다. 여기서 `V2TIMGroupChangeInfo`의 type은 `V2TIMGroupChangeInfo.V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER`이며, value는 새 그룹 소유자의 UserID입니다.

예시 코드는 다음과 같습니다.



```dart
groupManager.transferGroupOwner(groupID: "", userID: "userID");
```


## 온라인 그룹 구성원 수 가져오기
`getGroupOnlineMemberCount` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupOnlineMemberCount.html))를 호출하여 온라인 그룹 구성원 수를 가져옵니다.

> ?
> 1. 현재는 라이브 방송 그룹(AVChatRoom)의 온라인 구성원 수만 가져올 수 있습니다.
> 2. 이 API는 SDK에서 60초마다 한 번씩 호출할 수 있습니다.

예시 코드는 다음과 같습니다.


```dart
groupManager.getGroupOnlineMemberCount(groupID: '');
```

