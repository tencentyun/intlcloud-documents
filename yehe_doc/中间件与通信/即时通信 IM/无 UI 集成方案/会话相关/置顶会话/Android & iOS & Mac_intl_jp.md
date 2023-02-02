## 機能説明
セッションの先頭固定表示とは、ユーザーが簡単に見つけられるように、シングルチャット又はグループチャットのセッションをセッションリストの最上部に固定して、他のセッションの更新によって一番下に移動されないことを意味します。先頭固定表示の状態はサーバーに保存され、端末デバイスを切り替えると、先頭固定表示の状態が新しいデバイスに同期されます。

>? セッションの先頭固定表示機能は、拡張バージョン5.3.425以降でのみサポートされています。先頭固定表示セッションの数の上限は50で、増やすことはできません。

## 先頭固定表示セッション
`pinConversation`([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a4da7467f54c891c4929152260e42f4b6) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a06cefb398f5a327dff4cefe6fb18c5b8) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#ab5afaa92ec352f112125f5dcef288f8d))インターフェースを呼び出して、セッションを先頭固定表示するかどうかを設定できます。

`getConversationList`を呼び出してセッションリストを取得するとき、このインターフェースから返されたセッションリストでは、先頭固定表示されたセッションが最初で、先頭固定表示されていないセッションがその次に表示されます。`V2TIMConversation`オブジェクトの`isPinned`フィールドを使用して、セッションが先頭固定表示されているかどうかを確認できます。

セッションは、`V2TIMConversation`オブジェクトの`orderKey`フィールドの順によって並べ替えられます。`orderKey`フィールドは整数です。新しいメッセージの送信、新しいメッセージの受信、ドラフト設定、またはセッションの先頭固定表示が行われるとき、セッションがアクティブになり、`orderKey`フィールドが増加します。

セッションが先頭固定表示されると、先頭固定表示されたセッションは常に、先頭固定表示されていないセッションの前に並べられます。複数のセッションが同時に先頭固定表示されても、これらのセッション間の相対的な順序は維持されます。
たとえば、5つのセッション1、2、3、4、5が順番に並べられており、セッション2と3を同時に先頭固定表示し、先頭固定表示後の順番は2、3、1、4、5になります。明らかにセッション2と3が一番最初で、セッション2は依然として3よりも前です。

サンプルコードは次のとおりです：
<dx-tabs>
::: Android
```java
// isPinnedパラメータがtrueの場合は、セッションの先頭固定表示を表し、そうでない場合は、先頭固定表示解除を表します。
String conversationID = "conversationID";
V2TIMManager.getConversationManager().pinConversation(conversationID, true, new V2TIMCallback() {
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
// isPinnedパラメータがYESの場合は、セッションの先頭固定表示を表し、そうでない場合は、先頭固定表示解除を表します。
NSString *conversationID = @"conversationID";
[[V2TIMManager sharedInstance] pinConversation:conversationID isPinned:YES succ:^{
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
bool isPinned = true;

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // セッションの先頭固定表示に成功しました
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // セッションの先頭固定表示に失敗しました
        delete callback;
    });

V2TIMManager::GetInstance()->GetConversationManager()->PinConversation(conversationID, isPinned, callback);
```
:::
</dx-tabs>

## セッションの先頭固定表示の変更通知
事前に`addConversationListener`([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMConversationManager.html#adb2c20ca824cac69d0703169f3a025a1))を呼び出してセッション監視装置（リスナー）を追加すると、`onConversationChanged`から`V2TIMConversation`オブジェクトの`isPinned`フィールドを取得できます。このフィールドによって、セッションの先頭固定表示状態が変化したかどうかを判断できます。

サンプルコードは次のとおりです：
<dx-tabs>
::: Android
```java
public void onConversationChanged(List<V2TIMConversation> conversationList) {
    // セッションメッセージの変更通知を受信しました
    Log.i("imsdk", "onConversationChanged");
}
```
:::
::: iOS & Mac
```objectivec
- (void)onConversationChanged:(NSArray<V2TIMConversation*> *) conversationList {
    for (V2TIMConversation *conv in conversationList) {
        if ([conv.conversationID isEqualToString:self.conversationData.conversationID]) {
            // conv.isPinnedはセッションの先頭固定表示状態です
        }
    }
}
```
:::
::: Windows
```cpp
class ConversationListener final : public V2TIMConversationListener {
public:
    void OnConversationChanged(const V2TIMConversationVector& conversationList) override {
        // セッションメッセージの変更通知を受信しました
    }
    // その他のメンバー...
};

// セッションイベントリスナーを追加します。イベントコールバックを受信できないことを避けるために、リスナーを削除する前に、conversationListenerの有効期間を維持する必要があることに注意してください。
ConversationListener conversationListener;
V2TIMManager::GetInstance()->GetConversationManager()->AddConversationListener(&conversationListener);
```
:::
</dx-tabs>
