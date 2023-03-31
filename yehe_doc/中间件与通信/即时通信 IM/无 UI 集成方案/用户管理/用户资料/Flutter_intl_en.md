## Overview
Users can set and get their nicknames, profile photos, and statuses as well as the profile information of non-friend users. The methods are in the `TencentImSDKPlugin.v2TIMManager.getFriendshipManager()` core class.


## Relationship Chain Event Listener
Call the `addFriendListener` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/addFriendListener.html)) to add a relationship chain event listener.

To stop receiving relationship chain events, call the `removeFriendListener` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/removeFriendListener.html)) to remove the relationship chain event listener.

> ! You need to set the relationship chain event listener in advance to receive event notifications.

Sample code:


```dart
    // Set the relationship chain listener
    V2TimFriendshipListener listener = V2TimFriendshipListener(
      onBlackListAdd: (List<V2TimFriendInfo> infoList) async {
        // Callback for adding a user to the blocklist
        // infoList: List of information of the user added
      },
      onBlackListDeleted: (List<String> userList) async {
        // Callback for removing users from the blocklist
        // userList: List of IDs of the users deleted
      },
      onFriendApplicationListAdded:
          (List<V2TimFriendApplication> applicationList) async {
        // Callback for the increase of friend requests
        // applicationList: List of the information of new friend requests
      },
      onFriendApplicationListDeleted: (List<String> userIDList) async {
        // Callback for the decrease of friend requests
        // userIDList: List of user IDs corresponding to the friend requests decreased
      },
      onFriendApplicationListRead: () async {
        // Callback for read friend request
      },
      onFriendInfoChanged: (List<V2TimFriendInfo> infoList) async {
        // Callback for friend information changes
        // infoList: list of friends whose information changes
      },
      onFriendListAdded: (List<V2TimFriendInfo> users) async {
        // Callback for the increase of users in the friend list
        // users: list of users added
      },
      onFriendListDeleted: (List<String> userList) async {
        // Callback for the decrease of users in the friend list
        // userList: list of users deleted
      },
    );
    TencentImSDKPlugin.v2TIMManager
        .getFriendshipManager()
        .addFriendListener(listener: listener); // Add a relationship chain listener
// Remove the relationship chain listener
 friendshipManager.removeFriendListener(listener: frindshipListener);
```



## User Profile Management
### Querying and modifying your own profile
Call the `getUsersInfo` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getUsersInfo.html)) with the `userIDList` parameter set to a user's `UserID` to query the user's profile.

Call the `setSelfInfo` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/setSelfInfo.html)) to modify a user's profile.
After the profile is modified successfully, you will receive the `onSelfInfoUpdated` callback ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/V2TimUserFullInfoCallback.html)).

Sample code:


```dart
// Obtain a user's personal profile
V2TimValueCallback<String> self = await TencentImSDKPlugin.v2TIMManager.getLoginUser();
TencentImSDKPlugin.v2TIMManager.getUsersInfo(userIDList: [self.data]);

// Set the user's profile
 TencentImSDKPlugin.v2TIMManager.setSelfInfo(userFullInfo: V2TimUserFullInfo(nickName: "",role: 0,faceUrl: ""));

```


### Querying the user profile of a non-friend user
Call the `getUsersInfo` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getUsersInfo.html)) with the `userIDList` parameter set to a non-friend user's `UserID` to query the non-friend user's profile.

> ? The profile of a non-friend user cannot be modified.

### Querying and modifying a friend's profile
Call the `getFriendsInfo` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/getFriendsInfo.html)) to query the profile of the specified friend. The relationship between the user and the friend can be obtained through the `relation` field of the `V2TIMFriendInfoResult` in the callback:

| relation                                          | Relationship                    |
| ------------------------------------------------- | ------------------------------- |
| `V2TIM_FRIEND_RELATION_TYPE_NONE`                 | Not a friend                    |
| `V2TIM_FRIEND_RELATION_TYPE_BOTH_WAY`             | Two-way friend                  |
| `V2TIM_FRIEND_RELATION_TYPE_IN_MY_FRIEND_LIST`    | The user is in your contacts.   |
| `V2TIM_FRIEND_RELATION_TYPE_IN_OTHER_FRIEND_LIST` | You are in the user's contacts. |



```dart
// Get friend information
V2TimValueCallback<List<V2TimFriendInfoResult>> friendsInfo = await friendshipManager.getFriendsInfo(userIDList: []);
```


Call the `setFriendInfo` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/setFriendInfo.html)) to modify the information of a friend such as remarks.



```dart
// Set friend information
TencentImSDKPlugin.v2TIMManager.setSelfInfo(userFullInfo: V2TimUserFullInfo(nickName: "",role: 0,faceUrl: ""));
```


## FAQs
### Why can't the SDK enhanced edition get the latest user profiles?
There are two types of user profile updates in the enhanced SDK:
 - Friend's profile: when the profile of a friend is updated, the backend will send a system notification to the SDK, so the friend's profile will be updated in real time.
 - Stranger's profile: when the profile of a stranger is updated, the backend will not send any system notification because the stranger is not a friend of yours, so the stranger's profile will not be updated in real time. To avoid sending a network request to the backend every time the user profile is obtained, the SDK adds a caching logic, setting a 10-minute interval between pulls of the same user's profile from the backend.
