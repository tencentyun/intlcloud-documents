<dx-alert infotype="notice" title="Note">
Chat provides Flutter SDK API call examples. You can visit [GitHub](https://github.com/TencentCloud/chat-sdk-flutter/tree/main/example) to obtain the source code.
</dx-alert infotype="notice" title="Note">

## Initialization and Login APIs

To use the Tencent Cloud Chat service, you need to initialize the SDK and log in.

| API                                                          | Description                                          |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| [initSDK](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/initSDK.html) | Initializes the SDK.                                 |
| [unInitSDK](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/unInitSDK.html) | Uninitializes the SDK.                               |
| [login](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/login.html) | Logs in.                                             |
| [logout](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/logout.html) | Logs out.                                            |
| [getLoginUser](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getLoginUser.html) | Gets the UserID of the current login user.           |
| [getLoginStatus](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getLoginStatus.html) | Gets the login status.                               |
| [getServerTime](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getServerTime.html) | Gets the current server time (not supported on web). |
| [getVersion](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getVersion.html) | Gets the version number.                             |
| [getConversationManager](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getConversationManager.html) | Conversation feature entry.                          |
| [getFriendshipManager](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getFriendshipManager.html) | Relationship chain feature entry.                    |
| [getGroupManager](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getGroupManager.html) | Advanced group feature entry.                        |
| [getMessageManager](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getMessageManager.html) | Advanced message feature entry.                      |
| [getOfflinePushManager](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getOfflinePushManager.html) | Gets the version number.                             |
| [getSignalingManager](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getSignalingManager.html) | Signaling entry.                                     |

## Signaling APIs

| API                                                          | Description                         |
| ------------------------------------------------------------ | ----------------------------------- |
| [addSignalingListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMSignalingManager/addSignalingListener.html) | Adds a signaling listener.          |
| [removeSignalingListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMSignalingManager/removeSignalingListener.html) | Removes a signaling listener.       |
| [invite](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMSignalingManager/invite.html) | Invites a user.                     |
| [inviteInGroup](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMSignalingManager/inviteInGroup.html) | Invites certain users in the group. |
| [cancel](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMSignalingManager/cancel.html) | The inviter cancels the invitation. |
| [accept](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMSignalingManager/accept.html) | The invitee accepts the invitation. |
| [reject](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMSignalingManager/reject.html) | The invitee rejects the invitation. |
| [getSignalingInfo](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMSignalingManager/getSignalingInfo.html) | Gets signaling information.         |
| [addInvitedSignaling](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMSignalingManager/addInvitedSignaling.html) | Creates a signaling request.        |

## Message Creation APIs

After a message is created, an `id` field will be returned. You can pass in the `id` field and related information to the message sending API (`sendMessage`) to send the message.

| API                                                          | Description                       |
| ------------------------------------------------------------ | --------------------------------- |
| [createTextMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createTextMessage.html) | Creates a text message.           |
| [createCustomMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createCustomMessage.html) | Creates a custom message.         |
| [createImageMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createImageMessage.html) | Creates an image message.         |
| [createSoundMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createSoundMessage.html) | Creates an audio message.         |
| [createVideoMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createVideoMessage.html) | Creates a video message.          |
| [createTextAtMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createTextAtMessage.html) | Creates an @ text message.        |
| [createFileMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createFileMessage.html) | Creates a file message.           |
| [createLocationMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createLocationMessage.html) | Creates a location message.       |
| [createFaceMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createFaceMessage.html) | Creates an emoji message.         |
| [createMergerMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createMergerMessage.html) | Creates a combined message.       |
| [createForwardMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createForwardMessage.html) | Creates a forward message.        |
| [createTargetedGroupMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createTargetedGroupMessage.html) | Creates a targeted group message. |
| [appendMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/appendMessage.html) | Adds a multi-element message.     |

## Message Sending and Receiving APIs

If you need to send or receive rich media messages (such as image, video, and file messages) and use advanced features such as recalling messages, marking messages as read, and querying message history, we recommend the following advanced message APIs. (The original APIs for simple message sending and receiving used by v3.6.0 and earlier versions have been disused. Please use new APIs to create and send messages.)

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [addAdvancedMsgListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/addAdvancedMsgListener.html) | Sets an event listener for advanced messages.                |
| [removeAdvancedMsgListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/removeAdvancedMsgListener.html) | Removes the event listener for advanced messages.            |
| [getC2CHistoryMessageList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getC2CHistoryMessageList.html) | Gets historical one-to-one (C2C) messages.                   |
| [getHistoryMessageList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getHistoryMessageList.html) | Gets historical messages (advanced API).                     |
| [getGroupHistoryMessageList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getGroupHistoryMessageList.html) | Gets historical group messages.                              |
| [markC2CMessageAsRead](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/markC2CMessageAsRead.html) | Marks one-to-one (C2C) messages as read.                     |
| [markGroupMessageAsRead](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/markGroupMessageAsRead.html) | Marks group messages as read.                                |
| [markAllMessageAsRead](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/markAllMessageAsRead.html) | Marks all messages as read.                                  |
| [deleteMessageFromLocalStorage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/deleteMessageFromLocalStorage.html) | Deletes a message from the local storage.                    |
| [deleteMessages](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/deleteMessages.html) | Deletes local and roaming messages.                          |
| [insertGroupMessageToLocalStorage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/insertGroupMessageToLocalStorage.html) | Adds a message to the message list of a group chat.          |
| [insertC2CMessageToLocalStorage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/insertC2CMessageToLocalStorage.html) | Adds a message to the message list of a one-to-one chat.     |
| [clearC2CHistoryMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/clearC2CHistoryMessage.html) | Clears the chat history with a user from local storage and the cloud (without deleting the conversation). |
| [clearGroupHistoryMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/clearGroupHistoryMessage.html) | Clears the chat history of a group from local storage and the cloud (without deleting the conversation). |
| [downloadMergerMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMergerMessage.html) | Gets the sub messages of a combined message.                 |
| [reSendMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/reSendMessage.html) | Resends a message.                                           |
| [setC2CReceiveMessageOpt](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/setC2CReceiveMessageOpt.html) | Sets the one-to-one message receiving option for a user (batch setting supported). |
| [getC2CReceiveMessageOpt](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getC2CReceiveMessageOpt.html) | Queries the one-to-one message receiving option of a user.   |
| [setGroupReceiveMessageOpt](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/setGroupReceiveMessageOpt.html) | Modifies the group message receiving option.                 |
| [setLocalCustomData](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/setLocalCustomData.html) | Sets custom message data (saved locally, will not be sent to the peer end, and will become invalid after the app is uninstalled and reinstalled). |
| [setLocalCustomInt](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/setLocalCustomInt.html) | Sets custom message data and marks whether a voice or video message is played (such a message will be saved locally, not be sent to the peer end, and become invalid after the app is uninstalled and reinstalled). |
| [revokeMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/revokeMessage.html) | Recalls a message. By default, you can recall only messages that are sent within two minutes. You can customize the time limit for message recall via the console (**Feature Configuration** > **Login and Message** > **Message Recall Settings**). |
| [modifyMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/modifyMessage.html) | Modifies a message.                                          |
| [sendMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/sendMessage.html) | Sends a message.                                             |
| [sendReplyMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/sendReplyMessage.html) | Sends a reply message.                                       |
| [searchLocalMessages](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/searchLocalMessages.html) | Searches for local messages.                                 |
| [sendMessageReadReceipts](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/sendMessageReadReceipts.html) | Sends group message read receipts.                           |
| [getMessageReadReceipts](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageReadReceipts.html) | Gets read receipts for messages sent by yourself.            |
| [getGroupMessageReadMemberList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getGroupMessageReadMemberList.html) | Gets the list of members who have (or have not) read a message sent by yourself. |

## Group APIs

Tencent Cloud Chat SDK supports five preset group types, each of which pertains to different scenarios.

- Work group (Work): Users can join a work group only after being invited by members of the group. This group type is the same as private group (Private) in earlier versions.
- Public group (Public): Users can join the group through requests, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): used together with [TRTC](https://www.tencentcloud.com/products/trtc) to enable scenarios such as video conferencing and online education. Users can join and leave the group freely and view the message history before they join. Same as chat room (ChatRoom) in earlier versions.
- Community (Community): A community allows users to join and leave freely and is ideal for ultra-large community group chat scenarios, such as knowledge sharing and game communication.
- Audio-video group (AVChatRoom): An audio-video group allows users to join and leave freely and is suitable for scenarios such as live streaming and chat rooms with on-screen comments. There is no limit on the number of group members.

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [addGroupListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/addGroupListener.html) | Adds an event listener for groups.                           |
| [setGroupListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/setGroupListener.html) | Sets an event listener for groups.                           |
| [removeGroupListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/removeGroupListener.html) | Removes an event listener for groups.                        |
| [createGroup](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/createGroup.html) | Creates a group (advanced). The group information and the initial group members can be set during group creation. |
| [joinGroup](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/joinGroup.html) | Joins a group.                                               |
| [quitGroup](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/quitGroup.html) | Leaves a group.                                              |
| [dismissGroup](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/dismissGroup.html) | Deletes a group. Only the group owner and group admin can delete the group. |
| [getJoinedGroupList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getJoinedGroupList.html) | Gets the list of groups the current user has joined, excluding audio-video groups. |
| [getGroupsInfo](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupsInfo.html) | Gets the profiles of groups.                                 |
| [setGroupInfo](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html) | Modifies the profile of a group.                             |
| [initGroupAttributes](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/initGroupAttributes.html ) | Initializes group attributes. This will clear the existing group attribute list. |
| [setGroupAttributes](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/setGroupAttributes.html) | Sets group attributes. If the group attributes already exist, their values are updated. Otherwise, the group attributes are added. |
| [deleteGroupAttributes](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/deleteGroupAttributes.html) | Deletes specified group attributes. Passing in `null` for `keys` means clearing all group attributes. |
| [getGroupAttributes](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupAttributes.html) | Gets specified group attributes. Passing in `null` for `keys` means getting all group attributes. |
| [searchGroups](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/searchGroups.html) | Searches for groups.                                         |
| [getGroupOnlineMemberCount](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupOnlineMemberCount.html) | Gets the number of online users in a group. (This API is currently supported only by audio-video groups.) |
| [getGroupMemberList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupMemberList.html) | Gets the group member list.                                  |
| [getGroupMembersInfo](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupMembersInfo.html) | Gets the profiles of specified group members.                |
| [setGroupMemberInfo](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/setGroupMemberInfo.html) | Modifies the profile of a specified group member.            |
| [searchGroupMembers](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/searchGroupMembers.html) | Searches for group members.                                  |
| [muteGroupMember](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/muteGroupMember.html) | Mutes a group member.                                        |
| [kickGroupMember](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/kickGroupMember.html) | Removes members from a group.                                |
| [setGroupMemberRole](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/setGroupMemberRole.html) | Sets a role for a group member.                              |
| [transferGroupOwner](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/transferGroupOwner.html) | Transfers the ownership of a group.                          |
| [inviteUserToGroup](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/inviteUserToGroup.html) | Invites users to a group.                                    |
| [getGroupApplicationList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupApplicationList.html) | Gets the list of requests to join a group.                   |
| [acceptGroupApplication](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/acceptGroupApplication.html) | Accepts a request to join a group.                           |
| [refuseGroupApplication](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/refuseGroupApplication.html) | Rejects a request to join a group.                           |
| [setGroupApplicationRead](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/setGroupApplicationRead.html) | Marks the request list as read.                              |
| [getJoinedCommunityList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getJoinedCommunityList.html) | Gets the list of community groups the current user has joined. |
| [createTopicInCommunity](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/createTopicInCommunity.html) | Creates a topic.                                             |
| [deleteTopicFromCommunity](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/deleteTopicFromCommunity.html) | Deletes a topic.                                             |
| [setTopicInfo](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/setTopicInfo.html) | Sets topic attributes.                                       |
| [getTopicInfoList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getTopicInfoList.html) | Gets the topics of a group.                                  |

## Conversation List APIs

The conversation list is the list a user sees on the first screen after login. It includes elements such as conversation node, conversation name, group name, last message, and unread count.

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [addConversationListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/addConversationListener.html) | Adds a relationship chain listener.                          |
| [removeConversationListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/removeConversationListener.html) | Removes a relationship chain listener.                       |
| [setConversationListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/setConversationListener.html) | Sets a conversation listener.                                |
| [getConversationList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/getConversationList.html) | Gets the conversation list.                                  |
| [getConversationListByConversaionIds](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/getConversationListByConversaionIds.html) | Gets the list of specified conversations by conversation IDs. |
| [pinConversation](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/pinConversation.html) | Pins a conversation to the top.                              |
| [getTotalUnreadMessageCount](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/getTotalUnreadMessageCount.html) | Gets the total unread message count of a conversation.       |
| [getConversation](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/getConversation.html) | Gets a specified conversation.                               |
| [deleteConversation](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/deleteConversation.html) | Deletes a conversation.                                      |
| [setConversationDraft](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/setConversationDraft.html) | Sets a draft for a conversation.                             |

## User Profile APIs

You can use the following APIs to query user profiles, modify your profile, and block messages from a specified user (that is, adding a specified user to the blocklist).

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getUsersInfo](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getUsersInfo.html) | Gets user profiles.                                          |
| [getUserStatus](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getUserStatus.html) | Gets users' online statuses.                                 |
| [setSelfInfo](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/setSelfInfo.html) | Modifies one's own user profile.                             |
| [setSelfStatus](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/setSelfStatus.html) | Sets the status of the current logged-in user.               |
| [addToBlackList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/addToBlackList.html) | Blocks messages from a user, which means adding the user to the blocklist. |
| [deleteFromBlackList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/deleteFromBlackList.html) | Unblocks messages from a user, which means removing the user from the blocklist. |
| [getBlackList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/getBlackList.html) | Gets the blocklist.                                          |

