## Feature Description
A user's conversation list usually contains multiple conversations. If there is a new message in one of the conversations, a badge needs to be displayed in the list cell to indicate the unread count.
After the user clicks to enter the conversation and goes back to the conversation list, the unread count is cleared, and the badge disappears.
In some applications, the total unread count of all the conversations is calculated and displayed at the bottom tab of the conversation list.

This document describes how to implement the conversation unread count notification feature.

[](id:getTotalUnreadMessageCount)
## Getting the Total Unread Count of All the Conversations
In general cases, to get the total unread count of all the conversations, you can traverse the conversation list to get the `V2TIMConversation` information of each conversation and add the `unreadCount` values of all the `V2TIMConversation` objects to get the final result and display it on the UI.
The IM SDK provides the `getTotalUnreadMessageCount` API to query the total unread count of all the conversations.
When the total unread count changes, the SDK will notify the latest total unread count through the `onTotalUnreadMessageCountChanged` callback.

> ?
> 1. This feature is supported only by the SDK of the Enhanced edition on v5.3.425 or later.
> 2. It applies only to work groups (Work), public groups (Public), and communities (Community), but not to audio-video groups (AVChatRoom) or meeting groups (Meeting). For more information on group types, see [Group Overview](https://intl.cloud.tencent.com/document/product/1047/48169).

Below are detailed steps.

### Getting the total unread count
Call `getTotalUnreadMessageCount` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a08bdd15d7ee2737335a01285d7f9c44a) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#abe76208f616713a09df582a6c1665d38)) to get the total unread message count of all conversations and display it on the UI.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getConversationManager().getTotalUnreadMessageCount(new V2TIMValueCallback<Long>() {
    @Override
    public void onSuccess(Long aLong) {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] getTotalUnreadMessageCount:^(UInt64 totalCount) {
    // Obtained the total unread count successfully. `totalCount` is the total unread message count.
    // Update the unread count on the UI
} fail:^(int code, NSString *desc) {
    // Failed to obtain the conversation list
}];
```
:::
</dx-tabs>

### Notification of a change in the total unread count
Call `addConversationListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9)) to add a conversation listener to receive notifications of a change in the total unread count.

You can get the changed total unread count in `onTotalUnreadMessageCountChanged` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html#a292e893a04cb092fe49c06873c1ea4b3) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMConversationListener-p.html#ab254716e0edb04a0192fb56d27b611e4)) of `V2TIMConversationListener`.

Sample code:
<dx-tabs>
::: Android
```java
public void onTotalUnreadMessageCountChanged(long totalUnreadCount) {
    // Received a change in the total unread count
    Log.i("imsdk", "onTotalUnreadMessageCountChanged");
}
```
:::
::: iOS and macOS
```objectivec
// Add a conversation listener
[[V2TIMManager sharedInstance] addConversationListener:self];

// Received a change in the total unread count
- (void)onTotalUnreadMessageCountChanged:(UInt64)totalUnreadCount {
    // `totalUnreadCount` is the total unread count.
}
```
:::
</dx-tabs>


[](id:markMessageAsRead)
## Clearing the Conversation Unread Count
After the user clicks to enter a conversation and goes back to the conversation list, the unread count needs to be cleared, after which the badge in the conversation list needs to disappear.
The IM SDK provides three APIs to clear the unread count for different conversation types:
* `markC2CMessageAsRead` is used to clear the unread count of a **one-to-one** conversation.
* `markGroupMessageAsRead` is used to clear the unread count of a **group** conversation.
* `markAllMessageAsRead` is used to clear the unread count of **all** the conversations.

Below are detailed steps.

>? This feature is supported only by the SDK of the Enhanced edition on v5.8.1668 or later. 

### One-to-one chat
Call `markC2CMessageAsRead` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7c09d0ba4a8018f5f9eec4760c4c7b9b) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acb3a67bd2fa131b50c611a48fa78f34d)) to clear the unread count of a specified one-to-one conversation.

Sample code:
<dx-tabs>
::: Android
```java
String userID = "userID";
V2TIMManager.getMessageManager().markC2CMessageAsRead(userID, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] markC2CMessageAsRead:@"conversationID" // ID of the target one-to-one conversation
                                               succ:^{
    // Cleared the unread count successfully
} fail:^(int code, NSString *msg) {
    // Failed to clear the unread count
}];
```
:::
</dx-tabs>

After the `markC2CMessageAsRead` is called successfully:
1. If the caller has called `addConversationListener` to add a conversation listener, it will receive the `onConversationChanged` callback and update the UI.
2. The sender will receive the `onRecvC2CReadReceipt` callback that contains the timestamp when the conversation unread count is cleared.

