## Initialization and Login APIs

To use the Tencent Cloud Chat service, you need to initialize the SDK and log in.


| API                                                          | Description                                |
| ------------------------------------------------------------ | ------------------------------------------ |
| [initSDK](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/initSDK.html) | Initializes the SDK.                       |
| [unInitSDK](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/unInitSDK.html) | Uninitializes the SDK.                     |
| [login](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/login.html) | Logs in.                                   |
| [logout](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/logout.html) | Logs out.                                  |
| [getLoginUser](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/getLoginUser.html) | Gets the UserID of the current login user. |
| [getLoginStatus](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/getLoginStatus.html) | Gets the login status.                     |
| [getServerTime](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/getServerTime.html) | Gets the server time.                      |
| [getVersion](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/getVersion.html) | Gets the version number.                   |

## Signaling APIs

| API                                                          | Description                         |
| ------------------------------------------------------------ | ----------------------------------- |
| [accept](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/accept.html) | The invitee accepts the invitation. |
| [addInvitedSignaling](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/addInvitedSignaling.html) | Creates a signaling request.        |
| [addSignalingListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/addSignalingListener.html) | Adds a signaling listener.          |
| [cancel](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/cancel.html) | The inviter cancels the invitation. |
| [getSignalingInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/getSignalingInfo.html) | Gets signaling information.         |
| [invite](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/invite.html) | Invites a user.                     |
| [inviteInGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/inviteInGroup.html) | Invites certain users in the group. |
| [reject](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/reject.html) | The invitee rejects the invitation. |
| [removeSignalingListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/removeSignalingListener.html) | Removes a signaling listener.       |

## Message APIs

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [addAdvancedMsgListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/addAdvancedMsgListener.html) | Adds an event listener for advanced messages.                |
| [appendMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/appendMessage.html) | Appends another message to a message and adds it to the list. |
| [clearC2CHistoryMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/clearC2CHistoryMessage.html) | Clears the chat history with a user from local storage and the cloud (without deleting the conversation). |
| [clearGroupHistoryMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/clearGroupHistoryMessage.html) | Clears the chat history of a group from local storage and the cloud (without deleting the conversation). |
| [createCustomMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createCustomMessage.html) | Creates a custom message.                                    |
| [createFaceMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createFaceMessage.html) | Creates an emoji message.                                    |
| [createFileMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createFileMessage.html) | Creates a file message.                                      |
| [createForwardMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createForwardMessage.html) | Creates a forward message.                                   |
| [createImageMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createImageMessage.html) | Creates an image message.                                    |
| [createLocationMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createLocationMessage.html) | Creates a location message.                                  |
| [createMergerMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createMergerMessage.html) | Creates a combined message.                                  |
| [createSoundMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createSoundMessage.html) | Creates an audio message.                                    |
| [createTargetedGroupMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createTargetedGroupMessage.html) | Creates a targeted group message.                            |
| [createTextAtMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createTextAtMessage.html) | Creates a text message with the @ notification feature (unavailable for audio-video groups). |
| [createTextMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createTextMessage.html) | Creates a text message.                                      |
| [createVideoMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createVideoMessage.html) | Creates a video message.                                     |
| [deleteMessageExtensions](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/deleteMessageExtensions.html) | Deletes message extensions.                                  |
| [deleteMessageFromLocalStorage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/deleteMessageFromLocalStorage.html) | Deletes a message from the local storage.                    |
| [deleteMessages](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/deleteMessages.html) | Deletes local and roaming messages.                          |
| [downloadMergerMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/downloadMergerMessage.html) | Gets the sub messages of a combined message.                 |
| [downloadMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/downloadMessage.html) | Downloads a multimedia message.                              |
| [getC2CHistoryMessageList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getC2CHistoryMessageList.html) | Gets historical one-to-one messages.                         |
| [getC2CReceiveMessageOpt](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getC2CReceiveMessageOpt.html) | Queries the one-to-one message receiving option of a user.   |
| [getGroupHistoryMessageList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getGroupHistoryMessageList.html) | Gets historical group messages.                              |
| [getGroupMessageReadMemberList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getGroupMessageReadMemberList.html) | Gets the list of members who have or have not read the group message. |
| [getHistoryMessageList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getHistoryMessageList.html) | Gets historical messages (advanced API).                     |
| [getMessageExtensions](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageExtensions.html) | Gets message extensions.                                     |
| [getMessageOnlineUrl](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageOnlineUrl.html) | Gets the URL of a multimedia message.                        |
| [getMessageReadReceipts](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageReadReceipts.html) | Gets message read receipts.                                  |
| [insertC2CMessageToLocalStorage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/insertC2CMessageToLocalStorage.html) | Adds a message to the message list of a one-to-one chat.     |
| [insertGroupMessageToLocalStorage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/insertGroupMessageToLocalStorage.html) | Adds a message to the message list of a group chat.          |
| [markAllMessageAsRead](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/markAllMessageAsRead.html) | Marks all messages as read.                                  |
| [markC2CMessageAsRead](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/markC2CMessageAsRead.html) | Marks one-to-one (C2C) messages as read.                     |
| [markGroupMessageAsRead](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/markGroupMessageAsRead.html) | Marks group messages as read.                                |
| [modifyMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/modifyMessage.html) | Modifies a message.                                          |
| [removeAdvancedMsgListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/removeAdvancedMsgListener.html) | Removes the listener for advanced messages.                  |
| [reSendMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/reSendMessage.html) | Resends a message.                                           |
| [revokeMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/revokeMessage.html) | Recalls a message.                                           |
| [searchLocalMessages](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/searchLocalMessages.html) | Searches for local messages.                                 |
| [sendMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/sendMessage.html) | Sends a message.                                             |
| [sendMessageReadReceipts](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/sendMessageReadReceipts.html) | Sends message read receipts.                                 |
| [sendReplyMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/sendReplyMessage.html) | Sends a reply message.                                       |
| [setC2CReceiveMessageOpt](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/setC2CReceiveMessageOpt.html) | Sets the one-to-one message receiving option of a user.      |
| [setGroupReceiveMessageOpt](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/setGroupReceiveMessageOpt.html) | Sets the group message receiving option.                     |
| [setLocalCustomData](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/setLocalCustomData.html) | Sets custom message data.                                    |
| [setLocalCustomInt](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/setLocalCustomInt.html) | Sets custom message data.                                    |
| [setMessageExtensions](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/setMessageExtensions.html) | Gets message extensions.                                     |




