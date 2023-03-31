## Feature Description

Users can set and get their nicknames, profile photos, and statuses as well as the profile information of non-friend users. The methods are in the `TencentImSDKPlugin.v2TIMManager.getFriendshipManager()` core class.

## Relationship Chain Event Listener

Call `addFriendListener` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/addFriendListener.html)) to add a relationship chain event listener.

To stop receiving relationship chain events, call `removeFriendListener` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/removeFriendListener.html)) to remove the relationship chain event listener.

> ! You need to set the relationship chain event listener in advance to receive event notifications.

Sample code:

```javascript
// Add a relationship chain listener
const frindshipListener = {
  onBlackListAdd: (infoList) => {},
  onBlackListDeleted: (userids) => {},
  onFriendApplicationListAdded: (applicationlist) => {},
  onFriendApplicationListDeleted: (applicationlist) => {},
  onFriendApplicationListRead: () => {},
  onFriendInfoChanged: (frindInfolist) => {},
  onFriendListAdded: (frindInfolist) => {},
  onFriendListDeleted: (userd) => {},
};
friendshipManager.addFriendListener(frindshipListener);
// Remove the relationship chain listener
friendshipManager.removeFriendListener(frindshipListener);
```

## User Profile Management

### Querying and modifying your own profile

Call the `getUsersInfo` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMManager/getUsersInfo.html)) and enter a user's `UserID` for the `userIDList` parameter to query the user's profile.

Call the `setSelfInfo` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMManager/setSelfInfo.html)) to modify a user's profile.
After the profile is modified successfully, you will receive the `onSelfInfoUpdated` callback ([Details](https://comm.qq.com/im/doc/RN/en/Callback/V2TimUserFullInfo.html)).

Sample code:

```javascript
// Get a user's profile
const self = await TencentImSDKPlugin.v2TIMManager.getLoginUser();
TencentImSDKPlugin.v2TIMManager.getUsersInfo([self.data]);

// Set the user's profile
TencentImSDKPlugin.v2TIMManager.setSelfInfo({
  nickName: "",
  role: 0,
  faceUrl: "",
});
```

### Querying the user profile of a non-friend

Call the `getUsersInfo` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMManager/getUsersInfo.html)) and enter the `UserID` of a non-friend user for the `userIDList` parameter to query the profile of the non-friend user.

> ? The profile of a non-friend user cannot be modified.

### Querying and modifying a friend's profile

Call the `getFriendsInfo` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/getFriendsInfo.html)) to query the profile of the specified friend. The relationship between the user and the friend can be obtained through the `relation` field of the `V2TIMFriendInfoResult` in the callback:

| relation                                          | Relationship                    |
| ------------------------------------------------- | ------------------------------- |
| `V2TIM_FRIEND_RELATION_TYPE_NONE`                 | Not a friend                    |
| `V2TIM_FRIEND_RELATION_TYPE_BOTH_WAY`             | Two-way friend                  |
| `V2TIM_FRIEND_RELATION_TYPE_IN_MY_FRIEND_LIST`    | The user is in your contacts.   |
| `V2TIM_FRIEND_RELATION_TYPE_IN_OTHER_FRIEND_LIST` | You are in the user's contacts. |

```javascript
// Get the information of a friend
const friendsInfo = await friendshipManager.getFriendsInfo(["userID"]);
```

Call the `setFriendInfo` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/setFriendInfo.html)) to modify the information of a friend such as remarks.

```javascript
// Set the friend's information
TencentImSDKPlugin.v2TIMManager.setSelfInfo({
  nickName: "",
  role: 0,
  faceUrl: "",
});
```

## FAQs

### What should I do if the user profile obtained in the Enhanced edition is not the latest?

There are two types of user profile updates in the enhanced SDK:

- Friend's profile: When the profile of a friend is updated, the backend will send a system notification to the SDK, so the profile will be updated in real time.
- Non-friend user's profile: When the profile of a non-friend user is updated, the backend cannot send a system notification to the SDK; therefore, the profile cannot be updated in real time. To avoid sending a network request to the backend every time the user profile is obtained, the SDK adds the caching logic and allows a user to pull the profile from the backend every ten minutes.
