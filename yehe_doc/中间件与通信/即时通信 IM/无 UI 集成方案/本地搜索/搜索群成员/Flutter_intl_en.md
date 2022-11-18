## Feature Description
Only locally stored group members can be searched for, such as the list of group members or group member profiles that have been pulled.

> ? This feature is supported by the SDK for Flutter on v3.8.0 or later. It cannot be used for audio-video groups (AVChatRoom) as the group members are not stored locally.

## Searching a Local Group
Call the `searchGroupMembers` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/searchGroupMembers.html)) to search for a local group member.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `memberUserID`, `memberNickName`, `memberRemark`, and `memberNameCard` fields of a group member.

Depending on whether `groupIDList` of the `V2TIMGroupMemberSearchParam` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupMemberSearchParam.html)) in `searchGroupMembers` is empty (`null`/`nil`), there are two cases:
- If `groupIDList` is left empty, members in all the groups will be searched for and returned by `groupID`.
- If `groupIDList` is not left empty, members in the specified group will be searched for.

Sample code:



```dart
// Search for group members by the keyword and group ID
V2TimValueCallback<V2GroupMemberInfoSearchResult> searchGroupMem = await groupManager.searchGroupMembers(param: V2TimGroupMemberSearchParam(groupIDList: ['The group ID can be specified'],keywordList: ['Keyword'],isSearchMemberNameCard: true,isSearchMemberNickName: true,isSearchMemberRemark: true,isSearchMemberUserID: true,));
```



