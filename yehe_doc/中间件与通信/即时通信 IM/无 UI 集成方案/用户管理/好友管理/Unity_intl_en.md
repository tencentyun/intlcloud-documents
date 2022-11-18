## Feature Description
The IM SDK supports friend management, and users can add and delete friends and set to send messages only to friends.

### Getting contacts
The IM SDK supports the logic for the friend relationship chain. You can call the `FriendshipGetFriendProfileList` API ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipGetFriendProfileList_com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_FriendProfile___)) to get contacts.

Sample code:


```c#
// Get contacts
TIMResult res = TencentIMSDK.FriendshipGetFriendProfileList((int code, string desc, List<FriendProfile> profile_list, string user_data)=>{
 // Process the async logic
});
```



### Adding a friend
Call the `FriendshipAddFriend` API ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipAddFriend_com_tencent_imsdk_unity_types_FriendshipAddFriendParam_com_tencent_imsdk_unity_callback_ValueCallback_com_tencent_imsdk_unity_types_FriendResult__)) to add a friend.

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


The process has the following variations depending on whether friend verification is required.

#### Option 1. Friend request approval is not required
1. Users A and B call `SetOnAddFriendCallback` to set the relationship chain listener.

2. User B specifies that friend request approval is not required (`kTIMProfileAddPermission_AllowAny`) through the `user_profile_item_add_permission` field ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.types.UserProfileItem.html#com_tencent_imsdk_unity_types_UserProfileItem_user_profile_item_add_permission)) in the `ProfileModifySelfUserProfile` function.

3. User A can add user B as a friend successfully by calling `FriendshipAddFriend`, after which the `friendship_add_friend_param_friend_type` of the `FriendshipAddFriendParam` request parameter can be set to either value as needed:
   * If it is set to `TIMFriendType.FriendTypeBoth` (two-way friend), both users A and B will receive the `OnAddFriendCallback` callback ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_SetOnAddFriendCallback_com_tencent_imsdk_unity_callback_OnAddFriendCallback_com_tencent_imsdk_unity_callback_OnAddFriendStringCallback_)).
   * If it is set to `TIMFriendType.FriendTypeSignle` (one-way friend), only user A will receive the `OnAddFriendCallback` callback.


#### Option 2. Friend request approval is required
1. Users A and B call `SetOnAddFriendCallback` to set the relationship chain listener.

2. User B specifies that friend request approval is required (`kTIMProfileAddPermission_NeedConfirm`) through the `user_profile_item_add_permission` field in the `ProfileModifySelfUserProfile` function.

3. User A calls `FriendshipAddFriend` to request to add user B as a friend. The `code` parameter in the callback for successful API call returns `30539`, indicating that the request needs to be approved by user B.

4. User B will receive the `SetFriendAddRequestCallback` callback and can accept or reject the request.
    - User B calls `FriendshipHandleFriendAddRequest` ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipHandleFriendAddRequest_com_tencent_imsdk_unity_types_FriendRespone_com_tencent_imsdk_unity_callback_ValueCallback_com_tencent_imsdk_unity_types_FriendResult__)) to accept the friend request. If the type is `TIMFriendResponseAction.ResponseActionAgree` (one-way friend):
      - User A will receive the `OnAddFriendCallback` callback, indicating that the one-way friend was added successfully.
      - User B will receive the `FriendApplicationListDeletedCallback` callback ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_SetFriendApplicationListDeletedCallback_com_tencent_imsdk_unity_callback_FriendApplicationListDeletedCallback_com_tencent_imsdk_unity_callback_FriendApplicationListDeletedStringCallback_)). At this point, user B has become a friend of user A, but not vice versa.
    - User B calls `FriendshipHandleFriendAddRequest` to accept the friend request. If the type is `TIMFriendResponseAction.ResponseActionAgreeAndAdd` (two-way friend), both users A and B will receive the `OnAddFriendCallback` callback, indicating that they added each other as a friend successfully.
    - User B calls `FriendshipHandleFriendAddRequest` and passes in the `TIMFriendResponseAction` parameter to reject the friend request, and both users will receive the `FriendApplicationListDeletedCallback` callback.


### Deleting a friend
Call the `FriendshipDeleteFriend` API ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipDeleteFriend_com_tencent_imsdk_unity_types_FriendshipDeleteFriendParam_com_tencent_imsdk_unity_callback_ValueCallback_com_tencent_imsdk_unity_types_FriendResult__)) to delete a friend.

Sample code:


```c#
// Delete a two-way friend
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



### Checking the friend relationship
Call the `FriendshipCheckFriendType` API ([Details](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipCheckFriendType_com_tencent_imsdk_unity_types_FriendshipCheckFriendTypeParam_com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_FriendshipCheckFriendTypeResult___)) to check the friend relationship.

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
By default, IM SDK does not check the relationship when sending one-to-one messages. This default setting is generally applied in customer service scenarios, where having to friend a customer service agent before chatting is inefficient.
To implement "adding a friend before sending a message" like WeChat or QQ, you can log in to the [IM console](https://console.cloud.tencent.com/im), select **Feature Configuration** > **Login and Message** > **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. After it is enabled, a user can send messages only to friends. If the user sends a message to a non-friend user, the SDK will report error code 20009.



