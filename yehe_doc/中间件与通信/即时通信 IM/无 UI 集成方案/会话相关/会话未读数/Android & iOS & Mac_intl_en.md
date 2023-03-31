## Overview
A user's conversation list usually contains multiple conversations. If there is a new message in one of the conversations, a badge needs to be displayed in the list cell to indicate the unread count.
After the user clicks to enter the conversation and goes back to the conversation list, the unread count is cleared, and the badge disappears.
The Chat SDK also supports getting the total unread message count of all or some conversations (using filters), which is displayed at the bottom tab of the conversation list.

This document describes how to implement the conversation unread count notification feature.

[](id:getTotalUnreadMessageCount)
## Getting the Total Unread Count of All Conversations
In general cases, to get the total unread count of all the conversations, you can traverse the conversation list to get the `V2TIMConversation` information of each conversation and add the `unreadCount` values of all the `V2TIMConversation` objects to get the final result and display it on the UI.
The Chat SDK provides the `getTotalUnreadMessageCount` API to query the total unread count of all the conversations.
When the total unread count changes, the SDK will notify the latest total unread count through the `onTotalUnreadMessageCountChanged` callback.

> ?
> 1. This feature is supported only by the SDK of the Enhanced edition on v5.3.425 or later.
> 2. This feature applies only to work groups (Work), public groups (Public), and communities (Community), but not to audio-video groups (AVChatRoom) or meeting groups (Meeting). For more information on the group types, see [Group Overview](https://intl.cloud.tencent.com/document/product/1047/48169).

Below are detailed steps.

### Getting the total unread count of all conversations
Call `getTotalUnreadMessageCount` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a08bdd15d7ee2737335a01285d7f9c44a) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#abe76208f616713a09df582a6c1665d38) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#a50e0d25b7f47c12c815e610bf5b9a048)) to get the total unread message count of all conversations and display it on the UI.

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
    // Obtained successfully. `totalCount` is the total unread message count of all conversations.
    // Update the unread count on the UI
} fail:^(int code, NSString *desc) {
    // Failed to obtain
}];
```
:::
::: Windows
```cpp
template <class T>
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T& value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

auto callback = new ValueCallback<uint64_t>{};
callback->SetCallback(
    [=](const uint64_t& count) {
        // Got the total unread count of all conversations successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to get the total unread count of all conversations
        delete callback;
    });

V2TIMManager::GetInstance()->GetConversationManager()->GetTotalUnreadMessageCount(callback);
```
:::
</dx-tabs>

### Notification of a change in the total unread count
Call `addConversationListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#adb2c20ca824cac69d0703169f3a025a1)) to add a conversation listener to receive notifications of a change in the total unread count of all conversations (such notifications can be received only after the `getTotalUnreadMessageCount` API is called).

You can get the changed total unread count in `onTotalUnreadMessageCountChanged` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html#a292e893a04cb092fe49c06873c1ea4b3) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMConversationListener-p.html#ab254716e0edb04a0192fb56d27b611e4) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationListener.html#ad73f5c7260833575c7d8f4c0ae508388)) of `V2TIMConversationListener`.

Sample code:
<dx-tabs>
::: Android
```java
public void onTotalUnreadMessageCountChanged(long totalUnreadCount) {
    // Received a notification of a change in the total unread count of all conversations
    Log.i("imsdk", "onTotalUnreadMessageCountChanged");
}
```
:::
::: iOS and macOS
```objectivec
// Add a conversation listener
[[V2TIMManager sharedInstance] addConversationListener:self];

// Received a notification of a change in the total unread count of all conversations
- (void)onTotalUnreadMessageCountChanged:(UInt64)totalUnreadCount {
    // `totalUnreadCount` is the total unread count.
}
```
:::
::: Windows
```cpp
class ConversationListener final : public V2TIMConversationListener {
public:
    /**
     * Notification of the change of the total unread message count of all conversations (supported by 5.3.425 or later)
     *
     * @note
     *  - The total unread message count excludes the unread message count of Do-Not-Disturb conversations (conversations whose message receiving option is
     *  V2TIM_NOT_RECEIVE_MESSAGE or V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE).
     */
    void OnTotalUnreadMessageCountChanged(uint64_t totalUnreadCount) override {
        // Received a notification of a change in the total unread count of all conversations
    }
    // Other member functions...
};

// Add a conversation event listener. Keep `conversationListener` valid before the listener is removed to ensure event callbacks are received.
ConversationListener conversationListener;
V2TIMManager::GetInstance()->GetConversationManager()->AddConversationListener(&conversationListener);
```
:::
</dx-tabs>


