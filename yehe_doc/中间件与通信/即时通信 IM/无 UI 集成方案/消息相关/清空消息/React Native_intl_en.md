## Feature Description

One-to-one messages and group messages can be cleared.
When messages in a conversation are cleared, all the messages in the conversation will be cleared both **locally and from the cloud**, but the conversation itself will not be deleted.

> ?**Do not** use this API if you do not want to clear messages from the cloud.

If the last message is deleted, the `lastMessage` in the conversation will become the last but one message.

### Clearing one-to-one messages

Call `clearC2CHistoryMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/clearC2CHistoryMessage.html)) to clear one-to-one messages.

Below is the sample code:

```javascript
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .clearC2CHistoryMessage("userid");
```

### Clearing group messages

Call `clearGroupHistoryMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/clearGroupHistoryMessage.html)) to clear group messages.

Below is the sample code:

```javascript
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .clearGroupHistoryMessage("groupID");
```
