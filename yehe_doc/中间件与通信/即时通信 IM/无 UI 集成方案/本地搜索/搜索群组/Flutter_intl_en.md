## Feature Description
Only locally stored groups can be searched for, such as the list of joined groups and group profiles that have been pulled.

> ? This feature is supported by the SDK for Flutter on v3.8.0 or later.

## Searching a Local Group
Call the `searchGroups` API ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/searchGroups.html)) to search a local group.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `userID` and `groupName` fields of a group.

Sample code:



```dart
// Search for a group by the keyword
V2TimValueCallback<List<V2TimGroupInfo>> searchGroup  = await groupManager.searchGroups(searchParam: V2TimGroupSearchParam(keywordList: ['Keyword'],isSearchGroupID: true,isSearchGroupName: true));
```