## Conversation APIs

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [addConversationListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/addConversationListener.html) | Sets a conversation listener.                                |
| [deleteConversation](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/deleteConversation.html) | Deletes a conversation.                                      |
| [getConversation](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/getConversation.html) | Gets the information of a conversation.                      |
| [getConversationList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/getConversationList.html) | Gets the conversation list.                                  |
| [getConversationListByConversaionIds](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/getConversationListByConversaionIds.html) | Gets the list of specified conversations by conversation IDs. |
| [getTotalUnreadMessageCount](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/getTotalUnreadMessageCount.html) | Gets the total unread message count of a conversation.       |
| [pinConversation](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/pinConversation.html) | Pins a conversation to the top.                              |
| [removeConversationListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/removeConversationListener.html) | Removes a conversation listener.                             |
| [setConversationDraft](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/setConversationDraft.html) | Sets a draft for a conversation.                             |


## Relationship Chain APIs

| API                                                          | Description                                     |
| ------------------------------------------------------------ | ----------------------------------------------- |
| [acceptFriendApplication](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/acceptFriendApplication.html) | Accepts a friend request.                       |
| [addFriend](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/addFriend.html) | Adds a friend.                                  |
| [addFriendListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/addFriendListener.html) | Adds a relationship chain listener.             |
| [addFriendsToFriendGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/addFriendsToFriendGroup.html) | Adds friends to a friend list.                  |
| [addToBlackList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/addToBlackList.html) | Adds a user to the blocklist.                   |
| [checkFriend](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/checkFriend.html) | Checks your relationship with a specified user. |
| [createFriendGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/createFriendGroup.html) | Creates a friend list.                          |
| [deleteFriendApplication](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/deleteFriendApplication.html) | Deletes a friend request.                       |
| [deleteFriendGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/deleteFriendGroup.html) | Deletes a friend list.                          |
| [deleteFriendsFromFriendGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/deleteFriendsFromFriendGroup.html) | Accepts a friend request.                       |
| [deleteFromBlackList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/deleteFromBlackList.html) | Removes a user from the blocklist.              |
| [deleteFromFriendList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/deleteFromFriendList.html) | Deletes friends.                                |
| [getBlackList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/getBlackList.html) | Gets the blocklist.                             |
| [getFriendApplicationList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/getFriendApplicationList.html) | Gets the list of friend requests.               |
| [getFriendGroups](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/getFriendGroups.html) | Gets the information of friend lists.           |
| [getFriendList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/getFriendList.html) | Gets the contacts.                              |
| [getFriendsInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/getFriendsInfo.html) | Gets the profiles of specified friends.         |
| [refuseFriendApplication](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/refuseFriendApplication.html) | Rejects a friend request.                       |
| [removeFriendListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/removeFriendListener.html) | Removes a relationship chain listener.          |
| [renameFriendGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/renameFriendGroup.html) | Modifies the name of a friend list.             |
| [searchFriends](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/searchFriends.html) | Searches for friends.                           |
| [setFriendApplicationRead](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/setFriendApplicationRead.html) | Marks a friend request as read.                 |
| [setFriendInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/setFriendInfo.html) | Sets the profile of a specified friend.         |

