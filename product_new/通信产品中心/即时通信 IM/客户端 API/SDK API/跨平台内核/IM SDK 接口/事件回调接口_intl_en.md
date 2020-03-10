
## TIMAddRecvNewMsgCallback

Adds the callback for receiving new messages.

**Prototype**

```c
TIM_DECL void TIMAddRecvNewMsgCallback(TIMRecvNewMsgCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMRecvNewMsgCallback | The callback function for new messages. For more information, see [TIMRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timrecvnewmsgcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

> If the user is logged in, the IM SDK will send newly received messages by using the callback set by this API. Note that not only unread messages are sent. Any messages that do not exist on the local terminal are sent. For example, if a message has been read on another terminal, when the IM SDK pulls recent contact messages, the last message in the conversation can be obtained. If the message does not exist on the local terminal, it will be sent by using this method. After the user logs in, the IM SDK will pull offline messages. In order not to miss any message notifications, the user needs to register new message notifications before login.


## TIMRemoveRecvNewMsgCallback

Deletes the callback for receiving new messages.

**Prototype**

```c
TIM_DECL void TIMRemoveRecvNewMsgCallback(TIMRecvNewMsgCallback cb);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMRecvNewMsgCallback | The callback function for new messages. For more information, see [TIMRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timrecvnewmsgcallback). |

