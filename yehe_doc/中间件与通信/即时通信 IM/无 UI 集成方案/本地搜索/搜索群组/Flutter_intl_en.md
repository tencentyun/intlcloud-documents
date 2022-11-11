## Feature Description
Only locally stored groups can be searched for, such as the list of joined groups and group profiles that have been pulled.

> ? This feature is supported by the SDK for Flutter on v3.8.0 or later.

## Searching a Local Group
Call the `searchGroups` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/searchGroups.html)) to search a local group.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `userID` and `groupName` fields of a group.

Sample code:



```dart
// Search for a group by the keyword
V2TimValueCallback<List<V2TimGroupInfo>> searchGroup  = await groupManager.searchGroups(searchParam: V2TimGroupSearchParam(keywordList: ['Keyword'],isSearchGroupID: true,isSearchGroupName: true));
```





