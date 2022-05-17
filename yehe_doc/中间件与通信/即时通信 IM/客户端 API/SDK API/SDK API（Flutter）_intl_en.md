## Initialization and Login APIs
To use Tencent Cloud IM services, you need to perform initialization and log in.

| API | Description |
|---------|---------|
| [initSDK](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/initSDK.html) | Initializes the SDK. |
| [unInitSDK](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/unInitSDK.html) | Uninitializes the SDK. |
| [login](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/login.html) | Logs in. |
| [logout](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/logout.html) | Logs out. |
| [getLoginStatus](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/getLoginStatus.html) | Gets the login status. |
| [getLoginUser](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/getLoginUser.html) | Gets the UserID of the current login user. |

## Simple Message APIs
Use the following message APIs if you only need to use text and signaling (a piece of custom buffer) messages.

| API | Description |
|---------|---------|
| [addSimpleMsgListener](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/addSimpleMsgListener.html) | Sets an event listener for simple messages (text messages and custom messages). Do not use it and [addAdvancedMsgListener](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/addAdvancedMsgListener.html) at the same time. |
| [removeSimpleMsgListener](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/removeSimpleMsgListener.html) | Removes the event listener for simple messages (text messages and custom messages). |
| [sendC2CTextMessage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/sendC2CTextMessage.html) | Sends a one-to-one (C2C) text message. |
| [sendC2CCustomMessage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/sendC2CCustomMessage.html) | Sends a one-to-one (C2C) custom (signaling) message. |
| [sendGroupTextMessage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/sendGroupTextMessage.html) | Sends a group text message. |
| [sendGroupCustomMessage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/sendGroupCustomMessage.html) | Sends a group custom (signaling) message. |

## Signaling APIs
| API | Description |
|---------|---------|
| [addSignalingListener](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_signaling_manager/V2TIMSignalingManager/addSignalingListener.html) | Adds a signaling listener. |
| [removeSignalingListener](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_signaling_manager/V2TIMSignalingManager/removeSignalingListener.html) | Removes a signaling listener. |
| [invite](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_signaling_manager/V2TIMSignalingManager/invite.html) | Invites a user. |
| [inviteInGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_signaling_manager/V2TIMSignalingManager/inviteInGroup.html) | Invites certain users in the group. |
| [cancel](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_signaling_manager/V2TIMSignalingManager/cancel.html) | The inviter cancels the invitation. |
| [accept](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_signaling_manager/V2TIMSignalingManager/accept.html) | The invitee accepts the invitation. |
| [reject](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_signaling_manager/V2TIMSignalingManager/reject.html) | The invitee rejects the invitation. |

## Advanced Message APIs
If you need to send/receive rich media messages (images, videos, files, etc.) and use advanced features such as recalling messages, marking messages as read, and querying message history, use the following set of advanced message APIs. Do not use simple messages APIs and advanced message APIs at the same time.

| API | Description |
|---------|---------|
| [addAdvancedMsgListener](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/addAdvancedMsgListener.html) | Sets an event listener for advanced messages. Do not use it and [addSimpleMsgListener](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/addSimpleMsgListener.html) at the same time. |
| [removeAdvancedMsgListener](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/removeAdvancedMsgListener.html) | Removes the event listener for advanced messages. |
| [sendCustomMessage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/sendCustomMessage.html) | Sends a custom message. |
| [sendImageMessage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/sendImageMessage.html) | Sends an image message. |
| [sendSoundMessage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/sendSoundMessage.html) | Sends a voice message. |
| [sendVideoMessage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/sendVideoMessage.html) | Sends a video message. |
| [sendFileMessage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/sendFileMessage.html) | Sends a file message. |
| [sendLocationMessage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/sendLocationMessage.html) | Sends a location message. |
| [getC2CHistoryMessageList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getC2CHistoryMessageList.html) | Gets the one-to-one (C2C) message history. |
| [getGroupHistoryMessageList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupHistoryMessageList.html) | Gets the group message history. |
| [markC2CMessageAsRead](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/markC2CMessageAsRead.html) | Marks one-to-one (C2C) messages as read. |
| [markGroupMessageAsRead](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/markGroupMessageAsRead.html) | Marks group messages as read. |
| [deleteMessageFromLocalStorage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/deleteMessageFromLocalStorage.html) | Deletes a message from the local storage. |
| [insertGroupMessageToLocalStorage](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/insertGroupMessageToLocalStorage.html) | Adds a message to the group message list. |

