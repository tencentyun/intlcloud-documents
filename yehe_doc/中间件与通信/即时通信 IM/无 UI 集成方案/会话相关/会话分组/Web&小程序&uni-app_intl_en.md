## Feature Description
In some cases, you may need to group conversations, for example, into a "Product experience" or "R&D" group, which can be implemented through the following API.
> ?
- To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577).
- This feature is available only in v2.22.0 or later.

## Conversation Group

### Creating a conversation group
Call the [createConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createConversationGroup) API to create a conversation group. After the API is called successfully, the SDK distributes the [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) and [TIM.EVENT.CONVERSATION_GROUP_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_GROUP_LIST_UPDATED) events.
>? Up to 20 conversation groups can be created. After this limit is exceeded, the `51010` error will be reported. Groups that are no longer used should be promptly deleted.


**API**

<dx-codeblock>
:::  js

tim.createConversationGroup(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type   | Description                                                  |
| ------------------ | ------ | ------------------------------------------------------------ |
| conversationIDList | String | List of conversation IDs                                     |
| groupName          | String | Conversation group name, which can be up to 32 bytes in length |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.createConversationGroup({
  conversationIDList: ['GROUPtest', 'C2Cexample'],
  groupName: 'Suppliers',
});
promise.then(function(imResponse) {
  // Created the conversation group successfully
  const { successConversationIDList, failureConversationIDList } = imResponse.data;
  // successConversationIDList - List of IDs of the conversations that were created successfully
  // Get the conversation list
  const conversationList = tim.getConversationList(successConversationIDList);

  // failureConversationIDList - List of IDs of the conversations that failed to be created
  failureConversationIDList.forEach((item) => {
    const { conversationID, code, message } = item;
  });
}).catch(function(imError){
  console.warn('createConversationGroup error:', imError);
});
:::
</dx-codeblock>

### Deleting a conversation group
Call the [deleteConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationGroup) API to delete a conversation group. After the API is deleted successfully, the SDK distributes the [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) and [TIM.EVENT.CONVERSATION_GROUP_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_GROUP_LIST_UPDATED) events.
>? If the target conversation group doesn't exist, the `51009` error will be reported.

**API**

<dx-codeblock>
:::  js

tim.deleteConversationGroup(groupName);

:::
</dx-codeblock>

**Parameters**

| Name      | Type   | Description                                                  |
| --------- | ------ | ------------------------------------------------------------ |
| groupName | String | Conversation group name, which can be up to 32 bytes in length |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.deleteConversationGroup('Suppliers');
promise.then(function() {
  // Deleted successfully
}).catch(function(imError){
  console.warn('deleteConversationGroup error:', imError);
});

:::
</dx-codeblock>

### Renaming a conversation group
Call the [renameConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#renameConversationGroup) API to rename a conversation group. After the API is renamed successfully, the SDK distributes the [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) and [TIM.EVENT.CONVERSATION_GROUP_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_GROUP_LIST_UPDATED) events.

**API**

<dx-codeblock>
:::  js

tim.renameConversationGroup(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name    | Type   | Description                                           |
| ------- | ------ | ----------------------------------------------------- |
| oldName | String | Old group name                                        |
| newName | String | New group name, which can be up to 32 bytes in length |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.renameConversationGroup({
  oldName: 'Suppliers_old',
  newName: 'Suppliers_new'
});
promise.then(function(imResponse) {
  // Renamed successfully
}).catch(function(imError){
  console.warn('renameConversationGroup error:', imError);
});

:::
</dx-codeblock>

### Getting the list of conversation groups
Call the [getConversationGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationGroupList) API to get the list of conversation groups.

**API**

<dx-codeblock>
:::  js

tim.getConversationGroupList();

:::
</dx-codeblock>

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.getConversationGroupList();
promise.then(function(imResponse) {
  const groupNameList = imResponse.data; // Conversation group name list
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Obtain all conversations in a specified conversation group
let promise = tim.getConversationList({ groupName: 'Suppliers' });
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // Conversation list
});

:::
</dx-codeblock>

### Adding a conversation to a group
After creating a group, you can call the [addConversationsToGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addConversationsToGroup) API to add a conversation to the group. After the API is called successfully, the SDK distributes the [TIM.EVENT.CONVERSATION_IN_GROUP_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_GROUP_LIST_UPDATED) event.

**API**

<dx-codeblock>
:::  js

tim.addConversationsToGroup(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type   | Description                                                  |
| ------------------ | ------ | ------------------------------------------------------------ |
| conversationIDList | String | List of conversation IDs                                     |
| groupName          | String | Conversation group name, which can be up to 32 bytes in length |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.addConversationsToGroup({
  conversationIDList: ['GROUPtest', 'C2Cexample'],,
  groupName: 'Suppliers_new',
});
promise.then(function(imResponse) {
  // Added the conversation to the group successfully
  const { successConversationIDList, failureConversationIDList } = imResponse.data;
  // successConversationIDList - List of IDs of the conversations that were created successfully
  // Get the conversation list
  const conversationList = tim.getConversationList(successConversationIDList);

  // failureConversationIDList - List of IDs of the conversations that failed to be created
  failureConversationIDList.forEach((item) => {
    const { conversationID, code, message } = item;
  });
}).catch(function(imError){
  console.warn('addConversationsToGroup error:', imError);
});

:::
</dx-codeblock>

### Deleting a conversation from a group
Call the [deleteConversationsFromGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationsFromGroup) API to delete a conversation from a group. After the API is called successfully, the SDK distributes the [TIM.EVENT.CONVERSATION_IN_GROUP_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_GROUP_LIST_UPDATED) event.

**API**

<dx-codeblock>
:::  js

tim.deleteConversationsFromGroup(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type   | Description                                                  |
| ------------------ | ------ | ------------------------------------------------------------ |
| conversationIDList | String | List of conversation IDs                                     |
| groupName          | String | Conversation group name, which can be up to 32 bytes in length |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.deleteConversationsFromGroup({
  conversationIDList: ['GROUPtest', 'C2Cexample'],,
  groupName: 'Suppliers_new',
});
promise.then(function(imResponse) {
  // Deleted the conversation from the group successfully
  const { successConversationIDList, failureConversationIDList } = imResponse.data;
  // successConversationIDList - List of IDs of the conversations that were created successfully
  // Get the conversation list
  const conversationList = tim.getConversationList(successConversationIDList);

  // failureConversationIDList - List of IDs of the conversations that failed to be created
  failureConversationIDList.forEach((item) => {
    const { conversationID, code, message } = item;
  });
}).catch(function(imError){
  console.warn('deleteConversationsFromGroup error:', imError);
});

:::
</dx-codeblock>

### Listening for the notification of a conversation group change

Trigger such listening in the case of a conversation group change, such as conversation group creation, deletion, and renaming.

**Sample**

<dx-codeblock>
:::  js

let onConversationGroupListUpdated = function(event) {
  console.log(event.data); // List of all conversation groups
}
tim.on(TIM.EVENT.CONVERSATION_GROUP_LIST_UPDATED, onConversationGroupListUpdated);

:::
</dx-codeblock>

### Listening for the notification of a conversation change in a conversation group

Trigger such listening in the case of a conversation change in a conversation group, for example, adding a conversation to a conversation group or deleting a conversation from a conversation group.

**Sample**

<dx-codeblock>
:::  js

let onConversationInGroupUpdated = function(event) {
  const { groupName, conversationList }  = event.data;
  // groupName - Conversation group name
  // conversationList - List of conversations in the group
}
tim.on(TIM.EVENT.CONVERSATION_IN_GROUP_UPDATED, onConversationInGroupUpdated);

:::
</dx-codeblock>
