## Overview

Pinning a conversation to the top is to fix a one-to-one or group conversation at the top of the conversation list to facilitate search. The status of a conversation being pinned to the top will be stored on the server and synced to new devices.
After this API is called successfully, the conversation list will be sorted again, and the SDK will distribute the [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) event.

>! This feature is supported only by the SDK on v2.14.0 or later. The maximum number of conversations that can be pinned to the top is 50, and this limit cannot be increased.

## Pinning/Unpinning a Conversation to/from the Top

**API**

<dx-codeblock>
:::  js

tim.pinConversation(options);

:::
</dx-codeblock>

The `options` parameter is of the `Object` type. It contains the following attribute values:

**Parameters**

| Name           | Type    | Description                                                  |
| -------------- | ------- | ------------------------------------------------------------ |
| conversationID | String  | Conversation ID, which consists of:<br/><li>C2C${userID} (for one-to-one chats)</li><li>GROUP{groupID} (for group chats)</li><li>@TIM#SYSTEM (system notification conversation)</li><li>GROUP${topicID} (topic). It is supported by v2.19.1 or later.</li> |
| isPinned       | Boolean | If it is `true`, the conversation is pinned to the top; if it is `false`, the conversation is unpinned from the top. |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Pin a conversation to top. Supported from v2.14.0.
let promise = tim.pinConversation({ conversationID: 'C2CExample', isPinned: true });
promise.then(function(imResponse) {
  // The conversation is pinned to top successfully.
  const { conversationID } = imResponse.data; // ID of the conversation pinned to top
}).catch(function(imError){
  console.warn('pinConversation error:', imError); // Error information
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Unpin a conversation from top. Supported from v2.14.0.
let promise = tim.pinConversation({ conversationID: 'C2CExample', isPinned: false });
promise.then(function(imResponse) {
  // The conversation is unpinned from top successfully.
  const { conversationID } = imResponse.data; // ID of the conversation unpinned from top
}).catch(function(imError){
  console.warn('pinConversation error:', imError); // Error information
});

:::
</dx-codeblock>
