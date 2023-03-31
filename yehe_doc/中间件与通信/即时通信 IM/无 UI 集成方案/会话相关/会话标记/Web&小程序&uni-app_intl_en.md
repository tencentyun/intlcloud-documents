## Feature Description
In some cases, you may need to mark a conversation, for example, as "favorite", "collapsed", "hidden", or "unread", which can be implemented through the following API.
> ?
> - To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577).
> - This feature is available only in v2.22.0 or later.

## Conversation Mark

### Marking a conversation
Call the [markConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markConversation) API to mark or unmark a conversation.
> ! When a user marks a conversation, the SDK records only the mark value and will not change the underlying logic of the conversation. For example, if a conversation is marked as [CONV_MARK_TYPE_UNREAD](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.CONV_MARK_TYPE_UNREAD), the unread count at the underlying layer will not change.

**API**

<dx-codeblock>
:::  js

tim.markConversation(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type    | Description                   |
| ------------------ | ------- | ----------------------------- |
| conversationIDList | String  | List of conversation IDs      |
| markType           | String  | Conversation mark type        |
| enableMark         | Boolean | `true`: Mark. `false`: Unmark |

> ? The SDK provides four default marks ("favorite", "collapsed", "hidden", and "unread"). If they cannot meet your requirements, you can customize extended marks, which must meet the following conditions:
1. The value of an extended mark cannot be the same as that of an existing one.
2. The value of an extended mark must be `Math.power(2, n)` (32 ≤ n < 64, indicating that `n` must be equal to or greater than 32 and less than 64). For example, `Math.power(2, 32)` indicates "Online on an iPhone".

**Response**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Mark a conversation as "favorite"
let promise = tim.markConversation({
  conversationIDList: ['GROUPtest', 'C2Cexample'],
  markType: TIM.TYPES.CONV_MARK_TYPE_STAR,
  enableMark: true
});
promise.then(function(imResponse) {
  // Marked the conversation as "favorite" successfully
  const { successConversationIDList, failureConversationIDList } = imResponse.data;
  // successConversationIDList - List of conversations that were marked successfully
  // Get the conversation list
  const conversationList = tim.getConversationList(successConversationIDList);

  // failureConversationIDList - List of conversations that failed to be marked as "favorite"
  failureConversationIDList.forEach((item) => {
    const { conversationID, code, message } = item;
  });
}).catch(function(imError){
  console.warn('markConversation error:', imError);
});

:::
</dx-codeblock>

### Listening for the notification of a conversation mark change
After a conversation is marked or unmarked, the `markList` field in [Conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html) will change. You can listen for such a change notification through the [CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) event.

**Sample**

<dx-codeblock>
:::  js

let onConversationListUpdated = function(event) {
  console.log(event.data); // Array that stores Conversation instances
};
tim.on(TIM.EVENT.CONVERSATION_LIST_UPDATED, onConversationListUpdated);

:::
</dx-codeblock>

### Pulling a specified marked conversation
Call the [getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList) API to pull a specified marked conversation.

**Sample**

<dx-codeblock>
:::  js

// Obtain all conversations that are marked as "favorite"
let promise = tim.getConversationList({ markType: TIM.TYPES.CONV_MARK_TYPE_STAR });
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // Conversation list
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Obtain all one-to-one conversations that are marked as "collapsed"
let promise = tim.getConversationList({
  markType: TIM.TYPES.CONV_MARK_TYPE_FOLD,
  type: TIM.TYPES.CONV_C2C
});
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // Conversation list
});

:::
</dx-codeblock>
