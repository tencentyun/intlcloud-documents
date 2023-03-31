## Feature Description

In certain cases, you may want a message to be received by the receiver only when online; that is, the receiver won't notice the message when offline. You only need to set `onlineUserOnly` to `true` when calling `sendMessage`. A message sent in this way differs from a general one in that:

1. It cannot be stored offline; that is, it cannot be received if the receiver is offline.
2. It cannot be roamed across devices; that is, if it is received on a device, it cannot be received on another, whether it is read or not.
3. It cannot be stored locally; that is, it cannot be pulled from local or cloud historical messages.

## Sample

### Implementing the feature of "The other party is typing..."

In one-to-one chats, you can call the `sendMessage` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/sendMessage.html)) to send the prompt "I am typing...". After receiving the message, the receiver can display "The other party is typing..." on the UI.

Below is the sample code:

```javascript
const data = 'Typing...';
const createCustomMessageRes =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createCustomMessage(data);
  TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: createCustomMessageRes.data.id, receiver: "", groupID: "",onlineUserOnly: true);
```
