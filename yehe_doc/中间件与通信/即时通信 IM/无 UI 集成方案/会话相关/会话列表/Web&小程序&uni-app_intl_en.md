## Overview

With conversation lists, users can easily locate target conversations after they log in to the application.

The conversation list feature includes getting the conversation list and listening for conversation list update events. The core data structure is [Conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html).

## Getting the Conversation List

Call the [getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList) API on the access side to get the conversation list.

### Getting the full conversation list
<dx-codeblock>
:::  js

// Get the full conversation list
let promise = tim.getConversationList();
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // This full conversation list will overwrite the original conversation list.
  const isSyncCompleted = imResponse.data.isSyncCompleted; // Whether synchronizing the conversation list from the cloud is completed
}).catch(function(imError){
  console.warn('getConversationList error:', imError); // Error information
});

:::
</dx-codeblock>

### Getting the list of specified conversations
<dx-codeblock>
:::  js

// Get the list of specified conversations
let promise = tim.getConversationList([conversationID1, conversationID2]);
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // List of specified conversations that already exist in the cache
}).catch(function(imError){
  console.warn('getConversationList error:', imError); // Error information
});

:::
</dx-codeblock>

### Getting all group conversations
<dx-codeblock>
:::  js

// Get all group conversations
let promise = tim.getConversationList({ type: TIM.TYPES.CONV_GROUP });
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // Conversation list
});

:::
</dx-codeblock>

### Getting all conversations that are marked as "favorite"
<dx-codeblock>
:::  js

// Obtain all conversations that are marked as "favorite"
let promise = tim.getConversationList({ markType: TIM.TYPES.CONV_MARK_TYPE_STAR });
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // Conversation list
});

:::
</dx-codeblock>

### Getting all conversations in a specified conversation group
<dx-codeblock>
:::  js

// Obtain all conversations in a specified conversation group
let promise = tim.getConversationList({ groupName: 'Suppliers' });
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // Conversation list
});

:::
</dx-codeblock>

## Listening for Conversation List Update Events

Listen for [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) events on the access side to get conversation list update notifications.

**Sample**

<dx-codeblock>
:::  js

let onConversationListUpdated = function(event) {
  console.log(event.data); // Array that stores Conversation instances
};
tim.on(TIM.EVENT.CONVERSATION_LIST_UPDATED, onConversationListUpdated);

:::
</dx-codeblock>
