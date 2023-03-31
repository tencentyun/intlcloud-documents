## Overview
In some cases, you may need to mark a conversation, for example, as "favorite", "collapsed", "hidden", or "unread", which can be implemented through the following API.
> ?
- To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577).
- This feature is available only in SDK enhanced edition v6.5.2803 or later.

## Conversation Mark

### Marking a conversation
Call the `markConversation` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#aa1dab66f08df9aef4acb0aad8cb77d72) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a77c02a146f774979e1e04d7334cd2d06) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#ab8d1930cd9956457cd465bd23aa3bd63)) to mark or unmark a conversation.
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
<dx-tabs>
::: Android
```java
List<String> conversationIDList = new ArrayList<>();
conversationIDList.add("c2c_user1");
// Mark type
long markType = V2TIMConversation.V2TIM_CONVERSATION_MARK_TYPE_STAR;
// Extended mark type
// long markType = 0x1L << 32;
V2TIMManager.getConversationManager().markConversation(conversationIDList, markType, true, new V2TIMValueCallback<List<V2TIMConversationOperationResult>>() {
    @Override
    public void onSuccess(List<V2TIMConversationOperationResult> v2TIMConversationOperationResults) {
        // Marked the conversation successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to mark the conversation
    }
});
```
:::
::: iOS and macOS
```objectivec
// Mark type
NSNumber *markType = @(V2TIM_CONVERSATION_MARK_TYPE_STAR);
// Extended mark type
// NSNumber *markType = @(0x1LL << 32);
// Mark a conversation
BOOL enableMark = YES; 
// Unmark a conversation
//  BOOL enableMark = NO; 
[[V2TIMManager sharedInstance] markConversation:@[@"c2c_yahaha"] markType:markType enableMark:enableMark succ:^(NSArray<V2TIMConversationOperationResult *> *result){
    // Marked the conversation successfully
} fail:^(int code, NSString *desc) {
    // Failed to mark the conversation
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

V2TIMStringVector conversationIDList;
conversationIDList.PushBack(u8"c2c_user1");
// Mark type
uint64_t markType = V2TIMConversationMarkType::V2TIM_CONVERSATION_MARK_TYPE_STAR;
// Extended mark type
uint64_t markType = static_cast<uint64_t>(0x1) << 32;

auto callback = new ValueCallback<V2TIMConversationOperationResultVector>{};
callback->SetCallback(
    [=](const V2TIMConversationOperationResultVector& conversationOperationResultList) {
        // Marked the conversation successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to mark the conversation
        delete callback;
    });

V2TIMManager::GetInstance()->GetConversationManager()->MarkConversation(conversationIDList, markType, true,
                                                                        callback);
```
:::
</dx-tabs>

### Listening for the notification of a conversation mark change
After a conversation is marked or unmarked, the `markList` field ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#af8ed1769cee83f972be1727d35e10eb6) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a1778161ca64b919acb1a10c8520538e6) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMConversation.html#a729a11d417ac87cd427a3839e8fa6669)) in `V2TIMConversation` of the conversation will change. You can call the `addConversationListener` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#adb2c20ca824cac69d0703169f3a025a1)) to listen for such a change notification.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMConversationListener listener = new V2TIMConversationListener() {
    @Override
    public void onConversationChanged(List<V2TIMConversation> conversationList) {
        for (V2TIMConversation conversation : conversationList) {
            // Get the new mark information of the conversation
            List<Long> markList = conversation.getMarkList();
        }
    }
};
V2TIMManager.getConversationManager().addConversationListener(listener);
```
:::
::: iOS and macOS
```objectivec
// Delete the conversation group
[[V2TIMManager sharedInstance] addConversationListener:self];
- (void)onConversationChanged:(NSArray<V2TIMConversation*> *) conversationList
{
    for (V2TIMConversation *conv in conversationList) {
        // Get the new mark information of the conversation
        NSArray *mark_list = conv.markList;
    }
}
```
:::
::: Windows
```cpp
class ConversationListener final : public V2TIMConversationListener {
public:
    void OnConversationChanged(const V2TIMConversationVector& conversationList) override {
        for (size_t i = 0; i < conversationList.Size(); ++i) {
            const V2TIMConversation& conversation = conversationList[i];
            // Get the new mark information of the conversation
            const UInt64Vector& markList = conversation.markList;
        }
    }
    // Other members …
};

// Add a conversation event listener. Keep `conversationListener` valid before the listener is removed to ensure event callbacks are received.
ConversationListener conversationListener;
V2TIMManager::GetInstance()->GetConversationManager()->AddConversationListener(&conversationListener);
```
:::
</dx-tabs>


### Pulling a specified marked conversation
Call the `getConversationListByFilter` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#ace956492c5ee80187ebd1795e52b0de8)) to pull a specified marked conversation.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMConversationListFilter filter = new V2TIMConversationListFilter();
filter.setMarkType(V2TIMConversation.V2TIM_CONVERSATION_MARK_TYPE_STAR);
filter.setCount(50);
filter.setNextSeq(0);
V2TIMManager.getConversationManager().getConversationListByFilter(filter, new V2TIMValueCallback<V2TIMConversationResult>() {
    @Override
    public void onSuccess(V2TIMConversationResult v2TIMConversationResult) {
        // Conversation list obtained successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to obtain the conversation list
    }
});
```
:::
::: iOS and macOS
```objectivec
// Pull a specified marked conversation
V2TIMConversationListFilter *filter = [[V2TIMConversationListFilter alloc] init];
filter.markType = V2TIM_CONVERSATION_MARK_TYPE_STAR;
filter.count = 50;
filter.nextSeq = 0;
[[V2TIMManager sharedInstance] getConversationListByFilter:filter succ:^(NSArray<V2TIMConversation *> *list, uint64_t nextSeq, BOOL isFinished) {
   // Obtained the conversation list successfully. `list` is the conversation list.
} fail:^(int code, NSString *desc) {
   // Failed to obtain the conversation list
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

V2TIMConversationListFilter filter;
filter.nextSeq = 0;
filter.count = 50;
filter.markType = V2TIMConversationMarkType::V2TIM_CONVERSATION_MARK_TYPE_STAR;

auto callback = new ValueCallback<V2TIMConversationResult>{};
callback->SetCallback(
    [=](const V2TIMConversationResult& conversationResult) {
        // Conversation list obtained successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain the conversation list
        delete callback;
    });

V2TIMManager::GetInstance()->GetConversationManager()->GetConversationListByFilter(filter, callback);
```
:::
</dx-tabs>
