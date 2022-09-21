## Feature Description
Only locally stored users can be searched for, such as contacts or user profiles that have been pulled.

> This feature is supported by the SDK for Flutter on v3.8.0 or later.

## Searching for the Local User Profile
Call the `searchFriends` API ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMFriendshipManager/searchFriends.html)) to search for the local user profile.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `userID`, `nickName`, and `remark` fields of a user.

Sample code:



```dart
// Search for a friend by keyword
V2TimValueCallback<List<V2TimFriendInfoResult>> serchFriend= await friendshipManager.searchFriends(searchParam: V2TimFriendSearchParam(isSearchNickName: true,isSearchRemark: true,isSearchUserID: true,keywordList: ['Keyword']));
```

