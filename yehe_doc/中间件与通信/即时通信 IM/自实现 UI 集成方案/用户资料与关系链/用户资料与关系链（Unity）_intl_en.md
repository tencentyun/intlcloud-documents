## User Profile Management

### Querying and modifying your own profile

-  Use [ProfileGetUserProfileList](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_ProfileGetUserProfileList_com_tencent_imsdk_unity_types_FriendShipGetProfileListParam_com_tencent_imsdk_unity_callback_ValueCallback_) to **query your own profile**, where `userIDList` indicates your own UserID.
- Use [ProfileModifySelfUserProfile](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_ProfileModifySelfUserProfile_com_tencent_imsdk_unity_types_UserProfileItem_com_tencent_imsdk_unity_callback_ValueCallback_) to **modify your own profile**. You will receive the [UpdateFriendProfileCallback](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.callback.UpdateFriendProfileCallback.html) callback after your profile is modified successfully.

## Blocking Messages from a Specified User

- **Blocking a user*
  To block messages from a specified user, call the [FriendshipAddToBlackList](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipAddToBlackList_System_Collections_Generic_List_System_String__com_tencent_imsdk_unity_callback_ValueCallback_) API to add the user to the blocklist to block the user.
  By default, the blocked user is unaware of the "blocked" status. An error code indicating blocking will not be returned after the user sends a message. If you want blocked users to receive the blocked message in this situation, see [How do I enable error messages when blocked users try to send a message](#block).
- **Removing a user from the blocklist**
  Call [FriendshipDeleteFromBlackList](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipDeleteFromBlackList_System_Collections_Generic_List_System_String__com_tencent_imsdk_unity_callback_ValueCallback_) to remove a user from your blocklist and receive the user's messages again.
- **Obtaining the blocklist**
  Call [FriendshipGetBlackList](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipGetBlackList_com_tencent_imsdk_unity_callback_ValueCallback_) to view and manage the blocklist.

## Friend Management

### Determining whether a friend request is required

By default, the IM SDK does not check the relationship between two parties when sending one-to-one chat messages. This default setting is generally applied in customer service scenarios, where having to friend a customer service agent before chatting is inefficient.
If you want to demand users to be friends before they can chat, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. With this feature enabled, users can send messages to friends only, and will receive the 20009 error code from the SDK when sending a message to a non-friend user.
![](https://qcloudimg.tencent-cloud.cn/raw/be6046b44a6f6bd3b47be3ba1b0de55d.png)

### Friend list management

The IM SDK supports relationship chain logic. You can call [FriendshipGetFriendProfileList](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipGetFriendProfileList_com_tencent_imsdk_unity_callback_ValueCallback_) to obtain the friend list, or call [FriendshipAddFriend](https://comm.qq.com/im/sdk/unity_plus/_site/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipAddFriend_com_tencent_imsdk_unity_types_FriendshipAddFriendParam_com_tencent_imsdk_unity_callback_ValueCallback_) to add a friend.

## FAQs

### 1. How to disable messaging between two users who are not friends?

By default, the IM SDK does not prevent message sending and receiving between strangers. If you want messages to be sent or received only between friends, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Messages** > **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. After this feature is enabled, you can send messages only to friends. When you try to send messages to strangers, the IM SDK returns the 20009 error code.

### 2. How do I enable error messages when blocked users try to send a message?[](id:block)

When a user is added to the blocklist, by default, the user does not know that he/she is in the blocklist. That is, after this user sends a message, the user is still prompted that the message was sent successfully, but in fact, the recipient will not receive the message. If you want a user in the blocklist to know that his/her message failed to be sent, log in to the [IM console](https://console.cloud.tencent.com/im), choose **Feature Configuration** > **Login and Message** > **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. After this feature is disabled, the IM SDK will return the 20007 error code when a user in the blocklist sends a message.

### 3. Why can't the SDK enhanced edition get the latest user profiles?

There are two types of user profile updates in the enhanced SDK:

- Friend's profile: when the profile of a friend is updated, the backend will send a system notification to the SDK, so the friend's profile will be updated in real time.
- Stranger's profile: when the profile of a stranger is updated, the backend will not send any system notification because the stranger is not a friend of yours, so the stranger's profile will not be updated in real time. To avoid sending a network request to the backend every time the user profile is obtained, the SDK adds a caching logic, setting a 10-minute interval between pulls of the same user's profile from the backend.
