## Initialization and Login APIs

To use Tencent Cloud IM services, you need to perform initialization and log in.

| API | Description |
|---------|---------|
| [initSDK](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_initSDK_System_Int32_com_tencent_imsdk_unity_LogLevel_) | Initializes the SDK. |
| [unInitSDK](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_unInitSDK) | Uninitializes the SDK. |
| [login](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_login_System_String_System_String_) | Logs in. |
| [logout](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_logout) | Logs out. |
| [getLoginStatus](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_getLoginStatus) | Gets the login status. |
| [getLoginUser](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_getLoginUser) | Gets the UserID of the current login user. |

## Simple Message APIs

Use the following message APIs if you only need to use text and signaling (a piece of custom buffer) messages.

| API | Description |
|---------|---------|
| [addSimpleMsgListener](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_addSimpleMsgListener) | Sets an event listener for simple messages (text messages and custom messages). Do not use it and [addAdvancedMsgListener](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_addAdvancedMsgListener) at the same time. |
| [sendC2CTextMessage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendC2CTextMessage_System_String_System_String_) | Sends a one-to-one (C2C) text message. |
| [sendC2CCustomMessage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendC2CCustomMessage_System_String_System_String_) | Sends a one-to-one (C2C) custom (signaling) message. |
| [sendGroupTextMessage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendGroupTextMessage_System_String_System_String_com_tencent_imsdk_unity_MessagePriority_) | Sends a group text message. |
| [sendGroupCustomMessage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendGroupCustomMessage_System_String_System_String_com_tencent_imsdk_unity_MessagePriority_) | Sends a group custom (signaling) message. |

## Signaling APIs

