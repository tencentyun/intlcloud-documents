## Feature Description
- The method for recalling a message is `MsgRevoke` ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgRevoke.html)).
- The receiver listens for a message recall notification through `SetMsgRevokeCallback` ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetMsgRevokeCallback.html)).

## Recalling a Message
The sender can recall a successfully sent message.

By default, the sender can recall a message sent within two minutes. You can change the time limit for message recall as instructed in [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

Message recall can be implemented through the receiver UI code: When a message is recalled, the receiver will receive the `MsgRevokeCallback` notification which contains the `msgID` of the recalled message. You can identify the recalled message at the UI layer based on the `msgID` and change the bubble for the message to the "Message recalled" status.

### Recalling a message (by the sender)
The sender calls `MsgRevoke` ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgRevoke.html)) to recall a message.

Sample code:


```c#
    Message message = new Message(); // Here, the message can be an instance returned by another API, such as the message list API.

    TIMResult res = TencentIMSDK.MsgRevoke(conv_id, TIMConvType.kTIMConv_C2C, message, (int code, string desc, string user_data) => {
      // Process the callback logic
    });
```


### Noticing a message recall (by the receiver)
- The receiver receives a message recall notification through `SetMsgRevokeCallback` ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/SetMsgRevokeCallback.html)).

Sample code:


```c#
TencentIMSDK.SetMsgRevokeCallback((List<MsgLocator> msg_locator, string user_data) => {
      // Process the recalled message among locally maintained messages
});
```
