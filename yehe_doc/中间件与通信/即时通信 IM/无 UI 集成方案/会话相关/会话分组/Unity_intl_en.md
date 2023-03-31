## Overview
In some cases, you may need to group conversations, for example, into a "Product experience" or "R&D" group, which can be implemented through the following API.
> ?
- To use this feature, you need to purchase the [Ultimate edition](https://buy.cloud.tencent.com/avc?from=17220).
- This feature is supported only on the enhanced edition on native SDK 6.5 or later.

## Conversation Group

### Creating a conversation group
Call the `ConvCreateConversationGroup` ([details](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvCreateConversationGroup.html)) API to create a conversation group.
>? Up to 20 conversation groups can be created. After this limit is exceeded, the `51010` error will be reported. Groups that are no longer used should be promptly deleted.

| Attribute          | Definition               | Description                                                  |
| ------------------ | ------------------------ | ------------------------------------------------------------ |
| groupName          | Conversation group name  | It must be greater than 0 in length and can contain up to 32 bytes; otherwise, the `51011` error will be reported. |
| conversationIDList | List of conversation IDs | It cannot be empty.                                          |

Sample code:

```c#
    // Create a conversation group
    TIMResult res = TencentIMSDK.ConvCreateConversationGroup("groupName", new List<string> {
      conv_id
    }, (int code, string desc, List<ConversationOperationResult> results, string user_data)=>{
      // Async result of the conversation group creation
    });
```


### Deleting a conversation group
Call the `ConvDeleteConversationGroup` ([details](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvDeleteConversationGroup.html)) API to delete a conversation group.
>? If the target conversation group doesn't exist, the `51009` error will be reported.

Sample code:

```c#
    // Delete the conversation group
    TIMResult res = TencentIMSDK.ConvDeleteConversationGroup("groupName", (int code, string desc, string result, string user_data)=>{
      // Async result of the conversation group deletion
    });
```

### Renaming a conversation group
Call the `ConvRenameConversationGroup` ([details](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvRenameConversationGroup.html)) API to rename a conversation group.

Sample code:

```c#
    // Rename a conversation group
    TIMResult res = TencentIMSDK.ConvRenameConversationGroup("oldGroupName", "newGroupName", (int code, string desc, string result, string user_data)=>{
      // Async result of the conversation group renaming
    });
```

### Getting the list of conversation groups
Call the `ConvGetConversationGroupList` ([details](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvGetConversationGroupList.html)) API to get the list of conversation groups.

Sample code:

```c#
    // Get the list of conversation groups
    TIMResult res = TencentIMSDK.ConvGetConversationGroupList((int code, string desc, List<string> results, string user_data)=>{
      // Async result of the conversation group list getting
    });
```


To get the list of conversations under a group, you can call the `ConvGetConversationListByFilter` ([details](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvGetConversationListByFilter.html)) API.

Sample code:

```c#
    // Get the conversation list
    ConversationListFilter filter = new ConversationListFilter
    {
        conversation_list_filter_conv_type: TIMConvType.kTIMConv_C2C,// Conversation type
        conversation_list_filter_mark_type: TIMConversationMarkType.kTIMConversationMarkTypeStar,// Conversation mark type
        conversation_list_filter_conversation_group: "groupName"// Named of the group whose data is to be pulled
    };
    ulong next_seq = 0; // Pulling cursor
    uint count = 10; // Pulling count
    // Advanced API for getting the conversation list
    TIMResult res = TencentIMSDK.ConvGetConversationListByFilter(filter, next_seq, count, (int code, string desc, ConversationListResult result, string user_data)=>{
      // Async result of the conversation list getting
      if (code == 0) {
        // Pulled successfully
        bool isFinished = result.conversation_list_result_is_finished; // Whether pulling is completed
        next_seq = result.conversation_list_result_next_seq; // Cursor for subsequent paged pulling
        var conversationList = result.conversation_list_result_conv_list; // List of messages pulled this time
        // If more conversations need to be pulled, use the returned `nextSeq` to continue pulling until `isFinished` is `true`.
      }
    });
```

### Adding a conversation to a group
After a group is created, you can call the `ConvAddConversationsToGroup` ([details](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvAddConversationsToGroup.html)) API to add a conversation to the group.

Sample code:

```c#
    // Add a conversation to a conversation group
    TIMResult res = TencentIMSDK.ConvAddConversationsToGroup("groupName", new List<string> {
      conv_id
    }, (int code, string desc, List<ConversationOperationResult> results, string user_data)=>{
      // Async result of adding a conversation to a conversation group
    });
```


### Deleting a conversation from a group
Call the `ConvDeleteConversationsFromGroup` ([details](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvDeleteConversationsFromGroup.html)) API to delete a conversation from a group.

Sample code:

```c#
    // Delete a conversation from a conversation group
    TIMResult res = TencentIMSDK.ConvDeleteConversationsFromGroup("groupName", new List<string> {
      conv_id
    }, (int code, string desc, List<ConversationOperationResult> results, string user_data)=>{
      // Async result of deleting a conversation from a conversation group
    });
```


### Listening for the notification of a conversation group change
Call the `SetConvEventCallback` ([details](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetConvEventCallback.html)) API to listen for conversation group change notifications.

Sample code:

```c#
    // Set the conversation listener
    TencentIMSDK.SetConvEventCallback((TIMConvEvent conv_event, List<ConvInfo> conv_list, string user_data)=>{
      // Process the callback logic
    });
```
