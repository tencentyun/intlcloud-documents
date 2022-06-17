>? IM provides Flutter SDK API call examples. You can visit [GitHub](https://github.com/tencentyun/imApiFlutterExample) to obtain the source code.

## Initialization and Login APIs
To use the Tencent Cloud IM service, you need to initialize the SDK and log in.

| API      | Description                         |
|---------|---------|
| [initSDK](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/initSDK.html) | Initializes the SDK. |
| [unInitSDK](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/unInitSDK.html) | Uninitializes the SDK. |
| [login](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/login.html) | Logs in. |
| [logout](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/logout.html) | Logs out. |
| [getLoginUser](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/getLoginUser.html) | Gets the UserID of the current login user. |
| [getLoginStatus](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/getLoginStatus.html) | Gets the login status. |
| [getServerTime](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/getServerTime.html) | Gets the current server time (not supported on web). |
| [getVersion](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/getVersion.html) | Gets the version number. |

## Simple Message Sending and Receiving APIs (Disused After v3.6.0)
>!These simple message sending and receiving APIs will be disused after v3.6.0. If you are still using them, replace them as soon as possible.

Use the following APIs for the sending and receiving of text and signaling (custom buffer) messages.

| API      | Description                         |
|---------|---------|
| [addSimpleMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/addSimpleMsgListener.html) | Sets an event listener for simple messages (text messages and custom messages). Do not confuse this API with the [addAdvancedMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/addAdvancedMsgListener.html) API. |
| [removeSimpleMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/removeSimpleMsgListener.html) | Removes the event listener for simple messages (text messages and custom messages). |
| [sendC2CTextMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/sendC2CTextMessage.html) | Sends a one-to-one (C2C) text message. |
| [sendC2CCustomMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/sendC2CCustomMessage.html) | Sends a one-to-one custom (signaling) message. |
| [sendGroupTextMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/sendGroupTextMessage.html) | Sends a group text message. |
| [sendGroupCustomMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/sendGroupCustomMessage.html) | Sends a group custom (signaling) message. |


## Signaling APIs
| API      | Description                         |
|---------|---------|
| [addSignalingListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/addSignalingListener.html) | Adds a signaling listener. |
| [removeSignalingListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/removeSignalingListener.html) | Removes a signaling listener. |
| [invite](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/invite.html) | Invites a user. |
| [inviteInGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/inviteInGroup.html) | Invites certain users in the group. |
| [cancel](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/cancel.html) | The inviter cancels the invitation. |
| [accept](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/accept.html) | The invitee accepts the invitation. |
| [reject](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/reject.html) | The invitee rejects the invitation. |
| [getSignalingInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/getSignalingInfo.html) | Gets signaling information. |

## Message Creation APIs

After a message is created, an `id` field will be returned. You can pass in the `id` field and related information to the message sending API (`sendMessage`) to send the message.

| API      | Description                         |
|---------|---------|
| [createTextMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createTextMessage.html) | Creates a text message. |
| [createCustomMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createCustomMessage.html) | Creates a custom message. |
| [createImageMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createImageMessage.html) | Creates an image message. |
| [createSoundMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createSoundMessage.html) | Creates an audio message. |
| [createVideoMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createVideoMessage.html) | Creates a video message. |
| [createTextAtMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createTextAtMessage.html) | Creates an @ text message. |
| [createFileMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createFileMessage.html) | Creates a file message. |
| [createLocationMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createLocationMessage.html) | Creates a location message. |
| [createFaceMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createFaceMessage.html) | Creates an emoji message. |
| [createMergerMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createMergerMessage.html) | Creates a combined message. |

## Message Sending and Receiving APIs
If you need to send or receive rich media messages (such as image, video, and file messages) and use advanced features such as recalling messages, marking messages as read, and querying message history, we recommend the following advanced message APIs. (The original APIs for simple message sending and receiving used by v3.6.0 and earlier versions have been disused. Please use new APIs to create and send messages.)

| API      | Description                         |
|---------|---------|
| [addAdvancedMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/addAdvancedMsgListener.html) | Sets an event listener for advanced messages. Do not confuse this API with the [addSimpleMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/addSimpleMsgListener.html) API. |
| [removeAdvancedMsgListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/removeAdvancedMsgListener.html) | Removes the event listener for advanced messages. |
| [getC2CHistoryMessageList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getC2CHistoryMessageList.html) | Gets the one-to-one message history. |
| [getHistoryMessageList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getHistoryMessageList.html) | Gets the message history (advanced API). |
| [getHistoryMessageListWithoutFormat](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getHistoryMessageListWithoutFormat.html) | Gets the message history (advanced API) (without processing the data returned by native SDKs). |
| [getGroupHistoryMessageList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupHistoryMessageList.html) | Gets the group message history. |
| [markC2CMessageAsRead](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markC2CMessageAsRead.html) | Marks a one-to-one message as read. |
| [markGroupMessageAsRead](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markGroupMessageAsRead.html) | Marks a group message as read. |
| [markAllMessageAsRead](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markAllMessageAsRead.html) | Marks all messages as read. |
| [deleteMessageFromLocalStorage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/deleteMessageFromLocalStorage.html) | Deletes a message from the local storage. |
| [deleteMessages](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/deleteMessages.html) | Deletes local and roaming messages. |
| [insertGroupMessageToLocalStorage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/insertGroupMessageToLocalStorage.html) | Adds a message to the group message list. |
| [insertC2CMessageToLocalStorage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/insertC2CMessageToLocalStorage.html) | Inserts a message in a one-to-one chat. |
| [clearC2CHistoryMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/clearC2CHistoryMessage.html) | Clears the chat history with a user from local storage and the cloud (without deleting the conversation). |
| [clearGroupHistoryMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/clearGroupHistoryMessage.html) | Clears the chat history of a group from local storage and the cloud. |
| [downloadMergerMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/downloadMergerMessage.html) | Gets the sub messages of a combined message. |
| [reSendMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/reSendMessage.html) | Resends a message. |
| [setC2CReceiveMessageOpt](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setC2CReceiveMessageOpt.html) | Sets the one-to-one message receiving option for a user (batch setting supported). |
| [getC2CReceiveMessageOpt](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getC2CReceiveMessageOpt.html) | Queries the one-to-one message receiving option of a user. |
| [setGroupReceiveMessageOpt](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setGroupReceiveMessageOpt.html) | Modifies the group message receiving option. |
| [setLocalCustomData](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setLocalCustomData.html) | Sets custom message data (saved locally, will not be sent to the peer end, and will become invalid after the app is uninstalled and reinstalled). |
| [setLocalCustomInt](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setLocalCustomInt.html) | Sets custom message data and marks whether a voice or video message is played (such a message will be saved locally, not be sent to the peer end, and become invalid after the app is uninstalled and reinstalled). |
| [revokeMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/revokeMessage.html) | Recalls a message. By default, you can recall only messages that are sent within two minutes. You can customize the time limit for message recall via the console (**Feature Configuration** > **Login and Message** > **Message Recall Settings**). |
| [sendMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) | Sends a message. |
| [sendReplyMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendReplyMessage.html) | Sends a reply message. |
| [searchLocalMessages](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/searchLocalMessages.html) | Searches for local messages. |
| [findMessages](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/findMessages.html) | Queries local messages in a conversation by `messageID`. |
|[sendMessageReadReceptes](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessageReadReceipts.html)| Sends group message read receipts. |
|[getMessageReadReceptes](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReadReceipts.html) | Gets read receipts for messages sent by yourself. |
|[getgroupMessageReadMemeberList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupMessageReadMemberList.html)| Gets the list of members who have (or have not) read a message sent by yourself. |
| [~~sendCustomMessage~~](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendCustomMessage.html) | Sends a custom message (disused). |
| [~~sendImageMessage~~](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendImageMessage.html) | Sends an image message (disused). |
| [~~sendSoundMessage~~](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendSoundMessage.html) | Sends a audio message (disused). |
|  [~~sendVideoMessage~~](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendVideoMessage.html) | Sends a video message (disused). |
| [~~sendFileMessage~~](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendFileMessage.html) | Sends a file message (disused). |
| [~~sendLocationMessage~~](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendLocationMessage.html) | Sends a location message (disused). |


## Group APIs
Tencent Cloud IM SDK supports the following predefined group types, each of which pertains to different application scenarios:
- Work group (Work): Users can join a work group only after being invited by members of the group. 
- Public group (Public): Users can join a public group through requests, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): When used together with [TRTC](https://Intl.cloud.tencent.com/product/trtc), a meeting group can enable scenarios such as video conferencing and online education. Users can join and leave a meeting group freely and view the messages sent before they join the group.
- Community (Community): A community allows users to join and leave freely and is ideal for ultra-large community group chat scenarios, such as knowledge sharing and game communication.
- Audio-video group (AVChatRoom): An audio-video group allows users to join and leave freely and is suitable for scenarios such as live streaming and chat rooms with on-screen comments. There is no limit on the number of group members.

| API      | Description                         |
|---------|---------|
| [setGroupListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/setGroupListener.html) | Sets an event listener for groups. |
| [createGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/createGroup.html) | Creates a group (simple API). |
| [createGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/createGroup.html) | Creates a group (Advanced API). You can set the group information and the initial group members during group creation. |
| [joinGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/joinGroup.html) | Joins a group. |
| [quitGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/quitGroup.html) | Quits a group. |
| [dismissGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/dismissGroup.html) | Disbands a group. Only the group owner and group admin can disband a group. |
| [getJoinedGroupList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getJoinedGroupList.html) | Gets the list of groups the current user has joined, excluding audio-video groups. |
| [getGroupsInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupsInfo.html) | Pulls the profile of a group. |
| [setGroupInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupInfo.html) | Modifies the profile of a group. |
| [initGroupAttributes](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/initGroupAttributes.html) | Initializes group attributes. This will clear the existing group attribute list. |
| [setGroupAttributes](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupAttributes.html) | Sets group attributes. If the group attributes already exist, their values are updated. Otherwise, the group attributes are added. |
| [deleteGroupAttributes](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/deleteGroupAttributes.html) | Deletes specified group attributes. Passing in `null` for `keys` means clearing all group attributes. |
| [getGroupAttributes](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupAttributes.html) | Gets specified group attributes. Passing in `null` for `keys` means getting all group attributes. |
| [searchGroups](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/searchGroups.html) | Searches for the group list. |
| [searchGroupByID](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/searchGroupByID.html) | Searches for a group by `groupID`. |
| [getGroupOnlineMemberCount](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupOnlineMemberCount.html) | Gets the number of online users in an audio-video group. |
| [getGroupMemberList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupMemberList.html) | Gets the group member list. |
| [getGroupMembersInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupMembersInfo.html) | Gets the profile of a group member. |
| [setGroupMemberInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupMemberInfo.html) | Modifies the profile of a group member. |
| [searchGroupMembers](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/searchGroupMembers.html) | Searches for a group member. |
| [muteGroupMember](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/muteGroupMember.html) | Mutes a group member. |
| [kickGroupMember](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/kickGroupMember.html) | Removes a member from a group. |
| [setGroupMemberRole](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupMemberRole.html) | Sets the role for a group member. |
| [transferGroupOwner](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/transferGroupOwner.html) | Changes the group owner. |
| [inviteUserToGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/inviteUserToGroup.html) | Invites users to a group. |
| [getGroupApplicationList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupApplicationList.html) | Gets the list of requests to join a group. |
| [acceptGroupApplication](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/acceptGroupApplication.html) | Accepts a request to join a group. |
| [refuseGroupApplication](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/refuseGroupApplication.html) | Rejects a request to join a group. |
| [setGroupApplicationRead](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupApplicationRead.html) | Marks the request list as read. |

## Conversation List APIs
The conversation list is the list a user sees on the first screen after logging in to WeChat or QQ. It includes elements such as conversation node, conversation name, group name, last message, and unread message count.

| API      | Description                         |
|---------|---------|
| [setConversationListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/setConversationListener.html) | Sets a conversation listener. |
| [getConversationList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getConversationList.html) | Gets the conversation list. |
| [getConversationListWithoutFormat](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getConversationListWithoutFormat.html) | Gets the conversation list (unformatted). |
| [getConversationListByConversaionIds](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getConversationListByConversaionIds.html) | Gets the list of specified conversations by conversation IDs. |
| [pinConversation](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/pinConversation.html) | Pins a conversation to the top. |
| [getTotalUnreadMessageCount](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getTotalUnreadMessageCount.html) | Gets the total unread message count of a conversation. |
| [getConversation](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getConversation.html) | Gets a specified conversation. |
| [deleteConversation](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/deleteConversation.html) | Deletes a conversation. |
| [setConversationDraft](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/setConversationDraft.html) | Sets a draft for a conversation. |

## User Profile APIs
You can use the following APIs to query user profiles, modify your profile, and block messages from a specified user (that is, adding a specified user to the blocklist).

| API      | Description                         |
|---------|---------|
| [getUsersInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/getUsersInfo.html) | Gets user profiles. |
| [setSelfInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager/setSelfInfo.html) | Modifies one’s own profile. |
| [addToBlackList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addToBlackList.html) | Blocks the messages from a user, which means adding the user to the blocklist. |
| [deleteFromBlackList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFromBlackList.html) | Unblocks the messages from a user, which means removing the user from the blocklist. |
| [getBlackList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getBlackList.html) | Gets the blocklist. |

## Offline Push APIs
We recommend you use the offline push service if you want your app to receive IM messages in real time when it runs in the background. As there is no unified push service in the Chinese mainland, you need to [configure Android offline push](https://intl.cloud.tencent.com/document/product/1047/39156) for devices of different vendors separately.

| API      | Description                         |
|---------|---------|
| [setOfflinePushConfig](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_offline_push_manager/V2TIMOfflinePushManager/setOfflinePushConfig.html) | Sets the offline push configuration. |

## Friend Management APIs
By default, Tencent Cloud IM does not check your relationship with a user when receiving and sending messages. You can enable **Check Relationship for One-to-One Messages** on **Feature Configuration** > **Login and Message** > **Relationship Check** in the [IM console](https://console.cloud.tencent.com/im) and use the following APIs to delete/add friends and manage your friends.

| API      | Description                         |
|---------|---------|
| [setFriendListener](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendListener.html) | Sets a relationship chain listener to receive friend and blocklist change events. |
| [getFriendList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendList.html) | Gets all friends. |
| [getFriendsInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendsInfo.html) | Gets the profiles of specified friends. |
| [setFriendInfo](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendInfo.html) | Sets the profile of a specified friend. |
| [addFriend](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriend.html) | Adds a friend. |
| [deleteFromFriendList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFromFriendList.html) | Deletes a friend. |
| [checkFriend](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/checkFriend.html) | Checks your relationship with a specified user. |
| [getFriendApplicationList](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendApplicationList.html) | Gets the list of friend requests. |
| [acceptFriendApplication](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/acceptFriendApplication.html) | Accepts a friend request. |
| [refuseFriendApplication](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/refuseFriendApplication.html) | Rejects a friend request. |
| [deleteFriendApplication](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendApplication.html) | Deletes a friend request. |
| [setFriendApplicationRead](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendApplicationRead.html) | Sets a friend request as read. |
| [createFriendGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/createFriendGroup.html) | Creates a friend list. |
| [getFriendGroups](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendGroups.html) | Gets the information of friend lists. |
| [deleteFriendGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendGroup.html) | Deletes a friend list. |
| [renameFriendGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/renameFriendGroup.html) | Modifies the name of a friend list. |
| [addFriendsToFriendGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriendsToFriendGroup.html) | Adds friends to a friend list. |
| [deleteFriendsFromFriendGroup](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendsFromFriendGroup.html) | Deletes friends from a friend list. |
| [searchFriends](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/searchFriends.html) | Searches for friends. |
