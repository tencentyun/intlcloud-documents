Tencent Cloud IM Cross-platform C APIs

**Download link for each platform:**

- [IM SDK for Windows](https://github.com/tencentyun/TIMSDK/tree/master/Windows), [Quick Integration with IM SDK for Windows](https://intl.cloud.tencent.com/document/product/1047/34310), and [Demo Quick Start](https://intl.cloud.tencent.com/document/product/1047/34553). IM SDK for Windows supports 32-bit and 64-bit operating systems.
- [IM SDK for iOS](https://github.com/tencentyun/TIMSDK/tree/master/iOS/IMSDK)
- [IM SDK for Mac](https://github.com/tencentyun/TIMSDK/tree/master/Mac/IMSDK)
- [IM SDK for Android](https://github.com/tencentyun/TIMSDK/tree/master/Android/IMSDK)

There are two types of callbacks. One is the asynchronous return from API calls, and the other is the notification pushed by the backend. The logic thread for callback triggering in the IM SDK may not be the same as the thread for API calls.
On the Windows platform, if you call the [TIMInit](https://intl.cloud.tencent.com/document/product/1047/34388) API to initialize the IM SDK after a UI message loop is created and the thread for calling the [TIMInit](https://intl.cloud.tencent.com/document/product/1047/34388) API is the main UI thread, the IM SDK will throw the callback to the main UI thread to call.

>!If the parameter string of the API contains Chinese characters, use UTF-8 encoding.



### Event callback APIs

| API                                             | Description                                                         |
|-----|-----|
| [TIMAddRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Adds the callback for receiving new messages |
| [TIMRemoveRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Deletes the callback for receiving new messages |
| [TIMSetMsgReadedReceiptCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for message read receipts |
| [TIMSetMsgRevokeCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for message recalls  |
| [TIMSetMsgElemUploadProgressCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for the upload progress of message element files |
| [TIMSetGroupTipsEventCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for group system messages |
| [TIMSetConvEventCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for conversation events |
| [TIMSetNetworkStatusListenerCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for network connection status |
| [TIMSetKickedOfflineCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for notifications of forced logout  |
| [TIMSetUserSigExpiredCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for user ticket expiration |
| [TIMSetOnAddFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for adding friends |
| [TIMSetOnDeleteFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for deleting friends |
| [TIMSetUpdateFriendProfileCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for updating friends' profiles |
| [TIMSetFriendAddRequestCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for friend requests |
| [TIMSetLogCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for logs |
| [TIMSetMsgUpdateCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | Sets the callback for message update notifications returned after messages are modified in the cloud |


### IM SDK initialization APIs

| API                                             | Description                                                         |
|-----|-----|
| [TIMInit](https://intl.cloud.tencent.com/document/product/1047/34388) | Initializes the IM SDK |
| [TIMUninit](https://intl.cloud.tencent.com/document/product/1047/34388) | Uninstalls the IM SDK |
| [TIMGetSDKVersion](https://intl.cloud.tencent.com/document/product/1047/34388) | Gets IM SDK version number |
| [TIMSetConfig](https://intl.cloud.tencent.com/document/product/1047/34388) | Sets extra user configurations |


### Login and logout APIs

| API                                             | Description                                                         |
|-----|-----|
| [TIMLogin](https://intl.cloud.tencent.com/document/product/1047/34390) | Logs in |
| [TIMLogout](https://intl.cloud.tencent.com/document/product/1047/34390) | Logs out |


### Conversation APIs

| API                                             | Description                                                         |
|-----|-----|
| [TIMConvCreate](https://intl.cloud.tencent.com/document/product/1047/34557) | Creates a conversation |
| [TIMConvDelete](https://intl.cloud.tencent.com/document/product/1047/34557) | Deletes a conversation |
| [TIMConvGetConvList](https://intl.cloud.tencent.com/document/product/1047/34557) | Gets the conversation list of recent contacts |
| [TIMConvSetDraft](https://intl.cloud.tencent.com/document/product/1047/34557) | Sets the draft of a conversation |
| [TIMConvCancelDraft](https://intl.cloud.tencent.com/document/product/1047/34557) | Deletes the draft of a conversation |


### Message APIs

| API                                             | Description                                                         |
|-----|-----|
| [TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1047/34391) | Sends a new message |
| [TIMMsgReportReaded](https://intl.cloud.tencent.com/document/product/1047/34391) | Marks a message as read |
| [TIMMsgRevoke](https://intl.cloud.tencent.com/document/product/1047/34391) | Recalls a message |
| [TIMMsgFindByMsgLocatorList](https://intl.cloud.tencent.com/document/product/1047/34391) |  Locates a message of a conversation by using the message locator |
| [TIMMsgImportMsgList](https://intl.cloud.tencent.com/document/product/1047/34391) | Imports a message list to a conversation |
| [TIMMsgSaveMsg](https://intl.cloud.tencent.com/document/product/1047/34391) | Saves a custom message |
| [TIMMsgGetMsgList](https://intl.cloud.tencent.com/document/product/1047/34391) | Gets the messages of a conversation |
| [TIMMsgDelete](https://intl.cloud.tencent.com/document/product/1047/34391) | Deletes the messages of a conversation |
| [TIMMsgDownloadElemToPath](https://intl.cloud.tencent.com/document/product/1047/34391) | Downloads message elements (such as image, video, audio, and file) to a path |
| [TIMMsgBatchSend](https://intl.cloud.tencent.com/document/product/1047/34391) | Sends a message to multiple users at a time, but not to groups |


### Group APIs

| API                                             | Description                                                         |
|-----|-----|
| [TIMGroupCreate](https://intl.cloud.tencent.com/document/product/1047/34393) | Creates a group |
| [TIMGroupDelete](https://intl.cloud.tencent.com/document/product/1047/34393) | Deletes a group |
| [TIMGroupJoin](https://intl.cloud.tencent.com/document/product/1047/34393) | Requests to join a group |
| [TIMGroupQuit](https://intl.cloud.tencent.com/document/product/1047/34393) | Quits a group |
| [TIMGroupInviteMember](https://intl.cloud.tencent.com/document/product/1047/34393) | Invites someone to join a group |
| [TIMGroupDeleteMember](https://intl.cloud.tencent.com/document/product/1047/34393member) | Removes a member from a group |
| [TIMGroupGetJoinedGroupList](https://intl.cloud.tencent.com/document/product/1047/34393) | Gets the list of groups that a user has joined |
| [TIMGroupGetGroupInfoList](https://intl.cloud.tencent.com/document/product/1047/34393) | Gets group information |
| [TIMGroupModifyGroupInfo](https://intl.cloud.tencent.com/document/product/1047/34393) | Modifies group information |
| [TIMGroupGetMemberInfoList](https://intl.cloud.tencent.com/document/product/1047/34393) | Gets group member information |
| [TIMGroupModifyMemberInfo](https://intl.cloud.tencent.com/document/product/1047/34393) | Modifies group member information |
| [TIMGroupGetPendencyList](https://intl.cloud.tencent.com/document/product/1047/34393) | Gets the pending group request list. <br/>Pending group requests are those that are not handled, for example, requests to join a group or to invite a user to join a group. |
| [TIMGroupReportPendencyReaded](https://intl.cloud.tencent.com/document/product/1047/34393) | Reports that a pending group request is read |
| [TIMGroupHandlePendency](https://intl.cloud.tencent.com/document/product/1047/34393) | Handles pending group requests |


### User profile APIs

| API                                             | Description                                                         |
|-----|-----|
| [TIMProfileGetUserProfileList](https://intl.cloud.tencent.com/document/product/1047/34558) | Gets the profiles of specified users |
| [TIMProfileModifySelfUserProfile](https://intl.cloud.tencent.com/document/product/1047/34558) | Modifies one’s own profile  |


### Relationship chain APIs

| API                                             | Description                                                         |
|-----|-----|
| [TIMFriendshipGetFriendProfileList](https://intl.cloud.tencent.com/document/product/1047/34559) | Gets friend lists |
| [TIMFriendshipAddFriend](https://intl.cloud.tencent.com/document/product/1047/34559) | Adds friends |
| [TIMFriendshipHandleFriendAddRequest](https://intl.cloud.tencent.com/document/product/1047/34559) | Handles friend requests |
| [TIMFriendshipModifyFriendProfile](https://intl.cloud.tencent.com/document/product/1047/34559) | Updates friends’ profiles (such as remarks) |
| [TIMFriendshipDeleteFriend](https://intl.cloud.tencent.com/document/product/1047/34559) | Deletes friends |
| [TIMFriendshipCheckFriendType](https://intl.cloud.tencent.com/document/product/1047/34559) | Checks the friend type (one-way or two-way) |
| [TIMFriendshipCreateFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559) | Creates a friend list |
| [TIMFriendshipGetFriendGroupList](https://intl.cloud.tencent.com/document/product/1047/34559) | Gets the information of a friend list |
| [TIMFriendshipModifyFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559) | Modifies a friend list |
| [TIMFriendshipDeleteFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559group) | Deletes a friend list |
| [TIMFriendshipAddToBlackList](https://intl.cloud.tencent.com/document/product/1047/34559) | Adds a user to the blocklist |
| [TIMFriendshipGetBlackList](https://intl.cloud.tencent.com/document/product/1047/34559) | Gets the blocklist |
| [TIMFriendshipDeleteFromBlackList](https://intl.cloud.tencent.com/document/product/1047/34559) | Removes a user from the blocklist |
| [TIMFriendshipGetPendencyList](https://intl.cloud.tencent.com/document/product/1047/34559) | Gets the pending friend request list |
| [TIMFriendshipDeletePendency](https://intl.cloud.tencent.com/document/product/1047/34559) |  Deletes a pending friend request |
| [TIMFriendshipReportPendencyReaded](https://intl.cloud.tencent.com/document/product/1047/34559) | Reports that a pending friend request is read |



