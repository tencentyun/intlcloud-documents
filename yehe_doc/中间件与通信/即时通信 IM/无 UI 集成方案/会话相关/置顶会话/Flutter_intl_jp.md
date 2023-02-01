## 機能説明
セッションのピン留めとは、友達との関連セッションやグループセッションをセッションリストの一番上に固定することです。これにより、ユーザーがセッションを見つけやすくなります。ピン留めステータスはサーバーに保存されます。端末を切り替えると、ピン留めステータスが新しい端末に同期されます。

>!ピン留めするセッションの最大数は50で、増加はサポートされていません。

## セッションのピン留め
`pinConversation`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/pinConversation.html))インターフェースを呼び出すことで、セッションをピン留めするかどうかを設定できます。

セッションの順序は、`V2TimConversation`オブジェクトの`orderKey`フィールドによって並べ替えられます。`orderKey`フィールドは整数型です。新しいメッセージを送信・受信したり、下書きを設定したり、またはセッションをピン留めしたりする場合、セッションが有効になり、`orderKey`フィールドの値が増加します。

ピン留めされたセッションは、ピン留めされていないセッションの前に常に並べ替えられることに注意してください。複数のセッションが同時にピン留めされている場合でも、これらのセッション間の相対的な順序は維持されます。たとえば、5つの連続したセッション1、2、3、4、5があるとします。同時にセッション2とセッション3をピン留めし、ピン留め後の順序は2、3、1、4、5です。明らかに、セッション2とセッション3は一番上に並べ替えられ、セッション2は依然としてセッション3の上にあります。

`getConversationList`を呼び出してセッションリストを取得すると、このインターフェースは先にピン留めされたセッションを返し、次にピン留めされていないセッションを返します。`V2TIMConversation`オブジェクトの`isPinned`フィールドを使用して、セッションがピン留めされているかどうかを確認できます。

サンプルコードは次のとおりです：


```dart
// isPinnedパラメータがtrueの場合は、セッションをピン留めすることを意味します。trueでない場合は、ピン留めをキャンセルすることを意味します。
bool isPinned = true;
conversationManager.pinConversation(conversationID: "conversationID", isPinned: isPinned);
```


## セッションのピン留めの変更通知
事前に`addConversationListener`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/addConversationListener.html))を呼び出してセッションリスナーを追加しておくと、`onConversationChanged`で`V2TimConversation`オブジェクトの`isPinned`フィールド値を取得できます。このフィールドによって、セッションのピン留めステータスが変化したかどうかを判断できます。
サンプルコードは次のとおりです：

```java
conversationManager.addConversationListener(listener: V2TimConversationListener(onConversationChanged: (conversationList) {
    // 変更後の最新セッション
  },));
```
