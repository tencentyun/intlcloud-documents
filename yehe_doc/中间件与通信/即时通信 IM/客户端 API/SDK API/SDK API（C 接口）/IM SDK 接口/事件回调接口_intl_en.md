
## TIMAddRecvNewMsgCallback

This API is used to add the callback function for receiving new messages.

**Prototype**

```c
TIM_DECL void TIMAddRecvNewMsgCallback(TIMRecvNewMsgCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMRecvNewMsgCallback | New message callback function. For more information, see [TIMRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?If a user has logged in, the IM SDK will send new messages using the callback function set by this API. New messages include not only unread messages but also any messages that do not exist on the local terminal. For example, when the IM SDK fetches recent contact messages, the last message in the conversation can be obtained. If the message does not exist on the local terminal, it will be sent using this method. After the user logs in, the IM SDK will fetch offline messages. In order not to miss message notifications, the user needs to register new message notifications before login.


## TIMRemoveRecvNewMsgCallback

This API is used to delete the callback function for receiving new messages.

**Prototype**

```c
TIM_DECL void TIMRemoveRecvNewMsgCallback(TIMRecvNewMsgCallback cb);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMRecvNewMsgCallback | New message callback function. For more information, see [TIMRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |

>?The `cb` parameter must be the same as that sent by [TIMAddRecvNewMsgCallback](#timaddrecvnewmsgcallback). Otherwise, the callback function cannot be deleted.


## TIMSetMsgReadedReceiptCallback

This API is used to set the callback function for message read receipts.

**Prototype**

```c
TIM_DECL void TIMSetMsgReadedReceiptCallback(TIMMsgReadedReceiptCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMMsgReadedReceiptCallback | Callback function for message read receipts. For more information, see [TIMMsgReadedReceiptCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?When the sender sends a message, the recipient calls the [TIMMsgReportReaded](https://intl.cloud.tencent.com/document/product/1047/34391) API to report that the message has been read. The IM SDK at the sender's end will send the receipt using the callback function set by this API.


## TIMSetMsgRevokeCallback

This API is used to set the callback function for notifying received message recall.

**Prototype**

```c
TIM_DECL void TIMSetMsgRevokeCallback(TIMMsgRevokeCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMMsgRevokeCallback | Callback function for notifying received message recall. For more information, see [TIMMsgRevokeCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?If the sender calls the [TIMMsgRevoke](https://intl.cloud.tencent.com/document/product/1047/34391) API to recall a message that it sends to the recipient, the IM SDK at the recipient's end will send a message recall notification using the callback function set by this API.


## TIMSetMsgElemUploadProgressCallback

This API is used to set the callback function for the upload progress of message element files.

**Prototype**

```c
TIM_DECL void TIMSetMsgElemUploadProgressCallback(TIMMsgElemUploadProgressCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMMsgElemUploadProgressCallback | Callback function for file upload progress. For more information, see [TIMMsgElemUploadProgressCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?Set the callback function for the message element upload progress. When a message contains image, voice, file, and video elements, the IM SDK will upload these files and trigger the callback function set by this API. Users can detect the upload progress based on the callback function.


## TIMGroupAttributeChangedCallback

This API is used to set the callback function for group attribute changes.

**Prototype**

```c
typedef void (*TIMGroupAttributeChangedCallback)(const char *group_id, const char* json_group_attibute_array, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| group_id | const char* | Group ID. |
| json_group_attibute_array | const char* | Group notification list. |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?If the attributes of a group you have joined are modified, all attributes of the group are returned (all members of the group can receive them).



## TIMSetGroupTipsEventCallback

This API is used to set the callback function for group system messages.

**Prototype**

```c
TIM_DECL void TIMSetGroupTipsEventCallback(TIMGroupTipsEventCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMGroupTipsEventCallback | Group message callback function. For more information, see [TIMGroupTipsEventCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?Group system message events include joining a group, leaving a group, being kicked out of a group, setting an admin, canceling an admin, modifying group information, and modifying group member information. These messages are sent to all group members.


## TIMSetConvEventCallback

This API is used to set the callback function for conversation events.

**Prototype**

```c
TIM_DECL void TIMSetConvEventCallback(TIMConvEventCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMConvEventCallback | Conversation event callback function. For more information, see [TIMConvEventCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?
>- Conversation events include:
>- Conversation creation
>- Conversation deletion
>- Conversation update
>- Any operation that generates a new conversation will trigger the conversation creation event, such as calling the [TIMConvCreate](https://intl.cloud.tencent.com/document/product/1047/34557) API to create a conversation or receiving the first message in an unknown conversation. Any operation that changes an existing conversation will trigger the conversation update event, such as receiving a new conversation message, recalling a message, and reporting that a message has been read. When the [TIMConvDelete](https://intl.cloud.tencent.com/document/product/1047/34557) API is called to delete a conversation, the conversation deletion event will be triggered.


## TIMConvTotalUnreadMessageCountChangedCallback

This API is used to set the callback function for obtaining the total unread message count of all conversations.

**Prototype**

```c
typedef void (*TIMConvTotalUnreadMessageCountChangedCallback)(int total_unread_count, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| total_unread_count | int | Total unread message count. |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |


## TIMSetNetworkStatusListenerCallback

This API is used to set the callback function for monitoring the network connection status.

**Prototype**

```c
TIM_DECL void TIMSetNetworkStatusListenerCallback(TIMNetworkStatusListenerCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMNetworkStatusListenerCallback | Network connection event callback function. For more information, see [TIMNetworkStatusListenerCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?
>- When the [TIMInit](https://intl.cloud.tencent.com/document/product/1047/34388) API is called, the IM SDK will connect to the Tencent Cloud backend. The callback function set by this API monitors the network connection status.
>- Network connection states include connecting, connection failed, connection successful, and connected. The network event does not indicate the user's local network status but only indicates whether the IM SDK is connected to the IM cloud server.
>- This callback function is optional. To allow users to detect whether the IM SDK is connected to the server, set this callback function. It notifies the caller whether the IM SDK is connected to or disconnected from the communication backend. If the network connection is interrupted, the IM SDK will reconnect to the network after the network recovers and automatically fetch messages to notify the caller. The caller does not need to be concerned about the network status. This callback function is for notification purposes only.
>- If a user has logged in, the IM SDK will reconnect to the network after the network recovers. The user does not need to be concerned about the network status.


## TIMSetKickedOfflineCallback

This API is used to set the callback function for kicked-offline notifications.

**Prototype**

```c
TIM_DECL void TIMSetKickedOfflineCallback(TIMKickedOfflineCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMKickedOfflineCallback | Callback function when the user is kicked offline. For more information, see [TIMKickedOfflineCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?
>- If a user has logged in on another terminal, the user will be kicked offline and receive a kicked offline notification. The common way to handle this is to inform the user to log out or kick the account on the other terminal offline.
>- If a user in the offline state is kicked offline, the user's next login will fail. A strong alert (login error code ERR_IMSDK_KICKED_BY_OTHERS: 6208) can be sent to the user. The user can also ignore this error and log in again.
>- Being kicked offline in online state:
A user logs in on device 1, stays online, and then logs in on device 2. At this time, the user will be kicked offline on device 1 and receive `TIMKickedOfflineCallback`. After the user receives the callback on device 1, the system prompts that the user can call login to log in on device 1 and kick device 2 offline.
>- Being kicked offline in offline state:
A user logs in on device 1 and exits the process without logging out on device 1. The user then logs in on device 2. As the user is offline on device 1, the user cannot detect this event. To explicitly notify the user of the event, the system will return the error code `ERR_IMSDK_KICKED_BY_OTHERS: 6208` when the user logs in on device 1 again. This error code indicates that the user was kicked offline the last time and allows the user to determine whether to go offline on the other device. If yes, the user can call login again to log in forcibly, and the instance online on device 2 will receive `TIMKickedOfflineCallback`.


## TIMSetUserSigExpiredCallback

This API is used to set the callback function for ticket expiration.

**Prototype**

```c
TIM_DECL void TIMSetUserSigExpiredCallback(TIMUserSigExpiredCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMUserSigExpiredCallback | Ticket expiration callback function. For more information, see [TIMUserSigExpiredCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?User tickets may expire. If a user ticket expires, the callback function set by this API will be called. [TIMLogin](https://intl.cloud.tencent.com/document/product/1047/34390) will return error code 70001. Developers can change the ticket based on the error code or ticket expiration callback function.


## TIMSetOnAddFriendCallback

This API is used to set the callback function for adding friends.

**Prototype**

```c
TIM_DECL void TIMSetOnAddFriendCallback(TIMOnAddFriendCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMOnAddFriendCallback | Callback function for adding friends. For more information, see [TIMOnAddFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?This callback function is used for multi-terminal synchronization. For example, the same IM SDK account has logged in to devices A and B. When device A adds a friend, the IM SDK on device B will receive a friend addition notification, and the IM SDK will notify the developer using this callback function.


## TIMSetOnDeleteFriendCallback

This API is used to set the callback function for deleting friends.

**Prototype**

```c
TIM_DECL void TIMSetOnDeleteFriendCallback(TIMOnDeleteFriendCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMOnDeleteFriendCallback | Callback function for deleting friends. For more information, see [TIMOnDeleteFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?This callback function is used for multi-terminal synchronization. For example, the same IM SDK account has logged in to devices A and B. When device A deletes a friend, the IM SDK on device B will receive a friend deletion notification, and the IM SDK will notify the developer using this callback function.


## TIMSetUpdateFriendProfileCallback

This API is used to set the callback function for updating friend profiles.

**Prototype**

```c
TIM_DECL void TIMSetUpdateFriendProfileCallback(TIMUpdateFriendProfileCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMUpdateFriendProfileCallback | Callback function for updating friend profiles. For more information, see [TIMUpdateFriendProfileCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?This callback function is used for multi-terminal synchronization. For example, the same IM SDK account has logged in to devices A and B. When device A updates a friend's profile, the IM SDK on device B will receive a friend profile update notification, and the IM SDK will notify the developer using this callback function.


## TIMSetFriendAddRequestCallback

This API is used to set the callback function for friend requests.

**Prototype**

```c
TIM_DECL void TIMSetFriendAddRequestCallback(TIMFriendAddRequestCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMFriendAddRequestCallback | Callback function for friend requests. For more information, see [TIMFriendAddRequestCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?If the logged-in user has set confirmation for friend requests and another user sends a friend request to this user, the logged-in user will receive the friend request callback, and the IM SDK will notify the developer using this callback function. If the same account has logged in on multiple terminals, each terminal will receive the callback.


## TIMFriendApplicationListDeletedCallback

This API is used to set the callback function for friend request deletion notifications.

**Prototype**

```c
typedef void(*TIMFriendApplicationListDeletedCallback)(const char* json_identifier_array, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_identifier_array | const char* | List of UserIDs whose friend requests are deleted. |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |


## TIMFriendApplicationListReadCallback

This API is used to set the callback function for friend request read notifications. When you call `setFriendApplicationRead` to set the friend request list as read, you will receive this callback (mainly used for multi-device synchronization).

**Prototype**

```c
typedef void(*TIMFriendApplicationListReadCallback)(const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |


## TIMFriendBlackListAddedCallback

This API is used to set the callback function for blocklist member addition notifications.

**Prototype**

```c
typedef void(*TIMFriendBlackListAddedCallback)(const char* json_friend_black_added_array, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_friend_black_added_array | const char* | List of UserIDs added to the blocklist. |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |



## TIMFriendBlackListDeletedCallback

This API is used to set the callback function for blocklist member deletion notifications.

**Prototype**

```c
typedef void(*TIMFriendBlackListDeletedCallback)(const char* json_identifier_array, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_identifier_array | const char* | List of UserIDs deleted from the blocklist. |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |


## TIMSetLogCallback

This API is used to set the callback function for logs.

**Prototype**

```c
TIM_DECL void TIMSetLogCallback(TIMLogCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMLogCallback | Log callback. For more information, see [TIMLogCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?After the log monitoring callback function is set, the IM SDK internal logs will be returned to the callback function set by this API. Developers can call the [TIMSetConfig](https://intl.cloud.tencent.com/document/product/1047/34388) API to configure the log levels of logs to be returned to the callback function.


## TIMSetMsgUpdateCallback

This API is used to set the callback function for message update notifications returned after messages are modified on the cloud.

**Prototype**

```c
TIM_DECL void TIMSetMsgUpdateCallback(TIMMsgUpdateCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMMsgUpdateCallback | Message update callback function. For more information, see [TIMMsgUpdateCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

>?
>- If a message that you send is modified on the server end, the IM SDK will notify you using this callback function.
>- You can intercept all IM messages on your server. For more information, see [Invoke a Callback Before Sending One-to-One Messages](https://intl.cloud.tencent.com/document/product/1047/34364).
>- After this callback function is set, the IM server will notify your business server of each message sent by your users.
>- Your business server can modify the messages (for example, filter sensitive words). If your server modifies a message, the IM SDK will notify you using this callback function.


