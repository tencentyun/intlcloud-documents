## Initialization and Login APIs

To use Tencent Cloud IM services, you need to perform initialization and log in.

| API | Description |
|---------|---------|
| [initSDK](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_initSDK_System_Int32_com_tencent_imsdk_unity_LogLevel_) | Initializes the SDK. |
| [unInitSDK](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_unInitSDK) | Uninitializes the SDK. |
| [login](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_login_System_String_System_String_) | Logs in. |
| [logout](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_logout) | Logs out. |
| [getLoginStatus](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_getLoginStatus) | Gets the login status. |
| [getLoginUser](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_getLoginUser) | Gets the UserID of the current login user. |

## Advanced Message APIs

If you need to send/receive rich media messages (images, videos, files, etc.) and use advanced features such as recalling messages, marking messages as read, and querying message history, use the following set of advanced message APIs. Do not use simple messages APIs and advanced message APIs at the same time.

| API | Description |
|---------|---------|
| [addAdvancedMsgListener](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_addAdvancedMsgListener) | Sets an event listener for advanced messages. Do not use it and `addSimpleMsgListener` at the same time. |
| [sendCustomMessage](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendCustomMessage_System_String_System_String_System_Int32_System_Boolean_System_String_) | Sends a custom message. |
| [sendImageMessage](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendImageMessage_System_String_System_String_System_Int32_System_Boolean_System_String_) | Sends an image message. |
| [sendSoundMessage](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendSoundMessage_System_String_System_String_System_Int32_System_Boolean_System_String_System_Int32_) | Sends a voice message. |
| [sendVideoMessage](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendVideoMessage_System_String_System_String_System_Int32_System_Boolean_System_String_System_String_System_String_System_Int32_) | Sends a video message. |
| [sendFileMessage](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendFileMessage_System_String_System_String_System_Int32_System_Boolean_System_String_System_String_) | Sends a file message. |
| [sendLocationMessage](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendLocationMessage_System_String_System_String_System_Int32_System_Boolean_System_Double_System_Double_) | Sends a location message. |
| [getC2CHistoryMessageList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_getC2CHistoryMessageList_System_Int32_System_String_System_String_) | Gets the one-to-one (C2C) message history. |
| [getGroupHistoryMessageList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_getGroupHistoryMessageList_System_Int32_System_String_System_String_) | Gets the group message history. |
| [markC2CMessageAsRead](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_markC2CMessageAsRead_System_String_) | Marks one-to-one (C2C) messages as read. |
| [markGroupMessageAsRead](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_markGroupMessageAsRead_System_String_) | Marks group messages as read. |
| [deleteMessageFromLocalStorage](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_deleteMessageFromLocalStorage_System_String_) | Deletes a message from the local storage. |
| [insertGroupMessageToLocalStorage](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_insertGroupMessageToLocalStorage_System_String_System_String_System_String_) | Adds a message to the group message list. |


## Group APIs

