## Feature Description
A targeted group message is a message sent to specified members in a group, which cannot be received by other group members.

> ?
> 1. This feature is supported only by the SDK for Unity on v1.7.7 or later.
> 2. To use this feature, you need to purchase the Ultimate edition.
> 3. The original message object used to create a targeted group message cannot be a group @ message.
> 4. The targeted group message feature is unavailable for communities (Community) and audio-video groups (AVChatRoom).
> 5. By default, targeted group messages are excluded from the unread count of a group conversation.

## Sending a Targeted Group Message
A targeted group message is a message sent to specified members in a group, which cannot be received by unspecified group members. It can be implemented in the following steps:
Call the `MsgSendMessage` API ([c#](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSendMessage.html)) to specify the list of group members to receive the message and send the message.

Sample code:


```c#
var message = new Message
{
   message_conv_id = conv_id,
   message_conv_type = TIMConvType.kTIMConv_Group,
   message_elem_array = new List<Elem>{new Elem
   {
     elem_type = TIMElemType.kTIMElem_Text,
     text_elem_content = Input.text
   }},
   message_target_group_member_array = userid_list, // Specify the list of `UserID` values of group members to receive the message
};
StringBuilder messageId = new StringBuilder(128);
TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_Group, message, messageId, (int code, string desc, string json_param, string user_data)=>{
 // Async message sending result
});
```


## Receiving a Targeted Group Message
By default, targeted group messages are excluded from the unread count of a group conversation.
A targeted group message can be received in the same way as an ordinary message. For detailed directions, see Receiving Message.




