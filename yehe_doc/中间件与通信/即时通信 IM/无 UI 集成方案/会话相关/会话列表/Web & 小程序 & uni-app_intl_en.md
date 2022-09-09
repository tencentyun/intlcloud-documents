## Feature Description

After a user logs in to the application, the list of recent conversations can be displayed to make it easy to locate the target conversation.
The conversation list is as follows:
<img src="https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/res/RPReplay_Final0511.gif" alt="" style="zoom:40%;" />

The conversation list feature includes getting the conversation list and processing the conversation list update. You can listen for [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) to process and render the conversation list data.

**Sample**

<dx-codeblock>
:::  js

let onConversationListUpdated = function(event) {
  console.log(event.data); // Array that stores Conversation instances
};
tim.on(TIM.EVENT.CONVERSATION_LIST_UPDATED, onConversationListUpdated);

:::
</dx-codeblock>