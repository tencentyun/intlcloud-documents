## Displaying the Conversation List

After logging in to the app, you can display a list of recent conversations like WeChat. The entire display process includes the following steps: **pulling the conversation list**, **processing the change notifications**, and **updating the UI content (including the unread count)**. This document describes these steps in detail.

## Pulling the Conversation List

You can call [ConvGetConvList](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvGetConvList.html) to pull the list of all conversations. The Unity SDK currently does not support pagination for the conversation list.

## Updating the Conversation List

When the information in a conversation changes, the SDK will call back the information to you via `ConvEventCallback`.

```c#
TencentIMSDK.ConvEventCallback((TIMConvEvent conv_event, List<ConvInfo> conv_list, string user_data)=>{
	// Information about conversation list changes
});
```

Update scenarios include:

- `lastMessage` update
- Network reconnection
- Conversation creation
- Pinning a conversation to the top
- Changes of conversation message receiving options

## Obtaining the Total Unread Message Count of All Conversations

You can call [ConvGetTotalUnreadMessageCount](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvGetTotalUnreadMessageCount.html) to get the total unread count of all conversations. The call details are as follows:

```c#
TencentIMSDK.ConvGetTotalUnreadMessageCount((int code, string desc, string json_param, string user_data)=>{
	
})
```

## Marking All Conversations Read

The Unity SDK provides the [MsgMarkAllMessageAsRead](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgMarkAllMessageAsRead.html) API to mark unread messages of all conversations as read.

```c#
TencentIMSDK.MsgMarkAllMessageAsRead((int code, string desc, string json_param, string user_data)=>{
	
})
```

## Pinning a Conversation to the Top

You can pin a one-to-one or group conversation to the top of the conversation list so you can quickly find it. The new SDK version has added the [ConvPinConversation](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvPinConversation.html) API to pin/unpin conversations to/from the top. It also supports roaming and multi-client synchronization.
The [ConvInfo](https://comm.qq.com/im/doc/unity/en/types/ConvAttributes/ConvInfo.html) conversation object has added the [conv_is_pinned](https://comm.qq.com/im/doc/unity/en/types/ConvAttributes/ConvInfo.html#convispinned) field, which is used to determine whether a conversation is pinned on top. When the pinned-on-top status of a conversation changes, the SDK will call back [ConvEventCallback](https://comm.qq.com/im/doc/unity/en/callback/ConvEventCallback.html) to your app.

```c#
TencentIMSDK.ConvPinConversation(conv_id,conv_type,is_pinned,(int code, string desc, string json_param, string user_data)=>{
	
})
```

## Deleting a Conversation

You can call the [ConvDelete](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvDelete.html) API to delete a conversation. Conversation deletion cannot be synchronized across multiple clients by default. You can enable the multi-client synchronization feature in the console. When a conversation is deleted, the message history of this conversation will be deleted from the local storage and the server by default, and cannot be recovered.

```c#
TencentIMSDK.ConvDelete(conv_id,conv_type,(int code, string desc, string json_param, string user_data)=>{

})
```

## Drafts

When sending a message, you may need to switch to another chat window before message editing is completed. In this case, you can call the [ConvSetDraft](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvSetDraft.html) API to save the unfinished message. Later, you can return to the original chat window and use the [conv_draft](https://comm.qq.com/im/doc/unity/en/types/ConvAttributes/ConvInfo.html#convdraft) field in [ConvInfo](https://comm.qq.com/im/doc/unity/en/types/ConvAttributes/ConvInfo.html) to continue editing the message.

## FAQs

### 1. What is the upper limit for the number of conversations that can be stored in a conversation list?

A locally stored conversation list can have unlimited number of conversations. A conversation list stored in the cloud can have up to 100 conversations.
If the information of a conversation has not been updated for a long time, this conversation can be stored in the cloud for at most 7 days. To adjust the period for storing the conversation, [contact us](https://intl.cloud.tencent.com/document/product/1047/41676).

### 2. Why are the conversation lists pulled on different mobile phones by using the same account inconsistent?

Locally stored conversations may not always be consistent with those stored in the cloud. If you do not call the `ConvDelete` API to delete the local conversations, these conversations will always exist. However, at most 100 conversations can be stored in the cloud. In addition, if the information of a conversation has not been updated for a long time, this conversation can be stored in the cloud for at most 7 days. Therefore, local conversations displayed on different mobile phones may be inconsistent with each other.

### 3. Why are repeated conversations pulled?

Conversations that are pulled by the `ConvGetConvList` API may have already been added to the data source of the UI conversation list through the `ConvEventCallback` callback API. Therefore, to avoid adding the same conversation repeatedly, you need to find and replace the same conversations based on `conv_id`.
