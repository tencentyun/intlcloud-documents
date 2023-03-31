## Feature Description
This feature enables any participant in a conversation to modify a successfully sent message in the conversation. The message will be synced to all the participants in the conversation once modified successfully.

> ? This feature is supported only by the Enhanced edition on v6.2 or later.

## Modifying a Message
A conversation participant can call `modifyMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5464602189e6af536540e86e8bcbbe73) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7609c2dd8550e43b23d24069200d37cb)) to modify a sent message in the conversation.
The IM SDK allows any conversation participant to modify a message in the conversation. You can add more restrictions at the business layer, for example, only allowing the message sender to modify the message.

Currently, the following information of a message can be modified:
* `cloudCustomData` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html#a9335c9c326a2bfa8f4e6951cb9714e62) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html#a99a1c55f183244cc56588e9769dac4d0)) 
* `V2TIMTextElem` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTextElem.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMTextElem.html)) 
* `V2TIMCustomElem` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCustomElem.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMCustomElem.html))
* `V2TIMLocationElem` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMLocationElem.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMLocationElem.html))
* `V2TIMFaceElem` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFaceElem.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMFaceElem.html))

Sample code:
<dx-tabs>
::: Android
```java
// The original message object in the conversation is `originMessage`.
// Modify the `cloudCustomData` information of the message object
originMessage.setCloudCustomData("modify_cloud_custom_data".getBytes());
// If the message is a text message, modify the text message content
if (V2TIMMessage.V2TIM_ELEM_TYPE_TEXT == originMessage.getElemType()) {
  originMessage.getTextElem().setText("modify_text");
}
V2TIMManager.getMessageManager().modifyMessage(originMessage, new V2TIMCompleteCallback<V2TIMMessage>() {
  @Override
  public void onComplete(int code, String desc, V2TIMMessage message) {
    // After the message is modified, `message` is the modified message object.
  }
});
```
:::
::: iOS and macOS
```objectivec
// Original message object in the conversation
V2TIMMessage *originMessage; 
// Modify the `cloudCustomData` information of the message object
originMessage.cloudCustomData = [@"modify_cloud_custom_data" dataUsingEncoding:NSUTF8StringEncoding];
// If the message is a text message, modify the text message content
if (V2TIM_ELEM_TYPE_TEXT == originMessage.elemType) {
    originMessage.textElem.text = @"modify_text";
}
[[V2TIMManager sharedInstance] modifyMessage:originMessage completion:^(int code, NSString *desc, V2TIMMessage *msg) {
    // After the message is modified, `msg` is the modified message object.
}];
```
:::
</dx-tabs>

## Listening for a Message Modification Callback
Conversation participants call `addAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab)) to add the advanced message listener.

After a message in the conversation is modified, all the participants will receive the `onRecvMessageModified` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#ade079c0c996ee408abdc9cc83ab56e40) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html#a1fb56e509cecc32663ebd460c1de88cb)), which contains the modified message object.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMAdvancedMsgListener advancedMsgListener = new V2TIMAdvancedMsgListener() {
  // Notification of the message content modification
  @Override
  public void onRecvMessageModified(V2TIMMessage msg) {
      // `msg` is the modified message object.
  }
};
// Add a message listener
V2TIMManager.getMessageManager().addAdvancedMsgListener(advancedMsgListener);
```
:::
::: iOS and macOS
```objectivec
// Add a message listener
[[V2TIMManager sharedInstance] addAdvancedMsgListener:self];
/// Notification of the message content modification
- (void)onRecvMessageModified:(V2TIMMessage *)msg {
    // `msg` is the modified message object.
}
```
:::
</dx-tabs>
