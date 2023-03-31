## Overview
This feature enables any member in a conversation to modify a successfully sent message in the conversation. The message will be synced to all the members in the conversation once modified successfully.

> ? This feature is supported only on native SDK 6.2.2363 or later.

## Modifying a Message
A conversation participant can call the `MsgModifyMessage` API ([details](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgModifyMessage.html)) to modify a sent message in the conversation.
The Chat SDK allows any conversation participant to modify a message in the conversation. You can add more restrictions at the business layer, for example, only allowing the message sender to modify the message.

Currently, the following information of a message can be modified:
- `message_custom_str` ([Details](https://comm.qq.com/im/doc/unity/zh/types/MessageAttributes/Message.html#messagecloudcustomstr))
- `message_custom_int` ([Details](https://comm.qq.com/im/doc/unity/zh/types/MessageAttributes/Message.html#messagecloudcustomstr))
- `message_cloud_custom_str` ([Details](https://comm.qq.com/im/doc/unity/zh/types/MessageAttributes/Message.html#messagecloudcustomstr))
- `kTIMElem_Text` ([Details](https://comm.qq.com/im/doc/unity/zh/enums/TIMElemType.html))
- `kTIMElem_Custom` ([Details](https://comm.qq.com/im/doc/unity/zh/enums/TIMElemType.html))

Sample code:


```c#
originMessage.message_cloud_custom_str = "change data";
TIMResult res = TencentIMSDK.MsgModifyMessage(originMessage, (int code, string desc, string json_param, string user_data)=>{
 // Async result of the message modification
});
```


## Listening for a Message Modification Callback

If you have added an event listener for message modification callbacks via the `SetMsgUpdateCallback` API, when a message in a conversation is modified, all participants of the conversation will receive the `MsgUpdateCallback` ([details](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetMsgUpdateCallback.html)) callback, which contains the modified message objects.

Sample code:


```c#
TencentIMSDK.SetMsgUpdateCallback((List<Message> message_list, string user_data) => {
  // `message_list` is the list of modified message objects.
});
```
