## User Profile Management
### Querying and modifying your own profile
Use [getUsersInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e) to **query your own profile**, where `userIDList` indicates your own UserID.
Use [setSelfInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a) to **modify your own profile**. You will receive the [onSelfInfoUpdated](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94852c92bb087e5aabb6cf6fe9ba77f8) callback after your profile is modified successfully.

### Querying the profile of a non-friend
Use [getUsersInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e) to query the user profile of a non-friend, where `userIDList` indicates the UserID of the user to query.

### Querying and modifying a friend’s profile
Use [getFriendsInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a88732b0f7a5e77a9dd34403fe7bbdd21) to **query the profile of a specified friend**. Use `getRelation()` of `V2TIMFriendInfoResult` to obtain your relationship from the callback information:
- `V2TIMCheckFriendResult.V2TIM_FRIEND_RELATION_TYPE_NONE`: the user is not a friend.
- `V2TIMCheckFriendResult.V2TIM_FRIEND_RELATION_TYPE_BOTH_WAY`: the user is a two-way friend.
- `V2TIMCheckFriendResult.V2TIM_FRIEND_RELATION_TYPE_IN_MY_FRIEND_LIST`: the user is in your friend list.

Use [setFriendInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a151b7de6219d966b4194ad7fcc8450fe) to **modify the information of a specified friend**, such as friend remarks.

