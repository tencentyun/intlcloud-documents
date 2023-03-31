## Overview
In certain cases, you might want a message to be received by the receiver only when online; that is, the receiver won't notice the message when offline.
You only need to set `onlineUserOnly` to `true/YES` when calling `sendMessage`. A message sent in this way differs from a general one in that:
1. It cannot be stored offline; that is, it cannot be received if the receiver is offline.
2. It cannot be roamed across devices; that is, if it is received on a device, it cannot be received on another, whether it is read or not.
3. It cannot be stored locally; that is, it cannot be pulled from local or cloud historical messages.

## Sample

### Implementing the feature of "The other party is typing..."

In one-to-one chats, you can use `sendMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a42db237e7ae52cd2aa7edebf4f435c61)) to send a specified custom online message. After receiving the specified custom online message and determining that the sender is typing, the receiver can display "The other party is typing..." on the UI.

Sample code:
<dx-tabs>
::: Android
```java
// Send the prompt "Typing…" to user A
JSONObject jsonObject = new JSONObject();
try {
	jsonObject.put("command", "textInput");
} catch (JSONException e) {
	e.printStackTrace();
}
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createCustomMessage(jsonObject.toString().getBytes());
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "userA", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, true,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
	@Override
	public void onError(int code, String desc) {}
	@Override
	public void onSuccess(V2TIMMessage v2TIMMessage) {}
	@Override
	public void onProgress(int progress) {}
});
```
:::
::: iOS and macOS

```objectivec
// Send the prompt "Typing..." to user A
NSString *customStr = @"{\"command\": \"textInput\"}";
NSData *customData = [customStr dataUsingEncoding:NSUTF8StringEncoding];
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createCustomMessage:customData];
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

// Send the prompt "Typing…" to user A
std::string str{u8"{\"command\": \"textInput\"}"};
V2TIMBuffer data = {reinterpret_cast<const uint8_t*>(str.data()), str.size()};
V2TIMMessage message =
    V2TIMManager::GetInstance()->GetMessageManager()->CreateCustomMessage(data, description, extension);

auto callback = new SendCallback{};
callback->SetCallback([=](const V2TIMMessage& message) { delete callback; },
                      [=](int error_code, const V2TIMString& error_message) { delete callback; },
                      [=](uint32_t progress) {});

V2TIMManager::GetInstance()->GetMessageManager()->SendMessage(
    message, "userA", {}, V2TIMMessagePriority::V2TIM_PRIORITY_DEFAULT, true, {}, callback);
```
:::
</dx-tabs>
