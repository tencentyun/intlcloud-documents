## Event Callback APIs


| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TIMAddRecvNewMsgCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMAddRecvNewMsgCallback.html?h=TIMAddRecvNewMsgCallback) | Adds the callback for receiving new messages.                |
| [TIMRemoveRecvNewMsgCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMRemoveRecvNewMsgCallback.html?h=TIMRemoveRecvNewMsgCallback) | Deletes the callback for receiving new messages.             |
| [TIMSetMsgReadedReceiptCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMSetMsgReadedReceiptCallback.html?h=TIMSetMsgReadedReceiptCallback) | Sets the callback for message read receipts.                 |
| [TIMSetMsgRevokeCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMSetMsgRevokeCallback.html?h=TIMSetMsgRevokeCallback) | Sets the callback for message recalls.                       |
| [TIMSetMsgElemUploadProgressCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMSetMsgElemUploadProgressCallback.html?h=TIMSetMsgElemUploadProgressCallback) | Sets the callback for the upload progress of message element files. |
| [TIMSetGroupTipsEventCallback](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMSetGroupTipsEventCallback.html?h=TIMSetGroupTipsEventCallback) | Sets the callback for group system messages.                 |
| [TIMSetConvEventCallback](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMSetConvEventCallback.html?h=TIMSetConvEventCallback) | Sets the callback for conversation events.                   |
| [TIMSetNetworkStatusListenerCallback](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMSetNetworkStatusListenerCallback.html?h=TIMSetNetworkStatusListenerCallback) | Sets the callback for network connection status.             |
| [TIMSetKickedOfflineCallback](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMSetKickedOfflineCallback.html?h=TIMSetKickedOfflineCallback) | Sets the callback for notifications of forced logout.        |
| [TIMSetUserSigExpiredCallback](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMSetUserSigExpiredCallback.html?h=TIMSetUserSigExpiredCallback) | Sets the callback for user ticket expiration.                |
| [TIMSetOnAddFriendCallback](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMSetOnAddFriendCallback.html?h=TIMSetOnAddFriendCallback) | Sets the callback for adding friends.                        |
| [TIMSetOnDeleteFriendCallback](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMSetOnDeleteFriendCallback.html?h=TIMSetOnDeleteFriendCallback) | Sets the callback for deleting friends.                      |
| [TIMSetUpdateFriendProfileCallback](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMSetUpdateFriendProfileCallback.html?h=TIMSetUpdateFriendProfileCallback) | Sets the callback for updating friends' profiles.            |
| [TIMSetFriendAddRequestCallback](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMSetFriendAddRequestCallback.html?h=TIMSetFriendAddRequestCallback) | Sets the callback for friend requests.                       |
| [TIMSetLogCallback](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMSetLogCallback.html?h=TIMSetLogCallback) | Sets the callback for logs.                                  |
| [TIMSetMsgUpdateCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMSetMsgUpdateCallback.html?h=TIMSetMsgUpdateCallback) | Sets the callback for message update notifications returned after messages are modified in the cloud. |


## Chat SDK Initialization APIs

| API                                                          | Description                     |
| ------------------------------------------------------------ | ------------------------------- |
| [TIMInit](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMInit.html?h=TIMInit) | Initializes the Chat SDK.       |
| [TIMUninit](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMUninit.html) | Uninstalls the Chat SDK.        |
| [TIMGetSDKVersion](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMGetSDKVersion.html) | Gets Chat SDK version number.   |
| [TIMSetConfig](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMSetConfig.html) | Sets extra user configurations. |


## Login and Logout APIs

| API                                                          | Description |
| ------------------------------------------------------------ | ----------- |
| [TIMLogin](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMLogin.html) | Logs in.    |
| [TIMLogout](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMLogout.html) | Logs out.   |


## Conversation APIs

| API                                                          | Description                                               |
| ------------------------------------------------------------ | --------------------------------------------------------- |
| [TIMConvCreate](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvCreate.html) | Creates a conversation.                                   |
| [TIMConvDelete](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvDelete.html) | Deletes a conversation.                                   |
| [TIMConvGetConvList](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvGetConvList.html) | Gets the conversation list of recent contacts.            |
| [TIMConvSetDraft](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvSetDraft.html) | Sets the draft of a conversation.                         |
| [TIMConvCancelDraft](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvCancelDraft.html) | Deletes the draft of a conversation.                      |
| [TIMConvGetConvInfo](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvGetConvInfo.html) | Gets a conversation list.                                 |
| [TIMConvGetTotalUnreadMessageCount](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvGetTotalUnreadMessageCount.html) | Gets the total unread message count of all conversations. |
| [TIMConvPinConversation](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvPinConversation.html) | Pins a conversation to the top.                           |