## Blocking Messages from a Specified User
- **Blocking a user**
To block messages from a specified user, call the [addToBlackList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8804c7f47000bf1c26aa6ab744a53456) API to block the user.
By default, the blocked user is unaware of the "blocked" status. An error code indicating blocking will not be returned after the user sends a message. If you want blocked users to receive the blocked message in this situation, see [How to display an error message to a blocked user after the user sends a message](#msgSendTips).

- **Removing a user from the blocklist**
Call [deleteFromBlackList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3dcd8f1c70dceafa94ab48796c2f26aa) to remove a user from your blocklist and receive the user’s messages again.

- **Obtaining the blocklist**
Call [getBlackList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6269df2d96c910648ab2f0c43e1931c6) to view and manage the blocklist.

## Friend Management
### Determining whether a friend request is required
By default, the IM SDK does not check the relationship between two parties when sending one-to-one chat messages. This default setting is generally applied in customer service scenarios, where having to friend a customer service agent before chatting is inefficient.
If you want to demand users to be friends before they can chat, as in WeChat and QQ, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Relationship Check**, and enable "Check Relationship for One-to-One Chat Messages". With this feature enabled, users can only send messages to friends and will receive the 20009 error code from the SDK when sending a message to a non-friend user.

### Friend list management

The IM SDK supports relationship chain logic. You can call [getFriendList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae478de55db21d42b72a6c5a6a5d16624) to obtain the friend list, call [deleteFromFriendList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af7ecf8641b58462d038a9c97bfbd4d61) to delete a friend from the friend list, or call [addFriend](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208) to add a friend.

The process has the following varations depending on whether friend verification is required.

#### Friend request approval is not required
1. User A and user B call [setFriendListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a17e92c5ca9abad7afe25b654f1fcd75c) to set a relationship chain listener.
2. User B calls [setSelfInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a) and sets `info` to `V2TIM_FRIEND_ALLOW_ANY` through the [setAllowType](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMUserFullInfo.html#a80c0d66aff28d26d9aee2bd8c5f41e61) API.
3. User A becomes user B’s friend simply by calling [addFriend](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208) to send a friend request. If [setAddType](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendAddApplication.html#a2c03288fc9e47b30eb49259c206f97b5) in the request parameter `V2TIMFriendAddApplication` is set to `V2TIMFriendInfo.V2TIM_FRIEND_TYPE_BOTH` (that is, setting as a two-way friend), both users A and B receive the [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adf243539e005e2f7cdaa833fa4cd221c) callback.
If this value is set to `V2TIMFriendInfo.V2TIM_FRIEND_TYPE_SINGLE` (that is, setting as a one-way friend), only user A receives the [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adf243539e005e2f7cdaa833fa4cd221c) callback.

#### Friend request approval is required
1. User A and user B call [setFriendListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a17e92c5ca9abad7afe25b654f1fcd75c) to set a relationship chain listener.
2. User B calls [setSelfInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a) and sets `info` to `V2TIM_FRIEND_NEED_CONFIRM` through the [setAllowType](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMUserFullInfo.html#a80c0d66aff28d26d9aee2bd8c5f41e61) API.
3. User A calls [addFriend](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208) to send a friend request to user B. [getResultCode](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendOperationResult.html#ae27793c0f10a54e83dc5a7c5b6fc8843) in the success callback parameter `V2TIMFriendOperationResult` returns the 30539 error code, indicating that user B’s approval is required in this case. At this time, both users A and B receive the [onFriendApplicationListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adffb4589ee3fbeb1b7e0e95c4a80ccfa) callback.
4. User B receives the [onFriendApplicationListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adffb4589ee3fbeb1b7e0e95c4a80ccfa) callback. If [getType](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendApplication.html#aec389cbe6ac7aff8ce7196e7dbc007df) in the parameter `V2TIMFriendApplication` is set to `V2TIMFriendApplication.V2TIM_FRIEND_APPLICATION_COME_IN`, user B can accept or reject the request.
- User B calls [acceptFriendApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ab69ed69330428caff6f468b7df5259fa) to accept the friend request. If the acceptance type is `V2TIMFriendApplication.V2TIM_FRIEND_ACCEPT_AGREE` (that is, accepting as a one-way friend), user A receives the [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adf243539e005e2f7cdaa833fa4cd221c) callback, indicating that a one-way relationship has been established. Meanwhile, user B receives the [onFriendApplicationListDeleted](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#a64a3bec67f85ddfee3e0d4dafb3b1e46) callback, indicating that user B is now in user A’s friend list, but user A is not in user B’s friend list.
- If the acceptance type is `V2TIMFriendApplication.V2TIM_FRIEND_ACCEPT_AGREE_AND_ADD` (that is, accepting as a two-way friend), both users A and B receive the [onFriendListAdded](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#adf243539e005e2f7cdaa833fa4cd221c) callback, indicating that they are now in each other’s friend list.
- User B calls [refuseFriendApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af1bcbc196015de8e7a94b1575c466f89) to reject the friend request and both users receive the [onFriendApplicationListDeleted](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipListener.html#a64a3bec67f85ddfee3e0d4dafb3b1e46) callback.

### Friend group management
To group friends into categories such as "classmates" and "coworkers", call the following APIs.

| Feature | API |
|---------|---------|
| Create a friend group | [createFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#afe729e7a74d1e7fd06a5f23c155a08ae) |
| Delete a friend group | [deleteFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ac9f06f447ee4452aa12e078b48023cee) |
| Modify a friend group | [renameFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5345957f4d75d8e57ea3b4cff9adee13) |
| Obtain the list of friend groups | [getFriendGroupList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a0043ca81fdeec5d3e842e85278003d1e) |
| Add friends to a friend group | [addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6de9168d476ac14e21025ec5c26251df) |
| Delete friends from a friend group | [deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae367dfec88522e96d96c5ab942e50653) |

## FAQs

### How can I disable messaging between two users who are not friends?
By default, the IM SDK does not prevent message sending and receiving between strangers. If you want messages to be sent or received only between friends, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Messages** > **Relationship Check**, and enable **Check Relationship for One-to-One Chat Messages**. After this feature is enabled, you can send messages only to friends. When you try to send messages to strangers, the IM SDK returns the 20009 error code.

[](id:msgSendTips)
### 2. How do I enable error messages when blocked users try to send a message?
When a user is added to the blocklist, by default, the user does not know that he/she is in the blocklist. That is, after this user sends a message, the user is still prompted that the message was sent successfully, but in fact, the recipient will not receive the message. If you want a user in the blocklist to know that his/her message failed to be sent, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Messages** > **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. After this feature is disabled, the IM SDK will return the 20007 error code when a user in the blocklist sends a message.

### 3. Why can't the SDK enhanced edition get the latest user profiles?
There are two types of user profile updates in the enhanced SDK: friend's profile and stranger's profile:
- Friend's profile: when the profile of a friend is updated, the backend will send a system notification to the SDK, so the friend's profile will be updated in real time.
- Stranger's profile: when the profile of a stranger is updated, the backend will not send any system notification because the stranger is not a friend of yours, so the stranger's profile will not be updated in real time. To avoid sending a network request to the backend every time the user profile is obtained, the SDK adds a caching logic, setting a 10-minute interval between pulls of the same user's profile from the backend.
