## TIMAddRecvNewMsgCallback

This API is used to add the callback function for receiving new messages.

**Prototype**

```c
TIM_DECL void TIMAddRecvNewMsgCallback(TIMRecvNewMsgCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                  | Description                                                  |
| --------- | --------------------- | ------------------------------------------------------------ |
| cb        | TIMRecvNewMsgCallback | New message callback function. For more information, see [TIMRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*          | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?If a user has logged in, the Chat SDK will send new messages using the callback function set by this API. New messages include not only unread messages but also any messages that do not exist on the local terminal. For example, when the Chat SDK fetches recent contact messages, the last message in the conversation can be obtained. If the message does not exist on the local terminal, it will be sent using this method. After the user logs in, the Chat SDK will fetch offline messages. In order not to miss message notifications, the user needs to register new message notifications before login.


## TIMRemoveRecvNewMsgCallback

This API is used to delete the callback function for receiving new messages.

**Prototype**

```c
TIM_DECL void TIMRemoveRecvNewMsgCallback(TIMRecvNewMsgCallback cb);
```

**Parameters**

| Parameter | Type                  | Description                                                  |
| --------- | --------------------- | ------------------------------------------------------------ |
| cb        | TIMRecvNewMsgCallback | New message callback function. For more information, see [TIMRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |

>?The `cb` parameter must be the same as that sent by [TIMAddRecvNewMsgCallback](#timaddrecvnewmsgcallback). Otherwise, the callback function cannot be deleted.


## TIMSetMsgReadedReceiptCallback

This API is used to set the callback function for message read receipts.

**Prototype**

```c
TIM_DECL void TIMSetMsgReadedReceiptCallback(TIMMsgReadedReceiptCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                        | Description                                                  |
| --------- | --------------------------- | ------------------------------------------------------------ |
| cb        | TIMMsgReadedReceiptCallback | Callback function for message read receipts. For more information, see [TIMMsgReadedReceiptCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?When the sender sends a message, the recipient calls the [TIMMsgReportReaded](https://intl.cloud.tencent.com/document/product/1047/34391) API to report that the message has been read or calls the [TIMMsgSendMessageReadReceipts](https://intl.cloud.tencent.com/document/product/1047/34391) API to send group message read receipts. The Chat SDK at the sender's end will send the receipts through the callback set by this API.


## TIMSetMsgRevokeCallback

This API is used to set the callback function for notifying received message recall.

**Prototype**

```c
TIM_DECL void TIMSetMsgRevokeCallback(TIMMsgRevokeCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                 | Description                                                  |
| --------- | -------------------- | ------------------------------------------------------------ |
| cb        | TIMMsgRevokeCallback | Callback function for notifying received message recall. For more information, see [TIMMsgRevokeCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*         | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?If the sender calls the [TIMMsgRevoke](https://intl.cloud.tencent.com/document/product/1047/34391) API to recall a message that is sent to the recipient, the Chat SDK at the recipient's end will send a message recall notification using the callback function set by this API.


## TIMSetMsgExtensionsChangedCallback

This API is used to set the callback function for updating message extensions.

**Prototype**

```c
TIM_DECL void TIMSetMsgExtensionsChangedCallback(TIMMsgExtensionsChangedCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                            | Description                                                  |
| --------- | ------------------------------- | ------------------------------------------------------------ |
| cb        | TIMMsgExtensionsChangedCallback | Callback function for updating message extensions. For more information, see [TIMMsgExtensionsChangedCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |


## TIMSetMsgExtensionsDeletedCallback

This API is used to set the callback function for deleting message extensions.

**Prototype**

```c
TIM_DECL void TIMSetMsgExtensionsDeletedCallback(TIMMsgExtensionsDeletedCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                            | Description                                                  |
| --------- | ------------------------------- | ------------------------------------------------------------ |
| cb        | TIMMsgExtensionsDeletedCallback | Callback function for deleting message extensions. For more information, see [TIMMsgExtensionsDeletedCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |


## TIMSetMsgElemUploadProgressCallback

This API is used to set the callback function for the upload progress of message element files.

**Prototype**

```c
TIM_DECL void TIMSetMsgElemUploadProgressCallback(TIMMsgElemUploadProgressCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                             | Description                                                  |
| --------- | -------------------------------- | ------------------------------------------------------------ |
| cb        | TIMMsgElemUploadProgressCallback | Callback function for file upload progress. For more information, see [TIMMsgElemUploadProgressCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                     | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?Set the callback function for the message element upload progress. When a message contains image, voice, file, and video elements, the Chat SDK will upload these files and trigger the callback function set by this API. Users can detect the upload progress based on the callback function.

## TIMSetGroupAttributeChangedCallback

This API is used to set the callback function for group attribute changes.

**Prototype**

```c
TIM_DECL void TIMSetGroupAttributeChangedCallback(TIMGroupAttributeChangedCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                             | Description                                                  |
| --------- | -------------------------------- | ------------------------------------------------------------ |
| cb        | TIMGroupAttributeChangedCallback | The callback function for group attribute changes. For more information, see [TIMGroupAttributeChangedCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                     | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?If the attributes of a group you have joined are modified, all attributes of the group are returned (all members of the group can receive them).


## TIMSetGroupCounterChangedCallback

This API is used to set the callback function for group counter changes.

**Prototype**

```c
TIM_DECL void TIMSetGroupCounterChangedCallback(TIMGroupCounterChangedCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                           | Description                                                  |
| --------- | ------------------------------ | ------------------------------------------------------------ |
| cb        | TIMGroupCounterChangedCallback | Callback function for group counter changes. For more information, see [TIMGroupCounterChangedCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                   | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?If the counters of a group that you have joined are modified, the new group counter values are returned to all members of the group.


## TIMSetGroupTipsEventCallback

This API is used to set the callback function for group system messages.

**Prototype**

```c
TIM_DECL void TIMSetGroupTipsEventCallback(TIMGroupTipsEventCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                      | Description                                                  |
| --------- | ------------------------- | ------------------------------------------------------------ |
| cb        | TIMGroupTipsEventCallback | Group message callback function. For more information, see [TIMGroupTipsEventCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*              | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?Group system message events include joining a group, leaving a group, being kicked out of a group, setting an admin, canceling an admin, modifying group information, and modifying group member information. These messages are sent to all group members.


## TIMSetConvEventCallback

This API is used to set the callback function for conversation events.

**Prototype**

```c
TIM_DECL void TIMSetConvEventCallback(TIMConvEventCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                 | Description                                                  |
| --------- | -------------------- | ------------------------------------------------------------ |
| cb        | TIMConvEventCallback | Conversation event callback function. For more information, see [TIMConvEventCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*         | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?
- Conversation events include:
 - Conversation creation
 - Conversation deletion
 - Conversation update
- Any operation that generates a new conversation will trigger the conversation creation event, such as calling the [TIMConvCreate](https://intl.cloud.tencent.com/document/product/1047/34557) API to create a conversation or receiving the first message in an unknown conversation. Any operation that changes an existing conversation will trigger the conversation update event, such as receiving a new conversation message, recalling a message, and reporting that a message has been read. When the [TIMConvDelete](https://intl.cloud.tencent.com/document/product/1047/34557) API is called to delete a conversation, the conversation deletion event will be triggered.


## TIMSetConvTotalUnreadMessageCountChangedCallback

This API is used to set the callback function for unread message count updates of all conversations.

**Prototype**

```c
TIM_DECL void TIMSetConvTotalUnreadMessageCountChangedCallback(TIMConvTotalUnreadMessageCountChangedCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                                          | Description                                                  |
| --------- | --------------------------------------------- | ------------------------------------------------------------ |
| cb        | TIMConvTotalUnreadMessageCountChangedCallback | Callback function for unread message count updates of all conversations. For more information, see [TIMConvTotalUnreadMessageCountChangedCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                                  | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?
- After you call TIMConvGetTotalUnreadMessageCount to get the total unread message count of all conversations, the Chat SDK notifies you of the latest unread message count through this callback upon any change to the unread message count.
- The total unread message count excludes the unread message count of Do-Not-Disturb conversations, namely conversations whose message receiving option is `kTIMRecvMsgOpt_Not_Receive` or `kTIMRecvMsgOpt_Not_Notify`.

## TIMSetConvUnreadMessageCountChangedByFilterCallback

This API is used to set the callback function for the unread message count updates by conversation filter.

**Prototype**

```c
TIM_DECL void TIMSetConvUnreadMessageCountChangedByFilterCallback(TIMConvTotalUnreadMessageCountChangedByFilterCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                                                  | Description                                                  |
| --------- | ----------------------------------------------------- | ------------------------------------------------------------ |
| cb        | TIMConvTotalUnreadMessageCountChangedByFilterCallback | Callback function for updates of the unread message count by conversation filter. For more information, see [TIMConvTotalUnreadMessageCountChangedByFilterCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                                          | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?
- You can call `subscribeUnreadMessageCountByFilter` to register for the listening to the changes of the total unread message count under specified filters. The Chat SDK notifies you of the latest unread message count through this callback.
- You can specify multiple filters for the unread count listening. The `filter` parameter in the callback lists the filters specified when you register for the listening. The `filter` parameter contains the `kTIMConversationListFilterConvType`, `kTIMConversationListFilterMarkType`, and `kTIMConversationListFilterGroupName` fields. Filters are distinguished by the values of these three fields.
- The total unread message count excludes the unread message count of Do-Not-Disturb conversations, namely conversations whose message receiving option is `kTIMRecvMsgOpt_Not_Receive` or `kTIMRecvMsgOpt_Not_Notify`.


## TIMSetNetworkStatusListenerCallback

This API is used to set the callback function for monitoring the network connection status.

**Prototype**

```c
TIM_DECL void TIMSetNetworkStatusListenerCallback(TIMNetworkStatusListenerCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                             | Description                                                  |
| --------- | -------------------------------- | ------------------------------------------------------------ |
| cb        | TIMNetworkStatusListenerCallback | Network connection event callback function. For more information, see [TIMNetworkStatusListenerCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                     | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?
- When the [TIMInit](https://intl.cloud.tencent.com/document/product/1047/34388) API is called, the Chat SDK will connect to the Tencent Cloud backend. The callback function set by this API monitors the network connection status.
- Network connection states include connecting, connection failed, connection successful, and connected. The network event does not indicate the user's local network status but only indicates whether the Chat SDK is connected to the Chat cloud server.
- This callback function is optional. To allow users to detect whether the Chat SDK is connected to the server, set this callback function. It notifies the caller whether the Chat SDK is connected to or disconnected from the communication backend. If the network connection is interrupted, the Chat SDK will reconnect to the network after the network recovers and automatically fetch messages to notify the caller. The caller does not need to be concerned about the network status. This callback function is for notification purposes only.
- If a user has logged in, the Chat SDK will reconnect to the network after the network recovers. The user does not need to be concerned about the network status.


## TIMSetKickedOfflineCallback

This API is used to set the callback function for kicked-offline notifications.

**Prototype**

```c
TIM_DECL void TIMSetKickedOfflineCallback(TIMKickedOfflineCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                     | Description                                                  |
| --------- | ------------------------ | ------------------------------------------------------------ |
| cb        | TIMKickedOfflineCallback | Callback function when the user is kicked offline. For more information, see [TIMKickedOfflineCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*             | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?
- If a user has logged in on another terminal, the user will be kicked offline and receive a kicked offline notification. The common way to handle this is to inform the user to log out or kick the account on the other terminal offline.
- If an offline user is kicked offline, the user's next login will fail. A strong alert (login error code ERR_IMSDK_KICKED_BY_OTHERS: 6208) can be sent to the user. The user can also ignore this error and log in again.
- Being kicked offline in online state:
A user logs in on device 1, stays online, and then logs in on device 2. At this time, the user will be kicked offline on device 1 and receive `TIMKickedOfflineCallback`. After the user receives the callback on device 1, the system prompts that the user can call login to log in on device 1 and kick device 2 offline.
- Being kicked offline in offline state:
A user logs in on device 1 and exits the process without logging out on device 1. The user then logs in on device 2. As the user is offline on device 1, the user cannot detect this event. To explicitly notify the user of the event, the system will return the error code `ERR_IMSDK_KICKED_BY_OTHERS: 6208` when the user logs in on device 1 again. This error code indicates that the user was kicked offline the last time and allows the user to determine whether to go offline on the other device. If yes, the user can call login again to log in forcibly, and the instance online on device 2 will receive `TIMKickedOfflineCallback`.


## TIMSetUserSigExpiredCallback

This API is used to set the callback function for ticket expiration.

**Prototype**

```c
TIM_DECL void TIMSetUserSigExpiredCallback(TIMUserSigExpiredCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                      | Description                                                  |
| --------- | ------------------------- | ------------------------------------------------------------ |
| cb        | TIMUserSigExpiredCallback | Ticket expiration callback function. For more information, see [TIMUserSigExpiredCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*              | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?User tickets may expire. If a user ticket expires, the callback function set by this API will be called. [TIMLogin](https://intl.cloud.tencent.com/document/product/1047/34390) will return error code 70001. Developers can change the ticket based on the error code or ticket expiration callback function.


## TIMSetOnAddFriendCallback

This API is used to set the callback function for adding friends.

**Prototype**

```c
TIM_DECL void TIMSetOnAddFriendCallback(TIMOnAddFriendCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                   | Description                                                  |
| --------- | ---------------------- | ------------------------------------------------------------ |
| cb        | TIMOnAddFriendCallback | Callback function for adding friends. For more information, see [TIMOnAddFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*           | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?This callback function is used for multi-terminal synchronization. For example, the same Chat SDK account has logged in to devices A and B. When device A adds a friend, the Chat SDK on device B will receive a friend addition notification, and the Chat SDK will notify the developer using this callback function.


## TIMSetOnDeleteFriendCallback

This API is used to set the callback function for deleting friends.

**Prototype**

```c
TIM_DECL void TIMSetOnDeleteFriendCallback(TIMOnDeleteFriendCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                      | Description                                                  |
| --------- | ------------------------- | ------------------------------------------------------------ |
| cb        | TIMOnDeleteFriendCallback | Callback function for deleting friends. For more information, see [TIMOnDeleteFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*              | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?This callback function is used for multi-terminal synchronization. For example, the same Chat SDK account has logged in to devices A and B. When device A deletes a friend, the Chat SDK on device B will receive a friend deletion notification, and the Chat SDK will notify the developer using this callback function.


## TIMSetUpdateFriendProfileCallback

This API is used to set the callback function for updating friend profiles.

**Prototype**

```c
TIM_DECL void TIMSetUpdateFriendProfileCallback(TIMUpdateFriendProfileCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                           | Description                                                  |
| --------- | ------------------------------ | ------------------------------------------------------------ |
| cb        | TIMUpdateFriendProfileCallback | Callback function for updating friend profiles. For more information, see [TIMUpdateFriendProfileCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                   | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?This callback function is used for multi-terminal synchronization. For example, the same Chat SDK account has logged in to devices A and B. When device A updates a friend's profile, the Chat SDK on device B will receive a friend profile update notification, and the Chat SDK will notify the developer using this callback function.


## TIMSetFriendAddRequestCallback

This API is used to set the callback function for friend requests.

**Prototype**

```c
TIM_DECL void TIMSetFriendAddRequestCallback(TIMFriendAddRequestCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                        | Description                                                  |
| --------- | --------------------------- | ------------------------------------------------------------ |
| cb        | TIMFriendAddRequestCallback | Callback function for friend requests. For more information, see [TIMFriendAddRequestCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?If the logged-in user has set confirmation for friend requests and another user sends a friend request to this user, the logged-in user will receive the friend request callback, and the Chat SDK will notify the developer using this callback function. If the same account has logged in on multiple terminals, each terminal will receive the callback.


## TIMSetFriendApplicationListDeletedCallback

This API is used to set the callback function for friend request deletion.

**Prototype**

```c
TIM_DECL void TIMSetFriendApplicationListDeletedCallback(TIMFriendApplicationListDeletedCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                                    | Description                                                  |
| --------- | --------------------------------------- | ------------------------------------------------------------ |
| cb        | TIMFriendApplicationListDeletedCallback | Callback function for friend request deletion. For more information, see [TIMFriendApplicationListDeletedCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                            | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?
- Proactively delete a friend request.
- Reject a friend request.
- Accept a friend request.
- Your friend request is rejected by others.


## TIMSetFriendApplicationListReadCallback

This API is used to set the callback function for friend request read notifications.

**Prototype**

```c
TIM_DECL void TIMSetFriendApplicationListReadCallback(TIMFriendApplicationListReadCallback cb, const void* user_data);

```

**Parameters**

| Parameter | Type                                 | Description                                                  |
| --------- | ------------------------------------ | ------------------------------------------------------------ |
| cb        | TIMFriendApplicationListReadCallback | Callback function for friend request read notifications. For more information, see [TIMFriendApplicationListReadCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                         | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?If you call `setFriendApplicationRead` to set the friend request list as read, you will receive this callback (mainly used for multi-device synchronization).


## TIMSetFriendBlackListAddedCallback

This API is used to set the callback function for adding a user to the blocklist.

**Prototype**

```c
TIM_DECL void TIMSetFriendBlackListAddedCallback(TIMFriendBlackListAddedCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                            | Description                                                  |
| --------- | ------------------------------- | ------------------------------------------------------------ |
| cb        | TIMFriendBlackListAddedCallback | Callback function for adding a user to the blocklist. For more information, see [TIMFriendBlackListAddedCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |


## TIMSetFriendBlackListDeletedCallback

This API is used to set the callback function for removing a user from the blocklist.

**Prototype**

```c
TIM_DECL void TIMSetFriendBlackListDeletedCallback(TIMFriendBlackListDeletedCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                              | Description                                                  |
| --------- | --------------------------------- | ------------------------------------------------------------ |
| cb        | TIMFriendBlackListDeletedCallback | Callback function for removing a user from the blocklist. For more information, see [TIMFriendBlackListDeletedCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*                      | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |


## TIMSetLogCallback

This API is used to set the callback function for logs.

**Prototype**

```c
TIM_DECL void TIMSetLogCallback(TIMLogCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type           | Description                                                  |
| --------- | -------------- | ------------------------------------------------------------ |
| cb        | TIMLogCallback | Log callback. For more information, see [TIMLogCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*   | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?After the log monitoring callback function is set, the Chat SDK internal logs will be returned to the callback function set by this API. Developers can call the [TIMSetConfig](https://intl.cloud.tencent.com/document/product/1047/34388) API to configure the log levels of logs to be returned to the callback function.


## TIMSetMsgUpdateCallback

This API is used to set the callback function for message update notifications returned after messages are modified on the cloud.

**Prototype**

```c
TIM_DECL void TIMSetMsgUpdateCallback(TIMMsgUpdateCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type                 | Description                                                  |
| --------- | -------------------- | ------------------------------------------------------------ |
| cb        | TIMMsgUpdateCallback | Message update callback function. For more information, see [TIMMsgUpdateCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*         | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

>?
- If a message that you send is modified on the server end, the Chat SDK will notify you using this callback function.
- You can intercept all Chat messages on your server. For more information, see [Before a One-to-One Message Is Sent](https://intl.cloud.tencent.com/document/product/1047/34364).
- After this callback function is set, the Chat server will notify your business server of each message sent by your users.
- Your business server can modify the messages (for example, filter sensitive words). If your server modifies a message, the Chat SDK will notify you using this callback function.
