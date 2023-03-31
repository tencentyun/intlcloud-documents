## Feature Description
You can set the message receiving option for a **one-to-one or group chat** to implement the notification muting feature.
The IM SDK supports the following three message receiving options as defined in `TIMReceiveMessageOpt`:

| Message Receiving Option                        | Feature Description                                          |
| ----------------------------------------------- | ------------------------------------------------------------ |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Receive     | Messages will be received when the user is online, and offline push notifications will be received when the user is offline. |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Receive | Messages will not be received no matter whether the user is online or offline. |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Notify  | Messages will be received when the user is online, and offline push notifications will not be received when the user is offline. |

Different `TIMReceiveMessageOpt` options can be used to implement group message notification muting:
**No messages will be received.**
After the message receiving option is set to `kTIMRecvMsgOpt_Not_Receive`, no one-to-one or group messages will be received, and the conversation list will not be updated.

**Messages will be received but will not be notified to the user, and a badge without the unread count will be displayed on the conversation list UI.**
1. The message receiving option is set to `kTIMRecvMsgOpt_Not_Notify`.
2. When the receiver receives a one-to-one or group message and needs to update the conversation list, it can get the unread count through the `total_unread_count` ([Details](https://comm.qq.com/im/doc/unity/en/callback/ConvTotalUnreadMessageCountChangedCallback.html)) in the `SetConvTotalUnreadMessageCountChangedCallback` callback for a change in the total unread count of a conversation.
3. The receiver displays a badge rather than the unread count when identifying the message receiving option as `kTIMRecvMsgOpt_Not_Notify` based on the `conv_recv_opt` ([Details](https://comm.qq.com/im/doc/unity/en/types/ConvAttributes/ConvInfo.html)) in `ConvInfo`.

> ? As this method requires the unread count feature, it applies only to work groups (Work) and public groups (Public). For more information on group types, see Group Overview.


## Setting the Message Receiving Option for a One-to-One Chat
Call the `MsgSetC2CReceiveMessageOpt` API ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSetC2CReceiveMessageOpt.html)) to set the message receiving option for a one-to-one chat.
You can use the `userIDList` parameter to specify up to 30 users at a time.

> ! This API can be called up to 5 times every second.

Sample code:


```c#
// Set not to receive messages no matter whether the user is online or offline
TIMResult res = TencentIMSDK.MsgSetC2CReceiveMessageOpt(user_id_list, TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Receive, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```


## Getting the Message Receiving Option for a One-to-One Chat
Call the `MsgGetC2CReceiveMessageOpt` API ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgGetC2CReceiveMessageOpt.html)) to get the message receiving option for a one-to-one chat.

Sample code:


```c#
TIMResult res = TencentIMSDK.MsgGetC2CReceiveMessageOpt(user_id_list, (int code, string desc, List<GetC2CRecvMsgOptResult> msg_opts, string user_data)=>{
 // Process the async logic
});
```



## Setting the Message Receiving Option for a Group Chat
Call the `MsgSetGroupReceiveMessageOpt` API ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSetGroupReceiveMessageOpt.html)) to set the message receiving option for a group chat.

Sample code:


```c#
TIMResult res = TencentIMSDK.MsgSetGroupReceiveMessageOpt(group_id, TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Receive, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```