## Offline Push APIs

We recommend you use the offline push service if you want your app to receive Chat service messages in real time when it runs in the background. As there is no unified push service in the Chinese mainland, you need to [configure Android offline push](https://intl.cloud.tencent.com/document/product/1047/39156) for devices of different vendors separately.

| API                                                          | Description                          |
| ------------------------------------------------------------ | ------------------------------------ |
| [setAPNSListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/setAPNSListener.html) | Sets the APNs offline push listener. |
| [doBackground](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMOfflinePushManager/doBackground.html) | Configures offline push.             |
| [doForeground](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMOfflinePushManager/doForeground.html) | Configures offline push.             |
| [setOfflinePushConfig](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMOfflinePushManager/setOfflinePushConfig.html) | Configures offline push.             |

## Friend Management APIs

By default, Tencent Cloud Chat does not check your relationship with a user when receiving and sending messages. You can enable **Check Relationship for One-to-One Messages** on **Feature Configuration** > **Login and Message** > **Relationship Check** in the [Chat console](https://console.cloud.tencent.com/im) and use the following APIs to delete/add friends and manage your friends.

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setFriendListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/setFriendListener.html) | Sets a relationship chain listener to receive friend and blocklist change events. |
| [addFriendListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/addFriendListener.html) | Adds a relationship chain listener.                          |
| [removeFriendListener](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/removeFriendListener.html) | Removes a relationship chain listener.                       |
| [getFriendList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/getFriendList.html) | Gets the contacts.                                           |
| [getFriendsInfo](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/getFriendsInfo.html) | Gets the profiles of specified friends.                      |
| [setFriendInfo](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/setFriendInfo.html) | Sets the profile of a specified friend.                      |
| [addFriend](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/addFriend.html) | Adds a friend.                                               |
| [deleteFromFriendList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/deleteFromFriendList.html) | Deletes friends.                                             |
| [checkFriend](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/checkFriend.html) | Checks your relationship with a specified user.              |
| [getFriendApplicationList](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/getFriendApplicationList.html) | Gets the list of friend requests.                            |
| [acceptFriendApplication](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/acceptFriendApplication.html) | Accepts a friend request.                                    |
| [refuseFriendApplication](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/refuseFriendApplication.html) | Rejects a friend request.                                    |
| [deleteFriendApplication](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/deleteFriendApplication.html) | Deletes a friend request.                                    |
| [setFriendApplicationRead](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/setFriendApplicationRead.html) | Marks a friend request as read.                              |
| [createFriendGroup](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/createFriendGroup.html) | Creates a friend list.                                       |
| [getFriendGroups](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/getFriendGroups.html) | Gets the information of friend lists.                        |
| [deleteFriendGroup](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/deleteFriendGroup.html) | Deletes a friend list.                                       |
| [renameFriendGroup](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/renameFriendGroup.html) | Modifies the name of a friend list.                          |
| [addFriendsToFriendGroup](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/addFriendsToFriendGroup.html) | Adds friends to a friend list.                               |
| [deleteFriendsFromFriendGroup](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/deleteFriendsFromFriendGroup.html) | Deletes friends from a friend list.                          |
| [searchFriends](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/searchFriends.html) | Searches for friends.                                        |