## Message APIs

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TIMMsgBatchSend](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgBatchSend.html) | Sends a message to multiple users at a time, but not to groups. |
| [TIMMsgCancelSend](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgCancelSend.html) | Cancels a message being sent based on `messageID`.           |
| [TIMMsgClearHistoryMessage](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgClearHistoryMessage.html) | Clears the messages of a conversation.                       |
| [TIMMsgDelete](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgDelete.html) | Deletes the messages of a conversation.                      |
| [TIMMsgDeleteMessageExtensions](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgDeleteMessageExtensions.html) | Deletes message extensions.                                  |
| [TIMMsgDownloadElemToPath](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgDownloadElemToPath.html) | Downloads message elements to a path.                        |
| [TIMMsgDownloadMergerMessage](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgDownloadMergerMessage.html) | Downloads a combined message.                                |
| [TIMMsgFindByMsgLocatorList](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgFindByMsgLocatorList.html) | Locates a message of a conversation by using the message locator. |
| [TIMMsgFindMessages](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgFindMessages.html) | Queries local messages by `messageID`.                       |
| [TIMMsgGetC2CReceiveMessageOpt](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgGetC2CReceiveMessageOpt.html) | Queries the one-to-one message receiving option of a user.   |
| [TIMMsgGetMessageExtensions](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgGetMessageExtensions.html) | Gets message extensions.                                     |
| [TIMMsgGetMsgList](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgGetMsgList.html) | Gets the message list of a specified conversation.           |
| [TIMMsgImportMsgList](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgImportMsgList.html) | Imports a message list to a conversation.                    |
| [TIMMsgListDelete](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgListDelete.html) | Deletes the local and roaming messages of a conversation.    |
| [TIMMsgModifyMessage](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgModifyMessage.html) | Modifies a message.                                          |
| [TIMMsgReportReaded](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgReportReaded.html) | Marks a message as read.                                     |
| [TIMMsgRevoke](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgRevoke.html) | Recalls a message.                                           |
| [TIMMsgSaveMsg](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSaveMsg.html) | Saves a custom message.                                      |
| [TIMMsgSearchLocalMessages](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSearchLocalMessages.html) | Searches for local messages.                                 |
| [TIMMsgSendNewMsg](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSendMessage.html) | Sends a new message.                                         |
| [TIMMsgSendMessageV2](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSendMessageV2.html) | Sends a new message. (V2)                                    |
| [TIMMsgSetC2CReceiveMessageOpt](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSetC2CReceiveMessageOpt.html) | Sets the one-to-one message receiving option of a user.      |
| [TIMMsgSetGroupReceiveMessageOpt](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSetGroupReceiveMessageOpt.html) | Sets the group message receiving option.                     |
| [TIMMsgSetMessageExtensions](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSetMessageExtensions.html) | Sets message extensions.                                     |


