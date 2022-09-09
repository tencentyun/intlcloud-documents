## Feature Description
A targeted group message is a message sent to specified members in a group, which cannot be received by other group members.

> ?
> 1. This feature is supported only by the SDK of the Enhanced edition on v6.0.1975 or later.
> 2. To use this feature, you need to purchase the Ultimate edition as instructed in [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
> 3. The original message object used to create a targeted group message cannot be a group @ message.
> 4. The targeted group message feature is unavailable for communities (Community) and audio-video groups (AVChatRoom).
> 5. By default, targeted group messages are excluded from the unread count of a group conversation.

## Sending a Targeted Group Message
A targeted group message is a message sent to specified members in a group, which cannot be received by unspecified group members. It can be implemented in the following steps:
1. Call the `createXXXMessage` API (here, `XXX` indicates the message type) to create an original message object `V2TIMMessage`.
2. Call the `createTargetedGroupMessage` API ([Android](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a4def1515746b2840e4b82047a53b91a2) / [iOS and macOS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a8bddd2f566a53362b4da5448fdd18fbc)) to create a targeted message object `V2TIMMessage` based on the original message object and specify the list of group members to receive the message.
3. Call the `sendMessage` API to send the targeted message.

Sample code:
<dx-tabs>
::: Android
```java
// Create an original message object
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage("This is a targeted group message.");
// Create a targeted group message object and specify the receivers "vinson" and "denny".
List<String> targetGroupMemberList = new ArrayList<>();
targetGroupMemberList.add("vinson");
targetGroupMemberList.add("denny");
V2TIMMessage targetGroupMessage = V2TIMManager.getMessageManager().createTargetedGroupMessage(v2TIMMessage, targetGroupMemberList);

// Send the targeted group message in the group `groupA`
V2TIMManager.getMessageManager().sendMessage(targetGroupMessage, null, "groupA",  V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, null, new V2TIMSendCallback<V2TIMMessage>() {
  @Override
  public void onError(int code, String desc) {
  	// Failed to send the message
  }
  @Override
  public void onSuccess(V2TIMMessage v2TIMMessage) {
  	// Message sent successfully
  }
  @Override
  public void onProgress(int progress) {

  }
});
```
:::
::: iOS and macOS
```objectivec
// Create an original message object
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"This is a targeted group message."];

// Create a targeted group message object and specify the receivers "vinson" and "denny".
NSMutableArray *receiverList = [NSMutableArray array];
[receiverList addObject:@"vinson"];
[receiverList addObject:@"denny"];
V2TIMMessage *targetGroupMessage = [V2TIMManager.sharedInstance createTargetedGroupMessage:message receiverList:receiverList];

// Send the targeted message in the group `groupA`
[[V2TIMManager sharedInstance] sendMessage:targetGroupMessage receiver:nil groupID:@"groupA"
priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:NO offlinePushInfo:nil progress:^(uint32_t progress) {
} succ:^{
    // Message sent successfully
} fail:^(int code, NSString *msg) {
    // Failed to send the message
}];
```
:::
</dx-tabs>

## Receiving a Targeted Group Message
By default, targeted group messages are excluded from the unread count of a group conversation.
A targeted group message can be received in the same way as an ordinary message. For detailed directions, see [Receiving Message](https://intl.cloud.tencent.com/document/product/1047/47995).