> The cb parameter must be consistent with that passed in by [TIMAddRecvNewMsgCallback] (#timaddrecvnewmsgcallback). Otherwise, the callback cannot be deleted.


## TIMSetMsgReadedReceiptCallback

Sets the callback for message read receipt.

**Prototype**

```c
TIM_DECL void TIMSetMsgReadedReceiptCallback(TIMMsgReadedReceiptCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMMsgReadedReceiptCallback | The callback function for message read receipt. For more information, see [TIMMsgReadedReceiptCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timmsgreadedreceiptcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

> When the sender sends a message, the recipient invokes the [TIMMsgReportReaded] (https://intl.cloud.tencent.com/document/product/1047/34391#timmsgreportreaded) API to report that the message has been read. Then, the IM SDK for the sender will send the receipt through the callback set by this API.


## TIMSetMsgRevokeCallback

Sets the callback for revoking received messages.

**Prototype**

```c
TIM_DECL void TIMSetMsgRevokeCallback(TIMMsgRevokeCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMMsgRevokeCallback | The callback function for message revocation notifications. For more information, see [TIMMsgRevokeCallback] (https://intl.cloud.tencent.com/document/product/1047/34550#timmsgrevokecallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

> After the sender sends a message to the recipient, if the sender then invokes the [TIMMsgRevoke] (https://intl.cloud.tencent.com/document/product/1047/34391#timmsgrevoke) API to revoke the message. the IM SDK for the recipient will send a notification through the callback set by this API.


## TIMSetMsgElemUploadProgressCallback

Sets the callback for checking the progress of uploading files pertaining to message elements.

**Prototype**

```c
TIM_DECL void TIMSetMsgElemUploadProgressCallback(TIMMsgElemUploadProgressCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMMsgElemUploadProgressCallback | The callback function for checking the file upload progress. For more information, see [TIMMsgElemUploadProgressCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timmsgelemuploadprogresscallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

> Sets the callback for checking the progress of uploading message elements. When a message contains the image, audio, file, or video elements, the IM SDK will upload these files and trigger the callback set by this API. Users can learn about the upload progress based on the callback.


## TIMSetGroupTipsEventCallback

Sets the callback for group system messages.

**Prototype**

```c
TIM_DECL void TIMSetGroupTipsEventCallback(TIMGroupTipsEventCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMGroupTipsEventCallback | The callback for group messages. For more information, see [TIMGroupTipsEventCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timgrouptipseventcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

> Group system message events include joining a group, exiting from a group, removing from a group, setting an admin, canceling an admin, modifying the group profile, and modifying group member profiles. These messages are sent to all group members.


## TIMSetConvEventCallback

Sets the callback for conversation events.

**Prototype**

```c
TIM_DECL void TIMSetConvEventCallback(TIMConvEventCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMConvEventCallback | The callback for conversation events. For more information, see [TIMConvEventCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timconveventcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

>
- Conversation events include:
 - Conversation creation
 - Conversation deletion
 - Conversation update
- Any operation that generates a new conversation will trigger the conversation creation event, such as invoking the [TIMConvCreate](https://intl.cloud.tencent.com/document/product/1047/34557#timconvcreate) API to create a conversation or receiving the first message in an unknown conversation. Any operation that changes an existing conversation will trigger the conversation update event, such as receiving a new conversation message, revoking messages, and reporting that a message has been read. When the [TIMConvDelete](https://intl.cloud.tencent.com/document/product/1047/34557#timconvdelete) API is invoked to delete a conversation, the conversation deletion event will be triggered.


## TIMSetNetworkStatusListenerCallback

Sets the callback for monitoring the network connection status.

**Prototype**

```c
TIM_DECL void TIMSetNetworkStatusListenerCallback(TIMNetworkStatusListenerCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMNetworkStatusListenerCallback | The callback for network connection events. For more information, see [TIMNetworkStatusListenerCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timnetworkstatuslistenercallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

>
- When the [TIMInit](https://cloud.tencent.com/document/product/269/33546#timinit) API is invoked, the IM SDK will connect to the Tencent Cloud backend. The callback set by this API monitors the network connection status. 
- Possible network connection states are connecting, connection failed, connection successful, and connected. The network event does not indicate the local network status but only indicates whether the IM SDK is connected to the IM cloud server.
- This callback is optional. To allow users to check whether the IM SDK is connected to the server, set this callback. It notifies the user of whether the link between the invoker and the communication backend is connected or disconnected. If the network connection is disconnected, the IM SDK will automatically reconnect to the network after the connection is restored, and will automatically pull messages and notify the user. In this case, the user does not need to be concerned about the network status. This callback is for notification purposes only.
- If the user is logged in, the IM SDK will automatically disconnect from and then reconnect to the network without user intervention.


## TIMSetKickedOfflineCallback

Sets the callback for forced logout notifications.

**Prototype**

```c
TIM_DECL void TIMSetKickedOfflineCallback(TIMKickedOfflineCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMKickedOfflineCallback | The callback for forced logout. For more information, see[TIMKickedOfflineCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timkickedofflinecallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

>
- If the user is logged in on another terminal, the user will be set offline and receive a forced offline notification. The typical way of handling this situation is to inform the user to perform the desired operation (log out or set the user on the other terminal offline).
- If the user is set offline when already in the offline status, the user’s next login will fail. In this case, the developer can set a very strong alert (with the login error code ERR_IMSDK_KICKED_BY_OTHERS: 6208) for users, or ignore this error and allow users to log in again.
- Setting offline mutually with two devices in the online state:
The user logs in on device 1, stays online, and then logs in on device 2. At this time, the user will be set offline on device 1 and receive the `TIMKickedOfflineCallback` callback. After the user receives the callback on device 1, the system prompts that the user can invoke login to log in on device 1 and force device 2 offline.
- Setting offline mutually with two devices in the offline state:
The user logs in on device 1 and terminates the process without logging out on device 1. Then, the user logs in on device 2. Since the user is not online on device 1, the user cannot receive this event. In this case, to explicitly notify the user of the occurred event, the system returns the error code ERR_IMSDK_KICKED_BY_OTHERS: 6208 when the user tries to log in on device 1 again to indicate that the user was set offline previously and allow the user to determine whether to force the other device offline. If yes, device 1 will invoke login again to log in forcibly, and the login instance on device 2 will receive the `TIMKickedOfflineCallback` callback.


## TIMSetUserSigExpiredCallback

Sets the callback for ticket expiration.

**Prototype**

```c
TIM_DECL void TIMSetUserSigExpiredCallback(TIMUserSigExpiredCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMUserSigExpiredCallback | The callback for ticket expiration. For more information, see [TIMUserSigExpiredCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timusersigexpiredcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

>User tickets may expire. If a user ticket expires, the callback set by this API will be invoked, and [TIMLogin](https://intl.cloud.tencent.com/document/product/1047/34390#timlogin) will return error code 70001. Developers can change the ticket based on the error code or ticket expiration callback.


## TIMSetOnAddFriendCallback

Sets the callback for adding friends.

**Prototype**

```c
TIM_DECL void TIMSetOnAddFriendCallback(TIMOnAddFriendCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMOnAddFriendCallback | The callback for adding friends. For more information, see [TIMOnAddFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timonaddfriendcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

> This callback is used for multi-terminal synchronization. For example, assume that the same IM SDK account has been logged in on devices A and B. When a friend is added on device A, the IM SDK for device B will receive a friend addition notification, and the IM SDK will notify the developer of the notification through this callback.


## TIMSetOnDeleteFriendCallback

Sets the callback for deleting friends.

**Prototype**

```c
TIM_DECL void TIMSetOnDeleteFriendCallback(TIMOnDeleteFriendCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMOnDeleteFriendCallback | The callback for deleting friends. For more information, see [TIMOnDeleteFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timondeletefriendcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

> This callback is used for multi-terminal synchronization. For example, assume that the same IM SDK account has been logged in on devices A and B. When a friend is deleted on device A, the IM SDK for device B will receive a friend deletion notification, and the IM SDK will notify the developer of the notification through this callback.


## TIMSetUpdateFriendProfileCallback

Sets the callback for updating friend profiles.

**Prototype**

```c
TIM_DECL void TIMSetUpdateFriendProfileCallback(TIMUpdateFriendProfileCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMUpdateFriendProfileCallback | The callback for updating friend profiles. For more information, see [TIMUpdateFriendProfileCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timupdatefriendprofilecallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

> This callback is used for multi-terminal synchronization. For example, assume that the same IM SDK account has been logged in on devices A and B. When a friend’s profile is updated on device A, the IM SDK for device B will receive a friend profile update notification, and the IM SDK will notify the developer of the notification through this callback.


## TIMSetFriendAddRequestCallback

Sets the callback for friend requests.

**Prototype**

```c
TIM_DECL void TIMSetFriendAddRequestCallback(TIMFriendAddRequestCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMFriendAddRequestCallback | The callback for friend requests. For more information, see [TIMFriendAddRequestCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timfriendaddrequestcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

> If the logged-in user has set that confirmation is required for friend requests and another user sends a friend request to this user, the logged-in user will receive the friend request callback, and the IM SDK will notify the developer through this callback. If the same account has been logged in on multiple terminals, each of these terminals will receive the callback.


## TIMSetLogCallback

Sets the callback for logs.

**Prototype**

```c
TIM_DECL void TIMSetLogCallback(TIMLogCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMLogCallback | The callback for logs. For more information, see [TIMLogCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timlogcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

> After the log monitoring callback is set, IM SDK internal logs will be returned to the callback set by this API. Developers can invoke the [TIMSetConfig](https://intl.cloud.tencent.com/document/product/1047/34388#timsetconfig) API to configure the log levels of logs to be returned to the callback.


## TIMSetMsgUpdateCallback

Sets the callback for message update notifications returned after messages are modified in the cloud.

**Prototype**

```c
TIM_DECL void TIMSetMsgUpdateCallback(TIMMsgUpdateCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMMsgUpdateCallback | The callback for message updating. For more information, see [TIMMsgUpdateCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timmsgupdatecallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without performing any processing. |

>
- After a message that you sent is modified on the server end, the IM SDK will notify you of this modification through this callback.
- You can intercept all IM messages on your server. For more information, see [Performing Callback Before Sending One-to-One Chat Messages](https://intl.cloud.tencent.com/document/product/1047/34364).
- After this callback is set, the IM server will notify your business server of each message sent by your users.
- The business server can modify the message (for example, filter out sensitive words). If the business server modifies the message, the IM SDK will notify you of this modification through this callback.


