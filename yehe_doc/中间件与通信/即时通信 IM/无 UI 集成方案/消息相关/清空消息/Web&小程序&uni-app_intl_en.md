
## Overview

When messages in a conversation are cleared, all the messages in the conversation will be cleared both locally and from the cloud, but the conversation itself will not be deleted.

> ?
> - Before using this API, upgrade your SDK to v2.25.0 or later.
> - When messages in a conversation are cleared, `unreadCount` will be set to `0`, and the content of `lastMessage` will be cleared as well.
> - This API cannot be used to clear messages in a topic.
> - To delete a conversation when clearing messages in the conversation, use the [deleteConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversation) API.


## Clearing Messages

**API**

<dx-codeblock>
:::  js

tim.clearHistoryMessage(conversationID);

:::
</dx-codeblock>

The `conversationID` parameter is described as follows:

**Parameters**

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| conversationID  | String | Conversation ID, in the format of:<br/><li>C2C${userID} (for one-to-one chats)</li><li>GROUP{groupID} (for group chats)</li>|

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Clear one-to-one messages locally and from the cloud
let promise = tim.clearHistoryMessage('C2CExample');
promise.then(function(imResponse) {
  // Messages cleared successfully
}).catch(function(imError){
  console.warn('clearHistoryMessage error:', imError); // Message clearing failure information
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Clear group messages locally and from the cloud
let promise = tim.clearHistoryMessage('GROUPExample');
promise.then(function(imResponse) {
  // Messages cleared successfully
}).catch(function(imError){
  console.warn('clearHistoryMessage error:', imError); // Message clearing failure information
});

:::
</dx-codeblock>
