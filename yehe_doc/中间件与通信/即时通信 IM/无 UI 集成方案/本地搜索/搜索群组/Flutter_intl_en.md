## Overview
Only locally stored groups can be searched for, such as the list of joined groups and group profiles that have been pulled.

> ? This feature is supported by the SDK for Flutter v3.8.0 or later.

## Searching a Local Group
Call the `searchGroups` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/searchGroups.html)) to search a local group.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `userID` and `groupName` fields of a group.

Sample code:



```dart
// Search for a group by the keyword
    // Settings for group profile search
    V2TimGroupSearchParam param = V2TimGroupSearchParam(
        isSearchGroupID: true, // Whether to search by group ID. The default value is `true`.
        isSearchGroupName: true, // Whether to search by group name. The default value is `true`.
        keywordList: []); // Search keyword list. Up to five keywords are supported.
    // Search a group profile
    V2TimValueCallback<List<V2TimGroupInfo>> searchGroupsRes =
        await TencentImSDKPlugin.v2TIMManager
            .getGroupManager()
            .searchGroups(searchParam: param);// Settings for group profile search
    if (searchGroupsRes.code == 0) {
      // Data found successfully
      searchGroupsRes.data?.forEach((element) {
        element.customInfo; // Custom group field
        element.faceUrl; // Group's profile photo URL
        element.groupAddOpt; // Group adding options
        element.groupID; // Group ID
        element.groupName; // Group name
        element.groupType; // Group type
        element.introduction; // Group introduction
        element.isAllMuted; // Whether to mute all group members
        element.isSupportTopic; // Whether the group supports topics
        element.joinTime; // Time when the current user joins the group
        element.lastInfoTime; // Time when the group profile is modified last time
        element.lastMessageTime; // Time when the last message is sent in the group
        element.memberCount; // Number of group members
        element.notification; // Group notice
        element.onlineCount; // Number of online members in the group
        element.owner; // Group owner
        element.recvOpt; // Current user's message receiving option in the group
        element.role; // Current user's role in the group
      });
    }
```
