## Overview
In some cases, you may need to mark a conversation, for example, as "favorite", "collapsed", "hidden", or "unread", which can be implemented through the following API.
> ?
- To use this feature, you need to purchase the [Ultimate edition](https://buy.cloud.tencent.com/avc?from=17220).
- This feature is supported only on native SDK 6.5 or later.

## Conversation Mark

### Marking a conversation
Call the `ConvMarkConversation` ([details](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvMarkConversation.html)) API to mark or unmark a conversation.
> ! When a user marks a conversation, the SDK records only the mark value and will not change the underlying logic of the conversation. For example, if a conversation is marked as `kTIMConversationMarkTypeUnread`, the unread count at the underlying layer will not change.

Parameters of the API for marking a conversation are as described below:

| Attribute          | Definition               | Description                                                  |
| ------------------ | ------------------------ | ------------------------------------------------------------ |
| conversationIDList | List of conversation IDs | Up to 100 conversations can be marked at a time.             |
| markType           | Mark type                | A conversation can be marked as a favorite, unread, collapsed, or hidden. |
| enableMark         | Mark/Unmark              | A conversation can be marked/unmarked.                       |

> ? The SDK provides four default marks ("favorite", "collapsed", "hidden", and "unread"). If they cannot meet your requirements, you can customize extended marks, which must meet the following conditions:
- The value of an extended mark cannot be the same as that of an existing one.
- The value of an extended mark must be 0x1LL << displacement value of n (`32 ≤ n < 64` indicates that `n` must be equal to or greater than 32 and less than 64). For example, `0x1LL << 32` indicates "Online on an iPhone".

Sample code:

```c#
    // Mark a conversation
    TIMResult res = TencentIMSDK.ConvMarkConversation(new List<string> {
      conv_id
    }, TIMConversationMarkType.kTIMConversationMarkTypeStar, true, (int code, string desc, List<ConversationOperationResult> results, string user_data)=>{
      // Async result of the conversation marking
    });
```

### Listening for the notification of a conversation mark change
After a conversation is marked or unmarked, the `conv_mark_array` ([details](https://comm.qq.com/im/doc/unity/zh/types/ConvAttributes/ConvInfo.html)) field of the conversation's `ConvInfo` will be changed. You can call the `SetConvEventCallback` ([details](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetConvEventCallback.html)) API to listen for conversation change notifications.

Sample code:

```c#
    // Set the conversation listener
    TencentIMSDK.SetConvEventCallback((TIMConvEvent conv_event, List<ConvInfo> conv_list, string user_data)=>{
      // Process the callback logic
    });
```



### Pulling a specified marked conversation
Call the `ConvGetConversationListByFilter` ([details](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvGetConversationListByFilter.html)) API to pull a specified marked conversation.

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
