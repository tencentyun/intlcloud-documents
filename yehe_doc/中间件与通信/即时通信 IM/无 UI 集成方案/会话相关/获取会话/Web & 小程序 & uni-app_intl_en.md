## Feature Description

The IM SDK provides an API for getting conversations, which can be used to get the [Conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html) object information of one or multiple specified conversations.

## Getting the Conversation List

>!
>- The profile in the conversation list obtained through this API is incomplete. It contains only the information which is sufficient to render the conversation list, such as profile photo and nickname. To query the detailed conversation profile, see [getConversationProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationProfile).
>- By default, the client can pull 100 recent conversations from the cloud. If you upgrade  to the Ultimate edition, up to 500 recent conversations can be pulled from the cloud.
>- The retention period of a conversation is the same as that of the last message, which is seven days by default.
>- Starting from v2.15.0, multiple specified conversations can be obtained.

**API**

<dx-codeblock>
:::  js

tim.getConversationList(options);

:::
</dx-codeblock>

**Parameter**

| Name    | Type               | Description                                                  |
| ------- | ------------------ | ------------------------------------------------------------ |
| options | undefined \| Array | Parameter option.<br/><li>If no value is passed in, it indicates to get all the conversations.</li><li>If a non-empty array parameter is passed in, it indicates to get multiple specified conversations.</li> |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Get the list of all the conversations
let promise = tim.getConversationList();
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // The list of all the conversations, which is used to overwrite the original conversation list.
}).catch(function(imError) {
  console.warn('getConversationList error:', imError); // Failed to obtain the conversation list
});

:::
</dx-codeblock>


<dx-codeblock>
:::  js

// Get the list of specified conversations
let promise = tim.getConversationList([conversationID1, conversationID2]);
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // List of specified conversations that exist in the cache
}).catch(function(imError) {
  console.warn('getConversationList error:', imError); // Failed to obtain the conversation list
});

:::
</dx-codeblock>

## Getting the Detailed Conversation Profile

**API**

<dx-codeblock>
:::  js

tim.getConversationProfile(conversationID);

:::
</dx-codeblock>


**Parameter**

| Name           | Type   | Description                                                  |
| -------------- | ------ | ------------------------------------------------------------ |
| conversationID | String | Conversation ID. Valid values:<br/><li>C2C${userID} (for a one-to-one chat)</li><li>GROUP{groupID} (for a group chat)</li><li>@TIM#SYSTEM (for a system notification conversation)</li> |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.getConversationProfile(conversationID);
promise.then(function(imResponse) {
  // Conversation profile obtained successfully
  console.log(imResponse.data.conversation); // Conversation profile
}).catch(function(imError) {
  console.warn('getConversationProfile error:', imError); // Failed to obtain the conversation profile
});

:::
</dx-codeblock>