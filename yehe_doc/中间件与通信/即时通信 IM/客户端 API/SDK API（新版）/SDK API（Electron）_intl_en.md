## Event Callback APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------ |
| [TIMAddRecvNewMsgCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Adds the callback for receiving new messages                               |
| [TIMRemoveRecvNewMsgCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Deletes the callback for receiving new messages                               |
| [TIMSetMsgReadedReceiptCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for message read receipts                             |
| [TIMSetMsgRevokeCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for message recalls                         |
| [TIMSetMsgElemUploadProgressCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for the upload progress of message element files               |
| [TIMSetGroupTipsEventCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for group system messages                             |
| [TIMSetConvEventCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for conversation events                                 |
| [TIMSetNetworkStatusListenerCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for network connection status                         |
| [TIMSetKickedOfflineCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for notifications of forced logout                             |
| [TIMSetUserSigExpiredCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for user ticket expiration                                 |
| [TIMSetOnAddFriendCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for adding friends                               |
| [TIMSetOnDeleteFriendCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for deleting friends                               |
| [TIMSetUpdateFriendProfileCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for updating friends' profiles                           |
| [TIMSetFriendAddRequestCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for friend requests                           |
| [TIMSetLogCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for logs                                     |
| [TIMSetMsgUpdateCallback](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the callback for message update notifications returned after messages are modified in the cloud |


## IM SDK Initialization APIs

| API                                                          | Description               |
| ------------------------------------------------------------ | ------------------ |
| [TIMInit](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Initializes the IM SDK      |
| [TIMUninit](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Uninstalls the IM SDK        |
| [TIMGetSDKVersion](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets IM SDK version number |
| [TIMSetConfig](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets extra user configurations |


## Login and Logout APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ---- |
| [TIMLogin](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Logs in |
| [TIMLogout](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Logs out |


## Conversation APIs

| API                                                          | Description                  |
| ------------------------------------------------------------ | ------------------------ |
| [TIMConvCreate](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Creates a conversation                 |
| [TIMConvDelete](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Deletes a conversation                 |
| [TIMConvGetConvList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets the conversation list of recent contacts |
| [TIMConvSetDraft](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sets the draft of a conversation       |
| [TIMConvCancelDraft](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Deletes the draft of a conversation       |


## Message APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [TIMMsgSendNewMsg](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sends a new message                                             |
| [TIMMsgReportReaded](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Marks a message as read                                           |
| [TIMMsgRevoke](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Recalls a message                                               |
| [TIMMsgFindByMsgLocatorList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Locates a message of a conversation by using the message locator                     |
| [TIMMsgImportMsgList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Imports a message list to a conversation                                 |
| [TIMMsgSaveMsg](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Saves a custom message                                         |
| [TIMMsgGetMsgList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets the messages of a conversation                                 |
| [TIMMsgDelete](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Deletes the messages of a conversation                                     |
| [TIMMsgDownloadElemToPath](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Downloads message elements (such as image, video, audio, and file) to a path |
| [TIMMsgBatchSend](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Sends a message to multiple users at a time, but not to groups                 |


## Group APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TIMGroupCreate](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Creates a group                                                     |
| [TIMGroupDelete](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Deletes a group                                             |
| [TIMGroupJoin](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Requests to join a group                                                 |
| [TIMGroupQuit](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Quits a group                                                     |
| [TIMGroupInviteMember](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Invites someone to join a group                                                 |
| [TIMGroupDeleteMember](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Removes a member from a group                                                 |
| [TIMGroupGetJoinedGroupList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets the list of groups that a user has joined                                           |
| [TIMGroupGetGroupInfoList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets group information                                             |
| [TIMGroupModifyGroupInfo](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Modifies group information                                                   |
| [TIMGroupGetMemberInfoList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets group member information                                           |
| [TIMGroupModifyMemberInfo](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Modifies group member information                                               |
| [TIMGroupGetPendencyList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets the pending group request list. <br/>Pending group requests are those that are not handled, for example, requests to join a group or to invite a user to join a group. |
| [TIMGroupReportPendencyReaded](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Reports that a pending group request is read                                           |
| [TIMGroupHandlePendency](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Handles pending group requests                                               |


## User Profile APIs

| API                                                          | Description                     |
| ------------------------------------------------------------ | -------------------------- |
| [TIMProfileGetUserProfileList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets the profiles of specified users |
| [TIMProfileModifySelfUserProfile](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Modifies one's own profile         |


## Relationship Chain APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | ---------------------------- |
| [TIMFriendshipGetFriendProfileList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets friend lists                 |
| [TIMFriendshipAddFriend](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Adds friends                     |
| [TIMFriendshipHandleFriendAddRequest](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Handles friend requests                 |
| [TIMFriendshipModifyFriendProfile](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Updates friends' profiles (such as remarks)       |
| [TIMFriendshipDeleteFriend](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Deletes friends                     |
| [TIMFriendshipCheckFriendType](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Checks the friend type (one-way or two-way)   |
| [TIMFriendshipCreateFriendGroup](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Creates a friend list                 |
| [TIMFriendshipGetFriendGroupList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets the information of a friend list   |
| [TIMFriendshipModifyFriendGroup](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Modifies a friend list                 |
| [TIMFriendshipDeleteFriendGroup](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Deletes a friend list                 |
| [TIMFriendshipAddToBlackList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Adds a user to the blocklist         |
| [TIMFriendshipGetBlackList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets the blocklist               |
| [TIMFriendshipDeleteFromBlackList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Removes a user from the blocklist   |
| [TIMFriendshipGetPendencyList](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Gets the pending friend request list |
| [TIMFriendshipDeletePendency](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Deletes a pending friend request |
| [TIMFriendshipReportPendencyReaded](https://comm.qq.com/en_doc_site/electron/doc/index.html) | Reports that a pending friend request is read |