| API | Description |
|---------|---------|
| [addSignalingListener](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMSignallingManager.html#com_tencent_imsdk_unity_V2TIMSignallingManager_addInvitedSignaling_com_tencent_imsdk_unity_SignalingInfo_) | Adds a signaling listener. |
| [invite](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMSignallingManager.html#com_tencent_imsdk_unity_V2TIMSignallingManager_invite_System_String_System_String_System_Boolean_System_Int32_com_tencent_imsdk_unity_OfflinePushInfo_) | Invites a user. |
| [inviteInGroup](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMSignallingManager.html#com_tencent_imsdk_unity_V2TIMSignallingManager_inviteInGroup_System_String_System_String___System_String_System_Boolean_System_Int32_) | Invites certain users in the group. |
| [cancel](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMSignallingManager.html#com_tencent_imsdk_unity_V2TIMSignallingManager_cancel_System_String_System_String_) | The inviter cancels the invitation. |
| [accept](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMSignallingManager.html#com_tencent_imsdk_unity_V2TIMSignallingManager_accept_System_String_System_String_) | The invitee accepts the invitation. |
| [reject](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMSignallingManager.html#com_tencent_imsdk_unity_V2TIMSignallingManager_reject_System_String_System_String_) | The invitee rejects the invitation. |

## Advanced Message APIs

If you need to send/receive rich media messages (images, videos, files, etc.) and use advanced features such as recalling messages, marking messages as read, and querying message history, use the following set of advanced message APIs. Do not use simple messages APIs and advanced message APIs at the same time.

| API | Description |
|---------|---------|
| [addAdvancedMsgListener](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_addAdvancedMsgListener) | Sets an event listener for advanced messages. Do not use it and `addSimpleMsgListener` at the same time. |
| [sendCustomMessage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendCustomMessage_System_String_System_String_System_Int32_System_Boolean_System_String_) | Sends a custom message. |
| [sendImageMessage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendImageMessage_System_String_System_String_System_Int32_System_Boolean_System_String_) | Sends an image message. |
| [sendSoundMessage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendSoundMessage_System_String_System_String_System_Int32_System_Boolean_System_String_System_Int32_) | Sends a voice message. |
| [sendVideoMessage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendVideoMessage_System_String_System_String_System_Int32_System_Boolean_System_String_System_String_System_String_System_Int32_) | Sends a video message. |
| [sendFileMessage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendFileMessage_System_String_System_String_System_Int32_System_Boolean_System_String_System_String_) | Sends a file message. |
| [sendLocationMessage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_sendLocationMessage_System_String_System_String_System_Int32_System_Boolean_System_Double_System_Double_) | Sends a location message. |
| [getC2CHistoryMessageList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_getC2CHistoryMessageList_System_Int32_System_String_System_String_) | Gets the one-to-one (C2C) message history. |
| [getGroupHistoryMessageList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_getGroupHistoryMessageList_System_Int32_System_String_System_String_) | Gets the group message history. |
| [markC2CMessageAsRead](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_markC2CMessageAsRead_System_String_) | Marks one-to-one (C2C) messages as read. |
| [markGroupMessageAsRead](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_markGroupMessageAsRead_System_String_) | Marks group messages as read. |
| [deleteMessageFromLocalStorage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_deleteMessageFromLocalStorage_System_String_) | Deletes a message from the local storage. |
| [insertGroupMessageToLocalStorage](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMMessageManager.html#com_tencent_imsdk_unity_V2TIMMessageManager_insertGroupMessageToLocalStorage_System_String_System_String_System_String_) | Adds a message to the group message list. |

## Group APIs

Tencent Cloud IM SDK supports four preset group types, each of which pertains to different scenarios.
- Work group (Work): similar to a regular WeChat group. Users can only join the group by being invited by existing group members.
- Public group (Public): similar to a QQ group. Users can join the group through requests, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): when used with [TRTC](https://intl.cloud.tencent.com/product/trtc), ideal for scenarios such as video conferencing and online education. Users can join and exit the group freely and view the existing message history before they join the group.
- Audio-video group (AVChatRoom): suitable for scenarios such as live streaming and chat rooms with on-screen comments. Users can join and exit the group freely. There is no limit on the number of group members.

| API | Description |
|---------|---------|
| [setGroupListener](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_setGroupListener) | Sets an event listener for groups. |
| [createGroup](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_createGroup_System_String_System_String_System_String_System_String_System_String_System_String_com_tencent_imsdk_unity_CreateGroupMemberInfoEntity___) | Creates a group (advanced). The group information and the initial group members can be set during group creation. |
| [joinGroup](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_joinGroup_System_String_System_String_) | Joins a group. |
| [quitGroup](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_quitGroup_System_String_) | Quits a group. |
| [dismissGroup](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_dismissGroup_System_String_) | Deletes a group. Only the group owner and group admin can delete the group. |
| [getJoinedGroupList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_getJoinedGroupList) | Gets the list of groups the current user has joined, excluding audio-video groups. |
| [getGroupsInfo](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_getGroupsInfo_System_String___) | Pulls the profiles of groups. |
| [setGroupInfo](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_setGroupInfo_System_String_System_String_System_String_System_String_System_String_System_String_System_Boolean_com_tencent_imsdk_unity_GroupAddOptType_) | Modifies the profile of a group. |
| [getGroupMemberList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_getGroupMemberList_System_String_com_tencent_imsdk_unity_GroupMemberFilterType_System_Int32_) | Gets the group member list. |
| [getGroupMembersInfo](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_getGroupMembersInfo_System_String_System_String___) | Gets the profiles of specified group members. |
| [setGroupMemberInfo](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_setGroupMemberInfo_System_String_System_String_System_String_) | Modifies the profile of a specified group member. |
| [muteGroupMember](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_muteGroupMember_System_String_System_String_System_Int32_) | Mutes a group member. |
| [kickGroupMember](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_kickGroupMember_System_String_System_String___System_String_) | Removes a member from a group. |
| [setGroupMemberRole](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_setGroupMemberRole_System_String_System_String_com_tencent_imsdk_unity_GroupMemberRoleType_) | Sets the role for a group member. |
| [transferGroupOwner](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_transferGroupOwner_System_String_System_String_) | Changes the group owner. |
| [inviteUserToGroup](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_inviteUserToGroup_System_String_System_String___) | Invites users to a group. |
| [getGroupApplicationList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_getGroupApplicationList) | Gets the list of requests to join a group. |
| [acceptGroupApplication](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_acceptGroupApplication_System_String_System_String_System_String_) | Accepts a request to join a group. |
| [refuseGroupApplication](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_refuseGroupApplication_System_String_System_String_System_String_) | Rejects a request to join a group. |
| [setGroupApplicationRead](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMGroupManager.html#com_tencent_imsdk_unity_V2TIMGroupManager_setGroupApplicationRead) | Marks the request list as read. |

## Conversation List APIs

The conversation list is the list a user sees on the first screen after logging in to WeChat or QQ. It includes elements such as conversation node, conversation name, group name, last message, and unread count.

| API | Description |
|---------|---------|
| [setConversationListener](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_setConversationListener) | Sets a conversation listener. |
| [getConversationList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMConversationManager.html#com_tencent_imsdk_unity_V2TIMConversationManager_getConversationList_System_Int32_System_Int32_) | Gets the conversation list. |
| [deleteConversation](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMConversationManager.html#com_tencent_imsdk_unity_V2TIMConversationManager_deleteConversation_System_String_) | Deletes a conversation. |
| [setConversationDraft](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMConversationManager.html#com_tencent_imsdk_unity_V2TIMConversationManager_setConversationDraft_System_String_System_String_) | Sets a draft for a conversation. |

## User Profile APIs

APIs for querying user profiles, modifying one's own user profile, and blocking messages from a specified user (or adding a specified user to the blocklist).

| API | Description |
|---------|---------|
| [getUsersInfo](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_getUsersInfo_System_String___) | Gets user profiles. |
| [setSelfInfo](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_setSelfInfo_System_String_System_String_System_String_com_tencent_imsdk_unity_Gender_com_tencent_imsdk_unity_FriendAllowType_Dictionary_System_String_System_String__) | Modifies one's own user profile. |
| [addToBlackList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_addToBlackList_System_String___) | Blocks the messages from a user, which means adding the user to the blocklist. |
| [deleteFromBlackList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_deleteFromBlackList_System_String___) | Unblocks the messages from a user, which means removing the user from the blocklist. |
| [getBlackList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_getBlackList) | Gets the blocklist. |
[setOfflinePushConfig](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_offline_push_manager/V2TIMOfflinePushManager/setOfflinePushConfig.html) | Sets the offline push configuration. |

## Friend Management APIs

By default, Tencent Cloud IM does not check your relationship with a user when receiving and sending messages. You can enable the "Check Relationship for One-to-One Messages" on **Feature Configuration** > **Login and Message** > **Relationship Check** in the [IM console](https://console.cloud.tencent.com/im) and use the following APIs to delete/add friends and manage your friend list.

| API | Description |
|---------|---------|
| [setFriendListener](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMManager.html#com_tencent_imsdk_unity_V2TIMManager_setFriendListener) | Sets a relationship chain listener to receive friend list and blocklist change events. |
| [getFriendsList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_getFriendList) | Gets the friend list. |
| [getFriendsInfo](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_getFriendsInfo_System_String___) | Gets the profiles of specified friends. |
| [setFriendInfo](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_setFriendInfo_System_String_System_String_Dictionary_System_String_System_String__) | Sets the profile of a specified friend. |
| [addFriend](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_addFriend_System_String_com_tencent_imsdk_unity_FriendType_System_String_System_String_System_String_) | Adds a friend. |
| [deleteFromFriendList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_deleteFromFriendList_System_String___com_tencent_imsdk_unity_FriendType_) | Deletes a friend. |
| [checkFriend](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_checkFriend_System_String_) | Checks your relationship with a specified user. |
| [getFriendApplicationList](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_getFriendApplicationList) | Gets the list of friend requests. |
| [acceptFriendApplication](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_acceptFriendApplication_System_String_com_tencent_imsdk_unity_FriendAcceptType_) | Accepts a friend request. |
| [refuseFriendApplication](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_refuseFriendApplication_System_String_) | Rejects a friend request. |
| [deleteFriendApplication](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_deleteFriendApplication_System_String_) | Deletes a friend request. |
| [setFriendApplicationRead](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_setFriendApplicationRead) | Sets a friend request as read. |
| [createFriendGroup](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_createFriendGroup_System_String_System_String___) | Creates a friend list. |
| [getFriendGroups](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_getFriendGroups_System_String___) | Gets the information of friend lists. |
| [deleteFriendGroup](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_deleteFriendGroup_System_String___) | Deletes friend lists. |
| [renameFriendGroup](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_renameFriendGroup_System_String_System_String_) | Modifies the name of a friend list. |
| [addFriendsToFriendGroup](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_addFriendsToFriendGroup_System_String_System_String___) | Adds friends to a friend list. |
| [deleteFriendsFromFriendGroup](https://testcomm.qq.com/im/apidoc/api/com.tencent.imsdk.unity.V2TIMFriendshipManager.html#com_tencent_imsdk_unity_V2TIMFriendshipManager_deleteFriendsFromFriendGroup_System_String_System_String___) | Deletes friends from a friend list. |