[](id:getUnreadMessageCountByFilter)
## Getting the Total Unread Message Count of Some Conversations by Filters
The Chat SDK provides the `getUnreadMessageCountByFilter` API for you to query the total unread message count of some conversations based on filters.
To listen for the changes of the total unread message count of some conversations based on filters, call `subscribeUnreadMessageCountByFilter` to register the listening. When the total unread count under the specified filters changes, the SDK will notify you of the latest total unread count through the `onUnreadMessageCountChangedByFilter` callback.

> ?
> 1. This feature is supported only by the SDK of the Enhanced edition on v7.0.3754 or later.
> 2. This feature applies only to work groups (Work), public groups (Public), and communities (Community), but not to audio-video groups (AVChatRoom) or meeting groups (Meeting). For more information on the group types, see [Group Overview](https://intl.cloud.tencent.com/document/product/1047/48169).

Below are detailed steps.

### Getting the total unread message count of some conversations
Call `getUnreadMessageCountByFilter` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ad68a1302b6cb775e09c4b4277bcb0c96) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a6ddcab75125f4b09e8bfc4521817d09d) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#a5a569ee64dc582e01865cd5ebfc9fbe3)) to get the total unread message count of some conversations and update it on the UI. The filter condition `V2TIMConversationListFilter` is described as follows:

