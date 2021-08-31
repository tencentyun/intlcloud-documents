## User Profile Management
### Querying and modifying your own profile
Use [getUsersInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#ac638c1dd6ec1e5204637e4b87129cd38) to **query your own profile**, where `userIDList` indicates your own UserID.
Use [setSelfInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a328a0d2d07e8d34e12effb73937c3437) to **modify your own profile**. You will receive the [onSelfInfoUpdated](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94852c92bb087e5aabb6cf6fe9ba77f8) callback after the profile is modified successfully.

### Querying the profile of a non-friend
Use [getUsersInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#ac638c1dd6ec1e5204637e4b87129cd38) to query the user profile of a non-friend, where `userIDList` indicates the UserID of the user to query.

### Querying and modifying a friend’s profile
Use [getFriendsInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a39f6752da11b595e4a5b6dcb0eb6a584) to **query the profile of a specified friend**. Use `getRelation()` of `V2TIMFriendInfoResult` to obtain your relationship from the callback information:
- `V2TIM_FRIEND_RELATION_TYPE_NONE`: the user is not a friend.
- `V2TIM_FRIEND_RELATION_TYPE_BOTH_WAY`: the user is a two-way friend.
- `V2TIM_FRIEND_RELATION_TYPE_IN_MY_FRIEND_LIST`: the user is in your friend list.

Use [setFriendInfo](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#ac258312c000c1af69fcf51dd6898b74b) to **modify the information of a specified friend**, such as friend remarks.

## Blocking Messages from a Specified User
- **Blocking a user**
To block messages from a specified user, call the [addToBlackList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a67d998da5085b5004bb6aa8d4322022c) API to block the user.
By default, the blocked user is unaware of the "blocked" status. An error code indicating blocking will not be returned after the user sends a message. If you want blocked users to receive error message in this situation, see [How to display an error message to a blocked user after the user sends a message](#sos).

- **Removing a user from the blocklist**
Call [deleteFromBlackList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#aa7e69a67185eaca658ba429cf6309a5f) to remove a user from the blocklist and receive the user’s messages again.

- **Obtaining the blocklist**
Call [getBlackList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a0d854d64c8ae936014a8424d55508fa3) to view and manage the blocklist.

## Friend Management

### Determining whether a friend request is required
By default, the IM SDK does not check the relationship between two parties when sending one-to-one chat messages. This default setting is generally applied in customer service scenarios, where having to friend a customer service agent before chatting is inefficient.
If you want to demand users to be friends before they can chat, as in WeChat and QQ, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Relationship Check**, and enable "Check Relationship for One-to-One Chat Messages". With this feature enabled, users can only send messages to friends and will receive the 20009 error code from the SDK when sending a message to a non-friend user.

### Friend list management

The IM SDK supports relationship chain logic. You can call [getFriendList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a81131d76924a03ec2b593addd6e4e101) to obtain the friend list, call [deleteFromFriendList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#af967134fb177b32d4060fedf3663ace3) to delete a friend from the friend list, or call [addFriend](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#ac1ea1c7de2bfc2b0a25e5f6b3192e304) to add a friend.

The process has the following varations depending on whether friend verification is required.

#### Friend request approval is not required
 1. User A and user B call [setFriendListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#acd403f586f3df84f56b1b757efb2d443) to set a relationship chain listener.
 2. User B calls [setSelfInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a328a0d2d07e8d34e12effb73937c3437) and sets [allowType](http://doc.qcloudtrtc.com/im/interfaceV2TIMUserFullInfo.html#a39e2e474ee15e2a642a430baae72a787) to `V2TIM_FRIEND_ALLOW_ANY`.
 3. User A becomes user B’s friend simply by calling [addFriend](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#ac1ea1c7de2bfc2b0a25e5f6b3192e304) to send a friend request.
- If [addType](http://doc.qcloudtrtc.com/im/interfaceV2TIMFriendAddApplication.html#a0b48b53a403cf4bf6aced22ee5557257) in the request parameter `V2TIMFriendAddApplication` is set to `V2TIM_FRIEND_TYPE_BOTH` (that is, setting as a two-way friend), both users A and B receive the [onFriendListAdded](http://doc.qcloudtrtc.com/im/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) callback;
- If this value is set to `V2TIM_FRIEND_TYPE_SINGLE` (that is, setting as a one-way friend), only user A receives the [onFriendListAdded](http://doc.qcloudtrtc.com/im/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) callback.

#### Friend request approval is required
1. User A and user B call [setFriendListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#acd403f586f3df84f56b1b757efb2d443) to set a relationship chain listener.
2. User B calls [setSelfInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a328a0d2d07e8d34e12effb73937c3437) and sets [allowType](http://doc.qcloudtrtc.com/im/interfaceV2TIMUserFullInfo.html#a39e2e474ee15e2a642a430baae72a787) to `V2TIM_FRIEND_NEED_CONFIRM`.
3. User A calls [addFriend](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#ac1ea1c7de2bfc2b0a25e5f6b3192e304) to send a friend request to user B. `resultCode` in the success callback parameter `V2TIMFriendOperationResult` returns the 30539 error code, indicating that user B’s approval is required in this case. At this time, both users A and B receive the [onFriendApplicationListAdded](http://doc.qcloudtrtc.com/im/protocolV2TIMFriendshipListener-p.html#a54c7c648088b88ebf0f235d363670566) callback.
4. User B receives the [onFriendApplicationListAdded](http://doc.qcloudtrtc.com/im/protocolV2TIMFriendshipListener-p.html#a54c7c648088b88ebf0f235d363670566) callback. If [type](http://doc.qcloudtrtc.com/im/interfaceV2TIMFriendApplication.html#a9e52fd30b3c8d77f7f6f50034f6ce2b7) in the parameter `V2TIMFriendApplication` is set to `V2TIM_FRIEND_APPLICATION_COME_IN`, user B can accept or reject the request.
    - User B calls [acceptFriendApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a51b913927028025e2e450e6e8ce848c0) to accept the friend request. If the acceptance type is `V2TIM_FRIEND_ACCEPT_AGREE` (that is, accepting as a one-way friend), user A receives the [onFriendListAdded](http://doc.qcloudtrtc.com/im/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) callback, indicating that a one-way relationship has been established. Meanwhile, user B receives the [onFriendApplicationListDeleted](http://doc.qcloudtrtc.com/im/protocolV2TIMFriendshipListener-p.html#a143207515faa3de58c8222afc21736e6) callback, indicating that user B is now in user A’s friend list, but user A is not in user B’s friend list.
- User B calls [acceptFriendApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a51b913927028025e2e450e6e8ce848c0) to accept the friend request. If the acceptance type is `V2TIM_FRIEND_ACCEPT_AGREE_AND_ADD` (that is, accepting as a two-way friend), both users A and B receive the [onFriendListAdded](http://doc.qcloudtrtc.com/im/protocolV2TIMFriendshipListener-p.html#a84234f0601846547f84904472ab820f8) callback, indicating that they are now in each other’s friend list.
    - User B calls [refuseFriendApplication](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a406b964a6513219cfe4803f87f0f00f8) to reject the friend request and both users receive the [onFriendApplicationListDeleted](http://doc.qcloudtrtc.com/im/protocolV2TIMFriendshipListener-p.html#a143207515faa3de58c8222afc21736e6) callback.

### Friend group management
To group friends into categories such as "classmates" and "coworkers", call the following APIs.

| Feature | API |
|---------|---------|
| Create a friend group | [createFriendGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a231a334fa4a064042d65a67f267ec664) |
| Delete a friend group | [deleteFriendGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a2dc49f2abb1238fc2d47ce6d4f14c1e7) |
| Modify a friend group | [renameFriendGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a93f6ba132d9706db7c74daff97a2abd0) |
| Obtain the list of friend groups | [getFriendGroupList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a63f3eaae567586077d5a8d27c31e2229) |
| Add friends to a friend group | [addFriendsToFriendGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a0265241c39600c390406ca1f8f6ff75d) |
| Delete friends from a friend group | [deleteFriendsFromFriendGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a4a14a878816c8d6a20981d1903fcf359) |



## FAQs

### How can I disable messaging between two users who are not friends?
By default, the IM SDK does not prevent message sending and receiving between strangers. If you want messages to be sent or received only between friends, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Messages** > **Relationship Check**, and enable **Check Relationship for One-to-One Chat Messages**. After this feature is enabled, you can send messages only to friends. When you try to send messages to strangers, the IM SDK returns the 20009 error code.

[](id:sos) 
### 2. How do I enable error messages when blocked users try to send a message?
When a user is added to the blocklist, by default, the user does not know that he/she is in the blocklist. That is, after this user sends a message, the user is still prompted that the message was sent successfully, but in fact, the recipient will not receive the message. If you want a user in the blocklist to know that his/her message failed to be sent, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Messages** > **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. After this feature is disabled, the IM SDK will return the 20007 error code when a user in the blocklist sends a message.