Sample code:
<dx-tabs>
::: Android
```java
public void onConversationChanged(List<V2TIMConversation> conversationList) {
    // The caller received the notification of a change in the conversation information.
    Log.i("imsdk", "onConversationChanged");
}

public void onRecvC2CReadReceipt(List<V2TIMMessageReceipt> receiptList) {
    // Read receipt for the one-to-one message
    Log.i("imsdk", "onRecvC2CReadReceipt");
}
```
:::
::: iOS and macOS
```objectivec
// Add a conversation listener
[[V2TIMManager sharedInstance] addConversationListener:self];

// The caller received the notification of a change in the conversation information.
- (void)onConversationChanged:(NSArray<V2TIMConversation*> *)conversationList {
    // Update the UI based on the `V2TIMConversation` in `conversationList`, for example, clear the badge in the cell of the one-to-one conversation
}

// Read receipt for the one-to-one message
- (void)onRecvC2CReadReceipt:(NSArray<V2TIMMessageReceipt *> *)receiptList {
    
}
```
:::
</dx-tabs>

### Group chat
Call `markGroupMessageAsRead` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ac0a65f18d361abde8a0ac16132027e69) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc)) to clear the unread count of a specified group conversation.

Sample code:
<dx-tabs>
::: Android
```java
String groupID = "groupID";
V2TIMManager.getMessageManager().markGroupMessageAsRead(groupID, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] markGroupMessageAsRead:@"conversationID" // ID of the target group conversation
                                               succ:^{
    // Cleared the unread count successfully
} fail:^(int code, NSString *msg) {
    // Failed to clear the unread count
}];
```
:::
</dx-tabs>

After `markGroupMessageAsRead` is called successfully, if the caller has called `addConversationListener` to add a conversation listener, it will receive the `onConversationChanged` callback and update the UI.

Sample code:
<dx-tabs>
::: Android
```java
public void onConversationChanged(List<V2TIMConversation> conversationList) {
    // The caller received the notification of a change in the conversation information.
    Log.i("imsdk", "onConversationChanged");
}
```
:::
::: iOS and macOS
```objectivec
// Add a conversation listener
[[V2TIMManager sharedInstance] addConversationListener:self];

// The caller received the notification of a change in the conversation information.
- (void)onConversationChanged:(NSArray<V2TIMConversation*> *)conversationList {
    // Update the UI based on the `V2TIMConversation` in `conversationList`, for example, clear the badge in the cell of the group conversation
}
```
:::
</dx-tabs>

### All conversations
Call `markAllMessageAsRead` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad097a0da2ea0002f2b0f2d1d11f3a4ab) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a53d889a6242b5551aa3655e40967a62f)) to clear the unread count of all the conversations.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().markAllMessageAsRead(new V2TIMCallback() {
    @Override
    public void onSuccess() {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] markAllMessageAsRead:^{
    // Cleared the unread count successfully
} fail:^(int code, NSString *desc) {
    // Failed to clear the unread count
}];
```
:::
</dx-tabs>

After `markAllMessageAsRead` is called successfully, if the caller has called `addConversationListener` in advance to add a conversation listener, it will receive the `onConversationChanged` callback and update the UI.

Sample code:
<dx-tabs>
::: Android
```java
public void onConversationChanged(List<V2TIMConversation> conversationList) {
    // Received the notification of a change in the conversation information
    Log.i("imsdk", "onConversationChanged");
}
```
:::
::: iOS and macOS
```objectivec
// Add a conversation listener
[[V2TIMManager sharedInstance] addConversationListener:self];

// The caller received the notification of a change in the conversation information.
- (void)onConversationChanged:(NSArray<V2TIMConversation*> *)conversationList {
    // Update the UI, for example, clear the badge on the bottom tab of the conversation list
}
```
:::
</dx-tabs>

[](id:isExcludedFromUnreadCount)
## Sending a Message Excluded from the Conversation Unread Count
In normal cases, both one-to-one messages and group messages that are sent will be included in the unread count. Specifically, you can get the conversation unread count through the `unreadCount` of the `V2TIMConversation` conversation object.
If you want to send messages that will not be included in the unread count, such as tips or control messages, you can set `isExcludedFromUnreadCount` to `true`/`YES` when calling `sendMessage`.

For directions on how to send a message by calling `sendMessage`, see [Sending Message](https://intl.cloud.tencent.com/document/product/1047/47994).

>? The `isExcludedFromUnreadCount` parameter is supported only by the SDK of the Enhanced edition on v5.3.425 or later.

Sample code:
<dx-tabs>
::: Android
```java
// Create a message object
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage(content);
// Set not to update the `lastMessage` of the conversation
v2TIMMessage.setExcludedFromUnreadCount(true);

// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "userID", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, null, new V2TIMSendCallback<V2TIMMessage>() {
    @Override
    public void onSuccess(V2TIMMessage v2TIMMessage) {
        Log.i("imsdk", "success");
    }

    @Override
    public void onProgress(int progress) {
        Log.i("imsdk", "progress:" + progress);
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
// Create a message object
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"This is a signaling message"];

// Set the identifier for excluding from the unread message count
message.isExcludedFromUnreadCount = YES;

// Send the message
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"userA" groupID:nil
priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:YES offlinePushInfo:nil progress:^(uint32_t progress) {
} succ:^{
    // Sent the message successfully
} fail:^(int code, NSString *msg) {
    // Failed to send the message
}];
```
:::
</dx-tabs>


