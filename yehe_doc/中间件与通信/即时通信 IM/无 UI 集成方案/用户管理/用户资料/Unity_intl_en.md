## Feature Description
Users can set and get their nicknames, profile photos, and statuses as well as the profile information of non-friend users.


## Relationship Chain Event Listener
Currently, relationship chain events include:

| Listener                                | Description                                       |
| --------------------------------------- | ------------------------------------------------- |
| SetOnAddFriendCallback                  | Callback for adding a friend                      |
| SetOnDeleteFriendCallback               | Callback for deleting a friend                    |
| SetUpdateFriendProfileCallback          | Callback for updating the profile of a friend     |
| SetFriendAddRequestCallback             | Callback for a friend request                     |
| SetFriendApplicationListDeletedCallback | Callback for deleting a friend request            |
| SetFriendApplicationListReadCallback    | Callback for reading a friend request             |
| SetFriendBlackListAddedCallback         | Callback for adding a friend to the blocklist     |
| SetFriendBlackListDeletedCallback       | Callback for removing a friend from the blocklist |

To stop receiving relationship chain events, call the same callback function and pass in `null` to remove the relationship chain event listener.

> ! You need to set the relationship chain event listener in advance to receive event notifications.



## User Profile Management
### Querying and modifying your own profile
Call the `ProfileGetUserProfileList` API ([Details](https://comm.qq.com/im/doc/unity/en/api/UserApi/ProfileGetUserProfileList.html)) and enter a user's `UserID` for the `friendship_getprofilelist_param_identifier_array` parameter to query the user's profile.

Call the `ProfileModifySelfUserProfile` API ([Details](https://comm.qq.com/im/doc/unity/en/api/UserApi/ProfileModifySelfUserProfile.html)) to modify a user's profile.

Sample code:


```c#
// Get a user's profile
FriendShipGetProfileListParam param = new FriendShipGetProfileListParam
{
  friendship_getprofilelist_param_identifier_array = new List<string>
  {
    "self_user_id"
  }
};
TIMResult res = TencentIMSDK.ProfileGetUserProfileList(param, (int code, string desc, List<UserProfile> profile, string user_data)=>{
 // Process the async logic
});

// Set the user's profile
UserProfileItem param = new UserProfileItem{
  user_profile_item_nick_name = "new_nick_name"
};
TIMResult res = TencentIMSDK.ProfileGetUserProfileList(param, (int code, string desc, string user_data)=>{
 // Process the async logic
});

```


### Querying the user profile of a non-friend
Call the `ProfileGetUserProfileList` API ([Details](https://comm.qq.com/im/doc/unity/en/api/UserApi/ProfileGetUserProfileList.html)) and enter the `UserID` of a non-friend user for the `friendship_getprofilelist_param_identifier_array` parameter to query the profile of the non-friend user.

> ? The profile of a non-friend user cannot be modified.

### Querying and modifying a friend's profile
Call the `FriendshipGetFriendsInfo` API ([Details](https://comm.qq.com/im/doc/unity/en/api/FriendshipApi/FriendshipGetFriendsInfo.html)) to query the profile of the specified friend. The relationship between the user and the friend can be obtained through the `friendship_friend_info_get_result_relation_type` field of the `FriendInfoGetResult` in the callback:

| relation                                                     | Relationship                    |
| ------------------------------------------------------------ | ------------------------------- |
| `TIMFriendshipRelationType.kTIMFriendshipRelationType_None`  | Not a friend                    |
| `TIMFriendshipRelationType.kTIMFriendshipRelationType_BothFriend` | Two-way friend                  |
| `TIMFriendshipRelationType.kTIMFriendshipRelationType_InMyFriendList` | The user is in your contacts.   |
| `TIMFriendshipRelationType.kTIMFriendshipRelationType_InOtherFriendList` | You are in the user's contacts. |



```c#
// Get the information of a friend
TIMResult res = TencentIMSDK.FriendshipGetFriendsInfo(friend_userids, (int code, string desc, List<FriendInfoGetResult> result, string user_data)=>{
 // Process the async logic
});
```


Call the `FriendshipModifyFriendProfile` API ([Details](https://comm.qq.com/im/doc/unity/en/api/FriendshipApi/FriendshipModifyFriendProfile.html)) to modify the information of a friend such as remarks.



```c#
// Set the friend's information
FriendshipModifyFriendProfileParam param = new FriendshipModifyFriendProfileParam
{
  friendship_modify_friend_profile_param_identifier = "friend_userid",
  friendship_modify_friend_profile_param_item = new FriendProfileItem
  {
    friend_profile_item_remark = "nickname" // Friend remarks
  }
};
TIMResult res = TencentIMSDK.FriendshipModifyFriendProfile(param, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```


## FAQs
### What should I do if the user profile obtained in the Enhanced edition is not the latest?
There are two types of user profile updates in the enhanced SDK:
 - Friend's profile: When the profile of a friend is updated, the backend will send a system notification to the SDK, so the profile will be updated in real time.
 - Non-friend user's profile: When the profile of a non-friend user is updated, the backend cannot send a system notification to the SDK; therefore, the profile cannot be updated in real time. To avoid sending a network request to the backend every time the user profile is obtained, the SDK adds the caching logic and allows a user to pull the profile from the backend every ten minutes.
