## Feature Description
If a message sender wants to know who has or has not read the message, the sender needs to enable the message read receipt feature.
After this feature is enabled, the sender can set whether a message requires a read receipt when sending the message; if yes, the sender will receive a receipt after the message is read by the receiver.

Read receipts are supported for both one-to-one and group messages in the same way.

> ?
> - To use this feature, you need to purchase the Ultimate edition.


## Message Read Receipt
### Specifying a group type for which to support message read receipts
Log in to the [IM console](https://console.cloud.tencent.com/im), select **Feature Configuration** > **Login and Message** > **Group Message Read Receipts**.

### Specifying that a message requires a read receipt (by the sender)

Sample code:


```c#
var message = new Message
{
  message_conv_id = conv_id,
  message_conv_type = TIMConvType.kTIMConv_Group,
  message_cloud_custom_str = "unity local custom data",
  message_elem_array = new List<Elem>{new Elem
  {
    elem_type = TIMElemType.kTIMElem_Text,
    text_elem_content = Input.text
  }},
  message_need_read_receipt = true,
};
StringBuilder messageId = new StringBuilder(128);
  TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, Message data, string user_data) => {
  // Process the callback logic
});
```


### Sending a message read receipt (by the receiver)
After receiving the message, the receiver determines whether the message requires a read receipt based on the `message_need_read_receipt` field in `Message` ([Details](https://comm.qq.com/im/doc/unity/en/types/MessageAttributes/Message.html#com_tencent_imsdk_unity_types_Message_message_need_read_receipt)). If yes, after the user reads the message, the receiver calls the `MsgSendMessageReadReceipts` API ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSendMessageReadReceipts.html)) to send a read receipt.

Sample code:


```c#
TIMResult res = TencentIMSDK.MsgSendMessageReadReceipts(msg_array, (int code, string desc, string user_data) => {
  // Process the callback logic
});
```


### Listening for a message read receipt notification (by the sender)
After the receiver sends a message read receipt, the sender can listen for a receipt notification through the `SetMsgReadedReceiptCallback` callback ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetMsgReadedReceiptCallback.html)) and update the UI based on the notification to display the message as, for example, "Read by two members".

Sample code:


```c#
TIMResult res = TencentIMSDK.SetMsgReadedReceiptCallback(msg_array, (List<MessageReceipt> message_receipt, string user_data) => {
  // Process the callback logic
});
```


### Pulling message read receipt information (by the sender)
After entering the message list, the sender pulls historical messages first, and then calls the `MsgGetMessageReadReceipts` API ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgGetMessageReadReceipts.html)) to pull the message read receipt information.


Sample code:


```c#
TIMResult res = TencentIMSDK.MsgGetMessageReadReceipts(msg_array, (int code, string desc, List<MessageReceipt> message_receipt, string user_data) => {
  // Process the callback logic
});
```


### Pulling the list of members who have or have not read a group message (by the sender)
To view the list of members who have or have not read a group message, the sender can call the `GetMsgGroupMessageReadMemberList` API ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/GetMsgGroupMessageReadMemberList.html)) to pull the member list by page.



```c#
TIMResult res = TencentIMSDK.MsgGetMessageReadReceipts(message, TIMGroupMessageReadMembersFilter.TIM_GROUP_MESSAGE_READ_MEMBERS_FILTER_READ, next_seq, 20, (List<GroupMemberInfo> json_group_member_array, ulong next_seq, bool is_finished, string user_data) => {
  // Process the callback logic
});
```