## Group APIs

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [addGroupListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/addGroupListener.html) | Adds an event listener for groups.                           |
| [dismissGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/dismissGroup.html) | Disbands a group.                                            |
| [joinGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/joinGroup.html) | Joins a group.                                               |
| [quitGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/quitGroup.html) | Leaves a group.                                              |
| [removeGroupListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/removeGroupListener.html) | Removes an event listener for groups.                        |
| [acceptGroupApplication](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/acceptGroupApplication.html) | Accepts a request to join a group.                           |
| [createGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/createGroup.html) | Creates a group.                                             |
| [createTopicInCommunity](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/createTopicInCommunity.html) | Creates a topic.                                             |
| [deleteGroupAttributes](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/deleteGroupAttributes.html) | Deletes group attributes.                                    |
| [deleteTopicFromCommunity](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/deleteTopicFromCommunity.html) | Deletes a topic.                                             |
| [getGroupApplicationList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupApplicationList.html) | Gets the list of requests to join a group.                   |
| [getGroupAttributes](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupAttributes.html) | Gets group attributes.                                       |
| [getGroupMemberList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupMemberList.html) | Gets the group member list.                                  |
| [getGroupMembersInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupMembersInfo.html) | Gets the profiles of specified group members.                |
| [getGroupOnlineMemberCount](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupOnlineMemberCount.html) | Gets the number of online group members.                     |
| [getGroupsInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupsInfo.html) | Gets the profiles of groups.                                 |
| [getJoinedCommunityList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getJoinedCommunityList.html) | Gets the list of community groups the current user has joined. |
| [getJoinedGroupList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getJoinedGroupList.html) | Gets the list of groups the current user has joined.         |
| [getTopicInfoList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getTopicInfoList.html) | Gets the topics of a group.                                  |
| [initGroupAttributes](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/initGroupAttributes.html) | Initializes group attributes.                                |
| [inviteUserToGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/inviteUserToGroup.html) | Invites users to a group.                                    |
| [kickGroupMember](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/kickGroupMember.html) | Kicks members out of a group.                                |
| [muteGroupMember](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/muteGroupMember.html) | Mutes a group member.                                        |
| [refuseGroupApplication](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/refuseGroupApplication.html) | Rejects a request to join a group.                           |
| [searchGroupMembers](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/searchGroupMembers.html) | Searches for group members.                                  |
| [searchGroups](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/searchGroups.html) | Searches for group profiles.                                 |
| [setGroupApplicationRead](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setGroupApplicationRead.html) | Marks all group requests as read.                            |
| [setGroupAttributes](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setGroupAttributes.html) | Sets group attributes.                                       |
| [setGroupInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setGroupInfo.html) | Modifies the profile of a group.                             |
| [setGroupMemberInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setGroupMemberInfo.html) | Modifies the profile of a specified group member.            |
| [setGroupMemberRole](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setGroupMemberRole.html) | Sets a role for a group member.                              |
| [setTopicInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setTopicInfo.html) | Sets topic attributes.                                       |
| [transferGroupOwner](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/transferGroupOwner.html) | Transfers the ownership of a group.                          |

## Offline Push APIs

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [doBackground](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMOfflinePushManager/doBackground.html) | This API can be called when the app detects that the app switches to the background. |
| [doForeground](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMOfflinePushManager/doForeground.html) | This API can be called when the app detects that the app switches to the foreground. |
| [setOfflinePushConfig](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMOfflinePushManager/setOfflinePushConfig.html) | Configures offline push.                                     |
