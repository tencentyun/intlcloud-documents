## Event Callback APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------ |
| [TIMAddRecvNewMsgCallback](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMAddRecvNewMsgCallback.html?h=addrecv) | Adds the callback for receiving new messages                               |
| [TIMRemoveRecvNewMsgCallback](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMRemoveRecvNewMsgCallback.html) | Deletes the callback for receiving new messages                               |
| [TIMSetMsgReadedReceiptCallback](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMSetMsgReadedReceiptCallback.html) | Sets the callback for message read receipts                             |
| [TIMSetMsgRevokeCallback](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMSetMsgRevokeCallback.html) | Sets the callback for message recalls                         |
| [TIMSetMsgElemUploadProgressCallback](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMSetMsgElemUploadProgressCallback.html) | Sets the callback for the upload progress of message element files               |
| [TIMSetGroupTipsEventCallback](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMSetGroupTipsEventCallback.html) | Sets the callback for group system messages                             |
| [TIMSetConvEventCallback](https://comm.qq.com/im/doc/electron/en/Api/conversationManager/TIMSetConvEventCallback.html) | Sets the callback for conversation events                                 |
| [TIMSetNetworkStatusListenerCallback](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMSetNetworkStatusListenerCallback.html) | Sets the callback for network connection status                         |
| [TIMSetKickedOfflineCallback](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMSetKickedOfflineCallback.html) | Sets the callback for notifications of forced logout                             |
| [TIMSetUserSigExpiredCallback](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMSetUserSigExpiredCallback.html) | Sets the callback for user ticket expiration                                 |
| [TIMSetOnAddFriendCallback](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMSetOnAddFriendCallback.html) | Sets the callback for adding friends                               |
| [TIMSetOnDeleteFriendCallback](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMSetOnDeleteFriendCallback.html) | Sets the callback for deleting friends                               |
| [TIMSetUpdateFriendProfileCallback](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMSetUpdateFriendProfileCallback.html) | Sets the callback for updating friends' profiles                           |
| [TIMSetFriendAddRequestCallback](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMSetFriendAddRequestCallback.html) | Sets the callback for friend requests                           |
| [TIMSetLogCallback](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMSetLogCallback.html) | Sets the callback for logs                                     |
| [TIMSetMsgUpdateCallback](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMSetMsgUpdateCallback.html) | Sets the callback for message update notifications returned after messages are modified in the cloud |


## IM SDK Initialization APIs

| API                                                          | Description               |
| ------------------------------------------------------------ | ------------------ |
| [TIMInit](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMInit.html) | Initializes the IM SDK      |
| [TIMUninit](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMUninit.html) | Uninstalls the IM SDK        |
| [TIMGetSDKVersion](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMGetSDKVersion.html) | Gets IM SDK version number |
| [TIMSetConfig](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMSetConfig.html) | Sets extra user configurations |


## Login and Logout APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ---- |
| [TIMLogin](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMLogin.html) | Logs in |
| [TIMLogout](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMLogout.html) | Logs out |


## Conversation APIs

| API                                                          | Description                  |
| ------------------------------------------------------------ | ------------------------ |
| [TIMConvCreate](https://comm.qq.com/im/doc/electron/en/Api/conversationManager/TIMConvCreate.html) | Creates a conversation                 |
| [TIMConvDelete](https://comm.qq.com/im/doc/electron/en/Api/conversationManager/TIMConvDelete.html) | Deletes a conversation                 |
| [TIMConvGetConvList](https://comm.qq.com/im/doc/electron/en/Api/conversationManager/TIMConvGetConvList.html) | Gets the conversation list of recent contacts |
| [TIMConvSetDraft](https://comm.qq.com/im/doc/electron/en/Api/conversationManager/TIMConvSetDraft.html) | Sets the draft of a conversation       |
| [TIMConvCancelDraft](https://comm.qq.com/im/doc/electron/en/Api/conversationManager/TIMConvCancelDraft.html) | Deletes the draft of a conversation       |


## Message APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [TIMMsgSendMessage](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMMsgSendMessage.html) | Sends a new message                                             |
| [TIMMsgReportReaded](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMMsgReportReaded.html) | Marks a message as read                                           |
| [TIMMsgRevoke](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMMsgRevoke.html) | Recalls a message                                               |
| [TIMMsgFindByMsgLocatorList](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMMsgFindByMsgLocatorList.html) | Locates a message of a conversation by using the message locator                     |
| [TIMMsgImportMsgList](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMMsgImportMsgList.html) | Imports a message list to a conversation                                 |
| [TIMMsgSaveMsg](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMMsgSaveMsg.html) | Saves a custom message                                         |
| [TIMMsgGetMsgList](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMMsgGetMsgList.html) | Gets the messages of a conversation                                 |
| [TIMMsgDelete](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMMsgDelete.html) | Deletes the messages of a conversation                                     |
| [TIMMsgDownloadElemToPath](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMMsgDownloadElemToPath.html) | Downloads message elements (such as image, video, audio, and file) to a path |
| [TIMMsgBatchSend](https://comm.qq.com/im/doc/electron/en/Api/advanceMessageManager/TIMMsgBatchSend.html) | Sends a message to multiple users at a time, but not to groups                 |


## Group APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TIMGroupCreate](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupCreate.html) | Creates a group                                                     |
| [TIMGroupDelete](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupDelete.html) | Deletes a group                                             |
| [TIMGroupJoin](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupJoin.html) | Requests to join a group                                                 |
| [TIMGroupQuit](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupQuit.html) | Quits a group                                                     |
| [TIMGroupInviteMember](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupInviteMember.html) | Invites someone to join a group                                                 |
| [TIMGroupDeleteMember](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupDeleteMember.html) | Removes a member from a group                                                 |
| [TIMGroupGetJoinedGroupList](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupGetJoinedGroupList.html) | Gets the list of groups that a user has joined                                           |
| [TIMGroupGetGroupInfoList](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupGetGroupInfoList.html) | Gets group information                                             |
| [TIMGroupModifyGroupInfo](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupModifyGroupInfo.html) | Modifies group information                                                   |
| [TIMGroupGetMemberInfoList](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupGetMemberInfoList.html) | Gets group member information                                           |
| [TIMGroupModifyMemberInfo](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupModifyMemberInfo.html) | Modifies group member information                                               |
| [TIMGroupGetPendencyList](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupGetPendencyList.html) | Gets the pending group request list. <br/>Pending group requests are those that are not handled, for example, requests to join a group or to invite a user to join a group. |
| [TIMGroupReportPendencyReaded](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupReportPendencyReaded.html) | Reports that a pending group request is read                                           |
| [TIMGroupHandlePendency](https://comm.qq.com/im/doc/electron/en/Api/groupManager/TIMGroupHandlePendency.html) | Handles pending group requests                                               |


## User Profile APIs

| API                                                          | Description                     |
| ------------------------------------------------------------ | -------------------------- |
| [TIMProfileGetUserProfileList](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMProfileGetUserProfileList.html) | Gets the profiles of specified users |
| [TIMProfileModifySelfUserProfile](https://comm.qq.com/im/doc/electron/en/Api/timbaseManager/TIMProfileModifySelfUserProfile.html) | Modifies one's own profile         |


## Relationship Chain APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | ---------------------------- |
| [TIMFriendshipGetFriendProfileList](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipGetFriendProfileList.html) | Gets friend lists                 |
| [TIMFriendshipAddFriend](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipAddFriend.html) | Adds friends                     |
| [TIMFriendshipHandleFriendAddRequest](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipHandleFriendAddRequest.html) | Handles friend requests                 |
| [TIMFriendshipModifyFriendProfile](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipModifyFriendProfile.html) | Updates friends' profiles (such as remarks)       |
| [TIMFriendshipDeleteFriend](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipDeleteFriend.html) | Deletes friends                     |
| [TIMFriendshipCheckFriendType](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipCheckFriendType.html) | Checks the friend type (one-way or two-way)   |
| [TIMFriendshipCreateFriendGroup](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipCreateFriendGroup.html) | Creates a friend list                 |
| [TIMFriendshipGetFriendGroupList](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipGetFriendGroupList.html) | Gets the information of a friend list   |
| [TIMFriendshipModifyFriendGroup](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipModifyFriendGroup.html) | Modifies a friend list                 |
| [TIMFriendshipDeleteFriendGroup](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipDeleteFriendGroup.html) | Deletes a friend list                 |
| [TIMFriendshipAddToBlackList](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipAddToBlackList.html) | Adds a user to the blocklist         |
| [TIMFriendshipGetBlackList](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipGetBlackList.html) | Gets the blocklist               |
| [TIMFriendshipDeleteFromBlackList](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipDeleteFromBlackList.html) | Removes a user from the blocklist   |
| [TIMFriendshipGetPendencyList](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipGetPendencyList.html) | Gets the pending friend request list |
| [TIMFriendshipDeletePendency](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipDeletePendency.html) | Deletes a pending friend request |
| [TIMFriendshipReportPendencyReaded](https://comm.qq.com/im/doc/electron/en/Api/friendshipManager/TIMFriendshipReportPendencyReaded.html) | Reports that a pending friend request is read |

