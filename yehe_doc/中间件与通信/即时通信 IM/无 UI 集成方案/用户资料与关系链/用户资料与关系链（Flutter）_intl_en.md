## User Profile Management
### Querying and modifying your own profile
Use [getUsersInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/getUsersInfo.html) to **query your own profile**, where `userIDList` indicates your own UserID.
Use [setSelfInfo](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html) to **modify your own profile**. You will receive the [onSelfInfoUpdated](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Listener/V2TimSDKListener.html#onselfinfoupdated) callback after your profile is modified successfully.

### Querying the user profile of a non-friend
Use [getUsersInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/getUsersInfo.html) to query the user profile of a non-friend, where `userIDList` indicates the UserID of the user to query.

### Querying and modifying a friend's profile
Use [getFriendsInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendsInfo.html) to **query the profile of a specified friend**. Use the `relation` field in `V2TIMFriendInfoResult` to obtain your relationship from the callback information:
- `FriendTypeWeb.V2TIM_FRIEND_RELATION_TYPE_NONE`: the user is not a friend.
- `FriendTypeWeb.V2TIM_FRIEND_RELATION_TYPE_BOTH_WAY`: the user is a two-way friend.
- `FriendTypeWeb.V2TIM_FRIEND_RELATION_TYPE_IN_MY_FRIEND_LIST`: the user is in your friend list.
- `FriendTypeWeb.V2TIM_FRIEND_RELATION_TYPE_IN_OTHER_FRIEND_LIST`: you are in your friend's friend list.

Use [setFriendInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendInfo.html) to **modify the information of a specified friend**, such as friend remarks.

## Blocking Messages from a Specified User
- **Blocking a user*
To block messages from a specified user, call the [addToBlackList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addToBlackList.html) API to add the user to the blocklist and block the user.
By default, the blocked user is unaware of the "blocked" status. An error code indicating blocking will not be returned after the user sends a message. If you want blocked users to receive the blocked message in this situation, see [How do I enable error messages when blocked users try to send a message](#msgSendTips).

- **Removing a user from the blocklist**
Call [deleteFromBlackList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFromBlackList.html) to remove a user from your blocklist and receive the user's messages again.

- **Obtaining the blocklist**
Call [getBlackList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getBlackList.html) to view and manage the blocklist.

## Friend Management
### Determining whether a friend request is required
By default, the IM SDK does not check the relationship between two parties when sending one-to-one chat messages. This default setting is generally applied in customer service scenarios, where having to friend a customer service agent before chatting is inefficient.
If you want to demand users to be friends before they can chat, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. With this feature enabled, users can send messages to friends only, and will receive the 20009 error code from the SDK when sending a message to a non-friend user.
![](https://qcloudimg.tencent-cloud.cn/raw/be6046b44a6f6bd3b47be3ba1b0de55d.png)

### Friend list management

The IM SDK supports relationship chain logic. You can call [getFriendList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendList.html) to obtain the friend list, call [deleteFromFriendList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFromFriendList.html) to delete a friend from the friend list, or call [addFriend](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriend.html) to add a friend.

The process has the following variations depending on whether friend verification is required.

#### Friend request approval is not required
1. User A and user B call [setFriendListener](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/method_channel_im_flutter/MethodChannelIm/setFriendListener.html) to set a relationship chain listener.
2. User B calls [setSelfInfo](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html): sets `userFullInfo` to `V2TimUserFullInfo.fromJson({...})`, and sets [allowType](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_user_full_info/V2TimUserFullInfo/allowType.html) in `V2TimUserFullInfo` to `AllowType.V2TIM_FRIEND_ALLOW_ANY`.
3. User A becomes user B's friend simply by calling [addFriend](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriend.html) to send a friend request. If the `addType` in the request parameter is set to `FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH` (that is, setting as a two-way friend), both users A and B receive the [onFriendListAdded](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendListAdded.html) callback.
	If `addType` is set to `FriendTypeEnum.V2TIM_FRIEND_TYPE_SINGLE` (that is, setting as a one-way friend), only user A receives the [onFriendListAdded](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendListAdded.html) callback.

#### Friend request approval is required
1. User A and user B call [setFriendListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendListener.html) to set a relationship chain listener.
2. User B calls [setSelfInfo](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html): sets `userFullInfo` to `V2TimUserFullInfo.fromJson({...})`, and sets [allowType](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_user_full_info/V2TimUserFullInfo/allowType.html) in `V2TimUserFullInfo` to `AllowType.V2TIM_FRIEND_NEED_CONFIRM`.
3. User A calls [addFriend](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriend.html) to send a friend request to user B. [code](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_value_callback/V2TimValueCallback/code.html) in the success callback parameter `V2TIMFriendOperationResult` returns the 30539 error code, indicating that user B's approval is required in this case. At this time, both users A and B receive the [onFriendApplicationListAdded](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendApplicationListAdded.html) callback.
4. User B receives the [onFriendApplicationListAdded](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendApplicationListAdded.html) callback. If [tyoe](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_friend_application/V2TimFriendApplication/type.html) in the parameter `V2TIMFriendApplication` is set to `V2TIMFriendApplication.V2TIM_FRIEND_APPLICATION_COME_IN`, user B can accept or reject the request.
	- User B calls [acceptFriendApplication](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/acceptFriendApplication.html) to accept the friend request. If the acceptance type is `FriendApplicationTypeEnum.V2TIM_FRIEND_ACCEPT_AGREE` (that is, accepting as a one-way friend), user A receives the [onFriendListAdded](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendListAdded.html) callback, indicating that a one-way relationship has been established. Meanwhile, user B receives the [onFriendApplicationListDeleted](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendApplicationListDeleted.html) callback, indicating that user B is now in user A's friend list, but user A is not in user B's friend list.
	- If the acceptance type is `FriendApplicationTypeEnum.V2TIM_FRIEND_ACCEPT_AGREE_AND_ADD` (that is, accepting as a two-way friend), both users A and B receive the [onFriendListAdded](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendListAdded.html) callback, indicating that they are now in each other's friend list.
	- User B calls [refuseFriendApplication](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/refuseFriendApplication.html) to reject the friend request, and both users receive the [onFriendApplicationListDeleted](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendApplicationListDeleted.html) callback.

### Friend group management
To group friends into categories such as "classmates" and "coworkers", call the following APIs.

| Feature                            | API                                                                                                                                                                                   |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create a friend group              | [createFriendGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/createFriendGroup.html)                       |
| Delete a friend group              | [deleteFriendGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendGroup.html)                       |
| Modify a friend group              | [renameFriendGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/renameFriendGroup.html)                       |
| Obtain the list of friend groups   | [getFriendGroups](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendGroups.html)                           |
| Add friends to a friend group      | [addFriendsToFriendGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriendsToFriendGroup.html)           |
| Delete friends from a friend group | [deleteFriendsFromFriendGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendsFromFriendGroup.html) |

## FAQs

### 1. How to disable messaging between two users who are not friends?
By default, the IM SDK does not prevent message sending and receiving between strangers. If you want messages to be sent or received only between friends, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Messages** > **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. After this feature is enabled, you can send messages only to friends. When you try to send messages to strangers, the IM SDK returns the 20009 error code.

[](id:msgSendTips)
### 2. How do I enable error messages when blocked users try to send a message?
When a user is added to the blocklist, by default, the user does not know that he/she is in the blocklist. That is, after this user sends a message, the user is still prompted that the message was sent successfully, but in fact, the recipient will not receive the message. If you want a user in the blocklist to know that his/her message failed to be sent, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. After this feature is disabled, the IM SDK will return the 20007 error code when a user in the blocklist sends a message.

### 3. Why can't the SDK enhanced edition get the latest user profiles?
There are two types of user profile updates in the enhanced SDK:
 - Friend's profile: when the profile of a friend is updated, the backend will send a system notification to the SDK, so the friend's profile will be updated in real time.
 - Stranger's profile: when the profile of a stranger is updated, the backend will not send any system notification because the stranger is not a friend of yours, so the stranger's profile will not be updated in real time. To avoid sending a network request to the backend every time the user profile is obtained, the SDK adds a caching logic, setting a 10-minute interval between pulls of the same user's profile from the backend.
