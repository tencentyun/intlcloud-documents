## Overview
In some cases, you may need to group conversations, for example, into a "Product experience" or "R&D" group, which can be implemented through the following API.
> ?
- To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577).
- This feature is available only in SDK enhanced edition v6.5.2803 or later.

## Conversation Group

### Creating a conversation group
Call the `createConversationGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a280dff193ef770efd5d878ca3e3821d5) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a2f5f4587c881aa26fbdce3b4d469aa0a) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#ab2d52eebca186348cdc6d655e39303b2)) to create a conversation group.
>? Up to 20 conversation groups can be created. After this limit is exceeded, the `51010` error will be reported. Groups that are no longer used should be promptly deleted.

| Attribute          | Definition               | Description                                                  |
| ------------------ | ------------------------ | ------------------------------------------------------------ |
| groupName          | Conversation group name  | It must be greater than 0 in length and can contain up to 32 bytes; otherwise, the `51011` error will be reported. |
| conversationIDList | List of conversation IDs | It cannot be empty.                                          |

Sample code:
<dx-tabs>
::: Android
```java
List<String> conversationIDList = new ArrayList<>();
conversationIDList.add("c2c_user1");
V2TIMManager.getConversationManager().createConversationGroup("conversation_group", conversationIDList, new V2TIMValueCallback<List<V2TIMConversationOperationResult>>() {
    @Override
    public void onSuccess(List<V2TIMConversationOperationResult> v2TIMConversationOperationResults) {
        // Created the conversation group successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to create the conversation group
    }
});
```
:::
::: iOS and macOS
```objectivec
// Create a conversation group
[[V2TIMManager sharedInstance] createConversationGroup:@"conversation_group" conversationIDList:@[@"c2c_yahaha"] succ:^(NSArray<V2TIMConversationOperationResult *> *result) {
    // Created the conversation group successfully
} fail:^(int code, NSString *desc) {
    // Failed to create the conversation group
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

V2TIMString groupName = u8"conversation_group";
V2TIMStringVector conversationIDList;
conversationIDList.PushBack(u8"c2c_user1");

auto callback = new ValueCallback<V2TIMConversationOperationResultVector>{};
callback->SetCallback(
    [=](const V2TIMConversationOperationResultVector& conversationOperationResultList) {
        // Created the conversation group successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to create the conversation group
        delete callback;
    });

V2TIMManager::GetInstance()->GetConversationManager()->CreateConversationGroup(groupName, conversationIDList,
                                                                               callback);
```
:::
</dx-tabs>

### Deleting a conversation group
Call the `deleteConversationGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a5ec09de4e1fb5e898e4c0800b06a63bc) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#aa7b91ded9e451335bc931525839ce736) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#a896e015bc43c459cf8b6d34665f201c6)) to delete a conversation group.
>? If the target conversation group doesn't exist, the `51009` error will be reported.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getConversationManager().deleteConversationGroup("conversation_group", new V2TIMCallback() {
    @Override
    public void onSuccess() {
        // Deleted the conversation group successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to delete the conversation group
    }
});
```
:::
::: iOS and macOS
```objectivec
// Delete the conversation group
[[V2TIMManager sharedInstance] deleteConversationGroup:@"conversation_group" succ:^{
        // Deleted the conversation group successfully
} fail:^(int code, NSString *desc) {
        // Failed to delete the conversation group
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

V2TIMString groupName = u8"conversation_group";

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Deleted the conversation group successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        //  Failed to delete the conversation group
        delete callback;
    });

V2TIMManager::GetInstance()->GetConversationManager()->DeleteConversationGroup(groupName, callback);
```
:::
</dx-tabs>

### Renaming a conversation group
Call the `renameConversationGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a0eba052e8f21602b5dbd249ada0c18eb) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a1a9492196c94450b2992079cffab96a6) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#aec1cf0ea82fc1a3e210d89f83bd06af8)) to rename a conversation group.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getConversationManager().renameConversationGroup("conversation_group", "conversation_group_rename", new V2TIMCallback() {
    @Override
    public void onSuccess() {
        // Renamed the conversation group successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to rename the conversation group
    }
});
```
:::
::: iOS and macOS
```objectivec
// Rename a conversation group
[[V2TIMManager sharedInstance] renameConversationGroup:@"conversation_group" newName:@"conversation_group_rename" succ:^{
        // Renamed the conversation group successfully
} fail:^(int code, NSString *desc) {
        // Failed to rename the conversation group
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

V2TIMString oldName = u8"conversation_group";
V2TIMString newName = u8"conversation_group_rename";

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Renamed the conversation group successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to rename the conversation group
        delete callback;
    });

