## User Profile Management
### Querying and modifying your own profile
Use [getUsersInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a0071a5be9f333698f05fd80aff203560) to **query your own profile**, where `userIDList` indicates your own UserID.
Use [setSelfInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2ff0139742c4a0bf6dce1ef7423f3bee) to **modify your own profile**. You will receive the [onSelfInfoUpdated](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94852c92bb087e5aabb6cf6fe9ba77f8) callback after the profile is modified successfully.

### Querying the profile of a non-friend
Use [getUsersInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a0071a5be9f333698f05fd80aff203560) to query the user profile of a non-friend, where `userIDList` indicates the UserID of the user to query.

### Querying and modifying a friend’s profile
Use [getFriendsInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a930bb2a8cd664a4037797970ce9fc0d8) to **query the profile of a specified friend**. Use `getRelation()` of `V2TIMFriendInfoResult` to obtain your relationship from the callback information:
- `V2TIM_FRIEND_RELATION_TYPE_NONE`: the user is not a friend.
- `V2TIM_FRIEND_RELATION_TYPE_BOTH_WAY`: the user is a two-way friend.
- `V2TIM_FRIEND_RELATION_TYPE_IN_MY_FRIEND_LIST`: the user is in your friend list.

Use [setFriendInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a97409aaccf135d60344f002aca06e63e) to **modify the information of a specified friend**, such as friend remarks.

