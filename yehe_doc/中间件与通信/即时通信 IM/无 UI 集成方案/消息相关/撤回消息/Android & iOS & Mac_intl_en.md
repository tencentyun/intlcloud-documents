## Overview
The sender can recall a successfully sent message.

By default, the sender can recall a message that is sent within 2 minutes. You can change the time limit for message recall. For detailed directions, see [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

Message recall can be implemented through the receiver UI code: When a message is recalled, the receiver will receive the `onRecvMessageRevoked` notification which contains the `msgID` of the recalled message. You can identify the recalled message at the UI layer based on the `msgID` and change the bubble for the message to the "Message recalled" status.

## Recalling a Message (by the Sender)
The sender can call `revokeMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dfce6be749165cd90a9ff67a1308b1) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a972ac3fb7744458eb0d6abd96ce35126) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a3f271fcb935ada0ef05709367638a1a6)) to recall a message.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().revokeMessage(v2TIMMessage, new V2TIMCallback() {
	@Override
	public void onError(int code, String desc) {
		// The message failed to be recalled
	}
	@Override
	public void onSuccess() {
		// Message recalled successfully
	}
});
```
:::
::: iOS and macOS
```objectivec
// `selectedMessage` is the message to be recalled.
[[V2TIMManager sharedInstance] revokeMessage:selectedMessage
										succ:^{
	// Message recalled successfully
} fail:^(int code, NSString *msg) {
	// The message failed to be recalled
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
        // Message recalled successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // The message failed to be recalled
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->RevokeMessage(message, callback);
```
:::
</dx-tabs>

## Noticing a Message Recall (by the Receiver)
1. The receiver calls `addAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a498688ee0f672f114e28d830761dfbf8)) to set the advanced message listener.
2. The receiver receives the message recall notification in `onRecvMessageRevoked` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a13d8197eaba83bfadc7a2f695d671272) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMAdvancedMsgListener.html#aebe1a0b1201ea400df10faf3bd1ec8cb)).

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().addAdvancedMsgListener(new V2TIMAdvancedMsgListener() {
	@Override
	public void onRecvMessageRevoked(String msgID) {
		// `msgList` is the message list on the current chat interface
		for (V2TIMMessage msg : msgList) {
			if (msg.getMsgID().equals(msgID)) {
				// `msg` is the recalled message. You need to change the corresponding message bubble state on the UI.
			}
		}
	}
}
```
:::
::: iOS and macOS
```objectivec
// V2TIMAdvancedMsgListener
- (void)onRecvMessageRevoked:(NSString *)msgID {
	// You need to change the bubble status for the message on the UI after receiving the message recall notification.
}
```
:::
::: Windows
```cpp
class AdvancedMsgListener final : public V2TIMAdvancedMsgListener {
public:
    /**
     * Received a new message
     *
     * @param message Message
     */
    /**
     * Received a message recall notification
     *
     * @param messageID Unique message ID
     */
    void OnRecvMessageRevoked(const V2TIMString& messageID) override {
        // `msgList` is the message list on the current chat interface
    }
    // Other members …
};

// Add an event listener for advanced messages. Keep `advancedMsgListener` valid before it is removed to ensure event callbacks are received.
AdvancedMsgListener advancedMsgListener;
V2TIMManager::GetInstance()->GetMessageManager()->AddAdvancedMsgListener(&advancedMsgListener);
```
:::
</dx-tabs>