V2TIMManager::GetInstance()->GetConversationManager()->RenameConversationGroup(oldName, newName, callback);
```
:::
</dx-tabs>

### Getting the list of conversation groups
Call the `getConversationGroupList` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ab469fbf92cfdf27d7b268e494028b589) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a037b0973be9feef207a64f2e043792ab) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#afd90c81411d1ab6eeaea2eb7bb888954)) to get the list of conversation groups.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getConversationManager().getConversationGroupList(new V2TIMValueCallback<List<String>>() {
    @Override
    public void onSuccess(List<String> strings) {
        // Obtained the group list successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to obtain the group list
    }
});
```
:::
::: iOS and macOS
```objectivec
// Get the list of conversation groups
[[V2TIMManager sharedInstance] getConversationGroupList:^(NSArray<NSString *> *groupList) {
    // Obtained the group list successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the group list
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

auto callback = new ValueCallback<V2TIMStringVector>{};
callback->SetCallback(
    [=](const V2TIMStringVector& stringList) {
        // Obtained the group list successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain the group list
        delete callback;
    });

V2TIMManager::GetInstance()->GetConversationManager()->GetConversationGroupList(callback);
```
:::
</dx-tabs>

Call the `getConversationListByFilter` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#abf71156b8b6423e98943e25a77dc1967) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ac1b77eedff7f2f8742a873cf766daec9) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#ace956492c5ee80187ebd1795e52b0de8)) to get the list of conversations in a group.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMConversationListFilter filter = new V2TIMConversationListFilter();
filter.setGroupName("conversation_group");
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
filter.groupName = @"conversation_group";
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
filter.groupName = u8"conversation_group";

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

### Adding a conversation to a group
After creating a group, you can call the `addConversationsToGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#abf0cd490796ff60730aa0a8fec037d87) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a37c78d27216882504d2710a066478db5) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#a31e93ef7ee2bbe8d665eb3b1f6520ed3)) to add a conversation to the group.

Sample code:
<dx-tabs>
::: Android
```java
List<String> conversationIDList = new ArrayList<>();
conversationIDList.add("c2c_user2");
V2TIMManager.getConversationManager().addConversationsToGroup("conversation_group", conversationIDList, new V2TIMValueCallback<List<V2TIMConversationOperationResult>>() {
    @Override
    public void onSuccess(List<V2TIMConversationOperationResult> v2TIMConversationOperationResults) {
        // Added the conversation to the group successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to add the conversation to the group
    }
});
```
:::
::: iOS and macOS
```objectivec
// Add a conversation to a group
[[V2TIMManager sharedInstance] addConversationsToGroup:@"conversation_group" conversationIDList:@[@"c2c_yahaha"] succ:^(NSArray<V2TIMConversationOperationResult *> *result) {
    // Added the conversation to the group successfully
} fail:^(int code, NSString *desc) {
    // Failed to add the conversation to the group
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

V2TIMString groupName = u8"conversation_group";
V2TIMStringVector conversationIDList;
conversationIDList.PushBack(u8"c2c_user1");

auto callback = new ValueCallback<V2TIMConversationOperationResultVector>{};
callback->SetCallback(
    [=](const V2TIMConversationOperationResultVector& conversationOperationResultList) {
        // Added the conversation to the group successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to add the conversation to the group
        delete callback;
    });

V2TIMManager::GetInstance()->GetConversationManager()->AddConversationsToGroup(groupName, conversationIDList,
                                                                               callback);
```
:::
</dx-tabs>

### Deleting a conversation from a group
Call the `deleteConversationsFromGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a9ca6ea0ac6d8f61c7d0f8a85f14a91b9) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a16ee46fa4b7278a0386be9ff633fa552) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#ad9b378df06d6b46031262e9712d82d6b)) to delete a conversation from a group.

