## Feature Description

Message extension allows you to configure keys and values for messages to implement polling, group notes, survey and other types of messages.

- For polling, create a custom message using the `createCustomMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5c2495d4b7ecd66e5636aeb865c17efd)/[iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316)/[Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a580ce76a38da8a0c1a6963b1e7e95cac)) API, where `data` stores the polling title and options. And store the user ID of the voter and selected option(s) in the `key` and `value` of the message extension, respectively. With the selected options of users, we can calculate the polling percentage real time.
- For group notices, create a custom message for group notification using the `createCustomMessage` API, where `data` stores the title of the group notice, and then store the user ID and the corresponding info in the `key` and `value` of the message extension, respectively.
- For survey, create a custom message using the `createCustomMessage` API, where `data` stores the title and options of the survey, and then store the user ID and the corresponding info in the `key` and `value` of the message extension, respectively.

> ?
> - To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577).
> - This feature is available only in SDK enhanced edition v6.7 or later.
> - You need to enable this feature via [IM console](https://console.cloud.tencent.com/im) > **Feature Configuration** > **Login and Message** > **Set message extension**.
> - This feature is not available for communities and audio/video groups.

### Setting message extension

Call the `setMessageExtensions` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a155f6219c2bbf7bc510beec9e905d5db) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2e8b8f7ef94d02823cfab0cf5b1e1fea) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a01d4d98b44f8b1dfdeff3abf1cd71d41)) API to set the message extension. If an extension already exists, modify its `value` info. Otherwise, add new ones.

The request parameters of the `setMessageExtensions` API are detailed as follows:

<table>
<thead>
<tr>
<th>Attribute</th>
<th>Definition</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>message</td>
<td>Message object</td>
<td>Three message conditions to meet:<ul style="margin-bottom: 0px;"><li>Set <code>supportMessageExtension</code> (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html#a9704130e8e105aade0b4797310975563">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html#aca71ee9c6df78832c40c33bdeee4a7ac">iOS &amp; macOS</a> / <a href="https://im.sdk.qcloud.com/doc/en/structV2TIMMessage.html#ad3e6009cd7900c4b08197f5057a8d2d9">Windows</a>) to `YES` before message sending.</li><li>The message is sent successfully.</li><li>The message is not a message of a community/audio-video group.</li></ul></td>
</tr>
<tr>
<td>extensions</td>
<td>Extensions</td>
<td>Modify the `value` info of an existing extension, or add new extensions.</td>
</tr>
</tbody></table>


> ? 
>
> 1. The `key` and `value` of an extension can contain up to 100 B and 1 KB, respectively. You can set up to 20 extensions each time and 300 extensions for a message.

2. If multiple users set or delete the `key` of the same extension simultaneously, only the first user can operate successfully, and other users will receive the error code 23001 and the latest extension info in the setting response packet, who can set it again if necessary.
3. We recommend setting unique keys of extensions by different users to avoid conflicts in most cases. For example, the `userID` can be set as the `key` of the extension in polling, group notices and survey.

Sample code:

<dx-tabs>
::: Android

```java
List<V2TIMMessageExtension> extensionList = new ArrayList<>();
V2TIMMessageExtension extension1 = new V2TIMMessageExtension();
extension1.setExtensionKey("key1");
extension1.setExtensionValue("value1");
extensionList.add(extension1);
V2TIMMessageExtension extension2 = new V2TIMMessageExtension();
extension2.setExtensionKey("key2");
extension2.setExtensionValue("value2");
extensionList.add(extension2);
V2TIMManager.getMessageManager().setMessageExtensions(lastMsg, extensionList, new V2TIMValueCallback<List<V2TIMMessageExtensionResult>>() {
    @Override
    public void onSuccess(List<V2TIMMessageExtensionResult> v2TIMMessageExtensionResults) {
        // Set message extensions successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to set message extensions
    }
});

```

:::
::: iOS and macOS

```objectivec
NSMutableArray *extensionList = [NSMutableArray array];
V2TIMMessageExtension *extension1 = [[V2TIMMessageExtension alloc] init];
extension1.extensionKey = @"key1";
extension1.extensionValue = @"value1";
[extensionList addObject:extension1];
V2TIMMessageExtension *extension2 = [[V2TIMMessageExtension alloc] init];
extension2.extensionKey = @"key2";
extension2.extensionValue = @"value2";
[extensionList addObject:extension2];
[[V2TIMManager sharedInstance] setMessageExtensions:message extensions:extensionList succ:^(NSArray<V2TIMMessageExtensionResult *> *extensionResultList) {
    // Set message extensions successfully
} fail:^(int code, NSString *desc) {
    // Failed to set message extensions
}];
```

:::
::: Windows

```cpp
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T &)>;
    using ErrorCallback = std::function<void(int, const V2TIMString &)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T &value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString &error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMMessageExtensionVector extensionList;
V2TIMMessageExtension extension1;
extension1.extensionKey = "key1";
extension1.extensionValue = "value1";
extensionList.PushBack(extension1);
V2TIMMessageExtension extension2;
extension2.extensionKey = "key2";
extension2.extensionValue = "value2";
extensionList.PushBack(extension2);

