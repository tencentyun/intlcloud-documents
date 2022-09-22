## Feature Description

Pinning a conversation to the top is to fix a one-to-one or group conversation at the top of the conversation list to facilitate search. The status of a conversation being pinned to the top will be stored on the server and synced to new devices.
After the API is called successfully, the conversations are re-sorted, and the SDK delivers the [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) event.

>! This feature is supported by v2.14.0 or later.

## Pinning/Unpinning a Conversation to/from the Top

**API**

<dx-codeblock>
:::  js

tim.pinConversation(options);

:::
</dx-codeblock>

The `options` parameter is of the `Object` type. It contains the following attribute values:

**Parameter**

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| conversationID     | String | Conversation ID. Valid values:<br/><li>C2C${userID} (for a one-to-one chat)</li><li>GROUP{groupID} (for a group chat)</li><li>@TIM#SYSTEM (for a system notification conversation)</li><li>GROUP${topicID} (for a topic). It is supported by v2.19.1 or later.</li> |
| isPinned           | Boolean | If it is `true`, the conversation is pinned to the top; if it is `false`, the conversation is unpinned from the top. |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Pin a conversation to the top. This feature is supported by v2.14.0 or later.
let promise = tim.pinConversation({ conversationID: 'C2CExample', isPinned: true });
promise.then(function(imResponse) {
  // Pinned the conversation to the top successfully
  const { conversationID } = imResponse.data; // ID of the conversation pinned to the top
}).catch(function(imError) {
  console.warn('pinConversation error:', imError); // Failed to pin the conversation to the top
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Unpin a conversation from the top. This feature is supported by v2.14.0 or later.
let promise = tim.pinConversation({ conversationID: 'C2CExample', isPinned: false });
promise.then(function(imResponse) {
  // Unpinned the conversation from the top successfully
  const { conversationID } = imResponse.data; // ID of the conversation unpinned from the top
}).catch(function(imError) {
  console.warn('pinConversation error:', imError); // Failed to unpin the conversation from the top
});

:::
</dx-codeblock>