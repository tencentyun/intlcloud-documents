## 기능 설명
그룹 구성원 검색은 풀링한 그룹 구성원 목록, 가져온 그룹 구성원 정보 등과 같이 로컬에 저장된 그룹 구성원만 검색할 수 있습니다.

> ? flutter sdk 3.8.0에서 지원하는 라이브 그룹(AVChatRoom)은 그룹 구성원을 로컬에 저장하지 않으며 그룹 구성원 검색 기능을 사용할 수 없습니다.

## 로컬 그룹 검색
`searchGroupMembers` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/searchGroupMembers.html)) API를 호출하여 로컬 그룹 구성원을 검색할 수 있습니다.
검색 키워드 'keywordList'를 설정하고 검색 범위, 즉 그룹 구성원의 'memberUserID', 'memberNickName', 'memberRemark', 'memberNameCard' 필드 검색 여부를 지정할 수 있습니다.

`searchGroupMembers` 입력 매개변수 `V2TIMGroupMemberSearchParam` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Group/V2TimGroupMemberSearchParam.html))의 `groupIDList`가 비어 있는지(`null`/`nil`) 여부에 따라 두 가지 경우가 있습니다.
- groupIDList가 비어 있으면 모든 그룹에서 그룹 구성원을 검색한다는 의미이며 반환된 결과는 groupID에 따라 분류됩니다.
- groupIDList 설정이 비어 있지 않으면 지정된 그룹에서 그룹 구성원을 검색한다는 의미입니다.

예시 코드는 다음과 같습니다.



```dart
    //매개변수 설정 검색
    V2TimGroupMemberSearchParam param = V2TimGroupMemberSearchParam(
        groupIDList: [],// 그룹 ID 목록 지정, null이면 모든 그룹에서 그룹 구성원 검색
        isSearchMemberNameCard: true,// 그룹 구성원 명함 검색 여부 설정, 기본값은 true
        isSearchMemberRemark: true,// 그룹 구성원의 댓글 검색 여부 설정, 기본값은 true
        isSearchMemberNickName: true,// 그룹 구성원 닉네임 검색 여부 설정, 기본값은 true
        isSearchMemberUserID: true,// 그룹 구성원의 userID를 검색할지 여부 설정, 기본값은 true
        keywordList: []);// 검색 키워드 목록, 최대 5개 지원
    //그룹 구성원 검색
    V2TimValueCallback<V2GroupMemberInfoSearchResult> searchGroupMembersRes =
        await TencentImSDKPlugin.v2TIMManager
            .getGroupManager()
            .searchGroupMembers(param: param); // 그룹 구성원에 대한 검색 매개변수
    if (searchGroupMembersRes.code == 0) {
      // 검색 성공
      searchGroupMembersRes.data?.groupMemberSearchResultItems;// 그룹 구성원 검색 결과
    }
```