## Group APIs
Tencent Cloud IM SDK supports four preset group types, each of which pertains to different scenarios.
- Work group (Work): similar to a WeChat group. Users can join the group only after being invited by group members. Same as private group (Private) in earlier versions.
- Public group (Public): similar to a QQ group. Users can join the group through requests, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): used together with [TRTC](https://intl.cloud.tencent.com/product/trtc) to enable scenarios such as video conferencing and online education. Users can join and leave the group freely and view the message history before they join. Same as chat room (ChatRoom) in earlier versions.
- Audio-video group (AVChatRoom): suitable for scenarios such as live streaming and chat rooms with on-screen comments. Users can join and leave the group freely. There is no limit on the number of group members.

| API | Description |
|---------|---------|
| [setGroupListener](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/setGroupListener.html) | Sets an event listener for groups. |
| [createGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/createGroup.html) | Creates a group (simple). |
| [createGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/createGroup.html) | Creates a group (advanced). The group information and the initial group members can be set during group creation. |
| [joinGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/joinGroup.html) | Joins a group. |
| [quitGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/quitGroup.html) | Quits a group. |
| [dismissGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/dismissGroup.html) | Deletes a group. Only the group owner and group admin can delete the group. |
| [getJoinedGroupList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/getJoinedGroupList.html) | Gets the list of groups the current user has joined, excluding audio-video groups. |
| [getGroupsInfo](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupsInfo.html) | Pulls the profiles of groups. |
| [setGroupInfo](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupInfo.html) | Modifies the profile of a group. |
| [getGroupMemberList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupMemberList.html) | Gets the group member list. |
| [getGroupMembersInfo](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupMembersInfo.html) | Gets the profiles of specified group members. |
| [setGroupMemberInfo](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupMemberInfo.html) | Modifies the profile of a specified group member. |
| [muteGroupMember](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/muteGroupMember.html) | Mutes a group member. |
| [kickGroupMember](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/kickGroupMember.html) | Removes a member from a group. |
| [setGroupMemberRole](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupMemberRole.html) | Sets the role for a group member. |
| [transferGroupOwner](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/transferGroupOwner.html) | Changes the group owner. |
| [inviteUserToGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/inviteUserToGroup.html) | Invites users to a group. |
| [getGroupApplicationList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupApplicationList.html) | Gets the list of requests to join a group. |
| [acceptGroupApplication](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/acceptGroupApplication.html) | Accepts a request to join a group. |
| [refuseGroupApplication](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/refuseGroupApplication.html) | Rejects a request to join a group. |
| [setGroupApplicationRead](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupApplicationRead.html) | Marks the request list as read. |

## Conversation List APIs
The conversation list is the list a user sees on the first screen after logging in to WeChat or QQ. It includes elements such as conversation node, conversation name, group name, last message, and unread count.

| API | Description |
|---------|---------|
| [setConversationListener](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_conversation_manager/V2TIMConversationManager/setConversationListener.html) | Sets a conversation listener. |
| [getConversationList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_conversation_manager/V2TIMConversationManager/getConversationList.html) | Gets the conversation list. |
| [deleteConversation](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_conversation_manager/V2TIMConversationManager/deleteConversation.html) | Deletes a conversation. |
| [setConversationDraft](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_conversation_manager/V2TIMConversationManager/setConversationDraft.html) | Sets a draft for a conversation. |

## User Profile APIs
APIs for querying user profiles, modifying one's own user profile, and blocking messages from a specified user (or adding a specified user to the blocklist).

| API | Description |
|---------|---------|
| [getUsersInfo](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/getUsersInfo.html) | Gets user profiles. |
| [setSelfInfo](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_manager/V2TIMManager/setSelfInfo.html) | Modifies one's own user profile. |
| [addToBlackList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addToBlackList.html) | Blocks the messages from a user, which means adding the user to the blocklist. |
| [deleteFromBlackList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFromBlackList.html) | Unblocks the messages from a user, which means removing the user from the blocklist. |
| [getBlackList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getBlackList.html) | Gets the blocklist. |

## Offline Push APIs
Use the offline push service if you want your app to receive IM messages in real time when it is in the background. As there is currently no unified push service in the Chinese mainland, to implement Android offline push, the mobile phones of different vendors need to be [specifically adapted](https://intl.cloud.tencent.com/document/product/1047/39156).

| API | Description |
|---------|---------|
| [setOfflinePushConfig](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_offline_push_manager/V2TIMOfflinePushManager/setOfflinePushConfig.html) | Sets the offline push configuration. |

## Friend Management APIs
By default, Tencent Cloud IM does not check your relationship with a user when receiving and sending messages. You can enable the "Check Relationship for One-to-One Messages" on **Feature Configuration** > **Login and Message** > **Relationship Check** in the [IM console](https://console.cloud.tencent.com/im) and use the following APIs to delete/add friends and manage your friend list.

| API | Description |
|---------|---------|
| [setFriendListener](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendListener.html) | Sets a relationship chain listener to receive friend list and blocklist change events. |
| [getFriendList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendList.html) | Gets the friend list. |
| [getFriendsInfo](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendsInfo.html) | Gets the profiles of specified friends. |
| [setFriendInfo](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendInfo.html) | Sets the profile of a specified friend. |
| [addFriend](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriend.html) | Adds a friend. |
| [deleteFromFriendList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFromFriendList.html) | Deletes a friend. |
| [checkFriend](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/checkFriend.html) | Checks your relationship with a specified user. |
| [getFriendApplicationList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendApplicationList.html) | Gets the list of friend requests. |
| [acceptFriendApplication](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/acceptFriendApplication.html) | Accepts a friend request. |
| [refuseFriendApplication](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/refuseFriendApplication.html) | Rejects a friend request. |
| [deleteFriendApplication](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendApplication.html) | Deletes a friend request. |
| [setFriendApplicationRead](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendApplicationRead.html) | Sets a friend request as read. |
| [createFriendGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/createFriendGroup.html) | Creates a friend list. |
| [getFriendGroups](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendGroups.html) | Gets the information of friend lists. |
| [deleteFriendGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendGroup.html) | Deletes friend lists. |
| [renameFriendGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/renameFriendGroup.html) | Modifies the name of a friend list. |
| [addFriendsToFriendGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriendsToFriendGroup.html) | Adds friends to a friend list. |
| [deleteFriendsFromFriendGroup](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendsFromFriendGroup.html) | Deletes friends from a friend list. |

