## Feature Description

The SDK supports message pull by page, sequence, or time range.

Historical messages stored in the cloud are subject to the following time limits:
* Free edition: The free storage period is 7 days and cannot be extended.
* Pro edition: The free storage period is 7 days and can be extended.
* Ultimate edition: The free storage period is 30 days and can be extended.

> ? 
> * Extending the storage period of historical messages is a value-added service. You can log in to the [IM console](https://console.cloud.tencent.com/im) to modify the relevant configuration. For billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). 
> * Rich media messages (such as images, files, and audios) have the same storage periods as historical messages.

## Pulling a Message List

### Pulling the message list of a specified conversation by page

This API is used to pull the list of messages in a specified conversation by page. It needs to be called when the message list is rendered for the first time after the user enters the conversation, or when the user pulls down the list to view more messages.

>! This API can be used to pull historical messages.

**API**

<dx-codeblock>
:::  js

tim.getMessageList(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type                | Description                                                  |
| ---------------- | ------------------- | ------------------------------------------------------------ |
| conversationID   | String              | Conversation ID, which consists of:<br/><li>C2C${userID} (for one-to-one chats)</li><li>GROUP${groupID} (for group chats)</li><li>GROUP${topicID} (topic). It is supported by v2.19.1 or later.</li><li>@TIM#SYSTEM (system notification conversation)</li> |
| nextReqMessageID | String \| undefined | Message ID used for the subsequent paged pull. Leave this field empty for the first pull and enter its the value returned by the `getMessageList` API for the subsequent pull. |
| count            | Number \| undefined | Number of messages to be pulled. It defaults to `15`, which is also the maximum value, indicating that up to 15 messages can be pulled and returned at a time. |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Pull the message list for the first time when a conversation is opened
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  const nextReqMessageID = imResponse.data.nextReqMessageID; // This parameter must be passed in for the next pull by page.
  const isCompleted = imResponse.data.isCompleted; // It indicates whether all messages have been pulled.
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Pull down the message list to view more messages
let promise = tim.getMessageList({conversationID: 'C2Ctest', nextReqMessageID, count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  const nextReqMessageID = imResponse.data.nextReqMessageID; // This parameter must be passed in for the next pull by page.
  const isCompleted = imResponse.data.isCompleted; // It indicates whether all messages have been pulled.
});

:::
</dx-codeblock>

### Pulling a message list by specified sequence or time range

This API is used to pull a message list by specified sequence or time range.

>! This API is supported by v2.20.0 or later.

**API**

<dx-codeblock>
:::  js

tim.getMessageListHopping(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name           | Type                | Description                                                  |
| -------------- | ------------------- | ------------------------------------------------------------ |
| conversationID | String              | Conversation ID, which consists of:<br/><li>C2C${userID} (for one-to-one chats)</li><li>GROUP${groupID} (for group chats)</li><li>GROUP${topicID} (topic). It is supported by v2.19.1 or later.</li> |
| sequence       | Number \| undefined | `sequence` of the message starting from which to pull roaming group messages |
| time           | Number \| undefined | Server time of the message, starting from which to pull roaming one-to-one messages |
| direction      | Number              | Message pull direction, which defaults to `0`.<br/><li>0: pull in reverse chronological order  to get older messages;</li><li>1: pull in chronological order to get recent messages</li> |
| count          | Number \| undefined | Number of messages to be pulled. It defaults to `15`, which is also the maximum value, indicating that up to 15 messages can be pulled and returned at a time. |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Pull roaming group messages by sequence. `direction`: 0: pull in reverse chronological order to get older messages; 1: pull in chronological order to get recent messages
let promise = tim.getMessageListHopping({conversationID: 'GROUPtest', sequence: xxx, count: 15, direction: 0});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Pull roaming one-to-one messages by sequence. `direction`: 0: pull in reverse chronological order to get older messages; 1: pull in chronological order to get recent messages
let promise = tim.getMessageListHopping({conversationID: 'C2Ctest', time: xxx, count: 15, direction: 0});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
});

:::
</dx-codeblock>