auto *callback = new ValueCallback<V2TIMMessageExtensionResultVector>{};
callback->SetCallback(
    [=](const V2TIMMessageExtensionResultVector &extensionResultList) {
        // Set message extensions successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString &error_message) {
        // Failed to set message extensions
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->SetMessageExtensions(message, extensionList, callback);
```

:::
</dx-tabs>

### Getting message extensions

Get the message extension list by calling `getMessageExtensions` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a832534327c08326d045c44b02f7ddbb7)/[iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3ae68d2d8aeff6abd21981914836dc1a)/[Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a7d0ec9f6d4201d916eb2861b19443605)).

> ? If the network is unavailable, the SDK will return the message extension list cached locally.

Sample code:

<dx-tabs>
::: Android

```java
V2TIMManager.getMessageManager().getMessageExtensions(lastMsg, new V2TIMValueCallback<List<V2TIMMessageExtension>>() {
    @Override
    public void onSuccess(List<V2TIMMessageExtension> extensions) {
        // Got message extensions successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to get message extensions
    }
});
```

:::
::: iOS and macOS

```objectivec
[[V2TIMManager sharedInstance] getMessageExtensions:message succ:^(NSArray<V2TIMMessageExtension *> *extensionList) {
    // Got message extensions successfully
} fail:^(int code, NSString *desc) {
    // Failed to get message extensions
}];
```

:::
::: Windows

```cpp
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T &)>;
    using ErrorCallback = std::function<void(int, const V2TIMString &)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T &value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString &error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

auto *callback = new ValueCallback<V2TIMMessageExtensionVector>{};
callback->SetCallback(
    [=](const V2TIMMessageExtensionVector &extensionList) {
        // Got message extensions successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString &error_message) {
        // Failed to get message extensions
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->GetMessageExtensions(message, callback);
```

:::
</dx-tabs>

### Deleting message extensions

Call `deleteMessageExtensions` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a25c02e90cd0940d34fe3bbfd803cc278)/[iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#af3fad5575625e7597a482375d7a65fa6)/[Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a319ceed3323c5005b3630ef1598d5886)) to delete message extensions. If the value of the `keys` field is set to `null`/`nil`, all message extensions will be cleared.

Sample code:

<dx-tabs>
::: Android

```java
List<String> keyList = new ArrayList<>();
keyList.add("key1");
keyList.add("key2");
V2TIMManager.getMessageManager().deleteMessageExtensions(lastMsg, keyList, new V2TIMValueCallback<List<V2TIMMessageExtensionResult>>() {
    @Override
    public void onSuccess(List<V2TIMMessageExtensionResult> v2TIMMessageExtensionResults) {
        // Deleted message extensions successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to delete message extensions
    }
});
```

:::
::: iOS and macOS

```objectivec
[[V2TIMManager sharedInstance] deleteMessageExtensions:message keys:@[@"key1",@"key2"] succ:^(NSArray<V2TIMMessageExtensionResult *> *extensionResultList){
    // Deleted message extensions successfully
} fail:^(int code, NSString *desc) {
    // Failed to delete message extensions
}];
```

:::
::: Windows

```cpp
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T &)>;
    using ErrorCallback = std::function<void(int, const V2TIMString &)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T &value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString &error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMStringVector keys;
keys.PushBack("key1");
keys.PushBack("key2");

auto *callback = new ValueCallback<V2TIMMessageExtensionResultVector>{};
callback->SetCallback(
    [=](const V2TIMMessageExtensionResultVector &extensionResultList) {
        // Deleted message extensions successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString &error_message) {
        // Failed to delete message extensions
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->DeleteMessageExtensions(message, keys, callback);
```

:::
</dx-tabs>


### Updating message extensions

If you have added an event listener for advanced messages by calling `addAdvancedMsgListener`, you will receive the `onRecvMessageExtensionsChanged` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a82082374724b74b95ed8e864842e984c)/[iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html#a406fffe5f5fd1841e62665528eee4f22)/[Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMAdvancedMsgListener.html#a10326b60293d36dd7656eeae394e45f8)) callback when message extensions are added or updated, and the `onRecvMessageExtensionsDeleted` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a8fb8497b0ccc1ff0ca77c672a41dd2db)/[iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html#a1754d7d8f0137ab079806663b5a30f57)/[Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMAdvancedMsgListener.html#a3fe04be92f1fd10f179358cee7f981f1)) callback when message extensions are deleted.

Sample code:

<dx-tabs>
::: Android

```java
V2TIMManager.getMessageManager().addAdvancedMsgListener(new V2TIMAdvancedMsgListener() {
        @Override
        public void onRecvMessageExtensionsChanged(String msgID, List<V2TIMMessageExtension> extensions) {
            // Received a notification of message extension change
        }

        @Override
        public void onRecvMessageExtensionsDeleted(String msgID, List<String> extensionKeys) {
            // Received a notification of message extension deletion
        }
});
```

:::
::: iOS and macOS

```objectivec
[[V2TIMManager sharedInstance] addAdvancedMsgListener:self];
- (void)onRecvMessageExtensionsChanged:(NSString *)msgID extensions:(NSArray<V2TIMMessageExtension *> *)extensions {
   // Received a notification of message extension change
}
- (void)onRecvMessageExtensionsDeleted:(NSString *)msgID extensionKeys:(NSArray<NSString *> *)extensionKeys {
   // Received a notification of message extension deletion
}
```

:::
::: Windows

```cpp
class AdvancedMsgListener final : public V2TIMAdvancedMsgListener {
public:
    void OnRecvMessageExtensionsChanged(const V2TIMString &msgID,
                                        const V2TIMMessageExtensionVector &extensions) override {
        // Received a notification of message extension change
    }

    void OnRecvMessageExtensionsDeleted(const V2TIMString &msgID,
                                        const V2TIMStringVector &extensionKeys) override {
        // Received a notification of message extension deletion
    }
    // Other members …
};

// Add an event listener for advanced messages. Keep `advancedMsgListener` valid before it is removed to ensure event callbacks are received.
AdvancedMsgListener advancedMsgListener;
V2TIMManager::GetInstance()->GetMessageManager()->AddAdvancedMsgListener(&advancedMsgListener);
```

:::
</dx-tabs>