| Attribute         | Definition                                                   | Description                                                  |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| type              | Conversation type (`0` indicates that this item is not filtered.) | One-to-one or group conversation                             |
| conversationGroup | Conversation group name (If no value is entered, this item is not filtered.) | It is not the group name but the conversation group name. For more information, see [Conversation Group](https://intl.cloud.tencent.com/document/product/1047/48854). |
| markType          | Conversation tag type (`0` indicates that this item is not filtered.) | For more information, see [Conversation Tag](https://intl.cloud.tencent.com/document/product/1047/48853). |

Sample code:
<dx-tabs>
::: Android
```java
V2TIMConversationListFilter filter = new V2TIMConversationListFilter();
filter.setConversationType(V2TIMConversation.V2TIM_GROUP);
filter.setConversationGroup("conversation_group");
filter.setMarkType(V2TIMConversation.V2TIM_CONVERSATION_MARK_TYPE_STAR);

V2TIMManager.getConversationManager().getUnreadMessageCountByFilter(filter, new V2TIMValueCallback<Long>() {
    @Override
    public void onSuccess(Long totalUnreadCount) {
        tvLog.setText("getUnreadMessageCountByFilter success, totalUnreadCount:" + totalUnreadCount);
    }

    @Override
    public void onError(int code, String desc) {
        tvLog.setText("getUnreadMessageCountByFilter failed");
    }
});
```
:::
::: iOS and macOS
```objectivec
V2TIMConversationListFilter *filter = [[V2TIMConversationListFilter alloc] init];
filter.type = V2TIM_GROUP;
filter.conversationGroup = @"conversation_group";
filter.markType = V2TIM_CONVERSATION_MARK_TYPE_STAR;

[[V2TIMManager sharedInstance] getUnreadMessageCountByFilter:filter succ:^(UInt64 totalUnreadCount) {
    [self appendString:[NSString stringWithFormat:@"getUnreadMessageCountByFilter success totalUnreadCount:%llu", totalUnreadCount]];
} fail:^(int code, NSString *desc) {
    [self appendString:[NSString stringWithFormat:@"getUnreadMessageCountByFilter failed"]];
}];
```
:::
::: Windows
```cpp
template <class T>
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T& value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

auto callback = new ValueCallback<uint64_t>{};
callback->SetCallback(
    [=](const uint64_t& count) {
        // Got the total unread count successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to get the total unread count
        delete callback;
    });

V2TIMConversationListFilter filter;
filter.type = V2TIM_GROUP;
filter.conversationGroup = "conversation_group";
filter.markType = V2TIM_CONVERSATION_MARK_TYPE_STAR;

V2TIMManager::GetInstance()->GetConversationManager()->GetUnreadMessageCountByFilter(filter, callback);
```
:::
</dx-tabs>

### Registering the listening for the changes of the total unread message count of some conversations
Call `addConversationListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#adb2c20ca824cac69d0703169f3a025a1)) to add a conversation listener. Then call the `subscribeUnreadMessageCountByFilter` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a27b7c9477c5a2fb4c4f05b2e499d6f61) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a123e1e578a92fa68b7087857c816fbd2) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#a39feb1af6519c85b0477b0244ec15b25)) API to register the listening for the changes of the total unread message count under specified filters.

You can get the changed total unread count in `onUnreadMessageCountChangedByFilter` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html#a774a1f3ba5276aa97b67c46f530bd500) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMConversationListener-p.html#a9145537b01df07bb0795c23e3cfa9f67) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationListener.html#a26d1c28f8d4151e9899f3e7b109e17db)) of `V2TIMConversationListener`.

You can specify multiple filters for the unread count listening. The `filter` parameter in the `onUnreadMessageCountChangedByFilter` callback lists the filters specified when `subscribeUnreadMessageCountByFilter` is called. The `filter` parameter contains the `conversationType`, `conversationGroup`, and `markType` fields. We can distinguish between different filters by checking whether all three fields are the same.

Sample code:
<dx-tabs>
::: Android
```java
// Add a conversation listener
V2TIMManager.getConversationManager().addConversationListener(conversationListener);

// Register the listening for the changes of the total unread message count under specified filters
V2TIMConversationListFilter filter = new V2TIMConversationListFilter();
filter.setConversationType(V2TIMConversation.V2TIM_GROUP);
filter.setConversationGroup("conversation_group");
filter.setMarkType(V2TIMConversation.V2TIM_CONVERSATION_MARK_TYPE_STAR);
V2TIMManager.getConversationManager().subscribeUnreadMessageCountByFilter(filter);

// Notification on the change of the total unread message count under specified filters
public void onUnreadMessageCountChangedByFilter(V2TIMConversationListFilter filter, long totalUnreadCount) {
    // `filter` indicates the filter conditions. `totalUnreadCount` indicates the total unread message count.
    Log.i(TAG, "onUnreadMessageCountChangedByFilter:" + totalUnreadCount + "\n");
}
```
:::
::: iOS and macOS
```objectivec
// Add a conversation listener
[[V2TIMManager sharedInstance] addConversationListener:self];

// Register the listening for the changes of the total unread message count under specified filters
V2TIMConversationListFilter *filter = [[V2TIMConversationListFilter alloc] init];
filter.type = V2TIM_GROUP;
filter.conversationGroup = @"conversation_group";
filter.markType = V2TIM_CONVERSATION_MARK_TYPE_STAR;
[[V2TIMManager sharedInstance] subscribeUnreadMessageCountByFilter:filter];

// Notification on the change of the total unread message count under specified filters
- (void)onUnreadMessageCountChangedByFilter:(V2TIMConversationListFilter *)filter totalUnreadCount:(UInt64)totalUnreadCount {
    // `filter` indicates the filter conditions. `totalUnreadCount` indicates the total unread message count.
}
```
:::
::: Windows
```cpp
class ConversationListener final : public V2TIMConversationListener {
public:
	  // Notification on the change of the total unread message count under specified filters
    void OnUnreadMessageCountChangedByFilter(const V2TIMConversationListFilter &filter, uint64_t totalUnreadCount) override {
         // `filter` indicates the filter conditions. `totalUnreadCount` indicates the total unread message count.
    }
    // Other member functions...
};

// Add a conversation event listener. Keep `conversationListener` valid before the listener is removed to ensure event callbacks are received.
ConversationListener conversationListener;
V2TIMManager::GetInstance()->GetConversationManager()->AddConversationListener(&conversationListener);

// Register the listening for the changes of the total unread message count under specified filters
V2TIMConversationListFilter filter;
filter.type = V2TIM_GROUP;
filter.conversationGroup = "conversation_group";
filter.markType = V2TIM_CONVERSATION_MARK_TYPE_STAR;
V2TIMManager::GetInstance()->GetConversationManager()->SubscribeUnreadMessageCountByFilter(filter);
```
:::
</dx-tabs>

### Canceling the listening for the changes of the total unread message count of some conversations
Call the `unsubscribeUnreadMessageCountByFilter` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#adbf33f34fa911bbeec55cf3a4f320ba7) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ae87d91af763df945ed4750cbda079bf2) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#a8b8bf0ed2575efdc08f0b6a7e04faafa)) API to cancel the listening for the changes of the total unread message count under specified filters.

Sample code:
<dx-tabs>
::: Android
```java
// Cancel the listening for the changes of the total unread message count under specified filters
V2TIMConversationListFilter filter = new V2TIMConversationListFilter();
filter.setConversationType(V2TIMConversation.V2TIM_GROUP);
filter.setConversationGroup("conversation_group");
filter.setMarkType(V2TIMConversation.V2TIM_CONVERSATION_MARK_TYPE_STAR);
V2TIMManager.getConversationManager().unsubscribeUnreadMessageCountByFilter(filter);
```
:::
::: iOS and macOS
```objectivec
// Cancel the listening for the changes of the total unread message count under specified filters
V2TIMConversationListFilter *filter = [[V2TIMConversationListFilter alloc] init];
filter.type = V2TIM_GROUP;
filter.conversationGroup = @"conversation_group";
filter.markType = V2TIM_CONVERSATION_MARK_TYPE_STAR;
[[V2TIMManager sharedInstance] unsubscribeUnreadMessageCountByFilter:filter];
```
:::
::: Windows
```cpp
// Cancel the listening for the changes of the total unread message count under specified filters
V2TIMConversationListFilter filter;
filter.type = V2TIM_GROUP;
filter.conversationGroup = "conversation_group";
filter.markType = V2TIM_CONVERSATION_MARK_TYPE_STAR;
V2TIMManager::GetInstance()->GetConversationManager()->UnsubscribeUnreadMessageCountByFilter(filter);
```
:::
</dx-tabs>
    
[](id:markMessageAsRead)
## Clearing the Conversation Unread Count
After the user clicks to enter a conversation and goes back to the conversation list, the unread count needs to be cleared, after which the badge in the conversation list needs to disappear.
The Chat SDK provides three APIs to clear the unread count for different conversation types:
* `markC2CMessageAsRead` is used to clear the unread count of a **one-to-one** conversation.
* `markGroupMessageAsRead` is used to clear the unread count of a **group** conversation.
* `markAllMessageAsRead` is used to clear the unread count of **all** the conversations.

Below are detailed steps.

>? This feature is supported only by the SDK of the Enhanced edition on v5.8.1668 or later. 

### One-to-one chat
Call `markC2CMessageAsRead` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7c09d0ba4a8018f5f9eec4760c4c7b9b) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acb3a67bd2fa131b50c611a48fa78f34d) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a024f95bcf2b37a354f11f5b5a4d6920f)) to clear the unread count of a specified one-to-one conversation.

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
::: Windows
```cpp
class Callback final : public V2TIMCallback {
public:
    using SuccessCallback = std::function<void()>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    Callback() = default;
    ~Callback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess() override {
        if (success_callback_) {
            success_callback_();
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMString userID = u8"userID";

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Cleared the unread count successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to clear the unread count
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->MarkC2CMessageAsRead(userID, callback);
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
::: Windows
```cpp
class ConversationListener final : public V2TIMConversationListener {
public:
    /**
     * If the key information of some conversations changes (for example, the unread count changes, or the last message is updated),
     * use "lastMessage -> timestamp" to sort the conversation list again.
     *
     * @param conversationList  Conversation list
     */
    void OnConversationChanged(const V2TIMConversationVector& conversationList) override {}
    // Other members …
};

// Add a conversation event listener. Keep `conversationListener` valid before the listener is removed to ensure event callbacks are received.
ConversationListener conversationListener;
V2TIMManager::GetInstance()->GetConversationManager()->AddConversationListener(&conversationListener);

class AdvancedMsgListener final : public V2TIMAdvancedMsgListener {
public:
    /**
     * One-to-one message read notification (This callback is received when the recipient calls the `MarkC2CMessageAsRead` API.
     * The callback contains only the UserID and read timestamp information of the recipient.)
     *
     * @param receiptList  Read receipt list
     */
    void OnRecvC2CReadReceipt(const V2TIMMessageReceiptVector& receiptList) override {}
    // Other members …
};

// Add an event listener for advanced messages. Keep `advancedMsgListener` valid before it is removed to ensure event callbacks are received.
AdvancedMsgListener advancedMsgListener;
V2TIMManager::GetInstance()->GetMessageManager()->AddAdvancedMsgListener(&advancedMsgListener);
```
:::
</dx-tabs>

### Group chat
Call `markGroupMessageAsRead` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ac0a65f18d361abde8a0ac16132027e69) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#abdf09c92dccfb71b58b8a36f42494b8d)) to clear the unread message count of a specified group conversation.

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
::: Windows
```cpp
class Callback final : public V2TIMCallback {
public:
    using SuccessCallback = std::function<void()>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    Callback() = default;
    ~Callback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess() override {
        if (success_callback_) {
            success_callback_();
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMString groupID = u8"groupID";

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Cleared the unread count successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Cleared the unread count successfully
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->MarkGroupMessageAsRead(groupID, callback);
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
::: Windows
```cpp
class ConversationListener final : public V2TIMConversationListener {
public:
    void OnConversationChanged(const V2TIMConversationVector& conversationList) override {}
    // The caller received the notification of a change in the conversation information.
};

// Add a conversation event listener. Keep `conversationListener` valid before the listener is removed to ensure event callbacks are received.
ConversationListener conversationListener;
V2TIMManager::GetInstance()->GetConversationManager()->AddConversationListener(&conversationListener);
```
:::
</dx-tabs>

### All conversations
Call `markAllMessageAsRead` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad097a0da2ea0002f2b0f2d1d11f3a4ab) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a53d889a6242b5551aa3655e40967a62f) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a78aa9bd36291eb581a347a2cba96509a)) to clear the unread message count of all conversations.

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
::: Windows
```cpp
class Callback final : public V2TIMCallback {
public:
    using SuccessCallback = std::function<void()>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    Callback() = default;
    ~Callback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess() override {
        if (success_callback_) {
            success_callback_();
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Cleared the unread count successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to clear the unread count
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->MarkAllMessageAsRead(callback);
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
::: Windows
```cpp
class ConversationListener final : public V2TIMConversationListener {
public:
    void OnConversationChanged(const V2TIMConversationVector& conversationList) override {}
    // The caller received the notification of a change in the conversation information.
};

// Add a conversation event listener. Keep `conversationListener` valid before the listener is removed to ensure event callbacks are received.
ConversationListener conversationListener;
V2TIMManager::GetInstance()->GetConversationManager()->AddConversationListener(&conversationListener);
```
:::
</dx-tabs>

[](id:isExcludedFromUnreadCount)
## Sending a Message Excluded from the Conversation Unread Count
In normal cases, both one-to-one messages and group messages that are sent will be included in the unread count. Specifically, you can get the conversation unread count through the `unreadCount` of the `V2TIMConversation` conversation object.
If you want to send messages that will not be included in the unread count, such as tips or control messages, when calling `sendMessage`, you can:
* Android: call `setExcludedFromUnreadCount` and set it to `true`.
* iOS/Windows: set the message object `isExcludedFromUnreadCount` to `YES`/`true`.

For how to use `sendMessage`, see [Sending Message](https://intl.cloud.tencent.com/document/product/1047/47994).

>? The `setExcludedFromUnreadCount` or `isExcludedFromUnreadCount` parameter is supported only by the SDK of the Enhanced edition on v5.3.425 or later.

Sample code:
<dx-tabs>
::: Android
```java
// Create the message object
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
// Create the message object
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"This is a signaling message"];

// Set the identifier for excluding from the unread message count
message.isExcludedFromUnreadCount = YES;

// Send the message
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"userA" groupID:nil
priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:YES offlinePushInfo:nil progress:^(uint32_t progress) {
} succ:^{
    // Message sent successfully
} fail:^(int code, NSString *msg) {
    // Failed to send the message
}];
```
:::
::: Windows
```cpp
class SendCallback final : public V2TIMSendCallback {
public:
    using SuccessCallback = std::function<void(const V2TIMMessage&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;
    using ProgressCallback = std::function<void(uint32_t)>;

    SendCallback() = default;
    ~SendCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback,
                     ProgressCallback progress_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
        progress_callback_ = std::move(progress_callback);
    }

    void OnSuccess(const V2TIMMessage& message) override {
        if (success_callback_) {
            success_callback_(message);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }
    void OnProgress(uint32_t progress) override {
        if (progress_callback_) {
            progress_callback_(progress);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
    ProgressCallback progress_callback_;
};

// Create the message object
V2TIMMessage message = V2TIMManager::GetInstance()->GetMessageManager()->CreateTextMessage(u8"content");
// Set not to update the `lastMessage` of the conversation
message.isExcludedFromUnreadCount = true;

auto callback = new SendCallback{};
callback->SetCallback([=](const V2TIMMessage& message) { delete callback; },
                      [=](int error_code, const V2TIMString& error_message) { delete callback; },
                      [=](uint32_t progress) {});

V2TIMManager::GetInstance()->GetMessageManager()->SendMessage(
    message, u8"userID", {}, V2TIMMessagePriority::V2TIM_PRIORITY_NORMAL, false, {}, callback);
```
:::
</dx-tabs>
