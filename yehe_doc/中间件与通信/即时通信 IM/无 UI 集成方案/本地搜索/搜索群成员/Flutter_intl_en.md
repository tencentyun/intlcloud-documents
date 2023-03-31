## Overview
Only locally stored group members can be searched for, such as the list of group members or group member profiles that have been pulled.

> ? This feature is supported by the SDK for Flutter on v3.8.0 or later. It cannot be used for audio-video groups (AVChatRoom) as the group members are not stored locally.

## Searching a Local Group
Call the [`searchGroupMembers`](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/searchGroupMembers.html) API to search for a local group member.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `memberUserID`, `memberNickName`, `memberRemark`, and `memberNameCard` fields of group members.

Depending on whether `groupIDList` of [`V2TIMGroupMemberSearchParam`](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Group/V2TimGroupMemberSearchParam.html) in `searchGroupMembers` is empty (`null`/`nil`), there are two cases:
- If `groupIDList` is left empty, members in all the groups will be searched for and returned by `groupID`.
- If `groupIDList` is not left empty, members in the specified group will be searched for.

Sample code:



```dart
    // Set the search parameter
    V2TimGroupMemberSearchParam param = V2TimGroupMemberSearchParam(
        groupIDList: [],// Set the group ID list. If null is passed in, group members of all groups are searched.
        isSearchMemberNameCard: true,// Specify whether to search for a group member's name card. Default value: `true`.
        isSearchMemberRemark: true,// Specify whether to search for a group member's remarks. Default value: `true`.
        isSearchMemberNickName: true,// Specify whether to search for a group member's nickname. Default value: `true`.
        isSearchMemberUserID: true,// Specify whether to search for a group member's `userID`. Default value: `true`.
        keywordList: []);// Search for the list of keywords. Up to five keywords are supported.
    // Search for a group member
    V2TimValueCallback<V2GroupMemberInfoSearchResult> searchGroupMembersRes =
        await TencentImSDKPlugin.v2TIMManager
            .getGroupManager()
            .searchGroupMembers(param: param); // Parameter for searching for a group member
    if (searchGroupMembersRes.code == 0) {
      // Data found successfully
      searchGroupMembersRes.data?.groupMemberSearchResultItems;// Group member search result
    }
```
