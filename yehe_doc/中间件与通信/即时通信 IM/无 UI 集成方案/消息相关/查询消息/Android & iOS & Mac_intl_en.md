## Overview
You can call `findMessages` to query a local message based on the `messageID`. Note that:
1. Only local messages can be queried, for example, received messages or historical messages pulled by API.
2. Audio-video group (AVChatRoom) messages cannot be queried, as they are not saved locally.

## Querying a Local Message
Call the `findMessages` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dbaec04bc389d01f815f46c550e2fd) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a4a0c47d706d8784656225c1e9065f6f1) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#ac5531e73378b8b8eadd056ba99e5427e)) to query a local message.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().findMessages(messageIDList, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {}

    @Override
    public void onError(int code, String desc) {}
});
```
:::
::: iOS and macOS
```objectivec
[V2TIMManager.sharedInstance findMessages:messageIDList
                                        succ:^(NSArray<V2TIMMessage *> *msgs) {
    // Messages queried successfully
} fail:^(int code, NSString *desc) {
    // Failed to query the messages
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

auto callback = new ValueCallback<V2TIMMessageVector>{};
callback->SetCallback(
    [=](const V2TIMMessageVector& messageVector) {
        // Messages queried successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to query the messages
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->FindMessages(messageIDList, callback);
```
:::
</dx-tabs>
