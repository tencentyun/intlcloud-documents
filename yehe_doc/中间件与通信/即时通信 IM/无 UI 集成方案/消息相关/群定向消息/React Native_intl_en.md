## Feature Description

A targeted group message is a message sent to specified members in a group, which cannot be received by other group members.

> ?
>
> 1. To use this feature, you need to purchase the Ultimate edition.
> 2. The original message object used to create a targeted group message cannot be a group @ message.
> 3. The targeted group message feature is unavailable for communities (Community) and audio-video groups (AVChatRoom).
> 4. By default, targeted group messages are excluded from the unread count of a group conversation.

## Sending a Targeted Group Message

A targeted group message is a message sent to specified members in a group, which cannot be received by unspecified group members. It can be implemented in the following steps:

1. Call the `createXXXMessage` API (here, `XXX` indicates the message type) to create an original message object `V2TIMMessage`.
2. Call the `createTargetedGroupMessage` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/createTargetedGroupMessage.html)) to create a targeted message object `V2TimMessage` based on the original message object and specify the list of group members to receive the message.
3. Call the `sendMessage` API to send the targeted message.

Below is the sample code:

```javascript
 // Create a message first
  const target = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextMessage("");
  // Get the ID for sending a message
  const id = target.data.id;
  // Create a targeted message
  const groupTarget = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTargetedGroupMessage(id, ['user1','user2'],);
  // Send the message
  TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: groupTarget.data.id, receiver: "", groupID: "groupID");
```

## Receiving a Targeted Group Message

By default, targeted group messages are excluded from the unread count of a group conversation.
A targeted group message can be received in the same way as an ordinary message. For detailed directions, see Receiving Message.