## Group APIs

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TIMGroupCreate](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupCreate.html) | Creates a group.                                             |
| [TIMGroupDelete](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupDelete.html) | Disbands a group.                                            |
| [TIMGroupDeleteGroupAttributes](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupDeleteGroupAttributes.html) | Deletes group attributes.                                    |
| [TIMGroupDeleteMember](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupDeleteMember.html) | Deletes a group member.                                      |
| [TIMGroupGetGroupAttributes](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetGroupAttributes.html) | Gets specified group attributes.                             |
| [TIMGroupGetGroupInfoList](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetGroupInfoList.html) | Gets group information.                                      |
| [TIMGroupGetJoinedGroupList](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetJoinedGroupList.html) | Gets the list of groups that a user has joined.              |
| [TIMGroupGetMemberInfoList](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetMemberInfoList.html) | Gets group member information.                               |
| [TIMGroupGetOnlineMemberCount](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetOnlineMemberCount.html) | Gets the number of online members of a group.                |
| [TIMGroupGetPendencyList](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetPendencyList.html) | Gets the list of pending group requests.                     |
| [TIMGroupHandlePendency](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupHandlePendency.html) | Handles pending group requests.                              |
| [TIMGroupInitGroupAttributes](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupInitGroupAttributes.html) | Initializes group attributes.                                |
| [TIMGroupInviteMember](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupInviteMember.html) | Invites someone to join a group.                             |
| [TIMGroupJoin](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupJoin.html) | Requests to join a group.                                    |
| [TIMGroupModifyGroupInfo](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupModifyGroupInfo.html) | Modifies group information.                                  |
| [TIMGroupModifyMemberInfo](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupModifyMemberInfo.html) | Modifies group member information.                           |
| [TIMGroupQuit](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupQuit.html) | Leaves a group.                                              |
| [TIMGroupReportPendencyReaded](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupReportPendencyReaded.html) | Reports that a pending group request is read.                |
| [TIMGroupSearchGroupMembers](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupSearchGroupMembers.html) | Searches for group members.                                  |
| [TIMGroupSearchGroups](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupSearchGroups.html) | Searches for groups.                                         |
| [TIMGroupSetGroupAttributes](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupSetGroupAttributes.html) | Sets group attributes.                                       |
| [TIMMsgGetGroupMessageReadMemberList](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMMsgGetGroupMessageReadMemberList.html) | Gets the list of members who have or have not read the group message. |
| [TIMMsgGetMessageReadReceipts](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMMsgGetMessageReadReceipts.html) | Gets message read receipts.                                  |
| [TIMMsgSendMessageReadReceipts](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMMsgSendMessageReadReceipts.html) | Sends message read receipts.                                 |

 



## User Profile APIs

| API                                                          | Description                           |
| ------------------------------------------------------------ | ------------------------------------- |
| [TIMProfileGetUserProfileList](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMProfileGetUserProfileList.html) | Gets the profiles of specified users. |
| [TIMProfileModifySelfUserProfile](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMProfileModifySelfUserProfile.html) | Modifies one's own profile.           |


## Relationship Chain APIs

| API                                                          | Description                                    |
| ------------------------------------------------------------ | ---------------------------------------------- |
| [TIMFriendshipAddFriend](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipAddFriend.html) | Adds friends.                                  |
| [TIMFriendshipAddToBlackList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipAddToBlackList.html) | Adds a user to the blocklist.                  |
| [TIMFriendshipCheckFriendType](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipCheckFriendType.html) | Checks the friend type (one-way or two-way).   |
| [TIMFriendshipCreateFriendGroup](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipCreateFriendGroup.html) | Creates a friend list.                         |
| [TIMFriendshipDeleteFriend](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipDeleteFriend.html) | Deletes friends.                               |
| [TIMFriendshipDeleteFriendGroup](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipDeleteFriendGroup.html) | Deletes a friend list.                         |
| [TIMFriendshipDeleteFromBlackList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipDeleteFromBlackList.html) | Removes a user from the blocklist.             |
| [TIMFriendshipDeletePendency](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipDeletePendency.html) | Deletes a pending friend request.              |
| [TIMFriendshipGetBlackList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipGetBlackList.html) | Gets the blocklist.                            |
| [TIMFriendshipGetFriendGroupList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipGetFriendGroupList.html) | Gets the information of a friend list.         |
| [TIMFriendshipGetFriendProfileList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipGetFriendProfileList.html) | Gets friend lists.                             |
| [TIMFriendshipGetFriendsInfo](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipGetFriendsInfo.html) | Gets friend information.                       |
| [TIMFriendshipGetPendencyList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipGetPendencyList.html) | Gets the pending friend request list.          |
| [TIMFriendshipHandleFriendAddRequest](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipHandleFriendAddRequest.html) | Handles a friend request.                      |
| [TIMFriendshipModifyFriendGroup](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipModifyFriendGroup.html) | Modifies a friend list.                        |
| [TIMFriendshipModifyFriendProfile](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipModifyFriendProfile.html) | Updates friends' profiles (such as remarks).   |
| [TIMFriendshipReportPendencyReaded](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipReportPendencyReaded.html) | Reports that a pending friend request is read. |
| [TIMFriendshipSearchFriends](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipSearchFriends.html) | Searches for friends.                          |
