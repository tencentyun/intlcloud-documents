## 機能説明

セッションの先頭固定表示とは、ユーザーが簡単に見つけられるように、友達やグループのセッションをセッションリストの最上部に固定することを意味します。先頭固定表示の状態はサーバーに保存され、端末デバイスを切り替えると、先頭固定表示の状態が新しいデバイスに同期されます。
インターフェースが正常に呼び出されると、セッションリストが再度並べ替えられ、SDKがイベント[TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED)をディスパッチします。

>! v2.14.0からサポートします。先頭固定表示セッションの数の上限は50で、増やすことはできません。

## セッションの先頭固定表示および先頭固定表示解除

**インターフェース**

<dx-codeblock>
:::  js

tim.pinConversation(options);

:::
</dx-codeblock>

パラメータoptionsはObjectタイプ、含まれている属性値は次のとおりです：

**パラメータ**

| Name           | Type    | Description                                                  |
| -------------- | ------- | ------------------------------------------------------------ |
| conversationID | String  | セッション ID。セッションIDの構成方式：<br/><li>C2C${userID}（シングルチャット）</li><li>GROUP{groupID}（グループチャット）</li><li>@TIM#SYSTEM（システム通知セッション）</li><li>GROUP${topicID}（トピック) v2.19.1からサポート</li> |
| isPinned       | Boolean | trueはセッションの先頭固定表示を表し、falseはセッションの先頭固定表示解除を表します |

**戻り値**

`Promise`オブジェクト。

**事例**

<dx-codeblock>
:::  js

// セッションの先頭固定表示、v2.14.0からサポート
let promise = tim.pinConversation({ conversationID: 'C2CExample', isPinned: true });
promise.then(function(imResponse) {
  // セッションの先頭固定表示に成功しました
  const { conversationID } = imResponse.data; // 先頭固定表示されたセッションID
}).catch(function(imError) {
  console.warn('pinConversation error:', imError); // セッションの先頭固定表示に失敗する関連情報
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// セッションの先頭固定表示解除、v2.14.0からサポート
let promise = tim.pinConversation({ conversationID: 'C2CExample', isPinned: false });
promise.then(function(imResponse) {
  // セッションの先頭固定表示解除に成功しました
  const { conversationID } = imResponse.data; // 先頭固定表示が解除されたセッションID
}).catch(function(imError) {
  console.warn('pinConversation error:', imError); // セッションの先頭固定表示解除に失敗する関連情報
});

:::
</dx-codeblock>
