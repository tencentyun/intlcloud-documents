## Feature Description
In certain cases, you might want a message to be received by the receiver only when online; that is, the receiver won't notice the message when offline. You only need to set `message_is_online_msg` to `true` when calling `MsgSendMessage`. A message sent in this way differs from a general one in that:

1. It cannot be stored offline; that is, it cannot be received if the receiver is offline.
2. It cannot be roamed across devices; that is, if it is received on a device, it cannot be received on another, whether it is read or not.
3. It cannot be stored locally; that is, it cannot be pulled from local or cloud historical messages.

## Sample

### Implementing the feature of "The other party is typing..."

In one-to-one chats, you can call the `MsgSendMessage` API ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSendMessage.html)) to send the prompt "Typing...". After receiving the prompt message, the receiver can display "The other party is typing..." on the UI.

Sample code:


```c#
var message = new Message
{
   message_conv_id = conv_id,
   message_conv_type = TIMConvType.kTIMConv_C2C,
   message_elem_array = new List<Elem>{new Elem
   {
     elem_type = TIMElemType.kTIMElem_Custom,
     custom_elem_data = "Typing..."
   }},
   message_is_online_msg = true
};
 StringBuilder messageId = new StringBuilder(128);
 TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc, Message data, string user_data) => {
  // Process the callback logic
 });
```