Sample code:
<dx-tabs>
::: Android
```java
List<String> conversationIDList = new ArrayList<>();
conversationIDList.add("c2c_user2");
V2TIMManager.getConversationManager().deleteConversationsFromGroup("conversation_group", conversationIDList, new V2TIMValueCallback<List<V2TIMConversationOperationResult>>() {
    @Override
    public void onSuccess(List<V2TIMConversationOperationResult> v2TIMConversationOperationResults) {
        // Deleted the conversation from the group successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to delete the conversation from the group
    }
});
```
:::
::: iOS and macOS
```objectivec
// Delete a conversation from a group
[[V2TIMManager sharedInstance] deleteConversationsFromGroup:@"conversation_group" conversationIDList:@[@"c2c_yahaha"] succ:^(NSArray<V2TIMConversationOperationResult *> *result) {
    // Deleted the conversation from the group successfully
} fail:^(int code, NSString *desc) {
    // Failed to delete the conversation from the group
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

V2TIMString groupName = u8"conversation_group";
V2TIMStringVector conversationIDList;
conversationIDList.PushBack(u8"c2c_user1");

auto callback = new ValueCallback<V2TIMConversationOperationResultVector>{};
callback->SetCallback(
    [=](const V2TIMConversationOperationResultVector& conversationOperationResultList) {
        // Deleted the conversation from the group successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to delete the conversation from the group
        delete callback;
    });

V2TIMManager::GetInstance()->GetConversationManager()->DeleteConversationsFromGroup(
    groupName, conversationIDList, callback);
```
:::
</dx-tabs>

### Listening for the notification of a conversation group change
Call the `addConversationListener` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#adb2c20ca824cac69d0703169f3a025a1)) to listen for the notification of a conversation group change.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMConversationListener listener = new V2TIMConversationListener() {
    @Override
    public void onConversationGroupCreated(String groupName, List<V2TIMConversation> conversationList) {
        // Received the notification of conversation group creation
    }

    @Override
    public void onConversationGroupDeleted(String groupName) {
        // Received the notification of conversation group deletion
    }

    @Override
    public void onConversationGroupNameChanged(String oldName, String newName) {
        // Received the notification of conversation group renaming
    }

    @Override
    public void onConversationsAddedToGroup(String groupName, List<V2TIMConversation> conversationList) {
        // Received the notification of a conversation added to a group
    }

    @Override
    public void onConversationsDeletedFromGroup(String groupName, List<V2TIMConversation> conversationList) {
        // Received the notification of a conversation deleted from a group
    }
};
V2TIMManager.getConversationManager().addConversationListener(listener);
```
:::
::: iOS and macOS
```objectivec
// Delete the conversation group
[[V2TIMManager sharedInstance] addConversationListener:self];
- (void)onConversationGroupCreated:(NSString *)groupName conversationList:(NSArray<V2TIMConversation *> *)conversationList {
    // Received the notification of conversation group creation
}
- (void)onConversationGroupDeleted:(NSString *)groupName {
    // Received the notification of conversation group deletion
}
- (void)onConversationGroupNameChanged:(NSString *)oldName newName:(NSString *)newName {
    // Received the notification of conversation group renaming
}
- (void)onConversationsAddedToGroup:(NSString *)groupName conversationList:(NSArray<V2TIMConversation *> *)conversationList {
    // Received the notification of a conversation added to a group
}
- (void)onConversationsDeletedFromGroup:(NSString *)groupName conversationList:(NSArray<V2TIMConversation *> *)conversationList {
    // Received the notification of a conversation deleted from a group
}
```
:::
::: Windows
```cpp
class ConversationListener final : public V2TIMConversationListener {
public:
    ConversationListener() = default;
    ~ConversationListener() override = default;

    void OnConversationGroupCreated(const V2TIMString& groupName,
                                    const V2TIMConversationVector& conversationList) override {
        // Received the notification of conversation group creation
    }

    void OnConversationGroupDeleted(const V2TIMString& groupName) override {
        // Received the notification of conversation group deletion
    }

    void OnConversationGroupNameChanged(const V2TIMString& oldName, const V2TIMString& newName) override {
        // Received the notification of conversation group renaming
    }

    void OnConversationsAddedToGroup(const V2TIMString& groupName,
                                     const V2TIMConversationVector& conversationList) override {
        // Received the notification of a conversation added to a group
    }

    void OnConversationsDeletedFromGroup(const V2TIMString& groupName,
                                         const V2TIMConversationVector& conversationList) override {
        // Received the notification of a conversation deleted from a group
    }
};

// Add a conversation event listener. Keep `conversationListener` valid before the listener is removed to ensure event callbacks are received.
ConversationListener conversationListener;
V2TIMManager::GetInstance()->GetConversationManager()->AddConversationListener(&conversationListener);
```
:::
</dx-tabs>
