## Overview
A targeted group message is a message sent to specified members in a group, which cannot be received by other group members.

> ?
> 1. This feature is available only in v2.23.1 or later.
> 2. To use this feature, you need to purchase the Ultimate edition as instructed in [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
> 3. When creating a group @ message, you cannot specify the list of group members to receive the message (`receiverList`).
> 4. The targeted group message feature is not available for community and audio-video (AVChatRoom) groups.
> 5. By default, targeted group messages are excluded from the unread count of the group conversation.

## Sending a Targeted Group Message
A targeted group message is a message sent to specified members in a group, which cannot be received by other group members through the [TIM.EVENT.MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED) event.


To send a targeted group message to specified members in a group, follow the instructions below:
- Call the `createXxxMessage` API (here, `Xxx` indicates the message type) to create a message (specify the message recipients via `receiverList`).
- Call the `sendMessage` API to send the message.

## Example
<dx-codeblock>
:::  js

// Create a targeted group message
let message = tim.createTextMessage({
  to: 'test',
  conversationType: TIM.TYPES.CONV_GROUP,
  payload: {
    text: 'Hello world!'
  },
  // The targeted group message feature is supported by v2.23.1 or later. To use it, purchase the Ultimate edition package and specify message recipients via `receiverList` when creating a message.
  // Note: Targeted group messages are excluded from the unread count of a conversation. `receiverList` supports up to 50 recipients.
  receiverList: ['user0', 'user1']
});

// Send the message
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Message sent successfully
  console.log(imResponse);
}).catch(function(imError){
  // The message failed to be sent
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

## Receiving a Targeted Group Message
By default, targeted group messages are excluded from the unread count of a group conversation.
A targeted group message can be received in the same way as an ordinary message. For detailed directions, see [Receiving Message](https://intl.cloud.tencent.com/document/product/1047/47996).
