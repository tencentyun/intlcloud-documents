## Overview
The Chat SDK supports friend management, and users can add and delete friends and set to send messages only to friends.

### Getting the contacts
The Chat SDK supports the logic for the friend relationship chain. You can call the `FriendshipGetFriendProfileList` API ([details](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipGetFriendProfileList.html)) to get contacts.

Sample code:


```c#
// Obtain the contacts
TIMResult res = TencentIMSDK.FriendshipGetFriendProfileList((int code, string desc, List<FriendProfile> profile_list, string user_data)=>{
 // Process the async logic
});
```



### Adding friends
Call the `FriendshipAddFriend` API ([details](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipAddFriend.html)) to add a friend.

Sample code:


```c#
// Add a two-way friend
FriendshipAddFriendParam param = new FriendshipAddFriendParam
{
  friendship_add_friend_param_identifier = "friend_userid",
  friendship_add_friend_param_friend_type = TIMFriendType.FriendTypeBoth,
  friendship_add_friend_param_remark = "nickname",
  friendship_add_friend_param_add_wording = "greeting"
};
TIMResult res = TencentIMSDK.FriendshipAddFriend(param, (int code, string desc, FriendResult result, string user_data)=>{
 // Process the async logic
});
```


The process has the following variations depending on whether friend request approval is required.

#### Friend request approval is not required
1. Users A and B call `SetOnAddFriendCallback` to set the relationship chain listener.
2. User B specifies that friend request approval is not required (`kTIMProfileAddPermission_AllowAny`) through the `user_profile_item_add_permission` field ([details](https://comm.qq.com/im/doc/unity/zh/api/UserApi/ProfileModifySelfUserProfile.html)) in the `ProfileModifySelfUserProfile` function.
3. User A can add user B as a friend successfully by calling `FriendshipAddFriend`, after which the `friendship_add_friend_param_friend_type` of the `FriendshipAddFriendParam` request parameter can be set to either value as needed:
   * If it is set to `TIMFriendType.FriendTypeBoth` (two-way friend), both users A and B will receive the `OnAddFriendCallback` callback ([details](https://comm.qq.com/im/doc/unity/zh/callback/OnAddFriendCallback.html)).
   * If it is set to `TIMFriendType.FriendTypeSignle` (one-way friend), only user A will receive the `OnAddFriendCallback` callback.


#### Friend request approval is required
1. Users A and B call `SetOnAddFriendCallback` to set the relationship chain listener.
2. User B specifies that friend request approval is required (`kTIMProfileAddPermission_NeedConfirm`) through the `user_profile_item_add_permission` field in the `ProfileModifySelfUserProfile` function.
3. User A calls `FriendshipAddFriend` to request to add user B as a friend. The `code` parameter in the callback for successful API call returns `30539`, indicating that the request needs to be approved by user B.
4. User B will receive the `SetFriendAddRequestCallback` callback and can accept or reject the request.
    - User B calls `FriendshipHandleFriendAddRequest` API ([details](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipHandleFriendAddRequest.html)) to accept the friend request. If the type is `TIMFriendResponseAction.ResponseActionAgree` (one-way friend):
      - User A will receive the `OnAddFriendCallback` callback, indicating that the one-way friend was added successfully.
      - User B will receive the `FriendApplicationListDeletedCallback` callback ([details](https://comm.qq.com/im/doc/unity/zh/callback/FriendApplicationListDeletedCallback.html)). At this point, user B has become a friend of user A, but not vice versa.
    - User B calls `FriendshipHandleFriendAddRequest` to accept the friend request. If the type is `TIMFriendResponseAction.ResponseActionAgreeAndAdd` (two-way friend), both users A and B will receive the `OnAddFriendCallback` callback, indicating that they added each other as a friend successfully.
    - User B calls `FriendshipHandleFriendAddRequest` and passes in the `TIMFriendResponseAction` parameter to reject the friend request, and both users will receive the `FriendApplicationListDeletedCallback` callback.


### Deleting friends
Call the `FriendshipDeleteFriend` API ([details](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipDeleteFriend.html)) to delete a friend.

Sample code:


```c#
// Two-way deletion
FriendshipDeleteFriendParam param = new FriendshipDeleteFriendParam
{
  friendship_delete_friend_param_friend_type = TIMFriendType.FriendTypeBoth,
  friendship_delete_friend_param_identifier_array = new List<string>
  {
    "user_id"
  }
};
TIMResult res = TencentIMSDK.FriendshipDeleteFriend(param, (int code, string desc, FriendResult result, string user_data)=>{
 // Process the async logic
});
```



### Checking friend relationships
Call the `FriendshipCheckFriendType` API ([details](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipCheckFriendType.html)) to check the friend relationship.

Sample code:


```c#
// Check whether the friend relationship is one-way or two-way
FriendshipCheckFriendTypeParam param = new FriendshipCheckFriendTypeParam
{
  friendship_check_friendtype_param_check_type = TIMFriendType.FriendTypeBoth,
  friendship_check_friendtype_param_identifier_array = new List<string>{
    "user_id"
  }
};
TIMResult res = TencentIMSDK.FriendshipCheckFriendType(param, (int code, string desc, List<FriendshipCheckFriendTypeResult> result_list, string user_data)=>{
 // Process the async logic
});
```


### Setting to send messages to friends only
By default, Chat SDK does not check the relationship when sending one-to-one messages. This default setting is generally applied in customer service scenarios, where having to friend a customer service agent before chatting is inefficient.
If you want to implement the interaction mode of “friending before chatting” as in WeChat and QQ, go to [Chat console](https://console.cloud.tencent.com/im) -> **Feature Configuration** -> **Login and Message** -> **Relationship Check** and enable "Check Relationship for One-to-One Messages". With this feature enabled, users can only send messages to friends, and will receive the 20009 error code from SDK when sending a message to a non-friend user.
