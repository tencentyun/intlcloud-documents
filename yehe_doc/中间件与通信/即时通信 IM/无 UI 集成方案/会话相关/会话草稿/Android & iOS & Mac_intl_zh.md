## 功能描述
在发送消息时，可能会遇到消息尚未编辑完，就要切换至其它聊天窗口的情况。这些未编辑完的消息可通过 `setConversationDraft` 接口保存，以便于下次回到这个聊天界面时，通过 `V2TIMConversation` 对象的 `draftText` 字段，获取到尚未编辑完的内容，继续编辑。

> ! 
> 1. 会话草稿仅支持文本内容。
> 2. 会话草稿仅在本地保存，不会存储到服务器，因此不能多端同步，程序卸载重装会失效。

## 设置会话草稿
您可以调用 `setConversationDraft`([Android](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ae7f2f52bf375dae69368eae42edb28ab) / [iOS & Mac](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a462cd163c03cdce230ed3647b414382b) / [Windows](https://im.sdk.qcloud.com/doc/zh-cn/classV2TIMConversationManager.html#a190fb079bf34077f71c340ec23e69ebf)) 接口，设置会话草稿。
如果传递的 `draftText` 参数为空，表示清除草稿。

示例代码如下：
<dx-tabs>
::: Android
```java
String conversationID = "conversationID";
String draftText = "The draft text";
V2TIMManager.getConversationManager().setConversationDraft(conversationID, draftText, new V2TIMCallback() {
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
::: iOS & Mac
```objectivec
NSString *conversationID = @"conversationID";
NSString *draftText = "The draft text";
[[V2TIMManager sharedInstance] setConversationDraft:conversationID draftText:draftText succ:^{
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
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

V2TIMString conversationID = u8"conversationID";
V2TIMString draftText = u8"The draft text";

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // 设置会话草稿成功
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // 设置会话草稿失败
        delete callback;
    });

V2TIMManager::GetInstance()->GetConversationManager()->SetConversationDraft(conversationID, draftText,
                                                                            callback);
```
:::
</dx-tabs>
