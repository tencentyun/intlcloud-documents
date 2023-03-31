## Feature Description

`findMessages` can be called to query a local message by `messageID`.

1. Only local messages can be queried, for example, received messages or historical messages pulled after the API is called.
2. Audio-video group (AVChatRoom) messages cannot be queried, as they are not saved locally.

## Querying a Local Message

Call the `findMessages` API ([Details](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#findMessages)) to query a local message.

Below is the sample code:

```javascript
// Query a message by message ID
const msgListRes = await TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .findMessages(["msgid"]);
```