## Blocking Messages from a Specified User
- **Blocking a user**
To block messages from a specified user, call the [addToBlackList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a67d998da5085b5004bb6aa8d4322022c) API to block the user.
By default, the blocked user is unaware of the "blocked" status. An error code indicating blocking will not be returned after the user sends a message. If you want blocked users to receive error message in this situation, see [How to display an error message to a blocked user after the user sends a message](#sos).

- **Removing a user from the blocklist**
Call [deleteFromBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#afe61664e0afee949f99ec63a288316e2) to remove a user from the blocklist and receive the user’s messages again.

- **Obtaining the blocklist**
Call [getBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#aa0e6338aefd556a23507c2798af6e717) to view and manage the blocklist.

## Friend Management

### Determining whether a friend request is required
By default, the IM SDK does not check the relationship between two parties when sending one-to-one chat messages. This default setting is generally applied in customer service scenarios, where having to friend a customer service agent before chatting is inefficient.
If you want to demand users to be friends before they can chat, as in WeChat and QQ, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Relationship Check**, and enable "Check Relationship for One-to-One Chat Messages". With this feature enabled, users can only send messages to friends and will receive the 20009 error code from the SDK when sending a message to a non-friend user.

### Friend list management

The IM SDK supports relationship chain logic. You can call [getFriendList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a8d03aec2e3efd16b7942944c6cb30d0e) to obtain the friend list, call [deleteFromFriendList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2786c60824ea6ec117429ef2b59630a1) to delete a friend from the friend list, or call [addFriend](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ae46b728a77d71e302e10b71ee6b0241e) to add a friend.

The process has the following varations depending on whether friend verification is required.

#### Friend request approval is not required
 1. User A and user B call [setFriendListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ae46b728a77d71e302e10b71ee6b0241e) to set a relationship chain listener.
 2. User B calls [setSelfInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2ff0139742c4a0bf6dce1ef7423f3bee) and sets [allowType](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMUserFullInfo.html#a39e2e474ee15e2a642a430baae72a787) to `V2TIM_FRIEND_ALLOW_ANY`.
 3. User A becomes user B’s friend simply by calling [addFriend](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ae46b728a77d71e302e10b71ee6b0241e) to send a friend request.
- If [addType](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMFriendAddApplication.html#a0b48b53a403cf4bf6aced22ee5557257) in the request parameter `V2TIMFriendAddApplication` is set to `V2TIM_FRIEND_TYPE_BOTH` (that is, setting as a two-way friend), both users A and B receive the [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) callback;
- If this value is set to `V2TIM_FRIEND_TYPE_SINGLE` (that is, setting as a one-way friend), only user A receives the [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) callback.

#### Friend request approval is required
1. User A and user B call [setFriendListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ae46b728a77d71e302e10b71ee6b0241e) to set a relationship chain listener.
2. User B calls [setSelfInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2ff0139742c4a0bf6dce1ef7423f3bee) and sets [allowType](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMUserFullInfo.html#a39e2e474ee15e2a642a430baae72a787) to `V2TIM_FRIEND_NEED_CONFIRM`.
3. User A calls [addFriend](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ae46b728a77d71e302e10b71ee6b0241e) to send a friend request to user B. `resultCode` in the success callback parameter `V2TIMFriendOperationResult` returns the 30539 error code, indicating that user B’s approval is required in this case. At this time, both users A and B receive the [onFriendApplicationListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a54c7c648088b88ebf0f235d363670566) callback.
4. User B receives the [onFriendApplicationListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a54c7c648088b88ebf0f235d363670566) callback. If [type](http://doc.qcloudtrtc.com/im/interfaceV2TIMFriendApplication.html#a9e52fd30b3c8d77f7f6f50034f6ce2b7) in the parameter `V2TIMFriendApplication` is set to `V2TIM_FRIEND_APPLICATION_COME_IN`, user B can accept or reject the request.
    - User B calls [acceptFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2546222b4994a5be9f67dfa8eb504e6b) to accept the friend request. If the acceptance type is `V2TIM_FRIEND_ACCEPT_AGREE` (that is, accepting as a one-way friend), user A receives the [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) callback, indicating that a one-way relationship has been established. Meanwhile, user B receives the [onFriendApplicationListDeleted](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a143207515faa3de58c8222afc21736e6) callback, indicating that user B is now in user A’s friend list, but user A is not in user B’s friend list.
- User B calls [acceptFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2546222b4994a5be9f67dfa8eb504e6b) to accept the friend request. If the acceptance type is `V2TIM_FRIEND_ACCEPT_AGREE_AND_ADD` (that is, accepting as a two-way friend), both users A and B receive the [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) callback, indicating that they are now in each other’s friend list.
    - User B calls [refuseFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#acb564676b24c76609acf645c4ad999ad) to reject the friend request and both users receive the [onFriendApplicationListDeleted](https://im.sdk.qcloud.com/doc/en/protocolV2TIMFriendshipListener-p.html#a143207515faa3de58c8222afc21736e6) callback.

### Friend group management
To group friends into categories such as "classmates" and "coworkers", call the following APIs.

| Feature | API |
|---------|---------|
| Create a friend group | [createFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#acd85704b4a6ad4293d8bbcdb73385f4c) |
| Delete a friend group | [deleteFriendGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a2dc49f2abb1238fc2d47ce6d4f14c1e7) |
| Modify a friend group | [renameFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2677f9d9febe8f28f16f3972f7c45638) |
| Obtain the list of friend groups | [getFriendGroupList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a44c12380968b1d51c5ea5f90fa627a56) |
| Add friends to a friend group | [addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a24b2297a1d9c2c3fa816839b3108ef72) |
| Delete friends from a friend group | [deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a65380db025573ac7c6d20f66a8b40ee2) |



## FAQs

### How can I disable messaging between two users who are not friends?
By default, the IM SDK does not prevent message sending and receiving between strangers. If you want messages to be sent or received only between friends, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Messages** > **Relationship Check**, and enable **Check Relationship for One-to-One Chat Messages**. After this feature is enabled, you can send messages only to friends. When you try to send messages to strangers, the IM SDK returns the 20009 error code.

[](id:sos) 
### 2. How do I enable error messages when blocked users try to send a message?
When a user is added to the blocklist, by default, the user does not know that he/she is in the blocklist. That is, after this user sends a message, the user is still prompted that the message was sent successfully, but in fact, the recipient will not receive the message. If you want a user in the blocklist to know that his/her message failed to be sent, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Messages** > **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. After this feature is disabled, the IM SDK will return the 20007 error code when a user in the blocklist sends a message.

### 3. Why can't the SDK enhanced edition get the latest user profiles?
There are two types of user profile updates in the enhanced SDK: friend's profile and stranger's profile:
- Friend's profile: when the profile of a friend is updated, the backend will send a system notification to the SDK, so the friend's profile will be updated in real time.
- Stranger's profile: when the profile of a stranger is updated, the backend will not send any system notification because the stranger is not a friend of yours, so the stranger's profile will not be updated in real time. To avoid sending a network request to the backend every time the user profile is obtained, the SDK adds a caching logic, setting a 10-minute interval between pulls of the same user's profile from the backend.
