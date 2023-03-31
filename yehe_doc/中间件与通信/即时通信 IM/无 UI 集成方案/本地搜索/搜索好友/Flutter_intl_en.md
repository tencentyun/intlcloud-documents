## Overview
Only locally stored users can be searched for, such as contacts or user profiles that have been pulled.

>?This feature is supported by the SDK for Flutter v3.8.0 or later.

## Searching for the Local User Profile
Call the `searchFriends` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/searchFriends.html)) to search for the local user profile.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `userID`, `nickName`, and `remark` fields of a user.

Sample code:



```dart
// Search for a friend by keyword
    // Search criteria
    V2TimFriendSearchParam searchParam = V2TimFriendSearchParam(
      isSearchNickName: true, // Whether to search by nickname
      isSearchRemark: true, // Whether to search by remarks
      isSearchUserID: true, // Whether to search by user ID
      keywordList: [], // Search keyword list. Up to five keywords are supported.
    );
    V2TimValueCallback<List<V2TimFriendInfoResult>> searchFriendsRes =
        await TencentImSDKPlugin.v2TIMManager
            .getFriendshipManager()
            .searchFriends(searchParam: searchParam); // Search criteria
    if (searchFriendsRes.code == 0) {
      // Queried successfully
      searchFriendsRes.data?.forEach((element) {
        element.relation; // Friend type: `0` (Not a friend), `1` (The user is in your contacts.), `2` (You are in the user's contacts), `3` (Two-way friend)
        element.resultCode; // Error code (query result)
        element.resultInfo; // Description (query result)
        // friendInfo: user profile of a friend. If you are not a friend, only the userID field has a value, and other fields are empty.
        element.friendInfo
            ?.friendCustomInfo; // Custom friend field. You need to first configure a custom friend field in the console (**Feature Configuration** > **Custom Friend Field**) and then call this API to specify the field.
        element.friendInfo?.friendGroups; // Lists to which a friend belongs
        element.friendInfo?.friendRemark; // Friend remarks
        element.friendInfo?.userID; // User ID
        element.friendInfo?.userProfile
            ?.allowType; // Friend adding mode: `0` (Accept all friend requests), `1` (Reject all friend requests), `2` (Require approval for friend requests)
        element.friendInfo?.userProfile?.birthday; // User's birthday
        element.friendInfo?.userProfile?.customInfo; // User's custom status
        element.friendInfo?.userProfile?.faceUrl; // User's profile photo URL
        element.friendInfo?.userProfile?.gender; // User's gender: `1` (male), `2` (female)
        element.friendInfo?.userProfile?.level; // User level
        element.friendInfo?.userProfile?.nickName; // User nickname
        element.friendInfo?.userProfile?.role; // User role
        element.friendInfo?.userProfile?.selfSignature; // User signature
        element.friendInfo?.userProfile?.userID; // User ID
      });
    }
```
