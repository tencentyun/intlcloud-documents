## Feature Description

This feature is used to recall a one-to-one or group message. After the message is recalled successfully, the value of its `isRevoked` attribute will be `true`.

>!
>- This feature is supported by v2.4.0 or later.
>- The time limit for message recall is two minutes by default. You can log in to [the IM console](https://console.cloud.tencent.com/im-detail/login-message) to change this limit.
>- Call the [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) API to pull a recalled message from roaming one-to-one or group messages. The receiver needs to properly display the recalled message based on the `isRevoked` attribute of the message object, for example, as "The other party recalled a message" in a one-to-one conversation or as "XXX recalled a message" in a group conversation.
>- You can recall a one-to-one message as instructed in [Recalling One-to-One Messages](https://intl.cloud.tencent.com/document/product/1047/35015) or a group message as instructed in [Recalling Group Messages](https://intl.cloud.tencent.com/document/product/1047/34965).


**API**

<dx-codeblock>
:::  js

tim.revokeMessage(message);

:::
</dx-codeblock>

**Parameter**

| Name    | Type    | Description      |
| ------- | ------- | ---------------- |
| message | Message | Message instance |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Recall a message
let promise = tim.revokeMessage(message);
promise.then(function(imResponse) {
  // Message recalled successfully
}).catch(function(imError) {
  // Failed to recall the message
  console.warn('revokeMessage error:', imError);
});

:::
</dx-codeblock>


<dx-codeblock>
:::  js

// Received a message recall notification
tim.on(TIM.EVENT.MESSAGE_REVOKED, function(event) {
  // event.name - TIM.EVENT.MESSAGE_REVOKED
  // event.data - An array that stores Message objects - [Message] - The `isRevoked` attribute value of each Message object is `true`.
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Encountered the recalled message while getting the list of messages in the conversation
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  messageList.forEach(function(message) {
    if (message.isRevoked) {
      // Process the recalled message
    } else {
      // Process ordinary messages
    }
  });
});

:::
</dx-codeblock>