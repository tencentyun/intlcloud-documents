## Feature Description
This feature enables any member in a conversation to modify a successfully sent message in the conversation. The message will be synced to all the members in the conversation once modified successfully.

> ? This feature is supported only by the SDK for Flutter on v4.0.0 or later.

## Modifying a Message
A conversation participant can call the `modifyMessage` API ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/modifyMessage.html)) to modify a sent message in the conversation.
The IM SDK allows any conversation participant to modify a message in the conversation. You can add more restrictions at the business layer, for example, only allowing the message sender to modify the message.

Currently, the following information of a message can be modified:
1. `localCustomData` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_message/V2TimMessage/localCustomData.html)) 
2. `localCustomInt` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_message/V2TimMessage/localCustomInt.html)) 
3. `cloudCustomData` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_message/V2TimMessage/cloudCustomData.html)) 
4. `V2TIMTextElem` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_text_elem/V2TimTextElem-class.html)) 
5. `V2TIMCustomElem` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_custom_elem/V2TimCustomElem-class.html))

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
Conversation participants call `addAdvancedMsgListener` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/addAdvancedMsgListener.html)) to add the advanced message listener.

After a message in the conversation is modified, all the participants will receive the `onRecvMessageModified` callback ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_callbacks/OnRecvMessageModified.html)), which contains the modified message object.

Sample code:


```java
onRecvMessageModified: (V2TimMessage message) {
      // `msg` is the modified message object.
},
```



