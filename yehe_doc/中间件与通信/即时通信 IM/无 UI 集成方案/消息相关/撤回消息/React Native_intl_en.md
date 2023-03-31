## Feature Description

- The method for recalling a message is in the core class `TencentImSDKPlugin.v2TIMManager.getMessageManager()`.
- The receiver listens for a message recall notification through `addAdvancedMsgListener`.

## Recalling a Message

The sender can recall a successfully sent message.

By default, the sender can recall a message sent within two minutes. You can change the time limit for message recall as instructed in [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

Message recall can be implemented through the receiver UI code: When a message is recalled, the receiver will receive the `onRecvMessageRevoked` notification which contains the `msgID` of the recalled message. You can identify the recalled message at the UI layer based on the `msgID` and change the bubble for the message to the "Message recalled" status.

### Recalling a message (by the sender)

Call `revokeMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/revokeMessage.html)) to recall a message.

Below is the sample code:

```javascript
const revokeMessage = await TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .revokeMessage("msgID");
```

### Noticing a message recall (by the receiver)

1. Call `addAdvancedMsgListener` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/addAdvancedMsgListener.html)) to set the advanced message listener.
2. Receive a message recall notification through `onRecvMessageRevoked` ([Details](https://comm.qq.com/im/doc/RN/en/Callback/OnRecvMessageRevoked.html)).

Below is the sample code:

```javascript
onRecvMessageRevoked: (messageid) => {
  // Process the recalled message among locally maintained messages
};
```
