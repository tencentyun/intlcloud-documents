## Feature Description
In some cases, you may need to mark a conversation, for example, as "favorite", "collapsed", "hidden", or "unread", which can be implemented through the following API.
> ?
> - To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577).
> - This feature is available only in v4.0.8 or later.

## Conversation Mark

### Marking a conversation
Call the `markConversation` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/markConversation.html)) API to mark or unmark a conversation.
> ! When a user marks a conversation, the SDK records only the mark value and will not change the underlying logic of the conversation. For example, if a conversation is marked as `V2TIM_CONVERSATION_MARK_TYPE_UNREAD`, the unread count at the underlying layer will not change.

Parameters of the API for marking a conversation are as described below:

| Attribute          | Definition               | Description                                                  |
| ------------------ | ------------------------ | ------------------------------------------------------------ |
| conversationIDList | List of conversation IDs | Up to 100 conversations can be marked at a time.             |
| markType           | Mark type                | A conversation can be marked as a favorite, unread, collapsed, or hidden. |
| enableMark         | Mark/Unmark              | A conversation can be marked/unmarked.                       |

> ? The SDK provides four default marks ("favorite", "collapsed", "hidden", and "unread"). If they cannot meet your requirements, you can customize extended marks, which must meet the following conditions:
1. The value of an extended mark cannot be the same as that of an existing one.
2. The value of an extended mark must be 0x1LL << displacement value of n (`32 ≤ n < 64` indicates that `n` must be equal to or greater than 32 and less than 64). For example, `0x1LL << 32` indicates "Online on an iPhone".

Sample code:

```dart
    // Mark a conversation
    V2TimValueCallback<List<V2TimConversationOperationResult>>
        markConversationRes = await TencentImSDKPlugin.v2TIMManager
            .getConversationManager()
            .markConversation(
                markType: 0,// Mark type
                enableMark: true,// Whether to support the marking feature
                conversationIDList: []);// List of IDs of the conversations to be marked
    if (markConversationRes.code == 0) {
      // Marked successfully
      markConversationRes.data?.forEach((element) {
        element.conversationID; // ID of the conversation marked
        element.resultCode; // Operation result error code of the conversation
        element.resultInfo; // Operation result description of the conversation
      });
    }
```

### Listening for the notification of a conversation mark change
After a conversation is marked or unmarked, the `markList` field ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#marklist)) in `V2TimConversation` of the conversation will change. You can call the `addConversationListener` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/addConversationListener.html)) API to listen for such a change notification.

Sample code:

```dart
    // Set the conversation listener
    V2TimConversationListener listener = V2TimConversationListener(
      onConversationChanged: (List<V2TimConversation> conversationList) => {
        // If the key information of some conversations changes (for example, the unread count changes, or the last message is updated), use "lastMessage -> timestamp" to sort the conversation list again.
        // conversationList: List of conversations that have changes
      }
    );
    // Add a conversation listener
    TencentImSDKPlugin.v2TIMManager
        .getConversationManager()
        .addConversationListener(listener: listener); // Conversation listener to add
```



### Pulling a specified marked conversation
Call the `getConversationListByFilter` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/getConversationListByFilter.html)) API to pull a specified marked conversation.

Sample code:

```dart
    // Get the conversation list
    V2TimConversationListFilter filter = V2TimConversationListFilter(
        conversationType: 0, // Conversation type
        nextSeq: 0,// Pull cursor
        count: 10,// Pull count
        markType: 0,// Conversation mark type
        groupName: "groupName");// Name of the pulled group
    // Advanced API for getting the conversation list
    V2TimValueCallback<V2TimConversationResult> getConversationListByFilterRes =
        await TencentImSDKPlugin.v2TIMManager
            .getConversationManager()
            .getConversationListByFilter(filter: filter);// Conversation list filter
    if (getConversationListByFilterRes.code == 0) {
      // Pulled successfully
      bool? isFinished =getConversationListByFilterRes.data?.isFinished; //Whether the list is fully pulled
      String? nextSeq =getConversationListByFilterRes.data?.nextSeq; // Cursor for the subsequent paged pull
      List<V2TimConversation?>? conversationList =getConversationListByFilterRes.data?.conversationList; // List of conversations pulled this time
      // If more conversations need to be pulled, use the returned `nextSeq` to continue pulling until `isFinished` is `true`.
      if (!isFinished!) {
        V2TimConversationListFilter nextFilter = V2TimConversationListFilter(
            conversationType: 0,
            nextSeq: int.parse(nextSeq!),// Use the returned `nextSeq` to continue pulling until `isFinished` is `true`.
            count: 10,
            markType: 0,
            groupName: "groupName");
        V2TimValueCallback<V2TimConversationResult> nextConversationListRes =
            await TencentImSDKPlugin.v2TIMManager
                .getConversationManager()
                .getConversationListByFilter(
                    filter: nextFilter); 
      }

      getConversationListByFilterRes.data?.conversationList?.forEach((element) {
        element
            ?.conversationID; // Unique conversation ID. It is in the format of `c2c_userID` for a one-to-one chat or `group_groupID` for a group chat.
        element?.draftText; // Draft message
        element?.draftTimestamp; // Draft editing time. It is automatically generated when a draft is set.
        element?.faceUrl; // Displayed conversation profile photo. It is the group profile photo for a group chat or the profile photo of the message receiver for a one-to-one chat.
        element?.groupAtInfoList; // List of @ information in the group conversation. Generally, it is used to display the notifications of "someone@me" and "@all".
        element?.groupID; // ID of the current group. If the conversation type is group chat, `groupID` is the ID of the current group. Otherwise, it is `null`.
        element?.groupType; // Type of the current group. If the conversation type is group chat, `groupType` is the type of the current group. Otherwise, it is `null`.
        element?.isPinned; // Whether the conversation is pinned to the top
        element?.lastMessage; // Last message in the conversation
        element?.orderkey; // Field for sorting conversations
        element?.recvOpt; // Message receiving option
        element
            ?.showName; // Displayed conversation name. The name of a group chat is displayed in the following order of priority: group name > group ID. The name of a one-to-one chat is displayed in the following order of priority: friend remarks of the message receiver > nickname of the message receiver > `userID` of the message receiver.
        element?.type; // Conversation type, which can be `C2C` (one-to-one chat) or `Group` (group chat).
        element?.unreadCount; // Unread message count of the conversation. It is invalid and defaults to `0` for an audio-video group (AVChatRoom).
        element?.userID; // User ID of the message receiver. If the conversation type is one-to-one chat, `userID` is the user ID of the message receiver. Otherwise, it is `null`.
      });
    }
```
