>?For API details, see [Unity APIs](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.html).

## Event Callback APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------ |
| [AddRecvNewMsgCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Adds the callback for receiving new messages. |
| [RemoveRecvNewMsgCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Deletes the callback for receiving new messages. |
| [SetMsgReadedReceiptCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for message read receipts. |
| [SetMsgRevokeCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for message recalls. |
| [SetMsgElemUploadProgressCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for the upload progress of message element files. |
| [SetGroupTipsEventCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for group system messages. |
| [SetConvEventCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for conversation events. |
| [SetNetworkStatusListenerCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for network connection status. |
| [SetKickedOfflineCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for kicked-offline notifications. |
| [SetUserSigExpiredCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for ticket expiration. |
| [SetOnAddFriendCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for adding friends. |
| [SetOnDeleteFriendCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for deleting friends. |
| [SetUpdateFriendProfileCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for updating friend profiles. |
| [SetFriendAddRequestCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for friend requests. |
| [SetLogCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for logs. |
| [SetMsgUpdateCallback](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the callback for message update notifications returned after messages are modified in the cloud. |


## IM SDK Initialization APIs

| API                                                          | Description               |
| ------------------------------------------------------------ | ------------------ |
| [Init](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Initializes the IM SDK. |
| [Uninit](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Uninstalls the IM SDK. |
| [GetSDKVersion](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the IM SDK version number. |
| [SetConfig](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets extra user configurations. |


## Login and Logout APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ---- |
| [Login](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Logs in. |
| [Logout](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Logs out. |


## Conversation APIs

| API                                                          | Description                  |
| ------------------------------------------------------------ | ------------------------ |
| [ConvCreate](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Creates a conversation. |
| [ConvDelete](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Deletes a conversation. |
| [ConvGetConvList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the conversation list of recent contacts. |
| [ConvSetDraft](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sets the draft of a conversation. |
| [ConvCancelDraft](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Deletes the draft of a conversation. |


## Message APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [MsgSendNewMsg](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sends a new message. |
| [MsgReportReaded](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Reports that a message is read. |
| [MsgRevoke](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Recalls a message. |
| [MsgFindByMsgLocatorList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Searches for messages in a conversation precisely based on message locations. |
| [MsgImportMsgList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Imports a list of messages to a conversation. |
| [MsgSaveMsg](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Saves a custom message. |
| [MsgGetMsgList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the message list of a conversation. |
| [MsgDelete](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Deletes messages of a conversation. |
| [MsgDownloadElemToPath](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Downloads the image, video, audio, or file elements in messages to a file path. |
| [MsgBatchSend](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Sends messages in batches. This API does not support sending messages to groups. |


## Group APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [GroupCreate](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Creates a group. |
| [GroupDelete](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Deletes a group. |
| [GroupJoin](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Applies to join a group. |
| [GroupQuit](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Quits a group. |
| [GroupInviteMember](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Invites users to a group. |
| [GroupDeleteMember](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Deletes group members. |
| [GroupGetJoinedGroupList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the list of joined groups. |
| [GroupGetGroupInfoList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the list of group information. |
| [GroupModifyGroupInfo](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Modifies group information. |
| [GroupGetMemberInfoList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the list of group member information. |
| [GroupModifyMemberInfo](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Modifies group member information. |
| [GroupGetPendencyList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the list of pending group requests.<br/>A pending group request is an operation that has not yet been processed, for example, an invite to join a group or a request to join a group. |
| [GroupReportPendencyReaded](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Reports that pending group requests are read. |
| [GroupHandlePendency](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Processes pending group requests. |


## User Profile APIs

| API                                                          | Description                     |
| ------------------------------------------------------------ | -------------------------- |
| [ProfileGetUserProfileList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the profiles of a list of users. |
| [ProfileModifySelfUserProfile](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Modifies one's own profile. |


## Relationship Chain APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | ---------------------------- |
| [FriendshipGetFriendProfileList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the friend list. |
| [FriendshipAddFriend](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Adds a friend. |
| [FriendshipHandleFriendAddRequest](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Processes friend requests. |
| [FriendshipModifyFriendProfile](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Updates the profile (such as remarks) of a friend. |
| [FriendshipDeleteFriend](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Deletes a friend. |
| [FriendshipCheckFriendType](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Checks the friend type (one-way or two-way). |
| [FriendshipCreateFriendGroup](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Creates a friend list. |
| [FriendshipGetFriendGroupList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the information of a friend list. |
| [FriendshipModifyFriendGroup](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Modifies a friend list. |
| [FriendshipDeleteFriendGroup](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Deletes a friend list. |
| [FriendshipAddToBlackList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Adds a friend to the blocklist. |
| [FriendshipGetBlackList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the blocklist. |
| [FriendshipDeleteFromBlackList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Removes a friend from the blocklist. |
| [FriendshipGetPendencyList](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Gets the list of pending friend requests. |
| [FriendshipDeletePendency](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Deletes a pending friend request. |
| [FriendshipReportPendencyReaded](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html) | Reports that a pending friend request is read. |

