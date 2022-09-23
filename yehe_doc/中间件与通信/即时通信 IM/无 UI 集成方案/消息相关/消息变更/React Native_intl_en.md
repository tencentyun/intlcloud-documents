## Feature Description

This feature enables any member in a conversation to modify a successfully sent message in the conversation. The message will be synced to all the members in the conversation once modified successfully.

## Modifying a Message

A conversation participant can call the `modifyMessage` API ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#modifyMessage)) to modify a message in the conversation.
The IM SDK allows any conversation participant to modify a message in the conversation. You can add more restrictions at the business layer, for example, only allowing the message sender to modify the message.

Currently, the following information of a message can be modified:
1. `localCustomData` ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimMessage.html#localCustomData))
2. `localCustomInt` ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimMessage.html#localCustomInt))
3. `cloudCustomData` ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimMessage.html#cloudCustomData))Ï
4. `V2TIMTextElem` ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimTextElem.html))
5. `V2TIMCustomElem` ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimCustomElem.html))

Below is the sample code:

```javascript
// Find the message to be modified
const msgListRes = await TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .findMessages(["msgid"]);
// Edit the message
if (msgListRes.code == 0) {
  const messageList = msgListRes.data;
  if (messageList.isNotEmpty) {
    const originMessage = messageList[0];
    originMessage.cloudCustomData = "change data";
    const modify = await TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .modifyMessage(originMessage);
    if (modify.code == 0) {
      if (modify.data.code == 0) {
        // Modified successfully
      }
    }
  }
}
```

## Listening for a Message Modification Callback

Conversation participants call `addAdvancedMsgListener` ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#addAdvancedMsgListener)) to add the advanced message listener.

After a message in the conversation is modified, all the participants will receive the `onRecvMessageModified` callback ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimAdvancedMsgListener.html#onRecvMessageModified)), which contains the modified message object.

Below is the sample code:

```javascript
onRecvMessageModified: (message) => {
  // `msg` is the modified message object.
};
```


