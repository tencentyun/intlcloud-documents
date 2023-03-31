## Overview
This feature enables any member in a conversation to modify a successfully sent message in the conversation. The message will be synced to all the members in the conversation once modified successfully.

> ? This feature is supported only by the SDK for Flutter on v4.0.0 or later.

## Modifying a Message
A conversation participant can call the `modifyMessage` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/modifyMessage.html)) to modify a sent message in the conversation.
The Chat SDK allows any conversation participant to modify a message in the conversation. You can add more restrictions at the business layer, for example, only allowing the message sender to modify the message.

Currently, the following information of a message can be modified:
- `localCustomData` ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Message/V2TimMessage.html#localcustomdata))
- `localCustomInt` ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Message/V2TimMessage.html#localcustomint))
- `cloudCustomData` ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Message/V2TimMessage.html#cloudcustomdata))
- `V2TIMTextElem` ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Message/V2TimMessage.html#textelem))
- `V2TIMCustomElem` ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Message/V2TimMessage.html#customelem))

Sample code:


```dart
// Find the message to be modified
V2TimValueCallback<List<V2TimMessage>> msgListRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().findMessages(messageIDList: ['msgid']);
// Edit the message
  if(msgListRes.code == 0){
    List<V2TimMessage> messageList = msgListRes.data;
    if(messageList.isNotEmpty){
      V2TimMessage originMessage = messageList[0];
      originMessage.cloudCustomData = "change data";
     V2TimValueCallback<V2TimMessageChangeInfo> modify = await TencentImSDKPlugin.v2TIMManager.getMessageManager().modifyMessage(message: originMessage);
     if(modify.code == 0){
       if(modify.data.code ==0){
         // Modified successfully
       }
     }
    }
  }
```


## Listening for a Message Modification Callback
Conversation participants call `addAdvancedMsgListener` ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/addAdvancedMsgListener.html)) to add the advanced message listener.

After a message in the conversation is modified, all the participants will receive the `onRecvMessageModified` callback ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvMessageModified.html)), which contains the modified message object.

Sample code:


```java
onRecvMessageModified: (V2TimMessage message) {
      // `msg` is the modified message object
},
```