Tencent Cloud IM SDK supports four preset group types, each of which pertains to different scenarios.
- Work group (Work): similar to a WeChat group. Users can join the group only after being invited by group members. Same as private group (Private) in earlier versions.
- Public group (Public): similar to a QQ group. Users can join the group through requests, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): used together with [TRTC](https://intl.cloud.tencent.com/product/trtc) to enable scenarios such as video conferencing and online education. Users can join and leave the group freely and view the message history before they join. Same as chat room (ChatRoom) in earlier versions.
- Audio-video group (AVChatRoom): suitable for scenarios such as live streaming and chat rooms with on-screen comments. Users can join and leave the group freely. There is no limit on the number of group members.

| API | Description |
|---------|---------|
| [setGroupListener](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_setGroupListener) | Sets an event listener for groups. |
| [createGroup](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_createGroup_System_String_System_String_System_String_System_String_System_String_System_String_com_tencent_imsdk_unity_CreateGroupMemberInfoEntity___) | Creates a group (advanced). The group information and the initial group members can be set during group creation. |
| [joinGroup](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_joinGroup_System_String_System_String_) | Joins a group. |
| [quitGroup](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_quitGroup_System_String_) | Quits a group. |
| [dismissGroup](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_dismissGroup_System_String_) | Deletes a group. Only the group owner and group admin can delete the group. |
| [getJoinedGroupList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_getJoinedGroupList) | Gets the list of groups the current user has joined, excluding audio-video groups. |
| [getGroupsInfo](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_getGroupsInfo_System_String___) | Pulls the profiles of groups. |
| [setGroupInfo](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_setGroupInfo_System_String_System_String_System_String_System_String_System_String_System_String_System_Boolean_com_tencent_imsdk_unity_GroupAddOptType_) | Modifies the profile of a group. |
| [getGroupMemberList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_getGroupMemberList_System_String_com_tencent_imsdk_unity_GroupMemberFilterType_System_Int32_) | Gets the group member list. |
| [getGroupMembersInfo](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_getGroupMembersInfo_System_String_System_String___) | Gets the profiles of specified group members. |
| [setGroupMemberInfo](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_setGroupMemberInfo_System_String_System_String_System_String_) | Modifies the profile of a specified group member. |
| [muteGroupMember](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_muteGroupMember_System_String_System_String_System_Int32_) | Mutes a group member. |
| [kickGroupMember](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_kickGroupMember_System_String_System_String___System_String_) | Removes a member from a group. |
| [setGroupMemberRole](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_setGroupMemberRole_System_String_System_String_com_tencent_imsdk_unity_GroupMemberRoleType_) | Sets the role for a group member. |
| [transferGroupOwner](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_transferGroupOwner_System_String_System_String_) | Changes the group owner. |
| [inviteUserToGroup](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_inviteUserToGroup_System_String_System_String___) | Invites users to a group. |
| [getGroupApplicationList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_getGroupApplicationList) | Gets the list of requests to join a group. |
| [acceptGroupApplication](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_acceptGroupApplication_System_String_System_String_System_String_) | Accepts a request to join a group. |
| [refuseGroupApplication](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_refuseGroupApplication_System_String_System_String_System_String_) | Rejects a request to join a group. |
| [setGroupApplicationRead](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_setGroupApplicationRead) | Marks the request list as read. |

## Conversation List APIs

The conversation list is the list a user sees on the first screen after logging in to WeChat or QQ. It includes elements such as conversation node, conversation name, group name, last message, and unread count.

| API | Description |
|---------|---------|
| [setConversationListener](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_setConversationListener) | Sets a conversation listener. |
| [getConversationList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMConversationManager.html#com_tencent_imsdk_unity_V2TIMConversationManager_getConversationList_System_Int32_System_Int32_) | Gets the conversation list. |
| [deleteConversation](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMConversationManager.html#com_tencent_imsdk_unity_V2TIMConversationManager_deleteConversation_System_String_) | Deletes a conversation. |
| [setConversationDraft](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMConversationManager.html#com_tencent_imsdk_unity_V2TIMConversationManager_setConversationDraft_System_String_System_String_) | Sets a draft for a conversation. |

## User Profile APIs

APIs for querying user profiles, modifying one's own user profile, and blocking messages from a specified user (or adding a specified user to the blocklist).

| API | Description |
|---------|---------|
| [getUsersInfo](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_getUsersInfo_System_String___) | Gets user profiles. |
| [setSelfInfo](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_setSelfInfo_System_String_System_String_System_String_com_tencent_imsdk_unity_Gender_com_tencent_imsdk_unity_FriendAllowType_Dictionary_System_String_System_String__) | Modifies one's own user profile. |
| [addToBlackList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_addToBlackList_System_String___) | Blocks the messages from a user, which means adding the user to the blocklist. |
| [deleteFromBlackList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_deleteFromBlackList_System_String___) | Unblocks the messages from a user, which means removing the user from the blocklist. |
| [getBlackList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_getBlackList) | Gets the blocklist. |
[setOfflinePushConfig](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_offline_push_manager/V2TIMOfflinePushManager/setOfflinePushConfig.html) | Sets the offline push configuration. |

## Friend Management APIs

By default, Tencent Cloud IM does not check your relationship with a user when receiving and sending messages. You can enable the "Check Relationship for One-to-One Messages" on **Feature Configuration** > **Login and Message** > **Relationship Check** in the [IM console](https://console.cloud.tencent.com/im) and use the following APIs to delete/add friends and manage your friend list.

| API | Description |
|---------|---------|
| [setFriendListener](sdk.unity.V2TIMMahttps://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imnager.html#com_tencent_imsdk_unity_V2TIMManager_setFriendListener) | Sets a relationship chain listener to receive friend list and blocklist change events. |
| [getFriendsList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_getFriendList) | Gets the friend list. |
| [getFriendsInfo](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_getFriendsInfo_System_String___) | Gets the profiles of specified friends. |
| [setFriendInfo](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_setFriendInfo_System_String_System_String_Dictionary_System_String_System_String__) | Sets the profile of a specified friend. |
| [addFriend](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_addFriend_System_String_com_tencent_imsdk_unity_FriendType_System_String_System_String_System_String_) | Adds a friend. |
| [deleteFromFriendList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_deleteFromFriendList_System_String___com_tencent_imsdk_unity_FriendType_) | Deletes a friend. |
| [checkFriend](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_checkFriend_System_String_) | Checks your relationship with a specified user. |
| [getFriendApplicationList](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_getFriendApplicationList) | Gets the list of friend requests. |
| [acceptFriendApplication](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_acceptFriendApplication_System_String_com_tencent_imsdk_unity_FriendAcceptType_) | Accepts a friend request. |
| [refuseFriendApplication](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_refuseFriendApplication_System_String_) | Rejects a friend request. |
| [deleteFriendApplication](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_deleteFriendApplication_System_String_) | Deletes a friend request. |
| [setFriendApplicationRead](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_setFriendApplicationRead) | Sets a friend request as read. |
| [createFriendGroup](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_createFriendGroup_System_String_System_String___) | Creates a friend list. |
| [getFriendGroups](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_getFriendGroups_System_String___) | Gets the information of friend lists. |
| [deleteFriendGroup](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_deleteFriendGroup_System_String___) | Deletes friend lists. |
| [renameFriendGroup](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_renameFriendGroup_System_String_System_String_) | Modifies the name of a friend list. |
| [addFriendsToFriendGroup](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_addFriendsToFriendGroup_System_String_System_String___) | Adds friends to a friend list. |
| [deleteFriendsFromFriendGroup](https://comm.qq.com/unity-im-sdk-document/v1.6.0/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_deleteFriendsFromFriendGroup_System_String_System_String___) | Deletes friends from a friend list. |
